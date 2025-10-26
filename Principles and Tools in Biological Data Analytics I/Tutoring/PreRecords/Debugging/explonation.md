# Debugging in Python: A Beginner's Guide

**Debugging** is the process of finding and fixing errors (bugs) in your code. Every programmer debugs - it's a normal part of coding! This guide will teach you how to find and fix bugs like a pro.

## Types of Errors

### 1. Syntax Errors

These happen when you break Python's grammar rules. Python won't run at all.

```python
# Missing colon
if x > 5
    print("Big number")

# SyntaxError: invalid syntax
```

**How to fix:** Read the error message - it tells you the line number!

**Common syntax errors:**
- Missing colons (`:`) after `if`, `for`, `while`, `def`
- Mismatched parentheses, brackets, or quotes
- Wrong indentation
- Misspelled keywords

### 2. Runtime Errors

The code looks correct, but crashes when running.

```python
numbers = [1, 2, 3]
print(numbers[5])

# IndexError: list index out of range
```

**Common runtime errors:**
- `IndexError` - Trying to access a list index that doesn't exist
- `KeyError` - Accessing a dictionary key that doesn't exist
- `ZeroDivisionError` - Dividing by zero
- `TypeError` - Using wrong data type for an operation
- `ValueError` - Right type, wrong value
- `FileNotFoundError` - File doesn't exist
- `AttributeError` - Object doesn't have that attribute/method

### 3. Logic Errors

The code runs but gives wrong results. These are the hardest to find!

```python
# Trying to calculate average
total = 10 + 20 + 30
average = total / 2  # Should be / 3

print(average)  # Output: 30 (wrong!)
```

Logic errors don't crash your program, so you need to test your code carefully to find them.

## Debugging Techniques

### 1. Print Debugging (Simplest Method)

Add `print()` statements to see what's happening. This is the most common debugging method for beginners!

```python
def calculate_total(prices):
    total = 0
    for price in prices:
        print(f"Adding: {price}")  # Debug print
        total += price
        print(f"Current total: {total}")  # Debug print
    return total

result = calculate_total([10, 20, 30])
print(f"Final result: {result}")
```

**Output:**
```
Adding: 10
Current total: 10
Adding: 20
Current total: 30
Adding: 30
Current total: 60
Final result: 60
```

**Tips for print debugging:**
- Use descriptive messages: `print(f"User age: {age}")` not just `print(age)`
- Print before and after important operations
- Print the type of variables: `print(type(variable))`
- Remove or comment out debug prints when done

### 2. Using the Python Debugger (pdb)

The built-in debugger lets you pause code execution and inspect variables step-by-step.

```python
import pdb

def divide(a, b):
    pdb.set_trace()  # Execution pauses here
    result = a / b
    return result

divide(10, 2)
```

When the code hits `pdb.set_trace()`, it opens an interactive debugger in your terminal.

**Common pdb commands:**

| Command | Description |
|---------|-------------|
| `n` (next) | Execute the next line |
| `s` (step) | Step into a function |
| `c` (continue) | Continue until next breakpoint |
| `p variable_name` | Print variable value |
| `pp variable_name` | Pretty-print variable |
| `l` (list) | Show code around current line |
| `w` (where) | Show the call stack |
| `q` (quit) | Exit debugger |
| `h` (help) | Show help |

**Example debugging session:**
```
> /path/to/file.py(4)divide()
-> result = a / b
(Pdb) p a
10
(Pdb) p b
2
(Pdb) n
> /path/to/file.py(5)divide()
-> return result
(Pdb) p result
5.0
(Pdb) c
```

### 3. Using breakpoint() (Python 3.7+)

A simpler, more modern way to use the debugger:

```python
def calculate(x, y):
    breakpoint()  # Modern way to set breakpoint
    result = x * y + 10
    return result

calculate(5, 3)
```

`breakpoint()` is exactly like `pdb.set_trace()` but shorter and more readable!

### 4. Try-Except Blocks (Error Handling)

Catch errors before they crash your program and handle them gracefully.

```python
def safe_divide(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Error: Cannot divide by zero!")
        return None
    except TypeError:
        print("Error: Please provide numbers!")
        return None

print(safe_divide(10, 2))    # Output: 5.0
print(safe_divide(10, 0))    # Output: Error: Cannot divide by zero!
print(safe_divide(10, "x"))  # Output: Error: Please provide numbers!
```

**More advanced error handling:**

```python
def read_file(filename):
    try:
        with open(filename, 'r') as f:
            content = f.read()
            return content
    except FileNotFoundError:
        print(f"File '{filename}' not found!")
    except PermissionError:
        print(f"No permission to read '{filename}'!")
    except Exception as e:
        # Catch any other errors
        print(f"Unexpected error: {e}")
    finally:
        # This runs no matter what
        print("Finished attempting to read file")
```

**Getting error details:**

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error occurred: {e}")
    print(f"Error type: {type(e).__name__}")
```

### 5. Logging (Better than Print for Large Projects)

The `logging` module is like print debugging, but more powerful and professional.

```python
import logging

# Set up logging
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def process_data(data):
    logging.debug(f"Starting to process: {data}")
    
    if not isinstance(data, (int, float)):
        logging.error(f"Invalid data type: {type(data)}")
        return None
    
    result = data * 2
    logging.info(f"Processing complete: {result}")
    return result

process_data(10)
process_data("invalid")
```

**Output:**
```
2025-10-25 10:30:15,123 - DEBUG - Starting to process: 10
2025-10-25 10:30:15,124 - INFO - Processing complete: 20
2025-10-25 10:30:15,125 - DEBUG - Starting to process: invalid
2025-10-25 10:30:15,126 - ERROR - Invalid data type: <class 'str'>
```

**Log levels** (from least to most serious):

| Level | When to Use |
|-------|-------------|
| `DEBUG` | Detailed information for diagnosing problems |
| `INFO` | Confirmation that things are working as expected |
| `WARNING` | Something unexpected happened, but the program continues |
| `ERROR` | A serious problem occurred |
| `CRITICAL` | The program may not be able to continue |

**Logging to a file:**

```python
logging.basicConfig(
    filename='app.log',
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s'
)
```

## Debugging in Different Environments

### Debugging in Jupyter Notebooks

Jupyter has special features that make debugging easier!

#### Method 1: Cell-by-Cell Debugging

The best feature of Jupyter - run cells one at a time and check outputs:

```python
# Cell 1
data = [1, 2, 3, 4, 5]
print(f"Data: {data}")
```

```python
# Cell 2
total = sum(data)
print(f"Total: {total}")
```

```python
# Cell 3
average = total / len(data)
print(f"Average: {average}")
```

If there's a bug, you know exactly which cell caused it!

#### Method 2: Using %debug Magic Command

When a cell crashes, run this in the next cell:

```python
# Cell that crashed
def buggy_function():
    x = 10
    y = 0
    return x / y

buggy_function()  # ZeroDivisionError
```

```python
# Next cell
%debug
```

This opens an interactive debugger right where the error occurred!

#### Method 3: Using %%debug Cell Magic

Debug an entire cell:

```python
%%debug
def problematic_code():
    values = [1, 2, 3]
    print(values[10])  # This will error

problematic_code()
```

### Debugging in VS Code

VS Code has powerful visual debugging tools for Python files.

**Setting up:**
1. Open your `.py` file in VS Code
2. Click to the left of line numbers to set breakpoints (red dot appears)
3. Press `F5` or click "Run and Debug" in the sidebar
4. Select "Python File" when prompted

**Features:**
- **Breakpoints**: Pause execution at specific lines
- **Step Over (F10)**: Execute current line, move to next
- **Step Into (F11)**: Go inside function calls
- **Step Out (Shift+F11)**: Exit current function
- **Continue (F5)**: Run until next breakpoint
- **Variables Panel**: See all variable values
- **Watch Panel**: Track specific variables
- **Call Stack**: See function call history

## Reading Error Messages

Error messages (tracebacks) tell you what went wrong, where, and why. Learn to read them!

```python
Traceback (most recent call last):
  File "script.py", line 10, in <module>
    result = calculate_average(numbers)
  File "script.py", line 5, in calculate_average
    return sum(nums) / len(nums)
ZeroDivisionError: division by zero
```

**How to read this:**

Read from **bottom to top**:
1. **Bottom line**: `ZeroDivisionError: division by zero` - The actual error
2. **Above it**: `return sum(nums) / len(nums)` - The line that caused the error
3. **File info**: `File "script.py", line 5` - Where the error is
4. **Call stack**: Shows how you got there (useful for complex programs)

**What to look for:**
- The error type (e.g., `ZeroDivisionError`)
- The line number
- The actual line of code that failed
- The file name

## Common Debugging Strategies

### Strategy 1: The "Rubber Duck" Method

Explain your code line-by-line to a rubber duck (or any object, or even out loud to yourself). Often you'll spot the bug while explaining!

**Why it works:** Forcing yourself to explain makes you think differently about the code.

### Strategy 2: Binary Search Debugging

If a large program is broken:
1. Comment out half the code
2. If it works, the bug is in the commented part
3. If it still breaks, the bug is in the running part
4. Repeat until you find the bug

```python
# Original code - something is broken
function1()
function2()
function3()
function4()
function5()

# Try this
function1()
function2()
# function3()
# function4()
# function5()

# Still broken? The bug is in function1() or function2()
# Fixed? The bug is in function3(), 4(), or 5()
```

### Strategy 3: Simplify the Problem

If your code is complex, create a minimal version that reproduces the bug:

```python
# Complex broken code
def process_user_data(users):
    results = []
    for user in users:
        if user['age'] > 18 and user['verified']:
            results.append(calculate_score(user))
    return results

# Simplified version to test
def test_simple():
    user = {'age': 20, 'verified': True}
    score = calculate_score(user)
    print(score)

test_simple()  # Now you can see if calculate_score() is the problem
```

### Strategy 4: Add Assertions

Use `assert` to check assumptions:

```python
def calculate_discount(price, discount_percent):
    assert price > 0, "Price must be positive"
    assert 0 <= discount_percent <= 100, "Discount must be 0-100"
    
    discount = price * (discount_percent / 100)
    return price - discount

calculate_discount(-50, 20)  # AssertionError: Price must be positive
```

### Strategy 5: Test with Simple Inputs

If your function fails with complex data, test with the simplest possible input:

```python
def process_list(items):
    # Failing with real data
    # Test with simple data first
    pass

# Instead of
process_list([complex_object1, complex_object2, ...])

# Try
process_list([1])  # Simplest list
process_list([])   # Empty list
process_list([1, 2])  # Two items
```

## Best Practices to Prevent Bugs

### 1. Write Small Functions

```python
# Bad - hard to debug
def do_everything(data):
    # 100 lines of code
    pass

# Good - easy to test and debug
def validate_data(data):
    pass

def process_data(data):
    pass

def save_results(results):
    pass
```

### 2. Test as You Go

Don't write 100 lines then test. Write a function, test it, then move on.

```python
def add(a, b):
    return a + b

# Test immediately
print(add(2, 3))  # Should be 5
print(add(-1, 1))  # Should be 0
```

### 3. Use Meaningful Variable Names

```python
# Bad - hard to debug
x = u * 0.8

# Good - easy to understand
discounted_price = original_price * 0.8
```

### 4. Add Comments for Tricky Parts

```python
def calculate_tax(income):
    # Tax rates: 0-10k: 10%, 10k-50k: 20%, 50k+: 30%
    if income <= 10000:
        return income * 0.10
    elif income <= 50000:
        return 1000 + (income - 10000) * 0.20
    else:
        return 9000 + (income - 50000) * 0.30
```

### 5. Use Type Hints (Intermediate)

```python
def greet(name: str, age: int) -> str:
    return f"Hello {name}, you are {age} years old"

# This helps catch bugs early
greet("Alice", "twenty")  # IDE will warn about wrong type
```

### 6. Write Unit Tests (Advanced)

```python
def add(a, b):
    return a + b

# Test function
def test_add():
    assert add(2, 3) == 5
    assert add(-1, 1) == 0
    assert add(0, 0) == 0
    print("All tests passed!")

test_add()
```

## Debugging Checklist

When you encounter a bug, go through this checklist:

- [ ] **Read the error message carefully** - What type of error? What line?
- [ ] **Check the line number mentioned** - Look at that line and nearby lines
- [ ] **Add print statements** - Print variables before the error
- [ ] **Check variable types** - Use `print(type(variable))`
- [ ] **Check variable values** - Are they what you expect?
- [ ] **Try with simpler input** - Use simple test data
- [ ] **Comment out code** - Binary search to isolate the problem
- [ ] **Search online** - Copy the error message into Google
- [ ] **Read documentation** - Are you using the function correctly?
- [ ] **Take a break** - Fresh eyes find bugs faster!

## Common Beginner Mistakes

### 1. Indentation Errors

```python
# Wrong
def greet(name):
print(f"Hello {name}")  # IndentationError

# Correct
def greet(name):
    print(f"Hello {name}")
```

### 2. Using = Instead of ==

```python
# Wrong - assigns 5 to x
if x = 5:
    print("x is 5")

# Correct - compares x to 5
if x == 5:
    print("x is 5")
```

### 3. Modifying a List While Iterating

```python
# Wrong - can skip elements
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)

# Correct - iterate over a copy
numbers = [1, 2, 3, 4, 5]
for num in numbers[:]:
    if num % 2 == 0:
        numbers.remove(num)
```

### 4. Not Handling None Returns

```python
# Wrong
result = some_function()
print(result.upper())  # AttributeError if result is None

# Correct
result = some_function()
if result is not None:
    print(result.upper())
```

## Resources for Getting Help

When you're stuck:

1. **Read the error message** - It usually tells you the problem
2. **Google the error** - Copy the error message (without your specific values)
3. **Stack Overflow** - Search for similar questions
4. **Python Documentation** - Official docs at docs.python.org
5. **Ask AI assistants** - ChatGPT, Claude, etc. can explain errors
6. **Python communities** - r/learnpython, Python Discord servers

## Summary

- **Debugging is normal** - Every programmer does it constantly
- **Start simple** - Use print statements before complex tools
- **Read error messages** - They tell you what, where, and why
- **Test as you go** - Don't write too much code before testing
- **Use the right tool** - Print for simple bugs, debugger for complex ones
- **Take breaks** - Fresh perspective helps find bugs
- **Search online** - Someone else has probably had the same error

Remember: Debugging is a skill that improves with practice. The more you debug, the faster you'll get at finding and fixing bugs!
