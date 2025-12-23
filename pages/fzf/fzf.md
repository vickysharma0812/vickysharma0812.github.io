---
title: "Getting started with fzf command"
tags: [fzf, cli, linux, unix]
summary: "This post describes the fzf  (fuzzy finder command line tool)"
date: 2024-03-25
authors: 
  - Vikas Sharma
---

## Introduction

`fzf` is a general purpose command-line fuzzy finder written in `go` programming language.
You can find it [here] ("https://github.com/junegunn/fzf"). The official website describes `fzf` as:

> It's an interactive Unix filter for command-line that can be used with any list; files, command history, processes, hostnames, bookmarks, git commits, etc.

## Getting started

If you run `fzf` without any argument then it will search all files in the current directory.

```bash
fzf
```

> Note that fzf updates the matches dynamically while you type the search terms in any order.

> Because fzf prints the selection into stdout, we can use this output as input for another command such as vim.

### Preview the file

We will use `bat` and `fzf` together.

```bash
fzf --preview 'bat --color=always {}'
```

### Configuration of fzf

To avoid typing this option every time, you can set the environment variable FZF_DEFAULT_OPTS to apply it automatically every time you run fzf:

```bash
export FZF_DEFAULT_OPTS="--preview 'bat --color~always {}'"
```

By default `fzf` uses `find` command, but we want to use `fd` command.

```bash
export FZF_DEFAULT_COMMAND="fd --type f"
```
