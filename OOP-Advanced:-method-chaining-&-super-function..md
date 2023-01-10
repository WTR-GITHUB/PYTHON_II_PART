## Method Chaining 

Method chaining is a technique in which _multiple method calls are chained together_ in a **single statement**, using the output of one method as the input for the next method. This can make code more concise and readable, as well as making it easy to chain together operations that need to be performed on an object.

Here's an example of method chaining in Python:

```python
class MyString:
    def __init__(self, value: str):
        self.value = value

    def add_exclamation(self) -> 'MyString':
        self.value += "!"
        return self

    def make_upper(self) -> 'MyString':
        self.value = self.value.upper()
        return self

my_string = MyString("hello")
my_string.add_exclamation().make_upper()

print(my_string.value) # output: "HELLO!"

```
In this example, we have a `MyString` class with two methods: `add_exclamation` and `make_upper`. Both of these methods return `self`, which allows us to chain the calls together. The `add_exclamation` method modifies the value of the `MyString` object by adding an exclamation point to it, and the `make_upper` method modifies the value by converting it to upper case.

We create an instance of `MyString` with the value `hello`, and then call `add_exclamation` and `make_upper` on it in one statement. This results in the value of the `MyString` object being modified to `HELLO!`.

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