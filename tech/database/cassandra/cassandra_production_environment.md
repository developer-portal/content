## How to run Cassandra in production environment

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

Follow the instructions to "Enabling remote access to server" from cassandra_configuration.md
