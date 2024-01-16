## `Introduction`
In Python, a `generator` is a special type of `iterable` **that produces a sequence of values one at a time**. This is in contrast to a `list`, **which stores all of its values in memory at once**. Generators are more **memory-efficient**, as they only produce the `values` that are **actually needed**. This can be useful for large or infinite sequences of data.

`Generators` are created using a `yield` statement. The yield statement is similar to the `return` statement, but it instead **suspends execution of the function and returns a value**. The next time the function is called, execution resumes from where it left off.

### `Overview`
Generators are a type of `iterable`, like `lists` or `tuples`. They **do not store their contents in memory**, but instead generate each value on the fly.

Simple generator expression: 

```python
from typing import Generator

def simple_generator(n: int) -> Generator[int, None, None]:
    for i in range(n):
        yield i

# Usage
for value in simple_generator(5):
    print(value)
```
Infinite Range Generator:

```python
from typing import Generator

def infinite_range(start: int = 0) -> Generator[int, None, None]:
    current = start
    while True:
        yield current
        current += 1

# Usage
counter = 0
for value in infinite_range(10):
    print(value)
    counter += 1
    if counter == 5:
        break

```

Another example: 

```python
def count_up_to(x: int) -> Generator[int, None, None]:
    count = 1
    while count <= x:
        yield count
        count += 1

for number in count_up_to(5):
    print(number)
# 1
# 2
# 3
# 4
# 5
```

In the above example, `count_up_to` is a `generator` that produces numbers up to a certain number. The `yield` keyword is used to produce a `value` and suspend the generator's execution.

In the `typing` module of Python, the `Generator` type is used to annotate `generator` functions. Here's the definition of `Generator` in the `typing' module:

```python
typing.Generator[ValueType, SendType, ReturnType]
```

 - `ValueType`: Type of values yielded by the generator (yield expressions).
 - `SendType`: Type of values that can be sent into the generator using the `generator.send(value)` method. This is optional and defaults to `None`.
 - `ReturnType`: Type of the value returned by the generator when it's exhausted (`raises StopIteration`). This is optional and defaults to `None`.

### `yield keyword`
The `yield` keyword is used in Python to define a `generator`. It works like a standard `return` keyword. But it will **return a generator**.

```python
def generator():
    yield 1
    yield 2
    yield 3

for value in generator():
    print(value)
# 1
# 2
# 3
```

In the above example, generator function `generator()` returns a `generator object`. You can `iterate` over the `generator object` using the `for` loop.

### `Generator Expressions`
Just as you can create a `list comprehension`, you can create `generator expressions` as well. These are more efficient than `list comprehensions` and can save memory if the resulting `list` is going to be **large**, because they generate each value on the fly rather than storing them in a list.

```python
numbers = (x for x in range(10))

for number in numbers:
    print(number)
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
```

In the above example, numbers is a `generator` that generates numbers from `0` to `9`. This is more memory-efficient than creating a `list` of these numbers.

## Exercises: 🧠
1) Write a Python program to create a generator that generates the `squares` of numbers up to a given number.
2) Write a Python program to create a generator that yields "n" random numbers between a `low` and `high` number that are `inputs`.
3) Write a Python program to create a generator that iterates over a `string`.
4) Write a Python program to create a `Fibonacci` series generator.
5) Write a Python program to create a generator from a `list` that yields item from the `list` if it is a `number`.
6) Create a `list` of `tuples`, each representing a person's information. Each `tuple` contains the following information: (name: str, age: int, city: 
 str, salary: float). Your task is to create Python generators to perform the following tasks:

 - Filtering Generator: Create a generator function that filters the people who are below a certain age threshold.
 - Mapping Generator: Create a generator function that maps the names of people to uppercase.
 - Aggregation Generator: Create a generator function that calculates the average salary of the selected group.

## 🌐  Extra reading (or watching 📺 ):

* [Real Phyton](https://realpython.com/introduction-to-python-generators/)
* [Youtube](https://www.youtube.com/watch?v=bD05uGo_sVI&ab_channel=CoreySchafer)
***