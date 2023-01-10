## OOP Advanced : Inheritance
### Task Nr.1
```python
class Shape:
    def __init__(self, name: str, sides: int) -> None:
        self.name = name
        self.sides = sides
    
    def area(self) -> float:
        raise NotImplementedError

class Rectangle(Shape):
    def __init__(self, width: float, height: float) -> None:
        super().__init__("Rectangle", 4)
        self.width = width
        self.height = height
    
    def area(self) -> float:
        return self.width * self.height

class Square(Rectangle):
    def __init__(self, side_length: float) -> None:
        super().__init__(side_length, side_length)
        self.side_length = side_length

square = Square(5)
print(square.name)  # prints "Rectangle"
print(square.sides)  # prints 4
print(square.area())  # prints 25

```

### Task Nr.3
```python

class Animal:
    def __init__(self, name: str):
        self.name = name

    def make_noise(self) -> None:
        print("Some generic animal noise")

class Mammal(Animal):
    def __init__(self, name: str, warm_blooded: bool):
        super().__init__(name)
        self.warm_blooded = warm_blooded

    def give_birth(self) -> None:
        print("Giving birth to a baby mammal")

class Primate(Mammal):
    def __init__(self, name: str, warm_blooded: bool, opposable_thumbs: bool):
        super().__init__(name, warm_blooded)
        self.opposable_thumbs = opposable_thumbs

    def swing(self) -> None:
        print("Swinging through the trees")

chimpanzee = Primate("Charlie", True, True)
print(chimpanzee.name)
print(chimpanzee.warm_blooded)
print(chimpanzee.opposable_thumbs)
chimpanzee.make_noise()
chimpanzee.give_birth()
chimpanzee.swing()

```

## OOP Advanced: method chaining & super function

### Task Nr. 1

```python
class Person:
    def __init__(self, name: str, age: int) -> None:
        self.name = name
        self.age = age

    def set_name(self, name: str) -> 'Person':
        self.name = name
        return self

    def set_age(self, age: int) -> 'Person':
        self.age = age
        return self

p = Person("John", 25)
p.set_name("Jhon Doe").set_age(30)

print(p.name) # output: Jhon Doe
print(p.age) # output: 30

```
### Task Nr. 3:

```python
class Animals:
    def speak(self) -> None:
        print("Animals can't speak")
    
class Dogs(Animals):
    def speak(self) -> None:
        print("Woof woof")

class Cats(Animals):
    def speak(self) -> None:
        super().speak()
        print("Meow meow")
        
dog = Dogs()
dog.speak() # Output: "Woof woof"
cat = Cats()
cat.speak() # Output: "Animals can't speak" and "Meow meow"
```

### Task Nr. 4:

```python
class Person:
    def __init__(self, name:str, age:int):
        self.name = name
        self.age = age
    
    def get_name(self) -> str:
        return self.name

    def get_age(self) -> int:
        return self.age

    def __str__(self) -> str:
        return f"{self.name} is {self.age} years old."
    
class Student(Person):
    def __init__(self, name:str, age:int, student_id:int, major:str):
        super().__init__(name, age)
        self.student_id = student_id
        self.major = major

    def get_student_id(self) -> int:
        return self.student_id

    def get_major(self) -> str:
        return self.major

    def __str__(self) -> str:
        return f"{super().__str__()} is a student of {self.major} major. Student id: {self.student_id}."

class GraduateStudent(Student):
    def __init__(self, name:str, age:int, student_id:int, major:str, program:str, advisor:str):
        super().__init__(name, age, student_id, major)
        self.program = program
        self.advisor = advisor

    def get_program(self) -> str:
        return self.program

    def get_advisor(self) -> str:
        return self.advisor

    def __str__(self) -> str:
        return f"{super().__str__()} program: {self.program} and advisor: {self.advisor}."

```