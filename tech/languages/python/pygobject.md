---
title: PyGObject
subsection: python
order: 8
---

# PyGObject (PyGI)

PyGObject, also known as PyGI, is a Python extension module that gives clean and consistent access to the entire GNOME software platform through the use of GObject Introspection.

PyGObject provides full support of GObject Introspection and all of its features (callbacks, GVariant support, closures, sub-classing, etc.).

To install PyGObject on Fedora, run:

```
$ sudo dnf install python3-gobject
```

## Getting started

### Writing your first Gtk+ application

```
import gi
gi.require_version('Gtk', '3.0')
from gi.repository import Gtk
```

In the beginning, we have to import the Gtk module to be able to access GTK+’s classes and functions. Since a user’s system can have multiple versions of GTK+ installed at the same, we want to make sure that we when we import Gtk that it refers to GTK+ 3 and not any other version of the library, which is the purpose of statement gi.require_version('Gtk', '3.0').

```
win = Gtk.Window()
```

The line above creates an empty window.

```
win.connect("delete-event", Gtk.main_quit)
```

After creating the window, we connect its delete event to ensure that the application is terminated if we click on the x button to close the window.

```
win.set_title("Hello World")
```

In the line above we set the window title to be a string of our choice, in this case: "Hello World".

```
win.show_all()
```

The show_all method called above displays the window and the widgets contained on it.
```
Gtk.main()
```

Finally, we start the GTK+ processing loop which we quit when the window is closed.

To run the program, save the file as `hello.py`, then open a terminal, change to the directory of the file, and enter:

```
$ python hello.py
```

The complete program can be seen below:


```python
import gi
gi.require_version('Gtk', '3.0')
from gi.repository import Gtk

win = Gtk.Window()
win.connect("delete-event", Gtk.main_quit)
win.set_title("Hello World")
win.show_all()

Gtk.main()

```

## What next?

- [Python GObject Introspection API Reference](http://lazka.github.io/pgi-docs/)
- [The Python GTK+ 3 Tutorial](http://python-gtk-3-tutorial.readthedocs.org/en/latest/)
- [GNOME Platform Demos in Python](https://developer.gnome.org/gnome-devel-demos/stable/py.html.en)
