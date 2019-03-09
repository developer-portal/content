---
title: SQLite
subsection: sqlite
section: tech-database
description: Software library that implements a self-contained server-less transactional SQL database engine.
---

# SQLite installation

To install basic SQLite (if it is not already), simply type:

```
$ sudo dnf install sqlite
```

This package provides the basic library and the command-line client `sqlite`. In
order to access SQLite databases from various programming languages (C, Tcl,
Java), the language bindings need to be installed separately:

```
$ sudo dnf install sqlite-devel sqlite-tcl sqlite-jdbc
```

## Graphical clients

The `sqlite` client shipped with the basic database engine is command line (CLI)
based. If you prefer an application with graphical user interface (GUI), install
the `sqlitebrowser` package:

```
$ sudo dnf install sqlitebrowser
```

## Working with SQLite

SQLite stores it's data in single database file. To open such file (which will
be created if necessary), pass it's name as CLI argument to `sqlite3`
executable:

```
$ sqlite3 hello-world.db
```

After executing this command, you will be greeted with a SQLite prompt and can
now insert the SQL commands to execute.

If you prefer using GUI, the [Sqlitebrowser][sqlitebrowser] application enables you to
construct your SQL queries using visual tool.

If you are new to SQL databases and would like to learn more, you can visit a
[W3CSchools SQL tutorial][sql-tut], which should give you a nice head start.

[sqlitebrowser]: https://sqlitebrowser.org/ "Sqlitebrowser home page"
[sql-tut]:   http://www.w3schools.com/sql/default.asp "W3CSchools SQL Tutorial"

## Getting help with SQLite

As is the custom in Fedora, SQLite documentation is available in `-doc`
sub-package. Additionally, the JavaDoc documentation for JDBC bindings is also
available:

```
$ sudo dnf install sqlite-doc sqlite-jdbc-javadoc
```

After the packages are installed, the actual documentation is located within `/usr/share/doc/PACKAGE` directory and is formatted in HTML. For example, to view documentation for SQLite itself, you can open this URL in your browser:

```
file:///usr/share/doc/sqlite-doc/index.html
```

If the documentation does not contain what you are looking for, you can visit
the project [homepage][sqlite-home], or ask in the [mailing lists][sqlite-lists].

[sqlite-home]:  https://sqlite.org/ "SQLite home page"
[sqlite-lists]: http://mailinglists.sqlite.org/cgi-bin/mailman/listinfo/sqlite-users "SQLite mailing list for users"
