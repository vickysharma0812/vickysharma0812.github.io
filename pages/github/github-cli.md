---
title: Getting started with Github CLI
date: 2023-11-04
summary: This post shows how to create an issue in Github using gh-cli
authors:
  - Vikas Sharma
tags:
  - cli
  - github
---

To install `gh` cli please follow the instruction given on official [website](https://cli.github.com/manual/) of gh.

To create an issue we will use the following command.

```bash
gh issue
```

This command has many options:

```bash
Work with GitHub issues.

USAGE
  gh issue <command> [flags]

GENERAL COMMANDS
  create:      Create a new issue
  list:        List issues in a repository
  status:      Show status of relevant issues

TARGETED COMMANDS
  close:       Close issue
  comment:     Add a comment to an issue
  delete:      Delete issue
  develop:     Manage linked branches for an issue
  edit:        Edit issues
  lock:        Lock issue conversation
  pin:         Pin a issue
  reopen:      Reopen issue
  transfer:    Transfer issue to another repository
  unlock:      Unlock issue conversation
  unpin:       Unpin a issue
  view:        View an issue

FLAGS
  -R, --repo [HOST/]OWNER/REPO   Select another repository using the [HOST/]OWNER/REPO format

INHERITED FLAGS
  --help   Show help for command

ARGUMENTS
  An issue can be supplied as argument in any of the following formats:
  - by number, e.g. "123"; or
  - by URL, e.g. "https://github.com/OWNER/REPO/issues/123".

EXAMPLES
  $ gh issue list
  $ gh issue create --label bug
  $ gh issue view 123 --web

LEARN MORE
  Use 'gh <command> <subcommand> --help' for more information about a command.
  Read the manual at https://cli.github.com/manual
```

We will only focus here on `gh issue create`

```bash
USAGE
  gh issue create [flags]

FLAGS
  -a, --assignee login   Assign people by their login. Use "@me" to self-assign.
  -b, --body string      Supply a body. Will prompt for one otherwise.
  -F, --body-file file   Read body text from file (use "-" to read from standard input)
  -l, --label name       Add labels by name
  -m, --milestone name   Add the issue to a milestone by name
  -p, --project name     Add the issue to projects by name
      --recover string   Recover input from a failed run of create
  -T, --template name    Template name to use as starting body text
  -t, --title string     Supply a title. Will prompt for one otherwise.
  -w, --web              Open the browser to create an issue

INHERITED FLAGS
      --help                     Show help for command
  -R, --repo [HOST/]OWNER/REPO   Select another repository using the [HOST/]OWNER/REPO format

EXAMPLES
  $ gh issue create --title "I found a bug" --body "Nothing works"
  $ gh issue create --label "bug,help wanted"
  $ gh issue create --label bug --label "help wanted"
  $ gh issue create --assignee monalisa,hubot
  $ gh issue create --assignee "@me"
  $ gh issue create --project "Roadmap"

LEARN MORE
  Use 'gh <command> <subcommand> --help' for more information about a command.
  Read the manual at https://cli.github.com/manual
```
