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

There is also *@vagrant* group available now so you can use that one as well. *@vagrant* group
was created with using libvirt provider in mind.


## Using libvirt from Vagrant without password prompts


Using `libvirt` provider requires you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by setting `polkit rules`
to allow Vagrant to use `libvirt` without explicit approvals. We include this file in `-doc`
sub-package. To get it, type:

```
$ sudo dnf install vagrant-libvirt-doc
```

And install the policy by copying the polkit `.rules` file:

```
$ sudo cp /usr/share/vagrant/gems/doc/vagrant-libvirt-0.0.30/polkit/10-vagrant-libvirt.rules /usr/share/polkit-1/rules.d/
```

This is an example for Fedora 23, for other versions change the version of `vagrant-libvirt` component in
the above path to the one installed.

As this package allows everyone in a `vagrant` group to access libvirt without password, you need to add yourself to this group to take advantage of the file:

```
$ sudo getent group vagrant >/dev/null || sudo groupadd -r vagrant
$ sudo gpasswd -a ${USER} vagrant
$ newgrp vagrant
```
