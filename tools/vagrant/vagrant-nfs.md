---
title: Synced folders with NFS
subsection: vagrant
order: 7
---

# Synced folders with NFS

NFS is a faster way of sharing your project's files between host and guests that
sync the files instantly.

To use NFS with Vagrant, `nfs-utils` package needs to be installed and nfs-server
needs to be running. If it is not, run:

```
$ sudo dnf install nfs-utils && sudo systemctl enable nfs-server
```

Afterwards enable `nfs`, `rpc-bind` and `mountd` services for `firewalld`:

```
$ sudo firewall-cmd --permanent --zone=libvirt --add-service=nfs3 \
    && sudo firewall-cmd --permanent --zone=libvirt --add-service=nfs \
    && sudo firewall-cmd --permanent --zone=libvirt --add-service=rpc-bind \
    && sudo firewall-cmd --permanent --zone=libvirt --add-service=mountd \
    && sudo firewall-cmd --reload
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

One of the common errors when using NFS this way might be that your NFS version does not support UDP protocol which gets added by Vagrant as a default.

In that case the error message is `mount.nfs: requested NFS version or transport protocol is not supported`. You can work around this by disabling UDP with `nfs_udp` option:

```
config.vm.synced_folder ".", "/vagrant", type: "nfs", nfs_udp: false
```

## Using NFS shares from Vagrant without password prompts

To not enter password many times a day when using NFS, put the following inside
your `/etc/sudoers` file by running `sudo visudo` (do not try to edit the file
directly, `visudo` will check that the content of the file is correct before
saving):

```
# Allow Vagrant to manage /etc/exports
Cmnd_Alias VAGRANT_EXPORTS_ADD = /usr/bin/tee -a /etc/exports
Cmnd_Alias VAGRANT_NFSD_CHECK = /usr/bin/systemctl status --no-pager nfs-server.service
Cmnd_Alias VAGRANT_NFSD_START = /usr/bin/systemctl start nfs-server.service
Cmnd_Alias VAGRANT_NFSD_APPLY = /usr/sbin/exportfs -ar
Cmnd_Alias VAGRANT_EXPORTS_REMOVE = /bin/sed -r -e * d -ibak /*/exports
Cmnd_Alias VAGRANT_EXPORTS_REMOVE_2 = /bin/cp /*/exports /etc/exports
%vagrant ALL=(root) NOPASSWD: VAGRANT_EXPORTS_ADD, VAGRANT_NFSD_CHECK, VAGRANT_NFSD_START, VAGRANT_NFSD_APPLY, VAGRANT_EXPORTS_REMOVE, VAGRANT_EXPORTS_REMOVE_2
```

Afterwards add yourself to the `vagrant` group if you are not there already by running:

```
$ sudo getent group vagrant >/dev/null || sudo groupadd -r vagrant
$ sudo gpasswd -a ${USER} vagrant
$ sudo -u ${USER} ${SHELL}
```
