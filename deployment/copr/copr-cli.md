---
title: Copr command line interface
subsection: copr
---

# Copr command line interface

[Copr](https://copr.fedoraproject.org/) features a command line interface that can help you with managing projects, submitting builds, etc.

## Setup

Install the copr-cli package:

```
$ sudo dnf install copr-cli
```

Log into the Copr web interface and get your API token at the [Copr API Page](https://copr.fedorainfracloud.org/api/)

3. Save the token to your system:

```
$ vim ~/.config/copr
```

## Creating a new project

To create a new project called `test-project`, which would provide packages for Fedora 22, type:

```
$ copr-cli create --chroot fedora-22-i386 --chroot fedora-22-x86_64 test-project
```

## Submitting a build

There are curently two ways of getting your SRPM(s) into Copr:

A. Building from URL:

```
$ copr-cli build test-project http://www.example.com/package-1.6-1.fc22.src.rpm
```

B. Uploading them into Copr directly:  

```
$ copr-cli build test-project ~/packages/package-1.6-1.fc22.src.rpm
```

The command line tool will now monitor your build and keeps you updated about any changes and results. You can safely interrupt it with `ctrl+c` at any time. The build will continue running.

## Adding a repository and installing the package

Now, when your build has been finished, you can add the repository and install your package:

First, make sure you have installed dnf core plugins:

```
$ sudo dnf install dnf-plugins-core
```

Enable your repository:

```
$ sudo dnf copr enable your_name/test-project
```

And install the package:

```
$ sudo dnf install package
```
