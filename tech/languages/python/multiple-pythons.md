---
title: Multiple Pythons
subsection: python
order: 8
---

# Multiple Python interpreters

If you are working on a piece of Python software, you probably want to test it
on multiple Python interpreters. On Fedora, that's easy: all you have to do is
use `dnf` to install what you need. Currently Fedora has the following Pythons
ready for you in the repositories:
 
 * CPython 3.9
 * CPython 3.8
 * CPython 3.7
 * CPython 3.6
 * CPython 3.5
 * CPython 3.4
 * CPython 2.7
 * CPython 2.6\*
 * PyPy
 * PyPy 3
 * Jython\*
 * MicroPython\*

Quite a nest, isn't it?
You can install them like this:

```console
$ sudo dnf install python39  # to get CPython 3.9
$ sudo dnf install python38  # to get CPython 3.8
$ sudo dnf install python37  # to get CPython 3.7
$ sudo dnf install python34  # to get CPython 3.4
$ sudo dnf install python26  # to get CPython 2.6
$ sudo dnf install pypy pypy3 jython python35  # to get more at once
```

After that, you can run an interactive console or your script with, let's say,
CPython 3.4:

```console
$ python3.4
Python 3.4.3 (default, Jul 11 2016, 11:30:44) 
[GCC 5.3.1 20160406 (Red Hat 5.3.1-6)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

**Warning:** For production purposes you should use the `python3` or `python2`
packages only. Other CPython versions might be **unstable** or even **dangerous**
(either because they are extremely old or quite the contrary alpha/beta quality)
and are intended solely for development.

**\*** Interpreters marked with \* do not work with Tox and virtualenv
packaged in Fedora.
For using tox, virtualenv or pip with these interpreters, see the bottom
sections of this page.

## Getting it and running it all with tox

[Tox](https://tox.readthedocs.io/) is tool that helps you test your Python code
on multiple Pythons. If you install it on Fedora via the dnf package manager,
you'll automatically get all supported CPythons and PyPys:

```console
$ sudo dnf install tox
```

If you are not yet familiar with tox, don't worry. This short example will show
you how to start.

Let's create a directory and a simple Python file in it that will say something nice:

```python
# say.py
print('Fedora is the best OS for Python developers', end='\n\n')
```

Now we'll test if it works with all the Pythons, with tox.
We'll create a simple configuration file for tox, `tox.ini`, in the same
directory:

```
[tox]
envlist = py27,py35,py36,pypy,pypy3
skipsdist = True
[testenv]
commands=python say.py
```

The `envlist` directive defines the list of Pythons to test on.
Normally, tox assumes you are testing a project with its own `setup.py`. For
the simplicity of this demo, we are not using it, and we need to tell this to
tox via the `skipsdist` option.
Finally the `commands` in `[testenv]` section tells tox what commands to run
for the test, normally that would be `python setup.py test`, `py.test` or
similar.

With `tox.ini`, just run tox in the same directory:

``` console
$ tox
[...]
ERROR:   py27: commands failed
  py35: commands succeeded
  py36: commands succeeded
ERROR:   pypy: commands failed
  pypy3: commands succeeded
```

As you can see, there's something wrong with the script: it only works on
Python 3. The full tox output (omitted here) contains the exact error.
If you want to support old Python 2 as well, you'll have to fix it:

```python
# say.py
from __future__ import print_function
print('Fedora is the best OS for Python developers', end='\n\n')
```

```console
$ tox
[...]
  py27: commands succeeded
  py35: commands succeeded
  py36: commands succeeded
  pypy: commands succeeded
  pypy3: commands succeeded
  congratulations :)
```

If you want to use tox for your projects, you can learn more at
[the documentation](https://tox.readthedocs.io/).

## Creating virtualenvs and installing packages

Fedora only packages Python modules for current versions of `python2`
and `python3`. For all other interpreters, you will need to install packages
from [PyPI](https://pypi.python.org/pypi), the Python Package Index.

The best way is to use Python virtual environments (virtualenvs, or venvs).
The invocation to create them differs for different Python versions.
Packages installed in a virtualenv are only available once the virtualenv
is activated. Here you can see two demos that create virtualenv in a folder
named `env` and install some package into it.

### Python 3 (including PyPy 3)

Recent versions of Python 3 include the `venv` module, which can create virtual
environments.

```console
$ python3.5 -m venv env  # create the virtualenv
$ . env/bin/activate  # activate it
(env)$ python -m pip install requests  # install a package with pip
...
(env)$ python  # run python from that virtualenv
Python 3.5.2 (default, Aug 16 2016, 21:50:46) 
[GCC 5.3.1 20160406 (Red Hat 5.3.1-6)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> ...
(env)$ deactivate  # go back to "normal"
```

### Python 2.7, PyPy 2

For other Python versions, a tool called `virtualenv` can create virtual
environments:

```console
$ dnf install /usr/bin/virtualenv  # install the necessary tool
$ virtualenv --python /usr/bin/python2.7 env  # create the virtualenv
Running virtualenv with interpreter /usr/bin/python2.7
New python executable in env/bin/python2.7
Also creating executable in env/bin/python
Installing setuptools, pip...done.
$ . env/bin/activate  # activate it
(env)$ python -m pip install requests  # install a package with pip
...
(env)$ python  # run python from that virtualenv
Python 2.7.11 (default, Jul  8 2016, 19:45:00) 
[GCC 5.3.1 20160406 (Red Hat 5.3.1-6)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> ...
(env)$ deactivate  # go back to "normal"
```

To learn more about virtualenvs, visit
[The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/dev/virtualenvs/).

### Python 2.6, Jython

The versions of virtualenv and tox packages in Fedora do not support the
following interpreters:
* Python 2.6
* Jython

If you really need to support such old interpreters, you will need to work around some issues or install
and use older virtualenv/tox from PyPI.

A workaround for Python 2.6 is to chnage the `install` and the `list_dependencies` commands with a `tox.ini` configuration like:

```
[testenv:py26]
install_command = pip install {opts} {packages}
list_dependencies_command = pip freeze
basepython = python2.6
```

A more generic approach is to install an older version of tox that still supports these python versions:

First, create a virtual environment with a newer Python, preferably `python3`:

```console
$ python3 -m venv py3env
$ . py3env/bin/activate  # activate it
```

Then, install older packages (virtualenv 15 and tox 2) into it:

```console
(py3env)$ python -m pip install 'virtualenv<16' 'tox<3'
```

Now, whenever the Python 3 virtual environment is activated, you can invoke
tox 2 using the `tox` command.
Include `py26` and/or `jython` in the `envlist` section in `tox.ini` to test
on the old interpreters.

You can also use the older virtualenv to create environments for
Python 2.6 or Jython:

```console
(py3env)$ python -m virtualenv --python /usr/bin/python2.6 py26env
(py3env)$ python -m virtualenv --python /usr/bin/jython jyenv
```

To activate these, you don't need the `py3env` activated.
That is only needed to create them.

```console
$ . py26env/bin/activate
(py26env)$ python --version
Python 2.6.9
(py26env)$ deactivate
```

```console
$ . jyenv/bin/activate
(jyenv)$ python --version
Jython 2.7.1
(jyenv)$ deactivate
```

### MicroPython

MicroPython does not support virtual environments.
It does have a rudimentary pip replacement called
[upip](https://pypi.python.org/pypi/micropython-upip/), which you can use to
install packages that support MicroPython. Run it to find out more:

```console
$ micropython -m upip
```

