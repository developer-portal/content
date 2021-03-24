---
title: Java
subsection: java
order: 1
section: tech-languages
description: General-purpose, object-oriented and concurrent computer programming language.
---

# Java installation

Fedora comes with [OpenJDK](http://openjdk.java.net/) - a free and open source implementation of the Java Platform, Standard Edition. To install it, simply type:

```
$ sudo dnf install java-15-openjdk-devel
```

This command will install Java Development Kit - runtime environment and associated development tools.

[IcedTea-Web](http://icedtea.classpath.org/wiki/IcedTea-Web) may come handy if your plan is to develop Java applets or to experiment with Java Web Start. To install it, simply type:

```
$ sudo dnf install icedtea-web
```

This command will install Java web browser plugin and free implementation of Java Web Start.

Later, when you will want to test your new application in a production-like environment, it's possible to install just Java runtime environment (JRE) - without development tools. This can be achieved by several means:

```
$ sudo dnf install java-15-openjdk-headless
```

The command above will install so-called "headless" JRE, i.e. JRE without support for graphic and audio. If your application is supposed to run on a server without any graphical user interface (GUI) installed, then this is likely what you want.

However, if your application needs support for GUI or audio, you will likely want to install full JRE. You can do that simply by typing:

```
$ sudo dnf install java-15-openjdk
```

<!-- TODO: add section about installing JDK from 3rd parties + how to switch between them -->
