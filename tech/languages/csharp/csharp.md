---
title: C# - IDEs
subsection: csharp
section: tech-languages
order: 1
version: 7.8.4
description: "C# programming language, .NET Core and Mono open source frameworks."
---

# C# IDEs in Fedora

## Visual Studio Code

_.NET Core Only_

VS Code is plugin-based IDE that by itself won't just run C#. You have to install the C# plugin, and NuGet Package Manager.

[code.visualstudio.com](https://code.visualstudio.com)

## JetBrains Rider

_.NET Core and Mono_

JetBrains Rider is full featured IDE for all things C#, and even F# on .NET Core. If you are familiar with other JetBrains products, such as the IntelliJ or Resharper, you might like this one as well.

[jetbrains.com/rider](http://jetbrains.com/rider)

## MonoDevelop

_Mono only_

MonoDevelop provides the best C# experience on Mono, the open-source multiplatform implementation of the .NET Framework.

[monodevelop.com](http://www.monodevelop.com)

```
$ sudo dnf install monodevelop
```

## Eclipse IDE (with plugin)

_Mono only, with upcoming support for .NET Core as well_

You can get [Eclipse IDE](/tools/eclipse/about.html) with [aCute plugin](https://github.com/mickaelistria/aCute), which relies on [OmniSharp](http://www.omnisharp.net) and [Language Server Protocol](https://github.com/Microsoft/language-server-protocol). Although it's still experimental, this already provides nice edition features for C# in the Eclipse IDE.

```
$ sudo dnf install eclipse eclipse-mpc
```
then install the aCute extension from [Eclipse Marketplace](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental)

## Summary

What would we recommend? JetBrains Rider is the best C# IDE, however it is not open source. VS Code is great for .NET Core and MonoDevelop for Mono. C# in Eclipse IDE is work in progress, and supports only Mono for now; it can already be useful if you're already an user of Eclipse IDE with any other programming language.
