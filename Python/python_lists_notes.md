# Python Lists - Complete Study Guide

## Table of Contents
1. [Introduction to Lists](#introduction-to-lists)
2. [Creating Lists](#creating-lists)
3. [Accessing List Items](#accessing-list-items)
4. [Modifying List Items](#modifying-list-items)
5. [List Methods](#list-methods)
6. [List Slicing](#list-slicing)
7. [Iterating Over Lists](#iterating-over-lists)
8. [List Comprehension](#list-comprehension)
9. [Common Patterns and Best Practices](#common-patterns-and-best-practices)

---

## Introduction to Lists

**Definition:** Lists are ordered, mutable collections of items in Python.

**Key Properties:**
- **Ordered**: Items maintain their position and can be accessed by index
- **Mutable**: You can change, add, or remove items after creation
- **Heterogeneous**: Can contain items of different data types (strings, integers, floats, booleans, etc.)

---

## Creating Lists

### Empty List
```python
# Create an empty list
my_list = []
print(type(my_list))  # Output: <class 'list'>
```

### List with Elements
```python
# List of strings
students = ["Alice", "Bob", "Charlie"]

# List of numbers
temperatures = [23, 25, 19, 30, 28]

# Mixed data types
employee_data = [101, "John Smith", 55000.50, True]
print(employee_data)  # Output: [101, 'John Smith', 55000.50, True]
```

---

## Accessing List Items

### Index-Based Access
Python uses **zero-based indexing** (first element is at index 0).

```python
cities = ["Tokyo", "Paris", "London", "Dubai", "Sydney"]

# Access first element
print(cities[0])  # Output: Tokyo

# Access third element
print(cities[2])  # Output: London

# Access last element (two ways)
print(cities[4])   # Output: Sydney
print(cities[-1])  # Output: Sydney (negative indexing from the end)
```

### Negative Indexing
Access elements from the end of the list using negative indices.

```python
cities = ["Tokyo", "Paris", "London", "Dubai", "Sydney"]

print(cities[-1])  # Last element: Sydney
print(cities[-2])  # Second-to-last: Dubai
print(cities[-3])  # Third-to-last: London
```

### Range Access (Slicing Preview)
```python
cities = ["Tokyo", "Paris", "London", "Dubai", "Sydney"]

# From index 1 to end
print(cities[1:])     # Output: ['Paris', 'London', 'Dubai', 'Sydney']

# From index 1 to 3 (excludes index 3)
print(cities[1:3])    # Output: ['Paris', 'London']
```

---

## Modifying List Items

### Replace Single Element
```python
colors = ["red", "green", "blue", "yellow", "purple"]

# Replace green with orange
colors[1] = "orange"
print(colors)  # Output: ['red', 'orange', 'blue', 'yellow', 'purple']
```

### Replace Multiple Elements
```python
colors = ["red", "green", "blue", "yellow", "purple"]

# Note: Replacing with a string replaces character by character
colors[1:] = "pink"
print(colors)  # Output: ['red', 'p', 'i', 'n', 'k']

# Use list methods like append() for proper word addition
```

---

## List Methods

### 1. append() - Add Item to End
Adds a single element to the end of the list.

```python
animals = ["dog", "cat", "elephant"]
animals.append("tiger")
print(animals)  # Output: ['dog', 'cat', 'elephant', 'tiger']
```

### 2. insert() - Add Item at Specific Index
Inserts an element at a specified position.

```python
animals = ["dog", "cat", "elephant"]
animals.insert(1, "lion")  # Insert at index 1
print(animals)  # Output: ['dog', 'lion', 'cat', 'elephant']
```

### 3. remove() - Remove First Occurrence
Removes the first occurrence of a specified value.

```python
animals = ["dog", "cat", "elephant", "cat"]
animals.remove("cat")  # Removes first cat
print(animals)  # Output: ['dog', 'elephant', 'cat']
```

### 4. pop() - Remove and Return Last Item
Removes and returns the last element (or element at specified index).

```python
animals = ["dog", "cat", "elephant", "tiger"]
popped_animal = animals.pop()
print(popped_animal)  # Output: tiger
print(animals)        # Output: ['dog', 'cat', 'elephant']

# Pop from specific index
second = animals.pop(1)
print(second)  # Output: cat
```

### 5. index() - Find Index of Element
Returns the index of the first occurrence of a value.

```python
animals = ["dog", "cat", "elephant", "lion"]
index = animals.index("elephant")
print(index)  # Output: 2
```

### 6. count() - Count Occurrences
Returns the number of times a value appears in the list.

```python
animals = ["dog", "cat", "elephant", "cat"]
cat_count = animals.count("cat")
print(cat_count)  # Output: 2
```

### 7. sort() - Sort List in Place
Sorts the list in ascending order (modifies the original list).

```python
animals = ["elephant", "dog", "cat", "lion"]
animals.sort()
print(animals)  # Output: ['cat', 'dog', 'elephant', 'lion']

# For numbers
scores = [85, 92, 78, 95, 88]
scores.sort()
print(scores)  # Output: [78, 85, 88, 92, 95]
```

### 8. reverse() - Reverse List Order
Reverses the elements of the list in place.

```python
animals = ["dog", "cat", "elephant"]
animals.reverse()
print(animals)  # Output: ['elephant', 'cat', 'dog']
```

### 9. clear() - Remove All Items
Removes all elements from the list.

```python
animals = ["dog", "cat", "elephant"]
animals.clear()
print(animals)  # Output: []
```

---

## List Slicing

Slicing allows you to extract portions of a list using the syntax: `list[start:end:step]`

### Basic Slicing
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Elements from index 2 to 5 (excludes 5)
print(numbers[2:5])    # Output: [3, 4, 5]

# Elements from index 5 to end
print(numbers[5:])     # Output: [6, 7, 8, 9, 10]

# Elements from start to index 5
print(numbers[:5])     # Output: [1, 2, 3, 4, 5]

# All elements
print(numbers[:])      # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Step Size in Slicing
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Every 2nd element
print(numbers[::2])    # Output: [1, 3, 5, 7, 9]

# Every 3rd element
print(numbers[::3])    # Output: [1, 4, 7, 10]

# Reverse the list
print(numbers[::-1])   # Output: [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

# Every 2nd element from the end
print(numbers[::-2])   # Output: [10, 8, 6, 4, 2]
```

### Practical Slicing Examples
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# First 5 elements
first_five = numbers[:5]

# Last 3 elements
last_three = numbers[-3:]

# Middle elements (exclude first and last)
middle = numbers[1:-1]

# Create a copy of the list
list_copy = numbers[:]
```

---

## Iterating Over Lists

### Basic For Loop
```python
countries = ["USA", "Canada", "Mexico", "Brazil", "Argentina"]

for country in countries:
    print(country)
# Output:
# USA
# Canada
# Mexico
# Brazil
# Argentina
```

### Iterate with Index using enumerate()
The `enumerate()` function provides both index and value.

```python
products = ["Laptop", "Mouse", "Keyboard", "Monitor", "Headphones"]

for index, product in enumerate(products):
    print(f"Index {index}: {product}")
# Output:
# Index 0: Laptop
# Index 1: Mouse
# Index 2: Keyboard
# Index 3: Monitor
# Index 4: Headphones
```

### Practical Examples
```python
# Sum all numbers
prices = [19.99, 25.50, 15.00, 30.25, 12.75]
total = 0
for price in prices:
    total += price
print(total)  # Output: 103.49

# Find maximum value
grades = [78, 92, 65, 88, 95]
max_grade = grades[0]
for grade in grades:
    if grade > max_grade:
        max_grade = grade
print(max_grade)  # Output: 95
```

---

## List Comprehension

List comprehension provides a concise way to create lists. It's more efficient and readable than traditional loops.

### Basic Syntax
```
[expression for item in iterable]
```

### Simple Examples

**Traditional approach:**
```python
# Cube numbers using traditional loop
cubes = []
for x in range(6):
    cubes.append(x ** 3)
print(cubes)  # Output: [0, 1, 8, 27, 64, 125]
```

**List comprehension:**
```python
# Cube numbers using list comprehension
cubes = [x ** 3 for x in range(6)]
print(cubes)  # Output: [0, 1, 8, 27, 64, 125]
```

### List Comprehension with Condition
```
[expression for item in iterable if condition]
```

**Example: Filter multiples of 5**

Traditional approach:
```python
multiples_of_5 = []
for i in range(50):
    if i % 5 == 0:
        multiples_of_5.append(i)
print(multiples_of_5)  # Output: [0, 5, 10, 15, 20, 25, 30, 35, 40, 45]
```

List comprehension:
```python
multiples_of_5 = [num for num in range(50) if num % 5 == 0]
print(multiples_of_5)  # Output: [0, 5, 10, 15, 20, 25, 30, 35, 40, 45]
```

### More Examples

**Extract numbers greater than 50:**
```python
ages = [23, 45, 67, 34, 89, 12, 56, 78]
seniors = [age for age in ages if age > 50]
print(seniors)  # Output: [67, 89, 56, 78]
```

**Multiply each number by 10:**
```python
multiplied = [x * 10 for x in range(1, 6)]
print(multiplied)  # Output: [10, 20, 30, 40, 50]
```

**Convert temperatures from Celsius to Fahrenheit:**
```python
celsius = [0, 10, 20, 30, 40]
fahrenheit = [(temp * 9/5) + 32 for temp in celsius]
print(fahrenheit)  # Output: [32.0, 50.0, 68.0, 86.0, 104.0]
```

### Nested List Comprehension
```
[expression for item1 in iterable1 for item2 in iterable2]
```

**Example: Create coordinate pairs**

Traditional approach:
```python
x_coords = [1, 2, 3]
y_coords = [10, 20, 30]
coordinates = []
for x in x_coords:
    for y in y_coords:
        coordinates.append([x, y])
print(coordinates)
```

List comprehension:
```python
x_coords = [1, 2, 3]
y_coords = [10, 20, 30]
coordinates = [[x, y] for x in x_coords for y in y_coords]
print(coordinates)
# Output: [[1, 10], [1, 20], [1, 30], [2, 10], [2, 20], [2, 30], [3, 10], [3, 20], [3, 30]]
```

### List Comprehension with Function Calls

**Example: Calculate squares using a function**
```python
def square(n):
    return n ** 2

numbers = [1, 2, 3, 4, 5]
squared = [square(num) for num in numbers]
print(squared)  # Output: [1, 4, 9, 16, 25]
```

**Example: Filter strings by length**
```python
languages = ["Python", "Java", "C", "JavaScript", "Ruby", "Go"]
short_names = [lang for lang in languages if len(lang) <= 4]
print(short_names)  # Output: ['Java', 'C', 'Ruby', 'Go']
```

---

## Common Patterns and Best Practices

### 1. Check if List is Empty
```python
my_list = []

# Pythonic way
if not my_list:
    print("List is empty")

# Less Pythonic
if len(my_list) == 0:
    print("List is empty")
```

### 2. Copy a List
```python
original = [100, 200, 300, 400, 500]

# Shallow copy using slicing
copy1 = original[:]

# Shallow copy using list()
copy2 = list(original)

# Shallow copy using copy method
copy3 = original.copy()
```

### 3. Combine Lists
```python
morning_tasks = ["breakfast", "exercise", "shower"]
evening_tasks = ["dinner", "reading", "sleep"]

# Using + operator
combined = morning_tasks + evening_tasks
print(combined)  # Output: ['breakfast', 'exercise', 'shower', 'dinner', 'reading', 'sleep']

# Using extend()
morning_tasks.extend(evening_tasks)
print(morning_tasks)  # Output: ['breakfast', 'exercise', 'shower', 'dinner', 'reading', 'sleep']
```

### 4. Remove Duplicates
```python
scores = [85, 90, 85, 78, 90, 92, 78]
unique = list(set(scores))
print(unique)  # Output: [78, 85, 90, 92] (order may vary)

# Preserve order
unique_ordered = []
for score in scores:
    if score not in unique_ordered:
        unique_ordered.append(score)
print(unique_ordered)  # Output: [85, 90, 78, 92]
```

### 5. Find Maximum and Minimum
```python
temperatures = [23, 31, 18, 27, 35, 22]

maximum = max(temperatures)
minimum = min(temperatures)
print(f"Max: {maximum}, Min: {minimum}")  # Output: Max: 35, Min: 18
```

### 6. Sum and Average
```python
expenses = [45.50, 23.00, 67.80, 12.30, 89.40]

total = sum(expenses)
average = sum(expenses) / len(expenses)
print(f"Sum: {total}, Average: {average:.2f}")  # Output: Sum: 238.0, Average: 47.60
```

---

## Summary

### Key Takeaways:
1. **Lists are versatile**: They can store any type of data and can be modified after creation
2. **Index starts at 0**: Python uses zero-based indexing
3. **Negative indexing**: Access elements from the end using negative indices
4. **Rich set of methods**: append(), insert(), remove(), pop(), sort(), reverse(), etc.
5. **Slicing is powerful**: Extract portions of lists with `[start:end:step]` syntax
6. **List comprehension**: Write cleaner, more efficient code for list operations
7. **Enumerate for indexing**: Use `enumerate()` when you need both index and value

### Best Practices:
- Use list comprehension for simple transformations (more readable and faster)
- Use meaningful variable names
- Be careful with mutable operations (lists are mutable)
- Consider using built-in functions like `sum()`, `max()`, `min()` for common operations
- Remember that list comprehensions create new lists (don't modify original)

---

## Practice Exercises

Try these exercises to reinforce your understanding:

1. Create a list of numbers from 1 to 30 and extract all numbers divisible by 7
2. Given a list of prices, create a new list with 20% tax added to each price
3. Reverse a list without using the reverse() method or [::-1]
4. Remove all numbers less than 10 from a list using list comprehension
5. Create a 4x4 matrix (nested lists) using list comprehension
6. Find the third smallest number in a list
7. Create a list of factorials for numbers 1 through 10

---

**Happy Learning! 🐍**

*Remember: Practice is key to mastering lists. Try to solve problems daily and experiment with different methods.*
