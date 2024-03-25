---
title: Flatpak Usage
subsection: flatpak
order: 4
---

# {{page.title}}

## Installing Flatpak Applications

## Setting up the Flathub repository:

Flathub is a a growing collection of apps which can be easily installed on any Linux distribution. Once setup, you can browse and install from an app center, like GNOME Software or KDE Discover. Alternatively, you can browse and install apps from the website or using the command line.

To add the Flathub repository, open the Terminal, and run:

```
$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

To add the Fedora Flatpaks repository (built in Fedora), run:

```
$ flatpak remote-add --if-not-exists fedora oci+https://registry.fedoraproject.org
```

## Installing Flatpaks On Gnome (GNOME Software):

GNOME Software already supports Flatpak repositories, so applications can be installed directly from GNOME Software.

Simply open "Software" from the GNOME Overview, and search for your desired application. If it is available as a flatpak, you will see it's source labeled as "flathub.org".

Select the flatpak entry and click "Install".

After that, the application can be launched as usual.



## Installing Flatpaks On KDE (KDE Discover):

Starting in Discover 5.12, Discover now supports Flatpak repositories, so you can directly install flatpak applications from it.

Simply open Discover and browse or search through the app lists as normal. Similar to Gnome Software, applications that are available as flatpaks will list "Flatpak" as it's source.

Upon installations, applications can be launched as usual.



## Installing Applications (Command Line):

The `flatpak` command also lists and installs apps and runtimes. To list all apps available in a specific repository, run the `remote-ls` command:

```
$ flatpak remote-ls flathub --app
```

Then, install an app with the `install` command:

```
$ flatpak install flathub org.gnome.Polari
```

Once installed, you can use the `run` command to run the application:

```
$ flatpak run org.gnome.Polari
```



## Further Reading

* [Flathub Applications](https://flathub.org/apps.html)
* [Fedora Flatpaks](https://docs.fedoraproject.org/en-US/flatpak/tutorial/)
