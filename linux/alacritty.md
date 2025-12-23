---
title: 'Alacritty'
author: Vikas Sharma, Ph.D.
date: 2025-01-14
tags: [alacritty, terminal, setup]
summary: This note explains how to setup alacritty on archlinux machine.
---

[Alacritty](https://alacritty.org/index.html) is a modern terminal emulator that comes with sensible defaults, but allows for extensive configuration. By integrating with other applications, rather than reimplementing their functionality, it manages to provide a flexible set of features with high performance. The supported platforms currently consist of BSD, Linux, macOS and Windows. 

To install alacritty on archlinux, run the following command:

```bash
sudo pacman -S alacritty
```

The configuration file for `alacrittiy` is located at `~/.config/alacritty/alacritty.toml`.

```bash
[general]

import = [ "./themes/tokyo-night.toml" ]

[env]
TERM = "xterm-256color"

[font]
builtin_box_drawing = true
size = 16.0

[font.bold]
family = "FiraCode Nerd Font Mono"
style = "Bold"

[font.bold_italic]
family = "FiraCode Nerd Font Mono"
style = "Bold Italic"

[font.italic]
family = "FiraCode Nerd Font Mono"
style = "Italic"

[font.normal]
family = "FiraCode Nerd Font Mono"
style = "Regular"

[[keyboard.bindings]]
action = "Paste"
key = "V"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "Copy"
key = "C"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "PasteSelection"
key = "Insert"
mods = "Shift"

[[keyboard.bindings]]
action = "ToggleFullscreen"
key = "F11"
mods = "None"

[[keyboard.bindings]]
action = "Paste"
key = "Paste"
mods = "None"

[[keyboard.bindings]]
action = "Copy"
key = "Copy"
mods = "None"

[[keyboard.bindings]]
action = "ClearLogNotice"
key = "L"
mods = "Control"

[[keyboard.bindings]]
chars = "\f"
key = "L"
mods = "Control"

[[keyboard.bindings]]
action = "ScrollPageUp"
key = "PageUp"
mode = "~Alt"
mods = "None"

[[keyboard.bindings]]
action = "ScrollPageDown"
key = "PageDown"
mode = "~Alt"
mods = "None"

[[keyboard.bindings]]
action = "ScrollToTop"
key = "Home"
mode = "~Alt"
mods = "Shift"

[[keyboard.bindings]]
action = "ScrollToBottom"
key = "End"
mode = "~Alt"
mods = "Shift"

[[keyboard.bindings]]
action = "CreateNewWindow"
key = "Return"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "SpawnNewInstance"
key = "N"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "IncreaseFontSize"
key = "Plus"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "IncreaseFontSize"
key = "Semicolon"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "DecreaseFontSize"
key = "NumpadSubtract"
mods = "Control"

[[keyboard.bindings]]
action = "DecreaseFontSize"
key = "Equals"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "ResetFontSize"
key = "Key0"
mods = "Control|Shift"

[[keyboard.bindings]]
action = "ToggleViMode"
key = "Space"
mode = "~Search"
mods = "Shift|Control"

[[keyboard.bindings]]
action = "ScrollToBottom"
key = "Space"
mode = "Vi|~Search"
mods = "Shift|Control"

[[keyboard.bindings]]
action = "ToggleViMode"
key = "I"
mode = "Vi|~Search"

[[keyboard.bindings]]
action = "ClearSelection"
key = "Escape"
mode = "Vi|~Search"

[[keyboard.bindings]]
action = "ScrollToBottom"
key = "G"
mode = "Vi|~Search"

[scrolling]
history = 5000

[window]
decorations = "full"
dynamic_padding = false
dynamic_title = true
opacity = 1.0
# option_as_alt = "Both"
title = "Alacritty"

[window.class]
general = "Alacritty"
instance = "Alacritty"

[window.padding]
x = 0
y = 0
```



