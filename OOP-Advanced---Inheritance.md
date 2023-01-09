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

### MRO - Method Resolution Order

In Python, when a class inherits from multiple superclasses, it can be ambiguous which version of an attribute or method to use. To resolve this ambiguity, Python uses a mechanism called the **method resolution order (MRO)**.

The MRO is the order in which a class's attributes and methods are inherited from its `superclasses`. It determines which implementation of an attribute or method will be used when an instance of the class calls it.

Here's an example of how the MRO works in Python:

```python
from typing import Type

class A:
    def foo(self) -> None:
        print("A.foo")

class B(A):
    def foo(self) -> None:
        print("B.foo")

class C(A):
    def foo(self) -> None:
        print("C.foo")

class D(B, C):
    pass

d = D()
d.foo()  # prints "B.foo"

```

In the example above, the `D` class inherits from both the `B` and `C` classes. The `foo` method is defined in both the `B` and `C` classes, so it is ambiguous which one to use.

To determine the `MRO` for the `D` class, Python follows these steps:

1. It starts with the `D` class and adds it to the MRO list.
2. It looks at the first superclass of `D`, which is `B`. It adds `B` to the MRO list, and then repeats this process with `B's` superclass, `A`.
3. It looks at the second superclass of `D`, which is `C`. It adds `C` to the MRO list, and then repeats this process with `C's` superclass, `A`.
4. It removes any duplicate classes from the MRO list. In this case, it removes the second instance of `A`, since it has already been added to the list.

The resulting MRO for the `D` class is `[D, B, A, C]`. This means that when we call the foo method on an instance of `D`, it will use the implementation of the foo method that is defined in the `B` class.

You can use the `__mro__` attribute of a class to see its MRO:

```python
print(D.__mro__)  
# prints (<class '__main__.D'>, <class '__main__.B'>, <class '__main__.A'>, <class '__main__.C'>)

```
