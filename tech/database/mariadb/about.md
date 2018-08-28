---
title: MariaDB
subsection: mariadb
section: tech-database
description: Transactional SQL database, an enhanced drop-in replacement for MySQL.
---

# MariaDB SQL database

[MariaDB](https://mariadb.org/en/about/) is a drop-in replacement of MySQL, forked by the community from the latter. To learn more about MariaDB, visit [upstream feature page](https://mariadb.com/kb/en/mariadb/mariadb-vs-mysql-features/), and to see main differences from MySQL, see [compatibility documentation](https://mariadb.com/kb/en/mariadb/mariadb-vs-mysql-compatibility/).

## What implementations of MySQL we have in Fedora
[MariaDB](https://src.fedoraproject.org/rpms/mariadb) is preferred MySQL implementation in Fedora. MariaDB can be usually used instead of MySQL as a drop-in replacement in most practical cases and most of the applications will work exactly the same. However, when you need to install Community MySQL, it is available as [community-mysql package](https://src.fedoraproject.org/rpms/community-mysql) in Fedora repositories.

Generally, most of the [documentation for MySQL](http://dev.mysql.com/doc/) is valid also for MariaDB.

## What versions do we have in Fedora

Fedora usually ships only the most recent stable version of MariaDB.
You can find various (unsupported) versions in the maintainer's [COPR repositories](https://copr.fedorainfracloud.org/coprs/mschorm/).
Learn more about current version at [upstream documentation](https://mariadb.com/kb/en/library/library-mariadb-releases/). The package is called `mariadb` (client tools) and `mariadb-server` (server daemon).

You can get an older version either by installing [Software Collection package of MariaDB 5.5](https://www.softwarecollections.org/en/scls/rhscl/mariadb55/) or by downloading [packages provided by upstream](https://downloads.mariadb.org/).

Fedora also ships MariaDB with Galera patch. The package with MariaDB Galera is called `mariadb-galera-server` and the wsrep plug-in is available in package `galera`. See section [How to install MariaDB Galera on Fedora](#how-to-install-mariadb-galera-on-fedora) for more information.

## How to install MariaDB on Fedora

In order to install MariaDB client package, run:

```
$ sudo dnf install mariadb
```

In order to install MariaDB server package, run:

```
$ sudo dnf install mariadb-server
```

If you need to connect to the MariaDB server using GUI, install either phpMyAdmin:

```
$ sudo dnf install phpMyAdmin
```

Or install Libre Office Base with JDBC plug-in for MariaDB:

```
$ sudo dnf install libreoffice-base mariadb-java-client
```

For connecting to the MariaDB server using ODBC, install `unixODBC` and `mariadb-connector-odbc` packages:

```
$ sudo dnf install mariadb-connector-odbc
```

## Basic tutorial for MariaDB in Fedora

MariaDB runs on port 3306 by default and creates a local unix socket at `/var/lib/mysql/mysql.sock`. By default, data is stored in the `/var/lib/mysql` directory and logs are located under `/var/log/mariadb/`. In order to change these directories, pay attention to use correct SELinux context and owner.

Right after installing, the data directory is empty. It is initialized during the first start.

To start MariaDB server, run:

```
$ sudo systemctl start mariadb
```

In order to setup MariaDB to start after system reboot, run:

```
$ sudo systemctl enable mariadb
```

The root user has no password set by default and so it is allowed to connect without the password:

```
mysql -u root
```

It is suggested to make the MariaDB more secure by running secure installation assistant:

```
$ sudo mysql_secure_installation
```

This tool asks you several questions and you are supposed to answer interactively. Do not provide the system administrator's password for your Linux system here. Use a different strong password, since this is a separate authentication for a MySQL user called "root."

## How to configure MariaDB

Configuration of both, client and server, is done by editing files `/etc/my.cnf`, `~/.my.cnf` and any files under `/etc/my.cnf.d/` with `.cnf` suffix. For more informations how to change configuration, see [the upstream documentation](https://mariadb.com/kb/en/mariadb/server-system-variables/#about-the-server-system-variables).

### How to configure MariaDB server for local development

When developing an application that uses MariaDB as the storage engine, developers typically use one user account that has full access to one dedicated database scheme. In order to do so, run the commands from section [Basic tutorial for MariaDB in Fedora](#basic-tutorial-for-mariadb-in-fedora) and then create the user and the dedicated database:

```
$ sudo systemctl start mariadb
$ sudo systemctl enable mariadb
$ sudo mysql_secure_installation
...My Account sudo mysql -u root -p
MariaDB [(none)]> create database db1;
Query OK, 1 row affected (0.00 sec)

MariaDB [(none)]> CREATE USER 'valeria'@'localhost' IDENTIFIED BY 'secretpass';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> GRANT ALL ON db1.* TO 'valeria'@'localhost';
Query OK, 0 rows affected (0.00 sec)

MariaDB [(none)]> exit
Bye
```

After that you may access the database from MariaDB command-line tool by running:

```
$ mysql -u valeria -p
```

By specifying  `-p` without password, you'll be asked for the password interactively.

In various frameworks or libraries, you will usually use the username, password and database to access the database.

### How to run MariaDB in production development

In order to run MariaDB in production development, you should pay extra attention to setting up the service in order to minimize the risk of being exploited. Among other things, this means:

 * use `mysql_secure_installation` as mentioned above
 * do not accept connections from all addresses unless absolutely necessary
 * **Always use a strong password**
 * Limit user permissions to those necessary for the application to run

By default, MariaDB cannot be accessed from another computer. In order to allow access from another computer, we need to do the following things.

Allow to accept connections on port 3306:

```
firewall-cmd --permanent --zone=public --add-port=3306/tcp
```

Allow to listen on all interfaces (or your preferred network interface) by adding configuration option:

```
bind-address = 0.0.0.0
```

### Other common configuration

In order to change configuration parameters for the MariaDB server, create the a configuration file under `/etc/my.cnf.d/` directory.

The following example shows content of the file `/etc/my.cnf.d/myconfig.cnf` which contains several commonly changed options (use any variables that matches your needs).

```
# The maximum permitted number of simultaneous client connections:
max_connections = 20

# The minimum length of the word to be included in a FULLTEXT index:
ft_min_word_len = 3

# The maximum length of the word to be included in a FULLTEXT index:
ft_max_word_len = My Account

# In case the native AIO is broken, it can be disabled by:
innodb_use_native_aio = 0

# Log slow queries:
slow_query_log = 1
slow_query_log_file = "/var/log/mariadb/slowquery.log"

# Log all queries (e.g. for debugging):
general_log = 1
general_log_file = "/var/log/mariadb/query.log"
```

After changing the configuration, restart the daemon using `$ sudo systemctl restart mariadb`.

## <a name="how-to-install-mariadb-galera-on-fedora"></a>How to install MariaDB Galera on Fedora

MariaDB Galera Cluster is a synchronous multi-master cluster for MariaDB.

In order to install MariaDB Galera server package, run:

```
$ sudo dnf install mariadb-galera-server galera
```

MariaDB Galera uses several packages from base MariaDB and also provides the same service name. Thus, for starting MariaDB Galera, run:

```
$ sudo systemctl start mariadb
```

## How to get MariaDB as Docker container

```
$ sudo docker pull fedora/mariadb
```

## How to extend MariaDB server by installing extensions available in Fedora

[MariaDB Connect Storage Engine](https://mariadb.com/kb/en/mariadb/connect/) enables MariaDB to access external local or remote data (MED). In order to install this engine, run:

```
$ dnf install mariadb-connect-engine
```

In order to install [The Open Query GRAPH computation engine](https://mariadb.com/kb/en/mariadb/oqgraph-storage-engine/), run:

```
$ dnf install mariadb-oqgraph-engine
```

## MariaDB server available as a dynamic library:

In Fedora, MariaDB server is available also as a dynamic library, that can be handy in some applications. This library (`libmysqld.so`) is available in the package `mariadb-embedded` and header files for building an application against this library are available in the package `mariadb-embedded-devel`.

However the use of the embedded library is discouraged. MySQL 8 dropped the embedded library and I expect MariaDB to go in the same direction.
