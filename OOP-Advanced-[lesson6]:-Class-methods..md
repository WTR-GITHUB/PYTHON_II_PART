## Class methods

Python’s `classmethod()` function is a powerful tool that allows developers to **manipulate class-level data** in a clean and efficient way. With its ability to create _factory methods, alternative constructors, manage class-level state, and implement class-level operations_, `classmethod()` provides a flexible and elegant solution to many programming challenges. We will explore how to use `classmethod()` in Python to improve your code’s organization and readability. Using `classmethod()` will enhance your Python skills and make your code more efficient and maintainable.

### What is `classmethod()` in Python?

`classmethod()` is a built-in function in Python that is used to define a **method that operates on the class instead of the instance of the class**. It is used to create a method that **can be called directly on the class**, rather than on an instance of the class. This means that the method can be used to manipulate class-level data or perform operations that are not specific to any one instance of the class.
The syntax of `classmethod()` is as follows:

```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1: Any, arg2: Any, ...) -> cls
        # code here
```
The `classmethod()` function is applied as a decorator to a method of a class. The first argument of a class method **is always the class itself**, represented by the parameter `cls`. This allows the method to access and modify class-level data.

###  Why use `classmethod()`?

The main benefit of using `classmethod()` is that it allows you to define methods that operate on the class itself, rather than on an instance of the class. This can be useful in a variety of situations, such as:
- **Creating factory methods**– `classmethods` can be used to create factory methods that create and return new instances of a class with a specific configuration:

```python
import datetime

class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name: str, birth_year: int) -> 'Person':
        age = cls.get_age(birth_year)
        return cls(name, age)

    @staticmethod
    def get_age(birth_year: int) -> int:
        return datetime.date.today().year - birth_year

person: Person = Person.from_birth_year('John', 1990)
print(person.name)  # John
print(person.age)  # 33

```
In this example, the `from_birth_year()` class method acts as a **factory method** that creates a new `Person` instance from a birth year. It calculates the age of the person using a static method `get_age()` and returns a new instance of the `Person` class.

- **Creating alternative constructors** – `classmethods` can be used to **create alternative constructors** for a class. This is useful when you want to create instances of a class with different sets of arguments: 

```python
class Point:
    def __init__(self, x: float, y: float):
        self.x = x
        self.y = y

    @classmethod
    def from_tuple(cls, point_tuple: tuple[float, float]) -> 'Point':
        x, y = point_tuple
        return cls(x, y)

point: Point = Point.from_tuple((3, 4))
print(point.x)  # 3
print(point.y)  # 4

```
In this example, the `rom_tuple()` class method acts as an **alternative constructor** that creates a new `Point` instance from a tuple of `(x, y)` values. It returns a new instance of the Point class.

- **Managing class-level state** – `classmethods` can be used to manage class-level state. This means that you can define a method that modifies or accesses a variable that is shared by all instances of the class:

```python
class Car:
    total_cars_sold: int = 0

    def __init__(self, make: str, model: str):
        self.make = make
        self.model = model
        Car.total_cars_sold += 1

    @classmethod
    def get_total_cars_sold(cls) -> int:
        return cls.total_cars_sold

car1: Car = Car('Toyota', 'Camry')
car2: Car = Car('Honda', 'Civic')

print(Car.get_total_cars_sold())  # 2

```
In this example, the `total_cars_sold` class-level variable is incremented every time a new instance of the `Car` class is created. The `get_total_cars_sold()` class method returns the current value of the `total_cars_sold` variable.

- **Implementing class-level operations** – `classmethods` can be used to implement class-level operations, such as sorting or filtering a list of instances of the class:

```python
class Student:
    all_students: list['Student'] = []

    def __init__(self, name: str, grade: float):
        self.name = name
        self.grade = grade
        Student.all_students.append(self)

    @classmethod
    def get_highest_grade(cls) -> 'Student':
        return max(cls.all_students, key=lambda student: student.grade)

    @classmethod
    def get_lowest_grade(cls) -> 'Student':
        return min(cls.all_students, key=lambda student: student.grade)

student1: Student = Student('John', 90)
student2: Student = Student('Jane', 95)
student3: Student = Student('Alice', 80)

print(Student.get_highest_grade().name)  # Jane
print(Student.get_lowest_grade().name)  # Alice

```
 The `all_students` attribute is declared as a class-level list that holds `Student` objects. The name attribute of the `Student` instances is declared as a string, and the grade attribute is declared as a float. The `get_highest_grade` and `get_lowest_grade` class methods return the `Student` object with the highest and lowest grade, respectively. The `student1`, `student2`, and `student3` instances are explicitly annotated with the `Student` class.


## Exercises: 

* Task Nr.1:  

  Create a class which takes temperature measurements in `Kelvins` and add static methods to transform those to `Celsius` and `Fahrenheit` units. Use 
  OOP abstraction. 


* Task Nr.2:
 
  Create a class that would take at least five `imperial system` measurements and would transform with the help of static methods to `metric` system 
  units.

* Task Nr.3:

  Create a class called `TimeUtils` that has a static method called `time_to_seconds` that takes a time string in the format `hh:mm:ss` and returns the 
  total number of seconds represented by that time. Use **functional programing paradigm**.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-3-2) 

* Task Nr.4: 

  Create a class called `Employee` with a static method called `calculate_payroll` that takes a list of `Employee` instances and returns the total amount 
  to be paid to all employees. Each `Employee` instance has two attributes: `name` and `salary`.

  [Answer](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/Z:-Exercise-answers.#task-nr-4-1) 


## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [RealPhyton](https://realpython.com/instance-class-and-static-methods-demystified/)
***