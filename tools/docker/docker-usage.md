---
title: Docker basics
subsection: docker
order: 2
---

# Docker basics

## Getting started with images

Use [docker images](https://docs.docker.com/engine/reference/commandline/images/) to see what images you have locally on your host.

```
$ sudo docker images
```

Use [docker search](https://docs.docker.com/engine/reference/commandline/search/) to see what images are available on [Docker Hub](https://hub.docker.com).

```
$ sudo docker search fedora
```

## Running a container

Use `docker run` to run an application inside a container.
The following command pulls Fedora image, creates a container from it and runs Bash shell inside it.

```
$ sudo docker run -it fedora bash
```

Other useful [options](https://docs.docker.com/engine/reference/run/#operator-exclusive-options) to use with `run` are for example `-d` to run a container in background (to daemonize it) or `--name` to give container a name which you can later use with `docker stop/start`.

See also [Docker run reference](https://docs.docker.com/engine/reference/run/).

Other useful commands regarding running containers are for example:

* [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) to list running containers
* [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) to stop running container and [docker start](https://docs.docker.com/engine/reference/commandline/start/) to start stopped container
* [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) to look inside container
* [docker exec](https://docs.docker.com/engine/reference/commandline/exec/) to enter running container, like: `docker exec -it [container-id] bash`

## Creating an image

If you change anything (like install new packages in the above example with Bash) in the running container and exit the container the changes are not automatically saved into the Fedora image.
If you want to save them in an image, use [docker commit](https://docs.docker.com/engine/reference/commandline/commit/).

Another option how to create an image is by building it from Dockerfile, see below.

## Writing a Dockerfile

There are already existing Dockerfiles in [Fedora-Dockerfiles](https://github.com/fedora-cloud/Fedora-Dockerfiles) repository. You can use them as examples for creating your own Dockerfile. Each directory contains a Dockerfile and a README with instructions how to build the image and run a container from it.

A Dockerfile content can be as simple as:

```
FROM fedora:latest
CMD env
```

For description of instructions used in Dockerfile see [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) and [Best practices for writing Dockerfiles](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)

## Building an image from Dockerfile

In a directory with a Dockerfile run

```
$ sudo docker build -t "my-image" .
```

If the build is successful you can see the `my-image` image in `docker images` output.

See also [Build your own image](https://docs.docker.com/engine/getstarted/step_four/) and [Building an image from a Dockerfile](https://docs.docker.com/engine/getstarted/step_four/#step-2-build-an-image-from-your-dockerfile) for more thorough description.
