---
title: Configuring Docker
subsection: docker
order: 3
---

# Configuring Docker

The docker engine can be extensively configured.

## Basic configuration

If you want to add any command line options (like `-D` for debugging) to docker daemon/service, do it in `/etc/sysconfig/docker`. Check [Control and configure Docker with systemd](https://docs.docker.com/engine/admin/systemd/) for basic instructions.

Other area you might tweak is [Network configuration](https://docs.docker.com/engine/userguide/networking).

If you want to change setting of storage that docker engine uses, check [docker-storage-setup](http://www.projectatomic.io/docs/docker-storage-recommendation) script.

If you want to use your own registry, check [Docker Registry](http://docs.docker.com/registry). In that case you'll probably want to add your registry to `/etc/containers/registries.conf` file.
