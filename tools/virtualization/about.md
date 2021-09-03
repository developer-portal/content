---
title: Virtualization  
subsection: virtualization  
section: tools  
description: Run virtual machines at near-native speeds and manage them at ease  
---

# Virtualization

## QEMU 

QEMU is a generic and open source machine & userspace emulator and virtualizer.

QEMU is capable of emulating a complete machine in software without any need for hardware virtualization support. By using dynamic translation, it achieves very good performance. QEMU can also integrate with the Xen and KVM hypervisors to provide emulated hardware while allowing the hypervisor to manage the CPU. With hypervisor support, QEMU can achieve near native performance for CPUs. When QEMU emulates CPUs directly it is capable of running operating systems made for one machine (e.g. an ARMv7 board) on a different machine (e.g. an x86_64 PC board).

QEMU is also capable of providing userspace API virtualization for Linux and BSD kernel interfaces. This allows binaries compiled against one architecture ABI (e.g. the Linux PPC64 ABI) to be run on a host using a different architecture ABI (e.g. the Linux x86_64 ABI). This does not involve any hardware emulation, simply CPU and syscall emulation.

QEMU aims to fit into a variety of use cases. It can be invoked directly by users wishing to have full control over its behaviour and settings. It also aims to facilitate integration into higher level management layers, by providing a stable command line interface and monitor API. It is commonly invoked indirectly via the libvirt library when using open source applications such as oVirt, OpenStack and virt-manager.

QEMU as a whole is released under the GNU General Public License, version 2. For full licensing details, consult the LICENSE file.

[Read more about QEMU here](https://www.qemu.org/)

## KVM

KVM (for Kernel-based Virtual Machine) is a full virtualization solution for Linux on x86 hardware containing virtualization extensions (Intel VT or AMD-V). It consists of a loadable kernel module, kvm.ko, that provides the core virtualization infrastructure and a processor specific module, kvm-intel.ko or kvm-amd.ko.

Using KVM, one can run multiple virtual machines running unmodified Linux or Windows images. Each virtual machine has private virtualized hardware: a network card, disk, graphics adapter, etc. KVM is open source software. The kernel component of KVM is included in mainline Linux, as of 2.6.20. The userspace component of KVM is included in mainline QEMU, as of 1.3.

[Read more about KVM here](https://www.linux-kvm.org/page/Main_Page)

## Libvirt

Libvirt is an open-source API, daemon and management tool for managing platform virtualization. It can be used to manage KVM, Xen, VMware ESXi, QEMU and other virtualization technologies. These APIs are widely used in the orchestration layer of hypervisors in the development of a cloud-based solution.

The Libvirt project:  
- is a toolkit to manage virtualization platforms
- is accessible from C, Python, Perl, Go and more
- is licensed under open source licenses
- supports KVM, QEMU, Xen, Virtuozzo, VMWare ESX, LXC, BHyve and more
- targets Linux, FreeBSD, Windows and macOS
- is used by many applications

[Read more about Libvirt here](https://libvirt.org/)
