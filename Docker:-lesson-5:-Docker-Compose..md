## Introduction
`Docker Compose` is a tool that allows you to define and run multi-container Docker applications. It provides a way to manage and orchestrate multiple Docker containers as a single unit, making it easier to develop, deploy, and scale complex applications.

With `Docker Compose`, you can define your application's `services`, `networks`, and `volumes` in a `YAML` file called **docker-compose.yml**. Each service represents a separate container in your application, and you can specify various settings for each service such as the image to use, environment variables, exposed ports, and more.

Here's a brief overview of the key components and functionality of Docker Compose:

### Services
Services are the building blocks of your application. Each service is defined in the docker-compose.yml file and represents a **separate container**. You can specify various parameters for each service, such as the image to use, environment variables, volume mounts, and port mappings.

### Networks

Networks allow containers to communicate with each other. Docker Compose creates a default network for your application, but you can also define custom networks to isolate containers or provide specific communication patterns.

### Volumes 
Volumes provide persistent storage for your containers. With Docker Compose, you can define named volumes or mount host directories into containers. This allows you to store and share data between containers or persist data even if a container is stopped or removed.

### Environment variables
Docker Compose allows you to set environment variables for your services. You can define them directly in the docker-compose.yml file or in a separate .env file. Environment variables are useful for configuring your application or passing sensitive information securely.

## Example 

Now, let's take a look at a simple example to illustrate how `Docker Compose` works. Suppose you have a web application consisting of a frontend and a backend service. Here's what your docker-compose.yml file might look like:

Folder structure: 

```
project/
├── app/
│   └── app.py
├── docker-compose.yml
└── requirements.txt

```

Create a Flask Web Application. In the app/ directory, create a file named app.py with the following content:

```python
from flask import Flask
from pymongo import MongoClient

app = Flask(__name__)

# Connect to MongoDB
client = MongoClient("mongodb://mongo:27017/")
db = client.mydatabase
collection = db.mycollection


@app.route('/')
def index():
    # Insert a document into MongoDB
    collection.insert_one({"message": "Hello from MongoDB!"})

    # Retrieve documents from MongoDB
    documents = collection.find()

    message = ""
    for doc in documents:
        message += doc["message"] + "<br>"

    return f"<h1>{message}</h1>"


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)

```

Create a Docker Compose File. In the project's root directory, create a `docker-compose.yml` file with the following content:

```yaml
version: "3"
services:
  web:
    build: ./app
    ports:
      - 5000:5000
    depends_on:
      - mongo
  mongo:
    image: mongo:latest
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:

```

In this example, we define two services: web and mongo. The web service builds an image from the ./app directory (where our Flask application resides). It maps port 5000 of the container to port 5000 of the host machine and specifies a dependency on the mongo service. The mongo service uses the mongo image and creates a volume named mongo-data to persist the MongoDB data.


Create a Requirements File. In the project's root directory, create a requirements.txt file with the following content:

```
Flask==2.0.1
pymongo==3.12.0
```
This file specifies the Python packages required for our Flask application and the MongoDB driver.

Build and Run the Application. Open a terminal, navigate to the project's root directory, and run the following command:

```docker
docker-compose up --build

```
Docker Compose will build the images, create the containers, and wire them together based on the defined configuration. It will also download the necessary Docker images if they are not already present.

Once the application is running, you can access it by opening a web browser and navigating to http://localhost:5000. You should see a page displaying the message "Hello from MongoDB!".

The Flask application communicates with the MongoDB database by using the service name mongo as the hostname. This works because Docker Compose creates a default network for the services defined in the docker-compose.yml file, and each service is reachable by its service name as a hostname.

## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***