# Exception Handling in Python

Python is dynamically typed language, meaning that before running the code there is no compiler check that would go through all the code and check if everything is in-tact. There is only check for a syntax errors. So as soon as it hits the problematic situation - Errors, Exceptions etc. - it simply terminates and throws that error at you to solve. 


## Exceptions vs Syntax Errors ❗ ❗ ❗ 

As mentioned before python parses syntax errors but Syntax Errors do not behave in the same fashion as exceptions errors:

```python
print( 0 / 0 ))
  File "<stdin>", line 1
    print( 0 / 0 ))
                  ^
SyntaxError: invalid syntax
```

The arrow indicates where the parser ran into the **syntax error**. In this example, there was one bracket too many. Remove it and run your code again:

```python
print( 0 / 0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```


This time, you ran into an **exception error**. This type of error occurs whenever syntactically correct Python code results in an error. The last line of the message indicated what type of exception error you ran into.  
Instead of showing the message exception error, Python details what type of exception error was encountered. In this case, it was a ZeroDivisionError. Python comes with [various built-in exceptions](https://docs.python.org/3/library/exceptions.html) as well as the possibility to create self-defined exceptions.

## Raising an Exception

How do we raise an Exception ourselves?


```python
x = 10
if x > 5:
    raise Exception('x should not exceed 5. The value of x was: {}'.format(x))
```

Try running this code, what is the outcome?

## The AssertionError Exception

Instead of waiting for a program to crash midway, you can also start by [making an assertion in Python](https://dbader.org/blog/python-assert-tutorial). We assert that a certain condition is met. If this condition turns out to be True, then that is excellent! The program can continue. If the condition turns out to be False, you can have the program throw an AssertionError exception.

Have a look at the following example, where it is asserted that the code will be executed on a Linux system:

```python
import sys
assert ('linux' in sys.platform), "This code runs on Linux only."
```

## `try` and `except` block: Handling Exceptions



The try and except block in Python is used to catch and handle exceptions. Python executes code following the try statement as a “normal” part of the program. The code that follows the except statement is the program’s response to any exceptions in the preceding try clause.

```python
def linux_interaction():
    assert ('linux' in sys.platform), "Function can only run on Linux systems."
    print('Doing something.')

try:
    linux_interaction()
except:
    do_something_else()
```

**PRO TIP** ❗ ❗ ❗ 

**DO NOT** simply pass the error if it occurs, this is considered as serious code smell and very bad practice:

```pyhon
try:
    something_that_breaks()
except:
    pass
```


**PRO TIP** the opposite of the code smell before it is usually super nice to except actual Exceptions and handle them accordingly, check the example below:  

```python
numbers = [1, 2, 3, 4, 5]

try:
    print(numbers[100])  # <- Out of range index
except IndexError:
    print("The requested index is out of range")
except KeyError:
    print("Could not retrieve that value.")
```  

Also it is important to raise the right errors in the right places, the same as with logging/ printing or anything else. We do not want to mislead other developers, clients, anyone involved into trying to solve issues that do not exists. For Example if we are expecting an integers from user and user gives us string -  we should raise ValueError:

```python
while True:
    try:
        x = int(input("Please enter a number: "))
        break
    except ValueError:
        print("Oops!  That was no valid number.  Try again...")
```



## Custom Exceptions

Right now we should know that Exception is also python object, once raised terminates the program flow. And for now we have seen Exceptions that are built into Python programming language. But we can also raise them ourselves if something our program is not being used the way we designed it. As seen before python has built in Object called exception, it is a class that in order to instantiate it we need a message. So we can simply try inheriting all the attributes of the class and create our own message if we want a custom Exception class. Let's see this in action.  

So how do we do this? Let's say we are creating a gambling website and we expect our users to be at least 21 years of age, we could do something similar to the program we have seen at the starting of the lecture, but before let's create a custom Exception class:

```python
class AgeTooLow(Exception):

    def __init__(self):
        self.message = "User should be atleast 21 years old!"
        super().__init__(self.message)
```  

Then we can just simply amend the program above to fit our needs.

```python
users_age = int(input("enter your age: "))

if users_age < 21:
   raise AgeTooLow
```

Isn't this neat? We not have crafted our own Exception in Python!  

## passing an argument to the Exception 

So how do we make sure that the message is a little bit more relevant and shows what exactly has been passed?


```python
class AgeTooLow(Exception):

    def __init__(self, age):
        self.message = f"User should be atleast 21 years old! current user is {age} year('s) old"
        super().__init__(self.message)
```  

And then use it the way we have designed it:

```python
users_age = int(input("enter your age: "))

if users_age < 21:
   raise AgeTooLow(users_age )
```  

try running the program yourselves, does it work? Try playing around with messages, variables etc.




# Exercises 🧠 
1. What if we also wanted to raise an error if the user is too old for our gambling website? Try implementing it yourselves




