
# 🐍 Python Basics

This guide explains Python in simple, beginner-friendly terms.  
It covers **core concepts** with examples and explains **why we use each feature**.

<br>

# 🧮 Arithmetic Operators

Arithmetic operators are used to **perform calculations** in Python.  
We use them to calculate totals, averages, scores, or any numeric result.

| Operator | Description | Example | Result |
|----------|------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `10 - 6` | `4` |
| `*` | Multiplication | `5 * 2` | `10` |
| `/` | Division (float result) | `5 / 2` | `2.5` |
| `//` | Floor division (whole number) | `5 // 2` | `2` |
| `%` | Modulus (remainder) | `5 % 2` | `1` |
| `**` | Exponentiation | `2 ** 3` | `8` |

---
<br>

# 📦 Variables — Your Digital Folders

A **variable** is like a **dossier or folder** where you store information — instead of paper, you store numbers, text, or other data.  

**Why we use it:**  
Variables allow your program to **remember values** and use them multiple times. Instead of repeating the same value, you give it a name.

## 📝 Example:
```python
name = "Alice"
age = 25
print("Name:", name, "Age:", age)
```

<br>

# 🔢 Python Data Types — Primitives and Composites

Every value in Python has a **type**, which defines what it is and how it behaves.  
Using the correct type is important because **different types behave differently** — numbers can be calculated, strings can be combined, and collections can store multiple items.

---

### 🟢 Primitive Types
These store a **single piece of data**.

| Type       | Example            | Why We Use It                                      | Easy Example |
| ---------- | ------------------ | -------------------------------------------------- | ------------ |
| `int`      | `10`               | Whole numbers (age, count, scores)               | `age = 25` |
| `float`    | `3.14`             | Numbers with decimals (measurements, prices)    | `height = 1.75` |
| `complex`  | `1 + 2j`           | Numbers with real and imaginary parts            | `z = 2 + 3j` |
| `str`      | `"Hello"`          | Text (names, messages, sentences)               | `name = "Alice"` |
| `bool`     | `True` / `False`   | Logic values (yes/no decisions)                 | `is_student = True` |

**Examples in use:**
```python
# Integer
age = 25
print("Age:", age)

# Float
height = 1.75
print("Height:", height)

# Complex number
z = 2 + 3j
print("Complex number:", z)

# String
name = "Alice"
print("Name:", name)

# Boolean
is_student = True
print("Is a student?", is_student)
```

## 🔵 Composite Types

Composite types store **multiple pieces of data** together.  
They are useful when you want to **group related data** in one variable.

| Type    | Example            | Why We Use It                                      | What They Can Be Used For                        | Easy Example |
| ------- | ------------------ | -------------------------------------------------- | ------------------------------------------------ | ------------ |
| `list`  | `[1,2,3]`          | Ordered collection of items you can change       | Storing a shopping list, scores, or tasks       | `fruits = ["apple", "banana", "cherry"]` |
| `tuple` | `(1,2,3)`          | Ordered collection of items that **cannot change** | Storing coordinates, fixed data, or constant sequences | `colors = ("red", "green", "blue")` |
| `set`   | `{1,2,3}`          | Unordered collection of **unique** items         | Removing duplicates, finding unique elements, membership checks | `unique_numbers = {1,2,3,2,1}` |
| `dict`  | `{"name":"Alice"}` | Key-value pairs — like labeled boxes for data    | Storing structured information like profiles, phonebooks, or settings | `person = {"name":"Alice","age":25}` |


---

### 📝 Examples in Use

```python
# List (mutable)
fruits = ["apple", "banana", "cherry"]
print("First fruit:", fruits[0])
fruits.append("orange")
print("Updated list:", fruits)

# Tuple (immutable)
colors = ("red", "green", "blue")
print("First color:", colors[0])
# colors[0] = "yellow"  # This would cause an error

# Set (unique items, unordered)
unique_numbers = {1, 2, 3, 2, 1}
print(unique_numbers)  # Output: {1, 2, 3}

# Dictionary
person = {"name": "Alice", "age": 25}
print("Name:", person["name"])
print("Age:", person["age"])
```
<br>

# ⚖️ Comparison Operators in Python

Comparison operators are used to **compare two values**.  
They always return a **Boolean value** (`True` or `False`).  
These are very important in programming because they help the program **make decisions**, like checking if a number is bigger than another or if a user meets a condition.

---

### 🔹 List of Comparison Operators

| Operator | Meaning               | Example      | Result  |
| -------- | ------------------- | ----------- | ------- |
| `==`     | Equal to            | `5 == 5`    | True    |
| `!=`     | Not equal to        | `5 != 3`    | True    |
| `>`      | Greater than        | `7 > 3`     | True    |
| `<`      | Less than           | `2 < 9`     | True    |
| `>=`     | Greater than or equal | `6 >= 6`  | True    |
| `<=`     | Less than or equal  | `4 <= 5`    | True    |

---

### 🔹 Why We Use Comparators

Comparators are essential for **decision-making** in programs:

- To check **conditions** (e.g., is a number bigger than 10?)  
- To perform **different actions based on input**  
- To control **loops** (e.g., repeat something while a value is less than a limit)  

---

### 📝 Examples

```python
# Check equality
age = 18
print(age == 18)  # True

# Check inequality
score = 75
print(score != 100)  # True

# Greater or less than:
temperature = 30
print(temperature > 25)  # True
print(temperature < 20)  # False
 ```

<br>

# 🧠 Logical Operators in Python: `and`, `or`, `not`

Logical operators allow us to **combine multiple conditions** or **invert a condition**.  
They are extremely important in programming because real-world decisions often depend on **more than one factor**.

---

### 🔹 Operators Overview

| Operator | Meaning                               | Example                | Result  |
| -------- | ------------------------------------- | --------------------- | ------- |
| `and`    | True if **both conditions** are True | `True and False`      | False   |
| `or`     | True if **at least one condition** is True | `True or False`   | True    |
| `not`    | Inverts a Boolean value               | `not True`            | False   |

---

### 🔹 Why We Use Logical Operators

- To **combine multiple conditions** in a single statement.  
- To **make decisions based on more complex rules**.  
- To **invert a condition** easily instead of rewriting it.

---

### 🔹 Examples

```python
# Using and
age = 20
has_id = True
print(age >= 18 and has_id)  # True only if both conditions are True

# Using or
day = "Saturday"
is_holiday = False
print(day == "Saturday" or is_holiday)  # True if at least one condition is True

# Using not
logged_in = False
print(not logged_in)  # True because the user is not logged in
```

<br>

# ⚙️ Decision Making — if, elif, else, and match

In real life, we constantly make choices based on conditions:  
> “If it’s raining, take an umbrella. Otherwise, wear sunglasses.”

Programming is the same — we use **conditional statements** to make our programs **decide what to do** based on information or inputs.

---

## 🔹 The `if` Statement

The `if` statement checks whether a condition is **True**.  
If it is, the indented code below it runs.  
If not, Python skips that block entirely.

**Example:**
```
temperature = 30
if temperature > 25:
    print("It's a hot day!")
```

🧠 **Explanation:**  
Python checks whether `temperature > 25`.  
If the condition is True, it runs the print line.  
If False, nothing happens.

---

## 🔹 The `else` Statement

`else` gives your program something to do **when the `if` condition is False**.  
It’s like saying:  
> “If not this, then do that instead.”

**Example:**
```python
age = 16
if age >= 18:
    print("You can vote.")
else:
    print("You are too young to vote.")
```

🧠 **Why use it:**  
Without `else`, your program would only respond when the first condition is True.  
`else` ensures that *both* outcomes are handled.

---

## 🔹 The `elif` Statement (short for "else if")

Sometimes there are **more than two possibilities**.  
That’s where `elif` helps.  
Python checks each condition in order until one is True, then stops checking further.

**Example:**
```python
score = 78
if score >= 90:
    print("Excellent!")
elif score >= 50:
    print("You passed.")
else:
    print("You failed.")
```

🧠 **Explanation:**  
The program checks from top to bottom:  
- If `score >= 90` is False, it tries the next condition `score >= 50`.  
- If that’s True, it runs the corresponding code and ignores the rest.

---

## 🔹 The `match` Statement

Python 3.10 introduced `match`.
It lets you **compare one value against many fixed patterns** in a clean and readable way.

**Example:**
```python
day = "Monday"

match day:
    case "Monday":
        print("Start of the week!")
    case "Friday":
        print("Almost weekend!")
    case "Saturday" | "Sunday":
        print("It's the weekend!")
    case _:
        print("Just another day.")
```

🧠 **Explanation:**  
- `match` compares `day` to each `case`.  
- When it finds a match, it executes that block and stops.  
- The underscore `_` is the **default case**, like `else`.

---

## 💡 Summary

| Keyword | Purpose | Example Use |
|----------|----------|-------------|
| `if` | Checks a condition | `if age > 18:` |
| `elif` | Adds more conditions | `elif age == 18:` |
| `else` | Runs when all above are False | `else:` |
| `match` | Compares one value to many patterns | `match color:` |

---

**In short:**  
- `if`, `elif`, and `else` help your program make **decisions**.  
- `match` is a newer, cleaner way to check **many possibilities** for one variable.  

<br>

# 🔁 Python Loops — for, while, and Nested Loops

Loops let us **repeat tasks automatically** instead of writing the same code over and over. Once you know **how to make decisions** with if/else, loops show you **how to do things multiple times**.

---

## 🔹 The `for` Loop

The `for` loop is used when you want to **repeat something a known number of times** or **iterate over items in a collection**.

Example: iterating over numbers

```python
for i in range(5):
    print(i)
```

This prints numbers 0 to 4.

Example: iterating over a list

```python
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print('I like', fruit)
```

### 🔹 What we can do with `for` loops:

* Repeat actions a specific number of times
* Process every item in a list, tuple, or string
* Generate sequences or patterns

---

## 🔹 The `while` Loop

The `while` loop repeats code **as long as a condition is True**. Use it when you **don’t know in advance** how many times you need to repeat.

Example: simple counter


```python
i = 0
while i < 5:
    print(i)
    i += 1
```

Example: waiting for user input

```python
password = ''
while password != 'python123':
    password = input('Enter password: ')
print('Access granted')
```

### 🔹 What we can do with `while` loops:

* Keep repeating until a certain condition is met
* Build interactive programs that wait for user input
* Handle situations where the number of repetitions is unknown

---

## 🔹 Nested Loops

A nested loop is a loop **inside another loop**. They are useful when working with **grids, tables, or combinations of items**.

Example: printing a multiplication table


```python
for i in range(1, 6):
    for j in range(1, 6):
        print(i*j, end=' ')
    print()
```

Example: iterating over a list of lists


```python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
for row in matrix:
    for value in row:
        print(value, end=' ')
    print()
```

### 🔹 What we can do with nested loops:

* Work with tables, grids, or multi-dimensional data
* Generate patterns or shapes
* Combine every item from one list with every item from another

---

## 💡 Key Points

* `for` loops: use when you **know how many times** to repeat or want to iterate over items
* `while` loops: use when you **repeat until a condition is False**, number of repetitions unknown
* Nested loops: use when **repetition requires multiple levels**, like rows and columns in a table
