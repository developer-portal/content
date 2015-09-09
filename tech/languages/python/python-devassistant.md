---
title: Python assistants for DevAssistant
page: python
order: 6
---

# Python assistants

DevAssistant provides several assistants for Python. If you run `da` command from the command line then projects are created in the current working directory.
In case that you run `da-gui` then projects are created in directories which you specify.

## Assistant for library

In order to create a basic template library, run:

```
$ da crt python lib -n <library_name>
```

## Assistant for Django

In order to create a web template application with Django, run:

```
$ da crt python django -n <app_name>
```

## Assistant for Flask

In order to create a web template application with Flask, run:

```
$ da crt python flask -n <app_name>
```

## Assistant for GTK+ 3

In order to create a basic GTK+3 application based on Python GTK, run:

```
$ da crt python gtk3 -n <app_name>
```
