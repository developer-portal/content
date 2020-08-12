---
title: Gtk+
subsection: c
order: 7
---

# Gtk+

Gtk+ is a cross-platform GUI toolkit created for the development of the GIMP project. Offering a complete set of widgets, Gtk+ is suitable for projects ranging from small one-off tools to complete applications suites.

For C programming with Gtk+ you need to install the development version of the important GNOME libraries. Those contain the header files and additional linker information:

```
sudo dnf install gtk3-devel gstreamer1-devel clutter-devel webkit2gtk3-devel libgda-devel gobject-introspection-devel
```

In addition, you will want to install the documentation packages of this libraries so you can view them in the API browser (devhelp):

```
sudo dnf install devhelp gtk3-devel-docs gstreamer1-devel-docs clutter-doc
```

## Getting started

To begin our introduction to Gtk+, we will start with the simplest program possible. This program will simply create a gtk+ window with the title "Hello World".

```c
#include <gtk/gtk.h>

int 
main(int   argc,
     char *argv[])
{
  GtkWidget *window;
    
  gtk_init (&argc, &argv);
    
  window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
  gtk_window_set_title (GTK_WINDOW (window), "Hello World");
  gtk_widget_show  (window);
    
  gtk_main ();
    
  return 0;
}
```

You can compile the above program with gcc using:

```
gcc hello.c -o hello `pkg-config --cflags --libs gtk+-3.0`
```

In the program above we initially included gtk/gtk.h, which declares all the gtk+ objects used in the rest of the program:

```c
#include <gtk/gtk.h>
```

or

```c
#include <gtk-3.0/gtk/gtk.h>
```

After the declaration of the window object variable, we call the gtk_init method which initializes the library and its internal procedures.

```c
gtk_init (&argc, &argv);
```

The next line creates a GtkWindow object with the GTK_WINDOW_TOPLEVEL type. Nearly always, that's the type of the GtkWindow, but it could differ if you are implementing something else.

```c
window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
```

Below that, we set the title of the GtkWindow to a string of our choice:

```c
gtk_window_set_title (GTK_WINDOW (window), "Hello World");
```

After that, the gtk_widget_show() function lets Gtk+ know that we are done setting the attributes of this widget, and that it can display it.

```c
gtk_window_show (window);
```

Finally, the last line enters the Gtk+ main processing loop.

```c
gtk_main ();
```

## Learn more

- [GNOME Plataform Demos](https://developer.gnome.org/gnome-devel-demos/stable/c.html.en)
- [Gtk+ 3 Reference Manual](https://developer.gnome.org/gtk3/stable/)
- [Compiling Gtk+ Applications](https://developer.gnome.org/gtk3/stable/gtk-compiling.html)
