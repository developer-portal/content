---
title: Docker images
subsection: docker
order: 4
---

# Docker images

Docker containers is a great concept to connect world of different distributions together. It is ideal tool to work with CentOS on Fedora, with Fedora on Red Hat Enterprise Linux or vise versa. That is the reason why we do not need to restrict our use cases on Fedora-based Docker containers only when we work on Fedora host machine, but we can use Docker containers based on CentOS or even Red Hat Enterprise Linux.

It is necessary to realize that when working with Docker containers, content of the image matters and is very important to trust it. Container itself is protected by cgroups and SELinux, but it still shares the kernel, so malicious container may theoretically harm the host system as well. See more information about security at [Docker Security](https://docs.docker.com/engine/security/security/) and [Project Atomic article](http://www.projectatomic.io/docs/docker-and-selinux/). Long story short, you should never run random image container on your production host.

## Fedora images

You can find all the official Docker images provided by Fedora community in the [official Fedora repository](https://hub.docker.com/_/fedora/) on Docker Hub.

Docker images in `fedora/` namespace feature `fedora:latest` tag for rawhide and `fedora:23` tag for Fedora 23.

To get Fedora 23 base image, run:

```
Pull the image from docker.io
$ sudo docker pull fedora:23
Run some command from the image
$ sudo docker run --rm -ti fedora:23 bash
```

There are also a lot of application Docker images built as layered images on top of Fedora base image. It's sources live in [Fedora Dockerfiles repository](https://github.com/fedora-cloud/Fedora-Dockerfiles) and are available under `fedora/` namespace on the Docker Hub.

For example, to pull and run the MariaDB Docker container, run:

```
Pull the image from docker.io
$ sudo docker pull fedora/mariadb
Run the container
$ sudo docker run fedora/mariadb
fedora/mariadb
```

The list of available Fedora Docker images is

## CentOS images

You can find find all the official Docker images provided by CentOS community in the [official CentOS repository](https://hub.docker.com/u/centos/) and the base Docker image in the [official library](https://hub.docker.com/_/centos/) on Docker Hub.

To get CentOS 7 base image, run:

```
Pull the image from docker.io
$ sudo docker pull centos:7
Run some command from the image
$ sudo docker run --rm -ti centos:7 bash
```

To get CentOS 6 base image, run:

```
Pull the image from docker.io
$ sudo docker pull centos:6
Run some command from the image
$ sudo docker run --rm -ti centos:6 bash
```

There is always `centos:latest` tag for the latest released version.

### Software Collections based images

The [official CentOS repository](https://hub.docker.com/u/centos/) contains Docker images that are similar to the images provided by Red Hat under `rhscl/` namespace.

These Docker images are based on [Software Collections](https://www.softwarecollections.org/en/). Some of them (older versions) are released under [the OpenShift organization](https://hub.docker.com/u/openshift/), the newer versions are available under [CentOS organization](https://hub.docker.com/u/centos/). Some of them are enabled for [Source-To-Image](https://github.com/openshift/source-to-image).

To download them just run `docker pull IMAGE_NAME`.

|    Image Name                   |    Description                            |
| :------------------------------ | ----------------------------------------- |
| centos/httpd-24-centos7	      | Apache HTTP 2.4 Server |
| centos/mariadb-100-centos7	  | MariaDB 10.0 SQL database server |
| centos/mongodb-26-centos7	      | MongoDB 2.6 NoSQL database server |
| centos/mysql-56-centos7	      | MySQL 5.6 SQL database server |
| centos/postgresql-94-centos7	  | PostgreSQL 9.4 SQL database server |
| centos/nginx-16-centos7	      | Nginx 1.6 server and a reverse proxy server |
| centos/nodejs-010-centos7	      | NodeJS 0.10 platform for building and running applications |
| centos/passenger-40-centos7	  | Phusion Passenger® 4.0 web server and application server |
| centos/perl-520-centos7	      | Perl 5.20 platform for building and running applications |
| centos/php-56-centos7	          | PHP 5.6 platform for building and running applications |
| centos/python-27-centos7	      | Python 2.7 platform for building and running applications |
| centos/python-34-centos7	      | Python 3.4 platform for building and running applications |
| centos/ror-41-centos7	          | Platform for building and running Ruby on Rails 4.1 applications |
| centos/ruby-22-centos7          | Ruby 2.2 platform for building and running applications |
| openshift/mysql-55-centos7      | MySQL 5.5 SQL database server |
| openshift/postgresql-92-centos7 | PostgreSQL 9.4 SQL database server |
| openshift/mongodb-24-centos7    | MongoDB 2.4 NoSQL database server |
| openshift/ruby-20-centos7       | Ruby 2.0 platform for building and running applications |
| openshift/python-33-centos7     | Python 3.3 platform for building and running applications |
| openshift/nodejs-010-centos7    | NodeJS 0.10 platform for building and running applications |
| openshift/perl-516-centos7      | Perl 5.16 platform for building and running applications |

