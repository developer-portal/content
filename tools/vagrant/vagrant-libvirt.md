---
title: Vagrant with libvirt provider
page: vagrant
order: 2
---

## Vagrant with libvirt support installation


To use Vagrant with libvirt, you need to install the `vagrant-libvirt` package:

```
# dnf install vagrant-libvirt
```

There is also *@vagrant* group available now so you can use that one as well. *@vagrant* group
was created with using libvirt provider in mind.


### Using libvirt from Vagrant without password prompts


Using `libvirt` provider require you to type your administrator password every time you create,
start, halt or destroy your domains. Fortunately you can avoid this by setting `polkit rules`
to allow Vagrant to use `libvirt` without explicit approvals. We included this file in `-doc`
sub-package. To get it, type:

```
# dnf install vagrant-libvirt-doc
```

And install the policy by coping the polkit `.rules` file:

```
# cp /usr/share/vagrant/gems/doc/vagrant-libvirt-0.0.26/polkit/10-vagrant-libvirt.rules /usr/share/polkit-1/rules.d/
```

This is example for Fedora 22, for other versions change the version of `vagrant-libvirt` component in
the above path to the one installed.
