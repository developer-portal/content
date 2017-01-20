---
title: Google Android Studio
subsection: mobile-app
order: 2
---

# How to install Google Android Studio on Fedora

## From android website

You can install it from [Android Studio on developer.android.com](https://developer.android.com/studio/index.html) and follow their instructions.

## From [DevAssistant](https://devassistant.org) command line:

First of all install [DevAssistant](https://devassistant.org) project:

```bash
$ sudo dnf install devassistant
```

If you prefer GUI run:

```bash
$ sudo dnf install devassistant-gui
```

Install DAP plugin [Google Android studio](https://github.com/phracek/dap-google-android-studio) for DevAssistant:

```bash
$ da pkg install android-studio
```

If you want to install only packages which are needed by Google Android Studio, run:

```bash
$ da crt --deps-only android-studio --name <your_project_name>
```

To install Google Android Studio run:

```bash
$ da crt android-studio --name <name_of_your_project>
```

It will download the latest versions of Google Android Studio and SDKs and will create an empty project, but you can delete the project after installation if you want. Example usage:

```bash
$ da crt android-studio --name my_test
INFO: Android studio was not found on system.
Downloading android studio takes a time. Do you want to continue?
Select [y/n]
y
INFO: Downloading android studio from https://dl.google.com/dl/android/studio/ide-zips/1.3.0.10/android-studio-ide-141.2117773-linux.zip
INFO: Downloading done
INFO: Downloading android SDK from http://dl.google.com/android/android-sdk_r24.3.3-linux.tgz
INFO: Downloading done
INFO: Copy android template project to project destination
INFO: .
[devassistant]$ cp -r /home/$USER/.devassistant/files/crt/android-studio/. "my_test"
INFO: For import project into Android Studio execute command:
INFO: /home/$USER/android-studio/bin/studio.sh my_test/build.gradle

```

To configure AVD manager run:
```bash
$ da crt android-studio --name my_test --avd
```

It will show AVD Manager where you can specify your mobile device.

To download SDKs run:

```bash
$ da crt android-studio --name my_test --sdk
```
This will show SDK Manager where you can specify Android SDKs to download and install.

## Troubleshooting

When starting Android Studio, you may get the following error:

> 'tools.jar' seems to be not in Studio classpath. Please ensure JAVA_HOME points to JDK rather than JRE.

Make sure you have Oracle JDK Installed, [grab it from here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Install:

```bash
$ rpm -ivh jdk-<version>-linux-x64.rpm
```

Upgrade:
```bash
$ rpm -Uvh jdk-<version>-linux-x64.rpm
```

Enable it using the `alternatives`

```bash
$ alternatives --config java
```

Confirm you're using the right java command:

```bash
$ alternatives --list | grep /usr/java
java    manual  /usr/java/jdk1.8.0_121/jre/bin/java
```

```bash
$ java -version
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```
