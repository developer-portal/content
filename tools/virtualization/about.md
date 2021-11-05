---
title: Virtualization  
subsection: virtualization  
section: tools  
description: Run virtual machines at near-native speeds and manage them at ease  
---

# Virtualization

The method of executing a virtual instance of a computer system in a layer separate from the actual hardware is known as virtualization. It usually refers to running multiple operating systems on the same computer at the same time. It may appear to applications running on top of the virtualized machine that they are on their own dedicated machine, with their own operating system, libraries, and other programmes that are separate from the host operating system that sits underneath it.

Virtualization is used in computers for a variety of reasons. The most typical purpose for desktop users is to be able to use apps designed for a different operating system without having to swap machines or reboot. Virtualization gives server managers the flexibility to run multiple operating systems, but probably more critically, it allows them to divide a huge system into many smaller portions, allowing the server to be utilised more efficiently by a variety of users or applications with varying requirements. It also enables isolation, which protects programmes operating inside a virtual machine from processes running in another virtual machine on the same host.

## Common terms

### Hypervisor

A hypervisor is a tool that allows you to create and run virtual machines. Traditionally, hypervisors were divided into two types: type one, or "bare metal" hypervisors, which run guest virtual machines directly on a system's hardware, basically acting as an operating system. Type two hypervisors, often known as "hosted" hypervisors, act more like standard applications that may be launched and stopped just like any other programme. This split is less common in newer systems, especially with solutions like KVM. KVM (kernel-based virtual machine) is a component of the Linux kernel that allows you to run virtual machines directly, however you can still use a system running KVM virtual machines as a regular computer.

### Virtual machine

A virtual machine is a computer system that is imitated and runs on top of another system. Virtual machines can access a variety of resources, including computing power via hardware-assisted but limited access to the host machine's CPU and memory; one or more physical or virtual disc devices for storage; a virtual or real network interface; and any shared devices like video cards, USB devices, or other hardware. A disc image is used to describe a virtual machine that is kept on a virtual disc. A disc image can contain the files necessary for a virtual computer to boot, as well as any extra storage requirements.

## References
1. [https://opensource.com/resources/virtualization](https://opensource.com/resources/virtualization)
