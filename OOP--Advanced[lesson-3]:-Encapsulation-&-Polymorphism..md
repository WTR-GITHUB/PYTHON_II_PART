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

  Define a Shape class with the following attributes and methods:

  * A name attribute, which is a string that represents the name of the shape.
  * A sides attribute, which is an integer that represents the number of sides of the shape.
  * An area method, which returns the area of the shape.

  Then, define a Rectangle class that inherits from the Shape class and has the following attributes and methods:

  * A width attribute, which is a float that represents the width of the rectangle.
  * A height attribute, which is a float that represents the height of the rectangle.
  * An __init__ method that initializes the name, sides, width, and height attributes.
  * An area method that overrides the area method of the Shape class and returns the area of the rectangle.

  Finally, define a Square class that inherits from the Rectangle class and has the following attributes and methods:

  * A side_length attribute, which is a float that represents the length of the sides of the square.
  * An __init__ method that initializes the side_length attribute and calls the __init__ method of the Rectangle class to initialize the name, sides, 
  width, and height attributes.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers#oop-advanced--inheritance) 

* Task Nr.2:
 
  - Create a Bus, Taxi, Train child classes that inherits from the Vehicle class.
  - Implement at least five methods in a superclass what would describe those vehicles.
  - The default fare charge of any vehicle is seating capacity * 100 . If Vehicle is Bus 
  - instance, we need to add an extra 10% on full fare as a maintenance charge.

* Task Nr.3:

  - Define the Animal, Mammal, and Primate classes.
  - Animal should have a name attribute and a make_noise() method.
  - Mammal should have a warm_blooded attribute and a give_birth() method.
  - Primate should have an opposable_thumbs attribute and a swing() method.
  - Test the classes by creating a Chimpanzee and making it do various things :) 🐒 

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers#task-nr3) 

* Task Nr.4: 

  Lets say we have classes: A, B and C:
    - Modify the program to add a method say_hello to class A that prints "Hello from class A".
    - Modify the program to add a method say_hello to class B that prints "Hello from class B".
    - Modify the program to add a method say_hello to class C that prints "Hello from class C".
    - Create an object of class C and call the say_hello method on it. What is the output?
    - Modify the program so that class B's say_hello method calls the say_hello method of class A using the super() function.
    - Create an object of class C and call the say_hello method on it again. What is the output now?


## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [PyNative](https://pynative.com/python-inheritance/)
***