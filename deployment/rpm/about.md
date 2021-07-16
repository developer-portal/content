---
title: RPM Packaging
subsection: rpm
section: deployment
description: >
  How to package your application and ship it to RPM based systems.
---

# {{page.title}}

{{page.description}}

Biggest advantages of packaging your application is:

 * it puts together code, data, config files and post-installations scripts.
 * the package can be signed, therefore clients can verify that the package was not altered.
 * it standardize installation paths.
 * it describes requirements, which are automatically resolved by system.
 * it allows easy installation/upgrade/removal of your application.

## Setup

Run:

```bash
$ sudo dnf install fedora-packager rpmdevtools gcc
$ rpmdev-setuptree
$ cd ~/rpmbuild/SOURCES
$ wget http://ftp.gnu.org/gnu/hello/hello-2.10.tar.gz
$ cd ~/rpmbuild/SPECS
$ rpmdev-newspec --macros hello.spec
```

## Quick Start Guide

Now you can open hello.spec file and alter it. Put there this content:

```
Name:     hello
Version:  2.10
Release:  1%{?dist}
Summary:  The "Hello World" program from GNU
License:  GPLv3+
URL:      http://ftp.gnu.org/gnu/hello
Source0: https://ftp.gnu.org/gnu/hello/hello-%{version}.tar.gz

BuildRequires: gettext

Requires(post): info
Requires(preun): info

%description
The "Hello World" program, done with all bells and whistles of a proper FOSS
project, including configuration, build, internationalization, help files, etc.

%prep
%autosetup

%build
%configure
%make_build

%install
%make_install
%find_lang %{name}
rm -f %{buildroot}/%{_infodir}/dir

%post
/sbin/install-info %{_infodir}/%{name}.info %{_infodir}/dir || :

%preun
if [ $1 = 0 ] ; then
/sbin/install-info --delete %{_infodir}/%{name}.info %{_infodir}/dir || :
fi

%files -f %{name}.lang
%{_mandir}/man1/hello.1.*
%{_infodir}/hello.info.*
%{_bindir}/hello

%doc AUTHORS ChangeLog NEWS README THANKS TODO
%license COPYING

%changelog
* Tue Sep 06 2011 The Coon of Ty <Ty@coon.org> - 2.8-1
- Initial version of the package
```

Once you are done, you can run:

```bash
$ rpmbuild -ba hello.spec
```

Your package should be ready at `~/rpmbuild/RPMS/x86_64/hello-2.10-1.fc27.x86_64.rpm`.

This example is taken from [How to create a GNU Hello RPM package](https://fedoraproject.org/wiki/How_to_create_a_GNU_Hello_RPM_package). You can follow it there.


### Resources

You can learn more about all sections and tags of SPEC file at [Fedora documentation "How to create an RPM package"](https://fedoraproject.org/wiki/How_to_create_an_RPM_package) or at [RPM Packaging Guide](https://rpm-packaging-guide.github.io/).

If you prefer video over wiki, you can check recording of [Packaging Workshop](http://youtu.be/H4vxkuoimzc) at YouTube. Red Hat subscribers can check [Getting Started with RPMs](https://access.redhat.com/videos/214983) video.


## Packaging for other distribution

Command rpmbuild creates package only for architecture and distribution of your own workstation. If you want to create RPM for other distribution and other architecture, you need to use [Mock](https://github.com/rpm-software-management/mock/wiki). It can build packages for different architectures and different Fedora or RHEL versions than the build host has. Mock creates chroots and builds packages in them. Its only task is to reliably populate a chroot and attempt to build a package in that chroot.

### Setup

Run:

```bash
$ sudo dnf install mock mock-scm
$ sudo usermod -a -G mock YourUserName
$ newgrp mock
```

### Building package using Mock

Before you start using Mock, you have to have SRC.RPM (also called SRPM). You can create it using rpmbuild:

```bash
$ rpmbuild -bs hello.spec
```

Then you can run:

```bash
$ mock -r /etc/mock/epel-6-i386.cfg ~/rpmbuild/SRPMS/hello-2.10-1.fc27.src.rpm
```

This creates CentOS/RHEL package for i386 architecture even when your workstation architecture is x86_64 and your workstation is e.g. Fedora. List of available configurations can be found at `/etc/mock/` directory.

You can create RPM directly from git (or any other SCM) using mock-scm plugin. Just try:

```bash
$ mock -r fedora-22-x86_64 --scm-enable --scm-option method=git --scm-option package=PKG --scm-option git_get=set --scm-option spec=YOUR.SPEC --scm-option branch=master --scm-option write_tar=True --scm-option git_get='git clone git@git_ip_address:SCM_PKG.git SCM_PKG'
```

You can find more details in [mock-scm documentation](https://fedoraproject.org/wiki/Projects/Mock/Plugin/Scm).

More detailed tutorial can be found on page [Using Mock to test package builds](https://fedoraproject.org/wiki/Using_Mock_to_test_package_builds)

### Create Yum/Dnf repository

Once you have your RPM packages ready, you can put them in a directory (one directory per distribution-architecture) and run there:

```bash
$ sudo dnf install createrepo_c
$ cd where_are_your_packages/
$ createrepo_c --deltas --retain-old-md 1 ./
```

This will create Yum/Dnf repository. When you expose it to web and provide a link to it to users, they can use it as baseurl in a repo file (stored in /etc/yum.repos.d/), like:

```
[myproject]
name=Your application
baseurl=http://yourdomain.com/repository/
enabled=1
```

Note: If you are building an open-source software package, you can use [Copr service](/deployment/copr/about.html), which automates `mock` and `createrepo_c` part while it provides nice WebUI.
