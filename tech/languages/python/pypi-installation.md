---
title: Pip & PyPI
subsection: python
order: 2
---

# Using pip

If a Python package you need is not packaged for Fedora,
or if you need it in an isolated environment,
you can use `pip` to install it from the [Python Package Index (PyPI)](https://pypi.python.org/).

Note that software on PyPI is not part of Fedora, and has different standards of quality, security and licensing: essentially, anyone can upload code there.
Only install software you trust, and always double-check `install` commands for typos in package names.

You can either install such modules to a *virtual environment*, or to your home directory with the `--user` user switch. See below for both options.

Installing modules with pip to system directories is not recommended, as it can override system libraries and lead to an unstable system.


## Using pip in the virtual environment

The best practise is using pip in the virtual environment. It will keep all modules for one project at one place and it will not break your local system. Another advantage is that you can have more versions of the same module in different virtual environments.

Let's create a virtual environment called `project_venv` with the main Python 3 version in Fedora.
If you need to use another version of Python or a different interpreter such as PyPy, see the [Multiple Interpreters section](https://developer.fedoraproject.org/tech/languages/python/multiple-pythons.html).

```bash
$ python3 -m venv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

When the virtual environment is activated (you can see it's name in brackets at the beginning of your prompt), you can install modules with pip.
For example, if your project needs the [`requests`](https://requests.readthedocs.io/en/master/) library, run:

```bash
(project_venv) $ python -m pip install requests
```

When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

The environment is a directory.
If you no longer need it, deactivate it and delete it with `rm -rv project_venv`.


## User-specific installation

Sometimes, you don't want to use a virtual environment.
For example, you're installing a tool you will use in multiple projects, but the tool is not available in Fedora repositories.
In such cases, you might need to install `pip` if you do not already have it system-wide:

```bash
$ sudo dnf install python3-pip
```

Then, use pip's `--user` option.
For example, to install a Python implementation of `cowsay` (rather than the original Perl one available in Fedora), run:

```bash
$ python -m pip install --user cowsay
```


## Updating packages

Since software installed using `pip` is not part of Fedora, it is your responsibility to keep it updated as needed.
However you ran `pip install`, running it again with `--update` will update to the latest release.
For example, to update the `requests` library:

```bash
(project_venv) $ python -m pip install --update requests
```


### What next?

 * [PyPI - the Python Package Index](https://pypi.python.org/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
