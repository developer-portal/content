---
title: .NET Core
subsection: dotnet
order: 2
version: 7.8.4
---

## .NET Core Installation

### .NET Core 6 and 7

.NET Core 6 and 7 is included in Fedora 36 and 37 Simply install it using one of the below variants:

Install the latest SDK:
```
$ sudo dnf install dotnet
```

Or a specific version:
### Install .NET Core 6 SDK

```
$ sudo dnf install dotnet-sdk-6.0
```

To install runtime only, for example to merely deploy already prebuilt applications, where _x_ stands for major and _y_ stands for minor version:
```
$ sudo dnf install dotnet-runtime-x.y
```

### Preview versions

Preview packages can be installed after enabling the preview [copr repository](/deployment/copr/about.html) repository:
```
$ sudo dnf copr enable @dotnet-sig/dotnet-preview
$ sudo dnf install dotnet-sdk-x.y
```

## Getting Started

You can create your first console app following instructions in [this official guide](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/create).
