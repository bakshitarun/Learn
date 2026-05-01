# Classes & Object-Oriented Programming

---

## 14. Classes & OOP

Object-Oriented Programming organises code around **objects** — data and the functions that act on it, packaged together.

- **Class** = the blueprint
- **Instance** = the actual object created from the blueprint

---

### Defining a Class

```python
class ChaiRecipe:
    category = "Hot Beverage"   # class attribute — shared by ALL instances

    def __init__(self, name, spices, sugar):
        self.name   = name      # instance attributes — unique per object
        self.spices = spices
        self.sugar  = sugar

    def describe(self):         # instance method
        spice_list = ", ".join(self.spices)
        return f"{self.name} | {spice_list} | sugar={self.sugar}"

masala = ChaiRecipe("Masala Chai", ["cardamom", "ginger"], 2)
print(masala.describe())
print(masala.category)    # 'Hot Beverage'
```

---

### `__str__` and `__repr__`

| Method | When Used | Purpose |
|--------|-----------|---------|
| `__str__` | `print(obj)`, `str(obj)` | Human-readable output |
| `__repr__` | REPL, debugger, `repr(obj)` | Developer-readable representation |

```python
def __str__(self):
    return f"ChaiRecipe({self.name})"

def __repr__(self):
    return f"ChaiRecipe(name={self.name!r}, sugar={self.sugar})"

print(str(masala))    # ChaiRecipe(Masala Chai)
print(repr(masala))   # ChaiRecipe(name='Masala Chai', sugar=2)
```

---

### Inheritance

A child class **inherits** all attributes and methods of its parent. Use `super()` to call the parent's `__init__` or any overridden method.

```python
class IcedChai(ChaiRecipe):           # inherits ChaiRecipe
    def __init__(self, name, spices, sugar, ice_cubes):
        super().__init__(name, spices, sugar)   # call parent __init__
        self.ice_cubes = ice_cubes

    def describe(self):               # override parent method
        base = super().describe()     # call parent describe()
        return f"{base} | ice={self.ice_cubes} cubes"

iced = IcedChai("Iced Masala", ["cardamom"], 3, 6)
print(iced.describe())
print(isinstance(iced, ChaiRecipe))   # True — iced IS a ChaiRecipe
```

---

### `@property` — Controlled Attribute Access

`@property` lets you access a method **like an attribute**. Pair with a setter to validate values on assignment.

```python
class BrewTimer:
    def __init__(self, minutes):
        self._minutes = minutes    # _ prefix = intended for internal use

    @property
    def minutes(self):             # getter — read like an attribute
        return self._minutes

    @minutes.setter
    def minutes(self, value):      # setter — validates on assignment
        if value <= 0:
            raise ValueError("Brew time must be positive")
        self._minutes = value

    @property
    def seconds(self):             # computed property — no setter needed
        return self._minutes * 60

timer = BrewTimer(5)
print(timer.seconds)   # 300  — no () needed
timer.minutes = 7      # triggers setter validation
timer.minutes = -1     # raises ValueError
```

---

### Key Concepts at a Glance

| Concept | What It Does |
|---------|-------------|
| `__init__(self, ...)` | Constructor — runs automatically when an object is created |
| `self` | Reference to the current instance — always first parameter |
| Class attribute | Defined outside `__init__` — shared across all instances |
| Instance attribute | Defined in `__init__` with `self.` — unique per object |
| Inheritance | Child class reuses parent code and can override methods |
| `super()` | Calls the parent class method from inside the child |
| `@property` | Access a method like an attribute; supports getter/setter |

---

### When to Use OOP

**Use classes when:**
- Modelling real-world entities: users, orders, products, sensors
- Many objects share the same structure but hold different data
- You need specialised variants of a base type (inheritance)

**Avoid classes when:**
- Writing simple one-off scripts — plain functions are simpler
- Deep inheritance chains (more than 2 levels) — prefer composition
- Dumping unrelated methods in one class — keep classes focused

---

### Practical Pattern: Validation via `@property`

```python
class Order:
    def __init__(self, quantity):
        self.quantity = quantity   # calls the setter

    @property
    def quantity(self):
        return self._quantity

    @quantity.setter
    def quantity(self, value):
        if not isinstance(value, int) or value < 1:
            raise ValueError(f"Quantity must be a positive int, got {value!r}")
        self._quantity = value

o = Order(3)    # fine
o.quantity = 5  # fine
o.quantity = 0  # ValueError!
```
