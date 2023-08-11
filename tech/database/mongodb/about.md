---
title: MongoDB
subsection: mongodb
section: tech-database
description: Document-oriented and NoSQL database
order: 4
---

# MongoDB 

MongoDB is a database that uses a document-oriented data model and used to be free and open source.

## Security

Fedora has determined that the Server Side Public Licensev1 (SSPL) is not a Free Software License. Therefore, we need to drop MongoDB from Fedora or never update it again. Never updating it would bring security issues, hence we decided to remove it.

References:
* [MongoDB removal from Fedora](https://fedoraproject.org/wiki/Changes/MongoDB_Removal)

## How to install a specific upstream version

First we need configure the package management system, please note that:

> DNF by default uses the global configuration file at /etc/dnf/dnf.conf and all \*.repo files found under /etc/yum.repos.d. The
latter is typically used for repository configuration and takes precedence over global configuration.

Create a file mongodb-org-*release_series*.repo

```console
$ sudo nano /etc/yum.repos.d/mongodb-org-6.0.repo
```

Insert this content inside the mongodb-org-*release_series*.repo file, edit the *release_series* in the filename and the baseurl and gpgkey fields URLs if you want to install another version.

```
[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/6.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc
```

Now you can install with dnf

```console
$ sudo dnf install mongodb-org
```

Currently some packages do not install, however those packages do not affect the functionality of MongoDB.

**Warning:** MongoDB does not guarantee compatibility with Fedora Linux, so newer MongoDB server packages might fail to install. [See MongoDB issue ticket SERVER-58871](https://jira.mongodb.org/browse/SERVER-58870).

## Enable MongoDB services

To enable and start MongoDB service run:

```console
$ sudo systemctl enable mongod.service
$ sudo systemctl start mongod.service
```

## Check MongoDB current status

```console
$ sudo systemctl status mongod.service
```

## Test MongoDB connection

Run mongoshell to test the connection:

```console
$ mongosh
Current Mongosh Log ID:	<ID>
Connecting to:		mongodb://<address:port>
Using MongoDB:		6.0.8
```

## MongoDB GUI (not tested)

[MongoDB Admin](https://github.com/hatamiarash7/MongoDB_Admin/wiki/1.-Getting-Start) is a Cross Platform GUI.
