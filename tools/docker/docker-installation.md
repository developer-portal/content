---
title: Getting started with Docker on Fedora
subsection: docker
order: 1
---

# Getting started with Docker

## Installation

Install the `docker-ce` package using the Docker repository:

To install the dnf-plugins-core package (which provides the commands to manage your DNF repositories) and set up the stable repository.

```console
$ sudo dnf install dnf-plugins-core
```
To add the `docker-ce` repository

```
$ sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo
```

To install the docker engine 

```console
$ sudo dnf install docker-ce docker-ce-cli containerd.io
```

Afterwards you need to enable the backward compatability for Cgroups

```console
$ sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"
```

> Note: You must reboot after running the command for the changes to take effect


To start the Docker service use:

```console
$ sudo systemctl start docker
```

Now you can verify that Docker was correctly installed and is running by running the Docker hello-world image.

```console
$ sudo docker run hello-world
```

## Start the Docker daemon at boot

To make Docker start when you boot your system, use the command:

```console
$ sudo systemctl enable docker
```

For additional systemd configuration options for Docker, like adding an HTTP Proxy, refer to the Docker documentation [Systemd article](https://docs.docker.com/engine/admin/systemd/).

## Why can’t I use docker command as a non `root` user, by default?

The Docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user `root` and other users can access it with `sudo`. For this reason, Docker daemon always runs as the `root` user.

You can either [set up sudo](http://www.projectatomic.io/blog/2015/08/why-we-dont-let-non-root-users-run-docker-in-centos-fedora-or-rhel) to give docker access to non-root users.

Or you can create a Unix group called `docker` and add users to it. When the Docker daemon starts, it makes the ownership of the Unix socket read/writable by the `docker` group.

**Warning:** The `docker` group is equivalent to the `root` user; For details on how this impacts security in your system, see [Docker Daemon Attack Surface](https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface) for details.

To create the `docker` group and add your user:

```console
$ sudo groupadd docker && sudo gpasswd -a ${USER} docker && sudo systemctl restart docker
$ newgrp docker
```

You have to log out and log back in (or restart Docker daemon and use `newgrp` command as mentioned here) for these changes to take effect. Then you can verify if your changes were successful by running Docker without `sudo`.
