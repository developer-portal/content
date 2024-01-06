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
$ echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

## Rbenv rehash

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

# Installing Rails

Rails depends on a Javascript runtime. Follow [this guide](https://github.com/nodenv/nodenv?tab=readme-ov-file#basic-github-checkout)
to install `nodejs` using `nodenv`.

If you would rather have Fedora packaged `nodejs` and will not need multiple versions of `nodejs` (like for different projects)
you can install it with `dnf`:

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
