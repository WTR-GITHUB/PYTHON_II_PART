## `Continue`

### `Map function`

The first function on the docket is `map()`, which is a `Python` built-in function. With `map()`, you can apply a function to each element in an `iterable` in turn, and `map()` will return an `iterator` that `yields` the results. This can allow for some very concise code because a `map()` statement can often take the place of an explicit `loop`.

Syntax:

```python
map(<f>, <iterable>)
```

Let's revisit our function:
```python
def reverse(s):
    return s[::-1]

reverse("I am a string")
```

If you have a `list` of `strings`, then you can use `map()` to apply `reverse()` to each element of the list:


```python
animals = ["cat", "dog", "hedgehog", "gecko"]
iterator = map(reverse, animals)
iterator
# <map object at 0x7fd3558cbef0>
```


**NOTE** ❗ ❗ ❗ But remember, `map()` doesn’t return a list. It returns an `iterator` called a `map object`. To obtain the values from the `iterator`, **you need to either iterate over it** or use `list()`:

```python
animals = ["cat", "dog", "hedgehog", "gecko"]
def reverse(s):
    return s[::-1]

iterator = map(reverse, animals)
for i in iterator:
    print(i)
# tac
# god
# gohegdeh
# okceg

iterator = map(reverse, animals)
list(iterator)

```


Let's take it further once more, we already know that `lambdas` give us a function, let's try passing it to map function:

```python
animals = ["cat", "dog", "hedgehog", "gecko"]
iterator = map(lambda s: s[::-1], animals)
list(iterator)
# ['tac', 'god', 'gohegdeh', 'okceg']
```

Let's even do it a more compact way:

```python
list(map(lambda s: s[::-1], ["cat", "dog", "hedgehog", "gecko"]))
# ['tac', 'god', 'gohegdeh', 'okceg']
```

If the `iterable` contains something that is not suitable for a certain operation:

```python
list(map(lambda s: s[::-1], ["cat", "dog", 3.14159, "gecko"]))
# Traceback (most recent call last):
#  File "<stdin>", line 1, in <module>
#  File "<stdin>", line 1, in <lambda>
# TypeError: 'float' object is not subscriptable
```

In this case, the lambda function expects a string argument, which it tries to slice. The second element in the list, `3.14159`, is a `float` object, which isn’t sliceable. So a `TypeError` occurs.


## `Calling map with multiple iterables`

```python
map(<f>, <iterable₁>, <iterable₂>, ..., <iterableₙ>)
```

The number of <iterable> arguments specified to `map()` must match the number of arguments that <f> expects. <f> acts on the first item of each <iterable>, and that result becomes the first item that the return iterator `yields`. Then <f> acts on the second item in each <iterable>, and that becomes the second yielded item, and so on.

```python
def f(a, b, c):
    return a + b + c


list(map(f, [1, 2, 3], [10, 20, 30], [100, 200, 300]))
# [111, 222, 333]
```
Here is more visual representation of how the calculation is being done:
![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/map.webp)



## `filter function`

`filter()` a**llows you to select or filter items** from an `iterable` based on evaluation of the given function. It’s called as follows:

```python
filter(<f>, <iterable>)
```


`filter(<f>, <iterable>)` applies function <f> to each element of <iterable> and returns an `iterator` that `yields` all items for which <f> is `truthy`. Conversely, it filters out all items for which <f> is `falsy`.

```python
def greater_than_100(x):
    return x > 100

list(filter(greater_than_100, [1, 111, 2, 222, 3, 333]))
# [111, 222, 333]
```

As we see that function is the first argument, let's try applying `lambdas` function here.


```python
list(filter(lambda x: x > 100, [1, 111, 2, 222, 3, 333]))
```

What is more we can even combine there things with `range()` function - `range(n)` produces an `iterator` that yields the `integers` from `0` to `n - 1`. The following example uses `filter()` to select only the even numbers from the `list` and filter out the `odd` numbers:


```python
list(range(10))
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
def is_even(x):
    return x % 2 == 0

list(filter(is_even, range(10)))
# [0, 2, 4, 6, 8]

list(filter(lambda x: x % 2 == 0, range(10)))
# [0, 2, 4, 6, 8]

```

Can we do that with strings as well? As long as we have  a correct function that returns `True` or `False` based on string input - Yes!

```python
animals = ["cat", "Cat", "CAT", "dog", "Dog", "DOG", "emu", "Emu", "EMU"]

def all_caps(s):
    return s.isupper()

list(filter(all_caps, animals))
# ['CAT', 'DOG', 'EMU']

list(filter(lambda s: s.isupper(), animals))
# ['CAT', 'DOG', 'EMU']
```


## `Reduce function`

`reduce()` applies a function to the items in an `iterable` two at a time, progressively combining them to produce a single result.

To use `reduce()`, you need to import it from a module called `functools`. This is possible in several ways, but the following is the most straightforward:


```python
from functools import reduce
```

## `Calling reduce with two arugments`:

```python
reduce(<f>, <iterable>)
```

reduce(<f>, <iterable>) uses <f>, which must be a function that takes exactly two arguments, to progressively combine the elements in <iterable>. To start, `reduce()` invokes <f> on the first two elements of <iterable>. That result is then combined with the third element, then that result with the fourth, and so on until the list is exhausted. Then `reduce()` returns the final result.

Let's start with some simple examples:


```python
def f(x, y):
    return x + y


from functools import reduce
reduce(f, [1, 2, 3, 4, 5])
# 15
```

Here is a representation of what is happening behind the scenes when `reduce` is called:

![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/reduce.webp)

reduce is quite disliked function even by the python creator Guido van Rossum:

_So now reduce(). This is actually the one I’ve always hated most, because, apart from a few examples involving + or *, almost every time I see a reduce() call with a non-trivial function argument, I need to grab pen and paper to diagram what’s actually being fed into that function before I understand what the reduce() is supposed to do. So in my mind, the applicability of reduce() is pretty much limited to associative operators, and in all other cases it’s better to write out the accumulation loop explicitly. ([Source](https://www.artima.com/weblogs/viewpost.jsp?thread=98196))_

Even in our example we can see that there are simpler ways of doing our simple example.

The most simple one would probably be:
```python
sum([1, 2, 3, 4, 5])
```

Now let's use multiplication operator (*) to find a factorial of some number. [What is a factorial](https://www.mathsisfun.com/numbers/factorial.html)

```python
def multiply(x, y):
    return x * y


def factorial(n):
    from functools import reduce
    return reduce(multiply, range(1, n + 1))


factorial(4)  # 1 * 2 * 3 * 4

factorial(6)  # 1 * 2 * 3 * 4 * 5 * 6
```


Yet there is a quite simpler example on how to do this:
```python
from math import factorial

factorial(4)

factorial(6)
```


We could also use `reduce` to get the same result as `max()` does:

```python
max([23, 49, 6, 32])


def greater(x, y):
    return x if x > y else y


from functools import reduce
reduce(greater, [23, 49, 6, 32])
```

## `Calling reduce() with initial value`

```python
reduce(<f>, <iterable>, <init>)
```

When present, <init> specifies an `initial value` for the combination. In the first call to <f>, the arguments are <init> and the first element of <iterable>. That result is then combined with the second element of <iterable>, and so on:
```python
def f(x, y):
    return x + y


from functools import reduce
reduce(f, [1, 2, 3, 4, 5], 100)  # (100 + 1 + 2 + 3 + 4 + 5)
```

The graphical visualization of the actions taken:


![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/reduce2.webp)


As you’ve seen in the above examples, even in cases where you can accomplish a task using `reduce()`, it’s often possible to find a more straightforward and `Pythonic` way to accomplish the same task without it. Maybe it’s not so hard to imagine why `reduce()` was removed from the core language after all.

That said, `reduce()` is kind of a remarkable function. The description at the beginning of this section states that `reduce()` combines elements to produce a single result. But that result can be a composite object like a `list` or a `tuple`. For that reason, `reduce()` is a very generalized higher-order function from which many other functions can be implemented.

For example, you can implement `map()` in terms of reduce():

```python
numbers = [1, 2, 3, 4, 5]

list(map(str, numbers))


def custom_map(function, iterable):
    from functools import reduce

    return reduce(
        lambda items, value: items + [function(value)],
        iterable,
        [],
    )

print(list(custom_map(str, numbers)))
```

In fact, any operation on a sequence of objects can be expressed as a `reduction`.

## Exercises: 🧠 

1) Write a Python program to triple all numbers of a given list of integers. Use Python map
2) Write a Python program to square the elements of a list using map() function.
3) Write a Python program to add three given lists using Python map and lambda
4) Write a Python program to add two given lists and find the difference between lists. Use map() function.
5) Write a Python program to convert a given list of integers and a tuple of integers in a list of strings. 
6) Write a Python program to filter a list of integers using Lambda
   ```python
   Original list of integers:  
   [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]  

   Even numbers from the said list:  
   [2, 4, 6, 8, 10]  

   Odd numbers from the said list:  
   [1, 3, 5, 7, 9]
   ```  
7) Write a Python program to find numbers divisible by nineteen or thirteen from a list of numbers using Lambda.
   ```python
   Orginal list:
   [19, 65, 57, 39, 152, 639, 121, 44, 90, 190]

   Numbers of the above list divisible by nineteen or thirteen:
   [19, 65, 57, 39, 152, 190]
   ```   
8) Write a Python program to count the even, odd numbers in a given array of integers using Lambda. 
   ```python
   Original arrays: 
   [1, 2, 3, 5, 7, 8, 9, 10] 
 
   Number of even numbers in the above array: 3  
   Number of odd numbers in the above array: 5  
   ```

* Use reduce for following tasks

9) Write a python program that multiplies all the values in a given list of integers.
10) Write a python program that finds the maximum value within the given list.
11) Write a python function that given list of strings concatenates all of them together.


# 🌐 Extra reading:

* [Python documentation on functional programming](https://docs.python.org/3/howto/functional.html#:~:text=Functional%20programming%20wants%20to%20avoid,%2C%20transactions%2C%20etc.).)

* [Iterators](https://realpython.com/python-for-loop/#iterators)

* [Real python on functional programming](https://realpython.com/python-functional-programming/#what-is-functional-programming)

* [Youtube video](https://www.youtube.com/watch?v=SvK_GErE2nM)
