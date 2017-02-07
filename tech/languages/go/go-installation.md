---
title: Go
subsection: go
section: tech-languages
order: 1
version: 1.7
description: An open source programming language built to craft simple, reliable, and efficient software.
---

# Go on Fedora

Quoting the upstream documentation:

> The Go programming language is an open source project to make programmers more productive.

> Go is expressive, concise, clean, and efficient. Its concurrency mechanisms make it easy to write programs that get the most out of multicore and networked machines, while its novel type system enables flexible and modular program construction. Go compiles quickly to machine code yet has the convenience of garbage collection and the power of run-time reflection. It's a fast, statically typed, compiled language that feels like a dynamically typed, interpreted language.

## Go installation

To install the Go tools, type on a terminal:

```console
$ sudo dnf install golang
```

The `go` and `gofmt` binaries will become available on the system.

Go code lives in [a workspace](https://golang.org/doc/code.html#Workspaces) which is defined by the `GOPATH` environment variable. A common choice among developers, and the [default value of `GOPATH` starting from the Go 1.8 release](https://tip.golang.org/doc/code.html#GOPATH), is to use `$HOME/go`:

```console
$ mkdir -p $HOME/go
$ echo 'export GOPATH=$HOME/go' >> $HOME/.bashrc
$ source $HOME/.bashrc
```

Check that `GOPATH` is set correctly with this command:

```console
$ go env GOPATH
/home/user/go
```

Where 'user' will be your user name.

## Writing programs

To write programs in Go, we write files with the `.go` extension in a subdirectory of `$GOPATH/src`. These are the steps:

```console
$ mkdir -p $HOME/go/src/hello
$ cd $HOME/go/src/hello
$ touch hello.go
```

Now, edit the file `hello.go` with your favorite editor and type the following:

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, Fedora!")
}
```

Save your changes and, still on the same directory (`$HOME/go/hello`), run:

```console
$ go run hello.go
Hello, Fedora!
```

The command `go run` builds and runs a Go program, and is useful for quick experiments.
To build the program and generate a compiled binary, use `go build`:

```console
$ go build
$ ls
hello  hello.go
```

Without arguments, `go build` builds the package in the current directory, and in case of a main package it places a binary in the same directory. Let's try it:

```console
$ ./hello
Hello, Fedora!
```

Yet another option is to use `go install`:

```console
$ go install
$ ls
hello.go
$ ls $GOPATH/bin
hello
```

After building the current package, `go install` places the binary in `$GOPATH/bin`, instead of the current directory. It also builds and caches all dependencies in `$GOPATH/pkg`, making this command specially useful for bigger programs, such that `go install` can be faster than `go build` because of the cache.

Because programs are installed in `$GOPATH/bin`, it is common to add that to the `PATH` environment variable, so that you can run your Go programs without specifying their full path:

```console
$ echo 'export PATH=$PATH:$GOPATH/bin' >> $HOME/.bashrc
$ source $HOME/.bashrc
$ hello
Hello, Fedora!
```

## References

- [Go Documentation](https://golang.org/doc/)
