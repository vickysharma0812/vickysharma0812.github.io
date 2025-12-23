---
title: 'Docusaurus'
author: Vikas Sharma, Ph.D.
date: 2025-01-14
tags: [docs, docusaurus, fonts, setup]
summary: This note explains how to setup fonts on archlinux machine.
---

Docusaurus will help you ship a beautiful documentation site in no time.

To preview your changes as you edit the files, you can run a local development server that will serve your website and reflect the latest changes.

```bash
cd my-website
pnpm run start
```

Docusaurus is a modern static website generator so we need to build the website into a directory of static contents and put it on a web server so that it can be viewed. To build the website:

```bash
pnpm run build
```

There are many ways to update your Docusaurus version. One guaranteed way is to manually change the version number in package.json to the desired version. Note that all `@docusaurus/-namespaced` packages should be using the same version.

```bash
# package.json
{
  "dependencies": {
    "@docusaurus/core": "3.7.0",
    "@docusaurus/preset-classic": "3.7.0",
    // ...
  }
}
```

Then, in the directory containing package.json, run your package manager's install command:

```bash
pnpm install
```
