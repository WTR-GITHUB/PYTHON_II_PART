## Continue

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


###  Here are code examples for filtering MongoDB using `PyMongo` with the `$gte` (greater than or equal to) and `$lte` (less than or equal to) operators:

```python
from typing import List
from pymongo import MongoClient
from pymongo.collection import Collection

# Filtering using $gte operator
def filter_by_greater_than_equal(collection: Collection, field_name: str, value: int) -> List[dict]:
    query = {field_name: {"$gte": value}}
    result = collection.find(query)
    return list(result)

# Example usage: Filter documents where the "age" field is greater than or equal to 25
filtered_greater_than_equal = filter_by_greater_than_equal(collection, "age", 25)
print(filtered_greater_than_equal)


# Filtering using $lte operator
def filter_by_less_than_equal(collection: Collection, field_name: str, value: int) -> List[dict]:
    query = {field_name: {"$lte": value}}
    result = collection.find(query)
    return list(result)

# Example usage: Filter documents where the "rating" field is less than or equal to 4.5
filtered_less_than_equal = filter_by_less_than_equal(collection, "rating", 4.5)
print(filtered_less_than_equal)

```



## Exercises: 

* Task Nr.1 :
  Create the CLI application, that would populate MongoDB database with random data. The input should ask for :
  - database name
  - collection name
  - field name with types (string, number, date string objects etc.) with range of values (lets say field name = price , then value is number (float, 
    int) which is random number from a(min) to b(max) )
  - number o documents to create.

* Task Nr.2: 
  Write a function `filter_documents` that takes a `MongoDB` collection, a field name, an equal value, and a not equal value as parameters. The function 
  should return a list of documents from the collection where the specified field is equal to the equal value and not equal to the not equal value.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#mongo-db---lesson-3-quering-part1) 

* Task Nr.3:  
  With your own tool, create of database of grocery store. Store consist three different categories of items (lets say electronics, fruits, food etc.).
  The items as minimum should have these fields: name, price, quantity, year made (YYYY-MM-DD). 
  Task: 
   - Get all electronic items monetary value  made 1 years, 2 months and 12 days from today. 
   - Get average price for all items/categories in the store.
   - Get all items which names starts with letter `a`, and cost is between 10 and 100.
   - Find all item names (only) for prices > 50 and quantity < 10. 

## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***