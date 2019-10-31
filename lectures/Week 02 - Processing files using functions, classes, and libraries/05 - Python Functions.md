---
layout: default
title: 05 - Python Functions
parent: Week 02 - Processing files using functions, classes, and libraries
grand_parent: Lectures
nav_order: 9
---

# Python Functions
[Python Function Tutorial](https://www.datacamp.com/community/tutorials/functions-python-tutorial)

Functions are used to encapsulate a set of relatred instructions that you want to use within your program to carry out a specific task. This helps with the organization of your code as well as code reusability. Oftent times functions accept parameters and return values, but that's not always the case.

There are three types of functions in Python:

1. Built-in functions, such as help() to ask for help, min() to get the minimum value, print() to print an object to the terminal,… You can find an overview with more of these functions here.
1. User-Defined Functions (UDFs), which are functions that users create to help them out; And
1. Anonymous functions, which are also called lambda functions because they are not declared with the standard def keyword.

##  Functions vs. Methods

A method is a function that's part of a class which we'll discuss in another lecture. Keep in mind all methods are functions but not all functions are methods.

## Parameters vs. Arguments

Parameters are the names used when defining a function or a method, and into which arguments will be mapped. In other words, arguments are the things which are supplied to any function or method call, while the function or method code refers to the arguments by their parameter names.

Consider the function

```python
def sum(a, b):
    return a + b
```

```sum``` has 2 parameters *a* and *b*. If you call the ```sum``` function with values **2** and **3** then **2** and **3** are the arguments.

## Defining User Functions

The four steps to defining a function in Python are the following:

1. Use the keyword ```def``` to declare the function and follow this up with the function name.
1. Add parameters to the function: they should be within the parentheses of the function. End your line with a colon.
1. Add statements that the functions should execute.
1. End your function with a return statement if the function should output something. Without the return statement, your function will return an object None.


```python
# takes no parameters, returns none
def say_hello():
    print('hello')
```


```python
x = say_hello()
print(type(x), x)
```


```python
# takes parameters, returns none
def say_something(message):
    print(message)
```


```python
x = say_something('hello class')
print(type(x), x)
```

### The return Statement

Sometimes it's useful to reuturn values from functions. We'll refactor our code to return values.


```python
def get_message():
    return 'hello class'

def say_something():
    message = get_message()
    print(message)
```


```python
x = get_message()
print(type(x), x)
```


```python
say_something()
```


```python
print(type(say_something()))
```


```python
x = say_something()
print(type(x), x)
```

#### returning multiple values

In python you can return values in a variety of data types including [primitive data structures](https://www.datacamp.com/community/tutorials/data-structures-python#primitive) such as integers, floats, strings, & booleans as well as [non-primitive data structures](https://www.datacamp.com/community/tutorials/data-structures-python#nonprimitive) such as arrays, lists, tuples, dictionaries, sets, and files.


```python
# returning a list
def get_messages():
    return ['hello class', 'python is great', 'here we\'re retuning a list']

messages = get_messages()
print(type(messages), messages)

for message in messages:
    print(type(message), message)
```


```python
# returning a tuple... more on tuples later
def get_message():
    return ('hello class', 3)

message = get_message()
print(type(message), message)

for i in range(0, message[1]):
    print(message[0])
```


```python
def get_message():
    return 'hello class', 3 # ('s are optional

message = get_message()
print(type(message), message)

for i in range(0, message[1]):
    print(message[0])
```


```python
message, iterations = get_message()
print(type(message), message)

for i in range(0, iterations):
    print(message)
```

## Function Arguments in Python

There are four types of arguments that Python functions can take:

1. Default arguments
1. Required arguments
1. Keyword arguments
1. Variable number of arguments

### Default Arguments

Default arguments are those that take a default value if no argument value is passed during the function call. You can assign this default value by with the assignment operator =, just like in the following example:


```python
import random

def get_random_numbers(n=1):
    if n == 1:
        return random.random()
    elif n > 1:
        numbers = []
        for i in range(0, n):
            numbers.append(random.random())
        return numbers
    
w = get_random_numbers()
print('w:', type(w), w)

x = get_random_numbers(1)
print('x:', type(x), x)

y = get_random_numbers(n=3)
print('y:', type(y), y)

z = get_random_numbers(n=-1)
print('z:', type(z), z)
```

    w: <class 'float'> 0.6141949340866538
    x: <class 'float'> 0.7236096904538915
    y: <class 'list'> [0.21366182254549937, 0.8084507728839393, 0.5814525467640246]
    z: <class 'NoneType'> None


### Required Arguments

Required arguments are mandatory and you will generate an error if they're not present. Required arguments must be passed in precisely the right order, just like in the following example:


```python
def say_something(message, number_of_times):
    for i in range(0, number_of_times):
        print(message)

# arguments passed in the proper order
say_something('hello', 3)
```

    hello
    hello
    hello



```python
# arguments passed incorrectly
say_something(3, 'hello')
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-b19729b65905> in <module>
          1 # arguments passed incorrectly
    ----> 2 say_something(3, 'hello')
    

    <ipython-input-17-70cae7a69ece> in say_something(message, number_of_times)
          1 def say_something(message, number_of_times):
    ----> 2     for i in range(0, number_of_times):
          3         print(message)
          4 
          5 # arguments passed in the proper order


    TypeError: 'str' object cannot be interpreted as an integer


### Keyword Arguments

You can use keyword arguments to make sure that you call all the parameters in the right order. You can do so by specifying their parameter name in the function call.


```python
say_something(message='hello', number_of_times=3)
say_something(number_of_times=3, message='hello')
```

    hello
    hello
    hello
    hello
    hello
    hello


### Variable Number of Arguments

In cases where you don’t know the exact number of arguments that you want to pass to a function, you can use the following syntax with *args:


```python
def add(*x):
    print(type(x), x)
    total = 0
    for x in x:
        total += x
    return total

total = add(1)
print(total)

total = add(1, 1)
print(total)

total = add(1, 2, 3, 4, 5)
print(total)
```

    <class 'tuple'> (1,)
    1
    <class 'tuple'> (1, 1)
    2
    <class 'tuple'> (1, 2, 3, 4, 5)
    15


The asterisk ```*``` is placed before the variable name that holds the values of all nonkeyword variable arguments. Note here that you might as well have passed ```*varint```, ```*var_int_args``` or any other name to the ```plus()``` function.


```python
# You can spedify any combination of required, keyword, and variable arguments.
def add(a, b, *args):
    total = a
    for arg in args:
        total += arg
    return total

total = add(1, 1)
print(total)
total = add(1, 1, 2)
print(total)
total = add(1, 2, 3, 4, 5)
print(total)
```

    1
    3
    13


### Global vs Local Variables

In general, variables that are defined inside a function body have a local scope, and those defined outside have a global scope. That means that local variables are defined within a function block and can only be accessed inside that function, while global variables can be obtained by all functions that might be in your script:


```python
# global variable
score = 0

def player_hit():
    global score
    hit_points = -10 # local variable
    score += hit_points
    
def enemy_hit():
    global score
    hit_points = 5 # local variable
    score += hit_points 

enemy_hit()
enemy_hit()
enemy_hit()
enemy_hit()
player_hit()
enemy_hit()
player_hit()

print(score)
```

    5


## Anonymous Functions in Python

Anonymous functions are also called lambda functions in Python because instead of declaring them with the standard def keyword, you use the ```lambda``` keyword.


```python
double = lambda x: x * 2
```


```python
y = double(3)
print(y)
```

    6



```python
sdlfjsdk = lambda x, n: x if n < 5 else 0
result = sdlfjsdk(4, 6)
print(result)
```

    0



```python
add = lambda x, y: x + y
```


```python
x = add(2, 3)
print(x)
```

    5


You use anonymous functions when you require a nameless function for a short period of time, and that is created at runtime. Specific contexts in which this would be relevant is when you’re working with ```filter()```, ```map()``` and ```reduce()```:

* ```filter()``` function filters the original input list on the basis of a criterion > 10. 
* ```map()``` applies a function to all items of the list
* ```reduce()``` is part of the functools library. You use this function cumulatively to the items of the my_list list, from left to right and reduce the sequence to a single value.


```python
from functools import reduce

my_list = [1,2,3,4,5,6,7,8,9,10]

# Use lambda function with `filter()`
filtered_list = list(filter(lambda x: (x * 2 > 10), my_list))

# Use lambda function with `map()`
mapped_list = list(map(lambda x: x * 2, my_list))

# Use lambda function with `reduce()`
reduced_list = reduce(lambda x, y: x + y, my_list)

print(filtered_list)
print(mapped_list)
print(reduced_list)
```

    [6, 7, 8, 9, 10]
    [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
    55


## Using main() as a Function

You can easily define a main() function and call it just like you have done with all of the other functions above:


```python
# Define `main()` function
def main():
  print("This is a main function")

main()
```

    This is a main function


However, as it stands now, the code of your ```main()``` function will be called when you import it as a module. To make sure that this doesn’t happen, you call the ```main()``` function when ```__name__ == '__main__'```.


```python
# Define `main()` function
def main():
  print("This is a main function")
  
# Execute `main()` function 
if __name__ == '__main__':
    main()
```

    This is a main function



```python

```