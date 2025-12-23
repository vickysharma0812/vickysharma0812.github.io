---
title: "Getting started with tmux"
tags: [tmux, cli]
summary: This post covers the basic introduction to tmux configuration.
date: 2023-08-14
authors:
  - Vikas Sharma
---

This post covers `tmux` setup on MacOS and Linux.

## Environment

- Terminal: Alacritty
- Shell: Fish
- OS: ArchLinux, Ubuntu 22.04, MacOSX (M2 chip), MacOSX (Intel chip)

## Installing tmux

On MacOSX:

```bash
brew install tmux
```

On ArchLinux:

```bash
sudo pacman -S tmux
```

On Ubuntu:

```bash
sudo apt-get install -y tmux
```

## Installing Tmux package manager

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

## Configuration settings:

```bash
mkdir -pv ~/.config/tmux
touch ~/.config/tmux/tmux.conf
```

Open `tmux.conf`, and add following lines to it:

```bash
set -g default-terminal "tmux-256color"
# set -ga terminal-overrides ",*256col*:Tc"
set -ga terminal-overrides ",xterm-256color:Tc"
set -ga terminal-overrides '*:Ss=\E[%p1%d q:Se=\E[ q'
set-environment -g COLORTERM "truecolor"


## Mouse enable
set -g mouse on

## windows indexing

set -g base-index 1
set -g pane-base-index 1
set-window-option -g pane-base-index 1
set-option -g renumber-windows on


## My kemaps

### Prefix

unbind C-b
set -g prefix C-a
bind C-a send-prefix

### Reload config file

### Windows related

bind r source ~/.config/tmux/tmux.conf

bind < previous-window
bind > next-window

### Pane related

bind '"' split-window -v -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
bind Enter split-window -h -c "#{pane_current_path}"


# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'catppuccin/tmux'
set -g @catppuccin_flavour 'mocha' # or frappe, macchiato, mocha

## This plugin is a repackaging of Mislav Marohnić's tmux-navigator configuration
## described in this gist. When combined with a set of tmux key bindings,
## the plugin will allow you to navigate seamlessly between vim and tmux splits
## using a consistent set of hotkeys.
## https://github.com/christoomey/vim-tmux-navigator

set -g @plugin 'christoomey/vim-tmux-navigator'
run '~/.tmux/plugins/tpm/tpm'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

## Tmux keybindings

### Panes

| Key     | Action               |
| ------- | -------------------- |
| `Enter` | Horizonal split      |
| `%`     | Horizonal split      |
| `"`     | Vertical split       |
| `x`     | Close the pane       |
| `Right` | Go to the right pane |
| `Left`  | Go to the left pane  |
| `Top`   | Go to the top pane   |
| `Down`  | Go to the down pane  |
| `z`     | Zoom the pane        |
| `q`     | Show pane number     |
| `q+1`   | Goto pane 2          |

### Windows

| Key         | Action                    |
| ----------- | ------------------------- |
| `c`         | Create new window         |
| `,`         | Rename window             |
| `>`         | Go to next window         |
| `<`         | Go to previous window     |
| `&`         | Close window              |
| `w`         | List windows              |
| `p`         | Go to previous window     |
| `n`         | Go to next window         |
| `1, 2, ...` | Go to window 1, 2,        |
| `l`         | Toggle last active window |

### Sessions

Start new session.

```base
tmux new
```

```bash
:new
```

Start new session with a name `hello_world`.

```bash
tmux new -s hello_world
```

```bash
:new -s hello_world
```

Kill a session

```bash
tmux kill-session -t hello_world
```

Kill all session but the current:

```bash
tmux kill-session -a
```

Kill all session but `hello_world`

```bash
tmux kill-session -a -t hello_world
```

Rename the Session

```bash
<prefix> + $
```

Detach from session.

```bash
<prefix> + d
```

or,

```bash
:attach -d
```

List all session:

```bash
tmux ls
```

Show all session:

```bash
<prefix> + s
```

Attach to a Session:

```bash
tmux a -t hello_world
tmux attach -t hello_world
tmux attach-session -t hello_world
```

Go to the next session

```bash
<prefix> + )
```

Go to the previous session

```bash
<prefix> + (
```
