# 🧩 Python Classes — Building Your Own Data Structures

In Python, **classes** let you create your own **data types** by combining **data** (variables) and **behavior** (functions) in one place.
They are one of the most powerful tools in Python for organizing and structuring complex programs.

Think of a **class** as a **blueprint**, and an **object** as something built from that blueprint.
For example, a class can describe what a *Car* is, and each object can represent a specific car with its own color, speed, and brand.

---

## 🧱 What Is a Class?

A **class** defines how something should behave and what information it contains.

```python
class Car:
    # Constructor
    def __init__(self, brand, color):
        # Attributes
        self.brand = brand
        self.color = color

    # Method
    def drive(self):
        print(self.brand, "is driving.")
```

Here’s what each part means:

* `class Car:` → defines a new class called `Car`
* `__init__` → a special method that runs when you create a new object (it’s called the **constructor**)
* `self` → refers to the specific object being created or used
* `brand` and `color` → are **attributes** that belong to each object
* `drive()` → is a **method**, a function inside the class that defines an action

---

## 🚗 Creating and Using Objects

Once you have a class, you can create **objects** (also called **instances**) from it:

```python
my_car = Car("Toyota", "Red")
my_car.drive()
```

Output:
Toyota is driving.

You can create as many cars as you want, each with its own data:

```python
car2 = Car("BMW", "Blue")
car2.drive()
```

Output:
BMW is driving.

---

## ⚙️ The `__init__` Method

`__init__` is used to set up initial data for each object when it’s created.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

When you create a student:

```python
s1 = Student("Alice", 20)
print(s1.name, s1.age)
```

Output:
Alice 20

---

## 🧩 Adding Behavior with Methods

Classes can contain **methods** — functions that describe actions or behaviors related to that class.

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(self.name, "is barking!")


dog1 = Dog("Buddy")
dog1.bark()
```

Output:
Buddy is barking!

---

## 🔒 Public and Private Attributes/Methods

In Python, **public** attributes/methods can be accessed from outside the class, while **private** ones should not be accessed directly.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner          # public
        self.__balance = balance    # private

    def deposit(self, amount):     # public method
        self.__balance += amount

    def get_balance(self):         # public method to access private attribute
        return self.__balance

account = BankAccount("Alice", 100)
print(account.owner)         # works
print(account.get_balance()) # works
# print(account.__balance)    # error! cannot access private attribute
```

* Public attributes/methods: accessible everywhere.
* Private attributes/methods (prefix `__`): intended for internal use only.
* Use public methods to safely access or modify private data.

---

## 🏗️ Inheritance — Reusing and Extending Classes

Inheritance allows a new class to **reuse** and **extend** an existing class.

```python
class ElectricCar(Car):
    def __init__(self, brand, color, battery_size):
        super().__init__(brand, color)
        self.battery_size = battery_size

    def charge(self):
        print(f"{self.brand} is charging its {self.battery_size}kWh battery.")

ec = ElectricCar("Porche", "Black", 75)
ec.drive()
ec.charge()
```

Output:
Porche is driving.
Porche is charging its 75kWh battery.

* `ElectricCar` inherits from `Car` using `class ElectricCar(Car):`
* `super().__init__()` calls the parent class constructor
* You can add new attributes (`battery_size`) and methods (`charge`) specific to the child class

---

## 🔄 Polymorphism — Same Method, Different Behavior

Polymorphism lets objects of different classes be treated similarly if they implement the same method. Using **inheritance** makes it more organized:

```python
class Animal:
    def speak(self):
        pass  # base method, to be overridden by child classes

class Cat(Animal):
    def speak(self):
        print("Meow")

class Dog(Animal):
    def speak(self):
        print("Woof")

animals = [Cat(), Dog()]
for animal in animals:
    animal.speak()
```

Output:
Meow
Woof

* `Cat` and `Dog` inherit from `Animal`
* Both override the `speak()` method differently
* You can call `speak()` on any `Animal` object without checking its type — this is **polymorphism**

---

## 💡 Summary

| Concept           | Description                                     | Example                     |
| ----------------- | ----------------------------------------------- | --------------------------- |
| **Class**         | Blueprint for creating objects                  | `class Dog:`                |
| **Object**        | An instance of a class                          | `dog1 = Dog("Max")`         |
| **Attribute**     | Variable inside a class                         | `self.name`                 |
| **Method**        | Function inside a class                         | `def bark(self):`           |
| **Constructor**   | Initializes an object when created              | `__init__()`                |
| **Public**        | Accessible from anywhere                        | `self.owner`                |
| **Private**       | Internal use, not accessed directly             | `self.__balance`            |
| **Encapsulation** | Keep data and behavior together                 | `BankAccount` example       |
| **Inheritance**   | Reuse and extend another class                  | `class ElectricCar(Car):`   |
| **Polymorphism**  | Same method, different behavior via inheritance | `Animal -> Cat/Dog speak()` |

Classes help you move from writing simple scripts to building **organized, real-world applications**.
