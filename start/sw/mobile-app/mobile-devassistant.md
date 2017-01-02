---
title: Google Android Studio
subsection: mobile-app
order: 2
---

# How to install Google Android Studio on Fedora


First of all install [DevAssistant](https://devassistant.org) project:

```
$ sudo dnf install devassistant
```

Install DAP plugin [Google Android studio](https://github.com/phracek/dap-google-android-studio) for DevAssistant:

```
$ da pkg install android-studio
```

If you want to install only packages which are needed by Google Android Studio, run:

```
$ da crt --deps-only android-studio --name <your_project_name>
```

For installation Google Android Studio run:

```
$ da crt android-studio --name <name_of_your_project>
```

which downloads the latest versions Google Android Studio and SDKs.

```
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

For configuring AVD manager run:
```
$ da crt android-studio --name my_test --avd
```

This automatically shows AVD Manager where you can specify your mobile device.

For downloading SDKs run:

```
$ da crt android-studio --name my_text --sdk
```
This automatically shows SDK Manager where you can specify Android SDK which you would like to download and use it.

 
