---
title: Go installation
page: go
order: 1
---

## Go installation

To install Go compiler, type:

```
# dnf install go
```

`go` and `gofmt` binaries will become available on the system,
but you will still need to provide `$GOPATH` explicitly.

To set the `$GOPATH` to be your home directory, run:

```
$ echo 'export GOPATH=$HOME' >> $HOME/.profile
$ source $HOME/.profile
```

Run `go env` to check that `$GOPATH` is set correctly:

```
$ go env | grep GOPATH
GOPATH="/home/$USER"
```
