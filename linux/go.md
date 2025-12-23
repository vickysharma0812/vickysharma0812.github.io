---
title: 'Go lang'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [go, programming, setup]
summary: This note explains how to setup go programming language on ArchLinux.
---

[Go](https://go.dev/) is an open source programming language supported by Google. 

Install go by using following command. Install the go package, which includes the standard Go compiler and other development tools.

```bash
sudo pacman -S go
```

Configuration.

The go install command installs Go executables in the directory named by the `GOBIN` environment variable. `GOBIN` defaults to `$GOPATH/bin`, or `~/go/bin` if the `GOPATH` environment variable is not set. 

```bash
## GO related
set GOPATH $HOME/go
set PATH $PATH "$GOPATH/bin"
```

