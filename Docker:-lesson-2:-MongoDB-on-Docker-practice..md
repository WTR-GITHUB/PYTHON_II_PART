## Introduction

`MongoDB` can be run in a Docker container. There is an [official image](https://hub.docker.com/_/mongo) available on `Docker Hub` containing the MongoDB community edition, used in development environments. For production, you may custom-build a container with MongoDB’s enterprise version.

If you want to use your `MongoDB` database across several machines, using Docker containers for hosting MongoDB is a great approach – you can easily create new isolated instances. Furthermore, during development, it is easier to start a Docker instance than manually configure a server.

## Installation 

### Linux 

For Linux users, please go there: https://docs.docker.com/engine/install/ubuntu/

### Windows

For Windows users , please go there: https://docs.docker.com/desktop/install/windows-install/

### macOS

For macOS users , please go there: https://docs.docker.com/desktop/install/mac-install/

## Images

**Docker images** are a key concept in Docker, a popular platform for building, packaging, and deploying software applications. In simple terms, a Docker image is a lightweight, standalone, and executable package that contains all the necessary files, dependencies, and configurations required to run an application.

An image is created by specifying a series of instructions in a Dockerfile, which is a text file that contains the commands to build the image. These instructions typically include things like installing packages, copying files, and setting environment variables. Once the Dockerfile is built, the resulting image can be stored in a Docker registry or repository, such as Docker Hub or a private registry.

Images are designed to be portable and can be run on any host that supports Docker. When an image is executed, it creates a container, which is a lightweight, isolated runtime environment that runs the application. Multiple containers can be created from the same image, each with its own isolated runtime environment, allowing applications to be easily scaled and managed.

Overall, Docker images provide a simple and efficient way to package, distribute, and run applications, making it easier to develop, deploy, and manage software in a variety of environments.

### Working with images

Open up a terminal or command prompt and type in the following command to download a Docker image:

```
docker pull <image_name>

```

Replace <image_name> with the name of the image you want to download. For example, if you want to download the official `nginx` image, you would type:

```
docker pull python

```

Once the image is downloaded, you can start a container from it by typing:

```
docker run <image_name>

```

```
docker run ngix

```
You can also specify additional options when starting a container. For example, to start a container and **map a local port to the container's port 80** (so you can access the web server from your browser as for example), you would type:

```
docker run -p 8080:80 nginx

```

To list all images you have already downloaded: 

```
docker image list
```
To delete the image from the list: 

```
docker image rm <image_id>
```
or 


```
docker rmi <image_id>
```

##Containers

As already mentioned, a `container` is a lightweight, standalone, and executable package that includes everything needed to run an application, such as code, runtime, libraries, and system tools. Containers allow you to run your applications in an isolated environment that has all the necessary dependencies and configurations, without affecting the host system.

### Working with containers

Run a Docker container:

```
docker run <image_name>

```

List all running containers:

```
docker ps
```

Stop a running container:

```
docker stop <container_id>
```

Remove a stopped container:

```
docker rm <container_id>
```

View logs from a container:

```
docker logs <container_id>
```

Start a stopped container:

```
docker start <container_id>
```

## Exercises: 

* **Task Nr.1**:
 Go and find the latest mongo db image and install/ run it.

* **Task Nr.2**:
 Install several other images, and try to use all the commands from the examples.


 [Hint](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4) 

## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***