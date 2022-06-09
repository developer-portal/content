---
title: Installing libvirt and virt-install on Fedora Linux  
subsection: virtualization  
order: 3  
---

# Installing libvirt and virt-install on Fedora Linux

## Common terms

### Libvirt

Libvirt is an open-source API, daemon and management tool for managing platform virtualization. It can be used to manage KVM, Xen, VMware ESXi, QEMU and other virtualization technologies. These APIs are widely used in the orchestration layer of hypervisors in the development of a cloud-based solution.

The Libvirt project:  
- is a toolkit to manage virtualization platforms
- is accessible from C, Python, Perl, Go and more
- supports KVM, QEMU, Xen, Virtuozzo, VMWare ESX, LXC, BHyve and more
- targets Linux, FreeBSD, Windows and macOS
- is used by many applications

[Read more about Libvirt here](https://libvirt.org/)

### Virt-install

virt-install is a command line tool for creating new KVM , Xen, or Linux container guests using the "libvirt" hypervisor management library. See the EXAMPLES section at the end of this document to quickly get started.

virt-install tool supports both text based & graphical installations, using VNC or SDL graphics, or a text serial console. The guest can be configured to use one or more virtual disks, network interfaces, audio devices, physical USB or PCI devices, among others.

The installation media can be held locally or remotely on NFS , HTTP , FTP servers. In the latter case "virt-install" will fetch the minimal files necessary to kick off the installation process, allowing the guest to fetch the rest of the OS distribution as needed. PXE booting, and importing an existing disk image (thus skipping the install phase) are also supported.

Given suitable command line arguments, "virt-install" is capable of running completely unattended, with the guest 'kickstarting' itself too. This allows for easy automation of guest installs. An interactive mode is also available with the --prompt option, but this will only ask for the minimum required options.

[Read more about Virt-install here](https://linux.die.net/man/1/virt-install)

## Installing steps

1. Execute the following command to install libvirt on the host device, if not already installed.  
   ```console
   $ sudo dnf install libvirt -y
   ```
   ![01](/content/tools/virtualization/images/installing-libvirt-and-virt-install-on-fedora-linux/01.png)
2. Execute the following command to install virt-install on the host device, if not already installed.
   ```console
   $ sudo dnf install virt-install -y
   ```
   ![02](/content/tools/virtualization/images/installing-libvirt-and-virt-install-on-fedora-linux/02.png)

## Usages

1. [Setting up Fedora Workstation domain on libvirt](/tools/virtualization/setting-up-fedora-workstation-domain-on-libvirt.html)
