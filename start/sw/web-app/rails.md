---
title: Ruby on Rails      
subsection: web-app
order: 6
---

# Installing Ruby and Rails with rbenv

The first step is to install dependencies for Ruby and rbenv.

```
sudo dnf install git-core zlib zlib-devel gcc-c++ patch readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison libcurl-devel sqlite-devel rbenv rbenv-build-rbenv
```

Then configure your shell to enable rbenv:

```
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

Install a Ruby version, such as 3.1.2. See `rbenv install --list` for available versions.

```
rbenv install 3.1.2
rbenv global 3.1.2
ruby -v

```
Use this command if you do not want rubygems to install the documentation for each package locally.

```
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

Whenever you install a new version of Ruby or a gem, you should run the rehash sub-command. This will make rails executables known to rbenv, which will allow us to run those executables:

``` 
rbenv rehash 
``` 

# Installing Rails

Rails depends on a Javascript runtime, install nodejs.

```
sudo dnf install nodejs
```

And now install Rails

```
gem install rails -v 7.1.2
```
```
rbenv rehash
```

```
rails -v
```

#Create your first Rails app

```
rails new myapp

# Move into the application directory
cd myapp

# Create the database
rake db:create

# Start the server
rails server
```
You can now visit http://localhost:3000 to view your new website.
