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
