# Contribution Guidelines to Fedora Developer Portal

## How To Contribute

1. Find the issue to work on.
  1. Create an issue if it does not exist already.
1. Create a pull-request.

## Content

### General Content

1. A simple paragraph about the tech/tool
2. Installation and setup
3. Fedora-specific stuff
  1. The idea is to describe how Fedora differs from upstream (if it does).
4. Some quickstart
  1. Link to an upstream if it exists
  2. Custom content if not in upstream or if upstream uses different OS

### Language content

(You can get inspiration from Ruby content if unsure.)

1. General Content
2. How to install the associated package/s on Fedora?
  1. Whats the difference from upstream distribution?
  2. Are there any more implementations/versions?
    3. CRuby vs JRuby, Python2 vs Python3
    4. How to choose between them (rubypick)?
3. How to install other libraries from Fedora and/or upstream?
  1. e.g. RubyGems, pip, etc.
  2. Is there a special path you need to set up (`$GOPATH`, `$GEM_PATH`)?
  3. How to use packaged version of libraries in upstream bundle tools like [Bundler](http://bundler.io/)?
4. How to install famous frameworks?
  1. e.g. Ruby on Rails, Django, etc.
  2. Add this section only if they are packaged for Fedora or require special action on Fedora that would be unclear from upstream.
5. Is there a Special Interest Group within Fedora? Mention it ([Ruby SIG](https://fedoraproject.org/wiki/Ruby_SIG), [Python SIG](https://fedoraproject.org/wiki/Ruby_SIG)).

### Databases content

1. General Content
2. How to install the given database and its client tools from Fedora repositories?
  1. postgresql vs postgresql-server, sqliteman etc.
3. How to install packaged extensions?
  1. e.g. postgis, postgresql-contrib for hstore etc.
1. How to setup a development/basic production database?

### Tool Content

1. General Content

## Style and Formatting

* Please use `$ sudo ...` for commands requiring root password or root user.
* Use the names of upstream project and files properly - e.g. `Makefile` will have capital M.
* Referencing commands and names of binaries that would be ran in command line should be done using back-ticks ``.
* Add empty lines before and after headlines and code blocks.
* Format headlines as normal sentences e.g. About my program called Program, *not* About My Program Called Program
* Take a look at [Github markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

### Internal links

To reference a page in this repository, use the full path and replace `.md` extension to `.html`:

e.g. to reference `/tech/tools/vagrant/vagrant-libvirt.md` write `[Vagrant with libvirt](/tech/tools/vagrant/vagrant-libvirt.html)`

## Some general hints how to write documentation

###  Keep them simple

Don't use complicated sentences. Not everyone reading the documentation will be fluent in English, and if the solution texts get translated, it might be to Japanese, which is a language so fundamentally different that anything even a little bit complicated turns into a translation nightmare.

### Simple from technical standpoint

Keep the doc simple from a '''technical standpoint''' too. Not everyone reading the documentation will be an experienced admin/user.

### Avoid shorthands

They're just too informal.

#### Bad example:

```
The update won't be available...
```

#### Good example:

```
The update will not be available...
```

### Be direct

Avoid passive voice.

#### Bad example:

```
This can be fixed by...
```

#### Good example:

```
You can fix this issue by...
```

### Tell the user what is going on

When you tell users to run a set of commands, tell them what is going on. This mostly applies to cases where the documentation text contains some procedure (a set of commands) to do some complicated stuff. When that happens, don't just put in the commands, but explain them.

#### Bad example:

```
$ sudo systemctl disable firewalld
$ sudo systemctl stop firewalld
$ sudo cp PREUPGRADE_DIR/cleanconf/etc/sysconfig/iptables /etc/sysconfig/iptables
etc.
```

#### Good example:

```
First, disable and stop the firewalld service:\n
$ sudo systemctl disable firewalld
$ sudo systemctl stop firewalld
Then, copy the cleanconf/etc/sysconfig/iptables configuration file into your system's /etc/sysconfig/ directory:
$ sudo cp PREUPGRADE_DIR/cleanconf/etc/sysconfig/iptables /etc/sysconfig/iptables
etc.
```

If this makes the particular documentation too long, you could create a separate page about it and provide a link to the user instead.

### Be sure

If we say things like "this should be in...", it makes us sound like we don't even know what's actually going on.

#### Bad example:

```
You should be able to find this list in /etc/whatever/list.
```

#### Good example:

```
The list is located in /etc/whatever/list.
```

### How to document an issue in more versions

In case you want to document one issue for more versions of the product, while there are small differences in each version, create one article for the most current version and use notes to describe differences for other versions.
