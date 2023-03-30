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

To call an instance method on an object, you need to first create an instance of the class and then call the method on that instance:

```python
my_car = Car("Honda", "Civic", 2021)
my_car.drive(100)
print(f"My car's odometer reading is now {my_car.odometer_reading} miles.")

```

This will output: My car's odometer reading is now 100 miles.
## Exercises: 


## 🌐  Extra reading (or watching 📺 ):

* [Full OOP course - Youtube](https://www.youtube.com/watch?v=Ej_02ICOIgs)
* [Corey Schafer: Python OOP Tutorial (multiple videos)](https://www.youtube.com/watch?v=ZDa-Z5JzLYM)
* [QuanticDev - method chaining](https://quanticdev.com/articles/method-chaining/)
* [RealPhyton - super() function](https://quanticdev.com/articles/method-chaining/)
***