---
title: GTK+
subsection: gui-app
section: start-sw
description: 
---

# Create an application using GTK+

GTK+ is a cross platform graphical toolkit which stands for GIMP toolkit.
It was started in 1998 as an free and open source alternative to Qt which was
proprietary at the time. GTK+ is published under the GNU LGPL 2.1 license.

## Installing the development packages

GTK+ is written in C so the minimum required to create a GTK+ application is a
C compiler and the GTK+ development package:

```
$ sudo dnf install gcc gtk3-devel
```

After installing the compiler and development package you can follow the GTK+
[getting started guide][0] on GNOME website.

## Other languages

GTK+ is written in C but it also have official support for C++, JavaScript, 
Python, Vala and Rust.

### Vala

If you want to develop in Vala, you need to install a Vala compiler in addition
to the general development packages mentioned above. To do it you can run:

```
$ sudo dnf install vala
```

After that you can follow [GNOME Vala tutorial][1] to learn how to develop GUI
applications with Vala.

## Using GNOME Builder

GNOME Builder is an IDE made by GNOME developers to help create GTK+ applications.

To install GNOME Builder using dnf run the command:

```
$ sudo dnf install gnome-builder
```

If you want to install GNOME Builder using Flatpak run the command:

```
$ flatpak install --from https://flathub.org/repo/appstream/org.gnome.Builder.flatpakref
```

[0]: https://developer.gnome.org/gtk3/stable/gtk-getting-started.html
[1]: https://wiki.gnome.org/Projects/Vala/Tutorial
