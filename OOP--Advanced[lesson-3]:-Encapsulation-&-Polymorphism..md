## Encapsulation

Encapsulation is an essential aspect of object-oriented programming. Let’s explain encapsulation in plain words: **information hiding**. This means delimiting the internal interface and attributing from the external world.
In Python, this can be achieved by using access modifiers to control the visibility of attributes and methods of a class.

For example, consider a simple class that represents a person with a name and age:

```python
class Person:
    def __init__(self, name: str, age: int) -> None:
        self._name = name
        self._age = age
    
    def get_name(self) -> str:
        return self._name
    
    def set_name(self, name: str) -> None:
        self._name = name
    
    def get_age(self) -> int:
        return self._age
    
    def set_age(self, age: int) -> None:
        self._age = age

```

In this example, the `Person` class has two private attributes, `_name` and `_age`, and four public methods, `get_name()`, `set_name()`, `get_age()`, and `set_age()`. The underscore before the attribute names indicates that they are intended to be **private**, meaning they should not be accessed directly from outside the class. Instead, we provide public methods to access and modify the values of these attributes.

Here's an example of how we can use this class:

```python
person = Person("Alice", 25)
print(person.get_name())  # Output: Alice
person.set_name("Bob")
print(person.get_name())  # Output: Bob
print(person.get_age())   # Output: 25
person.set_age(30)
print(person.get_age())   # Output: 30

```

By using the public methods provided by the `Person` class, we can **interact with the object in a controlled and predictable way, without needing to know the implementation details of the class**. This makes our code more modular and easier to maintain.

The benefits of information hiding are reducing system complexity and increasing robustness. Why? Because encapsulation limits the interdependencies of different software components.

## Polymorphism
`Polymorphism` is the principle that one kind of thing can take a variety of forms. In the context of programming, this means that a single entity in a programming language can behave in multiple ways depending on the context. It’s similar to how a word like `express` can act as a verb in one sentence, a noun in another sentence, and an adjective in a third sentence. The sequence of letters on the page doesn’t change, but the meaning they add to the sentence is fundamentally different in each case. Likewise, in polymorphic programming languages, a single entity can act differently in different contexts.

### Operator Polymorphism
Operator polymorphism, or operator overloading, means that one symbol can be used to perform multiple operations. One of the simplest examples of this is the addition operator `+`. Python’s addition operator works differently in relation to different `data types`. For example, if the `+` operates on two integers, the result is additive, returning the sum of the two integers: 

```python
int_one = 10
int_two = 15
print(int_one + int_two)
# returns 25
```

In the example above, the `+` operator adds `10` and `15`, such that the output is `25`.

However, if the addition operator is used on two strings, **it concatenates** the strings. Here’s an example of how the + operator acts on string data types: 

```python
str_one = "10"
str_two = "15"
print(str_one + str_two)
# returns '1015'
```

In this case, the output is `1015` because the `+` operator concatenates the strings `10` and `15`. This is one example of how a single operator can perform distinct operations in **different contexts**.

### Function Polymorphism

Certain functions in Python are polymorphic as well, meaning that they can act on multiple data types and structures to yield different kinds of information.

Python’s built-in `len()` function, for instance, can be used to return the length of an object. However, it will measure the length of the object differently depending on the object’s data type and structure. For instance, if the object is a string, the `len()` function will return the number of characters in the string. If the object is a list, it will return the number of entries in the list.

Here’s an example of how the `len()` function acts on strings and lists:

```python
str_one = "animal"
print(len(str_one))
# returns 6
list_one = ["giraffe","lion","bear","dog"]
print(len(list_one))
# returns 4
```
The outputs are `6` and `4`, respectively, because the `len()` function counts the number of characters in a string and the number of entries in a list. The function operates differently depending on the nature of the data it’s acting on.

### Class and Method Polymorphism, Method Overriding.

Python’s polymorphic nature makes it easier to repurpose classes and methods. Remember that a class is like a blueprint, and an object is a concrete instantiation of that blueprint. So, a method that is part of a class will reoccur in the objects that instantiate that class. Likewise, if you generate a new class from a preexisting class, the new class will inherit the methods of the preexisting class. The new class in this scenario is called a “child class,” while the preexisting class is called the “parent class.”

In Python, it is possible for a `subclass` to **override** the attributes and methods of its superclass. This means that the subclass can define its own implementation of an attribute or method that already exists in the superclass.

Here's an example of how to use method overriding:

```python

class Vehicle:
    def __init__(self, make: str, model: str) -> None:
        self.make = make
        self.model = model

    def start(self) -> None:
        print(f"Starting {self.make} {self.model}")

class Car(Vehicle):
    def __init__(self, make: str, model: str, year: int) -> None:
        super().__init__(make, model)
        self.year = year

    def start(self) -> None:
        print(f"Inserting key in {self.year} {self.make} {self.model}")
        super().start()

car = Car("Honda", "Accord", 2020)
car.start()  # prints "Inserting key in 2020 Honda Accord", "Starting Honda Accord"

```
In this example, the `Car` class inherits from the `Vehicle` class and **overrides** the `start` method. When we create an instance of `Car` and call the `start` method, it uses the implementation of the `start` method that is defined in the `Car` class, which prints a message about inserting the key in the car. It then calls the `start` method of the `Vehicle` class using the `super().start()` syntax, which prints a message about starting the vehicle.

## Exercises: 
🧠 : Repeat the [OOP Part 2](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* Task Nr.1:  

   Nasa needs to calculate expenses for the new mission: using OOP principles implement Base and Space Shuttle classes.
   Create a simple calculator with: 
   - Base class should give a functionality to know info about spacecraft (age, cost, year built, weight etc.. ).
   - Through the main class you should be able to calculate the mission cost which includes: fuel cost (FUEL_COST x BURN_RATE (kg/mile) * 
     BURN_RATE_VARIABLE (2500 / orbit_height(in miles))) , average personals expenditures ( ppl x base_salary ).
   - Prepare the final report in the file document and on screen with a method `get_full_report` with all gathered and calculated data. 


* Cafeteria project :
  Create an `live` menu and payment system (a.k.a console program) :
  - First the program should ask if table was reserved/ not (Providing your full name) . And then if not would assign you a table (there is a specific 
    number single, double or family tables) . After table is assigned to you, system should show how many free tables are and how which are 
    reserved/occupied. The system must be able to show name/surname of the person of the reserved table (CLI option : enter reserved table nuber ; 
    OUTCOME: Name/Surname/Time Reserved) 
  - After assigning table, system should show different menu options for breakfast, lunch , dinner , drinks (alcohol. alcohol free), to choose from. 
    Special menu for vegetarian and vegan must be included too in the special menu. All menu items should have weight, preparation time in minutes, 
    calories, and price.
  - I have to have an option to change the order before the payment section. Thus I can delete, add more, update amount of the same order.
  - I should be able to choose whatever I want from all menus in one ordering. After I finish, I need to see what I chosen, the full payable amount and 
    approx waiting time for the food to be served
  - Add an option to add tips (% from the full cost) to the final bill.
  - After the payment , system should generate the receipt (logging).

 
  

## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
***