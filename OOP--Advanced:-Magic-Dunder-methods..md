## Magic Methods

In Python, _"magic methods"_ or _"dunder methods"_ are special methods that have **double underscores** at the beginning and end of their names (e.g. `__init__`, `__add__`). These methods are used to define the behavior of certain operations on objects of a class. For example, the `__add__` method is called when the `+` operator is used on objects of a class, and the `__init__` method is called when a new object of a class is created. By defining these methods in a class, you can customize the behavior of built-in operations for instances of that class. We will cover only some of them, the full list can be found [here](https://docs.python.org/3/reference/datamodel.html) 

### `__init__` :
As you already know, `__init__` method is a special method in Python classes that is called when a new instance of the class is created. It is used to set up the initial state of the object. The `__init__` method takes the first argument as self, which refers to the instance of the object being created. The self argument is automatically passed by Python when a new instance is created, so you don't need to include it in the method call.

Here is an example of a class `Person` that has an `__init__` method:

```python
class Person:
    def __init__(self, name:str, age:int):
        self.name = name
        self.age = age
```

### `__str__` : 

The `__str__` dunder method is used to define the _string representation_ of an object. It is called when the built-in `str()` or `print()` functions are used on an object, and returns a string that describes the object. Here is an example of how to use the `__str__` method to define the string representation of a custom object called `Person`:

```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Person(name={self.name}, age={self.age})"

p = Person("John", 30)
print(p) # Person(name=John, age=30)

```

### `__repr__` : 
The `__repr__` is used to define the _"official"_ or unambiguous _string representation_ of an object. It is called by the built-in `repr()` function and is also used by the interactive interpreter to display the object when **it is not assigned to a variable**. It should return a string that, if passed to the `eval()` function, would create an object that is equal to the original.

Here is an example of how to use the `__repr__` method to define the string representation of a custom object called `Person`:

```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("John", 30)
print(p) # Person('John', 30)
print(repr(p)) # Person('John', 30)

```

It's good practice to also implement the `__str__` method in classes, this method is used to return a user-friendly string representation of the object, such as when the `print()` function is called.


### `__eq__` : 

The `__eq__`  is used to define the behavior of the equality operator `==` for a custom object. It is called when the `==` operator is **used to compare two objects of the same class** and should return `True` if the objects are equal, or `False` if they are not.

Here is an example of how to use the `__eq__` method with the same `Person` class:

```python3
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __eq__(self, other: 'Person') -> bool:
        if isinstance(other, Person):
            return self.name == other.name and self.age == other.age
        return False

p1 = Person("John", 30)
p2 = Person("John", 30)
p3 = Person("Jane", 25)

print(p1 == p2) # True
print(p1 == p3) # False

```
It's important to note that when comparing custom objects, it is also a good practice to implement the `__ne__` method that **return the opposite** of `__eq__` method. It is called when the `!=` operator is used, this helps to maintain consistency in the behavior of the comparison operators.

### `__eq__` :


## Exercises: 
🧠 : Repeat the [OOP Part 2](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Task Nr.1**:
  
  Create a class `Person` that has two methods: `set_name` and `set_age`, which set the name and age attributes of the class, respectively.
  Modify these methods to return `self`, so that the calls can be chained together.
  

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1) 

* **Task Nr.2**:

  Create a class Currency that has the following properties:

    - code: A 3-letter currency code (e.g. "USD", "EUR", "GBP")
    - amount
    - exchange_rate

  Create the following methods:

    - set_code: A method that accepts a 3-letter currency code and sets the code attribute of the object
    - set_amount: A method that accepts a float number and sets the amount attribute of the object
    - set_exchange_rate: A method that accepts a float number and sets the exchange_rate attribute of the object
    - convert: A method that accepts a 3-letter currency code and a float number representing the new exchange rate, and calculates the new amount of 
      currency based on the exchange rate.
    - __str__: A method that returns a string representation of the Currency object in the following format "code: amount"

     Each method should return the instance of the class to allow method chaining.

* **Task Nr.3**:

  - Create a class Animal with a method speak that prints "Animal can't speak"

  - Create a class Dogs that inherits from Animals and overrides the speak method to print "Woof woof"

  - Create a class Cats that inherits from Animals and overrides the speak method. But in this new method call the speak method from the Animals class 
    using the super() function, after that print "Meow meow"

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3) 

* **Task Nr.4**: 

  Create a class Person that has the following properties:

   - name: A string representing the person's name
   - age: An integer representing the person's age

  Create the following methods:

   - get_name: A method that returns the person's name
   - get_age: A method that returns the person's age
   - __str__: A method that returns a string representation of the Person object in the following format: "name is age years old."

  Create a class Student that inherits from Person and adds the following properties:

   - student_id: An integer representing the student's id
   - major: A string representing the student's major

  Create the following methods:

   - get_student_id: A method that returns the student's id
   - get_major: A method that returns the student's major
   - __str__: A method that returns a string representation of the Student object in the following format: "name is a age years old student of major 
     major. Student id: student_id"

  Create a class GraduateStudent that inherits from Student and adds the following properties:

   - program: A string representing the graduate student's program
   - advisor: A string representing the graduate student's advisor

  Create the following methods:

   - get_program: A method that returns the graduate student's program
   - get_advisor: A method that returns the graduate student's advisor
   - __str__: A method that returns a string representation of the GraduateStudent object in the following format: "name is a age years old graduate 
     student of major major. Student id: student_id. program: program and advisor: advisor."
   - __init__: This method should take in the same parameters as Person's init, but also take in additional parameters student_id, major, program, 
     advisor and call the super's class init method with Person's parameters and set the additional parameters.

   Show examples with working code. 
   
 [Hint](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4) 

## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [QuanticDev - method chaining](https://quanticdev.com/articles/method-chaining/)
* [RealPhyton - super() function](https://quanticdev.com/articles/method-chaining/)
***