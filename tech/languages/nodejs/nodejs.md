---
title: Node.js
subsection: nodejs
section: tech-languages
order: 1
version: LTS
---

# Node.js

## Node.js and npm

Starting from Fedora 24, npm is a part of Node.js package and does not need to be installed separately. Therefore, to install both npm and Node.js, you need to run:
```
sudo dnf install nodejs
```
In case you are running Fedora 23, you should run:
```
sudo dnf install npm
```

This will install V8 Javascript Engine, Node.js runtime and npm package manager and their dependencies. Versions present in repositories are usually current or to-be (in Rawhide) Node.js LTS releases, including npm and V8 engine that come with them.

If you wish to install Node.js v4:
```
sudo dnf install nodejs --releasever=24
```
If you need Node.js v6:
```
sudo dnf install nodejs --releasever=25
```

Installing Node.js modules is covered in [Node.js modules](/tech/languages/nodejs/modules.html).
