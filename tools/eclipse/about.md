---
title: Eclipse
subsection: eclipse
section: tools
description: Full featured development environment for various programming languages integrating with plethora of different tools to make development process as integrated as possible
---

# What is Eclipse

[Eclipse](https://www.eclipse.org/ide/) is a full featured, multi language IDE aiding developers in every step of software development lifecycle. Starting new project, working on established project with complex structure, monitoring and performance optimizing application, writing documentation, interacting with issue tracking systems or CI all from inside Eclipse IDE.

## Installing Eclipse on Fedora

On Fedora the Eclipse IDE is available as a [Flatpak](/deployment/flatpak/about.html):

```
$ flatpak install org.eclipse.Java
```

This would give you Eclipse Platform with Java and Plugin development tools but it's easy to install support for various other languages and ecosystems as they are available in the Eclipse Marketplace:

* C/C++ - cdt
* PHP - pdt
* Ruby - dltk-ruby
* TCL - dltk-tcl
* Shell script - dltk-sh
* Python - pydev
* Photran - photran
* Web technologies - webtools-*

Plugins providing integration for various other technologies is also available:

* Git - egit and egit-github
* Subversion - subclipse
* Maven - m2e-*
* Gcov/Gprof - gcov/gprof
* Systemtap - systemtap
* Kernel Perf - perf
* Oprofile - oprofile
* Bug trackers and CIs - mylyn-*

The list above doesn't contain all Eclipse plugins available but is supposed to serve as an example of the range of different technologies integrated.

Last but not least there is [Eclipse Marketplace](http://marketplace.eclipse.org/) giving you access to even bigger list of plugins to integrate even more tools in your ide. Once Eclipse is running go to `Help\Eclipse Marketplace...` and search for plugins serving your needs.

