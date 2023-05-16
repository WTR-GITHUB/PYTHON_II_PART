## Introduction
We can query a `MongoDB` database using `PyMongo` with the `find` function to get all the results satisfying the given condition and also using the `find_one` function, which will return only one result satisfying the condition.

The following is the syntax of the find and find_one:

```python
your_collection.find( {<< query >>} , { << fields>>} )
```

## Filter

### Filter based on fields

For instance, you have hundreds of fields and you want to see only a few of them. You can do that by just putting all the required field names with the value `1`. For example:

```python
your_shop_collection.find_one( {}, { "week": 1, "checkout_price" : 1})
```

On the other hand, if you want to discard a few fields only from the complete document, you can put the field names equal to `0`. **Therefore, only those fields will be excluded**. Please note that you cannot use a combination of 1s and 0s to get the fields. Either all should be one, or all should be zero.

```python
your_shop_collection.find_one( {}, {"num_orders" : 0, "meal_id" : 0})
```

### Filter with a condition

Now, in this section, we will provide a condition **in the first braces and fields to discard in the second**. Consequently, it will return the `first document` with `center_id` equal to `55` and `meal_id` equal to `1885` and will also discard the fields `_id` and `week`.


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