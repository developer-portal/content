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

Cassandra installation and service initalization on Fedora box:

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

## How to configure Cassandra

Server configuration is done by editing the file `/etc/cassandra/cassandra.yaml`. For more
informations how to change configuration, see the the [upstream documentation](https://docs.datastax.com/en/archived/cassandra/3.x/cassandra/configuration/configCassandra_yaml.html).

### Controlling access to Cassandra database (users, passwords)

By default, authentication is disabled and to enable it you have to do the following steps:

1. Change the authenticator option in the cassandra.yaml file to `PasswordAuthenticator`:

```
authenticator: PasswordAuthenticator
```

By default, the authenticator option is set to `AllowAllAuthenticator`.

2. Restart Cassandra.

3. Start `cqlsh` using the default superuser name and password:

```
cqlsh -u cassandra -p cassandra
```

4. Create a new superuser:

```
cqlsh> CREATE ROLE <new_super_user> WITH PASSWORD = '<some_secure_password>' 
    AND SUPERUSER = true 
    AND LOGIN = true;
```

5. Log in as the newly created superuser:

```
$ cqlsh -u <new_super_user> -p <some_secure_password>
```

6. The cassandra superuser cannot be deleted from Cassandra. To neutralize the account, change the password to something long and incomprehensible, and alter the user's status to NOSUPERUSER:

```
cqlsh> ALTER ROLE cassandra WITH PASSWORD='SomeNonsenseThatNoOneWillThinkOf'
    AND SUPERUSER=false;
```

### Enabling remote access to server

Edit the `/etc/cassandra/cassandra.yaml` file, changing the following parameters:

```
listen_address: external_ip
rpc_address: external_ip
seed_provider/seeds: "<external_ip>"
```

### Other common configuration

Setting the name of the cluster. This needs to be consistent for all nodes that you intend to have in this cluster:

```
cluster_name: 'Test Cluster'
```

Set the directory where cassandra will write too, below is the default that will be used if unset. If possible
set this to a disk used only for storing cassandra data:

```
data_file_directories:
    - /var/lib/cassandra/data
```

Set which type of disk cassandra is using to store data on ssd or spinning:

```
disk_optimization_strategy: ssd|spinning
```

### How to run Cassandra in production environment

In order to run Cassandra in production environment, you should pay extra attention
to setting up the service in order to minimize the risk of being exploited. Among
other things, this means:

- do not accept connections from all addresses unless absolutely necessary
- Always use a strong passwordd
- Limit user permissions to those necessary for the application to run

By default, Cassandra cannot be accessed from another computer. In order to allow access from
another computer, we need to do the following things.

Allow to accept connections on port 9042:

firewall-cmd --permanent --zone=public --add-port=9042/tcp

Follow the previous instructions to "Enabling remote access to server"

## Log file

The package logs to `/var/log/cassandra/system.log` by default.

## nodetool utility

The nodetool utility is a command-line interface for monitoring Cassandra and performing routine
database operations.

```bash
$ sudo nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address    Load       Tokens       Owns (effective)  Host ID                               Rack
UN  127.0.0.1  143.43 KiB  256          100.0%            94becf56-8a2a-4935-bdf0-79e24694d207  rack1
```

## Running a Cassandra cluster

## Documentation

[Cassandra Datastax documentation](https://docs.datastax.com/en/cassandra/3.0/)

[The Cassandra Query Language (CQL)](http://cassandra.apache.org/doc/latest/cql/index.html)

[Recommended Production Settings For Apache Cassandra](https://docs.datastax.com/en/dse/5.1/dse-admin/datastax_enterprise/config/configRecommendedSettings.html)

## Language connectors/adapters/drivers (packages)

* Python -- [python3-cassandra-driver](https://src.fedoraproject.org/rpms/python-cassandra-driver)
* Java -- [cassandra-java-driver](https://src.fedoraproject.org/rpms/cassandra-java-driver)

## Cassandra in containers

There is a Cassandra image available
[for OpenShift](https://github.com/sclorg/cassandra-container).
