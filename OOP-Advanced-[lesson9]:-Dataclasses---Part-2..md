## Dataclasses (Continue)

### Default values, `field`
 One of the useful features of dataclasses is the ability to define default values for attributes and fields.

Here is an example of defining default values for fields in a `dataclass`:

```python
from dataclasses import dataclass

@dataclass
class Person:
    name: str
    age: int = 18
    gender: str = 'male'

p1 = Person('John')
print(p1)  # Person(name='John', age=18, gender='male')

p2 = Person('Jane', 25, 'female')
print(p2)  # Person(name='Jane', age=25, gender='female')

```
In the above code, we defined a `Person` dataclass with three fields: `name`, `age`, and `gender`. The `age` and `gender` fields have default values of `18` and `male`, respectively. When we create a new instance of the `Person` class, we can provide values for the `name`, `age`, and `gender` fields. If we don't provide a value for age and gender, their default values will be used.

We can also specify **default values for fields using factory functions**. Here's an example:

```python
from dataclasses import dataclass, field

def get_default_age():
    return 18

@dataclass
class Person:
    name: str
    age: int = field(default_factory=get_default_age)
    gender: str = 'male'

p1 = Person('John')
print(p1)  # Person(name='John', age=18, gender='male')

p2 = Person('Jane', gender='female')
print(p2)  # Person(name='Jane', age=18, gender='female')

```
In this example, we define a `get_default_age()` function that returns the default `age` value of `18`. We use the `field()` function to specify the `default value` for the `age` **field**, passing in the `get_default_age()` function as the `default_factory` argument. When we create a new instance of the `Person` class, the `age` field will be initialized with the value returned by the `get_default_age()` function.


## Exercises: 

* Task Nr.1:
 
  You have been asked to create a simple inventory management system for a small retail store. You need to define a `Product` class using the dataclass 
  module that represents a product in the store. Each `Product` should have a unique `ID`, a `name`, a `description`, a `price`, and a `quantity in 
  stock`. You also need to implement a method `calculate_total_cost` that calculates the total cost of a given number of items of the product, taking 
  into account any discounts that may apply.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-4) 


* Task Nr.2:

  You need to create a program to manage a list of books in a library. Each book has a `title`, an `author`, a `publication year`, and an `ISBN`. You 
  need to define a `Book` class using the `dataclass` module that contains attributes for these properties. You also need to implement a `Library` class 
  that manages a list of books. The `Library` class should allow you to `add` and `remove` books from the library, search for books by `title` or 
  `author`, and display the list of books currently in the library.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-3) 

* Task Nr.3:

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3-3) 

* Task Nr.4: 

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4-2) 


## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python class and static methods](https://www.youtube.com/watch?v=rq8cL2XMM5M&t)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***