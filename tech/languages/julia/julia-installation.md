---
title: Julia
subsection: julia
section: tech-languages
version: 1.7.3
order: 1
description: High-level, high-performance dynamic language for technical computing
---

# Julia installation and usage

## Julia installation

[Julia](https://julialang.org/) is a high-level, general-purpose language usually suited for numerical analysis and computational science. It provides a sophisticated compiler, distributed parallel execution, numerical accuracy, and an extensive mathematical function library. To install Julia on Fedora, simply type:

```bash
$ sudo dnf install julia
```

You can now start the Julia REPL (read-eval-print loop), which is an interactive session by invoking the `julia` command in the terminal. You can expect an output as below.

```bash
$ julia
               _
   _       _ _(_)_     |  Documentation: https://docs.julialang.org
  (_)     | (_) (_)    |
   _ _   _| |_  __ _   |  Type "?" for help, "]?" for Pkg help.
  | | | | | | |/ _` |  |
  | | |_| | | | (_| |  |  Version 1.7.3 (2022-05-06)
 _/ |\__'_|_|_|\__'_|  |  Fedora 36 build
|__/                   |

julia> 

```

Now, you can run julia commands inside the REPL.

```julia
julia> 1+1
2

julia> 

```

To exit the REPL, you can use <kbd>Ctrl + D</kbd> or type `exit()`.

Julia source files have the file extension `.jl`. Create a julia program `your_source.jl`. You can run the file using the command below:

```bash
$ julia your_source.jl
```

To see the manual page of `julia`, simply type:

```bash
$ man julia
```

## References

- [Julia Documentation](https://docs.julialang.org)
