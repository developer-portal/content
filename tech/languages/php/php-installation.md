---
title: PHP
page: php
section: tech-languages
---

## PHP Installation

### PHP

To install PHP, simply type:

```
# dnf install php
```

Above command will install latest stable PHP
packages including some additional modules. 

### Web server

To fully make use of PHP you will probably
want to install web server. 
Apache is one of the recommended and easy to
set up. To install Apache, type:

```
# dnf install httpd
```

Above command will install latest Apache web server.
Default working directory is /var/www/html.

To enable Apache autostart on boot, type:

```
# systemctl enable httpd.service
```

To start Apache, type:

```
# systemctl start httpd.service
```

### MySQL server

PHP applications can use MySQL server to store data.
To install MySQL server (Mariadb) type:

```
# dnf install mariadb mariadb-server php-mysql
```

To enable Mariadb autostart on boot:

```
# systemctl enable mariadb.service
```

To start Mariadb, type:

```
# systemctl start mariadb.service
```
