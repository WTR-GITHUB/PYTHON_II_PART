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

## Abstract class vs interface
As we already know, an abstract class is a class that contains one or more abstract methods, which are methods** that have a definition but no implementation**. A concrete subclass of an abstract class is required to provide an implementation for all of its abstract methods, before it can be instantiated. An abstract class can also define concrete methods, which have both a definition and an implementation.

An **interface**, on the other hand, **is a collection of abstract methods that a class can implement**. In Python, there is no built-in concept of an interface, but one can be implemented using an abstract _base class (ABC)_. An abstract base class is a class that contains only abstract methods, and it is not meant to be instantiated. Instead, other classes are expected to inherit from it and provide implementations for its abstract methods.

Here's an example of an abstract class:

```python3
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass
    
    def perimeter(self) -> float:
        pass

class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height
    
    def perimeter(self) -> float:
        return 2 * (self.width + self.height)

rect = Rectangle(3, 4)
print(rect.area()) # 12
print(rect.perimeter()) # 14
 
```

and interface: 

```python3
from abc import ABC, abstractmethod

class IAnimal(ABC):

    @abstractmethod
    def move(self) -> str:
        pass

    @abstractmethod
    def eat(self) -> str:
        pass

class Dog(IAnimals):
    def move(self) -> str:
        return 'Dog can walk and run'

    def eat(self) -> str:
        return 'Dog eat meat'

class Fish(IAnimals):
    def move(self) -> str:
        return 'Fish swim'

    def eat(self) -> str:
        return 'Fish eat small insects or plants'

dog = Dog()
print(dog.move())
print(dog.eat())

fish = Fish()
print(fish.move())
print(fish.eat())

```
## Exercises: 
🧠 : Repeat the [OOP Part 2](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Task Nr.1**:
  
  Create an abstract class Animal with which takes name of animal as an input and initialize it. 
  The create `speak` abstract method, to be overridden by subclasses.
  And `get_name` method which returns name of the animal.

  Now create two subclasses of Animals: `Dog` and `Cat` which overrides the `speak` method, and provide the implementation which returns a string "Dog 
  says Woof!" and "Cat says Meow!" respectively.
  

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-1) 

* **Task Nr.2**:

  Create an abstract class `Money` which takes `currency` and `value` as input and initializes it. A class must have these methods:
   - `get_value` method which returns the value of the money.
   - `get_currency` method which returns the currency of the money.
   - `convert_to_currency` abstract method, which takes target currency and conversion rate as input and converts the value of the money to the target 
      currency.

   Now create two subclasses of `Money`: `Cash` and `Card`. The `Cash` class should take the denomination of the cash as input in the constructor, and 
   should implement the `convert_to_currency` method. The `Card` class should take the credit limit of the card as input in the constructor, and should 
   implement the `convert_to_currency` method using the conversion rate to convert the value of the card to the target currency.

   [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2) 

* **Task Nr.3**:

  As per previous examples please create an example of your own. The abstract class should contain five (3 abstract and 2 normal ) methods. Create 2 
  subclasses that would inherit abstract class. 

* **Task Nr.4**: 

  Create a Calculator program : it should contain abstract class with methods (abstract and not), base class, `geometry`, `arithmetic` calculator 
  classes. 
  Every subclass should have at least 5 methods to make some meaningful calculus operations. 
  
## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [Official Documentation - Abstract Base Classes](https://docs.python.org/3/library/abc.html)
* [PythonTutorial](https://www.pythontutorial.net/python-oop/python-abstract-class/)
***