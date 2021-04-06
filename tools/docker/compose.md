---
title: Docker Compose
subsection: docker
order: 5
---

# Docker Compose

[Docker Compose](https://docs.docker.com/compose/) is a tool to orchestrate Docker containers using a simple YAML file which describes your whole setup.


## Installation

The package is named `docker-compose`, you can install it easily with:

```
$ sudo dnf install docker-compose
```


## Example usage

In this example we will go through a simple [Django](https://www.djangoproject.com/) & [PostgreSQL](http://www.postgresql.org/) development environment setup managed by `docker-compose`. We will mount the application sources inside a Docker container, which will allow us to interpret code as we change it. The application container will be linked with the database container so our Django application will be able to communicate with our PostgreSQL database.


### Prerequisites


#### Docker

This guide expects that you have Docker engine installed, configured and running (for more information see [the Fedora installation guide](/tools/docker/docker-installation.html)).


#### Images

We will use Fedora-based images from [fedora-dockerfiles](https://github.com/fedora-cloud/Fedora-Dockerfiles).

```
$ git clone https://github.com/fedora-cloud/Fedora-Dockerfiles.git
```

Let's start with Django.

```
$ sudo docker build --tag=fedora-django Fedora-Dockerfiles/Django
```

And now PostgreSQL (stock one is just fine):

```
$ sudo docker build --tag=fedora-postgresql Fedora-Dockerfiles/postgresql
```


### Guide

We will name our project `awesome_web`. So let's start by creating a directory for the project (in a directory where you store your projects):

```
$ cd ${MY_PROJECTS}
$ mkdir awesome_web
$ cd awesome_web
```

Whole database will live in subdirectory `db` (`postgres` user has to own it — docker still lacks user namespaces; `26` is UID of `postgres` user, see `/usr/share/doc/setup/uidgid`):

```
$ mkdir db
$ sudo chown 26:26 db
```

#### `docker-compose` configuration

First thing to do will be to create a YAML configuration file named `docker-compose.yml`. The file should live in the root of our project.

```
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

Take `fedora-django` image and use it for `web` container, map port `8000` from container to `8000` on host, mount directory `awesome_web` (that's where sources will be) to `/code` within container and link the `web` container to `db` container.

`db` container is even more simple. Mount `db` directory inside container so PostgreSQL can populate it. We also need to set some environment variables to create database with username/password access (do not forget to change those!).


#### Create Django project

Let's start new project with command `django-admin`:

```
$ sudo docker-compose run web django-admin startproject awesome_web .
```

Since the container runs as root by default, even our project will be created as root, let's fix it:

```
$ sudo chown -R $UID:$UID awesome_web
```

Since we use PostgreSQL, we need to change `DATABASES` variable in `settings.py`:

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


#### Time to populate database

Nowadays this is done by `manage.py migrate`. We need to run the database container first, then populate the database:

```
$ sudo docker-compose up -d db
$ sudo docker-compose run web python3 manage.py migrate
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
$ sudo docker exec -ti awesome_web_db_1 bash
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

This is how your directory layout should look:

```
├── awesome_web
│   ├── awesome_web
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── wsgi.py
│   └── manage.py
├── db
│   ├── base
│   ├── global
│   ├── pg_clog
│   ├── pg_dynshmem
│   ├── pg_hba.conf
│   ├── pg_ident.conf
│   ├── pg_log
│   ├── <...and more>
└── docker-compose.yml
```

### Troubleshooting

It may happen to you that something does not work and you will end up with error message like this:

```
Starting awesomeweb_db_1...
Cannot start container bg1f8cb2d227a6efa5e82d9669235430f63dadc76a5ddd4907248f1edc11490a:
    Cannot link to a non running container: /awesomeweb_db_1 AS /awesomeweb_web_run_2/awesomeweb_db_1
```

Best way to figure out what went wrong is to check logs:

```
$ sudo docker-compose logs
```

In thiscase , the `db` service was not running, so we can check logs of it exclusively:

```
$ sudo docker-compose logs db
```

### Time to spin the whole environment!

```
$ sudo docker-compose up
```

That's it! You have your development environment running in docker containers! You can check easily:

```
$ elinks -dump http://$(docker inspect -f '{% raw %}{{ .NetworkSettings.IPAddress }}{% endraw %}' awesomeweb_web_1):8000
```
