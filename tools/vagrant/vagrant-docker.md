---
title: Vagrant with Docker provider
subsection: vagrant
order: 4
---

# Vagrant with Docker support installation

To use Vagrant with Docker, you need to install the `vagrant` and `docker` packages:

```
$ sudo dnf install vagrant docker
```

And start `docker` service:

```
$ sudo systemctl start docker
```

Vagrant itself comes with the support for Docker baked-in. By installing Docker alongside
Vagrant you can start using Docker both as a provider and as a provisioner. Please refer to
the [official documentation](https://docs.vagrantup.com/v2/) for more.

Note: All Vagrant commands have to be ran as root (e.g. with `sudo`). This is similar to running
Docker commands directly.

## Using Docker as a default

To use Docker provider with any Vagrant commands, one has to explicitly append `--provider=docker`.

To avoid this, you can set the default provider for your project in the beginning of your
Vagrantfile as:

```
# Vagrantfile
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
...
```

Or set it for your environment with:

```
export VAGRANT_DEFAULT_PROVIDER=docker
```

## Using Docker from Vagrant without password prompts

To use Vagrant with Docker without password prompts it is enough to add yourself to the `docker`
group. This will make `docker` commands password-less as well.

To do so, type:

```
$ sudo groupadd docker && sudo gpasswd -a ${USER} docker && sudo systemctl restart docker
$ newgrp docker
```

Above commands will create the group `docker` and add current user to this group. This user
also need to have administrator privileges.

Note: This has security implications, read about this in the [official docs](https://docs.docker.com/articles/security/#docker-daemon-attack-surface).
