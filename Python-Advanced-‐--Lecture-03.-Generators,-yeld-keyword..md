## `Introduction`
In Python, a generator is a type of iterable, like lists or tuples. Unlike lists, they don't allow indexing with arbitrary indices, but they can still be iterated through with for loops. They can be created using functions and the yield keyword.

## `Overview`
Generators are a type of `iterable`, like lists or tuples. They do not store their contents in memory, but instead generate each value on the fly.

```python
def count_up_to(x):
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

In the above example, `count_up_to` is a generator that produces numbers up to a certain number. The `yield` keyword is used to produce a `value` and suspend the generator's execution.

## `yield keyword`
The yield keyword is used in Python to define a generator. It works like a standard return keyword. But it will return a generator.

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

In the above example, generator function generator() returns a generator object. You can iterate over the generator object using the for loop.

## `Generator Expressions`
Just as you can create a list comprehension, you can create generator expressions as well. These are more efficient than list comprehensions and can save memory if the resulting list is going to be large, because they generate each value on the fly rather than storing them in a list.

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

In the above example, numbers is a generator that generates numbers from 0 to 9. This is more memory-efficient than creating a list of these numbers.

## Exercises: 🧠
1) Write a Python program to create a generator that generates the squares of numbers up to a given number.
2) Write a Python program to create a generator that yields "n" random numbers between a low and high number that are inputs.
3) Write a Python program to create a generator that iterates over a string.
4) Write a Python program to create a Fibonacci series generator.
5) Write a Python program to create a generator from a list that yields item from the list if it is a number.

🌐 Extra reading:
Python Generators
Python yield keyword
[Python Generators](https://github.com/CodeAcademy-Online/python-new-material-level2/wiki/_new) vs List Comprehensions