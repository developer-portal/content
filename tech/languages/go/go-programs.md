---
title: Writing Go programs
subsection: go
order: 2
---

# Writing Go programs

This assumes you have already [installed Go](/tech/languages/go/go-installation.html#go-installation).

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

Save your changes and, still on the same directory (`$HOME/go/src/hello`), run:

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
