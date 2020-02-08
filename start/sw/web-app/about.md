---
title: Web Application
subsection: web-app
section: start-sw
description: Short introduction to web application development
---

# Web Application Development

Web application development is a broad topic, which covers range of different technologies. Under web application, we can imagine anything from classic server-side apps that render dynamic HTML pages, to real-time audio/video apps which allow us to watch movies or videochat online. Even if we only focus on the applications that users display in the web browser, a full-stack web developer needs to know dozens of technologies. What is common for all of them though, Fedora is here to offer all needed components and great development environment.

For learning more about web technologies, visit for example web [w3schools.com](https://www.w3schools.com/).

## Technologies used for web development

One technology that is almost always needed is HTML, a markup language for describing rich documents, which is almost always combined with CSS to make the HTML elements to look nice. To make the web applications more dynamic in the browser, JavaScript is used, often through some framework or libraries like JQuery or React. Even for the CSS styling, there are libraries to make the web applications look better and not reimplement all from scratch. One great example of such library is [patternfly](https://www.patternfly.org/).

That all mentioned so far, the front-end, is just one part. Another part is a back-end, that is usually written in dynamic languages like [Python]({% link tech/languages/python/flask-installation.md %}), [Ruby]({% link tech/languages/ruby/ruby-installation.md %}), [PHP]({% link tech/languages/php/php-installation.md %}), [JavaScript]({% link tech/languages/nodejs/nodejs.md %}), or some new, even compiled ones like [Golang]({% link tech/languages/go/go-installation.md %}) or [Rust]({% link tech/languages/rust/rust-installation.md %}). In simple scenarios, the static HTML pages might be only served by a web server ([Apache]({% link start/sw/web-app/apache.md %})) or [Nginx]({% link start/sw/web-app/nginx.md %})). As an opposite, most complex applications usually work with a database, on top of the code of the application itself. The most favourite open-source relational databases are [PostgreSQL]({% link tech/database/postgresql/about.md %}) or [MariaDB]({% link tech/database/mariadb/about.md %}).

A client application is most often a browser like Firefox or Chromium, which talks to the server via HTTP protocol. It does not need to be that case always, a client application might be also substituted by a [GUI]({% link start/sw/gui-app/about.md %}) or [terminal]({% link start/sw/cli-app/about.md %}) application.

## Certificates

No matter which technology you use on the server-side, what is common for the web applications is that the trafic between client and server machine goes over the Internet. To not reveal any sensitive information, many sites have utilized an SSL-secured connection over HTTP, shortly HTTPS. To work properly, the server needs to have a valid certificate, which either is obtained and signed by one of the authorities, or can be generated using service [Let's Encrypt](https://letsencrypt.org/). Such certificates require management though, so read about how to secure your webserver with improved Certbot in the [Fedora magazine](https://fedoramagazine.org/secure-your-webserver-improved-certbot/).

## Editing the source-code

For writing code in such heterogeneous environment, one needs a good IDE editor. Wes, `vim` works as great, but there are some alternatives available in the Fedora OS as well.

[PyCharm](https://www.jetbrains.com/pycharm/), a very popular IDE for Python development, is available as a [copr repository](https://copr.fedorainfracloud.org/coprs/phracek/PyCharm/). Microsoft's famous Visual Studio, rewritten to a modern web-based platform based on open-source technologies, is called [Visual Studio Code](https://code.visualstudio.com/) -- [read here](https://fedoramagazine.org/using-visual-studio-code-fedora/) how you can install it on your Fedora. [Atom](https://atom.io/) is another modern IDE, which can be [installed easily](https://fedoramagazine.org/install-atom-fedora/) as well.

