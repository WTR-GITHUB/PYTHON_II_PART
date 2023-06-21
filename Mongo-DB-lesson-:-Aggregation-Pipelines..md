## Introduction
`PyMongo` **aggregation pipelines** provide a powerful and flexible way to process and transform data in MongoDB. By utilizing a series of pipeline stages, PyMongo allows developers to _construct sophisticated data manipulation workflows_. The aggregation framework offers various stages and operators that enable **filtering, sorting, grouping, projecting, and joining documents** from multiple collections. This functionality empowers developers to perform complex data operations efficiently within the database, reducing the need for extensive data retrieval and processing in application code. Additionally, PyMongo's support for typing and adherence to good coding practices ensure that pipeline code remains clear, maintainable, and scalable. With PyMongo aggregation pipelines, developers can unleash the full potential of MongoDB's data processing capabilities, unlocking insights and delivering performant solutions for diverse data analysis and reporting requirements.


## Filtering Documents
PyMongo aggregation pipelines provide a flexible and efficient way to filter and process documents in MongoDB. The `$match` stage is commonly used to filter documents based on specific criteria. Let's explore an example:

```python
from pymongo import MongoClient
from pymongo.collection import Collection
from pymongo.cursor import Cursor
from typing import Dict, Any

def filter_documents(collection: Collection, filter_criteria: Dict[str, Any]) -> Cursor:
    pipeline = [
        {
            '$match': filter_criteria
        }
    ]
    return collection.aggregate(pipeline)

# Establish a connection to the MongoDB server
client = MongoClient('mongodb://localhost:27017')
db = client['your_database']
collection = db['your_collection']

# Define the filter criteria
criteria = {'status': 'active'}

# Call the filter_documents function
result = filter_documents(collection, criteria)

# Iterate over the cursor and print the filtered documents
for doc in result:
    print(doc)
```

In this example, we define a function `filter_documents` that takes a `Collection` object and a dictionary `filter_criteria` as input. The `filter_criteria` parameter allows you to specify the filtering conditions based on your requirements.

Within the function, we construct the pipeline using the `$match` stage with the provided `filter_criteria`. This stage filters the documents in the collection based on the specified criteria.

It's important to note that `filter_criteria` can include various filtering conditions such as equality, inequality, range queries, logical operators (`$and`, `$or`, `$not`), and more, depending on your needs. You can customize the `filter_criteria` dictionary to match your desired filtering logic.

The function returns a `Cursor` object, which can be iterated over to access the filtered documents. In this example, we simply print each document, but you can perform further processing or analysis on the filtered results as needed.

### More complex query 
 Here's a more complex example that demonstrates filtering objects using `$and`, `$or`, and `$not` operators in `PyMongo` aggregation pipelines:

```python
from pymongo import MongoClient
from pymongo.collection import Collection
from pymongo.cursor import Cursor
from pymongo.database import Database
from typing import Dict, Any, List

def filter_documents(collection: Collection, filter_criteria: List[Dict[str, Any]]) -> Cursor:
    pipeline = [
        {
            '$match': {
                '$and': filter_criteria
            }
        }
    ]
    return collection.aggregate(pipeline)

# Establish a connection to the MongoDB server
client: MongoClient = MongoClient('mongodb://localhost:27017')
db: Database = client['your_database']  # Type: Database
collection: Collection = db['your_collection']  # Type: Collection

# Define the filter criteria
criteria: List[Dict[str, Any]] = [
    {'status': 'active'},
    {'$or': [{'category': 'electronics'}, {'category': 'clothing'}]},
    {'$not': {'price': {'$gt': 100}}}
]  # Type: List[Dict[str, Any]]

# Call the filter_documents function
result: Cursor = filter_documents(collection, criteria)  # Type: Cursor

# Iterate over the cursor and print the filtered documents
for doc in result:
    print(doc)

```

In this example, the `filter_criteria` parameter is a list of dictionaries, where each dictionary represents a separate filtering condition. The list elements are combined using the `$and` operator to create a logical conjunction of the conditions.

The filter criteria consist of three conditions:

 - Documents with the `status` field set to `active`.
 - Documents where the `category` field is either `electronics` or `clothing`, achieved using the `$or` operator.
 - Documents where the `price` field is not greater than `100`, implemented using the `$not` operator.

These conditions demonstrate a more complex filtering scenario involving logical conjunction (`$and`), logical disjunction (`$or`), and negation (`$not`).

The `filter_documents` function constructs an aggregation pipeline with the `$match` stage, where the `$and` operator combines the filter criteria from the `filter_criteria` list.

The resulting pipeline is passed to the aggregate method, which returns a `Cursor` object. We then iterate over the cursor to access and print the filtered documents.

By utilizing operators such as `$and`, `$or`, and `$not`, you can create complex filter conditions to suit your specific requirements when working with PyMongo aggregation pipelines.

## Exercises: 


* Task Nr.1 :

  Instructions:
    - Connect to a MongoDB server running on localhost.
    - Create a new database named 'exercise_db' and a collection named 'exercise_collection'.
    - Define the following JSON schema validation rules for the collection:
    - The document must be an object.
    - The 'name' field is required and must be a string.
    - The 'age' field is required and must be an integer between 18 and 99.
    - The 'email' field is required and must be a string containing a valid email address.
    - Insert three documents into the collection, one that satisfies the validation rules and two that violate the validation rules.
    - Print all the documents in the collection.
    - Clean up by dropping the collection and closing the MongoDB connection.

 [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-7) 

* Task Nr.2: 

   Instructions:

   - Connect to a MongoDB server running on localhost.
   - Create a new database named 'shopping_db' and a collection named 'shopping_collection'.
   - Define the following JSON schema validation rules for the collection:
    - The document must be an object.
    - The 'name' field is required and must be a string.
    - The 'age' field is required and must be an integer between 18 and 99.
    - The 'email' field is required and must be a string containing a valid email address.
    - The 'address' field is required and must be an object.
    - The 'address' object must have the 'street', 'city', and 'postal_code' fields, each being a required string.
   - Insert three documents into the collection, one that satisfies the validation rules and two that violate the validation rules.
   - Print all the documents in the collection.
   - Clean up by dropping the collection and closing the MongoDB connection.

* Task Nr.3: 
  Update previous (task nr.3 from [lesson](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Mongo-DB---lesson-3:-Quering-%5BPart1%5D) ) with schema validation.
## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***