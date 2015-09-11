---
title: About DevAssistant
page: devassistant
section: tools
description: Basic information about DevAssistant
---

# What is DevAssistant

## The Basics

DevAssistant is a tool that helps you start with developing software—for every
project, you need dependencies, a certain file and directory structure, and
often some services or the firewall set up. You no longer need to copy commands
from lengthy tutorials online before developing any web app, library, or a
software tool. Now only one DevAssistant command (or a few clicks in the GUI)
and you are done.  Imagine that running the following command in the command
line:

    $ da create java maven --name MyJavaApp --github

gets you a fully functioning Maven-based Java application with dependencies,
metadata, and a fresh GitHub repository with the code already uploaded. The
same can be said about mostly every major language, because there is an
assistant (a script) for that. Have a look at a few examples of how to run
DevAssistant in the [tutorials](#tutorials.md).

You can run DevAssistant from the command line, or you can use the graphical
user interface (GUI). We strongly recommend using the command line interface
for reasons described in the [notes](#notes.md).

## Installing DevAssistant on Fedora

If you are running Fedora Workstation, there is a good chance that you already
have DevAssistant and the common assistants installed. To check that, try
looking for DevAssistant in your Applications menu, or type `da` into the
command line. If you get something like this, you already have DevAssistant:

    Couldn't parse input, displaying help ...

    You can either run assistants with:
    da [--debug] {create,tweak,prepare,extras} [ASSISTANT [ARGUMENTS]] ...

    Where:
    create   used for creating new projects
    tweak    used for working with existing projects
    prepare  used for preparing environment for upstream projects
    extras   used for performing custom tasks not related to a specific project
    You can shorten "create" to "crt", "tweak" to "twk" and "extras" to "extra".

    Or you can run a custom action:
    da [--debug] [ACTION] [ARGUMENTS]

    Available actions:
    doc      Display documentation for a DAP package.
    help     Print detailed help.
    pkg      Lets you interact with online DAPI service and your local DAP
    packages.
    version  Print version

If you do not see such a message, you can get DevAssistant from GNOME Software,
or install it through DNF:

    $ sudo dnf install devassistant

If that is not possible for whatever reason, you may install DevAssistant from
[PyPI](https://pypi.python.org) using the command `pip3` from the package
`python3-pip`:

    $ pip3 install devassistant --user

If you do this, however, you will not have any assistants available, and will
have to [install them yourself](#about.md/##Installing New Assistants).

## Under the Hood

DevAssistants is essentially an engine that loads and executes scripts called
assistants, one for each workflow you need to cover—the assistants may be tied
to programming languages (e. g. C, Java, Ruby, Python), or generic tasks like
publishing your code to GitHub. There are a few assistants that are maintained
by the DevAssistant upstream developers, and there are more that were created
by the community. In Fedora's repositories, you will find mostly the first
kind, packaged under the names `devassistant-dap-NAME`). Do not worry though,
you can easily install third party assistants too.

## Assistants

As said above, the assistants are the scripts that DevAssistants uses to set up
your environment. They are written in
[YAML](https://en.wikipedia.org/wiki/YAML), and there are four major roles that
the assistants fall into:

* **Create** empty projects – You run a `create` assistant when you want to
  start writing a completely new project, one that isn't existing yet.
* **Tweak** current project – This sort of assistants are run on the code you
  are currently working, be it one that you created with DevAssistant, or
  someone else's. In [Tutorials](#tutorials.md), there is a tutorial on
  how to publish your code to GitHub with a `tweak` assistant
* **Prepare** someone's code – As opposed to `create` assistants, `prepare`
  assistants set up code of an existing project for you to contribute to.
  Except for cloning the code from the internet, they install dependencies you
  need for testing the project or create a fork of the original project on
  GitHub.
* **Extras** – In this role, you can find assistants that cover other
  actions you may want to perform on your code, like creating distribution
  packages, validation and verification, and anything else.

All roles have their shortened version (`crt`, `twk`, `prep`, `extra`) that can
be used when invoking DevAssistant command-line interface.

For a quick illustration, If you want to create a brand new application based
on Django (a Python web framework) which supports Docker containers, you need
to run a command that looks like this (`da` is short for DevAssistant):

    da create python django --name MyAppName --docker

If you want to see how test the application locally, you run the following
command in the project's directory to start the container that was created
along with the app:

    da tweak docker develop

All you need is to point your browser to the address the assistant provided you
with. If you want to go through a more detailed description of how to develop
with DevAssistant, visit the [tutorials page](#tutorials.md).

If you can not find an assistant on the [DevAssistant Package
Index](https://dapi.devassistant.org) for a workflow you use often, or there is
one missing for your project, you can write an assistant yourself. To see how,
see the [page for developers](#developers.md).

## Installing New Assistants

Getting DevAssistant the way described on the top of this page gets you also a
common set of assistants for major languages. These assistants are packaged in
Fedora under the names `devassistant-dap-NAME`, and they get updates when the
rest of the system is updated etc. You can, however, install third party
assistants from the [DevAssistant Package Index
(DAPI)](https://dapi.devassistant.org) if they are not available through Fedora
channels. To get the third party assistants, run:

    $ da pkg install PackageName

Where `PackageName` is the name of package you got on the web version of the
DAPI, or found by searching in the command line:

    $ da pkg search KeyWord

Alternatively, you may list all the available packages and choose from that:

    $ da pkg list --available

Installing through `da pkg install` saves the assistants in a hidden folder
(`.devassistant`) inside your home directory, so they are not available to
other users. Update the assistants by running:

    $ da pkg update

