#**Adding Applications to the GNOME Software Center**

**Copyright 2016, Richard Hughes, Red Hat**
** Copyright 2017, Christian F.K. Schaller, Red Hat**

##Abstract

Traditionally we have had little information about Linux applications before they have been installed. With the creation of a software center we require access to rich set of metadata about an application before it is deployed so it it can be displayed to the user and easily installed.
This document is meant to be a guide for developers who wish to get their software appearing in the Software stores in Fedora Workstation and other distributions. Without the metadata described in this document your application is likely to go undiscovered by many or most linux users, but by reading this document you should be able to relatively quickly prepare you application.

![GNOME Software](/home/cschalle/Pictures/steam-gnome-software.png  "Example of Steam listing in GNOME Software")

###Introduction

Installing applications on Linux has traditionally involved copying binary and data files into a directory and just writing a single desktop file into a per-user or per-system directory so that it shows up in the desktop environment.  In this document we refer to applications as graphical programs, rather than other system add-on components like drivers and codecs. This document will explain why the extra metadata is required and what is required for an application to be visible in the software center. We will try to document how to do this regardless of if you choose to pakcage your application as a rpm package or as a flatpak bundle. The current rules is a combination of various standards that have evolved over the years and will will try to summarize and explain them here, going from bottom to top. 

###System Architecture
####Linux File Hierarchy
Applications on Linux are expected to install binary files to /usr/bin, the install architecture independent data files to /usr/share/ and configuration files to /etc. Small temporary files can be stored in /tmp and much larger files in /var/tmp. Per-user configuration is either stored in the users home directory (in ~/.config) or stored in a binary settings store such as dconf.
See the File Hierarchy Standard[[4](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)] for more information.

###Desktop files
Desktop files have been around for a long while now and are used by almost all Linux desktops to provide the basic description of a desktop application that your desktop environment will display. Like a human readable name and an icon. 

So the creation of a desktop file on Linux allows a program to be visible to the graphical environment, e.g. KDE or GNOME Shell. If applications do not have a desktop file they must be manually launched using a terminal emulator. Desktop files must adhere to the Desktop File Specification[[1](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#introduction) ] and provide metadata in an ini-style format such as:

- Binary type, typically ‘Application’
- Program name (optionally localized)
- Icon to use in the desktop shell
- Program binary name to use for launching
- Any mime types that can be opened by the applications (optional)
- The standard categories the application should be included in (optional)
- Keywords (optional, and optionally localized)
- Short one-line summary (optional, and optionally localized)

The desktop file should be installed into /usr/share/applications for applications that are installed system wide. An example desktop file provided below:

	[Desktop Entry]
	Type=Application
	Name=OpenSCAD
	Icon=openscad
	Exec=openscad %f
	MimeType=application/x-openscad;
	Categories=Graphics;3DGraphics;Engineering;
	Keywords=3d;solid;geometry;csg;model;stl;
	Keywords[de]=3D;solid;Geometrie;csg;Modell;stl;

*Text 1:  example desktop file for the OpenScad project*

The desktop files are used when creating the software center metadata, and so you should verify that you ship a .desktop file for each built application, and that these keys exist: Name, Comment, Icon, Categories, Keywords and Exec and that desktop-file-validate correctly validates the file. There should also be only one desktop file for each application.

The application icon should be in the PNG format with a transparent background and installed in /usr/share/icons, /usr/share/icons/hicolor/*/apps/*, or /usr/share/${app_name}/icons/*. The icon should be at least 64×64 in size.

The file name of the desktop file is also very important, as this is the assigned ‘application ID’. New applications typically use a reverse-DNS style, e.g. org.gnome.Nautilus.desktop but older programs may just use a short name, e.g. gimp.desktop. It is important to note that the file extension is also included as part of the desktop ID.

You can verify your desktop file using the command 'desktop-file-validate'.  You just run it like this:

	desktop-file-validate myapp.desktop

This tools is available through the desktop-file-utils package, which you can install on Fedora Workstation using this command

	dnf install desktop-file-utils

###AppData Files
At least one valid AppData file with the suffix .appdata.xml file should be installed into /usr/share/appdata with a name that matches the name of the .desktop file, e.g. gimp.desktop & gimp.appdata.xml or org.gnome.Nautilus.desktop & org.gnome.Nautilus.appdata.xml.

In the AppData file you should include several 16:9 aspect screenshots along with a compelling translated description made up of multiple paragraphs. 

In order to make it easier for you to do screenshots in 16:9 format we created a small GNOME Shell extension called 'Screenshot Window Sizer'. You can install it on Fedora Workstation through the Software tool.
Once it is installed you can resize the window of your application to 16:9 format by focusing it and pressing 'ctrl+alt+s'. It should resize your application window to a perfect 16:9 aspect ratio and let you screenshot it.

Make sure you follow the style guide, which can be tested using the appstream-util command line tool. appstream-util is part of the 'appstream' package in Fedora Workstation.:

	appstream-util validate foo.appdata.xml
	
If you don't already have the appstream-util installed it can be installed using this command on Fedora Workstation:

	dnf install appstream

What is allowed in an AppData file is defined in the AppStream specification[[2](https://www.freedesktop.org/software/appstream/docs/)] but common items typical applications add is:

- License of the upstream project in SPDX identifier format [[6](https://spdx.org/licenses/)], or ‘Proprietary’
- A translated name and short description to show in the software center search results
- A translated long description, consisting of multiple paragraphs, itemized and ordered lists.
- A number of screenshots, with localized captions, typically in 16:9 aspect ratio
- An optional list of releases with the update details and release information.
- An optional list of kudos which tells the software center about the integration level of the application
- A set of URLs that allow the software center to provide links to help or bug information
- An optional gettext or QT translation domain which allows the AppStream generator to collect statistics on shipped application translations.

A typical (albeit somewhat truncated) AppData file is shown below:

	<?xml version="1.0" encoding="UTF-8"?>
	<component type="desktop">
	  <id>org.gnome.MultiWriter.desktop</id>
	  <metadata_license>CC0-1.0</metadata_license>
	  <project_license>GPL-2.0+</project_license>
	  <name>MultiWriter</name>
	  <name xml:lang="bs">Grupni pisač</name>
	  <summary>Write an ISO file to multiple USB devices at once</summary>
	  <summary xml:lang="bs">Zapišite ISO datoteku na nekoliko USB uređaja odjednom</summary>
	  <description>
	    <p>GNOME MultiWriter can be used to write an ISO file to multiple USB devices at once. Supported drive sizes are between 1GB and 32GB.</p>
	    <p xml:lang="bs">Gnomov Grupni pisač može da se koristi za zapisivanje ISO datoteke na nekoliko USB uređaja odjednom. Podržane veličine diskova su od 1GB do 32GB.</p>
	  </description>
	  <screenshots>
	    <screenshot type="default">
	      <image>https://git.gnome.org/browse/gnome-multi-writer/plain/data/appdata/gmw-startup.png</image>
	      <caption>Initial screen for the application</caption>
	      <caption xml:lang="bs">Početni ekran programa</caption>
	    </screenshot>
	  </screenshots>
	  <releases>
	    <release version="3.20.0" date="2016-03-21">
	      <description>
	        <p>This is the first stable release for GNOME 3.20</p>
	      </description>
	    </release>
	  </releases>
	  <kudos>
	    <kudo>AppMenu</kudo>
	    <kudo>HiDpiIcon</kudo>
	    <kudo>ModernToolkit</kudo>
	  </kudos>
	  <url type="homepage">https://wiki.gnome.org/Apps/MultiWriter</url>
	  <url type="bugtracker">https://bugzilla.gnome.org/browse.cgi?product=gnome-multi-writer</url>
	  <translation type="gettext">gnome-multi-writer</translation>
	</component>

####Some Appstream background

The AppStream specification is a mature and evolving standard that allows upstream applications to provide metadata such as localized descriptions, screenshots, extra keywords and content ratings for parental control. The basic concept is that the upstream project ships one extra AppData XML file which is used to build a global application catalog called an AppStream file. Over 1000 open source projects now include AppData files, and the software center shipped in Fedora, Ubuntu and OpenSuse is an easy-to-use application filled with useful application metadata. Applications without AppData files are no longer shown which provides quite some incentive to upstream projects wanting visibility in popular desktop environments.

AppStream[[2](https://www.freedesktop.org/software/appstream/docs/) ] was first introduced in 2008 and since then many people have contributed to the specification. It is being used primarily for application metadata but also now is used for drivers, firmware, input methods and fonts. There are multiple projects producing AppStream metadata and also a number of projects consuming the final XML metadata.

When applications are being built as packages by a distribution then the AppStream generation is done automatically, and you do not need to do anything other than installing a .desktop file and an appdata.xml file in the upstream tarball or zip file.

If the application is being built on your own machines or cloud instance then the distributor will need to generate the AppStream metadata manually. This would for example be the case when internal-only or closed source software is being either used or produced. This document assumes you are currently building RPM packages and exporting yum-style repository metadata for Fedora or RHEL although the concepts are the same for rpm-on-OpenSuse or deb-on-Ubuntu.

NOTE: If you are building packages, make sure that there are not two applications installed with one single package. If this is currently the case split up the package so that there are multiple subpackages or mark one of the .desktop files as NoDisplay=true. Make sure the application-subpackages depend on any -common subpackage and deal with upgrades (perhaps using a metapackage) if you’ve shipped the application before.

###Summary of Package building
The steps outlined above explain the extra metadata that you need for your application to show up in GNOME Software. This tutorial does not cover how to set up your build system to build these, but both for  Meson and autotools you should be able to find a plethora of examples online. 
And there are also major resources available to explain how to create a [Fedora RPM](https://fedoraproject.org/wiki/How_to_create_an_RPM_package) or [how to build a Flatpak](http://docs.flatpak.org/en/latest/). You probably also want to tie both the Desktop file and the AppData file into your i18n system so the metadata in them can be translated.

It is worth nothing here that while this document explains how you can do everything yourself, we do generally recommend relying on existing community infrastructure for hosting source code and packages if you can (for instance if your application is open source), as they will save you work and effort over time. For instance putting your source code on GNOME's git will make it easy for the GNOME translation teams to work on your application and thus increase the chance that it gets translated in many languages. And by building your package in Fedora you can get peer review of your package and free hosting of the resulting package. We are also working on a service that will automatically generate a Flatpack bundle of your application in Fedora, meaning you get a Flatpak version of your application with no extra effort.

##Setting up hosting infrastructure for your package
We will here explain how you set up a Yum repository for RPM packages that provides the needed metadata. If you are making a Flatpak we recommend skipping ahead to the Flatpak section a bit further down.

###Yum hosting and metadata
When GNOME Software checks for updates it downloads various metadata files from the server describing the packages available in the repository. GNOME Software can also download AppStream metadata at the same time, allowing add-on repositories to include applications that are visible in the software center.

In most cases distributors are already building binary RPMS and then building metadata as an additional step by running something like this to generate the repomd files on a directory of packages. The tool for creating the repository metadata is called createrepo_c and is part of the package createrepo_c in Fedora. You can install it by running the command:

	dnf install createrepo_c

Once the tool is installed you can run these commands to generate your metadata: 

	$ createrepo_c --no-database --simple-md-filenames SRPMS/
	$ createrepo_c --no-database --simple-md-filenames x86_64/
		
This creates the primary and filelist metadata required for updating on the command line. Next to build the metadata required for the software center we we need to actually generate the AppStream XML. The tool you need for this is called appstream-builder. This works by decompressing .rpm files and merging together the .desktop file, the .appdata.xml file and preprocessing icons and screenshots. Remember, only applications installing AppData files will be included in the metadata.

You can install appstream-builder in Fedora Workstation by using this command:

	dnf install libappstream-glib-builder

Once it is installed you can run it by using the following syntax:

	$ appstream-builder				\
		--origin=yourcompanyname		\
		--basename=appstream		\
		--cache-dir=/tmp/asb-cache	\
		--enable-hidpi				\
		--max-threads=1			\
		--min-icon-size=32			\
		--output-dir=/tmp/asb-md		\
		--packages-dir=x86_64/		\
		--temp-dir=/tmp/asb-icons
This takes a few minutes and generates some files to the output directory.  Your output should look something like this:

	Scanning packages...
	Processing packages...
	Merging applications...
	Writing /tmp/asb-md/appstream.xml.gz...
	Writing /tmp/asb-md/appstream-icons.tar.gz...
	Writing /tmp/asb-md/appstream-screenshots.tar...
	Done!


The actual build output will depend on your compose server configuration. At this point you can also verify the application is visible in the yourcompanyname.xml.gz file.

We then have to take the generated XML and the tarball of icons and add it to the repomd.xml master document so that GNOME Software automatically downloads the content for searching. This is as simple as doing:

	modifyrepo_c					\
		--no-compress				\
		--simple-md-filenames		\
		/tmp/asb-md/appstream.xml.gz	\
		x86_64/repodata/
	modifyrepo_c					\
		--no-compress				\
		--simple-md-filenames		\
		/tmp/asb-md/appstream-icons.tar.gz	\
		x86_64/repodata/
		
Deploying this metadata will allow GNOME Software to add the application metadata the next time the repository is refreshed, typically, once per day.

####Hosting your Yum repository on Github
Github isn't really set up for hosting Yum repositories, but here is a method that currently works. So once you created a local copy of your repository create a new project on github. Then use the follow commands to import your repository into github.

	cd ~/src/myrepository
	git init
	git add -A
	git commit -a -m "first commit"
	git remote add origin git@github.com:yourgitaccount/myrepo.git
	git push -u origin master

Once everything is important go into the github web interface and drill down in the file tree until you find the file called 'repomd.xml' and click on it. You should now see a button the github interface called 'Raw'. Once you click that you get the raw version of the XML file and in the URL bar of your browser you should see a URL looking something like this:

	https://raw.githubusercontent.com/cschalle/hubyum/master/noarch/repodata/repomd.xml

Copy that URL as you will need the information from it to create your .repo file which is what distributions and users want in order to reach you new repository. To create your .repo file copy this example and edit it to match your data:

	[remarkable]
	name=Remarkable Markdown editor software and updates
	baseurl=https://raw.githubusercontent.com/cschalle/hubyum/master/noarch
	gpgcheck=0
	enabled=1
	enabled_metadata=1

So on top is your Repo shortname inside the brackets, then a name field with a more extensive name. For the baseurl paste the URL you copied earlier and remove the last bits until you are left with either the 'norach' directory or your platform directory for instance x86_64.

Once you have that file completed put it into /etc/yum.repos.d on your computer and load up GNOME Software. Click on the 'Updates' button in GNOME Software and then on the refresh button in the top left corner to ensure your database is up to date. If everything works as expected you should then be able to do a search in GNOME software and find your new application showing up.
![Example GNOME Software listing](/home/cschalle/Pictures/example-gnome-software-listing.png  "Example GNOME Software listing")


###Flapak hosting and Metadata
The flatpak-builder binary generates AppStream metadata automatically when building applications if the appstream-compose tool is installed on the flatpak build machine. Flatpak[5] repositories are exported with a separate ‘appstream’ branch which is automatically downloaded by GNOME Software and no additional work is required when building your application or updating the remote. Adding the remote is enough to add the application to the software center, on the assumption the AppData file is valid.

Extensive information on building flatpaks and on hosting and signing flatpak repostories can be found elsewhere[7].
In summary, to create an empty repository, you use:

        ostree init --mode=archive-z2 --repo=repo

To tell flatpak-builder to import the end result of a build into this repository, you pass --repo=repo:
        
        flatpak-builder --verbose --force-clean \
                                --repo=repo \
                                --gpg-homedir=gpg --gpg-sign=$GPG_KEY \
                                recipes flatpak/org.gnome.Recipes.json

To generate appstream branches and static deltas in this repository, you use:

        flatpak build-update-repo --generate-static-deltas --gpg-homedir=gpg --gpg-sign=$GPG_KEY repo

Note that both of these commands take a --gpg-sign argument. Flatpak uses GPG as a means to ensure that the repository
can be trusted, so you should sign your public repositories.

The best way to make your application and its Flatpak repository available to users is to publish a flatpakref file for it:
	
	[Flatpak Ref]
	Title=GNOME Recipes
	Name=org.gnome.Recipes
	Url=https://raw.githubusercontent.com/matthiasclasen/recipes-releases/master/repo/
	Branch=1.0
	IsRuntime=False
	GPGKey=...
	RuntimeRepo=https://sdk.gnome.org/gnome.flatpakrepo
	Comment=GNOME loves to cook

### Hosting a Flatpak repository on Github
Github isn't really set up for hosting Flatpak repositories, so we can't guarantee that this will keep working in the future. So once you created a local copy of your repository create a new project on github, enable github pages for the project and point it at the master branch.
Then use the follow commands to import your repository into github.

	cd ~/src/myrepository
	git init
	git add -A
	git commit -a -m "first commit"
	git remote add origin git@github.com:yourgitaccount/myrepo.git
	git push -u origin master

Now you should be able to refer to your repo with a raw.githubusercontent.com/ URL like the one shown in the flatpakrepo
example above.

###Getting it into Fedora Workstation
You now have your repository created and ready for users to connect to it. The final step is getting your repository added to Fedora Workstation.
To start the process for this you can file a [Fedora ticket](https://bugzilla.redhat.com/enter_bug.cgi?product=Fedora) against the Fedora-workstation-repositories component. The information needed is a decription of your application. We also need the URL where the repository is located.

This will allow the Fedora Workstation Working group to review your application and ask any needed follow-up questions. For more in depth-information about the process and rules for including 3rd party software in Fedora Workstation you can see the [Third Party Software for Fedora](https://fedoraproject.org/wiki/Workstation/Third_party_software_proposal) page.

###Conclusions
AppStream files allow us to build a modern software center experience either using legacy distro packages with yum-style metadata or with the new flatpak application deployment framework. By including a desktop file and AppData file for your Linux binary build your application can be easily installed by end users.
###Future Work
AppData currently uses the OARS content rating system which will be expanded for more uses cases and filtering options.
###	Related Work
The ODRS[3] is a web service which provides end-user moderated application reviews using the AppStream application ID.
###Acknowledgments
Much gratitude has to go to Red Hat for funding my work on this for the last few years. I have to also thank all the early-adopter projects that took a leap of faith for the software center I was trying to achieve.
###Citations
1. [Desktop Specification: 17th October 2016](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#introduction) 
2. [AppStream Specification 0.10: 17th October 2016](https://www.freedesktop.org/software/appstream/docs/) 
3. [Open Desktop Review System: 17th October 2016](https://odrs.gnome.org/) 
4. [Filesystem Hierarchy Standard: 17th October 2016](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) 
5. [Flatpak Homepage: 17th October 2016](http://flatpak.org/)
6. [SPDX license list](https://spdx.org/licenses/)
7. [Maintaining a Flatpak repository](https://blogs.gnome.org/alexl/2017/02/10/maintaining-a-flatpak-repository/)