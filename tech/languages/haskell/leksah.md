---
title: Leksah
subsection: haskell
order: 4
---

# Leksah

[Leksah](http://leksah.org/) is a Haskell IDE written in Haskell using Gtk. It offers Workspaces for complex project with multiple 
packages with automatic build of dependencies. It enables standard IDE features (debugging, auto completition etc.).

To install Leksah you need to install `ghc` and `cabal` first (or install the Haskell Platform).

You have to also install the necessary libraries for successful build by:

```
$ sudo dnf install gobject-introspection-devel webkitgtk3-devel gtksourceview3-devel
```

You can than install the IDE using `cabal` by:

```
$ cabal update
$ cabal install Cabal
$ cabal install alex happy
$ cabal install gtk2hs-buildtools
$ cabal install leksah
```

Than you can run the IDE:

```
$ leksah
```

NOTE: It might happen that you need to reboot the system before using Leksah.


