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

The first step is to install dependencies for Ruby.

```console
$ sudo dnf install git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel perl-FindBin
```

Then we are going to clone rbenv and the ruby-build rbenv plugin into the home directory.
To make rbenv command available we append your shell's rc file with initialization.

```console
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
$ echo 'eval "$(~/.rbenv/bin/rbenv init -)"' >> ~/.bashrc
```

Next step we have to refresh the shell to make the binaries available. This can be achieved
by either the following command or opening a new terminal:
```console
$ exec $SHELL
```

Now you can install Ruby simply via `rbenv install`
```console
$ rbenv install 3.0.4
$ rbenv global 3.0.4
$ ruby -v
```

Use this command if you do not want rubygems to install the documentation for each package locally.

```console
$ echo "gem: --no-document" > ~/.gemrc
```

Install bundler

```console
$ gem install bundler
```
