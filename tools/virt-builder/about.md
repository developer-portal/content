---
title: Virt-builder
subsection: virt-builder
section: tools
description: Tool to quickly build (and customize) virtual machine images
---

# Virt-builder

[Virt-builder](http://libguestfs.org/virt-builder.1.html) is a tool for
quickly building new virtual machines.  You can build a variety of
VMs for local or cloud use, usually within a few minutes or less.
Virt-builder also has many ways to customize these VMs.  Everything is
run from the command line and nothing requires root privileges, so
automation and scripting is simple.

Note that `virt-builder` does not install guests from scratch.  It takes
cleanly prepared, digitally signed OS templates and customizes them.
This approach is used because it is much faster, but if you need to do
fresh installs you may want to look at
[`virt-install(1)`](https://github.com/virt-manager/virt-manager/blob/master/man/virt-install.pod)
and
[`oz-install(1)`](https://github.com/clalancette/oz/wiki/oz-install).

Refer to the [extensive
documentation of `virt-builder`](http://libguestfs.org/virt-builder.1.html).

## Installation

Virt-builder tool is provided as part of `libguestfs-tools-c` RPM
package in Fedora:

    $ sudo dnf install libguestfs-tools-c

## Simple usage

Build a minimal VM disk image:

    $ virt-builder fedora-27 --root-password password:123456

will build a Fedora 27 image (called 'fedora-27.img', in the current
working directory, which will later be imported into libvirt for use)
for the same architecture as virt-builder (so running it from an i386
installation will try to build an i386 image, if available).  This will
have all default configuration (minimal size, no user accounts, random
root password, only the bare minimum installed software, etc.).

Import the above disk image into libvirt:

    $ virt-install \
       --name f27vm1 --ram 2048 \
       --disk path=fedora-27.img,format=raw \
       --os-variant fedora27 \
       --import

Note: The `--os-variant` doesn't _strictly_ have to be F27; the nearest
possible available Fedora variant is fine.  To find the list of variants
for your current Fedora release, run: `osinfo-query os | grep fedora`.

## Examples to create custom virtual machines

###  Create an up-to-date Fedora 27 VM

Prepare a QCOW2 Fedora 27 VM, with 40GB disk size, and update to latest
available packages:

    $ virt-builder fedora-27 -o f27vm2.qcow2 --format qcow2 \
        --update --selinux-relabel --size 40G

Import the disk image into libvirt, and provide it 4GB of memory:

    $ virt-install --name f27vm2 --ram 4096 \
        --disk path=f27vm2.qcow2,format=qcow2,cache=writeback \
        --nographics --os-variant fedora27 --import

### Create a rawhide VM disk image

This creates a rawhide disk image:

    $ virt-builder fedora-27 \
        --install fedora-repos-rawhide \
        --edit '/etc/yum.repos.d/fedora-rawhide.repo: s/enabled=0/enabled=1/' \
        --update \
        --selinux-relabel --size 40G \
        --output rawhide-vm.img

Import it into libvirt with `virt-install` (as shown in previous
examples).

NOTE: The 'fedora-repos-rawhide' RPM can also be installed from
inside the image too:

    $ sudo dnf install fedora-repos-rawhide

## Manipulating the virtual machines

Use the libvirt shell interface `virsh(1)` or `virt-manager(1)` to
manipulate the VM.  A couple of examples:

Enumerate all virtual machines:

    $ sudo virsh list --all

Start a VM:

    $ sudo virsh start f27vm1

Take a snapshot of a running virtual machine:

    $ sudo virsh snapshot-create-as f27vm1 snap1 "Clean F27 VM"

NOTE: With this kind of snapshot, the original and its delta (the
snapshot) are stored in a single disk image file (convenient for moving
them across machines).  The VM disk image should be of QCOW2 format.

Revert to a specific snapshot:

    $ sudo virsh snapshot-revert f27vm1 snap1

Cleaning up VMs and their associated storage:

To gracefully shutdown and delete a virtual machine (including all its
associated disk images):

    $ sudo virsh stop f27vm1
    $ sudo virsh undefine f27vm1 --remove-all-storage

NOTE: The flag `--remove-all-storage` will delete the VM's disk image(s),
so ensure you took out relevant data from your VMs.
