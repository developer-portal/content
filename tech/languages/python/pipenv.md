---
title: Pipenv
subsection: python
order: 11
---

# Pipenv

As the [official documentation of `pipenv`](https://pipenv.pypa.io/en/latest/) says.

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

Once it is done, you can use `pipenv` to create, manage and remove Python
environments with different Python versions.

Let's see what all operations `pipenv` provides.

## Usage

### Creating a virtual environment.

To create a new virtualenv with a `python3` interpreter:

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

This will create a file called `Pipfile` in your current directory.

You can get the project location using:

```
$ pipenv --where
/home/fedorauser/pipenv-dir
```

To get the virtualenv location for this project:

```
$ pipenv --venv
/home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2
```

To get the python interpreter location for this `virtualenv`:

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

Alternatively, you can install packages using the `pipenv` command itself.
In order to do that you can run `pipenv install <package-name>`.
For example let's install the [requests](https://requests.readthedocs.io/en/master/) package.

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

You can also install the packages for a specific environment.
For example, you might need [black](https://black.readthedocs.io/en/stable/)
of a specific version in your developement environment. To install it, run:

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

Now that you have installed `requests` and `black` in the current environment,
`pipenv` has added those to your `Pipfile`.

If you check the contents of `Pipfile`, it will be something like:

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

To launch a shell in the virtual environment, run `pipenv shell`:

```
$ pipenv shell
Launching subshell in virtual environment…
. /home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2/bin/activate
(pipenv-dir) $
```

You can run the program from this shell:

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
 . . .
```

You can also run it directly using `pipenv run` without activating the
shell:

```
$ pipenv run python http-request.py http://cheat.sh/pipenv
# pipenv
# Simple and unified Python development workflow.
# Manages packages and the virtual environment for a project.
# More information: <https://pypi.org/project/pipenv>.

# Create a new project:
pipenv

# Create a new project using Python 3:
pipenv --three
 . . .
```

### Generating dependency list for the project

To generate a `requirements.txt` file with a list of dependencies for the project, run:

```
pipenv lock --requirements
-i https://pypi.org/simple
certifi==2020.6.20
chardet==3.0.4
idna==2.10; python_version >= '2.7' and python_version not in '3.0, 3.1, 3.2, 3.3'
requests==2.24.0
urllib3==1.25.11; python_version >= '2.7' and python_version not in '3.0, 3.1, 3.2, 3.3, 3.4' and python_version < '4'
```

### Deactivating the virtual environment

The command to deactivate the virtual environment is `deactivate`. Or
you can just `exit`; both of these work just fine.

```
(pipenv-dir) $ deactivate
$
```

### Removing the virtual environment.

Finally, if you want to delete this virtual environment, you can do it
with:

```
$ pipenv --rm
Removing virtualenv (/home/fedorauser/.local/share/virtualenvs/pipenv-dir-O2-8SZy2)…

```
