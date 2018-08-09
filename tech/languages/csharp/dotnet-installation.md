---
title: .NET Core
subsection: csharp
order: 3
---

# .NET Core

## Fedora .NET SIG repository

.NET Core is still work in progress. The download location below contains packages that do not meet the official Fedora requirements yet (such as using prebuilt tools to build the source) but are _free_.

To enable the .NET SIG's copr repository:
```
$ sudo dnf copr enable @dotnet-sig/dotnet
```

### .NET Core SDK

.NET Core SDK enables building and publishing of C# source code.

To install the latest SDK version:

```
$ sudo dnf install dotnet
```

To install the latest SDK for a specific .NET Core Runtime, where the _x_ stands for major, _y_ for minor version of the runtime:
```
$ sudo dnf install dotnet-sdk-x.y
```

### .NET Core Runtime only

To install runtime only, for example to merely deploy already prebuilt applications, where _x_ stands for major and _y_ stands for minor version:
```
$ sudo dnf install dotnet-runtime-x.y
```

## References

* [Fedora .NET SIG copr](https://copr.fedorainfracloud.org/coprs/g/dotnet-sig/dotnet)
* [.NET Core API documentation](https://docs.microsoft.com/en-us/dotnet/api/index?view=netcore-2.0)

