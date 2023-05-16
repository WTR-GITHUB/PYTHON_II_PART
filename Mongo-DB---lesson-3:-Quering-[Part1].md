## Introduction
We can query a `MongoDB` database using `PyMongo` with the `find` function to get all the results satisfying the given condition and also using the `find_one` function, which will return only one result satisfying the condition.

The following is the syntax of the find and find_one:

```python
your_collection.find( {<< query >>} , { << fields>>} )
```

## Filter based on fields & conditions

For instance, you have hundreds of fields and you want to see only a few of them. You can do that by just putting all the required field names with the value `1`. For example:

```python
your_shop_collection.find_one( {}, { "week": 1, "checkout_price" : 1})
```

On the other hand, if you want to discard a few fields only from the complete document, you can put the field names equal to `0`. **Therefore, only those fields will be excluded**. Please note that you cannot use a combination of 1s and 0s to get the fields. Either all should be one, or all should be zero.

```python
your_shop_collection.find_one( {}, {"num_orders" : 0, "meal_id" : 0})
```

Now, in this section, we will provide a condition **in the first braces and fields to discard in the second**. Consequently, it will return the `first document` with `center_id` equal to `55` and `meal_id` equal to `1885` and will also discard the fields `_id` and `week`:

```python
your_shop_collection.find_one( {"center_id" : 55, "meal_id" : 1885}, {"_id" : 0, "week" : 0} )
```

## Filter based on Comparison Operators

<html><body>
<!--StartFragment-->

NAME | DESCRIPTION
-- | --
$eq | It will match the values that are equal to a specified value.
$gt | It will match the values that are greater than a specified value.
$gte | It will match all the values that are greater than or equal to a specified value.
$in | It will match any of the values specified in an array.
$lt | It will match all the values that are less than a specified value.
$lte | It will match all the values that are less than or equal to a specified value.
$ne | It will match all the values that are not equal to a specified value.
$nin | It will match none of the values specified in an array.

<!--EndFragment-->
</body>
</html>


### $eq and $ne

Here are code examples for filtering `MongoDB` using `PyMongo` with the `$eq` (equals) and `$ne` (not equals) operators:

```python
from typing import List
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["your_database_name"]
collection = db["your_collection_name"]

# Filtering using $eq operator
def filter_by_equals(field_name: str, value: str) -> List[dict]:
    query = {field_name: {"$eq": value}}
    result = collection.find(query)
    return list(result)

# Example usage: Filter documents where the "age" field is equal to 25
filtered_equals = filter_by_equals("age", "25")
print(filtered_equals)


# Filtering using $ne operator
def filter_by_not_equals(field_name: str, value: str) -> List[dict]:
    query = {field_name: {"$ne": value}}
    result = collection.find(query)
    return list(result)

# Example usage: Filter documents where the "name" field is not equal to "John"
filtered_not_equals = filter_by_not_equals("name", "John")
print(filtered_not_equals)

```
In the above code:

- The `filter_by_equals` function takes a field name and a value as parameters, creates a query using the `$eq` operator, executes the query using 
  `collection.find()`, and returns a list of matching documents.
- The `filter_by_not_equals` function is similar but uses the $ne operator instead.
- The resulting documents are converted to a list using `list(result)` to make it easier to work with the results.
- The function calls demonstrate filtering by the `age` field equal to `25` and the `name` field not equal to `John`, respectively.

By encapsulating the filtering logic in functions, you can reuse the code for different fields and values as needed. Additionally, converting the query results to a list provides a concrete data structure for further processing.


## Exercises: 

* Task Nr.1 :
  Create a class that would implement basic CRUD operations to manage book data in the library.
 
  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-6) 

* Task Nr.2:  
  Create a command-line task manager application using Python and MongoDB. The application should allow users to perform basic CRUD operations (Create, 
  Read, Update, Delete) on tasks stored in a MongoDB database. Users should be able to add new tasks, view all tasks, update task status, and delete 
  tasks.
 
  Requirements:

  - The application should utilize the PyMongo library for interacting with the MongoDB database.
  - Users should be able to perform the following actions:
        - Add a new task with a title and description.
        - View all tasks with their details.
        - Update the status of a task (e.g., mark as completed or in progress).
        - Delete a task.
   - Implement error handling and validation for user inputs.
   - Use appropriate functions and modular code structure for better code organization.
   - Include a README file with clear instructions on how to set up and run the application.

 

## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***