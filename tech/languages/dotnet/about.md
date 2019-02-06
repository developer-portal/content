---
title: .NET
subsection: dotnet
section: tech-languages
order: 1
version: 7.8.4
description: ".NET Core and Mono are open-source .NET platforms. .NET applications are developed using the C#, F# and VB.NET programming languages."
---

.NET Core and Mono are available on Fedora. .NET applications are developed using the C#, F# and VB.NET programming languages.

## .NET Core

[.NET Core](https://docs.microsoft.com/en-us/dotnet/core/) is a general-purpose, modular, cross-platform and open-source development Platform.

To install .NET Core, add the .NET SIG's [copr repository](/deployment/copr/about.html) repository and install the `dotnet` package.

```
$ sudo dnf copr enable @dotnet-sig/dotnet
$ sudo dnf install dotnet
```

See the [.NET Core](dotnet.html) page for more information.

## Mono

[Mono](http://www.mono-project.com/) is a free and open source implementation of the .NET Framework.

To install Mono, simply type:

```
$ sudo dnf install mono-devel
```

See the [Mono](mono.html) page for more information.
