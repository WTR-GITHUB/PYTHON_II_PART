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

## OOP Advanced: Abstraction

### Task Nr. 1:

```python3
from abc import ABC, abstractmethod

class Animals(ABC):
    def __init__(self, name: str):
        self.name = name

    @abstractmethod
    def speak(self)-> str:
        pass

    def get_name(self)-> str:
        return self.name

class Dog(Animals):
    def speak(self)-> str:
        return f"Dog says Woof!"

class Cat(Animals):
    def speak(self)-> str:
        return f"Cat says Meow!"

dog = Dog("Bob")
cat = Cat("Tom")

print(dog.speak())
print(dog.get_name())
print(cat.speak())
print(cat.get_name())

```
### Task Nr. 2:

```python3

from abc import ABC, abstractmethod
from typing import Dict

class Money(ABC):
    def __init__(self, currency: str, value: float):
        self.currency = currency
        self.value = value
        
    def get_value(self) -> float:
        return self.value

    def get_currency(self) -> str:
        return self.currency
    
    @abstractmethod
    def convert_to_currency(self, target_currency: str, conversion_rate: Dict[str,float]) -> None:
        pass

class Cash(Money):
    def __init__(self, currency: str, value: float, denomination: int):
        super().__init__(currency, value)
        self.denomination = denomination

    def convert_to_currency(self, target_currency: str, conversion_rate: Dict[str,float]) -> None:
        self.value = round(self.value * conversion_rate[self.currency] * conversion_rate[target_currency],2)
        self.currency = target_currency
        for _ in range(int(self.value/self.denomination)):
            self.value -= self.denomination

class Card(Money):
    def __init__(self, currency: str, value: float, credit_limit: float):
        super().__init__(currency, value)
        self.credit_limit = credit_limit

    def convert_to_currency(self, target_currency: str, conversion_rate: Dict[str,float]) -> None:
        self.value = round(min(self.value, self.credit_limit) * conversion_rate[self.currency] * conversion_rate[target_currency],2)
        self.currency = target_currency

```

## OOP Advanced: Magic/Dunder methods.

### Task Nr. 1:

```python
class Product:
    def __init__(self, name: str, price: float):
        self.name = name
        self.price = price

    def __str__(self):
        return f"Product: {self.name}, Price: {self.price}"

    def __repr__(self):
        return f"Product('{self.name}', {self.price})"

p1 = Product("Apple", 0.5)
print(p1)  # Product: Apple, Price: 0.5
print(repr(p1)) # Product('Apple', 0.5)

```

### Task Nr. 2:

```python
class MyQueue:
    def __init__(self):
        self.items = []

    def __bool__(self):
        return bool(self.items)

    def __repr__(self):
        return f"MyQueue({self.items})"

    def __len__(self):
        return len(self.items)

q = MyQueue()
q.items.append(1)
q.items.append(2)
print(bool(q))  # True
print(repr(q)) # MyQueue([1, 2])
print(len(q)) # 2

```

### Task Nr. 3:

```python
class Book:
    def __init__(self, title:str, author:str, ISBN:str, pages: int):
        self.title = title
        self.author = author
        self.ISBN = ISBN
        self.pages = pages

    def __bool__(self):
        return bool(self.title)

    def __repr__(self):
        return f"Book({self.title}, {self.author}, {self.ISBN})"

    def __len__(self):
        return self.pages

    def __str__(self):
        return f"{self.title} by {self.author} ({self.ISBN})"

    def __eq__(self, other):
        if isinstance(other, Book):
            return (self.ISBN) == (other.ISBN)
        raise TypeError("unsupported operand type(s) for ==: 'Book' and '{}'".format(type(other).__name__))

    def __add__(self, other):
        if isinstance(other, Book):
            pages = self.pages + other.pages
            return Book(self.title, self.author+" and "+other.author, self.ISBN, pages)

    def __getitem__(self, index):
        if index == 0:
            return self.title
        elif index == 1:
            return self.author
        else:
            raise IndexError("Invalid index")

```

## OOP Advanced [lesson5]: Class instance,  static methods.

### Task Nr. 3:

```python
class TimeUtils:
    @staticmethod
    def time_to_seconds(time_str: str) -> int:
        hours, minutes, seconds = map(int, time_str.split(':'))
        return (hours * 60 * 60) + (minutes * 60) + seconds

print(TimeUtils.time_to_seconds("01:30:00")) # Output: 5400
print(TimeUtils.time_to_seconds("12:30:00")) # Output: 45000

```

### Task Nr. 4:

```python
class Employee:
    def __init__(self, name: str, salary: float) -> None:
        self.name = name
        self.salary = salary
    
    @staticmethod
    def calculate_payroll(employees: List["Employee"]) -> float:
        return sum(employee.salary for employee in employees)

employees = [Employee("Alice", 5000.0), Employee("Bob", 6000.0), Employee("Charlie", 7000.0)]
print(Employee.calculate_payroll(employees)) # Output: 18000.0
```

## OOP Advanced [lesson6]: Class methods.

### Task Nr. 1:

```python
class MathOperations:
    @classmethod
    def factorial(cls, n: int) -> int:
        if n == 0:
            return 1
        else:
            return n * cls.factorial(n-1)

print(MathOperations.factorial(5)) # Output: 120

```

### Task Nr. 2:

```python
class StringUtils:
    @classmethod
    def reverse(cls, s: str) -> str:
        return s[::-1]

print(StringUtils.reverse('Hello, world!')) # Output: '!dlrow ,olleH'
```

### Task Nr. 3:

```python
class MathOperations:
    @classmethod
    def is_prime(cls, n: int) -> bool:
        if n <= 1:
            return False
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0:
                return False
        return True

    @classmethod
    def primes(cls, n: int) -> List[int]:
        primes_list = []
        for i in range(2, n+1):
            if cls.is_prime(i):
                primes_list.append(i)
        return primes_list

print(MathOperations.primes(20)) # Output: [2, 3, 5, 7, 11, 13, 17, 19]

```

### Task Nr. 4:

```python
from typing import List


class Book:
    def __init__(self, title: str, author: str, isbn: str, num_copies: int) -> None:
        self.title = title
        self.author = author
        self.isbn = isbn
        self.num_copies = num_copies


class User:
    def __init__(self, name: str, email: str) -> None:
        self.name = name
        self.email = email
        self.books_borrowed: List[Book] = []


class LibrarySystem:
    books: List[Book] = []
    users: List[User] = []

    @classmethod
    def add_book(cls, book: Book) -> None:
        cls.books.append(book)

    @classmethod
    def register_user(cls, user: User) -> None:
        cls.users.append(user)

    @classmethod
    def borrow_book(cls, user: User, isbn: str) -> None:
        for book in cls.books:
            if book.isbn == isbn:
                if book.num_copies > 0:
                    book.num_copies -= 1
                    user.books_borrowed.append(book)
                    print(f"{user.name} has borrowed {book.title}.")
                    return
                else:
                    print("Sorry, no copies of this book are available.")
                    return
        print("Sorry, the book with the given ISBN is not available in the library system.")

    @classmethod
    def return_book(cls, user: User, isbn: str) -> None:
        for book in user.books_borrowed:
            if book.isbn == isbn:
                book.num_copies += 1
                user.books_borrowed.remove(book)
                print(f"{user.name} has returned {book.title}.")
                return
        print("Sorry, the user has not borrowed the book with the given ISBN.")

    @classmethod
    def list_books(cls) -> List[Book]:
        return cls.books

    @classmethod
    def list_users(cls) -> List[User]:
        return cls.users


book1 = Book("The Hobbit", "J.R.R. Tolkien", "1234", 5)
book2 = Book("Harry Potter and the Philosopher's Stone", "J.K. Rowling", "5678", 3)
LibrarySystem.add_book(book1)
LibrarySystem.add_book(book2)

user1 = User("John Doe", "johndoe@example.com")
user2 = User("Jane Doe", "janedoe@example.com")
LibrarySystem.register_user(user1)
LibrarySystem.register_user(user2)

LibrarySystem.borrow_book(user1, "1234")
LibrarySystem.borrow_book(user2, "5678")
LibrarySystem.borrow_book(user1, "5678")
LibrarySystem.borrow_book(user1, "9012")

LibrarySystem.return_book(user1, "1234")
LibrarySystem.return_book(user1, "5678")
LibrarySystem.return_book(user2, "5678")

books = LibrarySystem.list_books()
for book in books:
    print(f"{book.title} by {book.author}, ISBN: {book.isbn}, Copies available: {book.num_copies}")

users = LibrarySystem.list_users()
for user in users:
    print(f"{user.name} ({user.email}) has borrowed:")
    for book in user.books_borrowed:
        print(f"- {book.title} by {book.author}, ISBN: {book.isbn}")

```

## OOP Advanced [lesson8]: Dataclasses Part 1.

### Task Nr. 1:

```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class Product:
    id: int
    name: str
    description: Optional[str] = None
    price: float = 0.0
    quantity: int = 0

    def calculate_total_cost(self, num_items: int) -> float:
        if num_items <= 0:
            return 0.0
        elif num_items > self.quantity:
            return self.quantity * self.price
        else:
            return num_items * self.price

```

```python
# Create a Product instance
p = Product(1, "Apple", "A tasty fruit", 1.0, 10)

# Calculate the total cost of 5 Apples
total_cost = p.calculate_total_cost(5)
print(total_cost) # Output: 5.0

```

### Task Nr. 2:

```python
from dataclasses import dataclass
from typing import List

@dataclass
class Book:
    title: str
    author: str
    publication_year: int
    isbn: str

@dataclass
class Library:
    books: List[Book] = []

    def add_book(self, book: Book) -> None:
        self.books.append(book)

    def remove_book(self, isbn: str) -> bool:
        for i, book in enumerate(self.books):
            if book.isbn == isbn:
                del self.books[i]
                return True
        return False

    def search_by_title(self, title: str) -> List[Book]:
        return [book for book in self.books if book.title == title]

    def search_by_author(self, author: str) -> List[Book]:
        return [book for book in self.books if book.author == author]

    def display_books(self) -> None:
        for book in self.books:
            print(f"{book.title} by {book.author}, published in {book.publication_year}, ISBN: {book.isbn}")

```

```python
book1 = Book(title="The Great Gatsby", author="F. Scott Fitzgerald", publication_year=1925, isbn="9780141392461")
book2 = Book(title="To Kill a Mockingbird", author="Harper Lee", publication_year=1960, isbn="9780446310789")

library = Library()
library.add_book(book1)
library.add_book(book2)

library.display_books()

book3 = Book(title="Pride and Prejudice", author="Jane Austen", publication_year=1813, isbn="9780486284736")
library.add_book(book3)

print(library.search_by_title("To Kill a Mockingbird"))
print(library.search_by_author("F. Scott Fitzgerald"))

library.remove_book("9780446310789")

library.display_books()

#OUTPUT:
The Great Gatsby by F. Scott Fitzgerald, published in 1925, ISBN: 9780141392461
To Kill a Mockingbird by Harper Lee, published in 1960, ISBN: 9780446310789
[Pride and Prejudice by Jane Austen, published in 1813, ISBN: 9780486284736]
[The Great Gatsby by F. Scott Fitzgerald, published in 1925, ISBN: 9780141392461]
The Great Gatsby by F. Scott Fitzgerald, published in 1925, ISBN: 9780141392461
Pride and Prejudice by Jane Austen, published in 1813, ISBN: 9780486284736

```


## OOP Advanced [lesson10]: Property decorators, setters.

### Task Nr. 1:

```python3
class Temperature:
    def __init__(self, celsius: float):
        self._celsius = celsius

    @property
    def celsius(self) -> float:
        return self._celsius

    @celsius.setter
    def celsius(self, value: float) -> None:
        self._celsius = value

    @property
    def fahrenheit(self) -> float:
        return (self.celsius * 1.8) + 32

```

### Task Nr. 2:

```python3
import re

class User:
    def __init__(self, password: str):
        self._password = password

    @property
    def password(self) -> str:
        return self._password

    @password.setter
    def password(self, value: str) -> None:
        if not self.is_password_strong(value):
            raise ValueError("Password is not strong enough")
        self._password = value

    @staticmethod
    def is_password_strong(password: str) -> bool:
        if len(password) < 8:
            return False
        if not re.search(r"[a-z]", password):
            return False
        if not re.search(r"[A-Z]", password):
            return False
        if not re.search(r"\d", password):
            return False
        return True

```

## Mongo DB - lesson 2: PyMongo and CRUD operations

### Task Nr. 1:

```python
from pymongo import MongoClient
from pymongo.collection import Collection
from typing import Dict, Any

class LibraryManager:
    def __init__(self, host: str, port: int, db_name: str, collection_name: str):
        self.client = MongoClient(host, port)
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def add_book(self, book: Dict[str, Any]) -> str:
        result = self.collection.insert_one(book)
        return str(result.inserted_id)

    def get_all_books(self) -> List[Dict[str, Any]]:
        return list(self.collection.find())

    def get_book(self, book_id: str) -> Dict[str, Any]:
        return self.collection.find_one({"_id": book_id})

    def update_book(self, book_id: str, updates: Dict[str, Any]) -> bool:
        result = self.collection.update_one({"_id": book_id}, {"$set": updates})
        return result.modified_count > 0

    def delete_book(self, book_id: str) -> bool:
        result = self.collection.delete_one({"_id": book_id})
        return result.deleted_count > 0


```

### Task Nr. 2:
database.py: 

```python
from pymongo import MongoClient
from pymongo.database import Database

def get_database() -> Database:
    client = MongoClient('mongodb://localhost:27017/')
    return client['task_manager']
```

task_manager.py

```python
from typing import List, Dict, Any
from database import get_database
from pymongo.collection import Collection

def add_task(task: Dict[str, Any]) -> str:
    db = get_database()
    collection = db['tasks']
    result = collection.insert_one(task)
    return str(result.inserted_id)

def view_all_tasks() -> List[Dict[str, Any]]:
    db = get_database()
    collection = db['tasks']
    return list(collection.find())

def update_task_status(task_id: str, status: str) -> int:
    db = get_database()
    collection = db['tasks']
    result = collection.update_one({'_id': task_id}, {'$set': {'status': status}})
    return result.modified_count

def delete_task(task_id: str) -> int:
    db = get_database()
    collection = db['tasks']
    result = collection.delete_one({'_id': task_id})
    return result.deleted_count

```

cli.py: 

```python
from task_manager import add_task, view_all_tasks, update_task_status, delete_task
from typing import Dict, Any

def display_tasks(tasks: List[Dict[str, Any]]) -> None:
    print("TASKS:")
    for task in tasks:
        print(f"ID: {task['_id']}")
        print(f"Title: {task['title']}")
        print(f"Description: {task['description']}")
        print(f"Status: {task.get('status', 'N/A')}")
        print("------------------------")

def add_task_cli() -> None:
    title = input("Enter task title: ")
    description = input("Enter task description: ")
    task = {'title': title, 'description': description}
    task_id = add_task(task)
    print(f"Task added with ID: {task_id}")

def view_all_tasks_cli() -> None:
    tasks = view_all_tasks()
    display_tasks(tasks)

def update_task_status_cli() -> None:
    task_id = input("Enter task ID: ")
    status = input("Enter task status: ")
    count = update_task_status(task_id, status)
    print(f"{count} task(s) updated")

def delete_task_cli() -> None:
    task_id = input("Enter task ID: ")
    count = delete_task(task_id)
    print(f"{count} task(s) deleted")

def display_menu() -> None:
    print("TASK MANAGER MENU")
    print("1. Add Task")
    print("2. View All Tasks")
    print("3. Update Task Status")
    print("4. Delete Task")
    print("5. Exit")

def main() -> None:
    while True:
        display_menu()
        choice = input("Enter your choice (1-5): ")
        
        if choice == '1':
            add_task_cli()
       

```

## Mongo DB - lesson 3: Quering [Part1]

### Task Nr. 1: 

```python
from typing import List
from pymongo import MongoClient
from pymongo.collection import Collection

def filter_documents(collection: Collection, field_name: str, eq_value: str, ne_value: str) -> List[dict]:
    """
    Filters documents in a MongoDB collection based on field values using $eq and $ne operators.

    Args:
        collection: The MongoDB collection to filter.
        field_name: The name of the field to filter.
        eq_value: The equal value to match.
        ne_value: The not equal value to exclude.

    Returns:
        A list of documents that match the filter criteria.
    """
    query = {
        field_name: {
            "$eq": eq_value,
            "$ne": ne_value
        }
    }
    result = collection.find(query)
    return list(result)

```

