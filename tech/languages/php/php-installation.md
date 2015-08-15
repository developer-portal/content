---
title: PHP
page: php
section: tech-languages
---

## PHP Installation

### PHP

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

### PEAR

The PHP Extension and Application Repository is a repository of PHP software code. 
To install PEAR, type:

```
# dnf install php-pear
```
Use pear command to install PEAR extensions. To install Mail_Mime package (for example), type:

```
# pear install Mail_Mime
```

You can [find more PEAR modules](http://pear.php.net/packages.php).

### PHP Developement Server

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