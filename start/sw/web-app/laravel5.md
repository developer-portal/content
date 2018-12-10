---
title: PHP Laravel 5
subsection: web-app
order: 4
---

## Laravel 5
> The PHP Framework For Web Artisans

Laravel is a high-level PHP Web framework.

#### Install Nginx Web Server
Follow the nginx installation instructions [here](/start/sw/web-app/nginx.html).


#### Install MariaDB Relational Database Server
Follow the MariaDB installation instructions [here](/tech/database/mariadb/about.html).

Or you can install by : 
```bash
# install MariaDB
$ dnf install mariadb-server mariadb
# start MariaDB
$ systemctl enable --now mysql
# initialize MariaDB
$ sudo mysql_secure_installation
```

#### Install PHP and all its dependencies
Follow the PHP installation instructions [here](/tech/languages/php/php-installation.html).

```bash
# It will install all required extensions, perk of Fedora
$ sudo dnf install composer
```

#### Install Valet Linux
We will need to set it up for easier development. Valet is original designed for MacOS by the Laravel Team; Valet Linux is a port to that. It setups up the neccesary environments for PHP Development, including a test domain. Please do not run valet as root. 
For More Information, you can check them out here: 
https://cpriego.github.io/valet-linux/ 
https://laravel.com/docs/5.7/valet

```bash
# Place the ~/.config/composer/vendor/bin directory in your PATH so the composer 
# global executable can be located by your system.
$ echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc
# Install valet 
$ composer global require cpriego/valet-linux
# Initialize valet
$ valet install
```

#### Install laravel installer

```bash
$ composer global require "laravel/installer"
```

Restart Terminal. Now you can create a laravel project with the commands 

```bash
$ laravel new ProjectName
```

#### Setup

```bash
$ cd ProjectName
$ cp .env.example .env
$ gedit .env #or nano,vim,emacs
```

Edit the .env file with DB_* lines with the correct info

```javascript
DB_HOST=localhost
DB_DATABASE=laravel_equals_winning
DB_USERNAME=Chur
DB_PASSWORD=Chur1
```

#### Serve

###### Do not run valet in sudo
```bash
$ php artisan serve
# Laravel development server started on http://localhost:PORT/

# or use valet
$ valet park
$ valet link DOMAIN

# Now visit http://DOMAIN.test/
```

###### if ssl is desired

```bash
$ valet secure
# Now visit https://DOMAIN.test/

```

###### if need a callback URL/share work
```bash
$ valet share
```

