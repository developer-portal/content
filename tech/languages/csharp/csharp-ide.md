---
title: IDEs
subsection: csharp
order: 2
---

# C# IDEs in Fedora

## JetBrains Rider

_.NET Core and Mono_

JetBrains Rider is full featured IDE for all things C#, and even F# on .NET Core. If you are familiar with other JetBrains products, such as the IntelliJ or Resharper, you might like this one as well.

[jetbrains.com/rider](http://jetbrains.com/rider)

## Visual Studio Code

_.NET Core Only_

* VS Code will not work with [our .NET Core packages](/tech/languages/csharp/dotnet-installation.html) due to an [upstream issue](https://github.com/dotnet/source-build/issues/125) affecting OmniSharp. You can still use it with [Microsoft's dotnet packages](https://www.microsoft.com/net/core#linuxfedora).

Visual Studio Code (aka VS Code) is plugin-based IDE that by itself won't just run C#. You have to install the C# plugin, and NuGet Package Manager.

Download the Visual Studio Code at [code.visualstudio.com](https://code.visualstudio.com) and the C# Extension at [marketplace.visualstudio.com](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)

## Eclipse

_.NET Core and Mono_

* Eclipse will not work with [our .NET Core packages](/tech/languages/csharp/dotnet-installation.html) due to an [upstream issue](https://github.com/dotnet/source-build/issues/125) affecting OmniSharp. You can still use it for mono, or with [Microsoft's dotnet packages](https://www.microsoft.com/net/core#linuxfedora).

You can use the [aCute plugin](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental) on top of the established and popular [Eclipse IDE](/tools/eclipse/about.html). This C# extension for Eclipse IDE relies on [OmniSharp](http://www.omnisharp.net) and [Language Server Protocol](https://github.com/Microsoft/language-server-protocol). It comes with complete edition features for C# in the Eclipse IDE, relying on the Eclipse IDE provides all typical features of a good IDE (Polyglot development, SCM, deployment...) and give access to a rich ecosystem of extensions for about all existing technologies.

```
$ sudo dnf install eclipse eclipse-mpc
```
then install the aCute extension from [Eclipse Marketplace](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental)

## MonoDevelop

_Mono only_

MonoDevelop provides the best C# experience on Mono, the open-source multiplatform implementation of the .NET Framework.

[monodevelop.com](http://www.monodevelop.com)

```
$ sudo dnf install monodevelop
```

## Summary

What would we recommend? JetBrains Rider is the best C# IDE, however it is not open source. VS Code is great for .NET Core and MonoDevelop for Mono. C# in Eclipse IDE is still young and not very friendly to former Windows developer, but it can be useful if you're already an Eclipse IDE user.
