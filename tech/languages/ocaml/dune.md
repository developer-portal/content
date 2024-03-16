---
title: Dune
subsection: ocaml
section: tech-languages
order: 2
---

# Dune

Dune is a build system for OCaml. It provides a comprehensive and uniform interface for the building, testing, and intalling OCaml projects, making it incredibly easy for developers to manage dependencies between packages. Its primary focus is to offer simplicity, speed, and ease of use, making it a suitable solution for even the most complex and extensive OCaml projects. With Dune, you can enjoy the benefits of incremental builds, which result in faster build times by recompiling only the necessary files. Moreover, Dune makes it convenient to generate optimized native code and perform static analysis, contributing to the development of high-performance and reliable OCaml applications.

## Install

You can install Dune with OPAM that we installed in the enviroment setup.

To install Dune using OPAM run:

```console
$ opam install dune
```

## Starting a new Project

Create a new directory for your project.

```console
$ mkdir yourprojectname
```

To initialize a Dune project change into the new directory and run the following command:

```console
$ cd yourprojectname
$ dune init
```

This will create the necessary files and directories for a basic Dune project, including a `dune` file and a `src` directory.

## Building the project

Change into the **root** directory of your project.
Run the following command to build the project:

```console
$ dune build
```

Dune will compile the source files and generate the necessary executables.

## Running the project

Change into the **root** directory of your project.
Run the following command to run the main executable:

```console
$ dune exec ./bin/your-executable.exe
```
> Replace `your-executable.exe` with the actual name of your executable.

## Adding a library to project

First, make sure you have the required library installed. You can use the following command to install a library using Opam:

```console
$ opam install library-name
```

Open the `dune` file in your project's root directory.
Add the following line to the `(library ...)` section to include the library:

```dune
(libraries library-name)
```

Replace `library-name` with the actual name of the library you want to add.
Save and close the `dune` file.
Rebuild the project using the following command:

```console
$ dune build
```

The added library should now be available for use in your project.
