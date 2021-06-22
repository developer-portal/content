---
title: OCaml
subsection: ocaml
section: tech-languages
order: 1
version: 1.0
description: An open source multi-paradigm programming language and toolchain. 
---

# What is OCaml?

OCaml is an industrial-strength programming language supporting functional, imperative and object-oriented styles.

## OCaml installation

To install the OCaml tools, type on a terminal:

```console
$ sudo dnf install ocaml ocaml-findlib 
```

The REPL (Read-Evaluate-Print-Loop) tool (`ocaml`), the library manager ( `ocamlfind`), the bytecode compiler (`ocamlc`), and the native-code compiler binaries (`ocamlopt`) will become available on the system. 

# OPAM

OPAM (**O**Caml **Pa**ckage **M**anager)  is a source-based package manager for OCaml. It supports multiple simultaneous compiler installations, flexible package constraints, and a Git-friendly development workflow.

### Installation

To install OPAM in your Fedora just:
```console
$ sudo dnf install opam
```

### Environment setup

You can use OPAM to install and manage your OCaml environment. First, it is necessary to add the environment variables in your default shell, OPAM does it for you when you run the `init` command, and after it, you can use `eval` in your first time to load the configuration.

```console
$ opam init
# the console will ask if you want to really modify your ~/.bashrc (or default), use 'y' to confirm.
$ eval $(opam env)
```

After adding the environment variables in your default shell you can install the desired version of OCaml compiler using the `switch` command and you can load the new environment variables running `eval` soon after it.

```console
$ opam switch create 4.12.0
$ eval $(opam env)
```

Now you can check if your OCaml version is the one you installed.

```console
$ ocaml -version
```

## References

- [OCaml Documentation](https://ocaml.org/docs/install.html)
- [OPAM Documentation](https://opam.ocaml.org/doc/Manual.html)
- [Functional Programming in OCaml](https://www.cs.cornell.edu/courses/cs3110/2019sp/textbook/)
