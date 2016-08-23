---
title: Rust
subsection: rust
section: tech-languages
order: 1
version: 1.10.0
description: Systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.
---

# Rust installation

In order to install the Rust compiler, type:
```
$ sudo dnf install rust
```
This will install the compiler (`rustc`), standard library, gdb support and a documentation generator (`rustdoc`).

To compile the Rust source code, type:
```
$ rustc test.rs
```
This will produce an executable file named `test`.
