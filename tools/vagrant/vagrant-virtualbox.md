---
title: Vagrant with VirtualBox provider
subsection: vagrant
order: 3
---

# Vagrant with VirtualBox support installation

To use Vagrant with VirtualBox, you just need to install the `vagrant` package:

```
$ sudo dnf install vagrant
```

Vagrant itself comes with the support for VirtualBox baked-in. Unfortunately, VirtualBox is
not part of Fedora and needs to be installed separately from the [official project page](https://www.virtualbox.org/).

How to use Vagrant together with VirtualBox can be found in [Vagrant official documentation](https://docs.vagrantup.com/v2/).

## Using VirtualBox as a default

Fedora project cannot support VirtualBox provider in Fedora and therefore the default Vagrant
provider has been changed from VirtualBox to libvirt. To use VirtualBox provider with any Vagrant
commands, one has to explicitly append `--provider=virtualbox`.

To avoid this, you can set the default provider for your project in the beginning of your
Vagrantfile as:

```
# Vagrantfile
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'
...
```

Or set it for your environment with:

```
export VAGRANT_DEFAULT_PROVIDER=virtualbox
```
