---
title: Fortran
subsection: fortran
section: tech-languages
version: 11.1.1
order: 1
description: A general-purpose, imperative computer programming language, especially suited to numeric computation and scientific computing.
---
# Fortran installation and usage

## gfortran installation
Fortran is a compiled language and as such it needs a compiler. To install gfortran
compiler, simply type:

```
$ sudo dnf install gcc-gfortran
```

This command should download and install package with compiler called gfortran. Create a Fortran program `your_source.f90`. `.f90` is the standard file extension for modern Fortran source files. The 90 refers to the first modern Fortran standard in 1990. To compile and link the program, simply run the `gfortran` command like this:

```
$ gfortran your_source.f90
```

This will produce a binary file created from your source code. By default, this binary
file is named `a.out`.
You can run this binary by typing:

```
$ ./a.out
```

There are many options you can use when running the compiler. To specify the binary file name, you can use:

```
$ gfortran your_source.f90 -o your_binary
```

You can run this binary file by typing:

```
$ ./your_binary
```

To see the man page of `gfortran`, simply type:

```
$ man gfortran
```

## References

- [Fortran website](https://fortran-lang.org/)
