---
title: Ruby on Rails
subsection: ruby
order: 4
---

# Ruby on Rails installation

## Installing Rails from RubyGems.org

To install Ruby on Rails on Fedora as a gem, install Ruby first together with `ruby-devel`, `gcc`, `zlib-devel` packages, and then install Rails using the `gem` command:

```
$ sudo dnf group install "C Development Tools and Libraries"
$ sudo dnf install ruby-devel zlib-devel
$ gem install rails
```

You might need to install other header files depending on the gems used in your application like installing `sqlite-devel` package for `sqlite3` gem. Note that you can always install the gems from the official repositories as RPM packages to avoid this.

## Installing Rails from Fedora official repositories

To install RPM-packaged Ruby on Rails run:

```
$ sudo dnf install rubygem-rails
```

This will install the framework itself, but if you wish to install all default gems suggested by Rails for new applications, run:

```
$ sudo dnf group install 'Ruby on Rails'
```

To take advantage of packaged gems, you need to run `rails` command with `--skip-bundle` option and then run `bundle --local` to lock your dependencies using system gems:

```
$ rails new app --skip-bundle
$ cd app
$ bundle --local
```
