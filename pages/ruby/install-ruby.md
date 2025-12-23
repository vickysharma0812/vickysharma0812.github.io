---
title: "Installing Ruby on Mac"
tags: [ruby, jekyll, macOS]
summary: This post describe the process of Ruby on MacOS.
authors:
  - Vikas Sharma
date: 2023-07-29
---

In this post I will demonstrate how to install ruby 3.1.3 on MacOS. I am currently using M2 chip.

```bash
neofetch
                    'c.          easifem@Vikass-MacBook-Pro.local
                 ,xNMM.          --------------------------------
               .OMMMMo           OS: macOS 13.4.1 22F82 arm64
               OMMM0,            Host: Mac14,7
     .;loddo:' loolloddol;.      Kernel: 22.5.0
   cKMMMMMMMMMMNWMMMMMMMMMM0:    Uptime: 8 days, 12 hours, 25 mins
 .KMMMMMMMMMMMMMMMMMMMMMMMWd.    Packages: 116 (brew)
 XMMMMMMMMMMMMMMMMMMMMMMMX.      Shell: fish 3.6.1
;MMMMMMMMMMMMMMMMMMMMMMMM:       Resolution: 1440x900
:MMMMMMMMMMMMMMMMMMMMMMMM:       DE: Aqua
.MMMMMMMMMMMMMMMMMMMMMMMMX.      WM: Quartz Compositor
 kMMMMMMMMMMMMMMMMMMMMMMMMWd.    WM Theme: Blue (Dark)
 .XMMMMMMMMMMMMMMMMMMMMMMMMMMk   Terminal: WarpTerminal
  .XMMMMMMMMMMMMMMMMMMMMMMMMK.   CPU: Apple M2
    kMMMMMMMMMMMMMMMMMMMMMMd     GPU: Apple M2
     ;KMMMMMMMWXXWMMMMMMMk.      Memory: 2591MiB / 16384MiB
       .cooc,.    .,coo:.
```

I use Jekyll to manage this website. Recently, I have shifted to M2 chip. When I tried to install `ruby:3.1.3` by using chruby and ruby-install package (as recommended by [Jekyll website](https://jekyllrb.com/docs/installation/macos/)), I faced some difficulties which lead to ultimate failed installation.

So, I followed different approach, which works very smoothly and quickly.

I use [rbenv](https://github.com/rbenv/rbenv) to manage ruby version on MacOS, which is located here.

#### Installing rbenv

```bash
brew install rbenv ruby-build
```

Then please run the following command, and follow the instruction.

```bash
# run this and follow the printed instructions:
rbenv init
```

I use `fish` shell, which gives me following instruction.

```bash
# Load rbenv automatically by appending
# the following to ~/.config/fish/config.fish:

status --is-interactive; and rbenv init - fish | source
```

#### Installing Ruby version

The `rbenv` install command does not ship with rbenv out-of-the-box, but is provided by the ruby-build plugin.

Before attempting to install Ruby, check that your build environment has the necessary tools and libraries. Then:

```bash
# list latest stable versions:
rbenv install -l

# list all local versions:
rbenv install -L

# install a Ruby version:
rbenv install 3.1.3
```

Set a Ruby version to finish installation and start using Ruby:

```bash
rbenv global 3.1.3   # set the default Ruby version for this machine
rbenv local 3.1.3   # set the Ruby version for this directory
```

I do not want to set Ruby globally, therefore, I use the second command.

Now go to the directory which contains your Ruby project. Then activate ruby to 3.1.3 by using

```bash
rbenv local 3.1.3
```

Then, we install jekyll.

```bash
gem install jekyll bundler
```

Then, build the site and make it available on a local server.

```bash
bundle install
bundle exec jekyll serve
```
