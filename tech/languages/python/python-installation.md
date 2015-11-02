---
title: Python
page: python
section: tech-languages
order: 1
version: 2.7.10
description: General-purpose, high-level programming language supporting multiple programming paradigms.
---

# Python installation

## CPython

Currently we have two releases; Python-2.7.10 and Python-3.4.2.
In Fedora 23 Workstation, both Python 2 and Python 3 come preinstalled, but if for whatever reason you need to install Python 2, simply type:

```
$ sudo dnf install python2
```

Similarly for Python 3:

```
$ sudo dnf install python3
```

The above command will install the latest stable Python 2/3 package and also the useful [python-pip](/tech/languages/python/pypi-installation.html).

## PyPy

Fedora also includes PyPy, a significantly faster (under most circumstances), JIT enabled, Python interpreter. It is not 100% compatible with CPython, so some modules might not work.

You can install PyPy with:

```
$ sudo dnf install pypy
```
