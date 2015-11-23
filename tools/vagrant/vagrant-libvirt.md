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

There is also *@vagrant* package collection created with libvirt provider in mind. With the following command you can install all necessary Vagrant packages as well:

```
$ sudo dnf install @vagrant
```

Afterwards make sure that libvirt daemon is running and that you have `kvm` module loaded in the kernel:

```
$ sudo systemctl enable libvirtd
$ lsmod | grep kvm
kvm_intel             167936  3
kvm                   499712  1 kvm_intel
```

If you do not have KVM capabilities, you will need to use `qemu` driver within your Vagrantfile as follows:

```
Vagrant.configure("2") do |config|
...
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
  end
...
end
```


## Using libvirt from Vagrant without password prompts


Using `libvirt` provider requires you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by adding yourself to the `libvirt` group:

```
$ sudo gpasswd -a ${USER} libvirt
$ newgrp libvirt
```
