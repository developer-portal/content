---
title: Python Django      
subsection: web-app
order: 3
---

# What's Django?

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. 
Django is one of the most popular Python Web Frameworks. It has very useful web page. Visit it by clicking on [this link](https://www.djangoproject.com/). 
Because you will need to work with Python packages, write this command to your command line.

```
$ sudo dnf install python3-pip
```

## Get started

### How to install virtualenv

It's recommended to keep your project inside virtual environment. But you can skip this step if you want. 
Enter this command to your command line for installation:

```
$ sudo dnf install python3-virtualenv
```


Get inside your working directory or create new where you want to store your virtual environment:

```
$ mkdir working-dir
$ cd working-dir
```

Now we will create virtual environment called venv inside this directory using following command:

```
$ virtualenv venv
```

When it's done, we will activate our virtualenv. Now we will use following commands:

```
$ cd venv
$ source bin/activate
```

When it's activated we will see indicator of same name as our virtualenv. 
Now we will check if we really have empty environment:

```
$ pip freeze
```

It will return nothing.

### How to install Django

Now if you installed `virtualenv` do not leave it, we will install Django now. If you installed `virtualenv` use this command 
inside your working directory with activated `virtualenv`:

```
$ pip3 install django
```

If you are following a book or a tutorial, you might want to specify the same exact version like this

```
$ pip3 install django==1.10
```


Of course you can use the version that is prepared by Fedora community by typing:

```
$ sudo dnf install python3-django
```

and when it's finished use following command to start your first project called mysite:

```
$ django-admin startproject mysite
```

Now if you will check your directory using ls you will see new directory called mysite. We 
will go inside that directory and we will run our project by following commands:

```
$ cd mysite/
$ python3 manage.py runserver
```

You will see message with information about your development server. When you insert URL into your browser, 
you will see welcome page (default URL for development server is http://127.0.0.1:8000/).
And you successfully started your first Django project.

### Switching Virtualenvs

You can use `virtualenvwrapper` after installing it with usual command

```
$ sudo dnf install python3-virtualenvwrapper
```

```
$ mkvirtualenv env1
$ mkvirtualenv env2
$ workon env1
$ workon env2
```

