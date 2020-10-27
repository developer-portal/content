---
title: Python
subsection: python
section: tech-languages
order: 1
version: 3.9.0
description: General-purpose, high-level programming language supporting multiple programming paradigms.
---

# Python in Fedora

[Python](https://www.python.org/) is a widely used, interpreted, object-oriented, high-level programming language with dynamic semantics. It is simple and easy to learn.
Python 3 is already pre-installed on Fedora. Let's use it!

## Running Python

1. Open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black square icon or just press `Enter`).
2. To run Python 3 type `python3`. You should see something like this:

```python
Python 3.9.0 (default, Oct  6 2020, 00:00:00) 
[GCC 10.2.1 20201005 (Red Hat 10.2.1-5)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Now you can start to write in Python! Let's print _Hello World_!

```python
print('Hello World!')
```

If you want to **exit** Python, press `Ctrl` + `D`.

To run a program written in Python, type `python3` followed by the path and name of the program. Like this:

```bash
$ python3 example.py
```

The command `python` (without the `3`) will also work.
You can also use a specific version of Python, like `python3.9`, if you have that interpreter installed.
See the [Multiple Interpreters section](https://developer.fedoraproject.org/tech/languages/python/multiple-pythons.html) for details.


## Python packages

Fedora contains many popular packages for Python.
Usually, they are named with a `python3-` prefix, such as `python3-requests`.

These are useful for scripting and exploring Python and for Fedora-specific applications.
For software development or reproducible data analysis, it is better to use virtual environments.


## Using virtual environments

When you work on a project, it is good to keep it inside a virtual environment. It will keep the dependencies you need in one place and you do not have to worry about different projects which need different versions of the same module.
It also makes it easy to collaborate with people who don't use Fedora yet.

Let's create a virtual environment called `project_venv` which will contain Python and pip. You can use pip to install a project's dependencies.

```bash
$ python3 -m venv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

When the virtual environment is activated (you can see its name in brackets at the beginning of your prompt), you can install modules via `pip install`.

```bash
(project_venv) $ python -m pip install requests
```

That is all, you have successfully created your own virtual environment. Now you can run Python (see above) and start working on your project.

When you finish your work, you can deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

Note that packages installed system-wide are not available in the virtual environments:
by default, virtual environments are isolated from the system.
As an alternative, you can create the environment with `--system-site-packages` -- but note that when you update your Fedora packages, they may get out of sync with modules installed inside the environment.


### What next?

* [Python homepage](https://www.python.org/)
* [Python 3 Documentation](https://docs.python.org/3/)
* [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)

## Python 2

If you are looking for the older major version of Python, Fedora also includes Python 2.7.

* [Python 2 Documentation](https://docs.python.org/2/)
