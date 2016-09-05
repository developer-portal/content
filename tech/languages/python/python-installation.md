# Python in Fedora

[Python](https://www.python.org/) is is a widely used interpreted, object-oriented, high-level programming language with dynamic semantics. It is simple and easy to learn.
Python 3 is already preinstalled on Fedora. Let's use it!

## Run Python

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

## bpython interpreter
bpython is a fancy interface to the Python interpreter available in Fedora. It highliths the syntax and autocompletes your code.

### Installation

Open the _Terminal_ (see above) and isntall _bpython_ for Python 3:

```bash
$ sudo dnf install python3-bpython
```

Now you can run _bpython_. For Python 3 version type `python3-bpython`. You should see something similar:

```python
bpython version 0.15 on top of Python 3.5.1 /usr/bin/python3
>>> 
```
Now you can start coding!

### What next?

 * [Python homepage](https://www.python.org/)
 * [Python 3 Documentation](https://docs.python.org/3/)
 * [bpython website](http://www.bpython-interpreter.org/)
