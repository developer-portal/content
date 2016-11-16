---
title: Django
subsection: python
order: 3
---

# Django
[Django](https://www.djangoproject.com/) is an open source web application framework written in Python, it encourages rapid development and clean, pragmatic design.

## How to install Django in the virtualenv
It’s recommended to keep your project inside virtual environment. Let's create a new virtual environment for your project.

At first open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black squere icon or just press `Enter`). Second, create a new folder `my_project` open it.

```bash
$ mkdir my_project
$ cd my_project
```

Let's create a virtual environment called `project_venv` which will contain Python and pip which you can use to install Django.

```bash
$ pyvenv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

Running the virtual environment, you can install Django.

```bash
(project_venv) $ pip install django
```
That is all, you have sucessfully installed Django in the virtual environment! Now you can start working on your project.

## First project

This is a short tutorial, how to create your first Django project. You can find a detailed tutorial in [Django Documentation](https://docs.djangoproject.com/en/1.10/intro/tutorial01/).

Now it is a good time to activate your virtual environment (see above). Let's initialize your project files structure. Replace `mysite` with the name of your project.

```bash
(project_venv) $ django-admin startproject mysite
```

Enter your new directory which was automatically created.

```bash
(project_venv) $ cd mysite
```

And run the server.

```bash
(project_venv) $ python3 manage.py runserver
```

Now that the server’s running, visit http://127.0.0.1:8000/ with your Web browser. You will see a “Welcome to Django” page, in pleasant, light-blue pastel. It worked!


When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

### What next?

 * [Django Documentation](https://docs.djangoproject.com/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
