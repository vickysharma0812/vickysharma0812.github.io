---
title: "Getting started with conda"
tags: [Python, Conda]
summary: This note discusses the key points of conda package manager.
author: Vikas Sharma
date: "07/17/2023"
categories: [programming, python]
---

Conda is a package manager and environment manager.

```bash
which conda
conda --version
```

## Installing conda

Please follow the instruction given [here](https://conda.io/projects/conda/en/latest/user-guide/install/index.html).

## Updating conda

```bash
conda update conda
```

## Creating environment

```bash
conda create -n easifem 
```

or

```bash
conda create --name easifem 
```

> Here, `easifem` is the name of virtual environment.

Then we can activate the environment by

```bash
conda activate easifem
```

To get list of all environment:

```bash
conda info --envs
```

We can create an environment with specific python:

```bash
conda create --name easifem_py39 python=3.9
```

## Searching packages

```bash
conda search easifem
```

## Installing packages

```bash
conda install easifem
```

We can check the installed packages by

```bash
conda list
```
