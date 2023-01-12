## Magic Methods

In Python, _"magic methods"_ or _"dunder methods"_ are special methods that have **double underscores** at the beginning and end of their names (e.g. `__init__`, `__add__`). These methods are used to define the behavior of certain operations on objects of a class. For example, the `__add__` method is called when the `+` operator is used on objects of a class, and the `__init__` method is called when a new object of a class is created. By defining these methods in a class, you can customize the behavior of built-in operations for instances of that class. We will cover only some of them, the full list can be found [here](https://docs.python.org/3/reference/datamodel.html).

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

### `__add__` :

The `__add__` is used to define the behavior of the addition operator `+` for a custom object. It is called when the `+` operator is used to **add two objects of the same class** and should return a new object that **represents the result of the addition**.

Here is an example of how to use the `__add__` method to define the addition for a custom object called `Vector`:

```python
class Vector:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    def __add__(self, other: 'Vector') -> 'Vector':
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        raise TypeError("unsupported operand type(s) for +: 'Vector' and '{}'".format(type(other).__name__))

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3.x, v3.y) # 4 6

```
It's important to note that when adding custom objects, it is also a good practice to implement the `__radd__` method that allow the commutativity of the addition operation. This method is called when an object of a **different class** is the left operand, and the right operand is an instance of the class that implements the `__add__` method:

```python3
class Vector:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    def __add__(self, other: 'Vector') -> 'Vector':
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        raise TypeError("unsupported operand type(s) for +: 'Vector' and '{}'".format(type(other).__name__))
    
    def __radd__(self, other: 'Vector') -> 'Vector':
        return self.__add__(other)

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2
print(v3.x, v3.y) # 4 6
v4 = 2 + v1
print(v4.x, v4.y) # 3 4

```
### `__len__` :

The `__len__` is used to define the behavior of the built-in `len()` function for a custom object. It **should return an integer** that represents the number of elements in the object.

Here is an example of how to use the `__len__` method to define the length of a custom object called `MyList`:

```python
class MyList:
    def __init__(self, items: list):
        self.items = items

    def __len__(self) -> int:
        return len(self.items)

ml = MyList([1, 2, 3, 4, 5])
print(len(ml)) # 5

```

It's worth to mention that the `__len__` method **should always return a non-negative integer**, if it returns a negative or non-integer value, a `TypeError` will be raised.


### `__bool__` :

The `__bool__` is used to define the behavior of the built-in `bool()` function and the _boolean value_ of a custom object. **It should return True if the object is considered "truthy" and False if it is "falsy".**

Here is an example of how to use the `__bool__` method to define the `boolea`n value of a custom object called `MyNumber`:

```python
class MyNumber:
    def __init__(self, num: int):
        self.num = num

    def __bool__(self):
        return bool(self.num)

mn = MyNumber(5)
print(bool(mn)) # True
mn2 = MyNumber(0)
print(bool(mn2)) # False

```
It's worth to mention that if the `__bool__` method is not defined, Python will use the `__len__` method to determine the `boolean value` of the object. If `__len__` **returns 0**, the object is considered to be `False`, otherwise, it is considered to be `True`.

```python
class MyNumber:
    def __init__(self, num: int):
        self.num = num

    def __bool__(self):
        return bool(self.num)
    
    def __len__(self) -> int:
        return 1

mn = MyNumber(5)
print(bool(mn)) # True
mn2 = MyNumber(0)
print(bool(mn2)) # False
print(len(mn)) # 1

```

### `__getitem__` :

The `__getitem__` is used to define the behavior of the square bracket notation `[]` for a custom object. It is called when the `square brackets []` are used to **access an element of the object and should return the element at the specified index or key**.

Here is an example of how to use the `__getitem__` method to define the element access for a custom object called `MyDict`:

```python
class MyDict:
    def __init__(self, data: dict):
        self.data = data

    def __getitem__(self, key: str):
        return self.data[key]

md = MyDict({'a':1, 'b':2})
print(md['a']) # 1

```
It's worth to mention that if the `__getitem__` method raises a `KeyError` when the **key does not exist in the object**, it's good practice to implement the `__missing__` method for the class that inherits from the built-in `dict` class. This method is called by the `dict` class **when a key is not found in the dictionary and should return the default value for the key**.

```python3
class MyDict(dict):
    def __missing__(self, key: str):
        return 'default'
    
md = MyDict({'a':1, 'b':2})
print(md['a']) # 1
print(md['c']) # default

```

## Exercises: 
🧠 : Repeat the [OOP Part 2](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-19:-OOP-(-Part-2))

* **Task Nr.1**:
  
  Create a class called `Product` that takes a `name` and `price` as parameters and has `__str__` and `__repr__` methods defined.

  - The `__str__` method should return a string in the format "Product: name, Price: price"
  - The `__repr__` method should return a string in the format "Product('name', price)"
  

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-1-2) 

* **Task Nr.2**:

  Create a class called `MyQueue` that has `__bool__`, `__repr__` and `__len__` methods defined.

  - The `__bool__` method should return `True` if the queue has any items and `False` if it is empty.
  - The `__repr__` method should return a string in the format `MyQueue(items)` where items is the list of items in the queue.
  - The `__len__` method should return the number of items in the queue.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-2-1)

* **Task Nr.3**:

  Create a class called `Book` that takes `title`, `author`, and `ISBN` as parameters. The class should have `__bool__`, `__repr__`, `__len__`, 
  `__str__`, `__eq__`, `__add__`, and `__getitem__` methods defined.

  - The `__bool__` method should return True if the book has a title, False otherwise.
  - The `__repr__` method should return a string in the format "Book(title, author, ISBN)" where title, author and ISBN are the respective attributes of 
    the class
  - The `__len__` method should return the number of pages of the book
  - The `__str__` method should return a string in the format "title by author (ISBN)"
  - The `__eq__` method should compare two books and return True if both ISBN are the same and False otherwise.
  - The `__add__` method should add two books and return a new book object that contains the contents of both books concatenated and the title of the new 
    book should be the title of the first book
  - The `__getitem__` method should return the title of the book if the index passed is 0, and the author of the book if the index passed is 1.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3) 

* **Task Nr.4**: 

  Create three different task with real world scenario what would include all magic methods we covered today and plus 3 others from the provided [list](https://docs.python.org/3/reference/datamodel.html). 

## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [Corey Schafer: Magic methods](https://www.youtube.com/watch?v=3ohzBxoFHAY)
* [DataCamp](https://www.datacamp.com/tutorial/introducing-python-magic-methods)

***