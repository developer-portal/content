---
title: Haskell
subsection: haskell
section: tech-languages
order: 1
version: 8.0.2
description: >
  An advanced, general-purpose, purely-functional programming language with
  non-strict semantics and strong static typing.
---

# Stack

## What it is

Stack is a cross-platform build tool for Haskell that handles management of the toolchain (including the GHC compiler and MSYS2 on Windows), building and registering libraries, and more.

## What you get

* Once downloaded, it has the capacity to download and install GHC and other core tools.
* Project development is isolated within sandboxes, including automatic download of the right version of GHC for a given project.
* It manages all Haskell-related dependencies, ensuring reproducible builds.
* It fetches from a curated repository of over a thousand packages by default, known to be mutually compatible.
* It can optionally use Docker to produce standalone deployments

## How to install

To install stack on Fedora, run:

```
$ sudo dnf install stack
```

# GHC installation

The Glasgow Haskell Compiler (GHC) is an open source native code compiler for
Haskell.

To install GHC on Fedora, run:

```
$ sudo dnf install ghc
```

This will install GHC including the `ghci` read-eval-print-loop, the `haddock`
documentation generator, and several other utilities.

Please refer to the official documentation at
[https://haskell.org/ghc](https://haskell.org/ghc) for more information about
GHC, or [https://haskell.org](https://haskell.org) for information about Haskell
in general.

# The Haskell Platform

Another option is to install the
[Haskell Platform](https://www.haskell.org/platform/), which provides `ghc` and
`ghci` as above, but also includes a plethora of useful Haskell libraries and
utilities to help kickstart your Haskell programming experience.

The Haskell Platform also includes Cabal, which aids in the packaging,
distribution, and installation of Haskell libraries and applications.

To install the Haskell Platform, run:

```
$ sudo dnf install haskell-platform
```
