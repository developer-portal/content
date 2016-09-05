---
title: Flask
subsection: python
order: 4
---

# Flask

[Flask](http://flask.pocoo.org/) is a micro web framework for Python, based on the Werkzeug toolkit and Jinja2 template engine.

## Install Flask
Let's install Flask. At first open the _Terminal_ (press `Alt` + `F1`, type _Terminal_ and click on the black squere icon or just press `Enter`). Second, type this command:

```bash
$ sudo dnf install python3-flask
```

That is all, you have sucessfully installed Flask!

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

Assuming that you have some Flask application called `foo.py`, you can run it like this.

```bash
$ python3 foo.py
 * Running on http://127.0.0.1:5000/
```

You should see that it is running on some address, in this case 127.0.0.1. Default port for Flask applications is 5000. Open it in web browser to see your application.

## DevAssistant for Flask
Fedora offers a tool called DevAssistant which will help you with creating of the new project. You can you GUI application or the command line interface.

### DevAssistant GUI
Open the _Software_ tool and search for _DevAssistant_, install it. Run a _DevAssistant_. In the _Create Project_ menu pick _Python_ and than Flask. Continue with _DevAssistant setup wizard_.

### DevAssistant in the command line
At first, you must install the _DevAssistant_:
```bash
$ sudo dnf install devassistant
```

Next, install an _Assistant_ for Python:
```bash
$ da pkg install python
```

And finally create a new Flask project:

```bash
$ da create python flask -n project_name
```

### What next?

 * [Flask Documentation](http://flask.pocoo.org/docs/)
 * [DevAssistant Documentation](http://doc.devassistant.org/en/latest/user_documentation.html)
