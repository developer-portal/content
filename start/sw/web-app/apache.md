---
title: Apache HTTP Server
subsection: web-app
order: 2
---

# What is Apache?

The Apache HTTP Server Project is an effort to develop and maintain an open-source HTTP server for modern operating systems including UNIX and Windows. The goal of this project is to provide a secure, efficient and extensible server that provides HTTP services in sync with the current HTTP standards.
The Apache HTTP Server was launched in 1995 and it has been the most popular web server on the Internet since April 1996. It has celebrated its 20th birthday as a project in February 2015. The Apache HTTP Server is a project of [The Apache Software Foundation](http://www.apache.org/).

# Installation

The Apache HTTP server is in Fedora known as ```httpd``` package. You will probably have this package already installed on your Fedora system. But in case you do not have it you can install it with this command:

```
sudo dnf install httpd
```

If you would like to start Apache server at each boot, type:
```
sudo systemctl enable httpd.service
```

For running Apache server immediately type:
```
sudo systemctl start httpd.service
```

Now you can try, if your Apache server is running by visiting your localhost page at [http://localhost](http://localhost). 

If is everything alright, you will see Fedora Test Page:

![](./images/screenshot.png?raw=true)

# How to run my own web presentation

The root directory of your web server is now situated at ```/var/www/html/```. 

**WARNING: Owner of this directory is root user!** 

For disabling web server to render Fedora Test Page, you have to comment out all lines in ```/etc/httpd/conf.d/welcome.conf```. After that, server will try to find page ```index.html``` in ```/var/www/html/``` directory.

You can create in this directory new file ```index.html``` with your customized content like:

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

Main server configuration file is situated at ```/etc/httpd/conf/httpd.conf```. Here you can change server root directory, server admin contact, supported file extension for index file (e.g. .htm, .php, .aspx etc. - you have to install that packages, which supported selected file extension) and many other things. For all possibilities, which you can set in this file, visit official Apache [getting started](https://httpd.apache.org/docs/current/getting-started.html) or [documentation](https://httpd.apache.org/docs/current/) page.

For applying new server settings, you have to reload apache and restart httpd service:

```
sudo apachectl reload
sudo systemctl restart httpd.service
```

# More information

For more information about Apache HTTP Server in Fedora you can visit [Fedora Wiki page](https://fedoraproject.org/wiki/Apache_HTTP_Server). 
For general information about Apache HTTP Server you can visit [Apache HTTP Server documentation page](https://httpd.apache.org/docs/current/).
