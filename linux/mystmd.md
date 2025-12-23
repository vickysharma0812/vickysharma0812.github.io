---
title: 'MyST'
author: Vikas Sharma, Ph.D.
date: 2025-01-13
tags: [SSH, linux-server]
summary: This note explains how to setup MyST on archlinux machine.
---

MyST is an ecosystem of open-source, community-driven tools designed to revolutionize scientific communication. Our powerful authoring framework supports blogs, online books, scientific papers, reports and journals articles.

You can read more about it on [official site](https://mystmd.org)

We will install myst command line interface by using node. Therefore, first install
node on your system.

:::{card} 
:link: ./node.md
Click here to read instruction for installing node.
:::

```bash
npm install -g mystmd
```

Check myst version by 

```bash
myst --version
```
