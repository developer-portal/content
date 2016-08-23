---
title: Rust
subsection: rust
section: tech-languages
order: 1
version: 1.10.0
description: Systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.
---

# Rust installation

In order to install Rust compiler, type:
```
$ sudo dnf install rust
```
This will install compiler (`rustc`), standard library, gdb support and documentation generator (`rustdoc`).

To compile a rust source code, simply type:
```
$ rustc test.rs
```
This will produce executable file named `test`.
