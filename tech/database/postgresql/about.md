---
title: PostgreSQL
subsection: postgresql
section: tech-database
description: World's most advanced open source database.
---

<!--
TODOs
- mention somehow
  - database role == PostgreSQL
  - open postgresql monitoring (OPM)
- README.rpm-dist export to MD
- quickstart
  - python/perl/c/c++
-->

# PostgreSQL

PostgreSQL is an advanced Object-Relational database management system (DBMS).

Fedora distribution provides feature-full package set for PostgreSQL client and
server, server-compatible plug-ins and database connectors.

## Quick start

PostgreSQL installation on Fedora box and basic command-line usage:

```bash
$ sudo dnf install postgresql postgresql-server    # install client/server
$ sudo postgresql-setup --initdb --unit postgresql # initialize PG cluster
$ sudo systemctl start postgresql                  # start cluster
$ sudo su - postgres                               # login as DB admin
$ createdb quick-start                             # create testing database
$ psql -d quick-start                              # connect to the new database
psql (9.3.9)
Type "help" for help.

quick-start=# create table test (id int);       -- create testing table
CREATE TABLE
quick-start=# insert into test values (1);      -- insert some data
INSERT 0 1
quick-start=# select * from test;               -- query data
 id
----
  1
(1 row)

quick-start=#
```

# Controlling access to PG cluster (pg_hba.conf, users, passwords)

Sometimes it is useful to create a new user (with password) for specific database
applications.  There is set of utilities in the `postgresql` package (see
`rpm -ql postgresql | grep /usr/bin`) that may simplify some of those tasks.  Lets try to
create additional user, password and database:

```
$ sudo su - postgres
$ createuser testuser -P
Enter password for new role:
Enter it again:
$ createdb testdb --owner testuser
$ # add 'local all testuser md5' line **before** 'local all all peer' line
$ # (typical mistake is "just" appending the line at the and of the file)
$ vim ~/data/pg_hba.conf
$ cat ~/data/pg_hba.conf | grep ^local
local   all             testuser                                md5
local   all             all                                     peer
$ ^D
$ sudo systemctl restart postgresql
$ psql -d testdb -U testuser
Password for user testuser:
psql (9.3.9)
Type "help" for help.

testdb=>
```

## Documentation

Packaging documentation is available as [README.rpm-dist](https://fedoraproject.org/wiki/PostgreSQL/README.rpm-dist) in the `postgresql` package (client package).  Anybody running PostgreSQL on Fedora should start here:

```bash
$ rpm -qd postgresql | grep README.rpm-dist
/usr/share/doc/postgresql/README.rpm-dist
$ less /usr/share/doc/postgresql/README.rpm-dist
```

Install/use official documentation with:

```
$ sudo dnf install postgresql-docs
$ firefox /usr/share/doc/postgresql-docs/html/index.html         # HTML version
$ rpm -ql postgresql-docs | grep pdf
/usr/share/doc/postgresql-docs/postgresql-9.3.9-US.pdf
$ okular /usr/share/doc/postgresql-docs/postgresql-9.3.9-US.pdf  # PDF version
```

This documentation is also available [online](http://www.postgresql.org/docs/),
please choose the version you have installed on you Fedora.
You can look up the version by:

```
$ rpm -q postgresql --qf "%{VERSION}\n"
```

Other documentation available on-line:

* [Fedora PostgreSQL Homepage](https://fedoraproject.org/wiki/PostgreSQL)
* [PostgreSQL project](http://www.postgresql.org/about/)
* [PostgreSQL wiki](https://wiki.postgresql.org/wiki/Main_Page)


## Graphical DB management tools

* [pgadmin3](https://src.fedoraproject.org/rpms/pgadmin3)
* [phpPgAdmin](https://src.fedoraproject.org/rpms/phpPgAdmin)

## Extensions/Tools available in (Fedora/RHEL/EPEL packages)

* postgresql-contrib (bunch of extensions, see
  `rpm -ql postgresql-contrib | grep so$`), postgresql-plperl,
  postgresql-plpython, postgresql-plpython3, postgresql-pltcl (language bindings
  extending SQL syntax)
* [postgis](https://src.fedoraproject.org/rpms/postgis)
* [postgresql-pgpool-II](https://src.fedoraproject.org/rpms/postgresql-pgpool-II)
* [pg-semver](https://src.fedoraproject.org/rpms/pg-semver)
* [postgresql-ip4r](https://src.fedoraproject.org/rpms/postgresql-ip4r)

### How to use extensions:

PostgreSQL implements the [CREATE
EXTENSION](http://www.postgresql.org/docs/9.4/static/sql-createextension.html)
syntax (example with
[hstore](http://www.postgresql.org/docs/9.4/static/hstore.html) extension):

```
$ sudo dnf install postgresql-contrib           -- install extension (hstore)
$ sudo su - postgres                            -- switch user to DB admin
$ psql -d quick-start                           -- connect to an existing DB
psql (9.3.9)
Type "help" for help.

quick-start=# CREATE EXTENSION hstore;          -- install extension to actual db
CREATE EXTENSION
quick-start=# SELECT 'a=>1,b=>2'::hstore;       -- use the extension
  hstore
  ----------
   "a"=>"1"
   (1 row)
```

## Language connectors/adapters (packages)

* Python -- [python-psycopg2](https://admin.fedoraproject.org/pkgdb/packages/python-psycopg2)
* Perl -- [perl-DBD-Pg](https://admin.fedoraproject.org/pkgdb/packages/perl-DBD-Pg)
* Java -- [postgresql-jdbc](https://admin.fedoraproject.org/pkgdb/packages/postgresql-jdbc)
* Tcl -- [tcl-pgtcl](https://admin.fedoraproject.org/pkgdb/packages/tcl-pgtcl)
* ODBC -- [postgresql-odbc](https://admin.fedoraproject.org/pkgdb/packages/postgresql-odbc)

## PostgreSQL in containers

Currently there is a prepared Docker container for Fedora 21.  Documentation
is available on the [Fedora-Dockerfiles github
page](https://github.com/fedora-cloud/Fedora-Dockerfiles/tree/master/postgresql).

There is also a PostgreSQL image available
[for OpenShift](https://github.com/openshift/postgresql).
