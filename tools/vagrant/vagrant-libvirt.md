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


## Manage guest networks via Vagrant

In Fedora `qemu://session` is used by default. This allows causes vagrant to run in userspace, not requiring password and being much safer. Downside is that not all Vagrant features are accessible, as they require root. To revert for your selected boxes to `qemu://system`:

- Fedora change: [https://fedoraproject.org/wiki/Changes/Vagrant_2.2_with_QEMU_Session](https://fedoraproject.org/wiki/Changes/Vagrant_2.2_with_QEMU_Session)
- Upstream documentation: [https://github.com/vagrant-libvirt/vagrant-libvirt#qemu-session-support](https://github.com/vagrant-libvirt/vagrant-libvirt#qemu-session-support)

## Using libvirt from Vagrant without password prompts


Using `libvirt` provider requires you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by adding yourself to the `libvirt` group:

```
$ sudo gpasswd -a ${USER} libvirt
$ newgrp libvirt
```
