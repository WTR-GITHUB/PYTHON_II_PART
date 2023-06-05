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

### WORKDIR
The `WORKDIR` instruction in a Dockerfile is used to set the working directory for any subsequent instructions in the Dockerfile. It allows you to define the directory from which relative paths are resolved when executing commands during the build process or running the container.

The WORKDIR instruction has the following syntax:

```docker
WORKDIR <directory>
```

Let's explore its key points:

 - <directory>: Specifies the directory path to set as the working directory. It can be an absolute path or a relative path to the current working 
   directory. If the directory does not exist, Docker will create it.

The `WORKDIR` instruction is typically used to provide a consistent and controlled environment for subsequent instructions. By setting the working directory, you can ensure that commands executed within the Dockerfile or in the container will have the correct context and can use relative paths relative to that directory.

Here are a few examples of `WORKDIR` instructions:

```docker
# Set the working directory to /app
WORKDIR /app

# Set the working directory to a relative path
WORKDIR relative/path/to/directory

# Set the working directory based on an environment variable
WORKDIR $MY_WORKDIR
```

### COPY
The `COPY` instruction in a `Dockerfile` is used to copy files or directories from the host machine (the build context) into the Docker image being built. It allows you to include files from the build context into the image, making them accessible during runtime.

The COPY instruction has the following syntax:

```docker
COPY <src> <dest>
```
Let's explore its key points:

- <src>: Specifies the source path of the file or directory on the host machine. It can be a relative or absolute path within the build context.

- <dest>: Specifies the destination path inside the Docker image. It can be a directory path or a file path. If the destination path does not exist, Docker will create it.

The `COPY` instruction is often used to add application code, configuration files, or other necessary files to the Docker image. By copying files into the image, you ensure they are available for use when running containers based on that image.

Here are a few examples of `COPY` instructions:

```docker
# Copy a single file from the build context to the image
COPY app.py /app/

# Copy a directory from the build context to the image
COPY src/ /app/src/

# Copy files from the build context to multiple destinations in the image
COPY file1.txt file2.txt /app/
```
The `COPY` instruction can also take advantage of **wildcard patterns** to copy multiple files matching a specific pattern:

```docker
COPY *.txt /app/
```

In the above example, all the files with the `.txt` extension in the build context will be copied to the `/app/ directory` inside the Docker image.

It's important to note that the `COPY` instruction **copies files and directories from the build context into the image during the build process**. It does not provide synchronization between the host machine and the running container.

By using the `COPY` instruction effectively, you can ensure that your Docker image contains all the necessary files and dependencies to run your application without relying on external resources.

**Remember to consider the size and contents of the files being copied, as it can impact the resulting image size and build performance.**

### RUN
The `RUN` instruction in a `Dockerfile` is used to execute commands during the image build process. It allows you to run **shell commands, install dependencies, set up your application, and perform other tasks** required to build the desired environment within the Docker image.

The RUN instruction has the following syntax:

```docker
RUN <command>
```

Let's explore its key points:

- <command>: Specifies the command(s) to be executed within the shell environment of the image. It can be a single command or multiple commands using 
  shell operators such as && or ||.

The `RUN` instruction is typically used for tasks such as installing software packages, running system updates, setting up dependencies, compiling code, and performing any necessary configuration steps required for your application to run correctly.

Here are a few examples of RUN instructions:

```docker
# Install dependencies using apt-get package manager
RUN apt-get update && apt-get install -y package1 package2

# Download and install a specific version of a software from a URL
RUN curl -o software.tar.gz https://example.com/software.tar.gz \
    && tar -xzf software.tar.gz \
    && rm software.tar.gz

# Compile and build the application
RUN make && make install

# Set an environment variable during build
RUN export MY_VAR=myvalue
```



## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***