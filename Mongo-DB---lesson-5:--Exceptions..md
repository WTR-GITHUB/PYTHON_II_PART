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

## Pymongo Exceptions

### PyMongoError Base Exception
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

###  CollectionInvalid Exception
Raised when collection validation fails.
Here's an example of a Python code implementation using PyMongo, including handling the CollectionInvalid exception. The code demonstrates how to create a collection in a MongoDB database and handle potential exceptions:

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


### ConfigurationError Exception
Raised when something is incorrectly configured.
Here's an example of a Python code implementation using PyMongo, including handling the `pymongo.errors.ConfigurationError` exception. The code demonstrates how to establish a MongoDB connection with a configuration file and handle potential exceptions:

```python
from pymongo import MongoClient
from pymongo.errors import ConfigurationError, PyMongoError

def connect_to_mongodb(config_file: str) -> MongoClient:
    try:
        # Read MongoDB configuration from file
        # Assuming the configuration file is in JSON format
        with open(config_file, 'r') as f:
            config_data = json.load(f)
        
        # Extract configuration parameters
        host = config_data.get('host', 'localhost')
        port = config_data.get('port', 27017)
        username = config_data.get('username')
        password = config_data.get('password')
        auth_source = config_data.get('auth_source')
        
        # Create a MongoDB connection string
        connection_string = f"mongodb://{username}:{password}@{host}:{port}/{auth_source}"
        
        # Connect to MongoDB
        client = MongoClient(connection_string)
        
        return client
    
    except ConfigurationError as e:
        print('Configuration error:', str(e))
        return None
    
    except PyMongoError as e:
        print('An error occurred:', str(e))
        return None

# Usage
config_file = 'mongodb_config.json'

client = connect_to_mongodb(config_file)

if client is not None:
    # Perform database operations using the client object
    # ...
    print('Connected to MongoDB successfully.')
else:
    print('Failed to connect to MongoDB.')

```
In the above code:

 - We define the connect_to_mongodb function, which takes a config_file parameter specifying the path to a JSON configuration file. The function returns 
   a MongoClient object if the connection is successful, or None if an error occurs.

 - The function reads the MongoDB configuration from the JSON file and extracts the relevant parameters, such as host, port, username, password, and 
   authentication source.

 - It constructs a MongoDB connection string using the extracted configuration parameters.

 - The function attempts to connect to MongoDB using the MongoClient constructor with the connection string.

 - If the connection is successful, the function returns the MongoClient object. Otherwise, it catches the ConfigurationError and PyMongoError exceptions 
   separately, prints the appropriate error message, and returns None.

 - In the usage section, we provide the path to the MongoDB configuration file and call the connect_to_mongodb function. Based on the return value, we 
   print the appropriate success or failure message.

By handling the ConfigurationError and PyMongoError exceptions, you can handle potential errors that may occur during the connection process and provide appropriate error messages or take necessary actions based on the returned MongoClient object or `None` value.


### ConnectionFailure Exception 
Raised when a connection to the database cannot be made or is lost.

Here's an example of a Python code implementation using PyMongo, including handling the pymongo.errors.ConnectionFailure exception. The code demonstrates how to connect to a MongoDB server and handle potential connection failures:

```python
from pymongo import MongoClient
from pymongo.errors import ConnectionFailure, PyMongoError

def connect_to_mongodb() -> MongoClient:
    try:
        # Connect to MongoDB
        client: MongoClient = MongoClient('mongodb://localhost:27017')
        
        return client
    
    except ConnectionFailure as e:
        print('Connection failure:', str(e))
        return None
    
    except PyMongoError as e:
        print('An error occurred:', str(e))
        return None

# Usage
client = connect_to_mongodb()

if client is not None:
    # Perform database operations using the client object
    # ...
    print('Connected to MongoDB successfully.')
else:
    print('Failed to connect to MongoDB.')

```

In the above code:

- We define the connect_to_mongodb function, which attempts to establish a connection to a MongoDB server. The function returns a MongoClient object if 
  the connection is successful, or None if an error occurs.

 - The function uses the MongoClient constructor to connect to the MongoDB server with the specified connection URL.

 - It wraps the connection attempt in a try-except block to catch any ConnectionFailure or PyMongoError exceptions.

 - If a ConnectionFailure exception occurs, it prints the connection failure message and returns None.

 - If any other PyMongoError exception occurs, it prints the general error message and returns None.

 - In the usage section, we call the connect_to_mongodb function to establish a connection to the MongoDB server. Based on the return value, we print the 
   appropriate success or failure message.

By handling the ConnectionFailure and PyMongoError exceptions, you can handle potential errors that may occur during the connection process and provide appropriate error messages or take necessary actions based on the returned MongoClient object or None value.


### ExecutionTimeout Exception

Raised when a database operation times out, exceeding the $maxTimeMS set in the query or command option.
Here's an example of a Python code implementation using PyMongo, including handling the pymongo.errors.ExecutionTimeout exception. The code demonstrates how to perform a MongoDB query with a specified timeout and handle potential timeout errors:

```python
from pymongo import MongoClient
from pymongo.errors import ExecutionTimeout, PyMongoError

def query_with_timeout(database_name: str, collection_name: str, query: dict, timeout_ms: int) -> list:
    try:
        # Connect to MongoDB
        client: MongoClient = MongoClient('mongodb://localhost:27017')
        db = client[database_name]
        collection = db[collection_name]
        
        # Set query options with timeout
        query_options = {'$query': query, '$maxTimeMS': timeout_ms}
        
        # Perform the query
        result = list(collection.find(query_options))
        
        # Close the MongoDB connection
        client.close()
        
        return result
    
    except ExecutionTimeout as e:
        print('Query execution timeout:', str(e))
        return []
    
    except PyMongoError as e:
        print('An error occurred:', str(e))
        return []

# Usage
database_name = 'mydatabase'
collection_name = 'mycollection'
query = {'name': 'John'}
timeout_ms = 5000

query_result = query_with_timeout(database_name, collection_name, query, timeout_ms)

if query_result:
    print('Query result:', query_result)
else:
    print('No results or error occurred during the query.')

```

In the above code:

- We define the query_with_timeout function, which takes the database_name, collection_name, query dictionary, and timeout_ms (timeout in milliseconds)  
  as input parameters. The function returns a list containing the query result or an empty list if an error occurs.

- The function connects to the MongoDB server using the MongoClient constructor.

- It selects the specified database and collection.

- The function sets the query options to include the specified query and a maximum execution time in milliseconds.

- It performs the query using the find method on the collection and converts the cursor result to a list.

- The MongoDB connection is closed.

- If an ExecutionTimeout exception occurs, the function prints the timeout error message and returns an empty list.

- If any other PyMongoError exception occurs, the function prints a general error message and returns an empty list.

- In the usage section, we provide the database name, collection name, query, and timeout value, and call the query_with_timeout function. Based on the 
  return value, we print the query result or an appropriate message if no results are returned or an error occurred.

By handling the ExecutionTimeout and PyMongoError exceptions, you can handle potential errors that may occur during the query execution and provide appropriate error messages or take necessary actions based on the returned result list or an empty list.

### OperationFailure Exception
Raised when a database operation fails.
Here's an example of a Python code implementation using PyMongo, including handling the pymongo.errors.OperationFailure exception. The code demonstrates how to perform a MongoDB update operation and handle potential operation failure errors:

```python
from pymongo import MongoClient
from pymongo.errors import OperationFailure, PyMongoError

def update_document(database_name: str, collection_name: str, filter_query: dict, update_query: dict) -> bool:
    try:
        # Connect to MongoDB
        client: MongoClient = MongoClient('mongodb://localhost:27017')
        db = client[database_name]
        collection = db[collection_name]
        
        # Perform the update operation
        result = collection.update_one(filter_query, update_query)
        
        # Close the MongoDB connection
        client.close()
        
        if result.modified_count > 0:
            return True
        else:
            return False
    
    except OperationFailure as e:
        print('Operation failure:', str(e))
        return False
    
    except PyMongoError as e:
        print('An error occurred:', str(e))
        return False

# Usage
database_name = 'mydatabase'
collection_name = 'mycollection'
filter_query = {'name': 'John'}
update_query = {'$set': {'age': 30}}

if update_document(database_name, collection_name, filter_query, update_query):
    print('Document updated successfully.')
else:
    print('Failed to update document.')

```

In the above code:

- We define the update_document function, which takes the database_name, collection_name, filter_query, and update_query as input parameters. The 
  function returns a boolean indicating whether the document update operation was successful.

- The function connects to the MongoDB server using the MongoClient constructor.

- It selects the specified database and collection.

- The function performs the update operation using the update_one method on the collection, applying the provided filter_query and update_query.

- The MongoDB connection is closed.

- If the update operation modifies at least one document (indicated by modified_count), the function returns True. Otherwise, it returns False.

- If an OperationFailure exception occurs, the function prints the operation failure error message and returns False.

- If any other PyMongoError exception occurs, the function prints a general error message and returns False.

- In the usage section, we provide the database name, collection name, filter query, and update query, and call the update_document function. Based on 
  the return value, we print the appropriate success or failure message.

By handling the OperationFailure and PyMongoError exceptions, you can handle potential errors that may occur during the update operation and provide appropriate error messages or take necessary actions based on the returned boolean value.

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