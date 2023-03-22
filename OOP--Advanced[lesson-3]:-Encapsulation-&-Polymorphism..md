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