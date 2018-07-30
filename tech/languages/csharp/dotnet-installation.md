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

.NET Core SDK will enable building and publishing C# source code.
```
$ sudo dnf install dotnet-sdk-2.1
```

### .NET Core Runtime only

You can install runtime only, if you are just deploying already prebuilt application.
```
$ sudo dnf install dotnet-runtime-2.1
```

## Create your app
You can create your first console app following instructions in [this official guide](https://www.microsoft.com/net/learn/get-started-with-dotnet-tutorial#create).

## Microsoft .NET Core packages

[.NET Core packages built by Microsoft](https://www.microsoft.com/net/download/linux) contain some proprietary libraries of the .NET Framework.


## References

* [Fedora .NET SIG copr](https://copr.fedorainfracloud.org/coprs/g/dotnet-sig/dotnet)
* [.NET Core API documentation](https://docs.microsoft.com/en-us/dotnet/api/index?view=netcore-2.0)

