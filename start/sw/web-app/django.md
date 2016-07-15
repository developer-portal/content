---
title: Python Django      
subsection: web-app
order: 3
---

# What's Django?

Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design. 
Django is one of the most popular Python Web Frameworks. It has very useful web page. Visit it by clicking on [this link](https://www.djangoproject.com/). 
Because you will need to work with Python packages, write this command to your command line.

For Python:

```
sudo dnf install python-pip
```

or Python 3:

```
sudo dnf install python3-pip
```

# Get started

## How to install virtualenv

It's recommanded to keep your project inside virtual enviroment. But you can skip this step if you want. 
Enter this command to your command line for installation:

```
sudo dnf install python-virtualenv
```

or installation for Python3:

```
sudo dnf install python3-virtualenv
```


Get inside your working directory or create new where you want to store your virtual enviroment:

```
mkdir working-dir
cd working-dir
```

Now we will create virtual enviroment called venv inside this directory using following command:

```
virtualenv venv
```

When it's done, we will activate our virtualenv. Now we will use following commands:

```
cd venv
source bin/activate
```

When it's activated we will see indicator of same name as our virtualenv. 
Now we will check if we really have empty enviroment:

```
pip freeze
```

It will return nothing.

## How to install Django

Now if you installed virtualenv do not leave it, we will install Django now. If you installed virtualenv use this command 
inside your working directory:

```
pip install django
```

If you did not use this command. 

For Python 2:

```
sudo dnf install python-django
```

or Python 3:

```
sudo dnf install python3-django
```

and when it's finished use following command to start your first project called mysite:

```
django-admin startproject mysite
```

Now if you will check your directory using ls you will see new directory called mysite. We 
will go inside that directory and we will run our project by following commands:

```
cd mysite/
python manage.py runserver
```

You will see message with information about your development server. When you insert URL into your browser, 
you will see welcome page (default URL for development server is http://127.0.0.1:8000/).
And you successfully started your first Django project.
