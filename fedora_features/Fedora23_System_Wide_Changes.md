---
title: System Wide Changes
section: fedoranext
subsection: fedoranext
---
## Fedora 23 Accepted System Wide Changes Proposals

These changes have been accepted by the Fedora Engineering Steering Committee for the Fedora 23 Release as System Wide Changes.

###Harden All Packages
Hardening is  the process of securing a system/application by reducing its unnecessary functions, or restricting access.
In Fedora 22 and before, it was up to the package maintainer to add %global _hardened_build 1 to their spec file to ensure their program was hardened. Beginning with Fedora 23 this will now become the defaults for all packages. You can compare the security by running the following as root:

####Owners
* Owner: Till Maas | Moez Roy | Florian Weimer
* Release notes owner:

###Mono 4###
Update the Mono stack in Fedora from 2.10 to 4.*

####Owners
* Owner: Claudio Rodrigo Pereyra Diaz
* Release notes owner:

###Disable SSL3 and RC4 by default###
This change will disable by default the SSL 3.0 protocol and the RC4 cipher in components which use the system wide crypto policy. That is, gnutls and openssl libraries, and all the applications based on them.

####Owners
* Owner: Nikos Mavrogiannopoulos
* Release notes owner:

###Changes/perl5.22 | Perl 5.22###
A new perl 5.22 version brings a lot of changes done over a year of development. Perl 5.22 should be released 5/20/2015. See  5.21.11 perldelta for more details about preparing release.

####Owners
* Owner: Petr Písař
* Release notes owner:

###Default Local DNS Resolver###
To install a local DNS resolver trusted for the DNSSEC validation running on 127.0.0.1:53. This must be the only name server entry in /etc/resolv.conf.

####Owners
* Owner: P J P |  Pavel Šimerda |  Tomas Hozza |  Petr Špaček
* Release notes owner:

###Fedora 23 Boost 1.59 Uplift
This change brings Boost 1.58.0 or later to Fedora 23. We generally aim to ship 1.59.0, as that seems likely to make it (hence the Change name), but 1.58.0 is out and available now.

####Owners
* Owner: Jon Wakely
* Release notes owner:

###Glibc locale subpackaging
This change should make it possible to install or uninstall locales individually.

####Owners
* Owner: Mike Fabian, Siddhesh Poyarekar,  Carlos O’Donell
* Release notes owner:

###SELinux policy store migration
The newest SELinux userspace project release 2015-02-02 includes a change of the location of the SELinux policy store, which defaults to /var/lib/selinux/.

####Owners
* Owner: Miroslav Grepl
* Release notes owner:

###Two Week Atomic
Fedora Atomic Host is an implementation of the Project Atomic pattern for a specialized operating system for the deployment of containerized applications. For the past two Fedora releases, we've included an Atomic Host cloud image as a non-blocking deliverable. However, upstream Atomic is moving very fast — by the end of the alpha, beta, final stabilization cycle Fedora uses, the released artifact is basically obsolete. Additionally, the Project Atomic team at Red Hat would like to do their ongoing development work in the Fedora upstream, and the six-month release cycle does not lend itself to that.

####Owners
* Owner:  Matthew Miller, Colin Walters, Joe Brockmeier, Kushal Das, Adam Miller, Dennis Gilmore
* Release notes owner:

###Unicode 8.0 support
Unicode 8.0 got release on 17th June 2015. It includes 41 new emoji characters (including five modifiers for diversity), 5,771 new ideographs for Chinese, Japanese, and Korean, the new Georgian lari currency symbol, and 86 lowercase Cherokee syllables. It also adds letters to existing scripts to support Arwi (the Tamil language written in the Arabic script), the Ik language in Uganda, Kulango in the Côte d’Ivoire, and other languages of Africa. In total, this version adds 7,716 new characters and six new scripts.

####Owners
* Owner: Mike Fabian  Pravin Satpute   Siddhesh Poyarekar
* Release notes owner:

