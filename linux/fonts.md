---
title: 'Fonts'
author: Vikas Sharma, Ph.D.
date: 2025-01-14
tags: [fonts, setup]
summary: This note explains how to setup fonts on archlinux machine.
---

To install all nerd fonts use the following.

```bash
sudo pacman -S nerd-fonts
```

To  install a specific fonts,  go the nerd-font [website](https://www.nerdfonts.com/)  and download the font.

unpack the font archive.

```bash
tar -xzvf xxx.tar.gz
```

On Linux systems, font binaries are generally installed in either the system font directory on the path 

- `/usr/share/fonts/` 

or in a user font directory that is frequently on one of the following paths: 

- `~/.local/share/fonts/`
- `/usr/local/share/fonts`. 

We’ll use the `~/.local/share/fonts/` path in this example. If the directory does not exist, create it.

Move your font binaries to the destination directory with `mv`.

Next, clear and regenerate your font cache with the following command:

```bash
fc-cache -f -v
```

Confirm that the fonts are installed by displaying the paths and style definitions with the fc-list executable filtered on the font family name with grepConfirm that the fonts are installed by displaying the paths and style definitions with the fc-list executable filtered on the font family name with grep.

```bash
fc-list | grep "Hack"
```