---
title: Web Application
subsection: web-app
section: start-sw
description: Short introduction to web application development
---

# Web Application Development

Web application development can be anything from classic server-side applications that render dynamic HTML pages, to real-time audio/video applications. What is common for all of them though, Fedora is here to offer all needed components and great development environment.

## Technologies used for web development

Except HTML, which is almost always improved by CSS, most developers add dynamic items to the web pages via JavaScript. For both, CSS nad JavaScript, libraries exist to make developers' tasks easier:

* [JQuery](https://jquery.com/), a fast, small, and feature-rich JavaScript library
* [React](https://reactjs.org/), a JavaScript library for building user interfaces
* [Angular](https://angular.io/), one framework for mobile and desktop
* [PatternFly](https://www.patternfly.org/) to build better experiences with repeatable, scalable design

A client application is most often a browser like Firefox or Chromium, which talks to the server via HTTP protocol. It does not need to be that case always, a client application might be also substituted by a [GUI]({% link content/start/sw/gui-app/about.md %}) or [terminal]({% link content/start/sw/cli-app/about.md %}) application.

### Languages often used for back-end development

* [Python]({% link content/tech/languages/python/flask-installation.md %})
* [Ruby]({% link content/tech/languages/ruby/ruby-installation.md %})
* [PHP]({% link content/tech/languages/php/php-installation.md %})
* [Node.js/JavaScript]({% link content/tech/languages/nodejs/nodejs.md %})
* [Golang]({% link content/tech/languages/go/go-installation.md %})
* [Rust]({% link content/tech/languages/rust/rust-installation.md %})

### Webservers for static pages or processing HTTP requests

* [Apache HTTPD]({% link content/start/sw/web-app/apache.md %})
* [Nginx]({% link content/start/sw/web-app/nginx.md %})

### Databases for more complex web applications

* [PostgreSQL]({% link content/tech/database/postgresql/about.md %})
* [MariaDB]({% link content/tech/database/mariadb/about.md %})

### Certificates

For web applications, the trafic between client and server machine goes over the Internet in many cases. To not reveal any sensitive information, many sites have utilized an SSL-secured connection over HTTP, shortly HTTPS.

To make it work properly, the server needs to have a valid certificate, which either is obtained and signed by one of the authorities, or can be generated using service [Let's Encrypt](https://letsencrypt.org/). Such certificates require management though, so read about how to secure your webserver with improved Certbot in the [Fedora magazine](https://fedoramagazine.org/secure-your-webserver-improved-certbot/).

## Editing the source-code

The following IDE are popular even for web development:

* [PyCharm](https://www.jetbrains.com/pycharm/), a popular IDE for Python development, is available as a [copr repository](https://copr.fedorainfracloud.org/coprs/phracek/PyCharm/)
* [Visual Studio Code](https://code.visualstudio.com/): Microsoft's famous Visual Studio, rewritten to a modern web-based platform based on open-source technologies, [read here](https://fedoramagazine.org/using-visual-studio-code-fedora/) how you can install it on your Fedora
* [Atom](https://atom.io/) is another modern IDE, which can be [installed easily on Fedora](https://fedoramagazine.org/install-atom-fedora/) as well

## More information
For learning more about web technologies, visit for example web [w3schools.com](https://www.w3schools.com/).
