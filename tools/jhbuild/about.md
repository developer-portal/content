---
title: JHBuild
subsection: jhbuild
section: tools
description: Build tool for GNOME development which downloads, configures and builds the code while figuring out dependencies.
---

# What is JHBuild
[JHBuild](https://developer.gnome.org/jhbuild/stable/introduction.html.en) is the recommended way to build and run GNOME development code. It will download the code, configure and build it for you, in a way that does not interfere with or modify your existing system. JHBuild will also figure out which dependencies are required from your distribution, and it will build any development software that is needed.

## Installing JHBuild on Fedora

Install basic required packages
```
$ sudo dnf install gnome-common yelp-tools autoconf gettext-devel docbook-xsl perl-XML-Parser cvs flex bison svn glib glib-devel pygobject2 dbus-python redhat-rpm-config
```

Make directory ~/jhbuild/checkout where all the code will live and cd to it
```
$ mkdir ~/jhbuild/checkout
$ cd ~/jhbuild/checkout
```

Clone jhbuild
```
$ git clone --depth=1 git://git.gnome.org/jhbuild
```

Cd to the source directory and build it
```
$ cd ~/jhbuild/
$ ./autogen.sh
$ make
$ make install
```

Add the JHBuild installation path (.local/bin) to your PATH directory
```
$ echo 'PATH=$PATH:~/.local/bin' >> ~/.bashrc
$ source ~/.bashrc
```

Check build prerequisites
```
$ jhbuild sanitycheck
```
Install system dependencies
```
$ jhbuild sysdeps --install
```

## More
More details can be found in the [JHBuild manual](https://developer.gnome.org/jhbuild/stable/) or on [HowDoI/JHBuild](https://wiki.gnome.org/HowDoI/Jhbuild)
