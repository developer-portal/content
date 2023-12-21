---
title: Ruby on Rails      
subsection: web-app
order: 6
---

# Installing Ruby and Rails with rbenv

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

Install a Ruby version, such as 3.1.2. See `rbenv install --list` for available versions.

```console
$ rbenv install 3.1.2
$ rbenv global 3.1.2
$ ruby -v
```
Use this command if you do not want rubygems to install the documentation for each package locally.

```console
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

## Rbenv rehash

Running rbenv rehash is not needed for simple `gem install`. rbenv triggers a rehash automatically.
It may be desired to rehash after installing gems with executables via bundler.
It will make the Ruby gem executables known to rbenv, which allows running those executables.

You can rehash by executing the following:

```console
$ rbenv rehash
```

Since [rbenv commit 325abac](https://github.com/rbenv/rbenv/commit/325abac17de79a230152bb7038126a0641c6aa64)
the `rbenv rehash` command is not required when using bundler.
A rehash will trigger automatically similarly to running `gem install`.

If you have cloned rbenv from upstream ensure you have the latest rbenv that contains the fix.
You can update rbenv pulled from upstream using git.

Assuming you have cloned your rbenv to `~/.rbenv`, enter rbenv's directory and pull latest updates
from the upstream git repository:

```console
$ cd ~/.rbenv
$ git pull
```

# Installing Rails

Rails depends on a Javascript runtime, install nodejs.

```console
$ sudo dnf install nodejs
```

And now install Rails

```console
$ gem install rails -v 7.1.2
```

```console
$ rails -v
```

# Create your first Rails app

```console
$ rails new myapp

# Move into the application directory
$ cd myapp

# Create the database
$ rake db:create

# Start the server
$ rails server
```
You can now visit http://localhost:3000 to view your new website.
