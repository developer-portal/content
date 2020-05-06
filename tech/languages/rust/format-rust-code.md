---
title: Format Rust code
subsection: rust
order: 3
---

# Format Rust code

`rustfmt` is a tool for formatting Rust source code. You can install it on Fedora by running:

```
$ sudo dnf install rustfmt
```

Now you can use `rustfmt` to format either a single file or the whole project:

* Single file:
```
$ rustfmt src/main.rs
```

* Project:
```
$ cargo fmt
```
