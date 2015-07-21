# content
Content for the Fedora Developer Portal in Markdown syntax.

## How To Create a Content
The website would consist of several sections. Each section would contain a set of pages.
**Each content file** must start with initial section in YAML syntax describing the title and where the file belongs. An example for DevAssistant:
```yaml
---
title: Some Title
page: devassistant
---
```
Each project might have several pages. **One** of them would be the **main page**, starting with:
```yaml
---
title: DevAssistant
page: devassistant
section: tools
---
```
### Section and Page Names
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
