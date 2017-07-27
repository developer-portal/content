---
title: .NET Core
subsection: csharp
order: 3
---

# .NET Core

## Fedora .NET SIG repository

.NET Core is still work in progress. The download location below contains packages that do not meet the official Fedora requirements yet (such as containing prebuilt binaries or bundled dependencies.) Please be patient, we should have reasonable packages within a few months.

[Fedora .NET SIG copr](https://copr.fedorainfracloud.org/coprs/g/dotnet-sig/dotnet)

To enable the .NET SIG's copr repository:

`$ sudo dnf copr enable @dotnet-sig/dotnet`

## .NET Core SDK

.NET Core SDK will enable building and publishing C# source code.

`$ sudo dnf install dotnet-sdk-2.0`

## .NET Core Runtime only

You can install runtime only, if you are just deploying already prebuilt application.

`$ sudo dnf install dotnet-runtime-2.0`

## API Reference

You can find .NET Core API documentation at [docs.microsoft.com](https://docs.microsoft.com/en-us/dotnet/api/index?view=netcore-2.0)

