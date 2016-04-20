---
title: Secondary Architectures
subsection: secondary_architectures
section: deployment
description: Building your application for architectures like s390(x), PowerPC, ARMv8

order: 1
---

# Secondary Architectures
In Fedora, we call s390(x), PowerPC and ARMv8 architectures as [Secondary Architectures](https://fedoraproject.org/wiki/Architectures#Secondary_Architectures). These are either not easily accessible or newly introduced as compared to [Primary Acrhitectures](https://fedoraproject.org/wiki/Architectures#Secondary_Architectures)

## Benefits

Developers generally have an Intel (i686/x86_64) based machine, so they can build and test their applications for that. A successful build and run of an application on one architecture (e.g. x86_64) doesn't ensure that it will compile and run successfully on other architectures (e.g. PowerPC) too. This is because behaviours like endianness, instruction set etc may vary by architectures. A developer can use Fedora Secondary architectures infrastructure to ensure that her application builds successfully on machines like PowerPC. This helps to make your application available to even larger audience.

## Pre-requisites

In Fedora, every application is shipped in [rpm](http://www.rpm.org/) format, which is also required to build an application using Fedora infrastructure. Most applications which meet [Fedora packaging licensing](https://fedoraproject.org/wiki/Packaging:Guidelines?rd=Packaging/Guidelines#Licensing) will be already available in Fedora.

Make sure you first follow below checklist before you start building your application using Fedora infrastructure:

* Check if rpm package of application is already [available in Fedora](https://apps.fedoraproject.org/packages/). If it is not packaged then please follow [RPM Packaging](https://developer.fedoraproject.org/deployment/rpm/about.html) guide to create one.
* Create a [Fedora Account System (FAS)](https://admin.fedoraproject.org/accounts) account and follow [basic process](https://fedoraproject.org/wiki/Join_the_package_collection_maintainers?rd=PackageMaintainers/Join#Create_a_Fedora_Account)
* Now, [create certificate](https://fedoraproject.org/wiki/Using_the_Koji_build_system#Fedora_Account_System_.28FAS2.29_Setup) in order to do build in [koji](https://fedoraproject.org/wiki/Koji) for available architetcures.

## Example

The following example (iprutils package) will demonstrate how to get an rpm package available in Fedora repository:

```
# Clone existing package available in Fedora repository e.g. iprutils
$ fedpkg clone -a iprutils && cd iprutils && ls
   0001-Service-start-is-controled-by-udev-rule.patch  iprdbg.8.gz  iprutils.spec  sources

# Fetch latest source available in Fedora repo for application iprutils
$ fedpkg sources && ls
   0001-Service-start-is-controled-by-udev-rule.patch  iprdbg.8.gz  iprutils  iprutils-2.4.11.1.tar.gz  sources

# Generates source rpm (*.src.rpm) for iprutils which we will use in ppc-koji to build
$ fedpkg srpm
  0001-Service-start-is-controled-by-udev-rule.patch  iprdbg.8.gz  iprutils-2.4.11.1-1.fc25.src.rpm  iprutils-2.4.11.1.tar.gz  iprutils.spec  sources

```

Further, to modify source or spec file follow below steps:

```
# Create required directory structure in ~/rpmbuild/
$ rpmbuild-setuptree

# Copy original or modified spec file in ~/rpmbuild/SPECS/ directory
$ cp 0001-Service-start-is-controled-by-udev-rule.patch ~/rpmbuild/SOURCES/
$ cp iprdbg.8.gz ~/rpmbuild/SOURCES
$ cp *.tar.gz ~/rpmbuild/SOURCES
$ cp iprutils.spec ~/rpmbuild/SOURCES/

# Create srpm file
$ rpmbuild -bs ~/rpmbuild/SOURCES/iprutils.spec

```
Generated srpm will be available in ~/rpmbuild/SRPMS/ directory

**Note:** iprutils package which is used as an example may get updated later on and hence content may change.
