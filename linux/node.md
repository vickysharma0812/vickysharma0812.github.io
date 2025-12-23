---
title: Node
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [node, npm, javascript, setup]
summary: This note explains how to setup node on archlinux machine.
---

Node.js is a JavaScript runtime environment combined with useful libraries. It uses Google's V8 engine to execute code outside of the browser. Due to its event-driven, non-blocking I/O model, it is suitable for real-time web applications. 

```bash
sudo pacman -S nodejs
```

Check the version.

```bash
node -v
```

## Installing node version manager

`nvm` allows you to quickly install and use different versions of node via the command line.

To install or update nvm, you should run the install script. To do that, you may either download and run the script manually, or use the following cURL or Wget command:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to 
`~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`)

Read more about nvm on the official website `https://github.com/nvm-sh/nvmhttps://github.com/nvm-sh/nvm`. 

## Installing package manager

[npm](https://www.npmjs.com) is the official package manager for node.js. It can be installed with the npm package. 

```bash
sudo pacman -S npm
```

We  will also install [pnpm](https://pnpm.io/), which is  fast and disk space  efficient package manager.

```bash
sudo pacman -S pnpm
```

We want to install packages locally. I use `fish` shell, so I have  added following lines to `fishconfig`.

```bash 
# installing npm packages locally
set -gx NPM_CONFIG_PREFIX "$HOME/.npm-packages"
set -gx NPM_PACKAGES "$HOME/.npm-packages"
set -gx NODE_PATH "$NPM_PACKAGES/lib/node_modules" $NODE_PATH
set PATH $PATH $NPM_PACKAGES/bin
set MANPATH $NPM_PACKAGES/share/man $MANPATH

# from pnpm setup
# Next configuration changes were made:
set -gx PNPM_HOME "$HOME/.local/share/pnpm"
if not string match -q -- $PNPM_HOME $PATH
    set -gx PATH "$PNPM_HOME" $PATH
end
```

