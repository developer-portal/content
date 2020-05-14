---
title: .NET Platforms
subsection: dotnet
section: tech-languages
order: 1
version: 7.8.4
description: ".NET Core and Mono are open-source .NET platforms. .NET applications are developed using the C#, F# and VB.NET programming languages."
permalink: /tech/languages/csharp/dotnet-installation.html
---

.NET Core and Mono are available on Fedora. .NET applications are developed using the C#, F# and VB.NET programming languages.

## .NET Core

[.NET Core](https://docs.microsoft.com/en-us/dotnet/core/) is a general-purpose, modular, cross-platform and open-source development Platform.

.NET Core 3.1 and later versions are packaged in Fedora since 32. Installing the latest SDK can be done with a simple

```
$ sudo dnf install dotnet
```

For older versions of Fedora and .NET Core 2.1, add the .NET SIG's [copr repository](/deployment/copr/about.html) repository and install the `dotnet-sdk-2.1` package.

```
$ sudo dnf copr enable @dotnet-sig/dotnet
$ sudo dnf install dotnet-sdk-2.1
```

It is not advised to mix these packages with those provided by Microsoft, please disable any other repositories providing dotnet before installing these.

See the [.NET Core](dotnetcore.html) page for more information.

## Mono

[Mono](http://www.mono-project.com/) is a free and open source implementation of the .NET Framework.

To install Mono, simply type:

```
$ sudo dnf install mono-devel
```

See the [Mono](mono.html) page for more information.
