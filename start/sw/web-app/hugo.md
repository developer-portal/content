---
title: Hugo
subsection: web-app
order: 8
---

# Hugo
Hugo is a fast and modern static site generator written in Go, and designed to make website creation fun again.

## Installation

```
$ sudo dnf install hugo
```

## Creating a new website
If you are starting a new website, instead of creating all the necessary files yourself you can use the `hugo new` command.

```
$ hugo new site my-site
$ cd my-site
```

The command will generate all the directories and config.toml files for your new website but you need to install a theme before building the site.

## Add a theme

Hugo have a list of themes on https://themes.gohugo.io/ that you can browse or you can create one yourself. Most themes use git so you just need to add them as git submodules:

```
$ git init
$ git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

To use the theme you need to add the theme parameter to the config.toml file

## Running Hugo built in server

Hugo comes with a built in web server to use if you don't want to install a web server. To run the server, you need to type:

```
$ hugo server
```

If you are editing and want to see your drafts, add the `-D` flag
