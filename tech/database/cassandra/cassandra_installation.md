---
title: Cassandra
subsection: cassandra
section: tech-database
description: OpenSource database server for high-scale application.
---

# Apache Cassandra

The Apache Cassandra database is the right choice when you need scalability and
high availability without compromising performance. Linear scalability and proven
fault-tolerance on commodity hardware or cloud infrastructure make it the perfect
platform for mission-critical data.

Cassandra is a partitioned row store. Rows are organized into tables with
a required primary key. Partitioning means that Cassandra can distribute your
data across multiple machines in an application-transparent matter. Cassandra
will automatically re-partition as machines are added/removed from the cluster.
Row store means that like relational databases, Cassandra organizes data by
rows and columns. The Cassandra Query Language (CQL) is a close relative of SQL.

## Quick start

Cassandra installation and service initialization on Fedora box:

```bash
$ sudo dnf install cassandra cassandra-server   # install client/server
$ sudo systemctl start cassandra                # initialize Cassandra server
```

To enable Cassandra to automatically start at boot time, run:

```
$ sudo systemctl enable cassandra
```

Basic command-line usage:

```bash
$ cqlsh                                         # run client tool
Connected to Test Cluster at 127.0.0.1:9042.
[cqlsh 5.0.1 | Cassandra 3.11.1 | CQL spec 3.4.4 | Native protocol v4]
Use HELP for help.
cqlsh> CREATE KEYSPACE k1 WITH REPLICATION = { 'class' : 'SimpleStrategy' ,  'replication_factor' : 1 };
cqlsh> USE k1;
cqlsh:k1> CREATE TABLE users (user_name varchar, password varchar, gender varchar, PRIMARY KEY (user_name));
cqlsh:k1> INSERT INTO users (user_name, password, gender) VALUES ('John', 'test123', 'male');
cqlsh:k1> SELECT * from users;

 user_name | gender | password
-----------+--------+----------
      John |   male |  test123

(1 rows)

```
