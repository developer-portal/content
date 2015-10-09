---
title: Docker Compose
page: docker
order: 5
---

# Docker Compose

[docker-compose](https://docs.docker.com/compose/) is a tool to orchestrate docker containers. No more 4 lines long `docker run` commands, just one YAML file which describes your whole setup.

In this example we'll go through a simple development environment setup:

* first step will be to start a [Django](https://www.djangoproject.com/) project
* we will bindmount sources inside a docker container (app will change as we code)
* our choice of database will be PostgreSQL (which we link to the container with sources)
* the whole development environment will be managed by docker-compose

We will name our project `awesome_web`. So let's start by creating directory for it:

```
$ mkdir awesome_web
$ cd awesome_web
```

Whole database will live in subdirectory `db` (postgres user has to own it -- docker still lacks user namespaces):

```
$ mkdir db
# chown 26:26 db
```

## Prerequisites

We'll use fedora-based images from [fedora-dockerfiles](https://github.com/fedora-cloud/Fedora-Dockerfiles).

```
$ git clone https://github.com/fedora-cloud/Fedora-Dockerfiles.git
```

Let's start with Django. Since we'll bindmount sources inside container, we won't use `Dockerfile` from `Fedora-Dockerfiles`, we'll improve it a bit instead:

```
FROM fedora
MAINTAINER http://fedoraproject.org/wiki/Cloud

RUN dnf -y update && dnf clean all
RUN dnf -y install python-pip python-django git sqlite python-psycopg2 && dnf clean all

# create directory /code and mount sources there
RUN mkdir /code
WORKDIR /code
VOLUME /code

EXPOSE 8000

CMD ./manage.py runserver 0.0.0.0:8000
```

```
$ cd Fedora-Dockerfiles/Django
$ docker build --tag=fedora-django .
$ cd ../..
```

And now PostgreSQL:

```
$ cd Fedora-Dockerfiles/postgresql
$ docker build --tag=fedora-postgresql .
```


## `docker-compose` configuration

```
$ cat docker-compose.yml
web:
  image: fedora-django
  ports:
   - "8000:8000"
  volumes:
   - ./awesome_web:/code
  links:
   - db
db:
  image: fedora-postgresql
  volumes:
   - ./db:/var/lib/pgsql/data
  environment:
   - POSTGRESQL_DATABASE=awesome_web
   - POSTGRESQL_USER=awesome_web_user
   - POSTGRESQL_PASSWORD=secret_password
```

Explanation:

Take `fedora-django` image and use it for `web` container, map port `8000` from container to `8000` on host, bindmount directory `awesome_web` (that's where sources will be) to `/code` within container and link the `web` container to `db` container.

`db` container is even more simple. Mount `db` directory inside container so PostgreSQL can populate it. We also need to set some environment variables to create database with username/password access (don't forget to change those!).


## Create Django project

Let's start new project with command `django-admin`:

```
$ docker-compose run web django-admin startproject awesome_web .
```

Since the container runs as root by default, even our project will be created as root, let's fix it:

```
$ sudo chown -R $UID:$UID awesome_web
```

Since we use PostgreSQL, we need change `DATABASE` variable in `settings.py`:
```
$ $EDITOR awesome_web/awesome_web/settings.py
...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'awesome_web',
        'USER': 'awesome_web_user',
        'PASSWORD': 'secret_password',
        'HOST': 'db',
        'PORT': 5432,
    }
}
...
```


## Time to populate database

Nowadays this is done by `manage.py migrate`. We need to run the database container first, then populate the database:

```
$ docker-compose up -d db
$ docker-compose run web python manage.py migrate
Operations to perform:
  Synchronize unmigrated apps: staticfiles, messages
  Apply all migrations: admin, contenttypes, auth, sessions
Synchronizing apps without migrations:
  Creating tables...
    Running deferred SQL...
  Installing custom SQL...
Running migrations:
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying sessions.0001_initial... OK
```

Is the database really populated?

```
$ docker exec -ti awesomeweb_db_1 bash
bash-4.3$ psql
psql (9.4.4)
Type "help" for help.


postgres=# \l
                                      List of databases
    Name     |      Owner       | Encoding |  Collate   |   Ctype    |   Access privileges
-------------+------------------+----------+------------+------------+-----------------------
 awesome_web | awesome_web_user | UTF8     | en_US.utf8 | en_US.utf8 |
 postgres    | postgres         | UTF8     | en_US.utf8 | en_US.utf8 |
 template0   | postgres         | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
             |                  |          |            |            | postgres=CTc/postgres
 template1   | postgres         | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
             |                  |          |            |            | postgres=CTc/postgres
(4 rows)

postgres=# \connect awesome_web
You are now connected to database "awesome_web" as user "postgres".
awesome_web=# \dt
                       List of relations
 Schema |            Name            | Type  |      Owner
--------+----------------------------+-------+------------------
 public | auth_group                 | table | awesome_web_user
 public | auth_group_permissions     | table | awesome_web_user
 public | auth_permission            | table | awesome_web_user
 public | auth_user                  | table | awesome_web_user
 public | auth_user_groups           | table | awesome_web_user
 public | auth_user_user_permissions | table | awesome_web_user
 public | django_admin_log           | table | awesome_web_user
 public | django_content_type        | table | awesome_web_user
 public | django_migrations          | table | awesome_web_user
 public | django_session             | table | awesome_web_user
(10 rows)
```


## Time to spin the whole environment!

```
$ docker-compose up
```

That's it! You have your development environment running in docker containers! You can check easily:

```
$ elinks -dump http://$(docker inspect -f '{% raw %}{{ .NetworkSettings.IPAddress }}{% endraw %}' awesomeweb_web_1):8000
```
