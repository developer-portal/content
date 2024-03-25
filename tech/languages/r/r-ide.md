---
title: R IDE
subsection: r
order: 4
---

# Integrated Development Environments for R

## RStudio

[RStudio](https://rstudio.com/) is an integrated development environment (IDE) for R. It includes a console, syntax-highlighting editor that supports direct code execution, as well as tools for plotting, history, debugging and workspace management.

### RStudio Desktop

The desktop version can be installed as follows:

```bash
$ sudo dnf install rstudio-desktop
```

Then, RStudio will be available in your _Applications_ menu.

[![RStudio Desktop](/content/tech/languages/r/rstudio_downscale.png)](/content/tech/languages/r/rstudio.png){:target="_blank"}

### RStudio Server

Alternatively, a web-based interface to RStudio is available, which is more suitable for Fedora Server or headless installations. To install and run RStudio Server:

```bash
$ sudo dnf install rstudio-server
$ sudo systemctl enable --now rstudio-server
```

Then, you can access RStudio in a Web browser at [http://127.0.0.1:8787](http://127.0.0.1:8787).
You will see a login page, where you can authenticate using your user/password.
Note that RStudio Server binds to all interfaces by default (to 0.0.0.0), and thus it is recommended to block that port in the firewall.

## Alternatives

These alternative IDEs for R are also available in Fedora:

- `rkward`: Graphical front-end for the R language.
- `emacs-ess`: Emacs Speaks Statistics under GNU Emacs.
