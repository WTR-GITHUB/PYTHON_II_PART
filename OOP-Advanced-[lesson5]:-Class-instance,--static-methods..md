## Instance methods
As we already know, `Instance methods` in Python are **functions** that are bound to a class instance. **They can access and modify the state** of the instance and can also access the class itself. Here is an example of an instance method in Python:

```python
class Car:
    def __init__(self, make: str, model: str, year: int) -> None:
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    
    def update_odometer(self, mileage: int) -> None:
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            raise ValueError("You can't roll back an odometer!")
    
    def drive(self, miles: int) -> None:
        self.update_odometer(self.odometer_reading + miles)

```

In this example, we define a `Car` class with an **instance method** `update_odometer()` and `drive()`.  The `update_odometer()` method takes an argument mileage and updates the value of the `odometer_reading` attribute of the car. The `drive()` method takes an argument `miles` and `calls` the `update_odometer()` method to increment the `odometer_reading` attribute by the specified number of miles.

Additionally, in object-oriented programming (OOP), a class is a blueprint for creating objects that contain data and methods. When you create an instance of a class, you create an object that has its own state and behavior. An instance method is a function that is associated with an instance of a class and can access and modify the instance's state.

Instance methods in Python are defined within a class and take self as the first argument. self refers to the instance of the class on which the method is called. This allows instance methods to access and modify the instance's attributes.

To call an instance method on an object, you need to first create an instance of the class and then call the method on that instance:

```python
my_car = Car("Honda", "Civic", 2021)
my_car.drive(100)
print(f"My car's odometer reading is now {my_car.odometer_reading} miles.")

```

This will output: `My car's odometer reading is now 100 miles`.

## Static Methods 
**Static methods** in Python are methods that _are bound to a class rather than an instanc_e of the class. They don't require access to the instance or the class itself and don't modify the state of the class or instance. **They are typically used for utility functions** that don't depend on the state of the object.

Here's an example of a static method in Python:

```python
class MathUtils:
    @staticmethod
    def add(a: int, b: int) -> int:
        return a + b

```
In this example, we define a `MathUtils` class with a add **static method** that takes two integer arguments `a` and `b` and returns their sum. We use the `@staticmethod` decorator to indicate that this is a static method.

To call a static method on a class, you can use the class name:

```python
result = MathUtils.add(2, 3)
print(result)  # Output: 5
```

In this example, we call the add `static method` on the `MathUtils` class, passing `2` and `3` as arguments. The method returns their sum, which is stored in the variable result.

**Static methods can be called on both the class and its instances**. However, since they don't require access to the instance, _it's more common to call them on the class itself_.

Here's another example of a static method that calculates the area of a circle:

```python
class Circle:
    PI = 3.14159
    
    def __init__(self, radius: float) -> None:
        self.radius = radius
    
    def area(self) -> float:
        return Circle.calculate_area(self.radius)
    
    @staticmethod
    def calculate_area(radius: float) -> float:
        return Circle.PI * radius ** 2

```
In this example, we define a `Circle` class with a `calculate_area` static method that takes a radius argument and returns the area of a circle with that radius. We also define an `__init__` method that takes a radius argument and initializes the instance's radius attribute, and an area method that returns the area of the circle calculated by calling the `calculate_area` static method.

To create an **instance** of the `Circle class` and call its area method, we can do:

```python
circle = Circle(5)
print(circle.area())  # Output: 78.53975
```

In this example, we create an instance of the `Circle` class with radius of 5. We then call the `area` method on the **instance circle**, which returns the area of the circle calculated by calling the calculate_area static method.

To sum up, for static method: 
 - Must have @staticmethod built-in function decorator.
 - With static methods, neither self (the object instance) nor myClass (the class) is implicitly passed as the first argument. They behave like plain
   functions except that you can call them from an instance or the class. It does not have any specific argument.
 - A static method is also a method that is bound to the class and not the object of the class.
 - A static method can’t access or modify the class state.
 - Static methods know nothing about the class state. They are utility-type methods that take some parameters and work upon those parameters. On the 
   other hand class methods must have class as a parameter.


## Exercises: 

* Task Nr.1:  

  Create a class which takes temperature measurements in Kelvins and add static methods to transform those to Celsius and Fahrenheit units. Use 
  OOP abstraction. 


* Task Nr.2:
 
  Create a class that would take at least five `imperial system` measurements and would transform with the help of static methods to `metric` system 
  units.

* Task Nr.3:

  Create a class called `TimeUtils` that has a static method called `time_to_seconds` that takes a time string in the format `hh:mm:ss` and returns the 
  total number of seconds represented by that time. Use functional programing paradigm.

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