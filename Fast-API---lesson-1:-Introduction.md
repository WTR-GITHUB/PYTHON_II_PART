## Introduction
`FastAPI` is a modern and high-performance web framework for building APIs with Python. It has gained significant popularity in the world of web development due to its speed, simplicity, and robust capabilities. Unlike traditional web frameworks, FastAPI leverages the latest advancements in Python type hints and asynchronous programming, making it an ideal choice for developing fast, efficient, and scalable web applications and APIs.

At its core, `FastAPI` is designed to help developers create web services quickly and easily while maintaining a high degree of flexibility and precision. It combines the power of automatic data validation and serialization with intuitive and straightforward syntax. One of its standout features is its ability to automatically generate detailed API documentation, making it a fantastic choice for teams looking to improve collaboration and streamline the development process.

`FastAPI` seamlessly integrates with popular data science and machine learning libraries, making it a favorite among data professionals for building robust and performant data-driven APIs. It also fully supports asynchronous programming, which is particularly valuable for handling concurrent requests and I/O-bound operations.

## Setting up
 
### Install `FastAPI` and `Uvicorn`:
First, make sure you have Python installed. You can install FastAPI and Uvicorn using `pip`:

```bash
pip install fastapi uvicorn

```

### Create a FastAPI App:
Create a Python file, let's call it `main.py`, to define your `FastAPI` application. In this example, we'll create a basic API that returns a `Hello, World!` message.

```python
from fastapi import FastAPI

# Create an instance of the FastAPI class
app = FastAPI()

```

### Define an API Endpoint:

Define a route using the @app.get decorator, specifying the HTTP method and the URL path. In this case, we'll define a root endpoint.

```python
@app.get("/")
def read_root():
    return {"message": "Hello, World!"}

```
### Run the FastAPI App:
Use Uvicorn to run your FastAPI app. Uvicorn is an ASGI server that can serve your FastAPI application.

```bash
curl http://localhost:8000

```
- `main` is the name of your Python file (main.py), and app is the instance of the `FastAPI` app you created.
- The `--reload` flag automatically reloads your app when you make code changes during development

### Access Your API:
Your `FastAPI` app is now running locally. You can access it in your web browser or via a tool like `curl` or `httpie`. Open a web browser and navigate to `http://localhost:8000`, or use curl to make a GET request:

```bash
curl http://localhost:8000
```
You should receive a JSON response with the "Hello, World!" message.

Let see again what we've done so far: 

- We start by importing the FastAPI class from the fastapi package.
- We create an instance of the FastAPI class, which represents our web application.
- We define a route using the `@app.get` decorator. In this case, it's a GET request to the root path ("/"). The function read_root() is the endpoint    
  handle that will be executed when someone accesses the root URL.
- Inside the read_root() function, we return a Python dictionary. `FastAPI` automatically serializes this dictionary into JSON and sends it as the response   
  to the client.
- We use `Uvicorn` to run our `FastAPI` app, specifying the Python file (main.py) and the `FastAPI` instance (app) as arguments.
- The app is hosted at http://localhost:8000 by default.

This is a basic setup to get you started with FastAPI. You can build more complex APIs by adding more routes and defining data models for request and response objects. FastAPI's automatic data validation, serialization, and API documentation generation features make it a powerful choice for developing APIs with Python.

## Operations 

`FastAPI` makes it easy to create APIs that support various HTTP methods like `GET`, `PUT`, `POST`, and `DELETE`. In this introduction, we'll explore these HTTP methods and provide examples of how to use them. HTTP Methods in FastAPI:

`FastAPI` leverages Python type hints to define routes and their respective HTTP methods, making it a breeze to work with HTTP verbs. Here's an overview of each of these methods:

- GET - Used for retrieving data from the server.
- POST - Used for creating new data on the server.
- PUT - Used for updating existing data on the server.
- DELETE - Used for deleting data on the server.

Examples of Using HTTP Methods in `FastAPI`:

### GET Method:

The `GET` method is used to **retrieve** data. In FastAPI, you can define a route that handles `GET` requests as follows:

```python
from fastapi import FastAPI
app = FastAPI()

# Define a GET route
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```

In this example, when you make a `GET` request to `/items/{item_id}`, it returns a `JSON` response with the `item_id` parameter.

### POST Method:

The `POST` method is used to **create** new data. Here's an example of handling `POST` requests:

```python
from fastapi import FastAPI
app = FastAPI()

# Define a POST route
@app.post("/items/")
def create_item(item: dict):
    # In a real application, you would typically save the item to a database.
    return item
```

In this example, when you make a POST request to /items/ with a JSON payload, it returns the same data you sent in the request.

### PUT Method:

The `PUT` method is used to **update** existing data. Here's an example:

```python
from fastapi import FastAPI
app = FastAPI()

# Define a PUT route
@app.put("/items/{item_id}")
def update_item(item_id: int, updated_item: dict):
    # In a real application, you would typically update the item with the given item_id in a database.
    return {"item_id": item_id, "updated_item": updated_item}
```

When you make a PUT request to `/items/{item_id}` with a `JSON` payload, it updates the item associated with the specified `item_id`.

### DELETE Method:

The DELETE method is used to **delete** data. Here's an example:

```python
from fastapi import FastAPI, HTTPException
app = FastAPI()

# Define a DELETE route
@app.delete("/items/{item_id}")
def delete_item(item_id: int):
    # In a real application, you would typically delete the item with the given item_id from a database.
    return {"message": f"Item {item_id} has been deleted"}
```

A `DELETE` request to `/items/{item_id}` deletes the item associated with the specified `item_id`.

In these examples, we've shown how to use `FastAPI` to handle common HTTP methods. FastAPI's automatic request and response handling, as well as its built-in data validation and documentation generation, make it a powerful tool for building web APIs that are not only easy to develop but also well-documented and efficient.

## Exercises: 

* Task Nr.1 :
  Create a simple API client which by default greets you and returns current time in `YYYY:MM:DD h:m:s` 

* Task Nr.2:  
  
 

## 🌐  Extra reading (or watching 📺 ):

* [Full FastAPI intro course - Youtube](https://www.youtube.com/watch?v=tLKKmouUams)
* [Official documentation](https://fastapi.tiangolo.com/)
***