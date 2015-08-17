---
title: Modules
page: perl
---

## Perl modules

Fedora currently ships with over three thousand of actively maintained Perl modules in its repositories; in most cases installing the module of your choice should be as simple as:

# dnf install 'perl(My::Module)'

If available, this is the preferred method.

If you require a module that isn't already available, you may still install them with the common Perl utilities such as `cpan` from Perl core:

```
# cpan My::Module
```

or the popular `cpanm`:

```
# dnf install cpanminus
# cpanm My::Module
```

However, note that binary modules installed this way may seemingly inexplicably break after upgrading to a newer Fedora release.  The reason is Perl doesn't maintain binary compatibility between major versions.  If this happens, remember to reinstall the local modules with:

```
# cpan -f -i My::Module
```

or:

```
# cpanm --reinstall My::Module
```
