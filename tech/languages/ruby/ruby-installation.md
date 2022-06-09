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

Above command will install latest stable CRuby packages including RDoc, Psych, JSON, BigDecimal and IO/Console, and interactive Ruby shell `irb`. Other bundled libraries such as TclTk bindings, Rake and Test::Unit found in upstream Ruby distribution needs to be installed separately:

```
$ sudo dnf install rubygem-{tk{,-doc},rake,test-unit}
```

Please note that we have already unbundled these libraries from Ruby itself, so they come in their own packages and need a specific dependency requirement in .gemspec or Gemfile as well as a specific `require()` call in your Ruby code.

## JRuby

Alternatively Fedora comes with JRuby packages that can be installed via:

```
$ sudo dnf install jruby
```

Please note that JRuby packages in Fedora are not yet in the best shape and things might be broken. If you are not willing to experiment, please use the CRuby packages for now or use a Ruby version manager of your choice.

## Choosing Ruby with RubyPick

All Rubies come installed with RubyPick, the Fedora Ruby manager. Therefore CRuby has its executable at `/usr/bin/ruby-mri`, JRuby has its at `/usr/bin/jruby` and `/usr/bin/ruby` is a RubyPick executable that chooses the right version of Ruby to run.

You don't need to do anything to set up RubyPick to use CRuby as CRuby is the default. RubyPick was actually introduced to enable Fedora users run other Ruby implementations that might make their way into official Fedora repositories such as JRuby.

To use different Ruby via RubyPick run:

```
ruby _mri_ [params]
ruby _jruby_ [params]
```

Or set the expected environment variables as follows:

```
RUBYPICK=_mri_
RUBYPICK=_jruby_
```

[Read more about RubyPick](https://github.com/fedora-ruby/rubypick).

## Installing Ruby with rbenv

The first step is to install dependencies for Ruby.

```
sudo dnf install git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel
```

Install rbenv

```
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
exec $SHELL
```

Install Ruby

```
rbenv install 2.6.6
rbenv global 2.6.6
ruby -v

```
Use this command if you do not want rubygems to install the documentation for each package locally.

```
echo "gem: --no-document" > ~/.gemrc
```

Install bundler

```
gem install bundler
```

Whenever you install a new version of Ruby or a gem, you should run the rehash sub-command. This will make executables known to rbenv, which will allow us to run those executables:

``` 
rbenv rehash 
``` 
