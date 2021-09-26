---
title: Installing QEMU on Fedora Linux  
subsection: virtualization  
order: 1  
---

# Installing QEMU

## QEMU 

QEMU is a generic and open source machine & userspace emulator and virtualizer.

QEMU is capable of emulating a complete machine in software without any need for hardware virtualization support. By using dynamic translation, it achieves very good performance. QEMU can also integrate with the Xen and KVM hypervisors to provide emulated hardware while allowing the hypervisor to manage the CPU. With hypervisor support, QEMU can achieve near native performance for CPUs. When QEMU emulates CPUs directly it is capable of running operating systems made for one machine (e.g. an ARMv7 board) on a different machine (e.g. an x86_64 PC board).

QEMU is also capable of providing userspace API virtualization for Linux and BSD kernel interfaces. This allows binaries compiled against one architecture ABI (e.g. the Linux PPC64 ABI) to be run on a host using a different architecture ABI (e.g. the Linux x86_64 ABI). This does not involve any hardware emulation, simply CPU and syscall emulation.

QEMU aims to fit into a variety of use cases. It can be invoked directly by users wishing to have full control over its behaviour and settings. It also aims to facilitate integration into higher level management layers, by providing a stable command line interface and monitor API. It is commonly invoked indirectly via the libvirt library when using open source applications such as oVirt, OpenStack and virt-manager.

[Read more about QEMU here](https://www.qemu.org/)

## KVM

KVM (for Kernel-based Virtual Machine) is a full virtualization solution for Linux on x86 hardware containing virtualization extensions (Intel VT or AMD-V). It consists of a loadable kernel module, kvm.ko, that provides the core virtualization infrastructure and a processor specific module, kvm-intel.ko or kvm-amd.ko.

Using KVM, one can run multiple virtual machines running unmodified Linux or Windows images. Each virtual machine has private virtualized hardware: a network card, disk, graphics adapter, etc.

[Read more about KVM here](https://www.linux-kvm.org/page/Main_Page)

## Installing steps

1. Execute the following command to install QEMU on the host device, if not already installed.  
   ```
   sudo dnf install qemu -y
   ```
   ![01](https://user-images.githubusercontent.com/49605954/127774416-b748ce6e-5c04-40d8-8470-7962b57053e4.png)  
