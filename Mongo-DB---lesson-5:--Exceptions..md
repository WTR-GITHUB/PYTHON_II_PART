## Introduction

`PyMong`o is a Python driver for `MongoDB`, which is a popular NoSQL database. When working with `PyMongo`, you may encounter various **exceptions** that are raised in different situations. These exceptions provide information about errors or exceptional conditions that occur during the execution of your MongoDB operations. Here are some commonly used PyMongo exceptions:

- `pymongo.errors.ConnectionError`: Raised when there is an error establishing a connection to the MongoDB server.

- `pymongo.errors.OperationFailure`: Raised when a database operation fails. It can occur due to authentication failures, write errors, or other command-specific errors.

- `pymongo.errors.DuplicateKeyError`: Raised when you attempt to insert a document with a duplicate key in a collection that has a unique index.

- `pymongo.errors.CursorNotFound`: Raised when trying to retrieve more data from a cursor that has already been closed or exhausted.

- `pymongo.errors.WriteError`: Raised when a write operation encounters an error, such as a write concern failure or a network error during a write operation.

- `pymongo.errors.InvalidURI`: Raised when there is an issue with the MongoDB connection URI.

- `pymongo.errors.InvalidOperation`: Raised when an invalid operation is performed, such as trying to modify an immutable attribute.

These are just a few examples of the exceptions provided by PyMongo. Each exception contains additional information, such as error codes and error messages, which can help you troubleshoot and handle errors in your MongoDB application effectively.

**Remember to handle exceptions appropriately in your code to provide error handling and recovery mechanisms when interacting with MongoDB using PyMongo.**

Lets go deeper with few examples: 

### pymongo.errors.PyMongoError
Base class for all PyMongo exceptions.
Here's an example of a Python code implementation using `PyMongo`, including handling the `PyMongoError` base exception. The code demonstrates how to connect to a MongoDB database, perform a query, and handle potential exceptions:

```python
from pymongo import MongoClient
from pymongo.errors import PyMongoError

def query_database() -> None:
    try:
        # Connect to MongoDB
        client = MongoClient('mongodb://localhost:27017')
        db = client['mydatabase']
        collection = db['mycollection']
        
        # Perform a query
        result = collection.find_one({'name': 'John'})
        
        # Process the result
        if result:
            print('Found document:', result)
        else:
            print('Document not found.')
        
        # Close the MongoDB connection
        client.close()
        
    except PyMongoError as e:
        print('An error occurred:', str(e))

# Call the function
query_database()

```

In the above code:

- We import the `MongoClient` class from `pymongo` to establish a connection to the MongoDB server, and the `PyMongoError` exception class to handle 
  MongoDB- related errors.

- The `query_database` function attempts to connect to the MongoDB server, select a database, and a collection.

- It performs a query using the find_one method to find a document with a specific name.

- If a document is found, it prints the result. Otherwise, it prints a message indicating that the document was not found.

- The code includes a try-except block to catch any PyMongoError exceptions that may occur during the execution of the code.

- If an exception is caught, it prints an error message containing the exception details.

By handling the `PyMongoError` exception, you can provide appropriate error handling and recovery mechanisms in your code when interacting with MongoDB using `PyMongo`.

###  pymongo.errors.CollectionInvalid
Raised when collection validation fails.
Here's an example of a Python code implementation using PyMongo, including handling the pymongo.errors.CollectionInvalid exception. The code demonstrates how to create a collection in a MongoDB database and handle potential exceptions:

```python
from pymongo import MongoClient
from pymongo.errors import CollectionInvalid, PyMongoError

def create_collection(database_name: str, collection_name: str) -> bool:
    try:
        # Connect to MongoDB
        client: MongoClient = MongoClient('mongodb://localhost:27017')
        db = client[database_name]
        
        # Create a collection
        db.create_collection(collection_name)
        
        # Close the MongoDB connection
        client.close()
        
        return True
    
    except CollectionInvalid as e:
        print('Collection creation error:', str(e))
        return False
    
    except PyMongoError as e:
        print('An error occurred:', str(e))
        return False

# Usage
database_name = 'mydatabase'
collection_name = 'mycollection'

if create_collection(database_name, collection_name):
    print('Collection created successfully.')
else:
    print('Failed to create collection.')

```
In the above code:

- We define the `create_collection` function, which takes the `database_name` and `collection_name` as input parameters and returns a `boolean` 
  indicating whether the collection creation was successful.

- The function attempts to connect to the MongoDB server and select the specified database.

- It calls the `create_collection` method on the database object to create a new collection with the specified name.

- If the collection creation is successful, the function returns True. Otherwise, it catches the CollectionInvalid exception specifically and prints an 
  error message. It also catches any other PyMongoError exception and handles it in a similar manner.

- In the usage section, we provide the desired `database_name` and `collection_name` values and call the `create_collection` function. Based on the 
  return value, we print the appropriate success or failure message.

By handling the `CollectionInvalid` and `PyMongoErro`r exceptions, you can handle potential errors that may occur during collection creation and provide appropriate error messages or take necessary actions based on the returned `boolean` value.

## Exercises: 

* Task Nr.1 :
  Create a simple database (type of db, collections, fields - pick your own) with your db creation tool and incorporate all new querying operators with the results.

* Task Nr.2: 
  Update previous (task nr.3 from [lesson](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Mongo-DB---lesson-3:-Quering-%5BPart1%5D) ) and get: 
  - all items (name and year made) where the quantity is less or equal to 10 and the price is equal or less of 20.00.
  - the average price per unit for those retrieved. 
  - all items where quantity is : 5, 10 , and 15 respectively.
 
## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***