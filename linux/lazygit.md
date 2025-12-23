---
title: 'Lazygit'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [git, lazygit, setup]
summary: This note explains how to setup lazygit application on ArchLinux.
---

[Lazygit](https://github.com/jesseduffield/lazygit) is a terminal application for git. You can download it by using the following command.

```bash
sudo pacman -S lazygit
```

## Configuration

```bash
mkdir -p ~/.config/lazygit
cd ~/.config/lazygit
touch config.yml
```

Contents of config.yml

```yml
# yaml-language-server: $schema=https://raw.githubusercontent.com/jesseduffield/lazygit/master/schema/config.json
gui:
  nerdFontsVersion: "3"
  showIcons: true
  showFileTree: true
  scrollHeight: 10
  scrollPastBottom: true
  mouseEvents: true
  skipDiscardChangeWarning: false
  skipStashWarning: true
  sidePanelWidth: 0.3333
  expandFocusedSidePanel: false
  mainPanelSplitMode: flexible
  theme:
    activeBorderColor:
      - "#89ddff"
      - bold
    inactiveBorderColor:
      - "#565f89"
    optionsTextColor:
      - "#3d59a1"
    selectedLineBgColor:
      - "#292e42"
      - bold
  commitLength:
    show: true
  skipNoStagedFilesWarning: false
```
