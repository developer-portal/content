---
title: Valkey
subsection: valkey
section: tech-database
description: In-memory data structure store, used as a database, cache and message broker
---

# Valkey

Valkey is a free and open source in memory data structure store forked from Redis. It is widely used as a database, in memory cache or a message broker.

## Quick start

To install Valkey on Fedora, run the following commands:

```console
$ sudo dnf install valkey     # Install valkey cli and server
$ sudo systemctl start valkey # Initialize valkey server
```

To start valkey on boot, run

```console
$ sudo systemctl enable valkey
```

To test valkey-cli, run

```console
$ valkey-cli ping
PONG
```

## Configuring Valkey

The config file for Valkey is located at `/etc/valkey/valkey.conf`.

```console
$ sudo nano /etc/valkey/valkey.conf
```

Valkey should be always restarted after changing settings. Restart valkey by running

```console
$ sudo systemctl restart valkey
```

Secure valkey by enabling authentication. Add this line in `/etc/valkey/valkey.conf`

```console
requirepass  <AuthPassword>
```

and after the Valkey server restarts, all clients must execute `AUTH <AuthPassword>` to be able to execute commands in Valkey.
