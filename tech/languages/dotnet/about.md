---
title: .NET Platforms
subsection: dotnet
section: tech-languages
order: 1
version: 7.8.4
description: ".NET and Mono are open-source .NET platforms. .NET applications are developed using the C#, F# and VB.NET programming languages."
permalink: /tech/languages/csharp/dotnet-installation.html
---

.NET, .NET Core and Mono are available on Fedora. .NET applications are developed using the C#, F# and VB.NET programming languages.

## .NET and .NET Core

[.NET](https://docs.microsoft.com/en-us/dotnet/core/) is a general-purpose, modular, cross-platform and open-source development Platform.

.NET 7 and .NET 6 are available in all supported versions of Fedora. Installing an SDK can be done with a simple

```
$ sudo dnf install dotnet-sdk-x.y
```

Where `x.y` is a .NET version number, like `7.0` or `6.0`.

It is not advised to mix these packages with those provided by Microsoft. Please disable any other repositories providing dotnet before installing these. If you run into any errors that refer to `/usr/share/dotnet` or a missing `libhostfxr.so` see [troubleshoot .NET errors related to missing files on Linux](https://learn.microsoft.com/en-us/dotnet/core/install/linux-package-mixup) which describes how to fix the errors.

See the [.NET](dotnetcore.html) page for more information.

## Mono

[Mono](http://www.mono-project.com/) is a free and open source implementation of the .NET Framework.

To install Mono, simply type:

```
$ sudo dnf install mono-devel
```

See the [Mono](mono.html) page for more information.
