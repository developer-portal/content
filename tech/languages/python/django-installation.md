---
title: Django
subsection: python
order: 4
---

# Django
[Django](https://www.djangoproject.com/) is an open source web application framework written in Python, it encourages rapid development and clean, pragmatic design.

## How to install Django in a virtual environment

Fedora includes a `python3-django` package that you can install and import.
However, unless you are developing or packaging an application for Fedora, it is more useful to install Django as a third-party package inside a *virtual environment*.
This will keep your project separate from your system, giving you more freedom in choosing additional libraries and their versions, and easing collaboration with people who aren't using Fedora yet.

Let's create a new project and a virtual environment.
Open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click `Enter`).
Then, create a new folder `my_project`, open it, and create a virtual environment called `project_venv`.

```bash
$ mkdir my_project
$ cd my_project
$ python3 -m venv project_venv
```

To work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

In an active the virtual environment (with the name `(project_venv)` included in your command line prompt), you can install Django [from PyPI](https://developer.fedoraproject.org/tech/languages/python/pypi-install.html).

```bash
(project_venv) $ python -m pip install django
```

That is all, you have sucessfully installed Django in the virtual environment!
Now you can start working on your project.


## First project

This is a short tutorial how to create your first Django project. You can find a detailed tutorial in [Django Documentation](https://docs.djangoproject.com/en/1.10/intro/tutorial01/).

If you haven't already, activate your virtual environment (see above).
Then, to start, initialize your project files structure.
Replace `mysite` with the name of your project.

```bash
(project_venv) $ django-admin startproject mysite
```

Enter your new directory which was automatically created.

```bash
(project_venv) $ cd mysite
```

And run the server.

```bash
(project_venv) $ python manage.py runserver
```

Now that the server’s running, visit http://127.0.0.1:8000/ with your Web browser. You will see a “Welcome to Django” page, in pleasant, light-blue pastel. It worked!


When you finish your work, you can deactivate the virtual environment.

```bash
(project_venv) $ deactivate
$
```

### What next?

 * [Django Documentation](https://docs.djangoproject.com/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
