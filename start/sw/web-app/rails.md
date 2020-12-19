---
title: Ruby on Rails      
subsection: web-app
order: 6
---

# Installing Ruby and Rails with rbenv

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
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

Install bundler

```
gem install bundler
```

Whenever you install a new version of Ruby or a gem, you should run the rehash sub-command. This will make rails executables known to rbenv, which will allow us to run those executables:

``` 
rbenv rehash 
``` 

# Installing Rails

Rails depends on a Javascript runtime, install nodejs.

```
sudo dnf install epel-release
sudo dnf install nodejs
```

And now install Rails

```
gem install rails -v 4.2.6
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
