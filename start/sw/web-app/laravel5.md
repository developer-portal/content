---
title: PHP Laravel 5      
subsection: web-app
order: 4
---

## Laravel 5
> The PHP Framework For Web Artisans

Laravel is a high-level PHP Web framework 


First we need to install PHP5+, Composer and the laravel installer.
[Laravel](https://laravel.com/)
[Composer](https://getcomposer.org/)


#### Install MariaDB
```bash
$ sudo dnf install mariadb-server
# Then to boot the server 
$ sudo systemctl start mariadb.service
# And stop with
$ sudo systemctl stop mariadb.service
```
#### Install PHP
And extras
```bash
# Install php cli and needed extras
$ sudo dnf install php-cli php-mcrypt-5.6.20 php-mysqlnd
```
Now we will need composer to install laravel and it's dependancies 
```bash
# Use PHP to read the file and create an executable for composer
php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php
php composer-setup.php
php -r "unlink('composer-setup.php');"
# now move the composer executable to make composer globally accessable 
$ sudo mv composer.phar /usr/local/bin/composer
# You can now test it is working with 
composer -V
```
---
#### Create Laravel Project 
There are to ways to create a laravel project, 
Use Composer to install the laravel installer 
or 
Use Composer create-Project

###### Install laravel installer
```bash
composer global require "laravel/installer"
```
And the following line to ~/.bash_profile before "export Path"
```php
PATH=$PATH:$HOME/.composer/vendor/bin
```
Now you can create a laravel project with the commands 
```bash
laravel new ProjectName
```

###### Create Project with composer
```bash
composer create-project --prefer-dist laravel/laravel ProjectName
```
---



#### Now setup and serve your laravel project 

###### Setup
```bash
cd ProjectName
cp .env.example .env
gedit .env
```

Edit the .env file with DB_* lines with the correct info
```javascript
DB_HOST=localhost
DB_DATABASE=laravel_equals_winning
DB_USERNAME=Chur
DB_PASSWORD=Chur1
```
###### Serve
```bash
$ sudo systemctl start mariadb.service
php artisan serve
# Laravel development server started on http://localhost:8000/
```





