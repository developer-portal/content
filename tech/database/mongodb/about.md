---
title: MongoDB
subsection: mongodb
section: tech-database
description: Document-oriented and NoSQL database
order: 4
---

# MongoDB 

MongoDB is a free and open source database and uses a document-oriented data model.

## Installation 

```
# dnf install mongodb mongodb-server
# service mongod start
```

## How to install a specific version 

First we need configure the package management system, please note that:

> DNF by default uses the global configuration file at /etc/dnf/dnf.conf and all *.repo files found under /etc/yum.repos.d. The
latter is typically used for repository configuration and takes precedence over global configuration.

Access the directory and create a file mongodb-org-*release_series*.repo

```
$ cd /etc/yum.repos.d/
$ sudo touch mongodb-org-4.0.repo  
```

Insert this content inside mongodb-org-*release_series*.repo, edit if you want install another version.

```
[Mongodb]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/4.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
```

Now you can install with dnf

```
$ sudo dnf install -y mongodb-org
```

## Run mongoDB 

Start mongoDB service and after run mongoshell to test connection  

```
$ sudo service mongod start
$ mongo
MongoDB shell version: 4.0.0
connecting to: test
```

## MongoDB GUI (Project is not updated since 2016 year!) 

Mongotron is a a Mongo DB GUI which uses Electron and AngularJS

It's easy install and run:

```
$ git clone git@github.com:officert/mongotron.git
$ cd mongotron/
$ npm install
$ npm start
```
