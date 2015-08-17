---
title: PHP
page: php
section: tech-languages
---

## PHP

### PHP Installation

To install PHP, simply type:

```
# dnf install php-cli
```

Above command will install latest stable PHP package, which includes the command-line interface executing PHP scripts, /usr/bin/php, and the CGI interface. 


You might want to install some other packages, e.g. phpunit for unit tests or composer to manage dependencies of PHP projects. You can install them with:

```
# dnf install phpunit composer
```

### PHP modules
PHP provides only a few set of extensions, other should be installed separately. For example, if you need "mysqli" extension, use:

```
# dnf install php-mysqli
```

### PHP Development Server

PHP contains simple web server which can be used instead of full-featured web server. It is intended to be used only for development, not for a production environment. 

You can start PHP Development Server by typing this in your project's root:

```
# php --server localhost:8080 --docroot  .
```
Server will be accessible on http://localhost:8080/ .


### Frameworks

We have packaged two popular PHP frameworks in Fedora: Zend and Symfony. 

To install Zend framework, type:

```
# dnf install php-ZendFramework2
```

To install Symfony, type:

```
# dnf install php-symfony
```