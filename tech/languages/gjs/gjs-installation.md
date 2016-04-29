---
title: Gjs
subsection: javascript
order: 0
---

# Gjs: Javascript Bindings for GNOME

Gjs is a Javascript binding for GNOME and can be used to interact with Gtk+. It is mainly based on the Spidermonkey Javascript engine and the GObject introspection framework.

To install Gjs on Fedora, run:

```
sudo dnf install gjs gjs-devel
```

## Getting started

### Writing your first Gtk+ application

Writing Gjs applications for the GNOME Desktop is very similiar to coding with traditional languages in the plataform such as Python.

Firstly, we need to import the desired libraries for our program:

```javascript
const Gtk = imports.gi.Gtk;
```

After that, we will initialize Gtk+.

```javascript
Gtk.init(null, 0);
```

To create our window, we need to create a GtkWindow object. Gjs allows the initialization of object attributes to be made when the object is constructed.

```javascript
let window = new Gtk.Window({
    title: "Hello World"
});
```

In the lines below we are connecting the destroy event of the window to ensure that the application is terminated if we click on the x button to close the window.

```javascript
window.connect("destroy", function () {
  Gtk.main_quit();
});
```

After that, we need to display the window, by calling its show method:

```javascript
window.show();
```

Finally, we start the GTK+ processing loop which we quit when the window is closed.

```javascript
Gtk.main();
```

To run the program, open a terminal, change to the directory of the file, and enter:

```
gjs hello.gjs
```

The complete program can be seen below:

```javascript
const Gtk = imports.gi.Gtk;

Gtk.init(null, 0);

let window = new Gtk.Window({
    title: "Hello World"
});

window.connect("destroy", function () {
  Gtk.main_quit();
});
window.show();

Gtk.main();
```

## More information

- [Example demo applications](https://developer.gnome.org/gnome-devel-demos/stable/js.html)
- [API Documentation](https://people.gnome.org/~gcampagna/docs/)
