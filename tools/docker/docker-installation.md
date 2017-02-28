---
title: Getting started with Docker on Fedora
subsection: docker
order: 1
---

# Getting started with Docker

## Installation

On Fedora 22 and above install the `docker` package:

```
$ sudo dnf install docker
```

To start the Docker service use:

```
$ sudo systemctl start docker
```

Now you can verify that Docker was correctly installed and is running by running the Docker hello-world image.

```
$ sudo docker run hello-world
```

## Start the Docker daemon at boot

To make Docker start when you boot your system, use the command:

```
$ sudo systemctl enable docker
```

For additional systemd configuration options for Docker, like adding an HTTP Proxy, refer to the Docker documentation [Systemd article](https://docs.docker.com/articles/systemd/).

## Why can’t I use docker command as a non `root` user, by default?

The Docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user `root` and other users can access it with `sudo`. For this reason, Docker daemon always runs as the `root` user.

You can either [set up sudo](http://www.projectatomic.io/blog/2015/08/why-we-dont-let-non-root-users-run-docker-in-centos-fedora-or-rhel) to give docker access to non-root users.

Or you can create a Unix group called `docker` and add users to it. When the Docker daemon starts, it makes the ownership of the Unix socket read/writable by the `docker` group.

**Warning:** The `docker` group is equivalent to the `root` user; For details on how this impacts security in your system, see [Docker Daemon Attack Surface](https://docs.Docker.com/articles/security/#Docker-daemon-attack-surface) for details.

To create the `docker` group and add your user:

```
$ sudo groupadd docker && sudo gpasswd -a ${USER} docker && sudo systemctl restart docker
$ newgrp docker
```

You have to log out and log back in (or restart Docker daemon and use `newgrp` command as mentioned here) for these changes to take effect. Then you can verify if your changes were successful by running Docker without `sudo`.
