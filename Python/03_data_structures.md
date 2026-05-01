# Data Structures: Lists, Tuples, Sets & Dictionaries

---

## Quick Reference

| Feature | List `[ ]` | Tuple `( )` | Set `{ }` | Dict `{k:v}` |
|---------|-----------|------------|---------|-------------|
| Ordered | Yes | Yes | No | Yes (3.7+) |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: No |
| Access By | Index | Index | Membership | Key |
| Best For | Dynamic sequences | Fixed records | Unique items | Key-value lookups |

---

## 6. Lists

An ordered, changeable collection. Index starts at `0`. Duplicates allowed.

```python
fruits = ["apple", "banana", "cherry", "kiwi", "guava"]

fruits[0]     # 'apple'              — first item
fruits[-1]    # 'guava'              — last item
fruits[1:3]   # ['banana', 'cherry'] — slice
fruits[::-1]  # reversed list
```

### Key Methods

| Method | Action | Modifies Original? |
|--------|--------|--------------------|
| `.append(x)` | Add x to end | Yes |
| `.extend(iterable)` | Add all items from another list/iterable | Yes |
| `.insert(i, x)` | Add x at index i | Yes |
| `.remove(x)` | Remove first occurrence of x | Yes |
| `.pop()` | Remove & return last item | Yes |
| `.sort()` | Sort ascending in place | Yes |
| `.reverse()` | Reverse in place | Yes |
| `.index(x)` | Find position of x | No |
| `.count(x)` | Count occurrences of x | No |

### List Comprehensions

```python
# Syntax: [expression for item in iterable if condition]

squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

evens = [n for n in range(10) if n % 2 == 0]
# [0, 2, 4, 6, 8]

upper = [name.upper() for name in ["alice", "bob"]]
# ['ALICE', 'BOB']
```

### Other Useful List Operations

```python
sugar_levels = [1, 2, 3, 4, 5]
max(sugar_levels)   # 5
min(sugar_levels)   # 1

# Concatenate two lists
base = ["water", "milk"]
extra = ["ginger"]
full = base + extra         # ['water', 'milk', 'ginger']

# Repeat a list
strong_brew = ["black tea", "water"] * 3
# ['black tea', 'water', 'black tea', 'water', 'black tea', 'water']

# extend — add all items from another list (modifies in place)
chai = ["water", "milk"]
spices = ["ginger", "cardamom"]
chai.extend(spices)
# chai is now ['water', 'milk', 'ginger', 'cardamom']
# vs append: chai.append(spices) → ['water', 'milk', ['ginger', 'cardamom']]
```

> `.extend()` flattens the items in. `.append()` adds the whole object as a single element.

### bytearray — Mutable Raw Bytes

A mutable sequence of bytes. Used when working with binary data, network payloads, or raw file content.

```python
raw_data = bytearray(b"CINNAMON")
raw_data = raw_data.replace(b"CINNA", b"CARD")
print(raw_data)   # bytearray(b'CARDMON')
```

| Type | Mutable? | Use Case |
|------|----------|---------|
| `bytes` | No | Immutable binary data |
| `bytearray` | Yes | Mutable binary data you need to modify |

---

Like a list, but **immutable** — can't be changed after creation.

```python
coords = (10.5, 20.3)
mixed  = (1, "Hello", 3.14, True)
packed = 1, "Hello", 3.14    # parentheses optional

coords[0]   # 10.5
coords[-1]  # 20.3

numbers = (1, 2, 3)
numbers[0] = 99   # TypeError! Tuples can't be changed
```

### Unpacking

```python
point = (10, 20, 30)
x, y, z = point          # x=10, y=20, z=30

# Extended unpacking
first, *middle, last = (1, 2, 3, 4, 5, 6)
# first=1  middle=[2,3,4,5]  last=6
```

### Lists vs Tuples

| Feature | List `[ ]` | Tuple `( )` |
|---------|-----------|------------|
| Mutable | Yes | No |
| Performance | Slightly slower | Slightly faster |
| Memory | More | Less |
| Can be dict key | No | Yes |
| Use case | Dynamic data | Fixed data (coords, configs) |

---

## 8. Sets

An unordered collection where every item is **unique**. Duplicates are auto-removed.

```python
my_set = {1, 2, 3, 4, 5}

# IMPORTANT: {} creates a dict, NOT a set!
empty_set = set()              # correct way to make empty set

my_set = set([1, 2, 2, 3, 4])
print(my_set)                  # {1, 2, 3, 4}
```

### Adding & Removing

| Method | Element Exists | Element Missing |
|--------|---------------|-----------------|
| `.add(x)` | Does nothing | Adds it |
| `.remove(x)` | Removes it | Raises `KeyError`! |
| `.discard(x)` | Removes it | Does nothing (safer) |
| `.pop()` | Removes arbitrary item | — |
| `.clear()` | Removes everything | — |

### Set Operations

```python
a = {1, 2, 3, 4, 5}
b = {4, 5, 6, 7, 8}

a.union(b)                 # {1,2,3,4,5,6,7,8} — all items
a.intersection(b)          # {4, 5}             — in both
a.difference(b)            # {1, 2, 3}          — in a, not b
a.symmetric_difference(b)  # {1,2,3,6,7,8}      — in one, not both
```

### Practical: Remove Duplicates

```python
names = ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob']
unique = set(names)   # {'Alice', 'Bob', 'Charlie'}
```

---

## 9. Dictionaries

Stores **key-value pairs**. Keys must be unique and immutable. Values can be anything.

```python
student = {'name': 'Krish', 'age': 32, 'grade': 'A'}

student['grade']                 # 'A'    — KeyError if missing!
student.get('grade')             # 'A'    — None if missing
student.get('last_name', 'N/A')  # 'N/A'  — custom default
```

### Modifying

```python
student['age'] = 33         # update existing key
student['address'] = 'India'  # add new key
del student['grade']          # delete a key

# Copying — IMPORTANT
wrong = student        # both point to the SAME dict!
right = student.copy() # independent copy
```

### Iterating

```python
for key in student.keys():
    print(key)

for value in student.values():
    print(value)

for key, value in student.items():
    print(f"{key}: {value}")
```

### `[ ]` vs `.get()`

| Method | Key Exists | Key Missing |
|--------|-----------|-------------|
| `dict["key"]` | Returns value | Raises `KeyError`! |
| `dict.get("key")` | Returns value | Returns `None` |
| `dict.get("key", default)` | Returns value | Returns default |

> Use `.get()` when a key might not exist. Use `[]` when you're certain it's there.

### Dictionary Comprehensions

```python
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

evens = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### Practical: Count Frequencies

```python
numbers = [1, 2, 2, 3, 3, 3, 4]
freq = {}
for n in numbers:
    freq[n] = freq.get(n, 0) + 1
# {1: 1, 2: 2, 3: 3, 4: 1}
```

### Dict as a Dispatch / Lookup Table

Replace long `if/elif` chains with a dictionary lookup — faster, shorter, and easier to extend:

```python
# Instead of this:
if coupon == "P20":
    discount = 0.20
elif coupon == "F10":
    discount = 0.10
# ...many more...

# Do this:
discounts = {
    "P20": (0.20, 0),   # (percent, fixed)
    "F10": (0.50, 0),
    "P50": (0.00, 10),
}

percent, fixed = discounts.get(coupon, (0, 0))  # unknown coupon → no crash
discount = total * percent + fixed
```

| Approach | Best For | Limitation |
|----------|---------|------------|
| `if/elif` | Complex conditions, ranges | Verbose with many branches |
| `match/case` | Fixed string/int values | Python 3.10+ only |
| Dict lookup | Code-to-value mappings | Keys must be hashable; no ranges |

---

## Quick Tips

- Use `set()` to remove duplicates from a list
- Use `.discard()` over `.remove()` when the element might not exist
- Always copy dicts with `.copy()` — assignment creates a reference, not a copy
- Use dict dispatch tables to replace long `if/elif` chains on fixed values
