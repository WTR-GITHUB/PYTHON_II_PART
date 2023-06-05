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

The `RUN` instruction allows you to customize your `Docker` image by executing **commands within the image's environment during the build process**. Each `RUN` instruction creates a new layer in the image, allowing for incremental builds and caching of intermediate results.

It's important to note that each `RUN` instruction in a Dockerfile is** executed as a separate step** during the image build. **If you need to perform multiple commands that depend on each other, consider combining them using shell operators (&&, ||)** to minimize the number of layers in the resulting image.

Remember to keep the number of `RUN` instructions minimal and consider any cleanup steps required to reduce the image size and remove unnecessary artifacts.

By using the `RUN` instruction effectively, you can automate various tasks and configure the environment within the Docker image to meet the requirements of your application or service.


### CMD

The `CMD` instruction in a `Dockerfile` is used to provide the **default command or executable to be executed when a container is started **from the Docker image. It specifies the main process to be run within the container.

The CMD instruction has the following syntax:

```docker
CMD ["executable", "param1", "param2", ...]
```
There are two forms of the `CMD` instruction:

#### Exec form (preferred)

```docker
CMD ["executable", "param1", "param2", ...]
```

In the exec form, the command and its arguments are specified as an array of strings. The command is directly executed without being invoked by a shell.

Example:

```docker
CMD ["python", "app.py"]
```
This runs the `python app.py` command as the main process inside the container.

#### Shell form

```docker
CMD command param1 param2 ...
```
In the shell form, the command is specified as a string and is executed within a shell. It can include shell-specific features like variable substitution, piping, and I/O redirection.

Example:

```docker
CMD python app.py
```
This runs the same `python app.py` command within a shell as the main process inside the container.


The `CMD` instruction is optional in a `Dockerfile`, but if it is specified, only the **last CMD instruction in the Dockerfile will have an effect. Previous CMD instructions are ignored.**

The `CMD` instruction provides the default behavior for a container. However, you can override the command by passing **arguments to the docker run command at runtime.**

It's important to note that the `CMD` instruction is not executed **during the build process but rather when a container is created from the image**.

Some best practices for using the `CMD` instruction include:

- Using the `exec` form whenever possible for better performance and signal handling.
- Providing a meaningful default command that allows the container to run as a standalone application.
- Considering the use of environment variables within the CMD instruction to make the command more flexible.

By utilizing the `CMD` instruction effectively, you can define the main process or command to be executed automatically when running a container based on your Docker image.


### EXPOSE

The `EXPOSE` instruction in a `Dockerfile` is used to inform Docker that a container created from the image will listen on specific network ports at runtime. It serves as a documentation mechanism to indicate which ports should be published and made available for communication with other containers or the host machine.

The `EXPOSE` instruction has the following syntax:

```docker
EXPOSE <port> [<port>/<protocol>...]
```

Let's explore its key points:

- <port>: Specifies the port number that the container listens on for incoming connections. It can be a single port number or a range of ports.

- <protocol> (optional): Specifies the network protocol used for communication on the specified port. It can be one of `tcp`, `udp`, or `sctp`. If no 
  protocol is specified, `tcp` is assumed by default.

The `EXPOSE` instruction is not responsible for actually publishing the ports to the host machine or exposing them to the outside world. It serves as metadata that can be used by tools or developers to understand which ports are intended to be used by the container.

Here's an example of the EXPOSE instruction in a Dockerfile:

```docker
# Expose port 8080 for HTTP traffic
EXPOSE 8080
```
In this example, the `Dockerfile` specifies that the container created from the image will listen on port `8080`.

After building an image with the `EXPOSE` instruction, you can use the `-p` flag with the docker run command to map the exposed container port to a port on the host machine:

```shell
docker run -p <host-port>:<container-port> <image-name>
```
For example, if the `Docker` image exposes port `8080` and you want to map it to port `8000` on the host machine, you would run:

```shell
docker run -p 8000:8080 <image-name>
```
This maps the host port `8000` to the container port `8080`, allowing communication with the container's exposed service.

Keep in mind that the `EXPOSE` instruction is primarily a **documentation feature**. **It is not necessary for internal container communication, communication between containers on the same network, or communication with the host machine.**

By using the `EXPOSE` instruction effectively, you can provide visibility and documentation of the network ports your container expects to use, making it easier for others to understand how to interact with your containerized application.

## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***