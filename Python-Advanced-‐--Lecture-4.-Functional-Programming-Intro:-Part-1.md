## `Introduction`

In computer science, functional programming is a **programming paradigm where programs are constructed by applying and composing functions**. It is a declarative programming paradigm in which function definitions are trees of expressions that map values to other values, rather than a sequence of imperative statements which update the running state of the program.

In this section We will pay more attention on some functions already supplied by python programming language to make our lives a bit easier. The things we are going to cover here are also useful for **OOP paradigms** as well. 

In Python in general everything is an **`object`**, thus functions do escape this either. Functions can be assigned to have other names etc.

## `Overview`

`Functional programming` in general does not store any state of the program. Mainly functions cannot know, nor change any `globals`. 
`Functional programing` is done with some rules:
-  We use pure/ idempotent functions.
-  We do not access a global state variables, nor we change them
-  Under no circumstances the results of the function provided same inputs cannot change

**NOTE** ❗functional programming functions do not have any side effect. Meaning that we do not store anything in memory when applying them, we simply map input to the output.

### `sorted function`

We have already seen this function in action in the beginning of the course.

```python
animals = ["ferret", "vole", "dog", "gecko"]
sorted(animals)
# ['dog', 'ferret', 'gecko', 'vole']
```

This is already something that we have seen, but `sorted` function [documentation](https://docs.python.org/3/library/functions.html#sorted) says that there might be another parameter passed into the function - `key`. _`key` specifies a function of one argument that is used to extract a comparison key from each element in `iterable` (for example, `key=str.lower`). The default value is `None` (compare the elements directly)._

So this key parameter accepts a callable and then tried to sort our data according to it:

```python
animals = ["ferret", "vole", "dog", "gecko"]
sorted(animals, key=len)
# ['dog', 'vole', 'gecko', 'ferret']
```



### `Lambda functions`


We have already had an intro to `lambdas` [here](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-11:-Functions-(-Part-2-))
Functional programming is all about calling functions and passing them around, so it naturally involves defining a lot of functions. You can always define a function in the usual way, using the [def](https://realpython.com/defining-your-own-python-function/#function-calls-and-definition) keyword as you have seen in previous tutorials in this series.

Sometimes, though, it’s convenient to be able to define an anonymous function on the fly, without having to give it a name. In Python, you can do this with a lambda expression:

```python
lambda <parameter_list>: <expression>
```

| Column 1 Header | Column 2 Header |
| :--------------- | :--------------- |
| lambda | The keyword that introduces a lambda expression |
| <parameter_list> | An optional comma-separated list of parameter names |
| : | Punctuation that separates <parameter_list> from <expression> |
| expression| An expression usually involving the names in <parameter_list> |

So let's continue now a bit on lambda functions. Let's say we want to define lambda function that returns string in reverse:

```python
reverse = lambda s: s[::-1]
reverse("I am a string")
# 'gnirts a ma I'
```

This is actually the equivalent of:

```python
def reverse(s):
    return s[::-1]


reverse("I am a string")
# 'gnirts a ma I'


reverse = lambda s: s[::-1]
reverse("I am a string")
# 'gnirts a ma I'

```

As you can see they both yield the same result.
What is more as you have already seen it is not necessary to assign lambda function a name, you can also call it directly:

```python
(lambda s: s[::-1])("I am a string")
# 'gnirts a ma I'
```

One more example:

```python
(lambda x1, x2, x3: (x1 + x2 + x3) / 3)(9, 6, 6)
# 7.0
(lambda x1, x2, x3: (x1 + x2 + x3) / 3)(1.4, 1.1, 0.5)
# 1.0
```

Now let's go back into the `sorted` function we have seen already. Since `lambda` gives us `callable`:

```python
callable(lambda s: s[::-1])
# True
```

**NOTE** ❗  callable: Return `True` if the object argument appears callable, `False` if not.


Reviewing our code from before:
```python
animals = ["ferret", "vole", "dog", "gecko"]

def reverse_len(string: str) -> int:
    return -len(string)

sorted(animals, key=reverse_len)
# ['ferret', 'gecko', 'vole', 'dog']
```

This could be changed with lambda function:

```python
animals = ["ferret", "vole", "dog", "gecko"]
sorted(animals, key=lambda s: -len(s))
# ['ferret', 'gecko', 'vole', 'dog']
```


Looks a little bit more compact and is still quite readable right? As any things in programming or life both approaches have up and down sides. Discuss the advantages and disadvanates of both approaches.



**NOTE** ❗ You can only define fairly rudimentary functions with `lambda`. The return value from a lambda expression can only be one single expression. A lambda expression can’t contain statements like assignment or return, nor can it contain control structures such as `for`, `while`, `if`, `else`, or `def`.

As we have seen before functions in python can return anything:

```python
def func(x):
    return x, x ** 2, x ** 3

func(2)
# (2, 4, 16)
```

In this case we simply return `Tuple`. Let's say we try to do the same with lambda functions:

```python
(lambda x: x, x ** 2, x ** 3)(3)
<stdin>:1: SyntaxWarning: 'tuple' object is not callable; perhaps you missed a comma?
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'x' is not defined
```

To work with this is all you got to do is explicitly tell python that this is a `Tuple` object that we are returning:

```python
(lambda x: (x, x ** 2, x ** 3))(3)
# (3, 9, 27)
(lambda x: [x, x ** 2, x ** 3])(3)
# [3, 9, 27]
(lambda x: {1: x, 2: x ** 2, 3: x ** 3})(3)
# {1: 3, 2: 9, 3: 27}
```

As you can see there might be plenty of variations of what **lambda functions** can return.


One more final detail: If you find a need to include a lambda expression in a formatted string literal (f-string), then you’ll need to enclose it in explicit parentheses:

```python
print(f"--- {lambda s: s[::-1]} ---")
  File "<stdin>", line 1
    (lambda s)
             ^
SyntaxError: f-string: invalid syntax
```

Do this instead:
```python
print(f"--- {(lambda s: s[::-1])} ---")
# --- <function <lambda> at 0x7f97b775fa60> ---
print(f"--- {(lambda s: s[::-1])('I am a string')} ---")
# --- gnirts a ma I ---
```

## Exercises: 🧠 

1) Write a Python program to find if a given `string` starts with a given character using `Lambda`. Output:`True` or `False`
2) Write a Python program to create a `lambda` function that adds `15` to a given number passed in as an argument, also create a `lambda` function that 
   multiplies argument `x` with argument `y` and print the result.
3) Write a Python program to square and cube every number in a given list of `integers` using `Lambda`.
4) Write a Python program to extract `year, month, date and time` using `Lambda`. Sample Output:
   ```python
   2020-01-15 09:03:32.744178
   2020
   1
   15
   09:03:32.744178
   ```
 
5) Write a Python program to `sort` a `list` of `tuples` using `Lambda`.
   ```python
   # Original list of tuples:
   [('English', 88), ('Science', 90), ('Maths', 97), ('Social sciences', 82)]

   # Sorted the List of Tuples:
   [('Social sciences', 82), ('English', 88), ('Science', 90), ('Maths', 97)]
   ```
6) Write a Python program to `sort` a `list` of dictionaries buy `color value` using `Lambda`.
   ```python
   # Original list of dictionaries :
   [{'make': 'Nokia', 'model': 216, 'color': 'Black'}, {'make': 'Mi Max', 'model': '2', 'color': 'Gold'}, {'make': 'Samsung', 'model': 7, 'color': 
   'Blue'}]

   # Sorted the List of dictionaries :
   [{'make': 'Nokia', 'model': 216, 'color': 'Black'}, {'make': 'Samsung', 'model': 7, 'color': 'Blue'}, {'make': 'Mi Max', 'model': '2', 'color': 
   'Gold'}]
   ```
7) Write a Python program to `sort` a given matrix in `ascending` order according to the sum of its rows using `lambda`.
   ```python
   # Original Matrix:  
   `[[1, 2, 3], [2, 4, 5], [1, 1, 1]]`
 
   # Sort the said matrix in ascending order according to the sum of its rows  
   `[[1, 1, 1], [1, 2, 3], [2, 4, 5]]`
  
   # Original Matrix:  
   `[[1, 2, 3], [-2, 4, -5], [1, -1, 1]]`  

   # Sort the said matrix in ascending order according to the sum of its rows  
   `[[-2, 4, -5], [1, -1, 1], [1, 2, 3]]`
   ```  

# 🌐 Extra reading:

* [Python functional programming documentation](https://docs.python.org/3/howto/functional.html#:~:text=Functional%20programming%20wants%20to%20avoid,%2C%20transactions%2C%20etc.).)

* [Iterators](https://realpython.com/python-for-loop/#iterators)

* [Real python on functional programming](https://realpython.com/python-functional-programming/#what-is-functional-programming)

* [Youtube](https://www.youtube.com/watch?v=SvK_GErE2nM)


