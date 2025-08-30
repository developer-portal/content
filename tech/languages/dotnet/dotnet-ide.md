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
| [JetBrains Rider](http://jetbrains.com/rider) | [Proprietary](https://www.jetbrains.com/store/license.html), free for [Education and OpenSource](https://www.jetbrains.com/store/#edition=discounts) | &#x2714; | &#x2714; | &#x2714; |  |
| [Visual Studio Code](https://code.visualstudio.com) with [C# plugin](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) | Binary is [Proprietary](https://code.visualstudio.com/License/), Source Code is [MIT](https://github.com/Microsoft/vscode/blob/master/LICENSE.txt), C# extension is [Proprietary](https://marketplace.visualstudio.com/items/ms-vscode.csharp/license) | &#x2714; |  | &#x2714; |  |

## Overview

[JetBrains Rider](#installing-jetbrains-rider) is the most complete C# IDE, however it is not open source.

[Visual Studio Code](#installing-visual-studio-code) and [MonoDevelop](#installing-monodevelop) work well for .NET Core and for Mono, respectively.

[Eclipse](#installing-eclipse) is still young and not yet friendly for the former Windows developer. It is a good choice if you're already an Eclipse IDE user.

## Installing JetBrains Rider

* Apply for a [license for Open Source projects or students](https://www.jetbrains.com/store/?fromMenu#edition=discounts) and [download Rider](http://jetbrains.com/rider)
* Or download the [Early Access](https://www.jetbrains.com/rider/eap) version

## Installing Visual Studio Code

### From Microsoft
[Visual Studio Code](https://code.visualstudio.com) is available:
  * packaged as an RPM

    First, lets import the GPG key:
    ```console
    $ sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    ```
    
    Then, we need to create a repo file `/etc/yum.repos.d/vscode.repo` with the following content:
    ```
    [code]
    name=Visual Studio Code
    baseurl=https://packages.microsoft.com/yumrepos/vscode
    enabled=1
    gpgcheck=1
    gpgkey=https://packages.microsoft.com/keys/microsoft.asc
    ```
    _You need root permissions to create file in this location._

    After creating the repo file you can install the Visual Studio Code with:
    ```console
    $ sudo dnf install code
    ```

  * distributed as a [Flatpak](/deployment/flatpak/about.html)
    ```console
    $ flatpak install com.visualstudio.code
    ```

After installing Visual Studio Code, to get full features of the editor, install the C# Extension from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

### VSCodium

[VSCodium](https://vscodium.com/) are Free/Libre Open Source Software Binaries of VSCode.


## Installing Eclipse

First install Eclipse through [Flatpak](/deployment/flatpak/about.html)
```
$ flatpak install org.eclipse.Java
```
then install the aCute extension from the [Eclipse Marketplace](https://marketplace.eclipse.org/content/acute-c-edition-eclipse-ide-experimental)


## References

* [Installing VSCode as an RPM](https://code.visualstudio.com/docs/setup/linux#_rhel-fedora-and-centos-based-distributions)
