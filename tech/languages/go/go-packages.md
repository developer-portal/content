---
title: Go packages
subsection: go
order: 3
---

# Go packages installation

## Go packages from upstream

Upstream projects can be installed with `go install` command, but only if they have `main` package. Package names follow the import paths so to install `github.com/go-delve/delve` from GitHub you need to reference the `main` package with a suffix like `@v1.2.3` or `@latest`.

To install a specific version run:
```console
$ go install github.com/go-delve/delve/cmd/dlv@v1.8.2
```

To install the highest available version run:
```console
$ go install github.com/go-delve/delve/cmd/dlv@latest
```

This will build and install the binary in `$GOPATH/bin`. If you have not added that to your `PATH` environment variable yet, you can do so with these commands:

```console
$ echo 'export PATH=$PATH:$GOPATH/bin' >> $HOME/.bashrc
$ source $HOME/.bashrc
```

## Go packages from Fedora

Alternatively, various Go packages are packaged and available in Fedora.

The package name idiom is that the import paths of libraries are fully qualified domain names. This way you have clarity to the precise upstream being used. By truncating domain names, using '-' instead of '/' and appending `-devel` suffix you know how is the associated Fedora package called. For example, 'github.com/gorilla/context' would become `golang-github-gorilla-context-devel`. Similarly, the 'code.google.com/p/go.net' repository would become `golang-googlecode-net-devel`.

To install `golang-googlecode-net-devel` package, you use DNF as usual:

```console
$ sudo dnf install golang-googlecode-net-devel
```

## References

- [Go Documentation: Deprecation of go get](https://go.dev/doc/go-get-install-deprecation)