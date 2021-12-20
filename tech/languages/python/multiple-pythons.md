---
title: Multiple Pythons
subsection: python
order: 3
---

# Multiple Python interpreters

If you are working on a piece of Python software, you probably want to test it
on multiple Python interpreters. On Fedora, that's easy: all you have to do is
use `dnf` to install what you need.

Fedora includes all Python versions which are [supported upstream](https://devguide.python.org/#status-of-python-branches), a few older ones and possibly a pre-release of a newer one.

At the time of this writing, Fedora has the following Pythons
ready for you in the repositories:
 
 * CPython 3.10
 * CPython 3.9
 * CPython 3.8
 * CPython 3.7
 * CPython 3.6
 * CPython 3.5<sup>💀</sup>
 * CPython 2.7
 * PyPy 2
 * PyPy 3
 * Jython<sup>💀</sup>
 * MicroPython

Quite a nest, isn't it?
You can install them like this:

```console
$ sudo dnf install python3.9  # to get CPython 3.9
$ sudo dnf install python3.8  # to get CPython 3.8
$ sudo dnf install python3.7  # to get CPython 3.7
$ sudo dnf install python3.6  # to get CPython 3.6
$ sudo dnf install python2.7  # to get CPython 2.7
$ sudo dnf install pypy2 pypy3 python3.10  # to get more at once
```

After that, you can run an interactive console or your script with, let's say,
CPython 3.6:

```console
$ python3.6
Python 3.6.12 (default, Aug 19 2020, 00:00:00) 
[GCC 10.2.1 20200723 (Red Hat 10.2.1-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

**Warning:** For production purposes you should use the `python3`
package only. Other CPython versions might be **unstable** or even **dangerous**
(either because they are extremely old or quite the contrary alpha/beta quality)
and are intended solely for development.

**\*** Interpreters marked with <sup>💀</sup> were removed in Fedora Linux 35 and are only available in Fedora Linux 34.

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
envlist = py27,py37,py38,py39,pypy,pypy3
skipsdist = True
[testenv]
commands=python say.py
```

The `envlist` directive defines the list of Pythons to test on.
Normally, tox assumes you are testing a project with its own `setup.py`. For
the simplicity of this demo, we are not using it, and we need to tell this to
tox via the `skipsdist` option.
Finally the `commands` in the `[testenv]` section tells tox what commands to run
for the test.
Normally, that would be `python setup.py test`, `pytest` or similar.

With `tox.ini` in place, run `tox` in the same directory:

``` console
$ tox
[...]
ERROR:   py27: commands failed
  py37: commands succeeded
  py38: commands succeeded
  py39: commands succeeded
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
  py37: commands succeeded
  py38: commands succeeded
  py39: commands succeeded
  pypy: commands succeeded
  pypy3: commands succeeded
  congratulations :)
```

If you want to use tox for your projects, you can learn more at
[the documentation](https://tox.readthedocs.io/).

## Creating virtual environments and installing packages

Fedora only packages Python modules for one current version of `python3`.
For all other interpreters, you will need to install packages
from [PyPI](https://pypi.python.org/pypi), the Python Package Index.

The best way is to use Python virtual environments.
The invocation to create them differs for different Python versions.
Packages installed in a virtual environment are only available once the
environment is activated.
Here you can see two demos that create a virtual environment in a folder
named `env` and install some package into it.

### Python 3 (including PyPy 3)

Recent versions of Python 3 include the `venv` module, which can create virtual
environments.
See the [PyPI & pip section](https://developer.fedoraproject.org/tech/languages/python/pypi-install.html) for details.

```console
$ python3.9 -m venv env  # create the environment
$ source env/bin/activate  # activate it
(env)$ python -m pip install requests  # install a package with pip
...
(env)$ python  # run python from that environment
Python 3.9.0 (default, Oct  6 2020, 00:00:00) 
[GCC 10.2.1 20200723 (Red Hat 10.2.1-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> ...
>>> exit()
(env)$ deactivate  # go back to "normal"
```

The environment is a directory.
If you no longer need it, deactivate it and delete it with `rm -rv env`.

### Python 2.7, PyPy 2

For other Python versions, a tool called `virtualenv` can create virtual
environments:

```console
$ sudo dnf install /usr/bin/virtualenv  # install the necessary tool
$ virtualenv --python /usr/bin/python2.7 env  # create the virtualenv
Running virtualenv with interpreter /usr/bin/python2.7
New python executable in env/bin/python2.7
Also creating executable in env/bin/python
Installing setuptools, pip...done.
$ source env/bin/activate  # activate it
(env)$ python -m pip install requests  # install a package with pip
...
(env)$ python  # run python from that virtualenv
Python 2.7.11 (default, Jul  8 2016, 19:45:00) 
[GCC 5.3.1 20160406 (Red Hat 5.3.1-6)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> ...
>>> exit()
(env)$ deactivate  # go back to "normal"
```



### Jython

**Warning:** Jython will be [removed from Fedora in Fedora 35](https://lists.fedoraproject.org/archives/list/users@lists.fedoraproject.org/thread/GCZL4Y63RPCSIHGX2KEJC5WRGTOKZVKS/).

The versions of virtualenv and tox packages in Fedora do not support Jython,
an interpreter that interoperates with the Java ecosystem.

If you need to support it, you will need to install
and use older virtualenv/tox versions from PyPI.

First, create and activate a virtual environment with a newer Python, preferably `python3`:

```console
$ python3 -m venv py3env
$ source py3env/bin/activate  # activate it
```

Then, install older packages (virtualenv 15 and tox 2) into it:

```console
(py3env)$ python -m pip install 'virtualenv<16' 'tox<3'
```

Now, whenever the Python 3 virtual environment is activated, you can invoke
tox 2 using the `tox` command.
Include `jython` in the `envlist` section in `tox.ini` to test
on that interpreters.

You can also use the older virtualenv to create environments for Jython:

```console
(py3env)$ python -m virtualenv --python /usr/bin/jython jyenv --no-setuptools --no-pip --no-wheel
```

To activate these, you don't need the `py3env` activated.
That is only needed to create them.

```console
$ source jyenv/bin/activate
(jyenv)$ python --version
Jython 2.7.1
```

To be able to install packages, run Jython's `ensurepip` command.
This will install a compatible version of `pip`.

```console
(jyenv)$ python -m ensurepip
(jyenv)$ python -m pip install requests
```

### MicroPython

MicroPython does not support virtual environments.
It does have a rudimentary pip replacement called
[upip](https://pypi.python.org/pypi/micropython-upip/), which you can use to
install packages that support MicroPython. Run it to find out more:

```console
$ micropython -m upip
```
