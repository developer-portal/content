---
title: Docker
page: Installation
section: tools
---

#**Getting started with Docker**

###**Installing Docker on Fedora**

####**Prerequisites**

Docker is currently supported on the following versions of Fedora:

* Fedora 20
* Fedora 21
* Fedora 22

Docker requires a **64-bit** version of Fedora and a minimum kernel version of **3.10**. 

The following command displays your kernel version and architecture:

```
$ uname -r
4.0.8-300.fc22.x86_64
```

If your kernel version is less than 3.10, you can update it using the following command:

```
$ sudo dnf update kernel
```

You need to restart your computer to boot with the new kernel version.

####**Installation**

The easiest way to install Docker on Fedora is from a Fedora package:

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

####**Creating a Docker group**

The Docker daemon binds to a Unix socket instead of a TCP port. By default that Unix socket is owned by the user `root` and other users can access it with `sudo`. For this reason, Docker daemon always runs as the `root` user.

To avoid having to use `sudo` when you use the Docker command, create a Unix group called Docker and add users to it. When the Docker daemon starts, it makes the ownership of the Unix socket read/writable by the Docker group.

**Warning:** The Docker group is equivalent to the `root` user; For details on how this impacts security in your system, see [Docker Daemon Attack Surface](https://docs.Docker.com/articles/security/#Docker-daemon-attack-surface) for details.

To create the Docker group and add your user:

```
$ sudo groupadd docker
$ sudo usermod -aG docker your_username
```

You have to log out and log back in for these changes to take effect. Then you can verify if your changes were successful by running Docker without `sudo`.

####**Start the Docker daemon at boot**

To make Docker start when you boot your system, use the command:

```
$ sudo systemctl enable docker
```

For additional Systemd configuration options for Docker, like adding an HTTP Proxy, reffer to Docker documentation [Systemd article](https://docs.docker.com/articles/systemd/)

###**Creating your first image**

TODO

###**Writing a Docker file**

TODO
