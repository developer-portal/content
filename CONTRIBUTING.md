# Contribution Guidelines to Fedora Developer Portal

## How To Contribute
1. Find the issue to work on
  1. create an issue if it does not exist already
1. Create a pull-request

## Content
### General Content
1. A simple paragraph about the tech/tool
2. Installation and setup
3. Fedora-specific stuff
  1. Idea is to describe how fedora differs from upstream (if it does)
4. Some quickstart
  1. Link to an upstream if it exists
  2. Custom content if not in upstream or if upstream uses different OS

### Language content
(You can get inspiration from Ruby content if unsure.)

1. General Content
2. how to install the associated package/s on fedora
  1. whats the difference from upstream distribution?
3. how to install other libraries from Fedora and/or upstream
  1. e.g. RubyGems, pip, etc.
  2. is there a special path you need to set up (GOLANG, GEM_PATH)? 
  3. how to use packaged version of libraries in upstream bundle tools like Bundler
4. how to install famous frameworks
  1. e.g. Ruby on Rails, Django, etc.
  2. only if there are packaged for fedora or require special action on Fedora that would be unclear from upstream 
5. is there a specific Special Interest Group within Fedora? mention it (Ruby SIG, Python SIG)

### Databases content
1. General Content
2. how to install given database from Fedora repositories and its client tools
  1.postgresql vs postgresql-server, sqliteman etc.
3. how to install packaged extensions
  1. e.g. postgis, postgresql-contrib for hstore etc.
1. how to setup development/basic production database

### Tool Content
1. General Content

## Style and Formatting
* giprefer # to sudo for commands requiring root password or root user
* keep the names of upstream project and files e.g. Makefile will have capital M
* referencing commands and names of binaries that would be ran in command line should be done using back-ticks `` 
* link to github markdown: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet 
