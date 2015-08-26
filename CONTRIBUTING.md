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
  2. Is there a special path you need to set up (`$GOLANG`, `$GEM_PATH`)?
  3. How to use packaged version of libraries in upstream bundle tools like [Bundler](http://bundler.io/)?
4. How to install famous frameworks?
  1. e.g. Ruby on Rails, Django, etc.
  2. Add this section only if they are packaged for Fedora or require special action on Fedora that would be unclear from upstream.
5. Is there a Special Interest Group within Fedora? Mention it ([Ruby SIG](https://fedoraproject.org/wiki/Ruby_SIG), [Python SIG](https://fedoraproject.org/wiki/Ruby_SIG)).
6. Mention [Fedora-Dockerfiles](https://github.com/fedora-cloud/Fedora-Dockerfiles) if there is a Dockerfile.

### Databases content
1. General Content
2. How to install the given database and its client tools from Fedora repositories?
  1. postgresql vs postgresql-server, sqliteman etc.
3. How to install packaged extensions?
  1. e.g. postgis, postgresql-contrib for hstore etc.
4. How to setup a development/basic production database?
5. Does [Fedora-Dockerfiles](https://github.com/fedora-cloud/Fedora-Dockerfiles) contain Dockerfile for this database technology?

### Tool Content
1. General Content

## Style and Formatting
* Prefer `#` to `sudo` for commands requiring root password or root user.
* Use the names of upstream project and files properly - e.g. `Makefile` will have capital M.
* Referencing commands and names of binaries that would be ran in command line should be done using back-ticks ``.
* Add empty lines before and after headlines and code blocks.
* Take a look at [Github markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
