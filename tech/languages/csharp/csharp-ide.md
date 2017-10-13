---
title: IDEs
subsection: csharp
order: 2
---

# C# IDEs in Fedora

## Visual Studio Code

_.NET Core Only_

Visual Studio Code (aka VS Code) is plugin-based IDE that by itself won't just run C#. You have to install the C# plugin, and NuGet Package Manager.

[code.visualstudio.com](https://code.visualstudio.com)

## JetBrains Rider

_.NET Core and Mono_

JetBrains Rider is full featured IDE for all things C#, and even F# on .NET Core. If you are familiar with other JetBrains products, such as the IntelliJ or Resharper, you might like this one as well.

[jetbrains.com/rider](http://jetbrains.com/rider)

## Eclipse IDE (with plugin)

_.NET Core and Mono_

You can use the [aCute plugin](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental) on top of the established and popular [Eclipse IDE](/tools/eclipse/about.html). This C# extension for Eclipse IDE relies on [OmniSharp](http://www.omnisharp.net) and [Language Server Protocol](https://github.com/Microsoft/language-server-protocol). It comes with complete edition features for C# in the Eclipse IDE. Relying on the Eclipse IDE provides all typical features of a good IDE (Polyglot development, SCM, deployment...) and give access to a rich ecosystem of extensions for about all existing technologies.

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
