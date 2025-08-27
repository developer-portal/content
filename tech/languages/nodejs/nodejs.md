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

### Alternative versions

Alternative supported versions can be installed by specifying stream version, for example for nodejs24:

```
$ sudo dnf install nodejs24
```

This will also install V8 Javascript Engine, Node.js runtime and npm package manager and their dependencies of the specified version.

### Managing multiple versions with nvm

[nvm](https://github.com/nvm-sh/nvm#about) (Node Version Manager) is a bash script to manage multiple Node.js versions. nvm makes it easier to install, uninstall, and switch between different versions. Visit its Github page to follow the latest [installation instructions](https://github.com/nvm-sh/nvm#installing-and-updating).

## Yarn

[Yarn](https://yarnpkg.com/en/) package manager is available since Fedora 29. You can install it by running:

```
$ sudo dnf install yarnpkg
```

Yarn can be used in the following manner:

```
$ yarnpkg add request
$ yarn add request
```

## Installing npm modules

Installing Node.js modules is covered in [Node.js modules](/tech/languages/nodejs/modules.html).

## Installing Global Modules

Create a directory for global installations inside your home directory:

```
mkdir ~/.npm-global
```

Set the new directory path for npm:

```
npm config set prefix '~/.npm-global'
```

Open/create the `~/.profile` file and add the following line:

```
export PATH=~/.npm-global/bin:$PATH
```

Update your system variables with this command:

```
source ~/.profile
```
