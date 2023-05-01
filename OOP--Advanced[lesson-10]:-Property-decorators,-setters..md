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

### How to Use the Property Decorator?

Let’s implement the `Student` class like this:

```python3
class Student:
    def __init__(self):
        self._score: int = 0

    @property
    def score(self) -> int:
        return self._score

    @score.setter
    def score(self, s: int) -> None:
        if 0 <= s <= 100:
            self._score = s
        else:
            raise ValueError('The score must be between 0 ~ 100!')

    @score.deleter
    def score(self) -> None:
        del self._score

Tom = Student()
Tom.score = 999
# ValueError: The score must be between 0 ~ 100!
```

As the above code shown, after using the `@property` decorator, we can both `set` the value directly and ensure the validity of it. The **property decorator** is a very useful and widely used mechanism in Python classes. It helps us call the `getter`, `setter` and `deleter` methods directly by the attribute.

A common template for using the property decorator is:

```python3
class C(object):

    @property
    def x(self):
        return self._x

    @x.setter
    def x(self, value):
        self._x = value

    @x.deleter
    def x(self):
        del self._x
```

Note: **The names of getter, setter and deleter methods should be the same. The best choice is to use the attribute’s name.**

### Define a Read-only Attribute

As we known, there are three methods (getter, setter and deleter) we can define by the property decorator. If one of the three methods is not defined, **we cannot use this method**. Therefore, we can skillfully use the property decorator _to define a read-only attribute_. For example:

```python3
class Student:
    def __init__(self):
        self._score = 0

    @property
    def score(self):
        return self._score

    @score.deleter
    def score(self):
        del self._score



Tom= Student()
Tom.score = 99
# AttributeError: can't set attribute
```

As the above example shown, we don’t define the `setter` method of `score` , so `score` **can’t be set.** In other words, it’s a `read-only` attribute. **This is an important usage scenario of the property decorator**.

## Exercises: 

* Task Nr.1:  
  Write a `Temperature class` that has a `celsius` property and a `fahrenheit` property. The `celsius` property stores the temperature in `Celsius`, and 
  the fahrenheit property stores the temperature in `Fahrenheit`. The `fahrenheit` property should be a computed property that converts the `Celsius` 
  temperature to `Fahrenheit`.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-5) 


* Task Nr.2 :
  Write a `User` class that has a `password` property. The `password` property should be a computed property that checks whether the password is strong 
  enough. A `password` is considered strong if it has at least 8 characters, contains at least one uppercase letter, one lowercase letter, and one 
  number.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-4) 
 
## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Real Python](https://realpython.com/python-property/)
***