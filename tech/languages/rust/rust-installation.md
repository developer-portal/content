---
title: Rust
subsection: rust
section: tech-languages
order: 1
version: 1.43
description: Systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.
---

# Rust installation

## Installing Fedora's Rust distribution

Fedora's repositories provide packaged versions of Rust and its package manager. They can be installed as follows:

```console
$ sudo dnf install rust cargo
```

This command will install the `rustc` compiler, the standard library, gdb support, the `rustdoc` documentation generator and the `cargo` package manager.

## Installing Rust with rustup

Rust's [official installation instructions](https://www.rust-lang.org/learn/get-started) recommend its own installation mechanism, `rustup`.

To install the `rustup` installer run:

```console
$ sudo dnf install rustup
```

Run `rustup-init` after installing the package to start the Rust installation.

## Which one do I need?

It depends on your preferences. Some people may prefer prepackaged Rust because it automatically updates via `dnf`. Others may prefer a standardized installation. If you go for prepackaged Rust, keep this in mind:

- `cargo clippy` is not included in Fedora's `cargo` package, but is available via the `clippy` package.
- To enable autocompletions and other code intelligence features in your IDE, you may need to install the `rust-src` and `rustfmt` packages.

To avoid conflicts, do not use the `rust` and `rustup` packages side by side.