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
$ cqlsh -u cassandra -p cassandra
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

```
$ sudo firewall-cmd --permanent --zone=public --add-port=9042/tcp
```

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

One of the main features of Apache Cassandra is its ability to run in a multi-node setup, providing the
following benefits:

- Fault tolerance: Data is automatically replicated to multiple nodes for fault-tolerance. Replication
across multiple data centers is supported. Failed nodes can be replaced with no downtime.

- Decentralization: There are no single points of failure. There are no network bottlenecks. Every node
in the cluster is identical.

- Scalability & Elasticity: Capability to run with dozens of thousands of nodes with petabytes of data.
Read and write throughput both increase linearly as new machines are added, with no downtime or interruption
to applications.

### Clearing existing data

If the server was started before or it's already running, all the existing data must be deleted, 
the reason for this is because all nodes must have the same ```cluster_name``` and it's better to
choose a different one from the default ```Test cluster``` name.

The following commands must be executed on each node:

```
$ sudo systemctl stop cassandra
$ sudo rm -rf /var/lib/cassandra/data/system/*
```

### Configuring the cluster

The Cassandra main configuration file ```/etc/cassandra/cassandra.yaml``` needs to be edited to setup the
cluster. The parameters that need to be modified are:

- ```cluster_name```: Name of your cluster.

- ```num_tokens```: Number of virtual nodes within a Cassandra instance. This is used to partition the data
  and spread the data throughout the cluster. The recommended value is 256.
  
- ```seeds```: Comma-delimited list of the IP address of each node in the cluster.

- ```listen_address```: The IP address or hostname that Cassandra binds to for connecting to other Cassandra
  nodes. It defaults to localhost and needs to be changed to the IP address of the node.
  
- ```rpc_address```: The listen address for client connections (CQL protocol).

- ```endpoint_snitch```:  Set to a class that implements the IEndpointSnitch. Cassandra uses snitches for
  locating nodes and routing requests. The default one is ```SimpleSnitch``` but we will change to
  ```GossipingPropertyFileSnitch``` which is more suitable for production environments:
  
  - ```SimpleSnitch```: Used for single-datacenter deployments or single-zone in public clouds. Does not
    recognize datacenter or rack information. It treats strategy order as proximity, which can improve cache
    locality when disabling read repair.

  - ```GossipingPropertyFileSnitch```: Recommended for production. The rack and datacenter for the local
    node are defined in the cassandra-rackdc.properties file and propagated to other nodes via gossip.
      
- ```auto_bootstrap```: This parameter is not present in the configuration file, so it has to be added and
  set to false. It makes new (non-seed) nodes automatically migrate the right data to themselves.

Configuration files for a 2-node cluster:

Node 1:

```
cluster_name: 'My Cluster'
num_tokens: 256
seed_provider:
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
        - seeds: 10.0.0.1, 10.0.0.2
listen_address: 10.0.0.1
rpc_address: 10.0.0.1
endpoint_snitch: GossipingPropertyFileSnitch
auto_bootstrap: false
```

Node 2:

```
cluster_name: 'My Cluster'
num_tokens: 256
seed_provider:
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
        - seeds: 10.0.0.1, 10.0.0.2
listen_address: 10.0.0.2
rpc_address: 10.0.0.2
endpoint_snitch: GossipingPropertyFileSnitch
auto_bootstrap: false
```

### Starting the cluster

The final step is to start each instance of the cluster, the seed instances must be started first,
then the remaing nodes.

```
$ sudo systemctl start cassandra
```

### Checking the cluster status

The cluster status can be checked with nodetool utility:

```bash
$ sudo nodetool status

Datacenter: datacenter1
===============
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address      Load       Tokens       Owns    Host ID                               Rack
UN  10.0.0.2  147.48 KB  256          ?       f50799ee-8589-4eb8-a0c8-241cd254e424  rack1
UN  10.0.0.1  139.04 KB  256          ?       54b16af1-ad0a-4288-b34e-cacab39caeec  rack1
 
Note: Non-system keyspaces don't have the same replication settings, effective ownership information is meaningless
```

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
