---
title: Redis
subsection: redis
section: tech-database
description: In-memory data structure store, used as a database, cache and message broker
---

# Redis

Redis is a free and open source in memory data structure store. It is widely used as a database, in memory cache or a message broker.

# Quick start

Redis installation on fedora

```sh
$ sudo dnf install redis     # Install redis cli and server
$ sudo systemctl start redis # Initialize redis server
```

To start redis on boot, run

```sh
sudo systemctl enable redis
```

To test, run

```sh
$ redis-cli ping # output will be pong
```

# Configuring Redis

The config file for redis is located at `/etc/redis.conf`.

```sh
sudo nano /etc/redis.conf
```

Redis should be always restarted after changing settings. Restart redis by running

```sh
sudo systemctl restart redis
```

Secure redis by enabling authentication. Add this line in redis.conf

```sh
requirepass  <AuthPassword>
```

and after redis server restart, all clients must execute `AUTH <AuthPassword>` to execute commands in redis.