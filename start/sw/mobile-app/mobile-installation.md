---
title: Mobile application
subsection: mobile-app
section: start-sw
order: 1
description: Creating mobile applications using Google Android Studio.
---

# Mobile application.

Today, a wide range of smart mobile devices make it possible to create clever applications.

## Getting started.

### Install the required libraries.

```$ sudo dnf install glibc.i686 glibc-devel.i686 libstdc++.i686 zlib-devel.i686 ncurses-devel.i686```

### Install Android Studio.

1. Download [Android Studio](https://developer.android.com/studio/index.html).

2. Unpack the .zip file using the command below: 

```$ unzip android-studio*.zip```

Install to the opt directory.

```$ sudo mv android-studio /opt/android-studio```

3. Navigate to the directory where Android Studio was installed and run the start script. This will start Android Studio with a wizard to complete the installation.

```$ ./bin/studio.sh```
