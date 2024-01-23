## Dataclasses

Python's `dataclass` module is a **decorator-based approach** to creating classes that are primarily **used to store data**. It was introduced in Python 3.7 and allows you to define classes with less boilerplate code. A dataclass is a class that mainly consists of data and provides methods for accessing and manipulating this data.

Here's an example of how to use the dataclass module:

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int
    email: str
```

In this example, we've defined a `Person` class using the `@dataclass` decorator. The class has three attributes: `name`, `age`, and `email`, each with a type hint. The `@dataclass` decorator automatically generates several special methods, such as `__init__`, `__repr__`, and `__eq__`, based on the attributes defined in the class.

You can then create an instance of the Person class and access its attributes as follows:

```python
person = Person("John Doe", 30, "johndoe@example.com")
print(person.name) # Output: John Doe

```

Here's another example that demonstrates how to use the `dataclass` module to create a class representing a 2D point:

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float

    def distance_from_origin(self) -> float:
        return (self.x ** 2 + self.y ** 2) ** 0.5

```

In this example, we've defined a `Point` class with two attributes: `x` and `y`, each of which is a `float`. We've also defined a method `distance_from_origin` that calculates the distance of the point from the origin.

You can then create an instance of the `Point` class and call its `distance_from_origin` method as follows:

```python
point = Point(3, 4)
print(point.distance_from_origin()) # Output: 5.0

```
Overall, Python's `dataclass` module is a useful tool for creating classes with less boilerplate code that mainly consist of data. By following good coding practices, such as using type hints and following the PEP 8 style guide, you can write clean and maintainable code that is easy to understand and modify.

### Why use `dataclasses`
There are many reasons we have an increase in programmer efficiency and code quality using `@dataclass` . Here’s a list of significant major improvements :
 - Data validation: @dataclass automatically generates methods for checking the validity of the data in a class instance. @dataclass ensures that the 
   data in a class instance is in the correct format and meets any specified constraints.
 - Improved readability: @dataclass improves understanding of the structure and purpose of a class by clearly separating the data fields from the 
   behavior.
 - Automatic generation of boilerplate code: The @dataclass decorator generates several methods, such as __init__, __repr__, and __eq__, often needed 
   when working with data classes.
 - Improved maintainability: @dataclass promote better maintenance and lower the cost of refactoring code by providing a clear separation between data 
   and behavior.
 - Improved performance: The @dataclass decorator generates methods that are optimized for performance, such as the __init__ method, which uses keyword- 
   only arguments to reduce the number of attribute lookups needed.
 - Improved compatibility with immutable data structures: Data values become immutable using the @dataclass frozen=TRUE option. We show, with an example, 
   how to transform a set of global constants into a shared package of constants.


## Exercises: 

1) You have been asked to create a simple inventory management system for a small retail store. You need to define a `Product` class using the dataclass 
   module that represents a product in the store. Each `Product` should have a unique `ID`, a `name`, a `description`, a `price`, and a `quantity in 
   stock`. You also need to implement a method `calculate_total_cost` that calculates the total cost of a given number of items of the product, taking 
   into account any discounts that may apply.

   [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-4) 

2) Create a set of data classes to model an online bookstore management system. The classes should include Author, Book, Customer, and Order. Your goal 
   is to design a system that enables the management of books, authors, customers, and orders in an online bookstore.

   Author Class:
    - Attributes: author_id (int), name (str), birth_year (int)).

   Book Class:
    - Attributes: book_id (int), title (str), author (Author), publication_year (int), price (float), quantity_in_stock (int).
    - Add a method sell that reduces the quantity_in_stock when a book is sold.

   Customer Class:
    - Attributes: customer_id (int), name (str), email (str).
   
   Order Class:
    - Attributes: order_id (int), customer (Customer), books (List[Book]), total_price (float), status (str) - either "Pending" or "Shipped".
    - Initialize the attributes in the `__init__` method (override).
    - Add a method `calculate_total_price` that calculates the total price of the order based on the books' prices and quantities.
    - Add a method `ship_order` that changes the order status to "Shipped" and updates the stock quantity for each book. 

3) You need to create a program to manage a list of books in a library. Each book has a `title`, an `author`, a `publication year`, and an `ISBN`. You 
   need to define a `Book` class using the `dataclass` module that contains attributes for these properties. You also need to implement a `Library` class 
   that manages a list of books. The `Library` class should allow you to `add` and `remove` books from the library, search for books by `title` or 
   `author`, and display the list of books currently in the library.

   [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-3) 

4) You are tasked with designing an advanced `Employee Management System` using Python data classes, functional programming operations, and various 
   methods for analysis and manipulation of employee data.

   `Employee Class`:

   Create a data class named `Employee` to represent an employee. The class should have attributes for `employee_id`, name, age, salary, and department.
   
   Department Class:
   Create a data class named Department to represent a department. The class should have attributes for department_id, name, and employe 
   (List[Employee]).
    - Add a method named `average_salary` that calculates and returns the average salary of employees in the department.
     
   EmployeeManagement Class: 
   Create a data class named EmployeeManagement to manage multiple departments and employees. The class should have an attribute for departments 
   (List[Department]).
   - Add a method named `total_salary` that calculates and returns the total salary of all employees in the organization.
   - Add a method named `get_employees_in_age_range` that takes a minimum and maximum age and returns a list of employees within that age range.
   - Add a method named `sort_employees_by_salary` that returns a sorted list of employees by their salary in descending order.
   - Add a method named `filter_employees_by_department` that takes a department name and returns a list of employees in that department.
   
   Functional Operations:

   Utilize functional programming operations such as `map`, `filter`, and `sorted` where appropriate in the implementation of the methods.
   Demonstrate the use of these operations to enhance the readability and efficiency of your code.

   Test Cases:

   Create a sample dataset with multiple `employees` and `departments` to thoroughly test your system.
   Use the implemented methods to perform various analyses, such as calculating average `salaries`, sorting `employees`, and filtering `employees` by 
   criteria.

5) Create a flight ticketing mini system: 
   - The CLI should ask you to choose departure place and destination (minimum 5 cities) (Use dictionary to create a distance between the cities matrix 
     map ).
   - Then it should show options for at least 3 flight options with different different aircraft (Airbus A330-300, A340-300,A 340-600, A350- 
     100, Boeing 747-400, 747-800, 777-300). Every aircraft has different seat configuration (economy, business, first with different seat amount, seat 
     pitch and average price)
   - When you select the ticket (the provided option) the final cost should be calculated depending on aircraft type, departure time, and fuel 
     consumption. (We can agree that flights that are departure earlier, has less seats and older, cost more). Use data classes and simple classes to 
     achieve the result.  

## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python class and static methods](https://www.youtube.com/watch?v=rq8cL2XMM5M&t)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***