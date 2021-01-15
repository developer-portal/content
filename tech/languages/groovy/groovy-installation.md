---
title: Groovy
subsection: groovy
order: 1
section: Powerful, optionally typed and dynamic language with static compilation capabilities on JVM.
description:
---

# Groovy installation

To install Groovy in Fedora, simply type:

```
$ sudo dnf install groovy
```

This command will install several command-line executables useful for development in Groovy, notably:

* groovy - Groovy interpreter
* grape - management tool for local Grape cache
* groovyc - Groovy compiler, it allows you to compile Groovy sources into bytecode
* groovydoc - utility for generating API documentation from Groovy sources

There is also a graphical Groovy console:

* groovyConsole


## Joint compilation

Joint compilation means that Groovy compiler will compile Groovy and Java source files mixed together. To enable this feature, you may need to install Java compiler (if you don't have it already):

```
$ sudo dnf install java-1.8.0-openjdk-devel
```
