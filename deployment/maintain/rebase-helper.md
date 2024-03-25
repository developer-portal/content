---
title: Rebase helper
subsection: maintain
order: 2
---

# Rebase-helper
Rebase-helper is a tool which helps package maintainers with updating package to the latest upstream version.
It automates a lot of manual tasks the package maintainer usually does, when a new upstream version of a package is released.

## Install rebase-helper
Begin installation on Fedora using the ``dnf`` command:

```sh
$ sudo dnf install rebase-helper
```

It requires several other programs like ``abipkgdiff``, ``rpmdiff``, ``mock``, ``fedpkg``, ``meld``, etc.
These programs are installed automatically as dependencies of rebase-helper.

Note: rebase-helper is also available as EPEL-7 package. Feel free to use it on CentOS and RHEL systems.

## How does rebase-helper work?
Rebase-helper workflow can be summarized in following steps:

- Downloads an archive with new sources.
- Rebases downstream patches on top of the latest upstream version using git rebase command.
- If patching was successful, it builds two sets of RPMs. One using the **old** sources and a second one using the **new** sources. Available build tools are ``mock``, ``rpmbuild``, ``fedpkg``.
  - If **new** RPMs build fails, downloads logs like `build.log` and `root.log`
  - If the build is successful, downloads all available RPM packages.
- If all builds succeed, rebase-helper runs several checkers, like ``pkgdiff``, ``rpmdiff``, ``abipkgdiff``. Rebase-helper compares **old** and **new** packages and reports results.

## How to rebase your packages?
Let's say we want to rebase a package foobar from ``foobar-1.2.0`` to ``foobar-1.2.1`` using rebase-helper:

```sh
# Change to the location of foobar.spec and other package components (cloned dist-git dir), e.g.
$ cd $HOME/rpmbuild/REPOS/foobar

# Update to the selected upstream version
$ rebase-helper 1.2.1
```

If you do not want to be bothered, add the ``--non-interactive`` option to rebase-helper's command line 

After rebase-helper finishes, check the output.

