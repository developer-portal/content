# Content for Fedora Developer Portal

[Fedora Developer Portal project page](https://fedoraproject.org/wiki/Websites/Developer)

[Content required for the first iteration](https://github.com/developer-portal/content/milestones/first%20release)

## How To Create a Content
The website would consist of several sections. Each section would contain a set of pages.
Each content file must start with initial section in YAML syntax describing the title and where the file belongs.

### An Example for DevAssistant
Every file except the main page would start with:
```yaml
---
title: Some Title      # This title is shown in menus
page: devassistant     # This is an ID of your content (select value from the list below)
order: 1
---

`order` attribute is optional, but it is highly recommended to include. Our templates sort navigation items according to this value
(smaller value means they come first).

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

#### Start
1. start-sw
  * web-app
  * cli-app
  * gui-app
  * mobile-app
2. start-hw
  * raspberry-pi
  * arduino
  * embeded-devices
3. start-tips
  * collaboration
  * documentation

#### Tools
1. tools
  * devassistant
  * docker
  * vagrant

#### Technology
1. tech-languages
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

#### Deployment
1. deployment
  * copr
  * scl
  * nulecule
  * xdgapp
  * rolekit
  * openshift
5. fedoranext
  * fedoranext
