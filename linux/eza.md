---
title: 'EZA'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [eza, exa, ls, rust, rust-app, utility, cli]
summary: This note explains how to setup EZA on archlinux machine.
---

`eza` is a modern replacement for lsa. Official website is given [here](https://github.com/eza-community/eza).

```bash
sudo pacman -S eza
```

```bash
if type -q eza
    set fzf_preview_dir_cmd eza --all --color=always
end

if type -q eza
    alias exa="eza --long --header --icons --git --sort=size"
end
```
