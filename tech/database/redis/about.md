---
title: Redis
subsection: redis
section: tech-database
description: In-memory data structure store, used as a database, cache and message broker
---

# Redis

Redis is a free and open source in memory data structure store. It is widely used as a database, in memory cache or a message broker.

## Quick start

To install Redis on Fedora, run the following commands:

```console
$ sudo dnf install redis     # Install redis cli and server
$ sudo systemctl start redis # Initialize redis server
```

To start redis on boot, run

```console
$ sudo systemctl enable redis
```

To test redis-cli, run

```console
$ redis-cli ping
pong
```

## Configuring Redis

The config file for Redis is located at `/etc/redis/redis.conf`.

```console
$ sudo nano /etc/redis/redis.conf
```

Redis should be always restarted after changing settings. Restart redis by running

```console
$ sudo systemctl restart redis
```

Secure redis by enabling authentication. Add this line in `/etc/redis/redis.conf`

```console
requirepass  <AuthPassword>
```

and after the Redis server restarts, all clients must execute `AUTH <AuthPassword>` to be able to execute commands in Redis.
