---
title: Vagrant with libvirt provider
page: vagrant
order: 2
---

# Vagrant with libvirt support installation

To use Vagrant with libvirt, you need to install the `vagrant-libvirt` package:

```
$ sudo dnf install vagrant-libvirt
```

There is also *@vagrant* package collection created with libvirt provider in mind. So you can use it to install all necessary Vagrant packages as well

```
$ sudo dnf install @vagrant
```


## Using libvirt from Vagrant without password prompts


Using `libvirt` provider requires you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by adding yourself to the `libvirt` group:

```
$ sudo gpasswd -a ${USER} libvirt
$ newgrp libvirt
```
