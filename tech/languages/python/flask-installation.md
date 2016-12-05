---
title: Flask
subsection: python
order: 4
---

# Flask

[Flask](http://flask.pocoo.org/) is a micro web framework for Python, based on the Werkzeug toolkit and Jinja2 template engine.

## Installation of Flask in the virtualenv

It’s recommended to keep your project inside virtual environment. Let's install and create a new virtual environment for your project.

At first open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black squere icon or just press `Enter`). Second, create a new folder `my_project` open it.

```bash
$ mkdir my_project
$ cd my_project
```

Let's create a virtual environment called `project_venv` which will contain Python and pip which you can use to install Flask.

```bash
$ pyvenv project_venv
```

If you want to work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

Running the virtual environment, you can install Flask.

```bash
(project_venv) $ pip install flask
```
That is all, you have sucessfully installed Flask in the virtual environment! Now you can start working on your project.

## First application

This is an example of how a minimal Flask application can look like.

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```

### Running

Assuming that you have some Flask application called `foo.py`, you can run it in your activated virtual environment (see above) like this.

```bash
(project_venv) $ python3 foo.py
 * Running on http://127.0.0.1:5000/
```

You should see that it is running on some address, in this case 127.0.0.1. Default port for Flask applications is 5000. Open it in web browser to see your application.

When you finish your work, just deactivate the virtual environment.

```bash
(project_venv) $ deactivate
```

### What next?

 * [Flask Documentation](http://flask.pocoo.org/docs/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
