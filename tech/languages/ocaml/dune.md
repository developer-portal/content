---
title: Dune
subsection: ocaml
order: 2
---

# Dune

Dune is a build system for OCaml. It provides a comprehensive and uniform interface for the building, testing, and intalling OCaml projects, making it incredibly easy for developers to manage dependencies between packages. Its primary focus is to offer simplicity, speed, and ease of use, making it a suitable solution for even the most complex and extensive OCaml projects. With Dune, you can enjoy the benefits of incremental builds, which result in faster build times by recompiling only the necessary files. Moreover, Dune makes it convenient to generate optimized native code and perform static analysis, contributing to the development of high-performance and reliable OCaml applications.

## Install

You can install Dune with OPAM that we installed in the enviroment setup. For do it just run:

```console
$ opam install dune
```

## Starting a new Project

1. Create a new directory for your project.

```console
$ mkdir yourprojectname
```

2. Change into the new directory and run the following command to initialize a Dune project:

```console
$ cd yourprojectname
$ dune init
```

3. This will create the necessary files and directories for a basic Dune project, including a `dune` file and a `src` directory.

## Building the project

1. Change into the **root** directory of your project.
2. Run the following command to build the project:

```console
$ dune build
```

3. Dune will compile the source files and generate the necessary executables.

## Running the project

1. Change into the **root** directory of your project.
2. Run the following command to run the main executable:

```console
$ dune exec ./bin/your-executable.exe
```
> Replace `your-executable.exe` with the actual name of your executable.

## Adding a library to project

1. First, make sure you have the required library installed. You can use the following command to install a library using Opam:

```console
$ opam install library-name
```

2. Open the `dune` file in your project's root directory.
3. Add the following line to the `(library ...)` section to include the library:

```dune
(libraries library-name)
```

4. Replace `library-name` with the actual name of the library you want to add.
5. Save and close the `dune` file.
6. Rebuild the project using the following command:

```console
$ dune build
```

7. The added library should now be available for use in your project.
