---
title: Synced folders with NFS
page: vagrant
---

## Synced folders with NFS

NFS is a faster way of sharing your project's files between host and guests that
sync the files instantly.

To use NFS with Vagrant, `nfs-utils` package needs to be installed and nfs-server
needs to be running. If it is not, run:

```
# dnf install nfs-utils && systemctl enable nfs-server
```

Afterwards enable `nfs`, `rpc-bind` and `mountd` services for `firewalld`:

```
# firewall-cmd --permanent --add-service=nfs &&
  firewall-cmd --permanent --add-service=rpc-bind &&
  firewall-cmd --permanent --add-service=mountd &&
  firewall-cmd --reload
```

You need these services added for the zone you will run your virtual bridge
(should be FedoraWorkstation as default).

Once done, `:nfs` can be used as an option for files sync in project's
Vagrantfile as follows:

```
Vagrant.configure("2") do |config|
  # ...

  config.vm.synced_folder ".", "/vagrant", type: "nfs"
end
```
