---
title: Getting started with Jujutsu (jj)
date: 2026-11-06
summary: This post shows how to install and work with jujutsu.
authors:
- Vikas Sharma
tags:
- jujutsu
- git
- cli
---

## Getting Started with JJ

`JJ` stands for Jujutsu, located at <https://www.jj-vcs.dev/latest/>, it is a
version control system. We will manage git using JJ.

Jujutsu is a DVCS, or "distributed version control system"
(<https://steveklabnik.github.io>). It also has a quality that's pretty rare in
programming: it's both simpler and easier to use than Git, yet more powerful.

Why do I use `jj` for maintaining easifem.

- Stable, tool-agnostic, Linux-first. It’s a general VCS with a large community.
- It doesn’t depend on a vendor’s app.
- Colocated mode keeps my existing git setup.
- `jj git init --colocate` sits on top of my existing `.git`, so GitHub, CI and FORD docs stay the same. If you don’t like it, delete `.jj` and you’re back to plain git.
- Auto-snapshots suit agent work. Every edit Claude makes is recorded in the working-copy change. jj op log / jj undo can roll back anything, including a bad refactor across many .F90 files.
- No staging area. Splitting Claude’s large diffs afterwards (jj split, jj squash -i) is easy.

## jj (Jujutsu) — Getting Started

### Mental model

- **The working copy is a commit (`@`).** jj snapshots your files into `@` automatically. There is no `git add` and no staging area.
- **Change IDs** (e.g. `kwwmurpv`) stay the same when a change is rewritten. Type only the first 2–4 letters.
- **Bookmarks = branches, but they don't move on their own.** After committing, move the bookmark yourself.
- **Everything is undoable:** `jj undo`, `jj op log`.
- Revision shorthands: `@` = working copy, `@-` = parent, `@--` = grandparent.
- In `jj log`, `◆` marks an immutable (pushed) commit.

### Install (CachyOS)

``` sh
sudo pacman -S jujutsu
jj --version
```

### User config

`jj config edit --user` opens `~/.config/jj/config.toml`:

```toml
[user]
name = "Vikas"
email = "vickysharma0812@gmail.com"

[ui]
editor = "helix"
default-command = "log"          # plain `jj` shows the log
diff-editor = ":builtin"         # TUI for jj split / squash -i / commit -i

[snapshot]
max-new-file-size = "10MiB"      # default 1MiB

[revset-aliases]
# never rewrite anything already pushed
"immutable_heads()" = "builtin_immutable_heads() | remote_bookmarks()"

[aliases]
# move the nearest bookmark up to @-
tug = ["bookmark", "move", "--from", "heads(::@- & bookmarks())", "--to", "@-"]
```

Shell completion:

```sh
echo 'COMPLETE=fish jj | source' >> ~/.config/fish/config.fish   # fish
echo 'source <(COMPLETE=zsh jj)' >> ~/.zshrc                      # zsh
```

## Set up a repo

### Existing git repo (e.g. easifemBase)

```sh
git status                     # commit/stash pending work first
jj git init --colocate         # keeps .git; remove .jj to go back
jj git fetch
jj bookmark track main@origin dev@origin vikas-dev@origin
jj new vikas-dev
```

### New repo (nothing committed, e.g. a Zig project)

```sh
jj git init --colocate
# .gitignore first:  .zig-cache/  zig-out/
jj st
jj commit -m "initial commit"
jj bookmark create main -r @-
jj bookmark create dev -r main      # local branch, no push needed
jj new dev
```

Push later:

```sh
jj git remote add origin git@github.com:<you>/<repo>.git
jj git push -b main      # first push of a new bookmark: follow jj's hint
                         # (--allow-new or jj bookmark track main@origin)
```

Make sure `.gitignore` covers build output (Fortran: `build/`, `*.mod`, `*.smod`, `*.o`, `*.a`, `*.so`), because jj tracks every file that isn't ignored. In a colocated repo, git reporting "detached HEAD" is normal.

### Looking around

```sh
jj                     # log
jj st                  # status of @
jj diff                # diff of @
jj show kw             # show a change
jj log -r 'vikas-dev@origin..vikas-dev'   # what will be pushed
```

### Committing

```sh
jj commit -m "message"               # describe @ + start new empty @
jj commit path/ -m "message"         # only these paths
jj commit -i -m "message"            # pick hunks interactively
```

`describe` only changes a message:

```sh
jj describe -m "msg"                 # @
jj describe -r @- -m "fix typo"      # previous commit
jj new dev -m "add tokenizer"        # describe-first style: start with a message
```

`jj describe -m` followed by `jj new` is the same as `jj commit -m`.

### Fixing history

| Task                           | Command                                   |
| ------------------------------ | ----------------------------------------- |
| Fold `@` into its parent       | `jj squash`                               |
| Fold only some hunks           | `jj squash -i`                            |
| Split a change                 | `jj split`                                |
| Edit an older change           | `jj edit kw` (descendants auto-rebase)    |
| Insert a change before another | `jj new -B kw`                            |
| Discard a change               | `jj abandon kw`                           |
| Restore a file in `@`          | `jj restore path/file.F90`                |
| Rebase change(s)               | `jj rebase -s kw -d vikas-dev`            |
| Undo last operation            | `jj undo`                                 |
| Restore whole repo state       | `jj op log`, then `jj op restore <op-id>` |

Conflicts don't stop a rebase. Resolve them later with `jj new <conflicted>`, edit the files, then `jj squash` (or use `jj resolve`).

## easifem workflow (main → dev → vikas-dev)

**1. Work and commit**

```sh
jj new vikas-dev -m "feat: ..."
# edit / Claude Code
jj commit -m "..."                   # repeat as needed
```

**2. Move the bookmark and push**

```sh
jj tug                               # or: jj bookmark set vikas-dev -r @-
jj git push -b vikas-dev
```

**3. PR into dev (GitHub CLI)**

``` sh
gh pr create --base dev --head vikas-dev --title "..." --body "..."
gh pr merge vikas-dev --merge        # never --delete-branch
```

**4. Release (every ~4 months)**

``` sh
gh pr create --base main --head dev --title "Release vX.Y.Z"
gh pr merge dev --merge
```

**5. Sync and start again**

``` sh
jj git fetch
jj bookmark set vikas-dev -r dev     # fast-forward
jj git push -b vikas-dev
jj new vikas-dev
```

Bring in coworkers' work from `dev` mid-cycle (merge, don't rebase pushed work):

``` sh
jj git fetch
jj new vikas-dev dev -m "Merge dev into vikas-dev"
jj bookmark set vikas-dev -r @
jj git push -b vikas-dev
```

## Gotchas

- **`jj tug` says "No bookmarks to update".** The local bookmark isn't below your commits. Set it directly:
  `jj bookmark set vikas-dev -r <id> --allow-backwards`.
  This is safe if `<id>` builds on `vikas-dev@origin`, because the push is still a fast-forward.
- **`gh pr create` can't detect the branch.** Always pass `--head <bookmark>`, since git is on a detached HEAD.
- **`gh pr merge --delete-branch`.** Avoid it: it deletes the branch and runs git checkout/pull behind jj's back.
- **Tags:** create them through a GitHub release, or with `git tag vX.Y.Z main && git push origin vX.Y.Z`.
- **Pushed commits are immutable** (per the config above). To change them, add a new commit instead.

## CLAUDE.md snippet

``` text
This repo uses jj (colocated with git).
- Use jj for all writes: jj new, jj describe, jj squash, jj split, jj bookmark, jj git push.
- git is read-only (git log/diff/blame OK). Never run git commit/checkout/switch/rebase/reset/stash/merge.
- Do not move bookmarks or push unless asked.
```

## Cheat sheet

| git                          | jj                                                              |
| ---------------------------- | --------------------------------------------------------------- |
| `git status`                 | `jj st`                                                         |
| `git status`                 | `jj diff`                                                       |
| `git status`                 | `jj diff --stat`                                                |
| `git status`                 | `jj diff --summary`                                             |
| `git add . && git commit -m` | `jj commit -m`                                                  |
| `git commit --amend`         | edit files, then `jj squash` (or `jj describe` for the message) |
| `git switch -c feat dev`     | `jj new dev -m "..."`                                           |
| `git branch -f dev X`        | `jj bookmark set dev -r X`                                      |
| `git fetch`                  | `jj git fetch`                                                  |
| `git push origin dev`        | `jj git push -b dev`                                            |
| `git rebase -i`              | `jj squash` / `split` / `edit` / `rebase`                       |
| `git stash`                  | `jj new @-` (old `@` stays as a change)                         |
| `git reflog` / undo          | `jj op log` / `jj undo`                                         |
