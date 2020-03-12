---
title: Python
subsection: python
section: tech-languages
order: 1
version: 3.5.2
description: General-purpose, high-level programming language supporting multiple programming paradigms.
---

# Python in Fedora

[Python](https://www.python.org/) is a widely used, interpreted, object-oriented, high-level programming language with dynamic semantics. It is simple and easy to learn.
Python 3 is already pre-installed on Fedora. Let's use it!

## Running Python

1. Open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black square icon or just press `Enter`).
2. To run Python 3 type `python3`. You should see something like this:

```python
Python 3.5.2 (default, Sep 14 2016, 11:28:32)
[GCC 6.2.1 20160901 (Red Hat 6.2.1-1)] on linux
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

## Using virtualenv

When you work on a project, it is good to keep it inside a virtual environment. It will keep the dependencies you need in one place and you do not have to worry about different projects which need different versions of the same module.

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
(project_venv) $ pip install name_of_module
```

That is all, you have successfully created your own virtual environment. Now you can run Python (see above) and start working on your project.

When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

### What next?

* [Python homepage](https://www.python.org/)
* [Python 3 Documentation](https://docs.python.org/3/)
* [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)

## Python 2

If you are looking for the older major version of Python, Fedora also includes Python 2.7.

* [Python 2 Documentation](https://docs.python.org/2/)
