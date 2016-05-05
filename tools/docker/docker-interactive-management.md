---
title: sen — interactive management
subsection: docker
description: Manage your containers interactively!
---

`sen` is a terminal user interface for docker engine. It allows you to interact with docker within your terminal. You can:

 * start, stop, remove, inspect your containers and images
 * fetch logs, or even view logs real-time
 * searching and filtering with the interface
 * `sen` updates listing as events occur (e.g. you can `docker pull` an image in other terminal and it will become available automatically in the interface)
 * keybindings are inspired by vim
 * and much more!

Feel free to visit [original project](https://github.com/TomasTomecek/sen) page for more information.

<img src="/content/tools/docker/sen-preview.gif" width="97%">


## Installation

Very simple! Just run:

```
$ sudo dnf install -y sen
```


## Prerequisites

In case you haven't set up your docker instance, please follow [this guide](https://developer.fedoraproject.org/tools/docker/docker-installation.html).

Make sure that docker daemon is running:

```
$ systemctl is-active docker
```


## Usage

Run `sen` from your terminal:

```
$ sen
```

(`sen` requires access to docker, you may need to run it with root privileges if your user cannot access docker)

Then you will be presented with list of all your containers and images. You can navigate via arrows. Sample commands are:

 * `s` — start a container
 * `t` — stop a container
 * `d` — delete a container or an image
 * `f` — follow logs of a container
 * `l` — get all logs of a container
 * `i` — inspect a container or an image

For more commands, type `h` to access help page.
