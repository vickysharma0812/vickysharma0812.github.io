---
title: 'Zoxide'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [zoxide, rust, rust-app, utility, cli]
summary: This note explains how to setup zoxide on archlinux machine.
---

`zoxide` is a smarter cd command, inspired by z and autojump. It remembers which directories you use most frequently, so you can "jump" to them in just a few keystrokes.
`zoxide` works on all major shells.

To install zoxide 

```bash
sudo pacman -S zoxide
```

fish configuration.

```bash
if type -q zoxide
    zoxide init fish | source
end
```