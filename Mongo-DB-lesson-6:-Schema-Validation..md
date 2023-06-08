## Introduction
`MongoDB Schema Validation` is a feature that allows you to enforce structure and integrity rules on the documents stored in a MongoDB collection. It **enables you to define a set of validation rules that govern the structure and content of your data, ensuring that only valid and consistent documents are inserted or updated in the database**.

With schema validation, you can specify **rules for fields such as data types, value ranges, required fields, and more**. It helps maintain the data quality and consistency of your MongoDB collections, reducing the chances of storing invalid or inconsistent data.

The validation rules are defined using the `JSON schema` format, which is a standardized way of describing the structure and constraints of `JSON` documents. You can define these rules when creating or updating a collection, and MongoDB will automatically enforce them when performing write operations on the collection.

Schema validation in MongoDB can be used to enforce a wide range of constraints, including simple checks like data type validation, as well as complex rules involving relationships between fields and cross-field validation. This allows you to define custom rules that suit your specific data requirements.

By enforcing schema validation, you can improve the reliability and quality of your data, making it easier to work with and ensuring that it adheres to the desired structure. It provides an additional layer of data integrity within your MongoDB deployments and helps prevent data inconsistencies and errors.

It's worth noting that schema validation is an optional feature in MongoDB, and you can choose whether or not to enable it for your collections. When used appropriately, schema validation can be a powerful tool for maintaining the integrity and consistency of your MongoDB data.

## Exercises: 


* Task Nr.1 :
  Using all Exceptions explained above, create a simple application(s) to test (if possible in local environment) all of them. Use Docker Container 
  for live connection.
* Task Nr.2: 
  Update previous (task nr.3 from [lesson](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Mongo-DB---lesson-3:-Quering-%5BPart1%5D) ) with updating code with possible error handling.
## 🌐  Extra reading (or watching 📺 ):

* [Full Mongo course - Youtube](https://www.youtube.com/watch?v=c2M-rlkkT5o)
* [Official documentation](https://www.mongodb.com/docs/)
***