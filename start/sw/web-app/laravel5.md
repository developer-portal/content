---
title: PHP Laravel 5      
subsection: web-app
order: 3
---

## Laravel 5
> The PHP Framework For Web Artisans

Laravel is a high-level PHP Web framework. We have to make sure all of these requirements are satisfied.

1. PHP >= 5.5.9
2. OpenSSL PHP Extension
3. PDO PHP Extension
4. Mbstring PHP Extension
5. Tokenizer PHP Extension

#### Install Apache Web Server
```bash
sudo dnf install httpd
# Setup Apache to automatically start upon system boot
sudo systemctl enable httpd.service
# Then to boot the server
sudo systemctl start httpd
# And stop with
sudo systemctl stop httpd
```

#### Install MariaDB Relational Database Server
```bash
sudo dnf install mariadb-server
sudo systemctl enable mariadb
# Then to boot the server
sudo systemctl start mariadb
# And stop with
sudo systemctl stop mariadb
sudo mysql_secure_installation
```

#### Install PHP and Extensions
```bash
# Enable remi repository for PHP 7
wget http://rpms.remirepo.net/fedora/remi-release-24.rpm
sudo dnf install remi-release-24.rpm
sudo dnf config-manager --set-enabled remi-php70
# Install PHP and Laravel required PHP extensions.
sudo dnf install php php-common php-cli php-pdo php-mbstring php-zip php-xml
# Restart Apache
sudo systemctl restart httpd
```

Now we will need composer to install laravel and it's dependancies
```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
chmod +x /usr/local/bin/composer
composer -V
```

###### Install laravel installer
```bash
composer global require "laravel/installer"
# Place the ~/.config/composer/vendor/bin directory in your PATH so the laravel 
# executable can be located by your system.
echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bash_profile
```

Now you can create a laravel project with the commands 
```bash
$ laravel new ProjectName
```

#### Now setup and serve your laravel project 

###### Setup
```bash
cd ProjectName
cp .env.example .env
nano .env
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
sudo systemctl start mariadb.service
php artisan serve
# Laravel development server started on http://localhost:PORT/
```
