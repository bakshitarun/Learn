# Python Data Structures Notes — Lists (from transcript)

> These notes are based on the pasted lecture transcript.  
> Focus: **Python Lists** — creation, indexing, slicing, modification, methods, iteration, and list comprehension.

---

## Table of Contents
- [1. What is a List?](#1-what-is-a-list)
- [2. Creating Lists](#2-creating-lists)
- [3. Accessing List Items (Indexing)](#3-accessing-list-items-indexing)
- [4. Slicing Lists](#4-slicing-lists)
- [5. Modifying List Items](#5-modifying-list-items)
- [6. Common List Methods](#6-common-list-methods)
- [7. Iterating Over Lists](#7-iterating-over-lists)
- [8. List Comprehension](#8-list-comprehension)
- [9. Nested List Comprehension](#9-nested-list-comprehension)
- [10. Common Errors & Gotchas](#10-common-errors--gotchas)
- [11. Quick Interview Tips](#11-quick-interview-tips)

---

## 1. What is a List?

A **list** is an:
- **Ordered** collection: items have a defined order and preserve insertion order.
- **Mutable** collection: items can be changed after creation.
- Can store **multiple data types** in the same list.

✅ Examples:
- `["apple", "banana", "cherry"]` (strings)
- `[1, 2, 3, 4]` (integers)
- `[1, "hello", 3.14, True]` (mixed types)

---

## 2. Creating Lists

### 2.1 Empty List
```python
lst = []
print(type(lst))   # <class 'list'>
```

### 2.2 List with Elements
```python
names = ["Croatia", "Jack", "Jacob"]
numbers = [1, 2, 3, 4, 5]
```

### 2.3 Mixed Data Type List
```python
mixed_list = [1, "text", 3.14, True]
print(mixed_list)
```

**Use case:** quick grouping of values when type consistency isn’t required.

---

## 3. Accessing List Items (Indexing)

Python uses **0-based indexing**:
```python
fruits = ["apple", "banana", "cherry", "kiwi", "guava"]

print(fruits[0])  # apple
print(fruits[2])  # cherry
print(fruits[4])  # guava
```

### Negative Indexing
Negative indexes count from the end:
```python
print(fruits[-1])  # guava (last element)
print(fruits[-2])  # kiwi
```

**Use case:** access last items without knowing list length.

---

## 4. Slicing Lists

Slicing returns a **sub-list**.

### Syntax
```python
lst[start:end]   # end is excluded
```

### Examples
```python
fruits = ["apple", "banana", "cherry", "kiwi", "guava"]

print(fruits[1:])     # from index 1 to end
# ['banana', 'cherry', 'kiwi', 'guava']

print(fruits[1:3])    # index 1 and 2 only
# ['banana', 'cherry']
```

### Step Size (Double Colon)
```python
numbers = [1,2,3,4,5,6,7,8,9,10]

print(numbers[::2])    # step by 2
# [1, 3, 5, 7, 9]

print(numbers[::-1])   # reverse list using slicing
# [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

**Use case:** sampling, reversing, extracting segments of data.

---

## 5. Modifying List Items

Lists are **mutable**, so you can replace items using indexing:

```python
fruits = ["apple", "banana", "cherry", "kiwi", "guava"]

fruits[1] = "watermelon"
print(fruits)
# ['apple', 'watermelon', 'cherry', 'kiwi', 'guava']
```

### Replacing a Slice (⚠️ Important Gotcha)
If you do:
```python
fruits[1:] = "watermelon"
print(fruits)
```

You’ll get character-by-character insertion (because a string is iterable):
```python
['apple', 'w', 'a', 't', 'e', 'r', 'm', 'e', 'l', 'o', 'n']
```

✅ Correct way:
```python
fruits[1:] = ["watermelon"]
```

---

## 6. Common List Methods

### 6.1 `append()` — add at the end
```python
fruits.append("orange")
```

### 6.2 `insert(index, item)` — add at a specific index
```python
fruits.insert(1, "watermelon")
```

### 6.3 `remove(item)` — remove first occurrence
```python
fruits.remove("banana")
```
⚠️ Removes only the **first matching** item.

### 6.4 `pop()` — remove and return last element (or by index)
```python
popped = fruits.pop()
print(popped)   # last element
```

### 6.5 `index(item)` — get index of first occurrence
```python
idx = fruits.index("cherry")
print(idx)
```

### 6.6 `count(item)` — count occurrences
```python
count_banana = fruits.count("banana")
```

### 6.7 `sort()` — sort ascending (in-place)
```python
fruits.sort()
```

### 6.8 `reverse()` — reverse list (in-place)
```python
fruits.reverse()
```

### 6.9 `clear()` — remove all elements
```python
fruits.clear()
print(fruits)   # []
```

---

## 7. Iterating Over Lists

### 7.1 Basic Loop
```python
numbers = [1,2,3,4,5]

for num in numbers:
    print(num)
```

### 7.2 Iterating with Index using `enumerate()`
```python
numbers = [1,2,3,4,5]

for idx, num in enumerate(numbers):
    print(idx, num)
```

**Use case:** when you need both index + value.

---

## 8. List Comprehension

List comprehensions create lists in a **concise** way.

### 8.1 Basic Syntax
```python
[expression for item in iterable]
```

### Example: Squares
```python
squares = [x*x for x in range(10)]
print(squares)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### 8.2 With Condition
Syntax:
```python
[expression for item in iterable if condition]
```

Example: even numbers
```python
evens = [num for num in range(10) if num % 2 == 0]
print(evens)
# [0, 2, 4, 6, 8]
```

**Use case:** transformations + filtering in one line.

---

## 9. Nested List Comprehension

Used when iterating over **two iterables**.

### Syntax (common pattern)
```python
[(i, j) for i in iterable1 for j in iterable2]
```

### Example: Pairing Two Lists
```python
list1 = [1, 2]
list2 = ["a", "b", "c", "d"]

pairs = [(i, j) for i in list1 for j in list2]
print(pairs)
# [(1, 'a'), (1, 'b'), (1, 'c'), (1, 'd'),
#  (2, 'a'), (2, 'b'), (2, 'c'), (2, 'd')]
```

**Use case:** Cartesian product, generating combinations.

---

## 10. Common Errors & Gotchas

### ✅ `NameError`
Using a variable before defining it:
```python
print(names)  # NameError if `names` not created yet
```

### ✅ Slice replacement with strings
```python
fruits[1:] = "watermelon"  # inserts characters
```

### ✅ Negative slicing confusion
Negative start/end can be confusing. Rule:
- Slicing still follows `start -> end` direction with a default positive step.
- To slice backwards, you need a **negative step** (e.g. `[::-1]`).

---

## 11. Quick Interview Tips

- **List vs Tuple:** list is mutable, tuple is immutable.
- **append vs extend:** append adds one item; extend adds all items from iterable.
- **sort vs sorted:** `sort()` modifies list in place; `sorted()` returns a new list.
- **List comprehension:** clean, fast, readable — but don’t overcomplicate it.

---

## Summary
- Lists are **ordered**, **mutable**, and can store **mixed types**.
- Indexing and slicing are core to extracting data.
- List methods (`append`, `insert`, `pop`, etc.) handle most operations.
- List comprehensions help write **cleaner** and **more efficient** code.
