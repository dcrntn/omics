# 🔄 Python Recursion — Functions That Call Themselves

In Python, **recursion** is when a function calls itself to solve a problem by breaking it down into smaller, similar problems.
It's one of the most elegant techniques in programming for handling complex, nested structures.

Think of recursion like **Russian nesting dolls** 🪆 — each doll contains a smaller version of itself, until you reach the tiniest one that can't be opened anymore.

---

## 🤔 What Is Recursion?

**Recursion** is a programming technique where a function solves a problem by calling itself with simpler inputs.

```python
def countdown(n):
    # Base case: stop when we reach 0
    if n <= 0:
        print("Blastoff! 🚀")
        return
    
    # Do something
    print(n)
    
    # Recursive case: call ourselves with a smaller number
    countdown(n - 1)

countdown(5)
```

Output:
```
5
4
3
2
1
Blastoff! 🚀
```

Here's what each part means:

* `countdown(n)` → the function that will call itself
* `if n <= 0:` → the **base case** that stops the recursion
* `countdown(n - 1)` → the **recursive call** with a simpler problem
* Without a base case, the function would run forever!

---

## 📜 The Two Rules of Recursion

Every recursive function MUST have these two parts:

1. **🛑 Base Case** — The condition that stops the recursion (like the smallest Russian doll that doesn't open)
2. **🔄 Recursive Case** — The part where the function calls itself with a simpler version of the problem

```python
def factorial(n):
    # Base case: stop when n is 1 or less
    if n <= 1:
        return 1
    
    # Recursive case: n! = n × (n-1)!
    return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```

* Base case: `if n <= 1: return 1`
* Recursive case: `return n * factorial(n - 1)`
* Each call solves a smaller problem until reaching the base case

---

## 🔍 How Does Recursion Work?

When you call `factorial(5)`, here's what happens step by step:

```
factorial(5)
  = 5 × factorial(4)
  = 5 × 4 × factorial(3)
  = 5 × 4 × 3 × factorial(2)
  = 5 × 4 × 3 × 2 × factorial(1)
  = 5 × 4 × 3 × 2 × 1
  = 120
```

Each function call waits for the one it called to finish before it can complete. This creates a **call stack**:

```
countdown(3) → prints 3, then calls countdown(2)
  countdown(2) → prints 2, then calls countdown(1)
    countdown(1) → prints 1, then calls countdown(0)
      countdown(0) → prints "Blastoff! 🚀", then stops
```

---

## 💡 When Is Recursion Better Than Loops?

### Example 1: Exploring Folders and Subfolders 📁

Imagine you want to find all files in a folder, including files in subfolders, subfolders of subfolders, and so on...

**With a Loop 😰 (Much Harder!)**

```python
import os

def list_all_files_loop(directory):
    # We need to manually track folders to visit
    folders_to_check = [directory]
    
    while folders_to_check:
        current_folder = folders_to_check.pop(0)
        
        try:
            items = os.listdir(current_folder)
        except PermissionError:
            continue
        
        for item in items:
            full_path = os.path.join(current_folder, item)
            
            if os.path.isfile(full_path):
                print(f"📄 File: {full_path}")
            elif os.path.isdir(full_path):
                print(f"📁 Folder: {full_path}")
                # Add this folder to our list to check later
                folders_to_check.append(full_path)

# This is complicated! We need to manually track folders 😓
```

**With Recursion 🎉 (Much Simpler!)**

```python
import os

def list_all_files_recursive(directory, indent=0):
    try:
        items = os.listdir(directory)
    except PermissionError:
        return
    
    for item in items:
        full_path = os.path.join(directory, item)
        
        if os.path.isfile(full_path):
            print("  " * indent + f"📄 {item}")
        elif os.path.isdir(full_path):
            print("  " * indent + f"📁 {item}/")
            # Just call ourselves on the subfolder - easy!
            list_all_files_recursive(full_path, indent + 1)

# So much cleaner! 🎨
```

**Why is recursion easier here?**
* Folders can contain folders, which can contain folders... it's naturally recursive!
* The loop version has to manually keep track of all folders using a list
* The recursive version just lets Python handle that for us

---

### Example 2: Finding All Python Files in a Project 🔍

Let's say you want to find all `.py` files in a project folder (including all subfolders):

```python
import os

def find_python_files(directory):
    """Find all .py files in directory and subdirectories"""
    python_files = []
    
    try:
        items = os.listdir(directory)
    except PermissionError:
        return python_files
    
    for item in items:
        full_path = os.path.join(directory, item)
        
        if os.path.isfile(full_path) and item.endswith('.py'):
            python_files.append(full_path)
        elif os.path.isdir(full_path):
            # Recursive call: search in the subfolder
            python_files.extend(find_python_files(full_path))
    
    return python_files

# Usage
files = find_python_files('/path/to/project')
for file in files:
    print(f"Found: {file}")
```

Try doing this with a loop - it gets messy fast! 😵

---

### Example 3: Sum of a List 📝

**With a Loop 🔁**

```python
def sum_list_loop(numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_list_loop([1, 2, 3, 4, 5]))  # Output: 15
```

**With Recursion 🔄**

```python
def sum_list_recursive(numbers):
    # Base case: empty list sums to 0
    if not numbers:
        return 0
    
    # Recursive case: first number + sum of the rest
    return numbers[0] + sum_list_recursive(numbers[1:])

print(sum_list_recursive([1, 2, 3, 4, 5]))  # Output: 15
```

For this simple example, loops are actually better! Recursion shines when the problem is naturally recursive (like exploring nested folders).

---

## 🧮 More Recursion Examples

### Fibonacci Sequence

The Fibonacci sequence is: 0, 1, 1, 2, 3, 5, 8, 13...
Each number is the sum of the two before it.

```python
def fibonacci(n):
    # Base cases
    if n <= 0:
        return 0
    if n == 1:
        return 1
    
    # Recursive case: fib(n) = fib(n-1) + fib(n-2)
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # Output: 8
```

### Reversing a String

```python
def reverse_string(text):
    # Base case: empty or single character
    if len(text) <= 1:
        return text
    
    # Recursive case: last char + reverse of the rest
    return text[-1] + reverse_string(text[:-1])

print(reverse_string("hello"))  # Output: olleh
```

### Counting Folders

```python
import os

def count_folders(directory):
    """Count total folders in directory and subdirectories"""
    count = 0
    
    try:
        items = os.listdir(directory)
    except PermissionError:
        return 0
    
    for item in items:
        full_path = os.path.join(directory, item)
        
        if os.path.isdir(full_path):
            count += 1  # Count this folder
            count += count_folders(full_path)  # Count subfolders
    
    return count
```

---

## ⚠️ Common Mistakes to Avoid

### Mistake #1: Forgetting the Base Case 🚫

```python
# WRONG! This will crash your program
def bad_countdown(n):
    print(n)
    bad_countdown(n - 1)  # Never stops!

# RIGHT! Always have a base case
def good_countdown(n):
    if n <= 0:  # Base case
        return
    print(n)
    good_countdown(n - 1)
```

Without a base case, you'll get:
```
RecursionError: maximum recursion depth exceeded
```

### Mistake #2: Base Case That Never Gets Reached 🎯

```python
# WRONG! The base case will never be true
def bad_function(n):
    if n == 0:  # Base case
        return
    bad_function(n - 2)  # If n is odd, we'll skip right over 0!

# RIGHT! Make sure you'll always hit the base case
def good_function(n):
    if n <= 0:  # This will catch 0, -1, -2, etc.
        return
    good_function(n - 2)
```

### Mistake #3: Not Moving Toward the Base Case 📉

```python
# WRONG! n never gets smaller
def bad_factorial(n):
    if n == 1:
        return 1
    return n * bad_factorial(n)  # Oops! Should be n-1

# RIGHT! Each call should be simpler
def good_factorial(n):
    if n == 1:
        return 1
    return n * good_factorial(n - 1)  # n gets smaller each time
```

---

## 🚧 Recursion Limits

Python has a safety limit (usually 1000 levels deep) to prevent infinite recursion:

```python
import sys
print(sys.getrecursionlimit())  # Check limit (usually 1000)

# You can increase it if needed (use carefully!)
sys.setrecursionlimit(2000)
```

If you exceed the limit:
```python
def infinite_recursion(n):
    return infinite_recursion(n)

# This will crash with: RecursionError: maximum recursion depth exceeded
```

---

## 🎯 Tail Recursion vs Non-Tail Recursion

There are two types of recursion based on **when** the recursive call happens:

### Non-Tail Recursion (Most Common) 📊

In **non-tail recursion**, the function does something **after** the recursive call returns.

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)  # Multiplication happens AFTER recursive call
    #      ↑ Work done after return
```

**What happens:**
```
factorial(4)
  = 4 * factorial(3)
  = 4 * (3 * factorial(2))
  = 4 * (3 * (2 * factorial(1)))
  = 4 * (3 * (2 * 1))
  = 4 * (3 * 2)
  = 4 * 6
  = 24
```

* Each call must wait for the next call to finish
* Python keeps all calls in memory (the call stack)
* Uses more memory as recursion goes deeper

### Tail Recursion (More Efficient) 🚀

In **tail recursion**, the recursive call is the **last thing** the function does (no work after it).

```python
def factorial_tail(n, accumulator=1):
    if n <= 1:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)  # Nothing after this!
    #      ↑ This is the last operation
```

**What happens:**
```
factorial_tail(4, 1)
  = factorial_tail(3, 4)
  = factorial_tail(2, 12)
  = factorial_tail(1, 24)
  = 24
```

* No waiting for calls to return
* Result is passed along in the accumulator
* Could be optimized by the compiler (though Python doesn't do this)

### Side-by-Side Comparison 🔄

**Non-Tail: Counting Down**
```python
def countdown_non_tail(n):
    if n <= 0:
        print("Blastoff! 🚀")
        return
    print(n)
    countdown_non_tail(n - 1)
    print(f"Back at {n}")  # Work done AFTER recursive call
```

Output:
```
5
4
3
2
1
Blastoff! 🚀
Back at 1
Back at 2
Back at 3
Back at 4
Back at 5
```

**Tail: Counting Down**
```python
def countdown_tail(n):
    if n <= 0:
        print("Blastoff! 🚀")
        return
    print(n)
    countdown_tail(n - 1)  # Last operation - nothing after this
```

Output:
```
5
4
3
2
1
Blastoff! 🚀
```

### Another Example: Sum of Numbers 🧮

**Non-Tail Version:**
```python
def sum_non_tail(n):
    if n <= 0:
        return 0
    return n + sum_non_tail(n - 1)  # Addition AFTER recursive call
```

**Tail Version:**
```python
def sum_tail(n, accumulator=0):
    if n <= 0:
        return accumulator
    return sum_tail(n - 1, accumulator + n)  # Pass result along
```

Both give the same result, but tail recursion is more memory efficient!

### Key Differences 📋

| Aspect              | Non-Tail Recursion              | Tail Recursion                    |
| ------------------- | ------------------------------- | --------------------------------- |
| **Work After Call** | Yes (multiplication, addition)  | No (call is the last thing)       |
| **Memory Usage**    | Higher (stack builds up)        | Lower (could be optimized)        |
| **Call Stack**      | Grows with each call            | Could be constant (with TCO)      |
| **Python Support**  | ✅ Fully supported              | ✅ Works, but not optimized       |
| **Readability**     | Often more intuitive            | May need accumulator parameter    |

**Note:** Python doesn't optimize tail recursion (unlike some other languages), so both types use the same amount of memory in Python. However, understanding tail recursion helps you write better code in other languages!

---

## 🆚 Recursion vs Loops — When to Use Each?

| Aspect            | Recursion 🔄                          | Loops 🔁                              |
| ----------------- | ------------------------------------- | ------------------------------------- |
| **Readability**   | Often cleaner for complex problems    | Can be verbose                        |
| **Memory**        | Uses call stack (can overflow)        | Uses less memory                      |
| **Performance**   | Generally slower (function overhead)  | Usually faster                        |
| **Best For**      | Trees, folders, nested structures     | Simple counting, basic iteration      |
| **Learning Curve** | Harder to understand at first        | More intuitive for beginners          |

### Use Recursion When: ✅
* Working with tree-like structures (folders, family trees, etc.)
* The problem naturally breaks into smaller versions of itself
* The code is much simpler with recursion
* You're traversing nested data (JSON, XML, directory trees)

### Use Loops When: ✅
* Simple counting or iteration
* Performance is critical (loops are faster)
* The problem is straightforward
* You need to process large datasets (to avoid stack overflow)

---

## 💡 Summary

| Concept           | Description                                   | Example                          |
| ----------------- | --------------------------------------------- | -------------------------------- |
| **Recursion**     | Function calling itself                       | `countdown(n - 1)`               |
| **Base Case**     | Condition that stops recursion                | `if n <= 0: return`              |
| **Recursive Case** | Function calling itself with simpler input   | `return n * factorial(n - 1)`    |
| **Call Stack**    | How Python tracks function calls              | Each call waits for the next     |
| **Best Use**      | Nested structures, trees, folders             | Directory traversal              |
| **Common Mistake** | Forgetting base case                         | Infinite recursion               |
| **Limitation**    | Stack overflow with too many calls            | Python limit ~1000 calls         |

Recursion helps you move from writing simple loops to solving **complex, nested problems** elegantly.