---
title: Mono
subsection: dotnet
order: 3
---

## Mono installation

To install Mono, simply type:

```
$ sudo dnf install mono-devel
```

This command will install Mono -- the runtime environment and associated development tools.


## NUnit installation

[NUnit](http://nunit.org/) is very useful for test driven development. To install it, simply type:

```
$ sudo dnf install nunit nunit-gui
```

## Documentation

The information about installing Mono and related details can be found at [mono-project.com/docs](http://www.mono-project.com/docs)

## API Reference

The documentation by Microsoft for the .NET Framework API generally applies to Mono as well, with minor differences.
You can find the .NET Framework API documentation for versions 4.5 and higher at [docs.microsoft.com](https://docs.microsoft.com/en-us/dotnet/api/index?view=netframework-4.5).
In the Fedora packages for Mono, we don't support earlier versions of the .NET Framework API.
