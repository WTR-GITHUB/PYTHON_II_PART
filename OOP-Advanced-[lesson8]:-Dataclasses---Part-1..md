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

```
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

* Task Nr.1:  

  Create a class method to return the **factorial** of a given number.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-3) 


* Task Nr.2:
 
  Create a class method to return the **reversed string** of a given string.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-2) 

* Task Nr.3:

  Create a class method to return t**he list of prime numbers** up to a given number.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3-3) 

* Task Nr.4: 

  Create a class to represent a library system. The library system should have a collection of books that can be borrowed by users. Users can register to 
  the library system, borrow books, and return books. The library system should keep track of the books borrowed by users, and the number of available 
  copies of each book.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4-2) 


## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python class and static methods](https://www.youtube.com/watch?v=rq8cL2XMM5M&t)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***