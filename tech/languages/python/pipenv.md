---
title: Pipenv
subsection: python
order: 11
---

# Pipenv

Pipenv is a tool that aims to bring the best of all packaging worlds (bundler,
composer, npm, cargo, yarn, etc.) to the Python world.

It automatically creates and manages a virtualenv for your projects, as well as
adds/removes packages from your Pipfile as you install/uninstall packages. It
also generates the ever-important Pipfile.lock, which is used to produce
deterministic builds.

Here we will see

- How to install `pipenv` on fedora?
- How to create a virtual environment with `python3`?
- How to install python packages in the virtual environment?
- How to use the virtual environment?
- How to remove this virtual environment?

## Installation

To install `pipenv` on your machine,

```bash
$ sudo dnf install pipenv
```

Once it is done, you can use `pipenv` to create, manage and remove python
environments with different python versions.

Let's see what all opetions `pipenv` provides.

## Usage

```
$ pipenv --help
Usage: pipenv [OPTIONS] COMMAND [ARGS]...

Options:
  --where                         Output project home information.
  --venv                          Output virtualenv information.
  --py                            Output Python interpreter information.
  --envs                          Output Environment Variable options.
  --rm                            Remove the virtualenv.
  --bare                          Minimal output.
  --completion                    Output completion (to be executed by the
                                  shell).

  --man                           Display manpage.
  --support                       Output diagnostic information for use in
                                  GitHub issues.

  --site-packages / --no-site-packages
                                  Enable site-packages for the virtualenv.
                                  [env var: PIPENV_SITE_PACKAGES]

  --python TEXT                   Specify which version of Python virtualenv
                                  should use.

  --three / --two                 Use Python 3/2 when creating virtualenv.
  --clear                         Clears caches (pipenv, pip, and pip-tools).
                                  [env var: PIPENV_CLEAR]

  -v, --verbose                   Verbose mode.
  --pypi-mirror TEXT              Specify a PyPI mirror.
  --version                       Show the version and exit.
  -h, --help                      Show this message and exit.


Usage Examples:
   Create a new project using Python 3.7, specifically:
   $ pipenv --python 3.7

   Remove project virtualenv (inferred from current directory):
   $ pipenv --rm

   Install all dependencies for a project (including dev):
   $ pipenv install --dev

   Create a lockfile containing pre-releases:
   $ pipenv lock --pre

   Show a graph of your installed dependencies:
   $ pipenv graph

   Check your installed dependencies for security vulnerabilities:
   $ pipenv check

   Install a local setup.py into your virtual environment/Pipfile:
   $ pipenv install -e .

   Use a lower-level pip command:
   $ pipenv run pip freeze

Commands:
  check      Checks for PyUp Safety security vulnerabilities and against PEP
             508 markers provided in Pipfile.

  clean      Uninstalls all packages not specified in Pipfile.lock.
  graph      Displays currently-installed dependency graph information.
  install    Installs provided packages and adds them to Pipfile, or (if no
             packages are given), installs all packages from Pipfile.

  lock       Generates Pipfile.lock.
  open       View a given module in your editor.
  run        Spawns a command installed into the virtualenv.
  shell      Spawns a shell within the virtualenv.
  sync       Installs all packages specified in Pipfile.lock.
  uninstall  Uninstalls a provided package and removes it from Pipfile.
  update     Runs lock, then sync.
```

### Creating a virtual environment.

To create a new virtualenv with a `python3` interpreter.

```
$ pipenv --python 3
Creating a virtualenv for this project…
Pipfile: /home/fedorauser/pipenv-dir/Pipfile
Using /usr/bin/python3.8 (3.8.2) to create virtualenv…
⠼ Creating virtual environment...Already using interpreter /usr/bin/python3.8
Using base prefix '/usr'
New python executable in /home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2/bin/python3.8
Also creating executable in /home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2/bin/python
Installing setuptools, pip, wheel...
done.
Running virtualenv with interpreter /usr/bin/python3.8

✔ Successfully created virtual environment!
Virtualenv location: /home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2
Creating a Pipfile for this project…
```

It will create a file called `Pipfile` in your current directory.

You can get the project location using

```
$ pipenv --where
/home/fedorauser/pipenv-dir
```

To get the virtualenv location for this project

```
$ pipenv --venv
/home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2
```

To get the python interpreter location for this `virtualenv`

```
$ pipenv --py
/home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2/bin/python
```

### Installing packages

Now that we have the virtualenv created, let's install some packages.
It can be done with `pipenv install`.

```
$ pipenv install
Installing dependencies from Pipfile.lock (db4242)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

This will install packages listed in the `Pipfile`.

Alternatively you can install packages using the `pipenv` command itself.
In order to do that you have to run `pipenv install <package-name>`.
For example let's install [requests](https://requests.readthedocs.io/en/master/) package.

```
$ pipenv install requests
Installing requests…
Adding requests to Pipfile's [packages]…
✔ Installation Succeeded
Pipfile.lock (db4242) out of date, updating to (fbd99e)…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Building requirements...
Resolving dependencies...
✔ Success!
Updated Pipfile.lock (fbd99e)!
Installing dependencies from Pipfile.lock (fbd99e)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

You can also install the packages for specific environment also.
For example, you will need [pytest](https://docs.pytest.org/en/latest/)
and [black](https://black.readthedocs.io/en/stable/) in the developement
environment. So in order to install `black` in dev envitonment. Also you can
specify the version of that package.

```
$ pipenv install --dev black=="20.8b0"
Installing black==20.8b0…
Adding black to Pipfile's [dev-packages]…
✔ Installation Succeeded
Pipfile.lock (fbd99e) out of date, updating to (a289be)…
Locking [dev-packages] dependencies…
Building requirements...
Resolving dependencies...
✔ Success!
Locking [packages] dependencies…
Building requirements...
Resolving dependencies...
✔ Success!
Updated Pipfile.lock (a289be)!
Installing dependencies from Pipfile.lock (a289be)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Now that you have installed `requests`, and `black` in the current environment,
`pipenv` has added those to your `Pipfile`.

If you caeck the contents of `Pipfile` it will be something like

```
$cat Pipfile
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]
black = "==20.8b0"

[packages]
requests = "*"

[requires]
python_version = "3.8"
```

### Using the virtual environment

Till now we have created a virtualenv and installed some packages.
Now let's use it. Let's write a simple python program for it.

```python
#!/usr/bin/env python

import requests
import sys

def make_request(url=None):
    if url:
        req = requests.get(url)
        if req:
            print(req.text)

if __name__ == "__main__":
    if len(sys.argv) >= 2:
        make_request(sys.argv[1])
```

To launch the virtual environment, run `pipenv shell`.

```
$ pipenv shell
Launching subshell in virtual environment…
. /home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2/bin/activate
(pipenv-dir) $
```

You can run this program from shell by using environment from the shell that
we launched using `pipenv shell`.

```
(pipenv-dir) $ python http-request.py http://cheat.sh/pipenv
# pipenv
# Simple and unified Python development workflow.
# Manages packages and the virtual environment for a project.
# More information: <https://pypi.org/project/pipenv>.

# Create a new project:
pipenv

# Create a new project using Python 3:
pipenv --three
......
```

You can also run it directly using `pipenv run` without activating the
shell.

```
$ pipenv run python http-request.py http://cheat.sh/pipenv
......
```

### Generating dependency list for the project

To Generate a `requirements.txt` (list of dependencies) for the project

```
pipenv lock --requirements
```

### Deactivating the virtual environment

To deactivate the virtual environment the command is `deactivate` or
you can just `exit` both of them work just fine.

```
(pipenv-dir) $ deactivate
$
```

### Removing the virtual environment.

Finally, if you want to delete this virtual environment, you can do it
with

```
$ pipenv --rm
Removing virtualenv (/home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2)…

```
