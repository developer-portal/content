---
title: Cargo
subsection: rust
order: 2
---

# Installing Cargo
Cargo is Rust's package manager. You can use it to download your project's dependencies
and to compile your project. You can start a new project using Cargo by typing:
```
$ cargo new my_project
```
This will create a new directory with manifest (`Cargo.toml`), a source code directory
(`src`) and a "Hello, World!" program in `src/main.rs`.
```
$ cd my_project/
$ tree .
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```

The manifest is written in [TOML language](https://github.com/toml-lang/toml) and
looks like this:
```toml
[package]
name = "my_project"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

[dependencies]
```

To run your new project, type:
```
$ cargo run
   Compiling my_project v0.1.0 (file:///home/fedora/rust/my_project)
     Running `target/debug/my_project`
Hello, world!
```

# Using Rust libraries ("crates")
Rust calls its compilation unit (either library or executable) a crate. Your project
is such a crate and it can also depend on other crates specified in `Cargo.toml`. The
default repository to look for dependencies is [crates.io](https://crates.io/) but you
can also specify dependencies on a git repository. More information about all the
different ways of specifying dependencies is available in the
[cargo book](https://doc.rust-lang.org/cargo/reference/specifying-dependencies.html).

While many Rust crates are also packaged for Fedora Linux (as `rust-$crate`, with
`rust-$crate-*-devel` packages available from the package repositories), the crates
packaged this way are primarily intended to be used for building RPM packages for Rust
applications. Using these crates as a replacement for [crates.io](https://crates.io/)
is not a supported use case. In some cases they also diverge from crates as published
on crates.io because of downstream-specific patches (both concerning crate dependencies
and behaviour), so they might not even be a suitable development target.

**Note:** Both crates.io and Fedora only distribute Rust crates as source code. Rust
does not yet provide a stable ABI, so it is not possible to distribute pre-compiled Rust
crates / libraries in a binary format.
