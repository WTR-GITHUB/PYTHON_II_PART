## Introduction

`MongoDB` can be run in a Docker container. There is an [official image](https://hub.docker.com/_/mongo) available on `Docker Hub` containing the MongoDB community edition, used in development environments. For production, you may custom-build a container with MongoDB’s enterprise version.

If you want to use your `MongoDB` database across several machines, using Docker containers for hosting MongoDB is a great approach – you can easily create new isolated instances. Furthermore, during development, it is easier to start a Docker instance than manually configure a server.

## Start image 

You can start a MongoDB server running the latest version of MongoDB using Docker with the following command:

```
docker run -d -p 27017:27017 --name test-mongo mongo:latest
```

This will pull the latest [official image](https://hub.docker.com/_/mongo/) from Docker Hub. Adding the -d flag will ensure that the Docker container runs as a background process, separate from the shell. The -p tag signifies the port that the container port is bound back to 27017. You can connect to MongoDB on localhost:27017.

To change the port number, you can change the -p flag argument to 8000:27017 to use localhost:8000. You can also use the --port flag to mention the post. Using the latest image helps you avoid version bumps. Execute this to run MongoDB on port 8000:

```
docker run -d --name test-mongo mongo:latest --port 8000
```
Or choose your own port:

```
docker run -d -p 27017:27017 --name example-mongo mongo:latest
```

Alternatively, if you pulled the image specifying a version tag, run the Docker container with this command:

```
docker run -d --name test-mongo mongo:4.0.4
```

## Manage database within a container: 

Use the following command to open the MongoDB shell:

```
docker exec -it <CONTAINER_NAME> bash
```


## 🌐  Extra reading (or watching 📺 ):

* [Full Docker course - Youtube](https://www.youtube.com/watch?v=pTFZFxd4hOI)
* [Official documentation](https://docs.docker.com/)
***