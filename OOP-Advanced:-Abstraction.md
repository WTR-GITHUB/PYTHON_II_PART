## Abstract classes and methods

In object-oriented programming, **abstraction** is a principle that helps to separate the implementation details of a class from its **interface** (look bellow ⏬ ), or the way that other classes interact with it. _This allows for greater flexibility and reusability of code_, as the implementation of a class can be changed without affecting other parts of the system.

**In Python, abstraction is achieved through the use of abstract classes and abstract methods**. An `abstract class` is a class that is defined but **not meant to be instantiated**. Instead, it serves as a **template** for other classes to **inherit from**. _Abstract classes can define abstract methods, which are methods that are defined in the abstract class but have no implementation_. Subclasses of the abstract class are **required to provide** an implementation for these methods.

Here is an example of an abstract class in Python:

```python
from abc import ABC, abstractmethod
from typing import Union

class Shape(ABC):
    @abstractmethod
    def area(self) -> int:
        pass

class Rectangle(Shape):
    def __init__(self, width: int, height: int):
        self.width = width
        self.height = height

    def area(self) -> int:
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius: float):
        self.radius = radius

    def area(self) -> float:
        return 3.14 * self.radius ** 2

```
In the above example, `Shape` is an `abstract class` that defines an abstract method `area()`. The `Rectangle` and `Circle` classes are subclasses of `Shape` and provide implementations for the `area()` method.

It's important to notice that `ABC` and `abstractmethod` are part of python built-in library `abc`, This library provided python with `abstract base class(ABC)` and decorator (check another lesson, TBA) `abstractmethod` which needs to be imported and used, when implementing `abstract` classes.

It's also important to mention **that it's not allowed to create instance of an abstract class**, If you try to create an instance of an abstract class, Python **will raise** a `TypeError` exception.

In addition to the above example, one more example is:

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def no_of_wheels(self) -> None:
        pass

class Car(Vehicle):
    def no_of_wheels(self) -> int:
        return 4

class Bike(Vehicle):
    def no_of_wheels(self) -> int:
        return 2
```
In this example, `Vehicle` is an abstract class that defines an abstract method `no_of_wheels()`, and `Car`, `Bike` are concrete subclasses, which provides an implementation for `no_of_wheels` method.

One more example about payment systems (more complex: abstraction, inheritance):

```python
from abc import ABC, abstractmethod
from typing import List

class Payment(ABC):
    @abstractmethod
    def get_transactions(self) -> List[str]:
        pass

    @abstractmethod
    def process_payment(self, amount: float) -> str:
        pass

class CreditCardPayment(Payment):
    def __init__(self, card_number: str):
        self.card_number = card_number
        self.transactions = []

    def get_transactions(self) -> List[str]:
        return self.transactions

    def process_payment(self, amount: float) -> str:
        transaction_id = "CC" + str(hash(str(amount) + self.card_number))
        self.transactions.append(transaction_id)
        return f"Payment of {amount} processed with card number {self.card_number}. Transaction ID: {transaction_id}"

class PayPalPayment(Payment):
    def __init__(self, email: str):
        self.email = email
        self.transactions = []

    def get_transactions(self) -> List[str]:
        return self.transactions

    def process_payment(self, amount: float) -> str:
        transaction_id = "PP" + str(hash(str(amount) + self.email))
        self.transactions.append(transaction_id)
        return f"Payment of {amount} processed with PayPal account {self.email}. Transaction ID: {transaction_id}"

```
In this example, there's an abstract class `Payment`, which defines two abstract methods `get_transactions()` and `process_payment()`.

`CreditCardPayment` and `PayPalPayment` are subclasses of `Payment`, which provide concrete implementations of the two abstract methods defined in the parent class.

Each of the subclasses has their own way of processing payments and generating transaction ID.

Each class also has an instance variable transactions which contains a list of transactions that have been made through this payment method. The `get_transactions()` method of each class returns the list of transactions made through this payment method.

This example demonstrates _the use of abstraction to separate the implementation details of the different payment methods from their common interface_, defined by the `Payment` class. _The Payment class provides a template for the subclasses to follow, and the subclasses provide concrete implementations of the abstract methods._

**It's best practice to keep all the abstract methods in a separate abstract class**, this way you can ensure that the common properties and methods for a group of similar classes, will be written and managed in a single place.

In a nutshell - _the abstraction principle in python allows for the separation of implementation details from the interface, and abstract classes and methods provide a way to define this separation by providing a template for subclasses to follow, this way subclasses are forced to implement certain methods which are defined in the abstract class_.

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