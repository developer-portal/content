---
title: .NET Core
subsection: dotnet
order: 2
version: 7.8.4
---

## .NET Core Installation

Enable the .NET SIG's [copr repository](/deployment/copr/about.html) repository:
```
$ sudo dnf copr enable @dotnet-sig/dotnet
```

Install the latest SDK:
```
$ sudo dnf install dotnet
```

Or a specific version:
```
# Install .NET Core 2.1 SDK
$ sudo dnf install dotnet-sdk-2.1
```

To install runtime only, for example to merely deploy already prebuilt applications, where _x_ stands for major and _y_ stands for minor version:
```
$ sudo dnf install dotnet-runtime-x.y
```

Preview packages can be installed after enabling the preview [copr repository](/deployment/copr/about.html) repository:
```
$ sudo dnf copr enable @dotnet-sig/dotnet-preview
$ sudo dnf install dotnet-sdk-x.y
```

## Getting Started

You can create your first console app following instructions in [this official guide](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/create).
