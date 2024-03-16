---
title: Further reading
subsection: rust
section: tech-languages
order: 4
---

# Learning resources

There is an official book describing the Rust programming language in detail.
[doc.rust-lang.org/book/](https://doc.rust-lang.org/book/index.html)

More examples of the concepts discussed in the book are available in this collection:
[doc.rust-lang.org/rust-by-example](https://doc.rust-lang.org/rust-by-example/)

When you finish with the language itself, there is an ongoing effort to create a set of examples of using core libraries for concurrency, data serialization, network programming, etc.
[rust-lang-nursery.github.io/rust-cookbook](https://rust-lang-nursery.github.io/rust-cookbook/intro.html)

Finally, you can find community pages with a list of resources such as this one:
[github.com/ctjhoa/rust-learning](https://github.com/ctjhoa/rust-learning)


# API documentation

Standard library documentation:
[doc.rust-lang.org/std](https://doc.rust-lang.org/std/)

The Cargo book:
[doc.rust-lang.org/cargo](https://doc.rust-lang.org/cargo/)

Documentation for crates available at [crates.io](https://crates.io/):
[docs.rs](https://docs.rs/)

# IDE recommendations

There are plugins for popular editor such as Vim, Atom or Gnome Builder which are based on the rust-analyzer implementation. Alternatively, IntelliJ IDEA provides their own, custom plugin. Unfortunatelly, the debugging support is available only in paid CLion IDE.

## Rustup

Before you try to configure your editor or IDE, it is recommended to install `rustup`

You can do so with DNF. Run:
```console
$ sudo dnf install rustup
```
The above command will install `rustup-init` command that you can then run to setup `rustup`.

Note that if you have installed rust via `dnf`, there may be warnings like:
```
warning: it looks like you have an existing installation of Rust at:
warning: /usr/bin
warning: It is recommended that rustup be the primary Rust installation.
warning: Otherwise you may have confusion unless you are careful with your PATH
warning: If you are sure that you want both rustup and your already installed Rust
warning: then please reply `y' or `yes' or set RUSTUP_INIT_SKIP_PATH_CHECK to yes
warning: or pass `-y' to ignore all ignorable checks.
error: cannot install while Rust is installed

Continue? (y/N)
```
This can be safely ignored as it is not known to cause any issues, simply answer with `y` and
continue.

To then register system installation with `rustup` run the following command:
```console
$ rustup toolchain link system /usr
```

Alternatively you install upstream `rustup` as described here: [rustup.rs](https://rustup.rs/).

## IDEs

If you want to start with Rust programming, it is easiest to try the rust-analyzer for Visual Studio Code:
 1. Install the VSCode RPM package: [code.visualstudio.com/docs/setup/linux](https://code.visualstudio.com/docs/setup/linux)
 2. Follow the instructions given at the extension Github page:  [https://rust-analyzer.github.io/manual.html#vs-code](https://rust-analyzer.github.io/manual.html#vs-code)

In case you prefer IDEs over editors, try the Intellij IDEA extension:
 1. Install the IDE (instructions are available under the "Installation Instructions" link): [www.jetbrains.com/idea/download/#section=linux](https://www.jetbrains.com/idea/download/#section=linux)
 2. Install the Rust plugin: [intellij-rust.github.io/docs/quick-start.html](https://intellij-rust.github.io/docs/quick-start.html)

Complete list of available options is here:
[areweideyet.com](https://areweideyet.com/)

# Other useful links

If you want to start with some web applications, a list of useful frameworks is available here:
[www.arewewebyet.org](http://www.arewewebyet.org/)

If you are brave enough and you want to try the nightly compiler edition (or you just want to try the awesome [Rocket framework](https://rocket.rs/)), it is recommended to use rustup:
[rustup.rs](https://rustup.rs/)
