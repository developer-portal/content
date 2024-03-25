---
title: Cabal
subsection: haskell
order: 2
---

# Cabal

To install Haskell libraries and build Haskell projects, you will likely want to
install `cabal` -- a system which aids in the packaging, distribution, and
installation of Haskell libraries and applications.

If you've chosen to install the Haskell Platform, then you already have Cabal
installed. Otherwise, you can install it by:

```
$ sudo dnf install cabal-install
```

You can then install packages from [Hackage](https://hackage.haskell.org/) by
using:

```
$ cabal install <package name>
```

Note that Fedora offers a large number of Hackage packages in its official
repositories as RPMs. You can always try installing a Hackage package via `dnf`
first using:

```
$ sudo dnf install ghc-<package name>
```
