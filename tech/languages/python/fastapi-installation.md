---
title: FastApi
subsection: python
order: 5
---

# FastApi

[FastApi](https://fastapi.tiangolo.com/) is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

## Installation of FastApi in a virtual environment

Fedora includes a `python3-fastapi` package that you can install and import.
However, unless you are developing or packaging an application for Fedora, it is more useful to install FastAPI as a third-party package inside a *virtual environment*.
This will keep your project separate from your system, giving you more freedom in choosing additional libraries and their versions, and easing collaboration with people who aren't using Fedora yet.

Let's create a new project a virtual environment.
Open the terminal. Then, create a new folder 'my_project', enter it, and create a virtual environment called 'project_env'.

```bash
$ mkdir my_project && cd my_project
$ virtualenv project_env
```
To work in the virtual environment, you have to activate it.

```bash
$ source project-env/bin/activate
```

Now that we have an active virtual environment (this can be identified by having the `(project_env)` in the command line prompt), install FastApi and a server using `pip`.

```bash
(project_env) $ pip install fastapi uvicorn[standard]
```
That is all, you have sucessfully installed FastApi in the virtual environment!
Now you can start working on your project.

## First Application

The following is an example of an application using FastApi.
Create a file named 'main.py'.

```python
from typing import Optional

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
def read_item(item_id: int, q: Optional[str] = None):
    return {"item_id": item_id, "q": q}
```
### Running

To run a FastApi app on a development server, go to that directory in the terminal and run:

```console
$ uvicorn main:app --reload
```
This will start the server listening on `127.0.0.1:8000`.

Then open the terminal and run this command to get the response.
```console
$ curl -X 'GET' \
  'http://127.0.0.1:8000/' \
  -H 'accept: application/json'
```

The response looks like this:
```
{"Hello":"World"}
```

See [FastApi Website](https://fastapi.tiangolo.com/) for complete documentation & deployment options.

When you finish your work, you can deactivate the virtual environemnt.

```bash
(project_env) $ deactivate
```

### What's next?

* [FastApi](https://fastapi.tiangolo.com/)
