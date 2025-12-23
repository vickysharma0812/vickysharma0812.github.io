---
title: "Building and Deploying PyPI packages"
tags: [python, pypi]
summary: This note explains about how to build a PyPI package and deploy it to pypi.org.
date: 2023-07-15
authors:
  - Vikas Sharma
---

In this tutorial, we will build a Python package for easifem command line interface (easifem-CLI).

In case of Python there are several tools available for publishing our open source packages. For example, we can use the Python Package Index, also known as PyPI. We will be using PyPI for this tutorial.

First of all we need to make an account at

- [test.pypo.org](https://test.pypi.org/account/register/)
- [pypi.org](https://pypi.org/account/register/)

> Both test.pypi.org and pypi.org require you to verify your email address. You will not be able to publish a package without confirming. Later steps in this tutorial require that the usernames and passwords for test.pypi.org and pypi.org are similar.

## Creating a Python package

I have created a command line interface for building, installing, uninstalling [easifem](https://www.easifem.com) components.

By using this CLI application we can install easifem as follows:

```bash
easifem install easifem
easifem update easifem
easifem clean easifem
easifem remove easifem
easifem uninstall easifem
```

## Project structure

```bash
├── LICENSE.txt
├── README.md
├── pyproject.toml
├── src
│   └── easifem
│       ├── __about__.py
│       ├── __init__.py
│       ├── __pycache__
│       ├── clean.py
│       ├── cmake.py
│       ├── components.py
│       ├── console.py
│       ├── easifem.py
│       ├── install.py
│       ├── parsers.py
│       ├── run.py
│       ├── setenv.py
│       ├── test.py
│       ├── uninstall.py
│       ├── utils_clean.py
│       ├── utils_install.py
│       ├── utils_run.py
│       ├── utils_setenv.py
│       └── utils_uninstall.py
└── tests
    ├── __init__.py
    ├── hello.F90
    ├── hello.md
    ├── test2.F90
    └── test2.md
```

The project has:

- A base folder named easifem-cli
- A module/library folder named easifem in src folder
- easifem folder contains several python files.

> Make sure that the module/library folder name is a unique name that is not used by an existing package in the Test Python Package Index test.pypi.org or the Python Package Index pypi.org. Make search queries to confirm the availability of the names you want to use.

In easifem directory create two files:

- `__init__.py`, keep this file empty.
- `__about__.py`, put the following lines in this file.

```python
__version__ = "23.6.0"
```

In the easifem directory `easifem.py` is the main file. Its contents are shown below:

```python
#!/usr/bin/env python3

import argparse
from easifem.utils_run import easifem_run as run
from easifem.utils_setenv import easifem_setenv as setenv
from easifem.utils_install import easifem_install as install
from easifem.utils_clean import easifem_clean as clean
from easifem.utils_uninstall import easifem_uninstall as uninstall
from easifem.parsers import *
import os

_DESCRIPTION = """
easifem is a CLI (Command Line Interface) to libeasifem.
It contains some subcommands to help you work with libeasifem.
It can help you in building an application based on easifem components.
It can also build and install the easifem library.

For more information visit:
website: https://www.easifem.com:
(c) Vikas Sharma, 2023
"""

## Some code goes here (not shown)

def main():
    args = parser.parse_args()
    if args.subcommand:
        if args.subcommand == "test":
            easifem_test(args)
        elif args.subcommand == "run":
            easifem_run(args)
        elif args.subcommand == "setenv":
            easifem_setenv(args)
        elif args.subcommand == "install":
            easifem_install(args)
        elif args.subcommand == "uninstall":
            easifem_uninstall(args)
        elif args.subcommand == "clean":
            easifem_clean(args)


if __name__ == "__main__":
    main()
```

## Install hatch

To build the PyPI package we will use [Hatch](https://hatch.pypa.io/latest/), which is a modern, extensible Python project manager.

Install hatch:

### pip

```bash
python3 -m pip install hatch
```

### pipx

```bash
pipx install hatch
```

### conda

```bash
conda install -c conda-forge hatch
```

## Configuration

All project-specific configuration recognized by Hatch can be defined in either the pyproject.toml file, or a file named hatch.toml where options are not contained within the tool.hatch table:

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "easifem"
dynamic = ["version"]
description = "easifem is a command line interface for using EASIFEM library. Expandable And Scalable Infrastructure for Finite Element Methods, EASIFEM, is Modern Fortran framework for solving partial differential equations (PDEs) using finite element methods."
readme = "README.md"
requires-python = ">=3.7"
license = "MIT"
keywords = ["engineering", "application", "high performance computing", "scientific computations", "Modern Fortran", "Fortran", "scientific library", "FEM", "finite element method", "easifem", "command line interface", "cli"]
authors = [
  { name = "Vikas Sharma", email = "Vickysharma0812@gmail.com" },
]
classifiers = [
  "Development Status :: 4 - Beta",
  "Programming Language :: Python",
  "Programming Language :: Python :: 3.7",
  "Programming Language :: Python :: 3.8",
  "Programming Language :: Python :: 3.9",
  "Programming Language :: Python :: 3.10",
  "Programming Language :: Python :: 3.11",
  "Programming Language :: Python :: Implementation :: CPython",
  "Programming Language :: Python :: Implementation :: PyPy",
]
dependencies = [
  "rich>=13",
]


[project.scripts]
easifem = "easifem.easifem:main"

[project.urls]
Documentation = "https://github.com/vickysharma0812/easifem#readme"
Issues = "https://github.com/vickysharma0812/easifem/issues"
Source = "https://github.com/vickysharma0812/easifem"

[tool.hatch.build]
ignore-vcs = false

# include = [
#   "pkg/*.py",
#   "/tests",
# ]
# exclude = [
#   "*.json",
#   "pkg/_compat.py",
# ]

[tool.hatch.version]
path = "src/easifem/__about__.py"

[tool.hatch.envs.default]
dependencies = [
  "coverage[toml]>=6.5",
  "pytest",
]
[tool.hatch.envs.default.scripts]
test = "pytest {args:tests}"
test-cov = "coverage run -m pytest {args:tests}"
cov-report = [
  "- coverage combine",
  "coverage report",
]
cov = [
  "test-cov",
  "cov-report",
]

[[tool.hatch.envs.all.matrix]]
python = ["3.7", "3.8", "3.9", "3.10", "3.11"]

[tool.hatch.envs.lint]
detached = true
dependencies = [
  "black>=23.1.0",
  "mypy>=1.0.0",
  "ruff>=0.0.243",
]
[tool.hatch.envs.lint.scripts]
typing = "mypy --install-types --non-interactive {args:src/easifem tests}"
style = [
  "ruff {args:.}",
  "black --check --diff {args:.}",
]
fmt = [
  "black {args:.}",
  "ruff --fix {args:.}",
  "style",
]
all = [
  "style",
  "typing",
]

[tool.black]
target-version = ["py37"]
line-length = 120
skip-string-normalization = true

[tool.ruff]
target-version = "py37"
line-length = 120
select = [
  "A",
  "ARG",
  "B",
  "C",
  "DTZ",
  "E",
  "EM",
  "F",
  "FBT",
  "I",
  "ICN",
  "ISC",
  "N",
  "PLC",
  "PLE",
  "PLR",
  "PLW",
  "Q",
  "RUF",
  "S",
  "T",
  "TID",
  "UP",
  "W",
  "YTT",
]
ignore = [
  # Allow non-abstract empty methods in abstract base classes
  "B027",
  # Allow boolean positional values in function calls, like `dict.get(... True)`
  "FBT003",
  # Ignore checks for possible passwords
  "S105", "S106", "S107",
  # Ignore complexity
  "C901", "PLR0911", "PLR0912", "PLR0913", "PLR0915",
]
unfixable = [
  # Don't touch unused imports
  "F401",
]

[tool.ruff.isort]
known-first-party = ["easifem"]

[tool.ruff.flake8-tidy-imports]
ban-relative-imports = "all"

[tool.ruff.per-file-ignores]
# Tests can use magic values, assertions, and relative imports
"tests/**/*" = ["PLR2004", "S101", "TID252"]

[tool.coverage.run]
source_pkgs = ["easifem", "tests"]
branch = true
parallel = true
omit = [
  "src/easifem/__about__.py",
]

[tool.coverage.paths]
easifem = ["src/easifem", "*/easifem-cli/src/easifem"]
tests = ["tests", "*/easifem-cli/tests"]

[tool.coverage.report]
exclude_lines = [
  "no cov",
  "if __name__ == .__main__.:",
  "if TYPE_CHECKING:",
]
```


## Build

Builds are configured using the `tool.hatch.build` table. Every target is defined by a section within `tool.hatch.build.targets`.

Invoking the build command without any arguments will build the sdist and wheel targets:

```bash
hatch build
```

To only build specific targets, use the `-t/--target` option:

```bash 
hatch build -t wheel
```

## Publishing

After your project is built, you can distribute it using the publish command.

The `-p/--publisher` option controls which publisher to use, with the default being index.

By default, the `dist` directory located at the root of your project will be used:

```bash
hatch publish
```

> Only files ending with .whl or .tar.gz will be published.

## Verifying using PyPI API token

API tokens provide an alternative way (instead of username and password) to authenticate when uploading packages to PyPI.

You can create a token for an entire PyPI account, in which case, the token will work for all projects associated with that account. Alternatively, you can limit a token's scope to a specific project.

It is strongly recommend that we authenticate with an API token where possible.

To make an API token:
- Verify your email address (check your account settings)
- In your [account](https://pypi.org/manage/account/) settings, go to the API tokens section and select "Add API token"

To use this API token:
Set your username to `__token__`
Set your password to the token value, including the `pypi-` prefix

```bash
hatch publish -u __token__ -a pypi-<your-api-token>
```

## Result

[easifem-cli](https://pypi.org/project/easifem/23.7.0/)


## References:

- [CircleCI.com](https://circleci.com/blog/publishing-a-python-package/?psafe_param=1&utm_source=google&utm_medium=sem&utm_campaign=sem-google-dg--japac-en-dsa-tROAS-auth-nb&utm_term=g_-_c__dsa_&utm_content=&gclid=CjwKCAjwh8mlBhB_EiwAsztdBA18z_fAJ-0rVK5M1rckRxZHFp0IBuxKeJdVpqqJC7bvF5m71XaBCBoCjWkQAvD_BwE)
