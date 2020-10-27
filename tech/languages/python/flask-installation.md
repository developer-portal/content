---
title: Flask
subsection: python
order: 5
---

# Flask

[Flask](http://flask.pocoo.org/) is a micro web framework for Python, based on the Werkzeug toolkit and Jinja2 template engine.

## Installation of Flask in a virtual environment

Fedora includes a `python3-flask` package that you can install and import.
However, unless you are developing or packaging an application for Fedora, it is more useful to install Flask as a third-party package inside a *virtual environment*.
This will keep your project separate from your system, giving you more freedom in choosing additional libraries and their versions, and easing collaboration with people who aren't using Fedora yet.

Let's create a new project and a virtual environment.
Open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click `Enter`).
Then, create a new folder `my_project`, open it, and create a virtual environment called `project_venv`.

```bash
$ mkdir my_project
$ cd my_project
$ python3 -m venv project_venv
```

To work in the virtual environment, you have to activate it.

```bash
$ source project_venv/bin/activate
```

In an active the virtual environment (with the name `(project_venv)` included in your command line prompt), you can install Flask [from PyPI](https://developer.fedoraproject.org/tech/languages/python/pypi-install.html).

```bash
(project_venv) $ python -m pip install flask
```
That is all, you have sucessfully installed Flask in the virtual environment!
Now you can start working on your project.

## First application

This is an example of how a minimal Flask application can look like.
Save the code as `hello.py`.

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello World!"
```

### Running

To run a Flask app in a development server, set an environment variable to tell Flask where the app is, and then run `flask`:

Assuming that you have some Flask application called `hello.py`, you can run it in your activated virtual environment (see above) like this.

```bash
(project_venv) $ export FLASK_APP=hello.py
(project_venv) $ python -m flask
 * Running on http://127.0.0.1:5000/
```

You should see that it is running on some address, in this case 127.0.0.1.
Open the address shown in a web browser to see your application.

And you're off!
See [Flask's website](https://flask.palletsprojects.com/) for complete documentation and deployment options.

When you finish your work, you can deactivate the virtual environment.

```bash
(project_venv) $ deactivate
$
```

### What next?

 * [Flask Documentation](http://flask.pocoo.org/docs/)
 * [Python Documentation: venv](https://docs.python.org/3/library/venv.html#module-venv)
