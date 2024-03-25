---
title: PEAR
subsection: php
order: 2
---

# PEAR Installation

The PHP Extension and Application Repository is a repository of PHP software code.
To install PEAR, type:

```
$ sudo dnf install php-pear
```

## Upstream PEAR modules

Use `pear` command to install PEAR extensions. To install `Mail_Mime` package (for example), type:

```
$ sudo pear install Mail_Mime
```

You can find more PEAR modules [at official PEAR site](http://pear.php.net/packages.php).

## PEAR modules from official Fedora repositories

Many PEAR modules are packaged and available in base Fedora to install. Not all these packages have `php-pear-`` prefix to upstream PEAR names, so you can browse [list of them online](http://rpms.remirepo.net/rpmphp/rpm.php?type=pear).

To install `Mail_Mime` you therefore install `php-pear-Mail-Mime` package:

```
$ sudo dnf install php-pear-Mail-Mime
```
