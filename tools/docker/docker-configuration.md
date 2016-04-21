---
title: Configuring Docker
subsection: docker
order: 3
---

# Configuring Docker

The docker engine can be extensively configured.

## Basic configuration

If you want to add any command line options (like `-D` for debugging) to docker daemon/service, do it in `/etc/sysconfig/docker`. Check [Configuring and running Docker on Fedora/RHEL/CentOS](http://docs.docker.com/articles/configuring/#configuring-docker-1) and [Control and configure Docker with systemd](http://docs.docker.com/articles/systemd) for basic instructions.

Other area you might tweak is [Network configuration](https://docs.docker.com/engine/userguide/networking).

If you want to change setting of storage that docker engine uses, check [docker-storage-setup](http://www.projectatomic.io/docs/docker-storage-recommendation) script.

If you want to use your own registry, check [Docker Registry](http://docs.docker.com/registry). In that case you'll probably want to add `--add-registry` and/or `--insecure-registry` into `/etc/sysconfig/docker`.
