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

## Accessing Databases and Collections

With `PyMongo`, you can access databases and collections using dot notation. You can retrieve a specific database using `client.database_name` and a collection using `client.database_name.collection_name`. `PyMongo` also provides methods for listing available databases and collections:

```python
from pymongo import MongoClient
from pymongo.database import Database
from pymongo.collection import Collection
from typing import List

def connect_to_mongodb(host: str, port: int, db_name: str) -> Database:
    client = MongoClient(host, port)
    database = client[db_name]
    return database

def get_database_collection(database: Database, collection_name: str) -> Collection:
    collection = database[collection_name]
    return collection

def list_databases(client: MongoClient) -> List[str]:
    return client.list_database_names()

def list_collections(database: Database) -> List[str]:
    return database.list_collection_names()

# Example usage
if __name__ == "__main__":
    # Connection details
    mongodb_host = 'localhost'
    mongodb_port = 27017
    database_name = 'mydatabase'
    collection_name = 'mycollection'

    # Connect to MongoDB
    client = MongoClient(mongodb_host, mongodb_port)
    db = connect_to_mongodb(mongodb_host, mongodb_port, database_name)

    # Retrieve a specific collection
    collection = get_database_collection(db, collection_name)
    print(f"Retrieved collection: {collection_name}")

    # List all databases
    databases = list_databases(client)
    print("List of databases:")
    for db_name in databases:
        print(db_name)

    # List collections in the connected database
    collections = list_collections(db)
    print("Collections in the connected database:")
    for collection_name in collections:
        print(collection_name)

```

In the above code:

- We import the necessary modules: MongoClient from pymongo for establishing the connection, Database from pymongo.database for type hinting the database 
  object, Collection from pymongo.collection for type hinting the collection object, and List from typing for type hinting the returned lists.

- The connect_to_mongodb function remains the same as before, which establishes the connection and returns the specified database.

- The get_database_collection function takes in the database object and the collection name as parameters. It retrieves and returns the specified 
   collection using dot notation.

- The list_databases function takes the MongoClient object as a parameter and returns a list of all the database names using list_database_names().

- The list_collections function takes the Database object as a parameter and returns a list of all the collection names in the connected database using 
  list_collection_names().

- In the example usage section, we provide the connection details: mongodb_host, mongodb_port, database_name, and collection_name.

- We first establish a connection to the MongoDB server using MongoClient and store it in the client variable.

- Then we connect to the specified database using the connect_to_mongodb function.

- We retrieve a specific collection using the get_database_collection function and store it in the collection variable.

- We use the list_databases function to retrieve all the database names and print them.

- We use the list_collections function to retrieve all the collection names in the connected database and print them.


## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***