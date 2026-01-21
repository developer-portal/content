---
title: Hosting metadata for software applications 
subsection: desktop
description: >
  How to host your GUI desktop application's metadata for yum/DNF or Flatpak in self- or Github-hosted repositories
---

# Hosting metadata for yum/DNF or Flatpak

Metadata for distribution tools and GNOME Software must be refreshed
periodically, such as when new versions of [packaged
applications](desktop-software.html) are released for consumption by
users.  In many cases, Linux distributions take care of the metadata
extraction, generation, and hosting for these purposes.  However, this
section provides information on how to host your own metadata in case
you need to do so.

## Install helper utilities

Install the following software to help parse and generate the metadata needed for hosting:

```console
$ sudo dnf install createrepo_c libappstream-glib-builder flatpak-builder
```

## Generating yum repository metadata

1. Run these commands to create the initial metadata for source
   packages and the standard *x86_64* architecture:

	```console
$ createrepo_c --no-database --simple-md-filenames SRPMS/
$ createrepo_c --no-database --simple-md-filenames x86_64/
	```

1. Next, generate the AppStream XML using the *appstream-builder*
   tool:

   ```console
$ appstream-builder				\
	--origin=yourcompanyname		\
	--basename=appstream			\
	--cache-dir=/tmp/asb-cache		\
	--enable-hidpi				\
	--max-threads=1				\
	--min-icon-size=32			\
	--output-dir=/tmp/asb-md		\
	--packages-dir=x86_64/			\
	--temp-dir=/tmp/asb-icons
Scanning packages...
Processing packages...
Merging applications...
Writing /tmp/asb-md/appstream.xml.gz...
Writing /tmp/asb-md/appstream-icons.tar.gz...
Writing /tmp/asb-md/appstream-screenshots.tar...
Done!
   ```

	The actual build output will depend on your compose server
    configuration. At this point you can also verify the application
    is visible in the *yourcompanyname.xml.gz* file.

1. Next, take the generated XML and the tarball of icons and add it to
   the *repomd.xml* master document, so that GNOME Software
   automatically downloads the content for searching:

	```console
$ modifyrepo_c					\
	--no-compress				\
	--simple-md-filenames			\
	/tmp/asb-md/appstream.xml.gz		\
	x86_64/repodata/
$ modifyrepo_c					\
	--no-compress				\
	--simple-md-filenames			\
	/tmp/asb-md/appstream-icons.tar.gz	\
	x86_64/repodata/
	```

	Deploying this metadata allows GNOME Software to add the
	application metadata the next time the repository is refreshed.

## Hosting a DNF repository on Github

While Github isn't ideal for hosting DNF repositories, this method currently works:

1. Once you've created a local copy of your repository, create a new
   project on Github. Then use the follow commands to import your
   repository into Github.

	```console
$ cd ~/src/myrepository
$ git init
$ git add -A
$ git commit -a -m "first commit"
$ git remote add origin git@github.com:yourgitaccount/myrepo.git
$ git push -u origin master
	```

1. Next, go to the Github web interface and browse down in the file
   tree until you find the file called *repomd.xml*, and click on
   it. You should now see a button in the Github interface called
   *Raw*. Click that to get the raw version of the XML file.  In the
   URL bar of your browser you should see a URL like this:

	```console
https://raw.githubusercontent.com/username/reponame/master/noarch/repodata/repomd.xml
	```

	Copy that URL, as you'll need it to create the *.repo* file that distributions and users use to reach your new repository.
	
1. Create a *.repo* file using this example as a template, and edit it to match your data:

	```console
[frobnicator]
name=Frobnicator 3D generator
baseurl=https://raw.githubusercontent.com/username/reponame/master/noarch
gpgcheck=0
enabled=1
enabled_metadata=1
	```

	For more information on this format, consult the [repository
    options in the DNF configuration documentation](http://dnf.readthedocs.io/en/latest/conf_ref.html#repo-options).
	
1. Copy this file to */etc/yum.repos.d* on your computer and load up
   GNOME Software. Click on the *Updates* button in GNOME Software,
   and then select the refresh button in the top left corner to ensure
   your database is up to date.  You should then be able to search in
   GNOME software and find your new application.

## Generating Flatpak metadata

The [Flatpak](https://flatpak.org) application packaging standard is another way to provide metadata for consumers. This guide assumes you are familiar with this standard, along with the [manifest and basic build operations required](http://docs.flatpak.org/en/latest/flatpak-builder.html).  You can find extensive information on building Flatpaks and on hosting and signing flatpak repostories [here](https://blogs.gnome.org/alexl/2017/02/10/maintaining-a-flatpak-repository/).

Create an empty repository in a *repo* folder with this command:

```console
$ ostree init --mode=archive-z2 --repo=repo
```

To tell flatpak-builder to import the end result of a build into this repository, pass the *--repo* option to use the folder you created:

```console
$ flatpak-builder --verbose --force-clean \
        --repo=repo --gpg-homedir=gpg --gpg-sign=$GPG_KEY \
	recipes flatpak/org.example.Frobnicator.json
```

To generate appstream branches and static deltas in this repository use this command:

```console
$ flatpak build-update-repo --generate-static-deltas \
        --gpg-homedir=gpg --gpg-sign=$GPG_KEY repo
```

Note that both of these commands take a *--gpg-sign* argument. Flatpak
uses GPG as a means to ensure that the repository can be trusted, so
you should sign your public repositories.

To make your application and its Flatpak repository available to users is to publish a flatpakref file:
	
```console
[Flatpak Ref]
Title=Frobnicator
Name=org.example.Frobnicator
Url=https://raw.githubusercontent.com/username/reponame/master/repo/
Branch=1.0
IsRuntime=False
GPGKey=...
RuntimeRepo=https://sdk.gnome.org/gnome.flatpakrepo
Comment=GNOME loves to Frobnicate
```

## Hosting a Flatpak repository on Github

Github isn't ideal for hosting Flatpak repositories, but this method currently works.

1. Once you create a local copy of your repository, create a new
   project on Github, enable Github pages for the project and point it
   at the master branch.

1. Next, import your repository into Github.

	```console
$ git remote add origin git@github.com:yourgitaccount/myrepo.git
$ git push -u origin master
	```

Now you should be able to refer to your repo with a
*raw.githubusercontent.com/* URL as shown in the flatpakrepo example
above.

## A note on third party repositories

For more information on inclusion in Fedora as a third party software
repository, consult with the [Fedora Workstation working
group](https://fedoraproject.org/wiki/Workstation).
