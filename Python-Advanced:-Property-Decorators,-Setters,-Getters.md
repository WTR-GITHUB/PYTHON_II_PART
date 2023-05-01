## Introduction

In object-oriented programming, each attribute of a class may have three basic methods:

* A `getter` method to get its value.
* A `setter` method to set its value.
* A `deleter` method to delete it.

In Python, properties are a way to control access to class attributes. The `@property` decorator can be used to define a `getter` method, which retrieves the value of an attribute, and the` @propertyname.setter` decorator can be used to define a setter method, which sets the value of an attribute. This allows for more control over the behavior of attributes, while still maintaining a simple, easy-to-use interface for the class user.

Here's an example of how to use the @property decorator to define a getter method:

```python3
class Rectangle:
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height

    @property
    def area(self) -> float:
        return self.width * self.height

r = Rectangle(3.0, 4.0)
print(r.area)  # output: 12.0

```
In this example, we define a class `Rectangle` with two attributes, `width` and `height`. We then use the `@property` decorator to define a getter method called area, which calculates the area of the rectangle by multiplying the `width` and `height` attributes. We can then use `r.area` to retrieve the area of the rectangle, without having to call a separate method.

## Exercises: 

* Task Nr.1:  


* Cafeteria project :
 
## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
***