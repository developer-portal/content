---
title: Vagrant
subsection: vagrant
section: tools
description: Create reproducible and portable development environments that can be easily shared in your team.

order: 1
---

# Vagrant

[Vagrant](https://www.vagrantup.com/) is a tool for creating reproducible and portable development environments.

## Installation

Vagrant works on top of some virtualization or containerization technology. To install Vagrant read the provider-specific instructions and tips:

- [Vagrant with libvirt](/tools/vagrant/vagrant-libvirt.html)
- [Vagrant with VirtualBox](/tools/vagrant/vagrant-virtualbox.html)
- [Vagrant with Docker](/tools/vagrant/vagrant-docker.html)

## Plugins

Vagrant can be extended by plenty of plugins, some of them are even packaged in
Fedora. [Read more](/tools/vagrant/vagrant-plugins.html).

## Limitations

Vagrant packaged in Fedora currently does not support Windows guests. This is due to missing various dependencies that will be hopefully added to Fedora. The other limitation is the lack of support for `vagrant push`. This is unfortunately due to the licencing of the libraries used by upstream and probably will not be resolved in the foreseeable future.
