---
title: Adding Applications to GNOME Software
section: deployment
subsection: desktop
description: >
  How to build and package your GUI desktop applications for easy deployment by your users
---

# Adding Applications to GNOME Software

The GNOME Software app provides a cross-distribution software center from which users can browse and manage apps for their Linux system.  This guide will help you produce the necessary metadata so your app can be listed in the software center.  Note that this guide covers apps as opposed to other system add-on components such as drivers and codecs.

![GNOME Software](/content/deployment/desktop/steam-gnome-software.png  "Example of Steam listing in GNOME Software")

This guide assumes an application package called Frobnicator, which contains an executable called *frob*.  It also assumes you are running Fedora Workstation with the standard GNOME desktop environment.

## Install helper utilities

Install the following packages on your Fedora system to help assemble
and validate the metadata for your application:

```console
$ sudo dnf install desktop-file-utils appstream-util gnome-shell-extension-screenshot-window-sizer
```

## Create a desktop application file

1. Write a *.desktop* file that follows the [Desktop File
   Specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#introduction).
   The required fields are *Name*, *Comment*, *Icon*, *Categories*,
   *Keywords*, and *Exec*.  Here is an example:
   
   ```console
[Desktop Entry]
Type=Application
Name=Frobnicator
Comment=Frobnicate a PNG into a 3D object
Icon=frob
Exec=frob %f
MimeType=application/x-frob;
Categories=Graphics;3DGraphics;Engineering;
Keywords=3d;solid;geometry;csg;model;stl;
	```
	
   Your package should install this file in the
   */usr/share/application* folder.  You may assign the desktop file a
   short name such as *frob.desktop* in this example.  However, new
   applications typically use a reverse-DNS style name, for example
   *org.example.Frobnicator.desktop*.

1. Create a PNG icon for the file at least 64x64 in size, with a
   transparent background.  The icon should be named as in the *Icon*
   field above, for example *frob.png*.  Your package should install
   this file in one of the following locations:
   - */usr/share/icons*
   - */usr/share/icons/hicolor/apps*
   - */usr/share/${app_name}/icons*
   
1. Verify the desktop file with the *desktop-file-validate* command:

   ```console
$ desktop-file-validate org.example.Frobnicator.desktop
   ```
   
## Create an AppData file

The AppData file provides XML metadata that follows the [AppStream
specification](https://www.freedesktop.org/software/appstream/docs/),
and is used by the GNOME Software app to display the app to users in
the software center.

1. Create an XML file for your application that follows the template
   below. Note that you should consult the [AppStream
   specification](https://www.freedesktop.org/software/appstream/docs/)
   to provide correct data for your application in this file.  Here is
   an example for the Frobnicator app:
   
   ```console
    <?xml version="1.0" encoding="UTF-8"?>
    <component type="desktop">
      <id>org.frobnicator.Frobnicator.desktop</id>
      <metadata_license>CC0-1.0</metadata_license>
      <project_license>GPL-2.0+</project_license>
      <name>Frobnicator</name>
      <summary>Frobnicate a PNG into a 3D object</summary>
      <description>
        <p>You can use Frobnicator to turn a PNG file into a 3D object magically, if you have the appropriate Frob interface card installed on your system.</p>
      </description>
      <screenshots>
        <screenshot type="default">
          <image>https://frobnicator.org/git/browse/frobnicator/plain/data/appdata/frob-startup.png</image>
          <caption>Initial screen for the application</caption>
        </screenshot>
      </screenshots>
      <releases>
        <release version="1.0.0" date="2017-12-02">
          <description>
            <p>This is the first stable release</p>
          </description>
        </release>
      </releases>
      <url type="homepage">https://example.org/Frobnicator</url>
      <provides>
        <binary>frob</binary>
      </provides>
      <mimetypes>
        <mimetype>application/x-frob</mimetype>
      </mimetypes>
    </component>
	```

1. Next, make the appropriate 16:9 aspect ratio screenshots for your
   package, showing the application in action.  To make screenshot
   creation easier, use the GNOME Shell extension called *Screenshot
   Window Sizer* which you installed earlier.  To resize the window of
   your application to 16:9 format, focus it and press *Ctrl+Alt+s*.
   Your application window is resized to a perfect 16:9 aspect ratio
   so you can screenshot it with *Alt+PrtScn*.
   
   Store the screenshots at the URL referenced in your AppData XML file.

1. Validate the AppData XML file:

	```console
$ appstream-util validate foo.appdata.xml
	```

NOTE: Do not install two applications with one single package. If
necessary, split up a package into multiple subpackages or mark one
*.desktop* file with *NoDisplay=true*. In this case, make sure the
application subpackages depend on any *-common* subpackage, and that
you deal with upgrades (perhaps using a metapackage) if you’ve shipped
the application before.

Normally distributions take care of hosting operations from this
point.  However, if you want to host your own metadata for use with
yum/DNF or Flatpak, [this guide](hosting-metadata.html) may be of use.
