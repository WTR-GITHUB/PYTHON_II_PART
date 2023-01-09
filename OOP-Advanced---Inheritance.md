## Multiple Inheritance & MRO (Method Resolution Order)

In Python, a class **can inherit from multiple superclasses**, a concept known as `multiple inheritance`. This allows a class to inherit attributes and methods from multiple superclasses.

Here's an example of how to use multiple inheritance in Python:

```python
from typing import Type

class Animal:
    def __init__(self, name: str) -> None:
        self.name = name
    
    def make_sound(self) -> None:
        print("Some generic animal sound")

class Dog(Animal):
    def __init__(self, name: str, breed: str) -> None:
        super().__init__(name)
        self.breed = breed
    
    def make_sound(self) -> None:
        print("Bark")

class Cat(Animal):
    def __init__(self, name: str, fur_color: str) -> None:
        super().__init__(name)
        self.fur_color = fur_color
    
    def make_sound(self) -> None:
        print("Meow")

# Here's an example of a class that inherits from both Dog and Cat
class DogCat(Dog, Cat):
    def __init__(self, name: str, breed: str, fur_color: str) -> None:
        super().__init__(name, breed)
        Cat.__init__(self, name, fur_color)

dogcat = DogCat("Fluffy", "Poodle", "White")
print(dogcat.name)  # prints "Fluffy"
print(dogcat.breed)  # prints "Poodle"
print(dogcat.fur_color)  # prints "White"
dogcat.make_sound()  # prints "Bark"

```
In the example above, the `DogCat` class inherits from both the `Dog` and `Cat` classes. It has access to all of the attributes and methods of both of these classes. When we create an instance of DogCat, it first calls the `__init__` method of the `Dog` class with the name and breed arguments, and then it calls the `__init__` method of the `Cat` class with the `name` and `fur_color` arguments.

When we call the `make_sound` method on a `DogCat` instance, it uses the implementation of the method that is defined in the `Dog` class, since the `Dog` class is listed before the `Cat` class in the inheritance list.

Multiple inheritance can be a powerful tool, but it can also make your code more complex and harder to understand, so you should use it with caution.
