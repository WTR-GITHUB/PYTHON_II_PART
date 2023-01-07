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








# Useful links:

[How to Write Beautiful Python Code With PEP 8](https://realpython.com/python-pep8/)

[Style Guide for Python Code](https://peps.python.org/pep-0008/#introduction)