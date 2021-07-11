---
title: Fortran
subsection: fortran
section: tech-languages
version: 
order: 1
description: A general-purpose, imperative computer programming language.
---
# Fortran installation and usage

## gfortran installation
Fortran is a compiled language and as such it needs a compiler. To install gfortran
compiler, simply type:

```
$ sudo dnf install gcc-gfortran
```

This command should download and install package with compiler called gfortran. To compile
and link a program written in Fortran, simply run the `gfortran` command like this:

```
gfortran your_source.f
```

This will produce a binary file created from your source code. By default, this binary
file is named `a.out`.
You can run this binary by typing:

```
$ ./a.out
```

To see the man page of `gfortran`, simply type:
```
$ man gfortran
```
