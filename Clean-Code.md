# PEP8

As any programming language has naming standards and standards for the ways it does certain things - Python is not an exception. With the naming standards we communicate better with other developers on what certain things must be and what they should not. It was written in 2001 by Guido van Rossum, Barry Warsaw, and Nick Coghlan. The primary focus of PEP 8 is to improve the readability and consistency of Python code.

PEP stands for Python Enhancement Proposal, and there are several of them. A PEP is a document that describes new features proposed for Python and documents aspects of Python, like design and style, for the community.

Why do we need it, simply as the [Zen of Python](https://peps.python.org/pep-0020/#the-zen-of-python) states: Readability counts. There are many benefits of standardizing the way people write code:
1. If you follow a certain standard it is easier for others to understand your code and the other way around.
1. Improved code readability.
1. Makes code clean.

These all sound like synonyms and of course they are, but let's see a few examples where the naming standards .

**NOTE** :

Never 🛑  use l, O single letter names as they might be mistakes for 1 and 0:
```python
O = 2  # This may look like you're trying to reassign 2 to zero
```

## Naming conventions

It is never too much of revisiting naming conventions as it really separates a good python programmer from great one. You might understand how language works but if you do not follow the naming conventions, nobody will understand you code to full extent.


| Attempt | #1    | #2    |
| :---   | :--- | :--- |
| Function| Use a lowercase word or words. Separate words by underscores to improve readability.| function, my_function|
| Variable| Use a lowercase single letter, word, or words. Separate words with underscores to improve readability.| 283   |
| Class| Start each word with a capital letter. Do not separate words with underscores. This style is called camel case or pascal case.   | Model, MyClass|
| Method| Use a lowercase word or words. Separate words with underscores to improve readability. | class_method, method  |
| Constant| Use an uppercase single letter, word, or words. Separate words with underscores to improve readability.  | CONSTANT, MY_CONSTANT, MY_LONG_CONSTANT |
| Module | Use a short, lowercase word or words. Separate words with underscores to improve readability.  | module.py, my_module.py|
| Package| Use a short, lowercase word or words. Do not separate words with underscores.  | package, mypackage  |


## Variable naming

Sometimes it ain't that easy to come up with good variable naming and thus many jokes are written about it:

![alt text](http://url/to/img.png)
![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/searching_meaningful_variable_name.png)

Why is this important? Readability.

Imagine getting to read code like this:

```python
x = input()
y, z = x.split()
print(z, y, sep=', ')
```

Is it easy to understand what is happening? What is the aim of the code? What is it supposed to do?
Now compare it with:


```python
name = input()
first_name, last_name = x.split()
print(last_name, first_name, sep=', ')
```

Which Zen of Python line does this reflect the best?
Discuss.

The same rules apply to everything, functions, classes etc.
**Do not** 🛑  go around abbreviating names like an example below, because this just brings chaos and misinterpretation of what was actually meant:

```python
def db(x):
  return x * 2
```

after some time it might not be obvious what _db_ does, it was when you were writing the function and using it, but after a week or two, you see usage of _db_ in your code and it is not that obvious anymore. Instead you can do something like:

```python
def multiply_by_two(x):
    return x * 2
```


Imagine now reviewing the code of your colleague:
```python
pi = 3.14
CustomerName = "John Doe"
CUSTOMER_AGE = 15
```


if later on these variable were used in the code, what would be the expectations of the developers for these variables? How would You do it?
Discuss by looking into naming conventions table above.


## Documentation strings

Documentation strings, or docstrings, are strings enclosed in double (""") or single (''') quotation marks that appear on the first line of any function, class, method, or module

They are required for more complex public modules, functions and methods. The ones that are exposed for your library consumers to understand how to use certain pieces of code 
 
```python
def quadratic(a, b, c, x):
    """Solve quadratic equation via the quadratic formula.

    A quadratic equation has the following form:
    ax**2 + bx + c = 0

    There always two solutions to a quadratic equation: x_1 & x_2.
    """
    x_1 = (- b+(b**2-4*a*c)**(1/2)) / (2*a)
    x_2 = (- b-(b**2-4*a*c)**(1/2)) / (2*a)

    return x_1, x_2
```

see this might be extremely useful when you are not entirely sure how function works.

## Whitespace around Binary Operators
Surround the following binary operators with a single space on either side:

* Assignment operators (=, +=, -=, and so forth)
* Comparisons (==, !=, >, <. >=, <=) and (is, is not, in, not in)
* Booleans (and, not, or) 

```python
# Recommended
y = x**2 + 5
z = (x+y) * (x-y)

# Not Recommended
y = x ** 2 + 5
z = (x + y) * (x - y)
```



```python
# Not recommended
if x > 5 and x % 2 == 0:
    print('x is larger than 5 and divisible by 2!')
```

In the above example, the and operator has lowest priority. It may therefore be clearer to express the if statement as below:


```python
# Recommended
if x>5 and x%2==0:
    print('x is larger than 5 and divisible by 2!')
```
## When to Avoid adding whitespace
In some cases, adding whitespace can make code harder to read. Too much whitespace can make code overly sparse and difficult to follow. PEP 8 outlines very clear examples where whitespace is inappropriate.

The most important place to avoid adding whitespace is at the end of a line. This is known as trailing whitespace. It is invisible and can produce errors that are difficult to trace.

* Immediately inside parentheses, brackets, or braces:

```python
# Recommended
my_list = [1, 2, 3]

# Not recommended
my_list = [ 1, 2, 3, ]
```
* Before a comma, semicolon, or colon:

```python
x = 5
y = 6

# Recommended
print(x, y)

# Not recommended
print(x , y)
```

* Before the open parenthesis that starts the argument list of a function call:

```python
def double(x):
    return x * 2

# Recommended
double(3)

# Not recommended
double (3)
```
* Before the open bracket that starts an index or slice:
```python
# Recommended
list[3]

# Not recommended
list [3]
```
* Between a trailing comma and a closing parenthesis:

# Recommended
tuple = (1,)

# Not recommended
tuple = (1, )


* To align assignment operators:

```python
# Recommended
var1 = 5
var2 = 6
some_long_var = 7

# Not recommended
var1          = 5
var2          = 6
some_long_var = 7
```





## Maximum line length

PEP 8 suggests lines should be limited to 79 characters. This is because it allows you to have multiple files open next to one another, while also avoiding line wrapping.

Python will assume line continuation if code is contained within parentheses, brackets, or braces:

```python
def function(arg_one, arg_two,
             arg_three, arg_four):
    return arg_one
```

If it is impossible to use implied continuation, then you can use backslashes to break lines instead:

```python
from mypkg import example1, \
    example2, example3
```


## Blank lines

How you lay out your code has a huge role in how readable it is. In this section, you’ll learn how to add vertical whitespace to improve the readability of your code. 


**Surround top-level functions and classes with two blank lines**
```python
class MyFirstClass:
    pass


class MySecondClass:
    pass


def top_level_function():
    return None
```

**Surround method definitions inside classes with a single blank line**

```python
class MyClass:
    def first_method(self):
        return None

    def second_method(self):
        return None
```

**Use blank lines sparingly inside functions to show clear steps** Sometimes, a complicated function has to complete several steps before the return statement. To help the reader understand the logic inside the function, it can be helpful to leave a blank line between each step.

In the example below, there is a function to calculate the variance of a list. This is two-step problem, so I have indicated each step by leaving a blank line between them. There is also a blank line before the return statement. This helps the reader clearly see what’s returned:

```python
def calculate_variance(number_list):
    sum_list = 0
    for number in number_list:
        sum_list = sum_list + number
    mean = sum_list / len(number_list)

    sum_squares = 0
    for number in number_list:
        sum_squares = sum_squares + number**2
    mean_squares = sum_squares / len(number_list)

    return mean_squares - mean**2
```


# Useful links:

[How to Write Beautiful Python Code With PEP 8](https://realpython.com/python-pep8/)

[Style Guide for Python Code](https://peps.python.org/pep-0008/#introduction)