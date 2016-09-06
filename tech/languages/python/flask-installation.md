---
title: Flask
subsection: python
order: 4
---

# Flask

[Flask](http://flask.pocoo.org/) is a micro web framework for Python, based on the Werkzeug toolkit and Jinja2 template engine.

## Installation
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

### What next?

 * [Flask Documentation](http://flask.pocoo.org/docs/)
