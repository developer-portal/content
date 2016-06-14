---
title: Flask
subsection: python
order: 4
---

# Flask

Flask is a web microframework for Python -- simpler than [Django](/tech/languages/python/django-installation.html), yet just as capable. Check out [the documentation](http://flask.pocoo.org/docs/0.10/) if you want to learn more.


## Installation

To install Flask on Fedora:

For Python 2:

```
$ sudo dnf install python-flask
```

For Python 3:

```
$ sudo dnf install python3-flask
```

## First application

This is an example of how a minimal Flask application can look like.

{% highlight python %}
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
{% endhighlight %}


## Running

Assuming that you have some Flask application called `foo.py`, you can run it like this.

```
$ python foo.py
 * Running on http://127.0.0.1:5000/
```

You should see that it is running on some address, in this case 127.0.0.1. Default port for Flask applications is 5000. Open it in web browser to see your application.
