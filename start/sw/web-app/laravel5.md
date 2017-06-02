---
title: PHP Laravel 5
subsection: web-app
order: 4
---

## Laravel 5
> The PHP Framework For Web Artisans

Laravel is a high-level PHP Web framework.

#### Install Apache Web Server
Follow the Apache installation instructions [here](/start/sw/web-app/apache.html).

#### Install MariaDB Relational Database Server
Follow the MariaDB installation instructions [here](/tech/database/mariadb/about.html).

#### Install PHP
Follow the PHP installation instructions [here](/tech/languages/php/php-installation.html).

#### Install PHP Extensions

```bash
# Laravel required PHP extensions.
$ sudo dnf install php php-common php-cli php-pdo php-mbstring php-zip php-xml
# Restart Apache
$ sudo systemctl restart httpd
```

#### Install Composer
We will need composer to install laravel and it's dependencies

```bash
$ curl -sS https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer
$ chmod +x /usr/local/bin/composer
$ composer -V
```

#### Install laravel installer

```bash
$ composer global require "laravel/installer"
# Place the ~/.config/composer/vendor/bin directory in your PATH so the laravel 
# executable can be located by your system.
$ echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc
```

Restart Terminal. Now you can create a laravel project with the commands 

```bash
$ laravel new ProjectName
```

#### Setup

```bash
$ cd ProjectName
$ cp .env.example .env
$ nano .env
```

Edit the .env file with DB_* lines with the correct info

```javascript
DB_HOST=localhost
DB_DATABASE=laravel_equals_winning
DB_USERNAME=Chur
DB_PASSWORD=Chur1
```

#### Serve

```bash
$ php artisan serve
# Laravel development server started on http://localhost:PORT/
```
