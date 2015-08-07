---
title: Gems
page: ruby
---

## Gems Installation

You can install new gems on Fedora by either installing upstream gems from RubyGems.org or packaged gems from Fedora official repositories.

### Installing gems from RubyGems.org

Installing upstream gems is as easy as running `gem install GEM_NAME` command, however some gems
might fail to install due to complication errors. If you need to compile gems C extensions, install Ruby header files with the following command:

```
# dnf install ruby-devel
```

In case you lack the C compiler on your Fedora, you can install C development tools group:

```
# dnf group install "C Development Tools and Libraries"
```

### Installing gems from official Fedora repositories

Many gems from RubyGems.org are packaged and available in base Fedora to install. These packages have `rubygem-` prefix to upstream gem names and comes with precompiled extensions.

To install `thor` gem you therefore install `rubygem-thor` package:

```
# dnf install rubygem-thor
```

This variant have the advantage of properly stating of all system dependencies and no need for any header files or development tools. Therefore you can just install the package and run it. It might also contain any security fixes or fixes that makes the gems run smoothly on Fedora without anytional tweaking. This makes it a safer choise as you get the security fixes for your gems with your system updates.

The disadvantage of installing Fedora packaged gems is the lack of versions to choose from. There is only one version that is usually available for a given Fedora at a time.

#### IsItFedoraRuby

To look whether the required gem is available as an RPM package, look at
[IsItFedoraRuby.com](http://isitfedoraruby.com/) site which tracks the Ruby
integration within the Fedora project by listing available information about
packaged gems.
