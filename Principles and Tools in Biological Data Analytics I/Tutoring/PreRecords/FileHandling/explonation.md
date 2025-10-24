# 📁 Python File Handling — Reading and Writing Files

In Python, **file handling** lets you work with files on your computer — reading data from them, writing data to them, and much more.
It's an essential skill for building real applications that need to save data, process documents, or work with external files.

Think of file handling like **opening a book** 📖 — you open it, read or write in it, and then close it when you're done.

---

## 📖 What Is File Handling?

**File handling** is the process of working with files stored on your computer. You can:

* **Read** data from existing files
* **Write** new data to files
* **Append** data to the end of files
* **Create** new files
* **Delete** or **rename** files

```python
# Opening a file
file = open("example.txt", "r")  # "r" means read mode
content = file.read()
print(content)
file.close()  # Always close the file when done!
```

Here's what each part means:

* `open("example.txt", "r")` → opens the file in **read mode**
* `file.read()` → reads all the content from the file
* `file.close()` → closes the file (important!)
* Always close files to free up computer resources

---

## 🔑 File Modes — How to Open Files

When opening a file, you need to specify a **mode** that tells Python what you want to do:

| Mode | Name            | Description                                      | Creates File? |
| ---- | --------------- | ------------------------------------------------ | ------------- |
| `"r"` | Read           | Read from file (file must exist)                 | No            |
| `"w"` | Write          | Write to file (overwrites if exists)             | Yes           |
| `"a"` | Append         | Add to end of file (keeps existing content)      | Yes           |
| `"x"` | Exclusive      | Create new file (fails if exists)                | Yes           |
| `"r+"` | Read & Write  | Read and write (file must exist)                 | No            |

```python
# Read mode
file = open("data.txt", "r")

# Write mode (overwrites everything!)
file = open("data.txt", "w")

# Append mode (adds to the end)
file = open("data.txt", "a")
```

* Use `"r"` when you only want to read
* Use `"w"` carefully — it **deletes** all existing content!
* Use `"a"` to add new content without deleting the old

---

## 📥 Reading Files

### Reading the Entire File

```python
# Method 1: read() - reads everything as one string
file = open("story.txt", "r")
content = file.read()
print(content)
file.close()
```

### Reading Line by Line

```python
# Method 2: readline() - reads one line at a time
file = open("story.txt", "r")
line1 = file.readline()
line2 = file.readline()
print(line1)
print(line2)
file.close()
```

### Reading All Lines into a List

```python
# Method 3: readlines() - reads all lines into a list
file = open("story.txt", "r")
lines = file.readlines()
for line in lines:
    print(line.strip())  # strip() removes extra newlines
file.close()
```

### Reading with a Loop (Best Practice!)

```python
# Method 4: Loop through the file (memory efficient!)
file = open("story.txt", "r")
for line in file:
    print(line.strip())
file.close()
```

* `read()` → entire file as one string
* `readline()` → one line at a time
* `readlines()` → all lines in a list
* Looping through the file → best for large files!

---

## 📤 Writing to Files

### Writing Text to a File

```python
# Write mode - creates new file or overwrites existing
file = open("output.txt", "w")
file.write("Hello, World!\n")
file.write("This is a new line.\n")
file.close()
```

**⚠️ Warning:** Write mode (`"w"`) will **delete** all existing content!

### Writing Multiple Lines

```python
lines = ["First line\n", "Second line\n", "Third line\n"]

file = open("output.txt", "w")
file.writelines(lines)  # Write multiple lines at once
file.close()
```

### Appending to a File

```python
# Append mode - adds to the end without deleting
file = open("log.txt", "a")
file.write("New log entry\n")
file.close()
```

* `write()` → write a single string
* `writelines()` → write a list of strings
* Use `"a"` mode to **add** content instead of replacing

---

## 🛡️ The `with` Statement — Automatic File Closing

The best way to work with files is using `with` — it **automatically closes** the file for you, even if an error happens!

```python
# The old way (manual closing)
file = open("data.txt", "r")
content = file.read()
file.close()  # Easy to forget!

# The better way (automatic closing)
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here!
```

**Why use `with`?**
* Automatically closes the file
* Safer — closes even if there's an error
* Cleaner code
* Always use `with` when possible!

---

## 🔄 Reading and Writing Together

### Reading a File and Writing to Another

```python
# Read from one file and write to another
with open("input.txt", "r") as input_file:
    content = input_file.read()

with open("output.txt", "w") as output_file:
    output_file.write(content.upper())  # Convert to uppercase
```

### Processing a File Line by Line

```python
# Read a file, process each line, and save to a new file
with open("numbers.txt", "r") as input_file:
    with open("doubled.txt", "w") as output_file:
        for line in input_file:
            number = int(line.strip())
            doubled = number * 2
            output_file.write(str(doubled) + "\n")
```

* You can nest `with` statements
* Process large files without loading everything into memory
* Common pattern for data transformation

---

## 📊 Practical Examples

### Example 1: Creating a Simple To-Do List 📝

```python
# Adding tasks to a to-do list
def add_task(task):
    with open("todo.txt", "a") as file:
        file.write(task + "\n")

# Reading all tasks
def show_tasks():
    try:
        with open("todo.txt", "r") as file:
            print("📋 Your To-Do List:")
            for i, line in enumerate(file, 1):
                print(f"{i}. {line.strip()}")
    except FileNotFoundError:
        print("No tasks yet!")

# Usage
add_task("Buy groceries")
add_task("Study Python")
show_tasks()
```

### Example 2: Counting Words in a File 📊

```python
def count_words(filename):
    try:
        with open(filename, "r") as file:
            content = file.read()
            words = content.split()
            return len(words)
    except FileNotFoundError:
        return 0

word_count = count_words("essay.txt")
print(f"The file contains {word_count} words.")
```

### Example 3: Creating a Simple Log File 📜

```python
from datetime import datetime

def log_message(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    log_entry = f"[{timestamp}] {message}\n"
    
    with open("app.log", "a") as file:
        file.write(log_entry)

# Usage
log_message("Application started")
log_message("User logged in")
log_message("Error: Connection timeout")
```

---

## ⚠️ Error Handling with Files

Files can cause errors! The file might not exist, or you might not have permission to read it. Always use **error handling**:

```python
# Without error handling (BAD!)
file = open("missing.txt", "r")  # Crashes if file doesn't exist!

# With error handling (GOOD!)
try:
    with open("missing.txt", "r") as file:
        content = file.read()
        print(content)
except FileNotFoundError:
    print("❌ Error: File not found!")
except PermissionError:
    print("❌ Error: No permission to read this file!")
except Exception as e:
    print(f"❌ Unexpected error: {e}")
```

**Common file errors:**
* `FileNotFoundError` → file doesn't exist
* `PermissionError` → no permission to access file
* `IsADirectoryError` → tried to open a folder as a file
* Always use `try-except` when working with files!

---

## 🗂️ Checking if a File Exists

Before opening a file, you might want to check if it exists:

```python
import os

# Check if file exists
if os.path.exists("data.txt"):
    print("✅ File exists!")
else:
    print("❌ File not found!")

# Check if it's a file (not a folder)
if os.path.isfile("data.txt"):
    print("✅ It's a file!")

# Check if it's a directory
if os.path.isdir("my_folder"):
    print("✅ It's a directory!")
```

* `os.path.exists()` → checks if file or folder exists
* `os.path.isfile()` → checks if it's specifically a file
* `os.path.isdir()` → checks if it's a directory

---

## 🗑️ Deleting and Renaming Files

```python
import os

# Delete a file
if os.path.exists("old_file.txt"):
    os.remove("old_file.txt")
    print("🗑️ File deleted!")

# Rename a file
if os.path.exists("old_name.txt"):
    os.rename("old_name.txt", "new_name.txt")
    print("✏️ File renamed!")

# Get file size
size = os.path.getsize("data.txt")
print(f"📏 File size: {size} bytes")
```

* `os.remove()` → delete a file
* `os.rename()` → rename or move a file
* `os.path.getsize()` → get file size in bytes
* Always check if file exists first!

---

## 🎯 Best Practices

### ✅ Do's:
* **Always use `with`** for automatic file closing
* **Use `try-except`** to handle errors
* **Close files** if not using `with`
* **Use `"r"`** as default mode (safest)
* **Check if file exists** before deleting or renaming

### ❌ Don'ts:
* Don't forget to close files manually
* Don't use `"w"` mode carelessly (it deletes everything!)
* Don't ignore errors (use try-except)
* Don't read huge files all at once (use line-by-line reading)
* Don't hardcode file paths (use `os.path.join()` for portability)

---

## 💡 Summary

| Concept          | Description                              | Example                           |
| ---------------- | ---------------------------------------- | --------------------------------- |
| **File Modes**   | How to open files                        | `"r"`, `"w"`, `"a"`               |
| **Reading**      | Get data from files                      | `read()`, `readline()`            |
| **Writing**      | Save data to files                       | `write()`, `writelines()`         |
| **with**         | Automatic file closing                   | `with open(...) as file:`         |
| **Error Handling** | Handle file errors safely              | `try-except FileNotFoundError`    |
| **os Module**    | File operations (delete, rename, check)  | `os.remove()`, `os.path.exists()` |
| **Best Practice** | Always use `with` and error handling    | Safe and clean code               |

File handling helps you move from working with temporary data to building **real applications that save and process information**. 🚀