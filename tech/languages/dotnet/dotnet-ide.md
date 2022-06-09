---
title: IDEs
subsection: dotnet
order: 4
---

# .NET IDEs in Fedora

{: .centered .striped .highlight}
| IDE | License | .NET Core | Mono | Debugger | Packaged in Fedora |
|---|---|---|---|---|---|
| [Eclipse](/tools/eclipse/about.html) with [aCute plugin](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental) | [EPL](http://www.eclipse.org/legal/epl-2.0/) | &#x2714; | &#x2714; |  |  |
| [Monodevelop](http://www.monodevelop.com/) | [LGPLv2](http://www.gnu.org/licenses/lgpl-2.1.html) |  | &#x2714; | &#x2714; | &#x2714; |
| [JetBrains Rider](http://jetbrains.com/rider) | [Proprietary](https://www.jetbrains.com/store/license.html), free for [Education and OpenSource](https://www.jetbrains.com/store/#edition=discounts) | &#x2714; | &#x2714; | &#x2714; |  |
| [Visual Studio Code](https://code.visualstudio.com) with [C# plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) | Binary is [Proprietary](https://code.visualstudio.com/License/), Source Code is [MIT](https://github.com/Microsoft/vscode/blob/master/LICENSE.txt), C# extension is [Proprietary](https://marketplace.visualstudio.com/items/ms-vscode.csharp/license) | &#x2714; |  | &#x2714; |  |

## Installing Eclipse

First install Eclipse through [Flatpak](/deployment/flatpak/about.html)
```
$ flatpak install org.eclipse.Java
```
then install the aCute extension from the [Marketplace](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental)

## Installing MonoDevelop

```
$ sudo dnf install monodevelop
```

## Installing JetBrains Rider

* Apply for a [license for Open Source projects or students](https://www.jetbrains.com/store/?fromMenu#edition=discounts) and [download Rider](http://jetbrains.com/rider)
* Or download the [Early Access](https://www.jetbrains.com/rider/eap) version

## Installing Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com) is available:
  * as an RPM downloadable from their website.
  * as a [Flatpak](/deployment/flatpak/about.html) package installable like so:
  ```
  $ flatpak install com.visualstudio.code
  ```

After installing Visual Studio Code you can install the C# Extension from the [Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

Alternatively use the [VSCodium](https://vscodium.com/) for Free/Libre Open Source Software Binaries of VSCode.

## Summary

JetBrains Rider is the most complete C# IDE, however it is not open source.

VS Code and MonoDevelop work well for .NET Core and for Mono, respectively.

C# via Eclipse is still young and not very friendly for the former Windows developer, but it can be useful if you're already an Eclipse IDE user.
