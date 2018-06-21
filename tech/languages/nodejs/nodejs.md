---
title: Node.js
subsection: nodejs
section: tech-languages
order: 1
version: LTS
description: Open-source cross-platform server-side JavaScript runtime environment.
---

# Node.js

## Node.js and npm installation

Starting from Fedora 24, npm is a part of Node.js package and does not need to be installed separately. Therefore, to install both npm and Node.js, you need to run:

```
$ sudo dnf install nodejs
```

This will install V8 Javascript Engine, Node.js runtime and npm package manager and their dependencies. Versions present in repositories are usually current or to-be (in Rawhide) Node.js LTS releases, including npm and V8 engine that come with them.

You can check the available versions with:

```
$ dnf info nodejs
$ dnf info nodejs --enablerepo rawhide
```

## Yarn

[Yarn](https://yarnpkg.com/en/) package manager is available since Fedora 29. You can install it by running:

```
$ sudo dnf install nodejs-yarn
```

Because of conflicts with other packages, yarn has to be used in the following manner:

```
$ nodejs-yarn add request
$ yarnpkg add request
```

If you still wish to use `yarn` instead of `nodejs-yarn`, the best way is to use bash alias.

## Installing npm modules

Installing Node.js modules is covered in [Node.js modules](/tech/languages/nodejs/modules.html).
