---
title: Vagrant plugins
subsection: vagrant
order: 5
---

# Vagrant plugins

## Upstream plugins

There are many more plugins for Vagrant apart from the providers mentioned here. They come in form of Ruby gems and usually have `vargant-` prefix in their name.

To install such a plugin from RubyGems.org type:

```
$ vagrant plugin install PLUGIN
```

If the installation fails it's most likely similar to installation failures of other gems.

To search for Vagrant plugins you can directly [search RubyGems.org](https://rubygems.org/search?utf8=%E2%9C%93&query=vagrant-).

## Packaged plugins

Some Vagrant plugins are packaged for Fedora and delivered as system plugins (in Vagrant terminology). If available they are the preferred method of getting Vagrant plugins on Fedora, especially because the installation is most likely without issues.

To install the plugin from Fedora repositories type:

```
$ sudo dnf install PLUGIN
```

To list available packaged gems try:

```
$ dnf search vagrant-*
```

### vagrant-registration

`vagrant-registration` plugin for Vagrant allows developers to easily register their guests for updates on systems with a subscription model (like Red Hat Enterprise Linux).

This plugin would run register action on vagrant up before any provisioning and unregister on `vagrant halt` or `vagrant destroy`. The actions then call the registration capabilities that have to be provided for given OS.

More information [on the project page](https://github.com/projectatomic/adb-vagrant-registration).
