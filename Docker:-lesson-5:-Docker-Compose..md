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



## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***