---
title: Apache HTTP Server
subsection: web-app
order: 2
---

# What is Apache?

The Apache HTTP Server Project is an effort to develop and maintain an open source HTTP server for modern operating systems including UNIX and Windows. The goal of this project is to provide a secure, efficient and extensible server that provides HTTP services in sync with the current HTTP standards.
The Apache HTTP Server was launched in 1995 and it has been the most popular web server on the Internet since April 1996. It celebrated its 20th birthday as a project in February 2015. The Apache HTTP Server is a project of [The Apache Software Foundation](http://www.apache.org/).

# Installation

The Apache HTTP server is known as a ```httpd``` package in Fedora. You will probably have this package already installed on your Fedora system but in case you do not have it, install it with this command:

```
sudo dnf install httpd
```

To start the Apache server at each boot, type:
```
sudo systemctl enable httpd.service
```

To run the Apache server immediately, type:
```
sudo systemctl start httpd.service
```

To try if your Apache server is running, visit your localhost page at [http://localhost](http://localhost). 

If everything goes as expected, you will see the Fedora Test Page:

![](./images/screenshot.png?raw=true)

# How to run your own web presentation

The root directory of your web server is now situated at ```/var/www/html/```. 

**WARNING: The owner of this directory is the root user!** 

To disable rendering the Fedora Test Page, comment out all the lines in ```/etc/httpd/conf.d/welcome.conf```.
After that, create an ```index.html``` file with your customized content in the ```/var/www/html/``` directory, for example:

```html

<html>
    <head>
        <title>Hello world</title>
    </head>
    <body>
        Hello world!
    </body>
</html>

```

Now, when you visit [http://localhost](http://localhost), you will see your new index page.

# Server configuration

The main server configuration file is situated at ```/etc/httpd/conf/httpd.conf```. Here you can change the server root directory, server admin contact, supported file extension for the index file (e.g., .htm, .php, .aspx and so on; you have to install the packages which support your selected file extension) and many other things. For everything that you can set in this file, visit the official Apache [getting started](https://httpd.apache.org/docs/current/getting-started.html) or [documentation](https://httpd.apache.org/docs/current/) page.

To apply the new server settings, reload apache and restart httpd.service:

```
sudo apachectl reload
sudo systemctl restart httpd.service
```

# More information

For more information about the Apache HTTP Server in Fedora you can visit [Fedora Wiki page](https://fedoraproject.org/wiki/Apache_HTTP_Server). 
For general information about the Apache HTTP Server you can visit [Apache HTTP Server documentation page](https://httpd.apache.org/docs/current/).
