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
$ sudo nano /etc/yum.repos.d/mongodb-org-7.0.repo
```

Insert this content inside the mongodb-org-*release_series*.repo file, edit the *release_series* in the filename and the baseurl and gpgkey fields URLs if you want to install another version.

```
[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/7.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-7.0.asc
```

Now you can install with dnf. We install all the dependencies separately because by default the `mongodb-org` package is dependent on `mongodb-mongosh`. This package has a dependency on static openssl installed with nodeJS which differs from the version of openssl installed on fedora by default. Therefore, we install `mongodb-mongosh-shared-openssl3` which links with the native openssl library which is openssl 3.x.x.
([See tickets MONGOSH-1231 and MONGOSH-1270 for more information.](https://jira.mongodb.org/browse/MONGOSH-1270?jql=text%20~%20%22mongodb-mongosh-shared-openssl3%22))

```console
$ sudo dnf install mongodb-org mongodb-mongosh-shared-openssl3 openssl mongodb-org-database-tools-extra mongodb-database-tools mongodb-org-tools mongodb-org-server mongodb-org-mongos mongodb-org-database
```

**Warning:** MongoDB does not guarantee compatibility with Fedora Linux, so newer MongoDB server packages might fail to install. [See MongoDB issue ticket SERVER-58871](https://jira.mongodb.org/browse/SERVER-58870).

## Enable MongoDB services

Restart the computer and then enable and start MongoDB service by running the command:

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

## MongoDB Compass

[MongoDB Compass](https://www.mongodb.com/products/tools/compass) is a GUI for interfacing with MongoDB.

To install Compass, run the command to retrieve the files using wget.

```console
$ wget https://downloads.mongodb.com/compass/mongodb-compass-1.43.0.x86_64.rpm
```

Then, install the files using yum.

```console
$ sudo yum install mongodb-compass-1.43.0.x86_64.rpm
```

Now, run the GUI from the terminal using the command:

```console
$ mongodb-compass
```
[Source](https://www.mongodb.com/docs/compass/current/install/)
