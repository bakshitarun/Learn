Python Functions: Explanation and Usage Guide

What is a Function in Python?

A function is a reusable block of code that performs a specific task. Functions help make code modular, readable, and maintainable.


---

Why Use Functions?

Avoid code repetition

Improve readability

Make debugging easier

Enable reuse across programs



---

Defining a Function

In Python, functions are defined using the def keyword.

def function_name(parameters):
    """Optional docstring"""
    # function body
    return value

Example

def greet(name):
    return f"Hello, {name}!"


---

Calling a Function

message = greet("Tarun")
print(message)

Output:

Hello, Tarun!


---

Function Parameters

1. Positional Parameters

def add(a, b):
    return a + b

add(3, 5)


---

2. Default Parameters

def greet(name="User"):
    return f"Hello, {name}!"

greet()
greet("Tarun")


---

3. Keyword Arguments

def introduce(name, age):
    return f"My name is {name} and I am {age} years old."

introduce(age=30, name="Tarun")


---

4. Variable-Length Arguments

*args (Non-keyword arguments)

def total(*numbers):
    return sum(numbers)

total(1, 2, 3, 4)

**kwargs (Keyword arguments)

def profile(**details):
    return details

profile(name="Tarun", role="Data Engineer")


---

Return Statement

Ends function execution

Sends a value back to the caller


def square(x):
    return x * x

If no return is used, the function returns None.


---

Lambda (Anonymous) Functions

Short, one-line functions.

square = lambda x: x * x

square(5)


---

Built-in Functions (Examples)

Function	Description	Example

len()	Length of object	len([1,2,3])
type()	Type of variable	type(10)
sum()	Sum of iterable	sum([1,2,3])
max()	Maximum value	max([1,2,3])
min()	Minimum value	min([1,2,3])



---

Docstrings

Used to document functions.

def add(a, b):
    """Returns the sum of two numbers"""
    return a + b

Access docstring:

help(add)


---

Best Practices

Use descriptive function names

Keep functions small and focused

Use docstrings

Avoid too many parameters



---

Summary

Functions are fundamental building blocks in Python that help write clean, reusable, and efficient code. Mastering functions is essential for interviews, real-world projects, and advanced Python 