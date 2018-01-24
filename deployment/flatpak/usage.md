---
title: Flatpak Usage
subsection: flatpak
section: deployment
---

# {{page.title}}

## Installing Flatpak Applications

### Setting up the Flathub repository: 

A team of Flatpak developers have started a project known as [Flathub](https://flathub.org). Flathub aims to provide a centralized repository for making Flatpak applications available to users. Flathub covers more than the GNOME application suite, and is regularly adding new applications.

To add the Flathub repository, open the Terminal, and run:

```
$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```



### Installing Applications (GNOME Software): 

GNOME Software already supports Flatpak repositories, so applications can be installed directly from GNOME Software.

Simply open "Software" from the GNOME Overview, and search for your desired application. If it is available as a flatpak, you will see it's source labeled as "flathub.org".

Select the flatpak entry and click "Install".

After that, the application can be launched as usual.



### Installing Applications (Command Line):

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

* [FedoraMagazine - Getting Started with Flatpak](https://fedoramagazine.org/getting-started-flatpak/)
* [A Flatpak Hello World](http://flatpak.org/hello-world.html)
* [Flathub Applications](https://flathub.org/apps.html)

