---
title: Synced folders with SSHFS
subsection: vagrant
order: 8
---

# Synced folders with SSHFS

SSHFS is an easy, cross platform, way to share your project's files
between the hosts and the guests and achieve two way synchronization.
You can read more about this folder sharing option 
[here](https://github.com/dustymabe/vagrant-sshfs).

This code is currently delivered as a
[vagrant plugin](/tools/vagrant/vagrant-plugins.html), and can be
installed as RPM `dnf install vagrant-sshfs` or via
`vagrant plugin install vagrant-sshfs` on other platforms that don't
support RPM.

Once the plugin is installed `sshfs` can be set as the `type` on the
synced folder configuration line in the project's `Vagrantfile`:

```
Vagrant.configure("2") do |config|
  # ...

  config.vm.synced_folder ".", "/sharedolder", type: "sshfs"
end
```

You should not need to provide any authentication to get this to work.
