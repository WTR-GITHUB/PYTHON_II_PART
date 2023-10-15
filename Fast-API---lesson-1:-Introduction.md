## Introduction
`FastAPI` is a modern and high-performance web framework for building APIs with Python. It has gained significant popularity in the world of web development due to its speed, simplicity, and robust capabilities. Unlike traditional web frameworks, FastAPI leverages the latest advancements in Python type hints and asynchronous programming, making it an ideal choice for developing fast, efficient, and scalable web applications and APIs.

At its core, `FastAPI` is designed to help developers create web services quickly and easily while maintaining a high degree of flexibility and precision. It combines the power of automatic data validation and serialization with intuitive and straightforward syntax. One of its standout features is its ability to automatically generate detailed API documentation, making it a fantastic choice for teams looking to improve collaboration and streamline the development process.

`FastAPI` seamlessly integrates with popular data science and machine learning libraries, making it a favorite among data professionals for building robust and performant data-driven APIs. It also fully supports asynchronous programming, which is particularly valuable for handling concurrent requests and I/O-bound operations.

## Seting up
 
### Install FastAPI and Uvicorn:
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

## Exercises: 

* Task Nr.1 :
  Create a class that would implement basic CRUD operations to manage book data in the library.
 
  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-6) 

* Task Nr.2:  
  Create a command-line task manager application using Python and MongoDB. The application should allow users to perform basic CRUD operations (Create, 
  Read, Update, Delete) on tasks stored in a MongoDB database. Users should be able to add new tasks, view all tasks, update task status, and delete 
  tasks.
 
  Requirements:

  - The application should utilize the PyMongo library for interacting with the MongoDB database.
  - Users should be able to perform the following actions:
        - Add a new task with a title and description.
        - View all tasks with their details.
        - Update the status of a task (e.g., mark as completed or in progress).
        - Delete a task.
   - Implement error handling and validation for user inputs.
   - Use appropriate functions and modular code structure for better code organization.
   - Include a README file with clear instructions on how to set up and run the application.

 

## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***