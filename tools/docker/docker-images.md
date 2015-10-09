---
title: Docker images
page: docker
order: 4
---

# Docker images

## Fedora images

Here is the [official Fedora repository](https://hub.docker.com/_/fedora/).

It features `fedora:latest` tag for rawhide and `fedora:22` tag for Fedora 22.

To get Fedora 22 image, run:

```
$ sudo docker pull fedora:22
```

## CentOS images

Here is the [official CentOS repository](https://hub.docker.com/_/centos/).

To get CentOS 7 image, run:

```
$ sudo docker pull centos:7
```

To get CentOS 6 image, run:

```
$ sudo docker pull centos:6
```

There is always `centos:latest` tag for the latest released version.

### Software Collections based images

You can also get Docker images based on [Software Collections](https://www.softwarecollections.org/en/) which are currently released under [the OpenShift organization](https://hub.docker.com/u/openshift/). Some of them are enabled for [Source-To-Image](https://github.com/openshift/source-to-image).

To download them just run `docker pull openshift/IMAGE_NAME`.

- `php-56-centos7`: PHP 5.6 platform for building and running applications
- `python-34-centos7`: Python 3.4 platform for building and running applications
- `python-27-centos7`: Python 2.7 platform for building and running applications
- `perl-520-centos7`: Perl 5.20 platform for building and running applications
- `ruby-22-centos7`: Ruby 2.2 platform for building and running applications
