---
title: Flatpak Installation
subsection: flatpak
section: deployment
---

# {{page.title}}

## Installing Flatpak

A `flatpak` package has been available for Fedora 24+ and has been installed by default on Fedora Workstation.

If you do not use Fedora Workstation, you can install Flatpak by running:

```
$ sudo dnf install flatpak
```



## Installing Flatpak Builder

Most applications require additional dependencies that aren’t provided by their runtimes. Flatpak allows these dependencies to be bundled as part of the application itself. In order to do this, each dependency 
must be built inside the application build directory. The `flatpak-builder` tool automates this multi-step build process, making it possible to build all application modules with a single command.

To install `flatpak-builder`, run the following command:

```
$ sudo dnf install flatpak-builder
```



## Further Reading

* [FedoraMagazine - Getting Started with Flatpak](https://fedoramagazine.org/getting-started-flatpak/)
* [Get Flatpak](https://flatpak.org/getting.html)