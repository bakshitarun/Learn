# Type Hints & Modules

---

## 16. Type Hints

Type hints are **optional annotations** describing what types a variable, parameter, or return value should be. Python does **not** enforce them at runtime — they are documentation for developers and tools like `mypy`.

### Basic Annotations

```python
# Variable annotations
name:  str   = "Tarun"
cups:  int   = 4
temp:  float = 92.5
ready: bool  = False

# Function signatures
def brew_chai(spice: str, cups: int) -> str:
    return f"{spice} chai for {cups} cup(s)"

def show_info(name: str, age: int) -> None:   # returns nothing
    print(f"{name} is {age} years old")
```

### Optional and Union

```python
from typing import Optional, Union

# Optional[X] — value is X or None
def get_note(order_id: int) -> Optional[str]:
    notes = {1: "Extra spicy", 2: None}
    return notes.get(order_id)

# Union[X, Y] — value can be X or Y
def set_sugar(level: Union[int, str]) -> str:
    if isinstance(level, str):
        return f"Sugar by name: {level}"
    return f"Sugar level: {level}"
```

### Collection Type Hints (Python 3.9+)

```python
def list_spices(spices: list[str]) -> None:
    for spice in spices:
        print(spice)

def low_stock(stock: dict[str, int]) -> dict[str, int]:
    return {k: v for k, v in stock.items() if v < 10}

def get_range(values: list[int]) -> tuple[int, int]:
    return min(values), max(values)
```

### Hints Are Not Enforced at Runtime

```python
def add(a: int, b: int) -> int:
    return a + b

add(3, 4)      # 7   — correct
add("3", "4")  # "34" — runs fine, but mypy flags it as an error
```

Run static checking from the terminal:
```bash
mypy your_script.py
```

### When to Use Type Hints

**Use them for:**
- All function signatures in team or shared code
- Any code others will import or maintain
- Catching bugs early with `mypy` or `pyright`

**Skip them for:**
- Small throwaway scripts — hints add noise without benefit
- Don't force `Optional` everywhere — only when `None` is a real possibility

---

## 17. Modules & Imports

A module is any `.py` file. Python ships with hundreds of standard-library modules. Import them to reuse code without rewriting it.

### Import Styles

```python
import math                          # full module
from datetime import datetime        # specific name
from random import choice, randint   # multiple names
import json as j                     # alias
```

### `math`

```python
import math

math.floor(250.75)   # 250
math.ceil(250.75)    # 251
math.sqrt(144)       # 12.0
math.pi              # 3.141592653589793
math.log(100, 10)    # 2.0
```

### `datetime`

```python
from datetime import datetime

now = datetime.now()
now.strftime("%Y-%m-%d %H:%M:%S")   # "2025-03-01 09:30:00"
print(now.year, now.month, now.day)
```

### `random`

```python
from random import choice, randint, shuffle

spices = ["ginger", "cardamom", "cinnamon"]
choice(spices)    # random item from list
randint(1, 5)     # random int between 1 and 5 inclusive
shuffle(spices)   # shuffle in-place
```

### `json`

```python
import json

order = {"type": "Masala", "sugar": 2}

# Python dict → JSON string
json_str = json.dumps(order, indent=2)

# JSON string → Python dict
loaded = json.loads(json_str)
print(loaded["sugar"])   # 2
```

### `os` and `sys`

```python
import os, sys

os.getcwd()               # current working directory
os.listdir(".")           # list files in current dir
os.path.exists("f.txt")   # check if file exists
os.path.join("dir", "f")  # cross-platform path builder

sys.version               # Python version string
sys.exit(0)               # exit the program
```

### `re` — Regular Expressions

```python
import re

text = "Order #1042: 2x Masala Chai, 1x Ginger Chai"

# Search for first match
match = re.search(r"#(\d+)", text)
if match:
    print(match.group(1))   # 1042

# Find all matches
quantities = re.findall(r"(\d+)x", text)
# ['2', '1']
```

### `__name__` Guard

Code inside `if __name__ == "__main__"` only runs when the file is **executed directly** — not when imported as a module.

```python
def brew():
    print("Brewing chai...")

if __name__ == "__main__":
    brew()   # only runs on direct execution
```

This means you can safely import functions from this file without triggering the script to run.

### String Encoding — `encode()` / `decode()`

Strings in Python are Unicode. When storing or transmitting text, you convert to `bytes` (encode), and back to `str` (decode).

```python
label = "Chai Spécial"

# str → bytes
encoded = label.encode("utf-8")
print(encoded)    # b'Chai Sp\xc3\xa9cial'

# bytes → str
decoded = encoded.decode("utf-8")
print(decoded)    # "Chai Spécial"
```

> UTF-8 is the standard encoding for most web and file work. Always specify it explicitly — don't rely on system defaults.

### `collections.namedtuple` — Readable Tuples

A `namedtuple` is a tuple where each position has a name. More readable than plain tuples, zero overhead vs a class.

```python
from collections import namedtuple

ChaiProfile = namedtuple("ChaiProfile", ["flavor", "aroma"])

masala = ChaiProfile(flavor="spicy", aroma="strong")
print(masala.flavor)   # "spicy"
print(masala[0])       # "spicy"  — index access still works
print(masala)          # ChaiProfile(flavor='spicy', aroma='strong')
```

| Feature | Tuple | namedtuple |
|---------|-------|------------|
| Access by index | Yes | Yes |
| Access by name | No | Yes |
| Mutable | No | No |
| Memory overhead | Minimal | Minimal |
| Readable output | No | Yes |

> Use `namedtuple` when a plain tuple would work but the meaning of each position isn't obvious. It's a lightweight alternative to a full class for simple data containers.

---

- Use the standard library before reaching for third-party packages — it's already there
- Always use the `__name__` guard in reusable scripts
- Use `os.path.join()` instead of string concatenation for file paths
- Prefer `from x import y` over `import x` when you only need one function
- Never use `from module import *` — pollutes the namespace and makes debugging painful
- Avoid circular imports (A imports B, B imports A) — restructure your code
