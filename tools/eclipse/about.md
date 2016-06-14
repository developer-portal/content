---
title: Eclipse
subsection: eclipse
section: tools
description: Full featured development environment for various programming languages integrating with plethora of different tools to make development process as integrated as possible
---

# What is Eclipse

[Eclipse](https://www.eclipse.org/ide/) is a full featured, multi language IDE aiding developers in every step of software development lifecycle. Starting new project, working on established project with complex structure, monitoring and performance optimizing application, writing documentation, interacting with issue tracking systems or CI all from inside Eclipse IDE.

## Installing Eclipse on Fedora

On Fedora install the eclipse package:

```
$ sudo dnf install eclipse
```

This would give you Eclipse Platform with Java and Plugin development tools but it's easy to install support for various other languages and ecosystems as they are packaged in Fedora:

* C/C++ - eclipse-cdt packages
* PHP - eclipse-pdt package
* Ruby - eclipse-dltk-ruby package
* TCL - eclipse-dltk-tcl package
* Shell script - eclipse-dltk-sh package
* Python - eclipse-pydev package
* Photran - eclipse-photran package
* Web technologies - eclipse-webtools-* packages

Plugins providing integration for various other technologies is also available:

* Git - eclipse-egit and eclipse-egit-github
* Subversion - eclipse-subclipse
* Maven - eclipse-m2e-*
* Gcov/Gprof - eclipse-gcov/eclipse-gprof
* Systemtap - eclipse-systemtap
* Kernel Perf - eclipse-perf
* Oprofile - eclipse-oprofile
* Bug trackers and CIs - eclipse-mylyn-* packages

The list above doesn't contain all Eclipse plugins available in Fedora but is supposed to serve as an example of the range of different technologies integrated.

Alternative method for installing Eclipse on Fedora is by using `gnome-software`. Some of the packaged plugins ship proper metadata so they can be seen and installed directly from it.

Last but not least there is [Eclipse Marketplace](http://marketplace.eclipse.org/) (`sudo dnf install eclipse-mpc`) giving you access to even bigger list of plugins to integrate even more tools in your ide. Once Eclipse is running go to `Help\Eclipse Marketplace...` and search for plugins serving your needs.

