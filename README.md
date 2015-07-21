# content
Content for the Fedora Developer Portal in Markdown syntax.

## How To Create a Content
The website would consist of several sections. Each section would contain a set of pages.
Each content file must start with initial section in YAML syntax describing the title and where the file belongs.

### An Example for DevAssistant
Every file except the main page would start with:
```yaml
---
title: Some Title      # This title is shown in menus
page: devassistant     # This is an ID of your content (select value from the list below)
---
```
The main page would contain:
```yaml
---
title: DevAssistant    # This title is shown in menus
page: devassistant     # This is an ID of your content (select value from the list below)
section: tools         # This page would be linked from the main menu in a group called tools (select value from the list below)
---
```


### Section and Page Names
First level is a section id. Second level is a page id.

1. tools
  * devassistant
  * docker
  * vagrant
2. tech-languages
  * python
  * ruby
  * php
  * perl
  * go
  * c
  * nodejs
  * java
3. tech-database
  * postgre
  * mariadb
  * sqlite
4. deployment
  * copr
  * scl
  * nulecule
  * xdgapp
  * rolekit
  * openshift
5. fedoranext
  * fedoranext
