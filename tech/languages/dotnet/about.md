---
title: C#, F#, VB.NET
subsection: dotnet
section: tech-languages
order: 1
version: 7.8.4
description: ".NET Core and Mono open-source .NET platforms"
---

.NET programming languages can be used on Fedora with .NET Core and Mono.

## .NET Core

[.NET Core](https://docs.microsoft.com/en-us/dotnet/core/) is a general-purpose, modular, cross-platform and open-source development Platform.

To install .NET Core, add the .NET SIG's copr repository and install the `dotnet` package.

```
$ sudo dnf copr enable -y @dotnet-sig/dotnet
$ sudo dnf install dotnet
```

See the [.NET Core](dotnet.md) page for more information.

## Mono

[Mono](http://www.mono-project.com/) is a free and open source implementation of the .NET Framework.

To install Mono, simply type:

```
$ sudo dnf install mono-devel
```

See the [Mono](mono.md) page for more information.