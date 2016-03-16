---
title: PHP
subsection: php
section: tech-languages
order: 1
version: 5.6.12
description: Server-side HTML embedded scripting language.
---

# PHP

## PHP Installation

To install PHP, simply type:

```
$ sudo dnf install php-cli
```

Above command will install latest stable PHP packages, which includes the command-line interface executing PHP scripts, `/usr/bin/php` executable, and the CGI interface.

You might want to install some other packages, e.g. PHPUnit for unit tests or Composer to manage dependencies of PHP projects. You can install them with:

```
$ sudo dnf install phpunit composer
```

## PHP modules

PHP provides only a few set of extensions, other should be installed separately. Packages of PHP modules are prefixed with `php-`, so if you need e.g. `mysqli` extension, use:

```
$ sudo dnf install php-mysqli
```

## PHP Development Server

PHP contains simple web server which can be used instead of full-featured web server. It is intended to be used only for development, not for a production environment.

You can start PHP development server by typing this in your project's root:

```
$ sudo php --server localhost:8080 --docroot  .
```
Server will be accessible on `http://localhost:8080/`.
