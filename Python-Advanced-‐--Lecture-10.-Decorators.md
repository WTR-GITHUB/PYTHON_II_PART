# Decorators

This is one of the advanced topic of Python programming language, even though decorators subject is present in other programming languages too. Here we are going to approach them from the very beginning. 

To understand Decorators properly we first need to dive into the **Functions**. For our purposes, a function returns a value based on the given arguments. Here is a very simple example:


```python
def add_one(number):
    return number + 1

add_one(2)
```  
As we have seen before in the lectures: Python functions are [first-class objects](https://dbader.org/blog/python-first-class-functions) just like (int, str, float etc.) Thus they can be passed into the the functions as arguments:

```python
from typing import Callable, Optional, Any


def say_hello(name: str) -> str:
    return f"Hello {name}"

def be_awesome(name: str):
    return f"Yo {name}, together we are the awesomest!"

def greet_bob(greeter_func: Callable) -> Any:
    return greeter_func("Bob")


greet_bob(say_hello)

greet_bob(be_awesome)
```

Stop here and analyze the code, make sure you understand what is going on here.
1. We create two functions that return string values.
1. One function accepts function as a parameter.
1. Once the function is called it behaves differently according to the argument (function) it receives.


## Inner Functions

Let's take it one level deeper. It is also possible to define a function within a function. Just like in some movie they went into people dreams and then it was impossible to understand anything. Let's try t understand what is happening here:

```python
def parent() -> None:
    print("Printing from the parent() function")

    def first_child():
        print("Printing from the first_child() function")

    def second_child():
        print("Printing from the second_child() function")

    second_child()
    first_child()
```

So what is happening here:  

1. we define parent() function
1. What is under this function - same as for variables in the function body - belongs only to this function, thus outside of the function first_child and second_child does not exist.
1. We simply call these functions once the parent() is called


## Returning Functions From Functions

Seems easy right? Let's spicy it up a bit.

```python
from typing import Callable


def parent(num: int) -> Callable:
    def first_child():
        return "Hi, I am Emma"

    def second_child():
        return "Call me Liam"

    if num == 1:
        return first_child
    else:
        return second_child
```

1. We allow user to pass in the number.
1. according to the number we are giving user back a function: either first_child() or second_child()
**NOTE** the functions are returned without "()" meaning that we are yet NOT executing those functions only returning them for user to user later on.

We now can use this function like this:

```python
first = parent(1)
second = parent(2)

print(first)

print(second)
```




