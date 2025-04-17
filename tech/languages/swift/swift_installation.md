---
title: Swift
subsection: swift
section: tech-languages
order: 1
version: 5.6.2
description:  Swift is a high-performance system programming language. It has a clean and modern syntax, offers seamless access to existing C and Objective-C code and frameworks, and is memory safe by default.
---

# About Swift

[Swift](https://www.swift.org) is a high-performance system programming language. It has a clean and modern syntax, offers seamless access to existing C and Objective-C code and frameworks, and is memory safe by default.

Although inspired by Objective-C and many other languages, Swift is not itself a C-derived language. As a complete and independent language, Swift packages core features like flow control, data structures, and functions, with high-level constructs like objects, protocols, closures, and generics. Swift embraces modules, eliminating the need for headers and the code duplication they entail.

# Installing Swift

To install Swift on Fedora, simply type:

```console
$ sudo dnf install swift-lang
```

You can now start Swift's REPL (read-eval-print loop), which is an interactive session by invoking the `swift` command in the terminal. The Swift REPL will start like this:

```console
$ swift
Swift version 5.6.1 (swift-5.6.1-RELEASE)
Target: aarch64-unknown-linux-gnu

Welcome to Swift!

Subcommands:

  swift build      Build Swift packages
  swift package    Create and work on packages
  swift run        Run a program from a package
  swift test       Run package tests
  swift repl       Experiment with Swift code interactively (default)

  Use `swift --help` for descriptions of available options and flags.

  Use `swift help <subcommand>` for more information about a subcommand.

Welcome to Swift version 5.6.1 (swift-5.6.1-RELEASE).
Type :help for assistance.
  1>
```
Now, you can run Swift commands inside the REPL.

```console
  1> let x = 6
x: Int = 6
  2> let y = 7
y: Int = 7
  3> print("The answer is \(x * y)")
The answer is 42
  4>
```
To exit the REPL, press <kbd>Ctrl + D</kbd>.

Swift source files have the file extension `.swift`. Create a Swift program `your_source.swift`. You can compile the file using the command below:

```console
$ swiftc your_source.swift
```

This will compile the file and create an executable file `your_source` in the current directory.
You can run the file like so:
```console
$ ./your_source
```

To see the manual page of `swift`, simply type:

```console
$ man swift
```

## References

- [Swift Documentation](https://www.swift.org/documentation/)
