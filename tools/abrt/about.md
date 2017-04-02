---
title: ABRT
subsection: abrt
section: tools
description: Handle crashes of your applications automatically and debug with ease!
order: 1
---

# What is ABRT

[ABRT](https://abrt.readthedocs.org/en/latest/index.html) (Automatic Bug Reporting Tool)
is a set of tools to help users detect and report application crashes.
It's main purpose is to ease the process of reporting an issue and finding a solution.

ABRT can also be a valuable tool in developer's toolbox, helping with collecting
and debugging crashes in various programming languages.

Coupled with [FAF](https://github.com/abrt/faf/#about-faf) (Fedora Analysis Framework)
it provides extensive statistics about crashes of your application
over its complete life cycle.

## Using ABRT

ABRT is installed by default on most Fedora spins. You can verify its
functionality by forcefully crashing an application of your choice. We choose
`sleep` as our victim for demonstration purposes. Following commands
will run `sleep` in background and then kill it with 
<abbr title="Segmentation Fault (see $ man 7 signal)">SIGSEGV</abbr> signal to produce
a crash:

    sleep 10m &
    kill -SIGSEGV $!

When ABRT handles a crash you will get notified via desktop pop-up or console notification
if `abrt-desktop` or `abrt-console-notification` package is installed. You can then investigate the
crash via `gnome-abrt` GUI application or use `abrt-cli` when working from console.

It is always a good idea to test the ABRT functionality for applications
you are developing or maintaining in Fedora. If you are building your own RPMs
you might have to enable handling of non-GPG signed software. In case
ABRT failed to handle crash of your application consult troubleshooting
section of ABRT project documentation.

## Reporting

If the crashing application is part of Fedora you can leverage reporting to Fedora hosted
[FAF instance](https://retrace.fedoraproject.org/faf/summary/) and
[Red Hat Bugzilla](https://bugzilla.redhat.com).
This is one of the advantages of having a package included in official Fedora repositories
that allows developers and maintainers to receive bug reports from users of their application.

## New ABRT CLI

Available since Fedora 23 is the new ABRT CLI tailored specifically for developers.
It is part of a `abrt-cli-ng` package and can be installed with:

    $ sudo dnf install abrt-cli-ng

CLI is then available as `abrt` executable, try running it on your system:

    $ abrt

By default it lists crashes that belong to currently logged-in user. To get detailed
information about a last crash use `info` subcommand:

    $ abrt info

If `bash-completion` is installed on your system, the CLI can use it to complete
hashes of problems or package names for its subcommands:

    $ abrt backtrace <TAB>

If the last parameter specifying problem to use is omitted subcommand will work
with the last problem that occurred on the system.

To run [GDB](https://www.gnu.org/software/gdb/) against a last problem use:

    $ abrt gdb

To install debuginfo packages for the affected package use

    $ abrt debuginfo-install

These two can be combined to automatically install debuginfo packages prior
running gdb with:

    $ abrt gdb --debuginfo-install

To get the full list of commands and options use

    $ abrt --help

or

    $ abrt <subcommand> --help

## Further reading

Refer to [ABRT project documentation](https://abrt.readthedocs.org/)
for more information and configuration examples.
