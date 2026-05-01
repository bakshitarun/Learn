# Variables, Data Types & Operators

---

## 1. Variables

A variable is a named container for a value. Python figures out the type automatically — no declaration needed.

```python
age = 32             # int
height = 6.1         # float
name = "Tarun"       # str
is_student = True    # bool
```

### Naming Rules

| Rule | Valid | Invalid | Why |
|------|-------|---------|-----|
| Start with letter or `_` | `first_name` | `2age` | Starts with a number |
| Letters, numbers, `_` only | `user_1` | `first-name` | Hyphens not allowed |
| No special characters | `_value` | `@name` | `@` not permitted |
| Case-sensitive | `Name` ≠ `name` | — | Treated as different vars |

> **Best practice:** use `snake_case` — `first_name`, `total_score`, `is_active`

### Dynamic Typing

The same variable can hold any type at any time:

```python
var = 10        # int
var = "Hello"   # now a string
var = 3.14      # now a float
print(type(var))  # <class 'float'>
```

### Type Conversion

```python
str(25)       # '25'
int('25')     # 25
int("Krish")  # ValueError — letters can't become int
```

> ⚠️ `input()` always returns a string. Use `int(input(...))` or `float(input(...))` for numbers.

### Object Identity — `id()`

Every value in Python lives somewhere in memory. `id()` returns that memory address. When you reassign a variable, Python points it at a new object — the old one stays untouched.

```python
sugar_amount = 2
print(id(sugar_amount))   # e.g. 140234567

sugar_amount = 12
print(id(sugar_amount))   # different address — new object
```

```python
spice_mix = set()
print(id(spice_mix))      # e.g. 140234999
spice_mix.add("Ginger")
print(id(spice_mix))      # SAME address — mutated in place, not replaced
```

> Immutable types (`int`, `str`, `tuple`) get a new `id` on every change. Mutable types (`list`, `set`, `dict`) keep the same `id` when modified in place.

---

## 2. Data Types

### Basic Types

| Type | Keyword | Example | Description |
|------|---------|---------|-------------|
| Integer | `int` | `age = 35` | Whole numbers |
| Float | `float` | `height = 5.11` | Decimal numbers |
| String | `str` | `name = "Krish"` | Text in quotes |
| Boolean | `bool` | `is_true = True` | `True` or `False` only |

### Collection Types

| Type | Syntax | Ordered? | Mutable? | Duplicates? |
|------|--------|----------|----------|-------------|
| List | `[1, 2, 3]` | Yes | Yes | Yes |
| Tuple | `(1, 2, 3)` | Yes | No | Yes |
| Set | `{1, 2, 3}` | No | Yes | No |
| Dictionary | `{"a": 1}` | Yes (3.7+) | Yes | Keys: No |

### Boolean as a Number — Upcasting

`True` and `False` are secretly `1` and `0`. When mixed with numbers, Python quietly promotes the bool to an int:

```python
is_boiling = True
stir_count = 5
total_actions = stir_count + is_boiling   # 5 + 1 = 6
print(total_actions)   # 6

bool(0)       # False
bool(1)       # True
bool("")      # False
bool("chai")  # True
```

### Precise Numeric Types

The built-in `float` has precision limits (IEEE 754). Use `Decimal` for exact decimal arithmetic, and `Fraction` for exact rational numbers:

```python
from decimal import Decimal
from fractions import Fraction
import sys

# Float precision problem:
print(0.1 + 0.2)          # 0.30000000000000004

# Decimal — exact decimal math (finance, measurements)
print(Decimal("0.1") + Decimal("0.2"))   # 0.3

# Fraction — exact rational math
print(Fraction(1, 3) + Fraction(1, 6))  # 1/2

# Float system limits
print(sys.float_info)   # max, min, epsilon, dig...
```

> Use `Decimal` for money calculations. Use `float` for general math where tiny rounding errors are acceptable.

### Common Error — Type Mismatch

```python
# WRONG
result = "Hello" + 5       # TypeError!

# CORRECT
result = "Hello" + str(5)  # "Hello5"
```

---

## 3. Operators

### Arithmetic

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division (float) | `10 / 5` | `2.0` |
| `//` | Floor Division | `21 // 5` | `4` |
| `%` | Modulus | `10 % 3` | `1` |
| `**` | Exponentiation | `2 ** 8` | `256` |

> ⚠️ `/` always returns a float. Use `//` when you need a whole number.

### Comparison (always return `True` or `False`)

```python
10 == 10   # True
10 != 5    # True
45 > 55    # False
45 < 55    # True
45 >= 45   # True
44 <= 45   # True
```

### Logical

| Operator | Returns `True` When |
|----------|---------------------|
| `and` | Both sides are `True` |
| `or` | At least one side is `True` |
| `not` | The value is `False` |

### Augmented Assignment

Shorthand for reading and writing the same variable:

| Operator | Meaning | Example | Same As |
|----------|---------|---------|---------|
| `+=` | Add and assign | `x += 3` | `x = x + 3` |
| `-=` | Subtract and assign | `x -= 3` | `x = x - 3` |
| `*=` | Multiply and assign | `x *= 3` | `x = x * 3` |
| `/=` | Divide and assign | `x /= 3` | `x = x / 3` |
| `//=` | Floor divide and assign | `x //= 3` | `x = x // 3` |
| `%=` | Modulus and assign | `x %= 3` | `x = x % 3` |
| `**=` | Exponentiate and assign | `x **= 3` | `x = x ** 3` |

```python
temperature = 40
temperature += 15   # now 55
```

---

## Quick Tips

- Use `//` and `%` together for conversions (e.g. seconds → minutes, even/odd checks)
- Chain comparisons: `1 < x < 10` instead of `x > 1 and x < 10`
- Never use `=` when you mean `==` — the classic bug
- Use `+=` for loop counters and running totals
