---
title: Julia
subsection: julia
section: tech-languages
version: 1.7.2
order: 1
description: High-level, high-performance dynamic language for technical computing
---
# Julia installation and usage

## julia installation
Julia is a high-level, high-performance dynamic programming language for technical computing, with syntax that is familiar to users of other technical computing environments. It provides a sophisticated compiler, distributed parallel execution, numerical accuracy, and an extensive mathematical function library. The library, largely written in Julia itself, also integrates mature best-of-breed C and Fortran libraries for linear algebra, random number generation, signal processing, and string processing.

```
$ sudo dnf install julia
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
