---
title: Perl modules
subsection: perl
order: 2
---

# Perl modules

Fedora currently ships with over three thousand of actively maintained Perl modules in its repositories; in most cases installing the module of your choice should be as simple as:

```
$ sudo dnf install 'perl(My::Module)'
```

If available, this is the preferred method.

If you require a module that is not already available, you may still install them with the common Perl utilities such as `cpan` from Perl core:

```
$ sudo cpan My::Module
```

or the popular `cpanm`:

```
$ sudo dnf install cpanminus
$ sudo cpanm My::Module
```

However, note that binary modules installed this way may seemingly inexplicably break after upgrading to a newer Fedora release.  The reason is Perl does not maintain binary compatibility between major versions.  If this happens, remember to reinstall the local modules with:

```
$ sudo cpan -f -i My::Module
```

or:

```
$ sudo cpanm --reinstall My::Module
```
