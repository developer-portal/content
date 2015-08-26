---
title: Synced folders with NFS
page: vagrant
order: 6
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

### Using NFS shares from Vagrant without password prompts

To not enter password many times a day when using NFS, put the following inside
your `/etc/sudoers` file by running `# visudo` (do not try to edit the file
directly, `visudo` will check that the content of the file is correct before
saving):

```
# Allow Vagrant to manage /etc/exports
Cmnd_Alias VAGRANT_EXPORTS_ADD = /usr/bin/tee -a /etc/exports
Cmnd_Alias VAGRANT_NFSD_CHECK = /usr/bin/systemctl status nfs-server.service
Cmnd_Alias VAGRANT_NFSD_START = /usr/bin/systemctl start nfs-server.service
Cmnd_Alias VAGRANT_NFSD_APPLY = /usr/sbin/exportfs -ar
Cmnd_Alias VAGRANT_EXPORTS_REMOVE = /bin/sed -r -e * d -ibak /etc/exports
%vagrant ALL=(root) NOPASSWD: VAGRANT_EXPORTS_ADD, VAGRANT_NFSD_CHECK, VAGRANT_NFSD_START, VAGRANT_NFSD_APPLY, VAGRANT_EXPORTS_REMOVE
```

Afterwards add yourself to the `vagrant` group if you are not there already by running:

```
# gpasswd -a ${USER} vagrant
$ newgrp vagrant
```
