---
title: C
page: c
section: tech-languages
---

## C installation and usage

### GCC installation

C is a compiled language and as such it needs a compiler. To install a gcc compiler, simply type:

```
# sudo dnf install gcc
```

This command should download and install package with compiler called gcc.
To compile and link a program written in C, simply run the gcc like this:

```
# gcc your_source.c
```

This will produce a binary file created from your source code. By default, this binary file is named `a.out`. 
You can run this binary by typing:

```
# ./a.out
```

There are many options which you can use when running a compiler. These are some of the basic options used with gcc:

```
# gcc -std=c11 your_source.c -o your_binary
```
The option `-std=c11` states that the c11 or iso9899:2011 C language standard will be used when compiling your code. 
The `-o name` option simply states the name of the binary created by gcc.
To see all the options which you can use with gcc simply view its man page like this:

```
# man gcc
```

### CLANG installation
Gcc is just one of many compilers that are available for compiling C code. Another recently very popular compiler is clang. 
Clang is designed to provide a substitute to gcc. One of its primary goals is to provide more detailed information about the 
compilation process. Error reports are much more specific and readable than reports produced by gcc. Unfortunately, clang 
is a compiler only for C-like languages like C, C++, Objective-C and Objective-C++. Other languages like Java, Fortran etc. are still 
dependant on gcc.

If you want to install clang compiler, the instructions are similar to those used to install gcc:

```
# sudo dnf install clang
```

Clang is designed to have the same options as gcc. For example try this command:

```
# clang -std=c11 your_source.c -o your_binary
```

The command above should produce the same result as gcc. To see all the options that clang provides simply type:

```
# man clang
```