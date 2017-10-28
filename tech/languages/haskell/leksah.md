---
title: Leksah
subsection: haskell
order: 4
---

# Leksah

[Leksah](http://leksah.org/) is a Haskell IDE written in Haskell using Gtk. It offers workspaces for complex project with multiple 
packages with automatic build of dependencies. It enables standard IDE features (debugging, auto completition etc.).

To install Leksah run command:

```
$ sudo dnf install ghc cabal-install
```

or install Haskell Platform by command:

```
$ sudo dnf install haskell-platform
```

You have to also install the necessary libraries for successful build by:

```
$ sudo dnf install gobject-introspection-devel webkitgtk3-devel gtksourceview3-devel
```

You can than install the IDE using `cabal`. First update all the packages by:

```
$ cabal update
```

Now upgrade cabal to the latest stable version:

```
$ cabal install Cabal
```

Install build packages and tools:

```
$ cabal install alex happy
$ cabal install gtk2hs-buildtools
```

Install the IDE:

```
$ cabal install leksah
```

Than you can run the IDE:

```
$ leksah
```

NOTE: It might happen that you need to reboot the system before using Leksah.


