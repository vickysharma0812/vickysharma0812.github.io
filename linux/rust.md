---
title: 'Rust'
author: Vikas Sharma, Ph.D.
date: 2025-01-14
tags: [rust, cargo, setup]
summary: This note explains how to setup rust environment on archlinux machine.
---

Rust is a multi-paradigm, general-purpose programming language that emphasizes performance, type safety, and concurrency.

To install rust use the following command.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Set the path in fish config.

```bash
set PATH $PATH "$HOME/.cargo/bin"
set PATH $PATH "$HOME/.local/bin"
```
