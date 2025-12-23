---
title: 'FZF'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [fzf, shell, fish, setup]
summary: This note explains how to setup fzf on ArchLinux.
---

[fzf](https://github.com/junegunn/fzf) is a general-purpose command-line fuzzy finder.

It's an interactive filter program for any kind of list; files, command history, processes, hostnames, bookmarks, git commits, etc. It implements a "fuzzy" matching algorithm, so you can quickly type in patterns with omitted characters and still get the results you want.It's an interactive filter program for any kind of list; files, command history, processes, hostnames, bookmarks, git commits, etc. It implements a "fuzzy" matching algorithm, so you can quickly type in patterns with omitted characters and still get the results you want.

To install  it use the following command.

```bash
sudo pacman -S  fzf
```

Add following to `config.fish`

```bash
# Set up fzf key bindings
fzf --fish | source
# https://github.com/PatrickF1/fzf.fish
fzf_configure_bindings
```
