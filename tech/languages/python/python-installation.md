---
title: Python
subsection: python
section: tech-languages
order: 1
version: 2.7.12
description: General-purpose, high-level programming language supporting multiple programming paradigms.
---

# Python in Fedora

[Python](https://www.python.org/) is is a widely used interpreted, object-oriented, high-level programming language with dynamic semantics. It is simple and easy to learn.
Python 3 is already preinstalled on Fedora. Let's use it!

## Running Python

1. Open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black squere icon or just press `Enter`).
2. To run Python 3 type `python3`. You should see something like this:

```python
Python 3.5.1 (default, Aug  9 2016, 15:35:51) 
[GCC 6.1.1 20160621 (Red Hat 6.1.1-3)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Now you can start to write in Python! Let's print _Hallo World_!

```python
print('Hallo World!')
```

If you want to **exit** Python, press `Ctrl` + `D`.

To run a program written in Python type `python3`, the path and the name of the program. Like this:

```bash
$ python3 example.py
```

## Using virtualenv
When you work at some project it is good to keep it inside a virtual environment. It will keep the dependencies you need at one place and you no dot have to worry about different projects which needs different version of the same module.

Let's create a virtual environment called `project_venv` which will contain Python and pip which you can use to install project's dependencies.

```bash
$ pyvenv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

When the virtual environment is activated (you can see it's name in brackets at the beginning of your prompt), you can install modules via `pip install`.

```bash
(project_venv) $ pip install name_of_module
```
That is all, you have sucessfully created your own virtual environment. Now you can run Python (see above) and start working on your project. 

When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

### What next?

 * [Python homepage](https://www.python.org/)
 * [Python 3 Documentation](https://docs.python.org/3/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
