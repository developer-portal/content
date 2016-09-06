---
title: Django
subsection: python
order: 3
---

# Django
[Django](https://www.djangoproject.com/) is an open source web application framework written in Python, it encourages rapid development and clean, pragmatic design.

## Installation
Let's install Django. At first open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black squere icon or just press `Enter`). Second, type this command,:

```bash
$ sudo dnf install python3-django
```

That is all, you have sucessfully installed Django!

## First project

This is a short tutorial, how to create your first Django project. You can find a detailed tutorial in [Django Documentation](https://docs.djangoproject.com/en/1.10/intro/tutorial01/).

Let's initialize your project files structure. Replace `mysite` with the name of your project.
```bash
$ django-admin startproject mysite
```

Enter your new directory which was automatically created.
```bash
$ cd mysite
```

And run the server.
```bash
$ python3 manage.py runserver
```

Now that the server’s running, visit http://127.0.0.1:8000/ with your Web browser. You willl see a “Welcome to Django” page, in pleasant, light-blue pastel. It worked!

### What next?

 * [Django Documentation](https://docs.djangoproject.com/)
 