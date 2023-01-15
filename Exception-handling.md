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


## Custom Exceptions

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

What is more if we simply to `except:` it means that we are placing all of the Exceptions into one bucket. But we can specify the error that we are excepting:

```python
try:
    linux_interaction()
except AssertionError as error:
    print(error)
    print('The linux_interaction() function was not executed')
except Exception as e:
    print(e)
```  


What is more, let's assume that we are trying to open some file in our program. But what happens if the file is not present when the program runs?

```python
try:
    with open('file.log') as file:
        read_data = file.read()
except:
    print('Could not open file.log')
```  

Could it be something else causing trouble and we will simply not see it here? It would be the best to specify the error here as well.
```python
try:
    with open('file.log') as file:
        read_data = file.read()
except FileNotFoundError as fnf_error:
    print(fnf_error)
```  
In this case, if file.log does not exist, the output will be the following: `[Errno 2] No such file or directory: 'file.log'`

If we combine the whole thing we can get something like this:
```python
try:
    linux_interaction()
    with open('file.log') as file:
        read_data = file.read()
except FileNotFoundError as fnf_error:
    print(fnf_error)
except AssertionError as error:
    print(error)
    print('Linux linux_interaction() function was not executed')
```

Because simply you will never know when the error occurred. What caused it etc.

Right now we should know that Exception is also python object, once raised terminates the program flow. And for now we have seen Exceptions that are built into Python programming language. But we can also raise them ourselves if something our program is not being used the way we designed it.

