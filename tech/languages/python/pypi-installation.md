---
title: Pypi
subsection: python
order: 2
---

# Using pip

If a Python module you need is not packaged for Fedora, you can use pip to install it from PyPI, but you must be a little careful. Installing modules with pip to system directories can lead to unstable system, so make sure you only use pip with the ```--user``` switch, which makes pip install modules to your home directory.

Pip gets installed alongside with Python 2 and 3, so if, for example, you want to install bokeh (interactive plots in HTML for Python) from PyPI simply type:

```
$ pip install --user bokeh
```

And there you go! Note that this will make bokeh available from Python 2 only. If you want to use it from Python 3, use ```pip3```, as such:

```
$ pip3 install --user bokeh
```

As of right now Fedora's PyPy does not come with pip, please consult [upstream documentation](http://doc.pypy.org/en/latest/install.html?highlight=pip#installing-pypy) on how to get pip for PyPy.
