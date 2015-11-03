---
title: Haskell
page: haskell
section: tech-languages
order: 1
version: 7.8.4
description: >
  An advanced, general-purpose, purely-functional programming language with
  non-strict semantics and strong static typing.
---

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
