---
title: Rebase helper
subsection: maintain
order: 2
---

# Rebase-helper
Rebase-helper is a tool which helps package maintainers with updating package to the latest upstream version.
It automates a lot of manual tasks the package maintainer usually does, when a new upstream version of a package is released.

## How to install rebase-helper
Begin installation on Fedora using the ``dnf`` command:

```
sudo dnf install -y rebase-helper
```

It requires several other programs like ``abipkgdiff``, ``rpmdiff``, ``mock``, ``fedpkg``, ``meld``, etc.
These programs are installed automatically as dependencies of rebase-helper.

Note: rebase-helper is also available as EPEL-7 package. Feel free to use it on CentOS and RHEL systems.

## How does the rebase-helper work?
Rebase-helper workflow can be summarized in following steps:

- Downloads an archive with new sources.
- Rebases downstream patches on top of the latest upstream version using git rebase command.
- If patching was successful, it builds two sets of RPMs. One using the ``old`` sources and a second one using the ``new`` sources. Available build tools are ``mock``, ``rpmbuild``, ``fedpkg``.
  - If ``new`` RPMs build fails, downloads logs like build.log and root.log
  - If the build is successful, downloads all available RPM packages.
- If all builds succeed, rebase-helper runs several checkers, like ``pkgdiff``, ``rpmdiff``, ``abipkgdiff``. Rebase-helper compares old and new packages and reports results.

## How to rebase your packages?
Let's say, we want to rebase a package foobar from ``foobar-1.2.0`` to ``foobar-1.2.1``.

To update to the latest upstream version execute command:

```
rebase-helper 1.2.1
```

If you do not want to be bothered, use option ``--non-interactive``
After rebase-helper finishes, check the output.

## Integration rebase-helper with an upstream monitoring service

This chapter demonstrates how to include rebase-helper in your upstream monitoring service. 
If you would like to integrate rebase-helper into your upstream monitoring services, this chapter is for you.
Rebase-helper provides an API which you can use either directly from Python, or directly from the command line.

### Patch new upstream version and start scratch builds
Example of patching new sources and starting scratch builds with fedpkg.
 This returns task_ids. The bash equivalents are included for comparison:
 
* ``Python API``

```
from rebasehelper.application import Application
cli = CLI([‘--non-interactive, ‘--builds-nowait’, ‘-buildtool’, ‘fedpkg’, upstream_version])
rh = Application(cli)
rh.set_upstream_monitoring() # Switch rebase-helper to upstream release monitoring mode.
rh.run()
```

* ``BASH``

```
rebase-helper --non-interactive --builds-nowait --buildtool fedpkg upstream_version
```

### Download logs and RPMs and compare with tools like abipkgdiff

* ``Python API``

```
cli = CLI([‘--non-interactive, ‘--builds-nowait’, ‘--fedpkg-build-tasks old_id,new-id])
rh.run() # Downloads RPMs, logs and runs checkers and provides logs.
rh.get_rebasehelper_data() # Get all information about the results
```

* ``BASH``

```
rebase-helper --non-interactive --builds-nowait --fedpkg-build-tasks old_id,new-id
```
