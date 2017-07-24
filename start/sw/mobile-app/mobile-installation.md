---
title: Mobile application
subsection: mobile-app
section: start-sw
order: 1
description: Creating mobile applications using Google Android Studio.
---

# Mobile application

Today wide range of smart mobile devices make it possible to create clever applications.

## Get started

### Install required libraries

```$ sudo dnf install glibc.i686 glibc-devel.i686 libstdc++.i686 zlib-devel.i686 ncurses-devel.i686```

### Install Android Studio

1. Download [Android Studio](https://developer.android.com/studio/index.html).

2. Unpack the .zip and install to the opt directory.

```$ unzip android-studio*.zip```

```$ sudo mv android-studio /opt/android-studio```

3. Navigate to directory where Android Studio was installed and run start script. This will start Android Studio with a wizard to complete the installation.

```$ ./bin/studio.sh```
