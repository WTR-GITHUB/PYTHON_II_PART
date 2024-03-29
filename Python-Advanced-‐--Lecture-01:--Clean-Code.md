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
| Variable| Use a lowercase single letter, word, or words. Separate words with underscores to improve readability.| variable, my_variable   |
| Class| Start each word with a capital letter. Do not separate words with underscores. This style is called camel case or pascal case.   | Model, MyClass|
| Method| Use a lowercase word or words. Separate words with underscores to improve readability. | class_method, method  |
| Constant| Use an uppercase single letter, word, or words. Separate words with underscores to improve readability.  | CONSTANT, MY_CONSTANT, MY_LONG_CONSTANT |
| Module | Use a short, lowercase word or words. Separate words with underscores to improve readability.  | module.py, my_module.py|
| Package| Use a short, lowercase word or words. Do not separate words with underscores.  | package, mypackage  |


## Variable naming

Sometimes it ain't that easy to come up with good variable naming and thus many jokes are written about it:

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
first_name, last_name = name.split()
print(last_name, first_name, sep=', ')
```

Which Zen of Python line does this reflect the best?
Discuss.

The same rules apply to everything, functions, classes etc.
**Do not** 🛑  go around abbreviating names like an example below, because this just brings chaos and misinterpretation of what was actually meant:

```python
def db(x: int) -> int:
  return x * 2
```

after some time it might not be obvious what _db_ does, it was when you were writing the function and using it, but after a week or two, you see usage of _db_ in your code and it is not that obvious anymore. Instead you can do something like:

```python
def multiply_by_two(x: int) -> int:
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
from typing import Tuple
def quadratic(a: float, b: float, c: float, x:float) -> Tuple[float, float]:
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
def double(x: int) -> int:
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

```python
# Recommended
tuple = (1,)

# Not recommended
tuple = (1, )
```

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

**PRO TIP** ✔️ 

Don’t compare Boolean values to True or False using the equivalence operator.

```python
# Not recommended
my_bool = 6 > 5
if my_bool == True:
    return '6 is bigger than 5'

# Recommended
if my_bool:
    return '6 is bigger than 5'
```




## Maximum line length

PEP 8 suggests lines should be limited to 79 characters. This is because it allows you to have multiple files open next to one another, while also avoiding line wrapping. Nowadays it is accepted to have between 120-140 characters length in one line. For Example for pylinter not to complain we can create a file in the project directory called ***.pylintrc*** :

```config
[FORMAT]
max-line-length=120
```
And pylint should not complain if the line length is less than 120 characters.




Python will assume line continuation if code is contained within parentheses, brackets, or braces:

```python
def function(arg_one: str, arg_two: str,
             arg_three: str, arg_four: str) -> str:
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


def top_level_function() -> None:
    return None
```

**Surround method definitions inside classes with a single blank line**

```python
class MyClass:
    def first_method(self) -> None:
        return None

    def second_method(self) -> None:
        return None
```

**Use blank lines sparingly inside functions to show clear steps** Sometimes, a complicated function has to complete several steps before the return statement. To help the reader understand the logic inside the function, it can be helpful to leave a blank line between each step.

In the example below, there is a function to calculate the variance of a list. This is two-step problem, so I have indicated each step by leaving a blank line between them. There is also a blank line before the return statement. This helps the reader clearly see what’s returned:

```python
from typing import List

def calculate_variance(number_list: List[float]) -> float:
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

# Linters

Linters are programs that analyze code and flag errors. They provide suggestions on how to fix the error. Linters are particularly useful when installed as extensions to your text editor, as they flag errors and stylistic problems while you write. In this section, you’ll see an outline of how the linters work, with links to the text editor extensions at the end.

Most popular python linters:

* flake8 
* autopep8 
* mypy
* pylint

Linters do not have any direct connections on how the code is being executed: linters might be complaining but code will run just fine. Nevertheless this is not the reason to ignore linter errors. In general linters will help you to keep you code clean and maintanable.

# Autoformatters

Autoformatters are programs that refactor your code to conform with PEP 8 automatically. Once such program is black, which autoformats code following most of the rules in PEP 8. One big difference is that it limits line length to 88 characters, rather than 79. However, you can overwrite this by adding a command line flag, as you’ll see in an example below.

```sh
pip install black
```

run black on a single file:

```sh
python -m black <filename>
```

This should automatically format the code to the best practices.

**PRO TIP** 💯:   
You may also use [this](https://marcobelo.medium.com/setting-up-python-black-on-visual-studio-code-5318eba4cd00#:~:text=Go%20to%20settings%20in%20your,%E2%80%9D%20and%20select%20%E2%80%9Cblack%E2%80%9D.) This will automatically format file upon saving it. 


# Setting up VSCode

In general as before we advice to use VSCode, of course this is far away from the only IDE you can chose. Upon installing VSCode also install Python extension, this will install a few things needed to efficiently write code in Python using VSCode. What is more also set up a linter as well.

`CTRL+SHIFT+P`
write
`linter` this should give an option _python: select linter_ and choose _mypy_ for example.

**What else to put here, what other extensions, features are useful here?**


## Exercises: 


* **Task Nr.1**:
Fix these coding examples according to the standards we learnt during this lecture:

**Example 1:**
```python
class person():
    def __init__(self, name, surname):
        self.name=name
        self.surname=surname
    def sayHello(self):
        print(f"hello, {self.name}")
PERSON = person("first", "person")
PERSON.sayHello()
```


**Example 2:**
```python
def x(a):
    """Function greets a person given full name as a string"""

    print(f"Hello {a.split()[0]} {a.split()[1]}, How are you today?")
```

**Example 3:**

```python
def Greet_User (age):
    eligiebleTo_enter = age>21
    
    if eligiebleTo_enter == True:
        print("Welcome")
    if eligiebleTo_enter == False:
        print("Access denied")
```


* **Task Nr.2**:
Magic Number problem. A number is said to be a magic number, if the sum of its digits are calculated till a single digit recursively by adding the sum of the digits after every addition. If the single digit comes out to be 1,then the number is a magic number. 

**For example**
Number = 50113 
=> 5+0+1+1+3=10 
=> 1+0=1 
This is a Magic Number 

**For example** 
Number = 1234 
=> 1+2+3+4=10 
=> 1+0=1 
This is a Magic Number


Write a python function that takes in one parameter - integer and then returns `True` if number is magic number or `False` if it is not a magic number 


# 🌐 Extra reading:

[How to Write Beautiful Python Code With PEP 8](https://realpython.com/python-pep8/)

[Style Guide for Python Code](https://peps.python.org/pep-0008/#introduction)

[more on linters](https://dsstream.com/improve-your-python-code-quality/#:~:text=Linters%20are%20programs%20that%20advise,Preventing%20bugs%20in%20a%20project.)

[80 char line in vscode](https://levelup.gitconnected.com/do-you-know-about-rulers-in-visual-studio-code-f754b221a135)