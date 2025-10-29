---
title: Python OOP – Complete Revision Guide with Real‑World Analogies, Code, and Exam Questions
author: HarshRajput
description: A concise-but-complete study and revision resource for Object-Oriented Programming (OOP) in Python with clear analogies, well‑commented examples, common pitfalls, best practices, and exam-focused questions.
---

# What is OOP (definition)

Object-Oriented Programming (OOP) is a way of organizing programs around objects—bundles of data (attributes) and behavior (methods)—instead of keeping data and functions separate. In Python, a class defines the blueprint, and an object (instance) is a concrete thing built from that blueprint. The core ideas are:
- Encapsulation: keep related data and behavior together and control access.
- Inheritance: reuse and extend existing classes.
- Polymorphism: same interface, different implementations.
- Abstraction: expose what’s essential, hide internal details.

Why it’s useful (in simple terms):
- Models the real world naturally (e.g., Car, Account, Order).
- Reuse code safely (write once in a class, reuse across many objects).
- Easier to maintain and change (localize changes inside classes).
- Extensible designs (add new subclasses without touching stable code).
- Team-friendly (clear boundaries and responsibilities per class/module).

# Why OOP? Real‑world intuition

- Think “blueprints and objects”: A class is a blueprint; an object is a house built from that blueprint.
- Robot analogy: Define a Robot class once (head, eyes, speak, move). Build many robots (objects), each with their own state but same behaviors. This is code reusability.
- Library analogy: Class Book defines common data (title, author, isbn) and behavior (borrow, return). Each physical copy is an object with its own availability.
- E‑commerce analogy: Class Order with items, total(), and pay(). Every new order object reuses the same logic, but carries different data.

Key benefits:
- Reusability: Write behavior once in a class, reuse with many objects.
- Organization: Group related data and functions together as attributes and methods.
- Extensibility: Inherit and extend without modifying existing working code.
- Maintainability: Encapsulate change—localize what varies.

Potential trade‑offs:
- Slight overhead and more structure than simple scripts.
- Can be overused—prefer simple functions where a class adds no clarity.


# Quick glossary (1‑minute skim)

- Class: Blueprint for creating objects. Defines attributes and methods.
- Object (Instance): A concrete realization of a class with actual data.
- Attribute: Data stored on a class or object (state).
- Method: Function defined inside a class that operates on the object/class (behavior).
- Constructor: The initializer method in Python is __init__(self, ...).
- Encapsulation: Keep data and methods together; restrict direct access to sensitive data.
- Inheritance: Create a new class reusing and extending an existing class.
- Polymorphism: Same interface, different implementations (e.g., start() for Car vs Bike).
- Abstraction: Expose what’s essential, hide implementation details (via ABCs in Python).

More basics (simple terms):
- self: The current object inside an instance method; Python passes it for you when you call obj.method().
- cls: The class itself inside a classmethod; use it to build instances or access class-level data.
- Instance variable vs Class variable: Instance variable lives on each object (different per object). Class variable lives on the class (shared by all objects).
- Namespace: A mapping from names to objects (e.g., variables in a function form a function namespace).
- Scope (LEGB): Where a name is looked up—Local, Enclosing, Global, Built-in.
- Identity vs Equality: is checks same object (identity), == checks same value (equality).


# 1) Classes and Objects

Definition: A class groups related data and behavior. An object is an instance created from a class.

Example: Car class and objects

```python
class Car:
    def __init__(self, color, model):  # constructor: initialize object state
        self.color = color             # instance attribute
        self.model = model

    def start(self):                   # instance method: uses 'self'
        print(f"The {self.color} {self.model} is starting.")

    def stop(self):
        print(f"The {self.color} {self.model} is stopping.")


# creating objects
car1 = Car("Red", "Audi")
car2 = Car("Blue", "BMW")

car1.start()  # The Red Audi is starting.
car2.stop()   # The Blue BMW is stopping.
```

Notes:
- self is the current object (like this in other languages). It’s passed automatically on instance method calls.
- __init__ is called right after the object is created to set up initial state.


# Prerequisites: concepts to know (easy mode)

- Names point to objects: In Python, a variable name stores a reference to an object (not the object itself). Think “label → box”.
- Every object has id, type, value: id is its identity (where it lives), type is its class, value is its data.
- Mutability matters:
    - Mutable: list, dict, set, most user-defined objects (can change in place).
    - Immutable: int, float, str, tuple, frozenset (changing means a new object).
- Function calls pass references: Arguments are passed by assignment (a reference is copied). Mutating a mutable argument changes the original.
- Indentation is syntax: Class, function, and method bodies must be indented consistently (spaces recommended).
- Scope rule (LEGB): Python resolves names in Local → Enclosing → Global → Builtins.
- Modules and import: A .py file is a module; you import names from modules. Classes usually live in modules.


# 2) Attributes and Methods

Types of attributes:
- Instance attribute: unique per object (e.g., color).
- Class attribute: shared across all instances (e.g., manufacturer).

```python
class Phone:
    manufacturer = "Acme"      # class attribute (shared)

    def __init__(self, model):
        self.model = model      # instance attribute (per object)

p1 = Phone("A1")
p2 = Phone("A2")
print(p1.manufacturer, p2.manufacturer)  # Acme Acme
Phone.manufacturer = "Globex"            # change on the class
print(p1.manufacturer, p2.manufacturer)  # Globex Globex
```

Kinds of methods:
- Instance method: def method(self, ...)
- Class method: @classmethod def method(cls, ...)
- Static method: @staticmethod def method(...)

```python
class Temperature:
    def __init__(self, celsius: float):
        self.celsius = celsius

    @classmethod
    def from_fahrenheit(cls, f: float):  # factory method using the class
        return cls((f - 32) * 5/9)

    @staticmethod
    def is_valid(value: float) -> bool:  # utility that doesn't depend on instance or class
        return -273.15 <= value <= 6_000

t1 = Temperature.from_fahrenheit(212)
print(t1.celsius)               # 100.0
print(Temperature.is_valid(25)) # True
```

### self vs cls in one minute

```python
class Demo:
    kind = "shared"     # class variable (one copy)

    def __init__(self, x):
        self.x = x       # instance variable (per object)

    @classmethod
    def make_default(cls):
        return cls(0)    # use the class (cls) to build an instance

    @staticmethod
    def helper(a, b):
        return a + b     # no access to self or cls

d = Demo(5)
print(d.x)               # 5          (instance data)
print(Demo.kind)         # shared     (class data)
print(Demo.make_default().x)  # 0     (built via cls)
```


# 3) Encapsulation (Data Hiding)

Goal: Restrict direct access to sensitive data and provide controlled interfaces.

Python specifics:
- Public by default. Conventionally, a single underscore _name means “internal use”.
- Double underscore __name triggers name mangling to reduce accidental access: _Class__name.

Example: Bank account with safe accessors

```python
class BankAccount:
    def __init__(self, owner: str, balance: float = 0.0):
        self.owner = owner
        self.__balance = float(balance)  # name-mangled: avoid accidental access

    def deposit(self, amount: float):
        if amount <= 0:
            raise ValueError("Deposit must be positive")
        self.__balance += amount

    def withdraw(self, amount: float):
        if amount <= 0:
            raise ValueError("Withdrawal must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        self.__balance -= amount

    def get_balance(self) -> float:   # controlled read access
        return self.__balance

acct = BankAccount("Aman", 500)
acct.deposit(250)
print(acct.get_balance())  # 750.0
```

Pro tip: For computed or validated fields, prefer @property over raw getters/setters.

```python
class Student:
    def __init__(self, name: str, percentage: float):
        self.name = name
        self._percentage = 0.0
        self.percentage = percentage  # use property to validate at creation

    @property
    def percentage(self) -> float:
        return self._percentage

    @percentage.setter
    def percentage(self, value: float):
        if not (0 <= value <= 100):
            raise ValueError("percentage must be between 0 and 100")
        self._percentage = float(value)
```


# 4) Inheritance

Definition: A class (child/derived) reuses and extends another class (parent/base).

Types you may see in exams:
- Single: A -> B
- Multilevel: A -> B -> C
- Multiple: A & B -> C
- Hierarchical: A -> B, A -> C
- Hybrid: combination of above

Example with override:

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):  # overriding
        print("Dog barks")

class Cat(Animal):
    def speak(self):  # overriding
        print("Cat meows")

Dog().speak()  # Dog barks
Cat().speak()  # Cat meows
```

super() and Method Resolution Order (MRO):

```python
class Vehicle:
    def start(self):
        print("Vehicle starting")

class Electric:
    def start(self):
        print("Battery check")

class ElectricCar(Electric, Vehicle):  # multiple inheritance
    def start(self):
        super().start()  # calls next in MRO: Electric.start
        print("ElectricCar rolling")

ec = ElectricCar()
ec.start()
# Battery check
# ElectricCar rolling
```

Note: Python uses C3 linearization to compute MRO. You can inspect it via Class.__mro__.

Composition vs Inheritance (HAS‑A vs IS‑A): Prefer composition to reuse behavior safely.

```python
class Engine:
    def ignite(self):
        print("Ignition!")

class Car:
    def __init__(self):
        self.engine = Engine()  # composition: has‑a engine

    def start(self):
        self.engine.ignite()
        print("Car started")
```


# 5) Polymorphism and Duck Typing

Polymorphism: One interface, many implementations.

```python
class Shape:
    def area(self):
        raise NotImplementedError

class Circle(Shape):
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14159 * self.r * self.r

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w = w; self.h = h
    def area(self):
        return self.w * self.h

for s in [Circle(5), Rectangle(4, 6)]:
    print(s.area())
```

Duck typing: “If it quacks like a duck…” In Python, you don’t need a common base class as long as the required methods exist.

```python
class PDF:
    def render(self):
        print("Render PDF")

class Image:
    def render(self):
        print("Render Image")

def preview(doc):
    doc.render()  # works for any object with .render()

preview(PDF())
preview(Image())
```

About “method overloading” in Python: Not like Java/C++.
- Defining the same method name twice in a class will keep only the last one.
- Use default parameters, *args/**kwargs, or @functools.singledispatch for function overloading.

```python
from functools import singledispatch

@singledispatch
def area(x):
    raise NotImplementedError

@area.register
def _(x: int):
    return x * x

@area.register
def _(x: float):
    return 3.14 * x * x

print(area(5))     # 25 (int)
print(area(5.0))   # 78.5 (float)
```


# 6) Abstraction (Abstract Base Classes)

Use abc.ABC to define abstract methods that must be implemented by subclasses.

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start(self):
        pass

class Car(Vehicle):
    def __init__(self, color, model):
        self.color = color; self.model = model
    def start(self):
        print(f"The {self.color} {self.model} car is starting.")

class Bike(Vehicle):
    def __init__(self, color, model):
        self.color = color; self.model = model
    def start(self):
        print(f"The {self.color} {self.model} bike is starting.")

Car("Red", "Audi").start()
Bike("Blue", "Yamaha").start()
```


# 7) Special (dunder) methods and operator overloading

Common ones:
- __str__/__repr__: string representations
- __eq__/__lt__/__hash__: comparisons and hashing
- __len__, __iter__, __getitem__: container protocols

```python
class Money:
    def __init__(self, rupees: int):
        self.rupees = rupees

    def __repr__(self):  # unambiguous
        return f"Money({self.rupees})"

    def __str__(self):   # user-friendly
        return f"₹{self.rupees}"

    def __add__(self, other):
        if not isinstance(other, Money):
            return NotImplemented
        return Money(self.rupees + other.rupees)

print(Money(10) + Money(25))   # Money(35)
print(str(Money(99)))          # ₹99
```


# 8) Data classes (Pythonic POJOs)

Use dataclasses for concise data containers; supports defaults, comparison, immutability.

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int = 0

p = Point(2)
print(p)         # Point(x=2, y=0)
print(p.x, p.y)  # 2 0
```

Advanced:
- frozen=True to make instances immutable.
- slots=True (3.10+) to reduce memory and speed attribute access.


# 9) Copying objects: shallow vs deep

```python
import copy

class Team:
    def __init__(self, name, members):
        self.name = name
        self.members = list(members)

t1 = Team("Alpha", ["A", "B"])     # original
t2 = copy.copy(t1)                    # shallow copy: same inner list reference
t3 = copy.deepcopy(t1)                # deep copy: new list

t1.members.append("C")
print(t2.members)  # ['A', 'B', 'C']  (changed)
print(t3.members)  # ['A', 'B']       (not changed)
```


# 10) Equality, hashing, and identity

- is checks identity (same object). == checks equality (via __eq__).
- If objects are used in sets/dicts, implement matching __eq__ and __hash__.

```python
class User:
    def __init__(self, uid):
        self.uid = uid
    def __eq__(self, other):
        return isinstance(other, User) and self.uid == other.uid
    def __hash__(self):
        return hash(self.uid)

u1 = User(1); u2 = User(1)
print(u1 == u2)   # True (equal)
print(u1 is u2)   # False (different objects)
```


# 11) Performance and memory tips

- __slots__: Prevent dynamic attribute creation; save memory for many small objects.

```python
class Pixel:
    __slots__ = ("x", "y")
    def __init__(self, x, y):
        self.x = x; self.y = y
```

- Prefer composition over deep inheritance chains.
- Use dataclasses with slots=True where suitable.


# 12) Patterns you’ll see

- Factory method (via @classmethod) to create instances in different ways.
- Strategy: inject interchangeable behavior objects.
- Singleton: rarely needed; prefer dependency injection.

Strategy example:

```python
class CashPayment:
    def pay(self, amount):
        print(f"Paid ₹{amount} in cash")

class CardPayment:
    def pay(self, amount):
        print(f"Paid ₹{amount} by card")

class Checkout:
    def __init__(self, payment):
        self.payment = payment  # any object with .pay()
    def complete(self, amount):
        self.payment.pay(amount)

Checkout(CashPayment()).complete(500)
Checkout(CardPayment()).complete(750)
```


# 13) End‑to‑end example using all four pillars

```python
from abc import ABC, abstractmethod

# Abstraction: common interface
class Vehicle(ABC):
    @abstractmethod
    def start(self):
        pass

# Encapsulation via private-ish attributes and properties
class Car(Vehicle):
    def __init__(self, color, model):
        self.__color = color
        self.__model = model

    @property
    def model(self):
        return self.__model

    def start(self):  # Polymorphism: specific behavior
        print(f"The {self.__color} {self.__model} car is starting.")

class Bike(Vehicle):
    def __init__(self, color, model):
        self.__color = color
        self.__model = model
    def start(self):  # Polymorphism
        print(f"The {self.__color} {self.__model} bike is starting.")

# Usage
Car("Red", "Audi").start()
Bike("Blue", "Yamaha").start()
```


# 14) Common pitfalls in Python OOP

- “Method overloading” by duplicate defs doesn’t work; last def wins. Use defaults or singledispatch.
- Private isn’t truly private; __name becomes _Class__name. Respect conventions.
- Don’t mutate class attributes with mutable defaults unintentionally.

```python
class Bad:
    items = []  # shared across ALL instances! dangerous if you expect per-instance
    def add(self, x):
        self.items.append(x)

class Good:
    def __init__(self):
        self.items = []  # per-instance list
```


# 15) Quick revision cheat sheet

- Class vs Object: blueprint vs constructed thing.
- Instance vs Class attribute: per-object vs shared.
- Methods: instance (self), class (cls), static (utility).
- Encapsulation: _internal, __mangled, properties for validation.
- Inheritance: extend and override; prefer composition when unsure.
- Polymorphism: same method name, different behavior; duck typing is idiomatic.
- Abstraction: ABCs enforce interface; @abstractmethod.
- Dunder methods: __str__, __repr__, __eq__, __hash__, __len__, __iter__.
- Dataclasses: concise, comparison, frozen, slots.
- Copies: copy vs deepcopy; beware shared mutable state.


# 16) Exam‑style questions (with answers)

Theory (short):
1) Define encapsulation and how Python implements it.  
Answer: Bundling data and methods; Python uses naming conventions, single underscore, and name-mangling with double underscore to discourage direct access.

2) Differentiate classmethod and staticmethod.  
Answer: classmethod receives cls and can construct/modify class-level state; staticmethod receives neither self nor cls; for standalone utilities.

3) What is polymorphism in Python?  
Answer: Different types implementing the same interface (method names); realized via overriding and duck typing, not compile-time overloading.

4) Composition vs Inheritance?  
Answer: HAS‑A vs IS‑A; prefer composition when simple reuse is desired without tight coupling or fragile base classes.

5) What are __str__ and __repr__ used for?  
Answer: __repr__ is unambiguous developer representation; __str__ is user-friendly display.

Output prediction:
```python
class A:
    def f(self): print("A.f")

class B(A):
    def f(self): print("B.f"); super().f()

B().f()
```
Answer: B.f then A.f (on separate lines).

```python
class X:
    def __init__(self): self.v = []

a = X(); b = X()
a.v.append(1)
print(a.v, b.v)
```
Answer: [1] [] — lists are per-instance.

Multiple choice:
1) Which is TRUE about Python overloading?  
 A) Python compiles and overloads by signature like Java  
 B) Python ignores earlier defs; last method definition wins  
 C) You must use @overload at runtime  
Answer: B

2) The purpose of @property is:  
 A) Make method static  
 B) Turn a method into an attribute access with optional validation  
 C) Hide method from users  
Answer: B

Coding tasks:
1) Implement a class Fraction supporting addition and string display.  
Hint: Implement __add__ and __str__, reduce using math.gcd.

2) Build an ABC Document with export(); implement Pdf and Docx.


# 17) Real‑world mini case studies

Library System (encapsulation, composition):
```python
from dataclasses import dataclass

@dataclass
class Book:
    title: str
    author: str

class Member:
    def __init__(self, name):
        self.name = name
        self._borrowed = []

    def borrow(self, book: Book):
        self._borrowed.append(book)

class Library:
    def __init__(self):
        self._books = []

    def add_book(self, book: Book):
        self._books.append(book)

    def lend(self, member: Member, title: str):
        for i, b in enumerate(self._books):
            if b.title == title:
                member.borrow(self._books.pop(i))
                return True
        return False
```

Order Checkout (strategy polymorphism): see section 12.


# 18) Frequently asked clarifications

- Why prefer @classmethod factories? They’re discoverable on the class, return correct subclass when inherited, and allow named constructors like from_json.
- When to use ABC? When you want to enforce an interface across subclasses.
- What is MRO? The order Python searches for attributes in a class hierarchy; inspect via Class.__mro__.


# 19) Practice exercises (try yourself)

1) Create a Shape hierarchy with Triangle and Square and compute areas. Use an abstract base class.  
2) Implement a Stack class supporting push, pop, len, and iteration (use __len__ and __iter__).  
3) Model a Playlist with Tracks; support total_duration and add/remove tracks using operator overloading (+ and -).


# 20) Quick self‑check

- Can you explain the difference among instance, class, and static methods with examples?
    Answer (easy terms):
    - Instance method: gets self (the current object). Use it when behavior depends on object data. Example: car.start().
    - Class method: gets cls (the class). Use it for alternate constructors or class-wide logic. Example: Temperature.from_fahrenheit().
    - Static method: gets neither. Use it for utility functions that logically belong to the class but don’t need object/class data.

- Can you write an ABC and a concrete subclass?
    Answer: Yes—define a class inheriting from abc.ABC and decorate required methods with @abstractmethod. Any subclass must implement them. See section 6 for Vehicle (ABC) and Car/Bike (concrete subclasses).

- Can you explain why Python doesn’t do compile‑time overloading and what to use instead?
    Answer: Python is dynamically typed and keeps only the last method definition with the same name. Instead, use default parameters, *args/**kwargs, or @functools.singledispatch for function-style overloading.

- Can you decide between composition and inheritance for a given design?
    Answer: Prefer composition (HAS‑A) when you just want to reuse behavior without tightly coupling types. Use inheritance (IS‑A) when the subclass truly “is a” specialized form of the base and should share its interface.

- Bonus: What’s the difference between instance and class variables?
    Answer: Instance variables live on each object and can differ per object. Class variables live on the class and are shared by all objects unless overridden on an instance.

- Bonus: What’s the difference between is and ==?
    Answer: is checks whether two names point to the exact same object (identity). == checks whether values are equal (uses __eq__).



