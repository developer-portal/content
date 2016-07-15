---
title: Apache HTTP Server
subsection: web-app
order: 2
---

# What is Apache?

The Apache HTTP Server Project is an effort to develop and maintain an open-source HTTP server for modern operating systems including UNIX and Windows. The goal of this project is to provide a secure, efficient and extensible server that provides HTTP services in sync with the current HTTP standards.
The Apache HTTP Server ("httpd") was launched in 1995 and it has been the most popular web server on the Internet since April 1996. It has celebrated its 20th birthday as a project in February 2015.

The Apache HTTP Server is a project of [The Apache Software Foundation](http://www.apache.org/).

The Apache HTTP server is in Fedora known as httpd package. You will probably have this package already installed on your Fedora system. But in case you don't have it you can install it with this command:

```
sudo dnf install httpd
```

If you would like to start Apache server at each boot, type this command:
```
sudo systemctl enable httpd.service
```

For running Apache server immediately type this command:
```
sudo systemctl start httpd.service
```

Now you can test result of Apache installation by visiting your localhost page at [http://localhost](http://localhost). 

If is everything alright, you should see Fedora Test Page.
![](./images/screenshot.png?raw=true)
