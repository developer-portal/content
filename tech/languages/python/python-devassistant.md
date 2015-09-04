---
title: DevAssistant
page: python
order: 6
---

# Python assistants

DevAssistant provides several assistants for python.
If you run `da` command from command line then projects are created in current working directory.
In case that you run `da-gui` then projects are created in directories which you specify.

## Assistant for library

In order to create a basic template library, run:

```
$ da crt python lib -n <library_name>
```

## Assistant for Django

In order to create a web template application with Django, run:

```
$ da crt python django -n <django_name>
```

## Assistant for Flask

In order to create a web template application with flask, run:

```
$ da crt python flask -n <flask_name>
```

## Assistant for GTK+ 3

In order to create a basic GTK+3 application based on Python GTK, run:

```
$ da crt python gtk3 -n <gtk3_name>
```