# Content for Fedora Developer Portal

This repository contains the text content for the [Fedora Developer Portal](https://developer.fedoraproject.org/). See the [project page](https://fedoraproject.org/wiki/Websites/Developer) on Fedora Wiki.

If you are here to submit issue or PR regarding the portal itself, please do so in the website repository: https://github.com/developer-portal/website.

## How to submit content

1. Read our [contribution guide](./CONTRIBUTING.md) about writing content
2. Learn about [markdown syntax](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
3. [Create new](https://help.github.com/articles/creating-new-files/) or modify existing files within this repository

## How to test your changes

You can easily review the markdown formatting directly on Github but if you want to see how your changes look in context of the whole website, you might want to take a look at the [website](https://github.com/developer-portal/website) repository and run a local instance of the portal.

### Structure

The website consists of several sections. Each section contains a set of pages.
Each content file must start with an initial section in YAML syntax describing the title and where the file belongs.


#### An example for DevAssistant

Every file except the main page would start with:

```yaml
---
title: Some Title      # This title is shown in menus
page: devassistant     # This is an ID of your content (select value from the list below)
order: 1               # Optional - order in menu
---
```

The main page would contain:

```yaml
---
title: DevAssistant    # This title is shown in menus
page: devassistant     # This is an ID of your content (select value from the list below)
section: tools         # This page would be linked from the main menu in a group called tools (select value from the list below)
description: Lorem ipsum...    # a short description to be shown in the section menu
---
```

#### Section and page names

First level is a section id. Second level is a page id.

##### Start

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
  * collaborate
  * documentation

##### Tools

1. tools
  * devassistant
  * docker
  * vagrant

##### Technology

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

##### Deployment

1. deployment
  * copr
  * scl
  * nulecule
  * xdgapp
  * rolekit
  * openshift
5. fedoranext
  * fedoranext
