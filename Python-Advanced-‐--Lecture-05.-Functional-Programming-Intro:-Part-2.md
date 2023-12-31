## `Continue`

### `Map function`

The first function on the docket is map(), which is a Python built-in function. With map(), you can apply a function to each element in an iterable in turn, and map() will return an iterator that yields the results. This can allow for some very concise code because a map() statement can often take the place of an explicit loop.

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

If you have a list of strings, then you can use map() to apply reverse() to each element of the list:


```python
animals = ["cat", "dog", "hedgehog", "gecko"]
iterator = map(reverse, animals)
iterator
# <map object at 0x7fd3558cbef0>
```


**NOTE** ❗ ❗ ❗ But remember, map() doesn’t return a list. It returns an iterator called a map object. To obtain the values from the iterator, you need to either iterate over it or use list():

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


Let's take it further once more, we already know that lambdas give us a function, let's try passing it to map function:

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

If the iterable contains something that is not suitable for a certain operation:

```python
list(map(lambda s: s[::-1], ["cat", "dog", 3.14159, "gecko"]))
# Traceback (most recent call last):
#  File "<stdin>", line 1, in <module>
#  File "<stdin>", line 1, in <lambda>
# TypeError: 'float' object is not subscriptable
```

In this case, the lambda function expects a string argument, which it tries to slice. The second element in the list, 3.14159, is a float object, which isn’t sliceable. So a TypeError occurs.


## Calling map with multiple iterables

```python
map(<f>, <iterable₁>, <iterable₂>, ..., <iterableₙ>)
```

The number of <iterablei> arguments specified to map() must match the number of arguments that <f> expects. <f> acts on the first item of each <iterablei>, and that result becomes the first item that the return iterator yields. Then <f> acts on the second item in each <iterablei>, and that becomes the second yielded item, and so on.

```python
def f(a, b, c):
    return a + b + c


list(map(f, [1, 2, 3], [10, 20, 30], [100, 200, 300]))
# [111, 222, 333]
```
Here is more visual representation of how the calculation is being done:
![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/map.webp)



# filter function

filter() allows you to select or filter items from an iterable based on evaluation of the given function. It’s called as follows:

```python
filter(<f>, <iterable>)
```


filter(<f>, <iterable>) applies function <f> to each element of <iterable> and returns an iterator that yields all items for which <f> is truthy. Conversely, it filters out all items for which <f> is falsy.

```python
def greater_than_100(x):
    return x > 100

list(filter(greater_than_100, [1, 111, 2, 222, 3, 333]))
# [111, 222, 333]
```

As we see that function is the first argument, let's try applying lambdas function here.


```python
list(filter(lambda x: x > 100, [1, 111, 2, 222, 3, 333]))
```

What is more we can even combine there things with range() function - range(n) produces an iterator that yields the integers from 0 to n - 1. The following example uses filter() to select only the even numbers from the list and filter out the odd numbers:


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


# Reduce function

reduce() applies a function to the items in an iterable two at a time, progressively combining them to produce a single result.

To use reduce(), you need to import it from a module called functools. This is possible in several ways, but the following is the most straightforward:


```python
from functools import reduce
```

## Calling reduce with two arugments:

```python
reduce(<f>, <iterable>)
```

reduce(<f>, <iterable>) uses <f>, which must be a function that takes exactly two arguments, to progressively combine the elements in <iterable>. To start, reduce() invokes <f> on the first two elements of <iterable>. That result is then combined with the third element, then that result with the fourth, and so on until the list is exhausted. Then reduce() returns the final result.

let's start with some simple examples:


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

Even in our example we can see that there are simpler ways of doing our simple example. Can you suggest any of them? Discuss

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


We could also use reduce to get the same result as max() does:

```python
max([23, 49, 6, 32])


def greater(x, y):
    return x if x > y else y


from functools import reduce
reduce(greater, [23, 49, 6, 32])
```

## Calling reduce() with initial value

```python
reduce(<f>, <iterable>, <init>)
```

When present, <init> specifies an initial value for the combination. In the first call to <f>, the arguments are <init> and the first element of <iterable>. That result is then combined with the second element of <iterable>, and so on:
```python
def f(x, y):
    return x + y


from functools import reduce
reduce(f, [1, 2, 3, 4, 5], 100)  # (100 + 1 + 2 + 3 + 4 + 5)
```

The graphical visualization of the actions taken:


![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/reduce2.webp)


As you’ve seen in the above examples, even in cases where you can accomplish a task using reduce(), it’s often possible to find a more straightforward and Pythonic way to accomplish the same task without it. Maybe it’s not so hard to imagine why reduce() was removed from the core language after all.

That said, reduce() is kind of a remarkable function. The description at the beginning of this section states that reduce() combines elements to produce a single result. But that result can be a composite object like a list or a tuple. For that reason, reduce() is a very generalized higher-order function from which many other functions can be implemented.

For example, you can implement map() in terms of reduce():

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

In fact, any operation on a sequence of objects can be expressed as a reduction.

## Exercises: 🧠 


**Lambdas section**: 
1. Write a Python program to find if a given string starts with a given character using Lambda. Sample Output:
True
False
1. Write a Python program to create a lambda function that adds 15 to a given number passed in as an argument, also create a lambda function that multiplies argument x with argument y and print the result.
1. Write a Python program to add two given lists using map and lambda.
1. Write a Python program to square and cube every number in a given list of integers using Lambda
1. Write a Python program to extract year, month, date and time using Lambda. Sample Output:
2020-01-15 09:03:32.744178
2020
1
15
09:03:32.744178
  

**Sorted section**: 
1. Write a Python program to sort a list of tuples using Lambda.
Original list of tuples:
[('English', 88), ('Science', 90), ('Maths', 97), ('Social sciences', 82)]
Sorting the List of Tuples:
[('Social sciences', 82), ('English', 88), ('Science', 90), ('Maths', 97)]
1. Write a Python program to sort a list of dictionaries buy color value using Lambda.Original list of dictionaries :
[{'make': 'Nokia', 'model': 216, 'color': 'Black'}, {'make': 'Mi Max', 'model': '2', 'color': 'Gold'}, {'make': 'Samsung', 'model': 7, 'color': 'Blue'}]
Sorting the List of dictionaries :
[{'make': 'Nokia', 'model': 216, 'color': 'Black'}, {'make': 'Samsung', 'model': 7, 'color': 'Blue'}, {'make': 'Mi Max', 'model': '2', 'color': 'Gold'}]
1. Write a Python program to sort a given matrix in ascending order according to the sum of its rows using lambda.Original Matrix:  
`[[1, 2, 3], [2, 4, 5], [1, 1, 1]]` 
Sort the said matrix in ascending order according to the sum of its rows  
`[[1, 1, 1], [1, 2, 3], [2, 4, 5]]`  
Original Matrix:  
`[[1, 2, 3], [-2, 4, -5], [1, -1, 1]]`  
Sort the said matrix in ascending order according to the sum of its rows  
`[[-2, 4, -5], [1, -1, 1], [1, 2, 3]]`  

**Map section**: 

1. Write a Python program to triple all numbers of a given list of integers. Use Python map
1. Write a Python program to square the elements of a list using map() function.
1. Write a Python program to add three given lists using Python map and lambda
1. Write a Python program to add two given lists and find the difference between lists. Use map() function.
1. Write a Python program to convert a given list of integers and a tuple of integers in a list of strings.

**Filter section**: 
1. Write a Python program to filter a list of integers using Lambda
Original list of integers:  
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]  
Even numbers from the said list:  
[2, 4, 6, 8, 10]  
Odd numbers from the said list:  
[1, 3, 5, 7, 9]  
1. Write a Python program to find numbers divisible by nineteen or thirteen from a list of numbers using Lambda.Orginal list:
[19, 65, 57, 39, 152, 639, 121, 44, 90, 190]
Numbers of the above list divisible by nineteen or thirteen:
[19, 65, 57, 39, 152, 190]
1. Write a Python program to count the even, odd numbers in a given array of integers using Lambda. Original arrays:  
[1, 2, 3, 5, 7, 8, 9, 10]  
Number of even numbers in the above array: 3  
Number of odd numbers in the above array: 5  



**Reduce section**: 

1. Write a python program that multiplies all the values in a given list of integers.
1. Write a python program that finds the maximum value within the given list.
1. Write a python function that given list of strings concatenates all of them together.
1. redo all the previous exercises with an initial value given to the reduce function.


# 🌐 Extra reading:

* [Python documentation on functional programming](https://docs.python.org/3/howto/functional.html#:~:text=Functional%20programming%20wants%20to%20avoid,%2C%20transactions%2C%20etc.).)

* [iterators](https://realpython.com/python-for-loop/#iterators)

* [real python on functional programming](https://realpython.com/python-functional-programming/#what-is-functional-programming)

* [youtube video](https://www.youtube.com/watch?v=SvK_GErE2nM)


# Solutions

**Lambdas section**: 
1. 
```python
starts_with = lambda x: True if x.startswith('P') else False
print(starts_with('Python'))
```
1. 
```python
r = lambda a : a + 15
print(r(10))
r = lambda x, y : x * y
print(r(12, 4))
```
1. 
```python
nums1 = [1, 2, 3]
nums2 = [4, 5, 6]
print("Original list:")
print(nums1)
print(nums2)
result = map(lambda x, y: x + y, nums1, nums2)
print("\nResult: after adding two list")
print(list(result))
```
1. 
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Original list of integers:")
print(nums)
print("\nSquare every number of the said list:")
square_nums = list(map(lambda x: x ** 2, nums))
print(square_nums)
print("\nCube every number of the said list:")
cube_nums = list(map(lambda x: x ** 3, nums))
print(cube_nums)
```
1.
```python
import datetime
now = datetime.datetime.now()
print(now)
year = lambda x: x.year
month = lambda x: x.month
day = lambda x: x.day
t = lambda x: x.time()
print(year(now))
print(month(now))
print(day(now))
print(t(now))
```


**sorted section**: 

1.
```python
subject_marks = [('English', 88), ('Science', 90), ('Maths', 97), ('Social sciences', 82)]
print("Original list of tuples:")
print(subject_marks)
subject_marks.sort(key = lambda x: x[1])
print("\nSorting the List of Tuples:")
print(subject_marks)
```
1.
```python
models = [{'make':'Nokia', 'model':216, 'color':'Black'}, {'make':'Mi Max', 'model':'2', 'color':'Gold'}, {'make':'Samsung', 'model': 7, 'color':'Blue'}]
print("Original list of dictionaries :")
print(models)
sorted_models = sorted(models, key = lambda x: x['color'])
print("\nSorting the List of dictionaries :")
print(sorted_models)
```

1.
```python
def sort_matrix(M):
    result = sorted(M, key=lambda matrix_row: sum(matrix_row)) 
    return result

matrix1 = [[1, 2, 3], [2, 4, 5], [1, 1, 1]]
matrix2 = [[1, 2, 3], [-2, 4, -5], [1, -1, 1]]

print("Original Matrix:")
print(matrix1)
print("\nSort the said matrix in ascending order according to the sum of its rows") 
print(sort_matrix(matrix1))
print("\nOriginal Matrix:")
print(matrix2) 
print("\nSort the said matrix in ascending order according to the sum of its rows") 
print(sort_matrix(matrix2))
```

**filter section**: 

1.
```python
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print("Original list of integers:")
print(nums)
print("\nEven numbers from the said list:")
even_nums = list(filter(lambda x: x%2 == 0, nums))
print(even_nums)
print("\nOdd numbers from the said list:")
odd_nums = list(filter(lambda x: x%2 != 0, nums))
print(odd_nums)
```
1.
```python
nums = [19, 65, 57, 39, 152, 639, 121, 44, 90, 190]
print("Orginal list:")
print(nums) 
result = list(filter(lambda x: (x % 19 == 0 or x % 13 == 0), nums)) 
print("\nNumbers of the above list divisible by nineteen or thirteen:")
print(result)
```
1.
```python
array_nums = [1, 2, 3, 5, 7, 8, 9, 10]
print("Original arrays:")
print(array_nums)
odd_ctr = len(list(filter(lambda x: (x%2 != 0) , array_nums)))
even_ctr = len(list(filter(lambda x: (x%2 == 0) , array_nums)))
print("\nNumber of even numbers in the above array: ", even_ctr)
print("\nNumber of odd numbers in the above array: ", odd_ctr)
```


**reduce section**: 
1. 
```python
reduce(lambda x, y: x * y, [1, 2, 3, 4, 5])
```
1. 
```python
def greater(x, y):
    return x if x > y else y


from functools import reduce
reduce(greater, [23, 49, 6, 32])
```
1. 
```python
def f(x:str , y: str) -> str:
    return x + y
reduce(f, ["cat", "dog", "hedgehog", "gecko"])
```