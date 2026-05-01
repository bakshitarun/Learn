# Conditionals & Loops

---

## 4. Conditional Statements

Python checks a condition and runs different code depending on `True` or `False`.

### if / elif / else

```python
age = 17

if age < 13:
    print("Child")
elif age < 18:
    print("Teenager")   # this runs
else:
    print("Adult")
```

### Nested Conditionals

```python
num = int(input('Enter a number: '))

if num > 0:
    print("Positive")
    if num % 2 == 0:
        print("and Even")
    else:
        print("and Odd")
else:
    print("Zero or Negative")
```

> Avoid nesting deeper than 3 levels — refactor into functions or guard clauses.

### Truthy and Falsy Values

Every value in Python has an implicit boolean meaning:

```python
# FALSY — treated as False:
False, None, 0, 0.0, "", [], {}, set()

# TRUTHY — everything else:
True, 1, -1, "hello", [0], {"a": 1}
```

```python
# Prefer this:
if my_list:           # checks if non-empty
if not milk_present:  # checks if zero or empty

# Over this:
if len(my_list) > 0:
if milk_present == 0:
```

> ⚠️ `if x:` means "if x is truthy" — that excludes `0`, `""`, and `[]`, not just `None`.

### User Input

```python
name = input("Enter your name: ")           # always returns a string
amount = int(input("Enter order amount: ")) # convert as needed
temp = float(input("Enter temperature: "))

# Normalise input immediately
cup = input("Choose size: ").lower().strip()
```

### Ternary Operator (Inline if/else)

A one-line `if/else` for simple value assignments. Keeps code compact without sacrificing readability.

```python
# Syntax: value_if_true if condition else value_if_false

order_amount = 350
delivery_fees = 0 if order_amount > 300 else 30
print(f"Delivery fees: {delivery_fees}")   # 0

# Same as writing:
if order_amount > 300:
    delivery_fees = 0
else:
    delivery_fees = 30
```

> Use for simple value choices. If the logic is complex, write a full `if/else` block — readability matters more than brevity.

### match / case (Python 3.10+)

Cleaner than long `if/elif` chains when checking one variable against fixed values:

```python
seat_type = input("Enter seat type: ").lower()

match seat_type:
    case "sleeper":
        print("Beds available")
    case "ac":
        print("Air conditioned")
    case "Saturday" | "Sunday":   # combine values with |
        print("Weekend")
    case _:                        # default (catch-all)
        print("Unknown type")
```

| Feature | if/elif/else | match/case |
|---------|-------------|------------|
| Default case | `else:` | `case _:` |
| Multiple values | `if x == 1 or x == 2:` | `case 1 \| 2:` |
| Python version | All | 3.10+ only |
| Best for | Complex boolean logic | Fixed set of known values |

---

## 5. Loops

### for Loop

```python
for i in range(5):          # 0, 1, 2, 3, 4
    print(i)

for i in range(1, 10, 2):  # 1, 3, 5, 7, 9  (start, stop, step)
    print(i)

for char in "Python":       # iterate any iterable
    print(char)
```

### while Loop

```python
count = 0
while count < 5:
    print(count)
    count += 1   # must update — or infinite loop!
```

### break, continue, pass

| Statement | What It Does |
|-----------|-------------|
| `break` | Exit the loop immediately |
| `continue` | Skip current iteration, move to next |
| `pass` | Do nothing (placeholder) |

```python
# break — stop at 5
for i in range(10):
    if i == 5: break
    print(i)           # 0 1 2 3 4

# continue — skip even numbers
for i in range(10):
    if i % 2 == 0: continue
    print(i)           # 1 3 5 7 9
```

### Nested Loops

```python
for i in range(3):      # outer: 3 times
    for j in range(2):  # inner: 2 times each
        print(f"i:{i}, j:{j}")
# Total: 6 iterations
```

> ⚠️ Nested loops on large data = O(n²). Look for alternatives.

### for/else and while/else

The `else` block runs **only if the loop was never `break`ed**. Useful for search patterns.

```python
staff = [("Amit", 16), ("Zara", 17), ("Raj", 15)]

for name, age in staff:
    if age <= 18:
        print(f"{name} is eligible")
        break
else:
    print("No one is eligible")  # only runs if break never triggered
```

| Scenario | `break` triggered? | `else` runs? |
|----------|--------------------|--------------|
| Item found | Yes | No |
| Loop finished, nothing found | No | Yes |

### Walrus Operator `:=` (Python 3.8+)

Assign a value **and** use it in the same expression — avoids repeating a function call:

```python
# Without walrus — input() called twice
flavor = input("Choose flavor: ")
while flavor not in flavors:
    print(f"{flavor} not available")
    flavor = input("Choose flavor: ")   # repeated!

# With walrus — clean
while (flavor := input("Choose flavor: ")) not in flavors:
    print(f"{flavor} not available")
print(f"You chose {flavor}")
```

> ⚠️ Parentheses around `(var := ...)` are required inside `while` conditions.

---

## Quick Tips

- Use `for` when you know the count or are iterating a sequence
- Use `while` for retry logic, input loops, or "until a condition changes"
- Chain `.lower().strip()` on `input()` immediately to prevent comparison bugs
- Use `for/else` instead of a `found = False` flag variable
- Only use `:=` when it removes a genuine repeated call — don't overuse it
