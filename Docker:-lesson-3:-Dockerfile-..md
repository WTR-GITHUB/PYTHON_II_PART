## Introduction

`Dockerfile` is a text file that contains a set of instructions for building a Docker image. It serves as a blueprint or recipe that `Docker` uses to create containers. With `Dockerfile`, **you can define the environment, dependencies, and configuration of your application**.

### Main concept and features:

- Base Image: A `Dockerfile` usually starts with a base image, which serves as the starting point for building your application's container. The base 
  image typically contains a minimal operating system or a specific runtime environment.

- Instructions: `Dockerfile` consists of a series of instructions that define the steps required to build the image. Each instruction creates a new layer 
  in the image, which allows for efficient caching and incremental builds.

- Commands: `Dockerfile` instructions include various commands such as `FROM`, `RUN`, `COPY`, `ADD`, `EXPOSE`, `CMD`, and more. These commands enable you 
  to install dependencies, copy files, set environment variables, expose ports, and define the commands to run when the container starts.

- Layered Filesystem: `Docker` images are built using a layered filesystem. Each instruction in the `Dockerfile` adds a new layer on top of the previous 
  one. This layering mechanism enables `Docker` to reuse cached layers during builds, improving build speed and reducing image size.

- Build Process: To build an image from a `Dockerfile`, you use the docker `build` command, providing the path to the directory containing the 
  `Dockerfile`. **Docker reads the instructions from the** `Dockerfile` and executes them in order, creating the image layer by layer.

- `Dockerfile` Best Practices: Following best practices can help optimize your `Dockerfile`. Some common best practices include **keeping the number of **
   **layers minimal, leveraging caching, using specific versions for dependencies, and cleaning up unnecessary artifacts.**

`Dockerfile` is a powerful tool that allows you to define the entire configuration of your application in a declarative manner, making it easy to reproduce and distribute your application as a containerized environment.


## COMMANDS
We will discuss few, most used Dockerfile commands: 

### FROM 
The `FROM` instruction in a `Dockerfile` is used to specify the base image upon which your Docker image will be built. It is typically the first instruction in a Dockerfile.

The FROM instruction has the following syntax:

```docker
FROM <image>[:<tag>] [AS <alias>]
```

Let's break down each part:

 - <image>: Specifies the base image for your Docker image. It can be an official image from the Docker Hub registry or a custom image you or someone 
   else has built. Examples include ubuntu, nginx, python, etc.

 - :<tag> (optional): Represents a specific version or tag of the base image. Tags are used to differentiate between different versions of an image. If 
   no tag is specified, Docker will use the latest tag by default. For example, ubuntu:18.04, nginx:1.19, python:3.9, etc.

 - AS <alias> (optional): Assigns an alias or a name to the current build stage. This is useful when you have multiple build stages in a multi-stage 
   build scenario. The alias allows you to reference and copy files from that specific build stage later in the Dockerfile.

The `FROM` instruction is required in every `Dockerfile` and sets the foundation for your image. It pulls the specified base image (or uses a locally available one) and starts building subsequent layers on top of it.

Here are a few examples of FROM instructions:

```docker
# Using an official Python 3.9 image as the base
FROM python:3.9

# Using a specific version of Ubuntu as the base
FROM ubuntu:20.04

# Using a custom image with an alias for multi-stage builds
FROM my-custom-image:latest AS build-stage
```
The `FROM` instruction is crucial in determining the starting point of your Docker image and influences the environment and tools available within the subsequent layers of the image.

Remember to choose a base image that aligns with your application's requirements and dependencies, as it will provide the underlying runtime and libraries needed for your application to run properly.

## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***