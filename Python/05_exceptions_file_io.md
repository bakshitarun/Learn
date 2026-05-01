# Exception Handling & File I/O

---

## 12. Exception Handling

Exceptions are runtime errors. When something goes wrong Python raises one and stops. Handling them lets your program recover gracefully instead of crashing.

### try / except

Wrap risky code in `try`. If an error occurs, execution jumps to `except` — the rest of `try` is skipped.

```python
def parse_sugar(value):
    try:
        level = int(value)
        return f"Sugar level: {level}"
    except ValueError:
        return f"Invalid: '{value}' is not a number"

parse_sugar("3")       # "Sugar level: 3"
parse_sugar("sweet")   # "Invalid: 'sweet' is not a number"
```

### Catching Multiple Exceptions

```python
def get_spice(spice_list, index):
    try:
        return spice_list[index]
    except IndexError:
        return "Index out of range"
    except TypeError:
        return "Index must be an integer"

get_spice(["ginger", "cardamom"], 10)      # Index out of range
get_spice(["ginger", "cardamom"], "first") # Index must be an integer
```

### else and finally

| Clause | When It Runs | Common Use |
|--------|-------------|------------|
| `try` | Always, until an error occurs | Risky code: file open, type convert, API call |
| `except` | Only when an exception is raised | Handle error, log it, return fallback |
| `else` | Only when NO exception occurred | Code that depends on `try` succeeding |
| `finally` | Always — even after an exception | Cleanup: close files, release connections |

```python
try:
    temp = float(input_value)
except ValueError:
    print("Not a number")
else:
    print(f"Brewing at {temp}°C")   # only if no error
finally:
    print("Attempt complete")        # always runs
```

### Raising Exceptions

Use `raise` to throw an exception deliberately when your own validation fails:

```python
def set_brew_time(minutes):
    if minutes <= 0:
        raise ValueError(f"Brew time must be positive, got: {minutes}")
    return f"Brew time: {minutes} min"

try:
    print(set_brew_time(-1))
except ValueError as e:
    print(f"Error: {e}")
```

### Custom Exception Classes

Create your own exception by subclassing `Exception`:

```python
class InsufficientSpiceError(Exception):
    pass

def check_stock(needed, available):
    if available < needed:
        raise InsufficientSpiceError(
            f"Need {needed}g but only {available}g available"
        )

try:
    check_stock(10, 5)
except InsufficientSpiceError as e:
    print(f"Spice error: {e}")
```

### Common Exceptions to Know

| Exception | When It Occurs |
|-----------|---------------|
| `ValueError` | Right type, wrong value — `int("abc")` |
| `TypeError` | Wrong type entirely — `"hello" + 5` |
| `KeyError` | Dict key doesn't exist — `d["missing"]` |
| `IndexError` | List index out of range — `lst[99]` |
| `FileNotFoundError` | File doesn't exist |
| `ZeroDivisionError` | Division by zero |
| `AttributeError` | Object doesn't have that method |

---

### ✅ Do This
- Catch **specific** exceptions, not bare `except:` — avoids hiding unexpected bugs
- Use `finally` to release resources (files, DB connections) whether or not an error occurred
- Use `raise` for your own validation failures

### ❌ Avoid This
- Silent `except` blocks — they swallow errors silently
- Catching `Exception` broadly when you can be more specific
- Raising exceptions for normal flow — use `return` values instead

---

## 13. File I/O

Python's `open()` reads and writes files. The `with` statement ensures the file closes automatically — even if an error occurs.

### Opening Modes

| Mode | Meaning | File Must Exist? |
|------|---------|-----------------|
| `"r"` | Read (default) | Yes — `FileNotFoundError` if missing |
| `"w"` | Write — overwrites | No — creates file if missing |
| `"a"` | Append — adds to end | No — creates file if missing |
| `"x"` | Create new — fails if exists | No — `FileExistsError` if exists |

### Writing

```python
with open("recipe.txt", "w") as file:
    file.write("Chai Recipe\n")
    file.write("Spices: ginger, cardamom\n")

# Write a list of strings at once
orders = ["Order 1: Masala\n", "Order 2: Ginger\n"]
with open("orders.txt", "w") as file:
    file.writelines(orders)
```

### Reading

```python
# Entire file as one string
with open("recipe.txt", "r") as file:
    content = file.read()

# All lines as a list
with open("recipe.txt", "r") as file:
    lines = file.readlines()   # ['Chai Recipe\n', ...]

# Line by line — best for large files
with open("recipe.txt", "r") as file:
    for line in file:
        print(line.strip())
```

### Appending & File Checks

```python
# Append — does NOT overwrite
with open("recipe.txt", "a") as file:
    file.write("Sugar: 2 teaspoons\n")

# Check existence and delete
import os

if os.path.exists("recipe.txt"):
    print("File found!")

os.remove("recipe.txt")
```

### Handling Missing Files

```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found — creating it")
    with open("data.txt", "w") as file:
        file.write("New file\n")
```

---

### ✅ Do This
- Always use `with open(...)` — guarantees the file closes even on error
- Use `"a"` to append; use `"w"` only when you intentionally want to overwrite
- Iterate line-by-line for large files — `file.read()` loads the whole thing into memory
- Use `os.path.join()` for file paths — cross-platform safe

### ❌ Avoid This
- Opening files without `with` — risk leaving file handles open
- Hardcoded path strings like `"C:\\Users\\tarun\\file.txt"`
- Using `"w"` when you meant `"a"` — silently destroys existing content
