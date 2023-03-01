---
title: Sphinx
subsection: python
order: 9
---

# Sphinx

[Sphinx](http://sphinx-doc.org/) is a tool for creating beautiful documentation for python projects. It uses [reStructuredText](http://docutils.sf.net/rst.html) as its markup language which it can build into various kinds of outputs. You can build HTML, PDF, manual pages and many others from one source! Sphinx can also link the documentation with your code and print syntax highlighted classes and functions. As extra, you can extend its functionality with many [plugins](http://sphinx-doc.org/develop.html#extensions) and style it with many prepared themes.


## Installation

To install Sphinx on Fedora, run:

```
$ sudo dnf install python3-sphinx
```


## Getting started

Navigate your terminal into project directory and run:

```
$ sphinx-quickstart
```

to initialize your documentation. You will be asked to choose the documentation directory, set the project name and provide some other basic information about it. Next, you will be asked which extensions you want to enable. Be sure to answer "yes" on creating Makefile for your documentation.

It may happen that will mis-type some answer or you just change your mind about it.
You can alter the configuration whenever you want by editing `conf.py` file.


## Writing your first text
As it was mentioned before, content for Sphinx is written in [reStructuredText](http://docutils.sf.net/rst.html), so in order to create new page in the documentation, you have to create a `.rst` file. For example `introduction.rst`:

```
Introduction
============

Here goes some introduction to your project and it is all written in rst format.
```

Now you have to open your master document, which is by default called `index.rst`.
Its serves as a welcome page and provides a table of contents for the documentation.
Therefore you should add link to `introduction.rst` here:

```
.. toctree::
   introduction
```

## See the results

Sphinx can process your content to the various output formats. Run `make help` to see all the possibilities. It should look like this:

```
$ make help
Please use `make <target>' where <target> is one of
  html       to make standalone HTML files
  dirhtml    to make HTML files named index.html in directories
  singlehtml to make a single large HTML file
  pickle     to make pickle files
  json       to make JSON files
  ...
```

You will probably want to use `html` for local testing purposes and `dirhtml` for deploying. You are able to test it by hitting `make html` to the command line. If Sphinx tells you that "Build finished. The HTML pages are in \_build/html", all is well. Open the web browser in the current working directory (if you are not sure which one it is, just run `pwd` to make sure), navigate to the build directory that Sphinx told you (i.e. `_build/html`) and open `index.html` -- your new documentation.

## latexpdf

In order to be able to run the `latexpdf` target, you will need to install the following dependencies:

``` sh
dnf -y install latexmk texlive-capt-of texlive-cmap texlive-ec texlive-fncychap texlive-framed texlive-makeindex texlive-metafont texlive-needspace texlive-parskip texlive-tabulary texlive-tex-gyre texlive-upquote texlive-wrapfig
```

Additionally, you need to install babel support for your project's language. for example, if your default language is English, install `texlive-babel-english`:

``` sh
dnf -y install texlive-babel-english
```

After that, you can continue building the target:

``` sh
make latexpdf
```

## What next
- See working examples to get an inspiration [Sphinx examples](http://sphinx-doc.org/examples.html)
- See the full Sphinx possibilities and features [Sphinx contents](http://sphinx-doc.org/contents.html)
