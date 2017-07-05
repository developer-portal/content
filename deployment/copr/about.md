---
title: Copr Build Service
subsection: copr
section: deployment
description: >
  Copr is a service that builds your application as an RPM and provides you
  with your own Dnf/Yum repository.
---

# {{page.title}}

[Copr](https://copr.fedoraproject.org/) is a service that builds your application as an RPM and provides you
  with your own Dnf/Yum repository.

Before you start, you need to have a source RPM (SRPM). If you do not know how to create a SRPM, then please check [RPM Packaging](../rpm/about.html) section of this documentation.

There is nice a [Screenshot Tutorial](https://docs.pagure.org/copr.copr/screenshots_tutorial.html#screenshots-tutorial), which describes every step.

If you prefer using the command line, there is [documentation of copr-cli](copr-cli.html).

Note: you can only use Copr for FOSS projects. More details can be found in the [What I can build in Copr](https://docs.pagure.org/copr.copr/user_documentation.html#what-i-can-build-in-copr) section of [Copr FAQ](https://docs.pagure.org/copr.copr/user_documentation.html#faq).
