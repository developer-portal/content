---
title: Ruby
subsection: ruby
section: tech-languages
order: 1
version: 2.2.2
description: A dynamic programming language with a focus on readability, simplicity and productivity.
---

# Ruby installation

## CRuby

To install CRuby, simply type:

```
$ sudo dnf install ruby
```

Above command will install latest stable CRuby packages including RDoc, Psych, JSON, BigDecimal and IO/Console. Other bundled libraries such as Rake, the interactive Ruby shell `irb`, Test::Unit and other bundled libraries found in upstream Ruby distribution need to be installed separately:

```
$ sudo dnf install rubygem-{irb,rake,rbs,rexml,typeprof,test-unit} ruby-bundled-gems
```

Please note that we have already unbundled these libraries from Ruby itself, so they come in their own packages and need a specific dependency requirement in .gemspec or Gemfile as well as a specific `require()` call in your Ruby code.

## Choosing Ruby with RubyPick

All Fedora Rubies come installed with RubyPick, the Fedora Ruby manager. Therefore CRuby has its executable at `/usr/bin/ruby-mri`, and `/usr/bin/ruby` is a RubyPick executable that chooses the right version of Ruby to run.

You don't need to do anything to set up RubyPick to use CRuby as CRuby is the default. RubyPick was actually introduced to enable Fedora users run other Ruby implementations that might make their way into official Fedora repositories such as JRuby.

To use different Ruby via RubyPick run:

```
ruby _mri_ [params]
```

Or set the expected environment variables as follows:

```
RUBYPICK=_mri_
```

[Read more about RubyPick](https://github.com/fedora-ruby/rubypick).

## Installing Ruby with rbenv

The first step is to install dependencies for Ruby and rbenv.

```console
$ sudo dnf install git-core zlib zlib-devel gcc-c++ patch readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison libcurl-devel sqlite-devel perl-FindBin perl-lib perl-File-Compare
```

To use Fedora packaged rbenv also install:
```console
$ sudo dnf install rbenv ruby-build-rbenv
```

To use upstream rbenv, follow the steps in [Installing Ruby with
rbenv](/tech/languages/ruby/ruby-installation.html#installing-ruby-with-rbenv).

Then configure your shell to enable rbenv:

```console
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
$ source ~/.bashrc
```

Install a Ruby version, such as 3.4.9. See `rbenv install --list` for available versions.

```console
$ rbenv install 3.4.9
$ rbenv global 3.4.9
$ ruby -v
```
Use this command if you do not want rubygems to install the documentation for each package locally.

```console
$ echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

### Rbenv rehash

`rbenv rehash` is not needed when installing gems via `gem install` as rbenv will automatically
trigger the rehash. You may need to trigger a rehash manually after installing gems using bundler.
You can do so by running
```console
$ rbenv rehash
```

Since [rbenv commit 325abac](https://github.com/rbenv/rbenv/commit/325abac17de79a230152bb7038126a0641c6aa64),
there is no need to run `rbenv rehash` when installing gems via bundler or `gem install`.
Rbenv will automatically trigger the rehash using either of those methods. To ensure you have this
version installed, follow the [basic git checkout installation instructions](https://github.com/rbenv/rbenv?tab=readme-ov-file#basic-git-checkout).


Install bundler:

```console
$ gem install bundler
```
