---
title: Autotools
subsection: c
order: 3
---

# Autotools

When you work on a project and you want to distribute this project among other users you also need to provide instructions about how to build the project.
Traditionally these instructions were provided in a file called `Makefile` which is basically a recipe that holds all the information
you need to build the package on your system. This can be achieved by using the command `make`. After initiating the command `make`
the system goes through the Makefile step by step and executes commands that are in it.

However, if you have a project that will be built on a different platform than it was developed on, your Makefile needs adjustments.
This is why the `configure` script was introduced. Configure script can automatically adjust the Makefile according to the system
requirements. The script probes the system for important information about the compilation and build processes and creates Makefiles for your project.

## Autotools installation

To install [GNU build system](https://en.wikipedia.org/wiki/GNU_build_system), also known as Autotools, you need to install autoconf and automake packages:

```
$ sudo dnf install autoconf automake
```

## Autotools usage

To create your own `configure` script, you need to create a few input files that will be used by `autoreconf` command which
creates the configure script. These files are `configure.ac` and `Makefile.am`. `Configure.ac` contains instructions to create `configure` script.
`Makefile.am` contains instructions for each directory, so there is one `Makefile.am` in each directory that your project contains.
You can find instructions about how to create these files in info page of `autoconf`. How to access the info page is described at the end.
When these files are ready, one simple command creates everything you need to distribute your project:

```
$ autoreconf --install
```

This command will produce several files: `configure` script, `config.h.in` and `Makefile.in` in every directory. The two latter are then used
by configure script to produce actual Makefiles. Now your project is ready to be distributed. Simply add these generated files to your
package. Now when someone wants to use your package she only needs to type:

```
$ ./configure
```

This command will produce `Makefile` in every directory and `config.h` in the main directory. Now simply type:

```
$ make
```

Now all important parts of project are compiled and linked and the program is ready to be used.
Note that this tutorial is very short and describes only absolute basics of GNU build system.
If you want to use `automake` in your project try reading the manual page:

```
$ man automake
```

If you need more detailed explanation of GNU build system and some simple examples of usage,
try this [guide to Autotools](http://www.freesoftwaremagazine.com/books/autotools_a_guide_to_autoconf_automake_libtool)
or info page:

```
$ info automake
```
