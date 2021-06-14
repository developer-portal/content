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

To install OPAM in your Fedora just:
```console
$ sudo dnf install opam
```

To use OPAM to install and manage your OCaml instalation just:
```console
# environment setup
$ opam init
$ eval $(opam env)
# install desired version of the compiler.
$ opam switch create 4.12.0
$ eval $(opam env)
# check you got what you want
$ ocaml -version
```

## References

- [OCaml Documentation](https://ocaml.org/docs/install.html)
- [OPAM Documentation](https://opam.ocaml.org/doc/Manual.html)
- [Functional Programming in OCaml](https://www.cs.cornell.edu/courses/cs3110/2019sp/textbook/)
