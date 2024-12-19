---
title: .NET
subsection: dotnet
order: 2
version: 7.8.5
---

## .NET Installation

.NET packages are available in Fedora repositories.

It is not advised to mix these packages with those provided by Microsoft. Please disable any other repositories providing dotnet before installing these. If you run into errors, see [troubleshooting linux package mixup](https://learn.microsoft.com/en-us/dotnet/core/install/linux-package-mixup) for some suggestions on how to fix the issue.

To install a .NET SDK only, run this command, where _x_ stands for major and _y_ stands for minor version:

```
$ sudo dnf install dotnet-sdk-x.y
```

To install the ASP.NET Core Runtime only, for example to deploy an already built ASP.NET Core applications, where _x_ stands for major and _y_ stands for minor version:

```
$ sudo dnf install aspnetcore-runtime-x.y
```

To install runtime only, for example to merely deploy an already built (non ASP.NET Core) applications, where _x_ stands for major and _y_ stands for minor version:

```
$ sudo dnf install dotnet-runtime-x.y
```

### .NET 9

.NET 9 is a Standard Term Support release and will reach its End of Life in May 2026.

Install the .NET 9 SDK:

```
$ sudo dnf install dotnet-sdk-9.0
```

Install the ASP.NET Core 9 Runtime:

```
$ sudo dnf install aspnetcore-runtime-9.0
```

Install the .NET 9 Runtime:

```
$ sudo dnf install dotnet-runtime-9.0
```

### .NET 8

.NET 8 is a Long Term Support release and will reach its End of Life in Nov 2026.

Install the .NET 8 SDK:

```
$ sudo dnf install dotnet-sdk-8.0
```

Install the ASP.NET Core 8 Runtime:

```
$ sudo dnf install aspnetcore-runtime-8.0
```

Install the .NET 8 Runtime:

```
$ sudo dnf install dotnet-runtime-8.0
```


### Preview versions

Preview packages can be installed after enabling the preview [copr repository](/deployment/copr/about.html) repository:
```
$ sudo dnf copr enable @dotnet-sig/dotnet-preview
$ sudo dnf install dotnet-sdk-x.y
```

Please note that these preview packages aren't fully tested. They may contain bugs and may destroy data.

## Getting Started

You can create your first console app following instructions in [this official guide](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/create).
