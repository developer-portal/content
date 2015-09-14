---
title: Tutorials
page: devassistant
order: 1
---

For the tutorials presented here, we assume you already have DevAssistant
installed. If you do not, or you are not sure, check out the [installation
guide](#about.md/##Installing DevAssistant on Fedora). Now, let us try out
kickstarting the development with some concrete examples. Mind you that each
language has different needs, so the assistants for Python look a little
different than those for Perl. For the most part, however, the arguments like
the name of the project or your GitHub username are always the same.

## The Basics

To launch DevAssistant, either run the `da` (or `da-gui` for the GUI) binaries,
or find DevAssistant in your Applications menu. In these tutorials, we will use
the command-line `da` binary, but the usage of the GUI is very much the same.
Check out the [notes](#notes.md) for more information about the GUI.

If you are unsure what assistant to run, you can use the `--help` or `-h` flag:

    $ da --help

On top of that, there is the bash completion, so you can autocomplete possible
options by hitting the `TAB` key. You can add `--help` to any command to see
what assistants and options are available. You will then receive a help message
similar to this one:

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
    pkg      Lets you interact with online DAPI service and your local DAP packages.
    version  Print version

To find more about creating projects, you can run `da create --help`:

    usage:  create [-h] [--deps-only] {c,cpp,dap,java,nodejs,nulecule,perl,php,python,ruby} ...

    Kickstart new projects easily with DevAssistant.

    optional arguments:
    -h, --help            show this help message and exit
    --deps-only           Only install dependencies

    subassistants:
      Following subassistants will help you with setting up your project.

      {c,cpp,dap,java,nodejs,nulecule,perl,php,python,ruby}

The above help message lists available assistants used for creating projects,
so you can choose one to try out. For this tutorial, we will go with one of Python
assistants—Flask. However, the same approach works for any assistant you
choose.

    $ da create python --help

Running help at this point lists the available sub-assistants and arguments in
a familiar help message:

    usage: create python [-h] {django,flask,gtk3,lib} ...

    This is base Python assistant. You have to choose a specific project type.

    optional arguments:
    -h, --help            show this help message and exit

    subassistants:
      Following subassistants will help you with setting up your project.

    {django,flask,gtk3,lib}


## Getting Started with Flask

For simplicity, let us walk through setting up a project based on Flask. Flask
is a lightweight but robust Python web framework, and it is perfect for
creating a simple, mostly static home pages. If you want something bigger, you
can try Django—there is an assistant for that too.

First, let us display the help message for Flask to find out how you can create
and customize a Flask-based project:
```
$ da create python flask --help
```

    usage: create python flask [-h] [--venv] [-e [ECLIPSE]] [-g [GITHUB]] -n NAME [-r] [-v]

    Flask assistant will help you create a basic Flask project and install its
    dependencies.

    optional arguments:
    -h, --help            show this help message and exit
    --venv                Use virtualenv to set up project and install
                          dependencies.
    -e [ECLIPSE], --eclipse [ECLIPSE]
                          Configure as Eclipse project (uses ~/workspace or
                          specified directory)
    -g [GITHUB], --github [GITHUB]
                          Create a GitHub repository and push your sources there
                          (uses your system username or specified name)
    -n NAME, --name NAME  Name of project to create
    -r, --rpm             This will create SPEC file and install dependencies
                          for building RPM package.
    -v, --vim             Configure VIM editor for various programming languages

Say that you want to name your Flask app `MyFancyWebserver` and want to publish
the source code on GitHub. As you can figure out from the help message above,
you will have to run the following command:

    $ da create python flask --name MyFancyWebserver --github UserName

That is a bit long, is it not? You can write it in a much shorter way,
especially if your GitHub username is the same as that on your local machine:

    $ da crt python flask -n MyFancyWebserver -g

When you run that, DevAssistant does all the magic for you—installs
dependencies, creates files and directories, and more:

    INFO: Resolving RPM dependencies with DNF...
    Installing 2 RPM packages with DNF. Is this ok? [y(es)/n(o)/s(how)]: s
    python-flask-wtf-0.10.0-2.fc22.noarch
    python-wtforms-2.0-4.fc22.noarch
    Installing 2 RPM packages with DNF. Is this ok? [y(es)/n(o)/s(how)]: y
    Installing dependencies ........... Done.
    INFO: Creating Flask project MyFancyWebserver in . ...
    INFO: Registering your project on GitHub as UserName/MyFancyWebserver...
    INFO: Your new repository: https://github.com/UserName/MyFancyWebserver
    INFO: Adding Github repo as git remote ...
    INFO: Successfully added Github repo as git remote.
    INFO: Source code was successfully pushed.
    INFO: Flask project MyFancyWebserver in . has been created.
    INFO: To run the application use: ./manage.py runserver
    INFO: For more information about Flask project visit https://flask.pocoo.org/docs/tutorial/

As you can see, DevAssistant allows you to verify which packages are about to
be installed.  During the run of the assistant, you may be asked for the
administrator (root) password several times, especially during dependencies
installation. After the run is finished, you can see that the directory
`MyFancyWebserver` now exists, and that it is populated with files
automatically:

    $ tree MyFancyWebserver
    MyFancyWebserver/
    ├── application
    ├── httpd.MyFancyWebserver.conf
    ├── LICENSE
    ├── manage.py
    └── MyFancyWebserver
        ├── __init__.py
        ├── static
        │   └── style.css
        └── templates
            └── index.html

    3 directories, 7 files

You can then go to the directory and run `./manage.py runserver` as advised in
the DevAssistant log. You now have a fully functioning webserver after running
a single command in DevAssistant, and can start editing it with your favourite
editor.

## Publishing Existing Code to GitHub

If you are interested in DevAssistant, there is a good chance you are already
working on some code on your own, but that code is not yet published anywhere.
We have thought of that, and DevAssistant provides a `tweak` assistant that
does just that. Run it in your project's directory like this:

    $ da tweak github create --push

What this command does is create a repository for your GitHub username under
the name of the current directory, and pushes the sources there. If you so
wish, you can specify a different GitHub username or omit the `--push` flag to
only create the repository, but not push the code into it immediately.

## Checking out or Forking a GitHub repository

With DevAssistant, not only the creation of your own software is easy, but
the modification of others' code is too. To check out a GitHub repository, run:

    $ da prepare custom --repo UserName/RepoName

The UserName and RepoName are GitHub identifiers of the repository, so to check
out DevAssistant's own code, you would run `da prepare custom --repo
devassistant/devassistant`. However, you could do it even more easily, because
we provide our custom set of assistants, so `da prepare devassistant` is
enough.

An important part of the checkout process is looking for a `.devassistant`
configuration file that the developer may have included in the repo, and
installing dependencies or setting up your machine if you want that—It may be
necessary to install some packages for testing etc. You are always asked if you
want to execute the contents of the `.devassistant` file when checking out the
repo for added security.
