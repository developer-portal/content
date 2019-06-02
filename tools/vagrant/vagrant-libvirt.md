---
title: Vagrant with libvirt provider
subsection: vagrant
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

If you do not have KVM capabilities, you will need to use `qemu` driver within your Vagrantfile. Note the `qemu` driver may severely impact performance of your Vagrant virtual machine.

```
Vagrant.configure("2") do |config|
...
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "qemu"
  end
...
end
```

Read more on the `vagrant-libvirt` configuration in the [upstream documentation](https://github.com/vagrant-libvirt/vagrant-libvirt).

## QEMU session or system connection

The vagrant-libvirt plugin, as packaged for Fedora, has enabled the QEMU session connection instead of the system connection.
This means that you don't have to type your administrator password at all, but it comes with some limitations.
For example, you won't be able to use the private network options, like specifying the private IP address that you want a virtual machine to use.

If you want to switch to the system connection instead, use the following configurations:

```
Vagrant.configure("2") do |config|
...
  config.vm.provider :libvirt do |libvirt|
    # Use QEMU system instead of session connection
    libvirt.qemu_use_session = false
  end
...
end
```

Note that this will require the administrator password to run your vagrant boxes.
For more information on this, see the [upstream documentation](https://github.com/vagrant-libvirt/vagrant-libvirt#qemu-session-support)

## Using QEMU system connection without password prompts

Using the `libvirt` provider with QEMU system connection requires you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by adding yourself to the `libvirt` group:

```
$ sudo gpasswd -a ${USER} libvirt
$ newgrp libvirt
```
