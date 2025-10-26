# Python Files vs Jupyter Notebooks: A Beginner's Guide

## What is a Basic Python File?

A **Python file** (with a `.py` extension) is a plain text file that contains Python code. Think of it like a recipe written from start to finish - you write all your instructions in order, save the file, and then run it all at once.

### Example: `hello.py`
```python
print("Hello, World!")
name = "Alice"
print(f"Welcome, {name}!")
```

When you run this file, Python reads it from top to bottom and executes everything in sequence.

## What is a Jupyter Notebook?

A **Jupyter Notebook** (with a `.ipynb` extension) is an interactive document that lets you write and run code in small chunks called "cells". It's like a digital lab notebook where you can:
- Write code in one cell and run it immediately
- See the results right below the code
- Add explanations, notes, and images between code sections
- Go back and re-run specific parts without running everything

### Example: Jupyter Notebook Cell
```python
# Cell 1
print("Hello, World!")
```
*[Run this cell, see output]*

```python
# Cell 2
name = "Alice"
print(f"Welcome, {name}!")
```
*[Run this cell separately]*

## Key Differences

| Feature | Python File (`.py`) | Jupyter Notebook (`.ipynb`) |
|---------|---------------------|------------------------------|
| **Execution** | Run entire file at once | Run individual cells one at a time |
| **Output** | Prints to terminal/console | Shows output directly below each cell |
| **Editing** | Edit in any text editor | Edit in Jupyter interface (browser or app) |
| **Best for** | Final programs, scripts, automation | Learning, experimenting, data analysis |
| **Format** | Plain text | JSON format with code, output, and notes |

## Understanding Python Libraries

### What is a Library?

A **library** is a collection of pre-written code that you can use in your programs. Instead of writing everything from scratch, you can use functions and tools that others have created.

Think of it like this:
- **No library**: Building a house by making your own bricks, nails, and tools
- **With library**: Going to a hardware store and buying ready-made materials

### Built-in Libraries (Come with Python)

Python includes many libraries by default. You just need to import them:

```python
import math

result = math.sqrt(25)  # Uses square root function from math library
print(result)  # Output: 5.0
```

**Common built-in libraries:**
- `math` - Mathematical functions
- `random` - Generate random numbers
- `datetime` - Work with dates and times
- `os` - Interact with your operating system

### External Libraries (Install with pip)

**pip** is Python's package installer - a tool that downloads and installs libraries from the internet.

#### How to Install a Library

Open your terminal or command prompt and type:
```bash
pip install pandas
```

For jupyter notebook type in a cell code:
```bash
%pip install pandas
```

This downloads the `pandas` library and installs it on your computer.

#### Using an Installed Library

After installation, you can import and use it just like built-in libraries:

```python
import pandas as pd

# Create sample RNA-seq data
data = {
    'Gene_ID': ['BRCA1', 'TP53', 'EGFR', 'MYC', 'KRAS'],
    'Sample_1_TPM': [45.2, 123.5, 78.9, 234.1, 56.7],
    'Sample_2_TPM': [52.1, 118.3, 82.4, 241.5, 61.2],
    'Chromosome': ['chr17', 'chr17', 'chr7', 'chr8', 'chr12']
}

df = pd.DataFrame(data)

# Filter for genes on chromosome 17
chr17_genes = df[df['Chromosome'] == 'chr17']
print(chr17_genes)
```

**Output:**
```
  Gene_ID  Sample_1_TPM  Sample_2_TPM Chromosome
0   BRCA1          45.2          52.1      chr17
1    TP53         123.5         118.3      chr17
```

```python
import pandas as pd

# Read protein data from UniProt
url = "https://rest.uniprot.org/uniprotkb/stream?format=tsv&query=organism_id:9606+AND+reviewed:true&fields=accession,gene_names,protein_name,length,mass&size=100"
df = pd.read_csv(url, sep='\t')

# Filter for proteins with "kinase" in the name
kinase_data = df[df['Protein names'].str.contains('kinase', case=False, na=False)]
print(kinase_data.head())
```

**Popular external libraries:**
- `requests` - Make web requests easily
- `pandas` - Work with data tables (like Excel)
- `numpy` - Fast math with arrays and matrices
- `matplotlib` - Create charts and graphs

### Creating Your Own Library

You can create your own libraries! Any Python file can be imported as a library.

#### Example: Creating a library

**File: `my_math.py`**
```python
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b
```

**File: `main.py`** (using your library)
```python
import my_math

result = my_math.add(5, 3)
print(result)  # Output: 8
```

When you create a `.py` file with functions, you can import it into other Python files in the same folder!

## When to Use Each

### Use Python Files (`.py`) when:
- Building a complete program or application
- Creating scripts that run automatically
- Writing code that others will use as a library
- Deploying production code

### Use Jupyter Notebooks (`.ipynb`) when:
- Learning Python and experimenting
- Analyzing data and creating visualizations
- Creating tutorials or documentation
- Sharing code with explanations and results

## Virtual Environments

### What is a Virtual Environment?

A **virtual environment** is like a separate, isolated workspace for each Python project. Imagine having different toolboxes for different projects - each one has exactly the tools (libraries) that project needs, without mixing them up.

### Why Do You Need Virtual Environments?

**The Problem Without Virtual Environments:**

Let's say you have two projects:
- **Project A** needs `requests` version 2.25.0
- **Project B** needs `requests` version 2.31.0

If you install both globally on your computer, they'll conflict! You can only have one version installed at a time.

**The Solution With Virtual Environments:**

Each project gets its own isolated environment with its own libraries. Project A's libraries don't affect Project B's libraries.

### Real-World Analogy

Think of virtual environments like separate apartments in a building:
- **Without virtual env**: Everyone shares one apartment (chaos!)
- **With virtual env**: Each project gets its own apartment with its own furniture (libraries)

### How to Create and Use Virtual Environments

#### Step 1: Create a Virtual Environment

In your project folder, run:
```bash
# Windows
python -m venv myenv

# Mac/Linux
python3 -m venv myenv
```

This creates a folder called `myenv` containing the isolated environment.

#### Step 2: Activate the Virtual Environment

**Windows:**
```bash
myenv\Scripts\activate
```

**Mac/Linux:**
```bash
source myenv/bin/activate
```

You'll see `(myenv)` appear in your terminal, showing the environment is active.

#### Step 3: Install Libraries

Now when you install libraries, they only go into this environment:
```bash
pip install requests pandas numpy
```

#### Step 4: Deactivate When Done

```bash
deactivate
```

### The requirements.txt File

When working with virtual environments, you'll often see a `requirements.txt` file. This lists all the libraries your project needs.

#### Creating requirements.txt

After installing your libraries, save the list:
```bash
pip freeze > requirements.txt
```

**Example `requirements.txt`:**
```
requests==2.31.0
pandas==2.1.0
numpy==1.24.3
```

#### Using requirements.txt

When someone else (or you on another computer) wants to run your project:
```bash
# Create and activate virtual environment first, then:
pip install -r requirements.txt
```

This installs all the exact library versions your project needs!

## Other Important Concepts

### The `__name__ == "__main__"` Pattern

You'll often see this in Python files:

```python
def greet(name):
    print(f"Hello, {name}!")

if __name__ == "__main__":
    greet("Alice")
```

**What does this mean?**

- When you **run this file directly**, the code under `if __name__ == "__main__":` executes
- When you **import this file as a library**, that code is skipped

This lets a file work both as a runnable program AND as a library!

### Package vs Module vs Library

Beginners often get confused by these terms:

- **Module**: A single `.py` file (e.g., `my_math.py`)
- **Package**: A folder containing multiple modules with a special `__init__.py` file
- **Library**: A general term for reusable code (can be a module or package)

**Example Package Structure:**
```
my_package/
    __init__.py
    math_tools.py
    string_tools.py
```

Usage:
```python
from my_package import math_tools
from my_package.string_tools import capitalize
```

### The .gitignore File

When sharing code (especially on GitHub), you should **NOT** share:
- Virtual environment folders (`venv/`, `myenv/`)
- Python cache files (`__pycache__/`, `*.pyc`)

Create a `.gitignore` file:
```
# Virtual environments
venv/
myenv/
env/

# Python cache
__pycache__/
*.pyc
*.pyo

# Jupyter checkpoints
.ipynb_checkpoints/
```

**Why?** These files are automatically generated and can be huge. Share your code and `requirements.txt` instead - others can recreate the environment.

### Python Path and Imports

Python needs to find your files when you import them. It looks in:
1. The current folder
2. Folders in the `PYTHONPATH` environment variable
3. Standard library locations

**Common import issues:**
```python
# If Python can't find your module:
ModuleNotFoundError: No module named 'my_module'
```

**Solutions:**
- Make sure the file is in the same folder
- Make sure you activated your virtual environment
- Install the library with pip if it's external

### Scripts vs Programs vs Applications

- **Script**: A simple `.py` file that automates a task (e.g., rename files, download data)
- **Program**: Multiple files working together with more features
- **Application**: A complete program with user interface (GUI or web interface)

All start as Python files, but grow in complexity!

## Quick Tips for Beginners

1. **Start with Jupyter Notebooks** if you're learning - they let you experiment easily
2. **Move to Python files** when you want to build complete programs
3. **Always use virtual environments** for projects - it prevents headaches later
4. **Create requirements.txt** for every project so others can run your code
5. **Install libraries as needed** - don't install everything at once
6. **Read documentation** - every library has guides on how to use it
7. **Use .gitignore** if sharing code online

## Virtual Environment Workflow (Recommended)

Here's the complete workflow for starting a new project:

```bash
# 1. Create project folder
mkdir my_project
cd my_project

# 2. Create virtual environment
python -m venv venv

# 3. Activate it
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows

# 4. Install libraries
pip install requests pandas

# 5. Save requirements
pip freeze > requirements.txt

# 6. Create your Python files
# Write your code here!

# 7. Deactivate when done
deactivate
```

## Summary

- **Python files** are like complete recipes - write once, run all
- **Jupyter Notebooks** are like interactive workbooks - experiment as you go
- **Libraries** are pre-made tools that save you time
- **pip** is how you download and install new libraries
- **Virtual environments** keep each project's libraries separate and organized
- **requirements.txt** shares what libraries your project needs
- **You can create your own libraries** by writing functions in `.py` files
