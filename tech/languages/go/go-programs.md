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

If you get errors about missing packages, you may need to set a $GOROOT environment variable also. Fedora's `golang-src` package installs common packages into a GOROOT at `/usr/lib/golang` which should clear up most missing packages. Some distributions use `/usr/lib/golang` so this may be confusing for Fedora users reading docs from other distros. If you don't have root or sudo access, you may need to download your own [local GOROOT](https://go.dev/doc/manage-install) archive with basic packages into your home dir.

```console
$ sudo dnf install golang-src
$ export GOROOT=/usr/lib/golang
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

The command `go run` compiles and runs the named main Go program, and is useful for quick experiments.
To build the program along with the dependencies, you need to configure the modules first, and use `go build`:

```console
$ go mod init
go: creating new go.mod: module hello
go: to add module requirements and sums:
	go mod tidy
$ go mod tidy
$ go build
$ ls
go.mod  hello  hello.go
```

Without arguments, `go build` builds the package in the current directory, and in case of a main package it places a binary in the same directory. Let's try it:

```console
$ ./hello
Hello, Fedora!
```

Yet another option is to use `go install`. You still need to configure the modules as mentioned above:

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

- [Go Documentation: Create a Go module](https://go.dev/doc/tutorial/create-module)
