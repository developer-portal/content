---
title: PHP Laravel 5
subsection: web-app
order: 4
---

## Laravel 5
> The PHP Framework For Web Artisans

Laravel is a high-level PHP MVC framework. It is also the most used PHP framework today. For more information, [click here](https://laravel.com/). 

This guide will help you setup your local development environment for Laravel, and it applies to setting up Lumen as well.


## Dependencies for Laravel
#### Install Nginx Web Server
Laravel Valet and Laravel recommends using Nginx. Follow the nginx installation instructions [here](/start/sw/web-app/nginx.html).

You can also choose [Apache](/start/sw/web-app/apache.html) as the web server.

#### Install MariaDB Relational Database Server (Or other database you prefer)
Follow the MariaDB installation instructions [here](/tech/database/mariadb/about.html).

#### Setup environment for PHP development
Follow the PHP installation instructions [here](/tech/languages/php/php-installation.html).

OR, you can rip the benefit of using Fedora, and install composer directly instead. This will install PHP, and all the required extensions/libraries needed.
```bash
# It will install all required extensions, perk of Fedora
$ sudo dnf install composer
```

Your web server needs to be restarted after installing PHP package.

#### Install Valet Linux
We will need to set it up for easier development. Valet is original designed for MacOS by the Laravel Team; Valet Linux is a port to that. It setups up the neccesary environments for PHP Development, including a test domain. Please do not run valet as root. 
For More Information, you can check them out here: 
[Valet Linux](https://cpriego.github.io/valet-linux/)  and  [Laravel Valet](https://laravel.com/docs/5.7/valet)

You can also setup Laravel using [Vagrant](/tools/vagrant/about.html), [Docker](/tools/docker/about.html).

```bash
# Place the ~/.config/composer/vendor/bin directory in your PATH so the composer 
# global executable can be located by your system.
$ echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc
# Install valet 
$ composer global require cpriego/valet-linux
# Initialize valet
$ valet install
```
## Setup Laravel

#### Install laravel installer

```bash
# Install Laravel Installer
$ composer global require "laravel/installer"
# use Laravel Installer to Create a new Laravel Project
$ laravel new ProjectName
```

#### Setup

```bash
$ cd ProjectName
$ cp .env.example .env
#Editing your environment file
$ gedit .env 
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

# or use valet
$ valet park
$ valet link DOMAIN

# Now visit http://DOMAIN.test/
```

##### If ssl is desired

```bash
$ valet secure
# Now visit https://DOMAIN.test/

```

##### If need a callback URL/an URL over the internet
```bash
$ valet share
```
