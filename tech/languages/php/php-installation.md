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


## Running your PHP Applications in Docker

After installing docker on your machine, you can start a web server with one command. The following will download a fully functional Apache installation with the latest PHP version, map `/path/to/your/php/files` to the document root, which you can view at `http://localhost:8080`

```
$ docker run -d --name my-php-webserver -p 8080:80 -v /path/to/your/php/files:/var/www/html/ php:apache

```

This will initialize and launch your container. `-d` makes it runs in the background. To stop and start it, simply run `docker stop my-php-webserver` and `docker start my-php-webserver` (the other parameters are not needed again)
