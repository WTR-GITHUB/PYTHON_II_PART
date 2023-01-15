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
