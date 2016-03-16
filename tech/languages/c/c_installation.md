---
title: C
subsection: c
section: tech-languages
version: 5.2.1
order: 1
description: A general-purpose, imperative computer programming language.
---

# C installation and usage

## GCC installation

C is a compiled language and as such it needs a compiler. To install a gcc compiler, simply type:

```
$ sudo dnf install gcc
```

This command should download and install package with compiler called GCC.
To compile and link a program written in C, simply run the `gcc` command like this:

```
$ gcc your_source.c
```

This will produce a binary file created from your source code. By default, this binary file is named `a.out`.
You can run this binary by typing:

```
$ ./a.out
```

There are many options which you can use when running a compiler. These are some of the basic options used with `gcc`:

```
$ gcc -std=c11 your_source.c -o your_binary
```

The option `-std=c11` states that the C11 or ISO/IEC 9899:2011 C language standard will be used when compiling your code.
The `-o name` option simply states the name of the binary created by `gcc` command.
To see all the options which you can use with `gcc` simply view its man page like this:

```
$ man gcc
```

### Compiling 32-bit binaries on a 64-bit Fedora

Let us assume you have a shiny modern computer with a 64-bit processor (AMD, Intel or similar compatible processor, this architecture is called x86_64 in Fedora) and installed 64-bit Fedora with gcc as per instructions above. GCC will naturally create 64-bit binaries suitable for your system. Yet sometimes for some sad reason you want to create a 32-bit binary (architecture like old Pentiums, called i686 in Fedora). Maybe you want to be compatible with some ancient piece of hardware or software. No matter the reason, first you need to

```
$ sudo dnf install libgcc.i686 glibc-devel.i686
```

If you use additional -devel packages, install them as well with the .i686 suffix. Then you can tell gcc to produce 32-bit binaries using "-m32" option:

```
$ gcc -m32 your_source.c -o your_binary
```


## CLANG installation

GCC is just one of many compilers that are available for compiling C code. Another recently very popular compiler is Clang.
Clang is designed to provide a substitute to GCC. One of its primary goals is to provide more detailed information about the
compilation process. Error reports are much more specific and readable than reports produced by GCC. Unfortunately, Clang
is a compiler only for C-like languages like C, C++, Objective-C and Objective-C++. Other languages like Java, Fortran etc. are still
dependant on GCC.

If you want to install clang compiler, the instructions are similar to those used to install GCC:

```
$ sudo dnf install clang
```

Clang is designed to have the same options as GCC. For example try this command:

```
$ clang -std=c11 your_source.c -o your_binary
```

The command above should produce the same result as `gcc` command. To see all the options that `clang` command provides simply type:

```
$ man clang
```
