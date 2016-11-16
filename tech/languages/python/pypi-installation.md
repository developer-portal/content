---
title: PyPI
subsection: python
order: 2
---

# Using pip

If a Python module you need is not packaged for Fedora, you can use pip to install it from [PyPI](https://pypi.python.org/), but you must be a little careful. Installing modules with pip to system directories can lead to unstable system, so make sure you only use pip with the ```--user``` switch, which makes pip install modules to your home directory.

Pip gets installed alongside with Python. For Python 3 it is `pip3`, so for example, you want to install `bokeh` (interactive plots in HTML for Python) from PyPI simply type:

```
$ pip3 install --user bokeh
```

And there you go!

## Using pip in the virtual environment

The best practise is using pip in the virtual environment. It will keep all modules for one project at one place and it will not break your local system. Another advantage is that you can have more versions of the same module in different virtual environments.

Let's create a virtual environment called `project_venv` which will contain the main Python 3 version in Fedora and pip. If you need to use another version of Python or different interpreter such as PyPy, see [Multiple Interpreters section](https://developer.fedoraproject.org/tech/languages/python/multiple-pythons.html).

```bash
$ pyvenv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

When the virtual environment is activated (you can see it's name in brackets at the beginning of your prompt), you can install modules with pip.

```bash
(project_venv) $ pip install module_name
```

When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

### What next?

 * [PyPI - the Python Package Index](https://pypi.python.org/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
