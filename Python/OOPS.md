# 🐍 Python OOPs Concepts: A Beginner’s Guide

Object-Oriented Programming (OOP) in Python helps us organize and structure our code better, especially as projects grow in size. It allows you to model real-world entities using **classes** and **objects**.

---

## 💡 What is OOP?

**Object-Oriented Programming** is a programming paradigm based on the concept of **objects**, which can hold data (**attributes**) and code (**methods**).

OOP helps:

* Reuse code (via inheritance)
* Hide complexity (via encapsulation)
* Structure logic naturally (like real-world entities)

---

## 🧱 Core Concepts in Python OOP

| Concept           | Description                                                              |
| ----------------- | ------------------------------------------------------------------------ |
| **Class**         | A blueprint for creating objects (e.g., `Car`, `Student`, `BankAccount`) |
| **Object**        | An instance of a class                                                   |
| **Attribute**     | A variable inside a class (e.g., `name`, `balance`)                      |
| **Method**        | A function inside a class that operates on attributes                    |
| **Constructor**   | `__init__()` method to initialize object values                          |
| **Self**          | A reference to the current object (used inside methods)                  |
| **Encapsulation** | Hiding internal details using private variables (`_` or `__`)            |
| **Inheritance**   | Deriving one class from another                                          |
| **Polymorphism**  | Using the same method name with different behaviors                      |

---

## 🧪 Basic Example: Class and Object

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        print(f"Hello, my name is {self.name} and I am {self.age} years old.")

# Creating an object
s1 = Student("Alice", 20)
s1.greet()
```

📜 Output:

```
Hello, my name is Alice and I am 20 years old.
```

---

## 🧰 Functions vs Methods

| Feature   | Function                      | Method                                 |
| --------- | ----------------------------- | -------------------------------------- |
| Defined   | Using `def`                   | Using `def` inside a class             |
| Called by | Name (e.g., `print()`)        | On an object (e.g., `obj.method()`)    |
| Access    | Doesn't have access to `self` | Has access to object's data via `self` |

---

## 🧬 Inheritance Example

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

d = Dog()
d.speak()
```

📜 Output:

```
Dog barks
```

---

## 🔐 Encapsulation Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # private variable

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount(100)
acc.deposit(50)
print(acc.get_balance())  # 150
```

---

## 🧐 Polymorphism Example

```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def area(self):
        return 3.14 * 5 * 5

class Square(Shape):
    def area(self):
        return 4 * 4

shapes = [Circle(), Square()]
for shape in shapes:
    print(shape.area())
```

📜 Output:

```
78.5
16
```

---

## ✅ Summary

| Concept       | Purpose                                                         |
| ------------- | --------------------------------------------------------------- |
| `class`       | Defines a blueprint for objects                                 |
| `object`      | Instance of a class                                             |
| `__init__()`  | Constructor to initialize attributes                            |
| `self`        | Refers to the current object inside the class                   |
| Encapsulation | Keeps data safe inside a class                                  |
| Inheritance   | Reuses code by extending other classes                          |
| Polymorphism  | Allows multiple forms of a method name across different classes |


