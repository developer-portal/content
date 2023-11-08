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

Writing Go programs is covered in [Go programs](/tech/languages/go/go-programs.html).

## Fedora Specific Notes

The default installation of Go on Fedora contains changes to the default values of `GOPROXY`, `GOSUMDB`, and `GOTOOLCHAIN` environment variables that Go developers should be aware of. The `go` command and related tools make extensive use of environment variables for configuration. Default values are set globally in `/usr/lib/golang/go.env`, and can be overridden on per user or per project basis.

For extensive help and information see:

```console
$ go help environment
```

### GOPROXY

The value of `GOPROXY` in `$GOROOT/go.env` is set to `direct`. A value of `direct` disables access to the module mirror. See [https://proxy.golang.org](https://proxy.golang.org) for more information on `GOPROXY` and the module mirror. A project specific `go.env` can override this setting. A user specific override can be set with:

```console
$ go env -w GOPROXY=https://proxy.golang.org,direct
```

### GOSUMDB

The value of `GOSUMDB` in `$GOROOT/go.env` is set to `off` replacing the default value of `sum.golang.org`. The GOSUMDB environment variable identifies the name of the checksum database used to help validate downloaded modules. A project specific `go.env` can override this setting. A user specific override can be set with:

```console
go env -w GOSUMDB=sum.golang.org
```

### GOTOOLCHAIN

Go 1.21 introduces `GOTOOLCHAIN` which facilitates project specific choices for the Go language toolchain of compiler, standard library, assembler, and other tools. The value of `GOTOOLCHAIN` is set to `local` instead of the default `auto`. When GOTOOLCHAIN is set to local, the go command always runs the bundled Go toolchain. See the [Go Toolchain](https://go.dev/doc/toolchain) documentation for more information on toolchains in Go. A project specific `go.env` file can override this setting. A user specific override can be set with:

```console
$ go env -w GOTOOLCHAIN=auto
```


## References

- [Go Documentation](https://golang.org/doc/)
- [Go Environment Variables](https://pkg.go.dev/cmd/go#hdr-Environment_variables)
- [Go Module Proxy](https://proxy.golang.org)
- [GOSUMDB Environment](https://goproxy.io/docs/GOSUMDB-env.html)
- [Go Toolchain](https://go.dev/doc/toolchain)
