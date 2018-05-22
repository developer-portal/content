---
title: Downloading Vagrant images from Atlas
subsection: vagrant
order: 6
---

# Downloading Vagrant images from Atlas

HashiCorp hosts an [index](https://app.vagrantup.com/boxes/search)
of images that you can use with Vagrant. To download an image using 
Vagrant you need to know the organization name as well as the individual
image name. In the case of Fedora we have the [Fedora](https://app.vagrantup.com/fedora/)
organization and under that we have different boxes that can be used.
An example of one of those is the `fedora/{{page.fedora_release}}-cloud-base` Vagrant box.
You can download this box with the following command:

```
$ vagrant box add fedora/{{page.fedora_release}}-cloud-base
```

This will ask you which provider you want to download the Vagrant box
for. You can choose `libvirt` or `virtualbox` based on which one of
those virtual machine technologies you are using.

After downloading this image you can then start up a machine with:

```
$ vagrant init fedora/{{page.fedora_release}}-cloud-base && vagrant up
```

*NOTE* you can skip the `vagrant box add` command if you want to. The
`vagrant up` command will automatically consult Atlas for that named
box and download it if it exists.

# Upgrading Vagrant images from Atlas

If you want to update the Vagrant box image at a later time you can do
so by issuing the following command:

```
vagrant box update --box fedora/{{page.fedora_release}}-cloud-base
```
