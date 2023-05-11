## Introduction

`PyMongo` is the official Python driver for MongoDB, which allows Python developers to interact with MongoDB databases from their Python applications. It provides a high-level, user-friendly interface to connect to a MongoDB server, perform database operations, and manipulate data.

## Installation 
`PyMongo` can be installed using Python's package manager, pip, by running the command : 

```shell
pip install pymongo
```  
This will install the necessary dependencies and make PyMongo available for use in your Python environment.

## Connecting to database
Connecting to MongoDB: `PyMongo` allows you to establish a connection to a MongoDB server using the `MongoClient` class. You need to provide the connection details such as the server's `hostname` and `port number`. Once connected, you can access databases and collections within the server:

```python
from pymongo import MongoClient
from pymongo.database import Database

def connect_to_mongodb(host: str, port: int, db_name: str) -> Database:
    client = MongoClient(host, port)
    database = client[db_name]
    return database

# Example usage
if __name__ == "__main__":
    # Connection details
    mongodb_host = 'localhost'
    mongodb_port = 27017
    database_name = 'mydatabase'

    # Connect to MongoDB
    db = connect_to_mongodb(mongodb_host, mongodb_port, database_name)
    print(f"Connected to MongoDB: {mongodb_host}:{mongodb_port}, Database: {database_name}")

```

In the above code:

- We import the necessary modules: `MongoClient` from `pymongo` for establishing the connection and `Database` from `pymongo.database` for type hinting 
  the returned database object.

- The `connect_to_mongodb` function takes in the host, port, and database name as parameters. It establishes a connection to the MongoDB server using 
  MongoClient and returns the specified database using dot notation.

- In the example usage section, we provide the connection details: `mongodb_host`, `mongodb_port`, and `database_name`.

- We call the `connect_to_mongodb` function with the provided connection details, and it returns the database object.

- Finally, we print a confirmation message displaying the connection details and the database name.




## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***