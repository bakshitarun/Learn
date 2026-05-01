# Functions & Comprehensions

---

## 10. Functions

A function is a named, reusable block of code. Define once with `def`, call anywhere. Keeps code DRY (Don't Repeat Yourself).

### Defining & Calling

```python
def greet(name):
    return f"Hello, {name}!"

message = greet("Tarun")   # "Hello, Tarun!"
```

### Parameters & Return Values

```python
def add(a, b):
    return a + b     # sends value back to caller

result = add(3, 4)   # 7
```

> Without `return`, a function returns `None`.

### Default Parameter Values

```python
def make_chai(base="black tea", sugar=2, milk=True):
    milk_label = "with milk" if milk else "without milk"
    return f"{base}, sugar={sugar}, {milk_label}"

make_chai()                      # all defaults
make_chai("green tea", sugar=0)  # override specific params
```

### `*args` and `**kwargs`

```python
# *args — any number of positional arguments → collected as a tuple
def list_spices(*spices):
    for spice in spices:
        print(f"  - {spice}")

list_spices("ginger", "cardamom", "cinnamon")

# **kwargs — any number of keyword arguments → collected as a dict
def order_chai(**details):
    for key, value in details.items():
        print(f"  {key}: {value}")

order_chai(type="Masala", size="Large", sugar=3)
```

### `enumerate` and `zip`

```python
spices = ["cardamom", "ginger", "cinnamon"]
grams  = [2, 5, 3]

# enumerate — index + value together
for index, spice in enumerate(spices, start=1):
    print(f"{index}. {spice}")
# 1. cardamom  2. ginger  3. cinnamon

# zip — pair two lists
for name, g in zip(spices, grams):
    print(f"{name}: {g}g")
# cardamom: 2g  ginger: 5g  cinnamon: 3g
```

---

## 11. Comprehensions

One-liners that create a new collection by transforming or filtering an iterable. Replaces multi-line `for` + `append` patterns.

### List — Transform

```python
# Traditional loop
squares = []
for x in range(10):
    squares.append(x**2)

# Comprehension — same result
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### List — Filter

```python
evens = [n for n in range(10) if n % 2 == 0]
# [0, 2, 4, 6, 8]

long_words = [w for w in ["hi", "hello", "hey", "world"] if len(w) > 3]
# ['hello', 'world']
```

### Ternary in Comprehension

```python
# if/else BEFORE the for = transform each item differently
labels = ["even" if n % 2 == 0 else "odd" for n in range(6)]
# ['even', 'odd', 'even', 'odd', 'even', 'odd']

# Clamp negatives to 0
nums = [4, -1, 7, -3, 0, 2]
clamped = [n if n >= 0 else 0 for n in nums]
# [4, 0, 7, 0, 0, 2]
```

### Dict Comprehension

```python
spices = ["cardamom", "ginger", "cinnamon"]

lengths = {s: len(s) for s in spices}
# {'cardamom': 8, 'ginger': 6, 'cinnamon': 8}

# With filter
short = {s: len(s) for s in spices if len(s) <= 6}
# {'ginger': 6}
```

### Set Comprehension

```python
first_letters = {spice[0] for spice in spices}
# {'c', 'g'}  — unordered, no duplicates
```

### Nested — Flatten a 2D List

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [num for row in matrix for num in row]
# [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

## 15. Lambda, Map, Filter & Sorted

Functional tools for quick transforms and sorting — no need for a full `def`.

### lambda — Inline Anonymous Function

```python
double = lambda x: x * 2
double(5)   # 10

ratio = lambda spice, water: round(spice / water, 4)
ratio(5, 250)   # 0.02
```

> Use `lambda` only for short single expressions. For anything more complex, write a named `def`.

### map — Apply to Every Item

```python
grams  = [10, 20, 30, 40]
ounces = list(map(lambda g: round(g * 0.03527, 2), grams))
# [0.35, 0.71, 1.06, 1.41]

names   = ["  ginger ", " cardamom"]
cleaned = list(map(lambda s: s.strip().lower(), names))
# ['ginger', 'cardamom']
```

> Wrap `map()` in `list()` to get a list back.

### filter — Keep Matching Items

```python
sugar_levels = [0, 1, 2, 3, 4, 5]
sweet = list(filter(lambda s: s >= 3, sugar_levels))
# [3, 4, 5]

spices     = ["ginger", "cardamom", "star anise", "cloves"]
long_names = list(filter(lambda s: len(s) > 6, spices))
# ['cardamom', 'star anise']
```

### sorted — Return a Sorted Copy

```python
brew_times = [5, 2, 8, 3, 7]
sorted(brew_times)               # [2, 3, 5, 7, 8]
sorted(brew_times, reverse=True) # [8, 7, 5, 3, 2]

# Sort by a field in a dict
orders = [{"name": "Priya", "sugar": 2}, {"name": "Arjun", "sugar": 4}]
by_sugar = sorted(orders, key=lambda o: o["sugar"])

# Sort strings by length
sorted(spices, key=len)
# ['ginger', 'cloves', 'cardamom', 'star anise']
```

### Tool Comparison

| Tool | What It Does | Returns |
|------|-------------|---------|
| `lambda` | Inline anonymous function | A function object |
| `map()` | Apply function to every item | map object → wrap in `list()` |
| `filter()` | Keep items where function is `True` | filter object → wrap in `list()` |
| `sorted()` | Sorted copy of iterable | New list — original unchanged |
| `list.sort()` | Sort in place | `None` — modifies original |

---

## Quick Tips

- Keep functions under ~20 lines — split into helpers if longer
- Use `enumerate()` when you need both the index and value in a loop
- Use `zip()` to pair multiple lists cleanly
- Prefer list comprehensions over `map()`/`filter()` when readability matters
- Use `sorted(key=lambda ...)` for custom sort orders — it's the cleanest approach
