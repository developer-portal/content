---
title: Gems
page: ruby
order: 2
---

# Gems installation

You can install new gems on Fedora by either installing upstream gems from RubyGems.org or packaged gems from Fedora official repositories.

## Installing gems from RubyGems.org

Installing upstream gems is as easy as running `gem install GEM_NAME` command, however some gems might fail to install due to compilation errors. If you need to compile gems C extensions, install Ruby header files with the following command:

```
$ sudo dnf install ruby-devel
```

In case you lack the C compiler on your Fedora, you can install C development tools group:

```
$ sudo dnf group install "C Development Tools and Libraries"
```

Other missing header files will depend on the particular gem you want to install. In Fedora the sub-packages containing header files are always suffixed with `-devel` so for example to install the `pg` gem, you will need to compile its C extensions against PostgreSQL header files that can be installed by installing `postgresql-devel` sub-package.

If you installed all the above, but the extensions would still not compile, you are probably running a Fedora image that misses `redhat-rpm-config` package. In that case `gcc` compiler would complain about one of the following:

```
gcc: error: conftest.c: No such file or directory
gcc: error: /usr/lib/rpm/redhat/redhat-hardened-cc1: No such file or directory
```

To solve this, simply run `sudo dnf install redhat-rpm-config`.

If you are getting compilation issues mentioning `Failed to complete patch task`, you are likely missing `patch` command:

```
$ sudo dnf install patch
```

## Installing gems from official Fedora repositories

Many gems from RubyGems.org are packaged and available in base Fedora to install. These packages have `rubygem-` prefix to upstream gem names and a `rubygem(name)` virtual provide, and also comes with precompiled extensions.

To install `thor` gem you therefore install `rubygem-thor` package:

```
$ sudo dnf install rubygem-thor
```
or
```
$ sudo dnf install 'rubygem(thor)'
```

This variant have the advantage of properly stating of all system dependencies and no need for any header files or development tools. Therefore you can just install the package and run it. It might also contain any security fixes or fixes that makes the gems run smoothly on Fedora without additional tweaking. This makes it a safer choice as you get the security fixes for your gems with your system updates.

The disadvantage of installing Fedora packaged gems is the lack of versions to choose from. There is only one version that is usually available for a given Fedora at a time. To use the packaged gems successfully with Bundler, you will need to lock the exact version of the gem in the project's Gemfile. If all gems are installed from Fedora repositories, you can take advantage of Bundler's `--local` switch:

```
$ bundle --local
```

This way Bundler won't try to get other gems from RubyGems.org and will only use and lock the gems found on your machine.

Note that system gems are installed into `/usr/share/gems` and this path needs to be included in `$GEM_PATH` in case you are about to modify it.

### IsItFedoraRuby

To look whether the required gem is available as an RPM package, look at
[IsItFedoraRuby.com](http://isitfedoraruby.com/) site which tracks the Ruby
integration within the Fedora project by listing available information about
packaged gems.
