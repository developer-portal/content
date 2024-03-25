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

# crates.io repository
Rust calls its compilation unit (either library or executable) a crate. Your project
is such a crate and it can also depend on other crates specified in `Cargo.toml`. The
default repository to look for dependencies is [crates.io](https://crates.io/) but you
can also specify dependencies on a git repository.

**Note:** Cargo currently supports only source dependencies.
