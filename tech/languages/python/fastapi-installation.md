---
title: FastApi
subsection: python
order: 5
---

# FastApi

[FastApi](https://fastapi.tiangolo.com/) is a modern, fast (high-performance), web framework for building APIs with Python 3.6+ based on standard Python type hints.

## Installation of FastApi in a virtual environment

It is always useful to install FastApi as a third-party package inside a *virtual environemnt*.
This will keep your project separate from your system, giving you more freedom in choosing additional libraries & their versions. And it's easy collaborating with
a different operating system.

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
(project_venv) $ pip install fastapi uvicorn[standard]
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
This will start the server in localhost and you're off.

See [FastApi Website](https://fastapi.tiangolo.com/) for complete documentation & deployment options.

When you finish your work, you can deactivate the virtual environemnt.

```bash
(project_env) $ deactivate
```

### What's next?

* [FastApi] (https://fastapi.tiangolo.com/)
