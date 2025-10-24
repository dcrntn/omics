# 🔄 Python Recursion — Problem-Solving Challenges

### 1. Folder Size Calculator
You need to calculate the total size of all files in a folder and its subfolders.  
Think about how recursion could help you navigate through nested folders, adding up file sizes as you go deeper into the directory structure.

---

### 2. Family Tree Depth Finder
You're building a family tree application that needs to find how many generations exist.  
Consider how recursion could traverse from parents to children to grandchildren, counting the depth until there are no more descendants.

---

### 3. Nested List Flattener
You have a list that contains numbers and other lists, which may also contain lists inside them.  
Think about how recursion could help you extract all numbers into a single flat list, no matter how deeply nested they are.

---

### 4. Directory Backup System
You want to create a backup of an entire folder structure, preserving all subfolders.  
Consider how recursion could copy each file and recursively handle subfolders, maintaining the same structure in the backup location.

---

### 5. Comment Thread Counter
A social media app has comments with replies, and replies can have their own replies.  
Think about how recursion could count all comments in a thread, including nested replies at any depth.

---

### 6. File Extension Finder
You need to find all files with a specific extension (like .txt or .jpg) in a project and all its subfolders.  
Consider how recursion could search through each folder and its subfolders, collecting matching files along the way.

---

### 7. Palindrome Checker
Check if a word or phrase reads the same forwards and backwards.  
Think about how recursion could compare the first and last characters, then recursively check the middle part until there's nothing left to compare.

---

### 8. Sum of Digits
Calculate the sum of all digits in a number (e.g., 1234 → 1+2+3+4 = 10).  
Consider how recursion could extract the last digit, add it to the sum of the remaining digits, until no digits are left.

---

### 9. Maze Path Finder
You have a maze represented as nested folders, and you need to find if a path exists to a goal.  
Think about how recursion could try each direction, backing up when hitting dead ends, until finding the exit or exhausting all possibilities.

---

### 10. Binary Search Implementation
Search for a number in a sorted list by repeatedly dividing the search space in half.  
Consider how recursion could check the middle element, then recursively search either the left or right half based on comparison.

---

### 11. Power Calculator
Calculate x raised to the power of n (x^n) without using the ** operator.  
Think about how recursion could multiply x by itself n times, with each recursive call reducing the power by 1.

---

### 12. Nested JSON Parser
You need to search for a specific key in a JSON-like nested dictionary structure.  
Consider how recursion could check each level, diving deeper into nested dictionaries until finding the key or reaching the end.

---

### 13. Greatest Common Divisor (GCD)
Find the largest number that divides two numbers without remainder using Euclid's algorithm.  
Think about how recursion could repeatedly replace the larger number with the remainder until one number becomes zero.

---

### 14. Tower of Hanoi
Move disks from one peg to another, following the rule that a larger disk can never be on top of a smaller one.  
Consider how recursion could break this into: move n-1 disks to spare peg, move largest disk to target, then move n-1 disks to target.

---

### 15. String Permutations Generator
Generate all possible arrangements of characters in a string.  
Think about how recursion could fix one character and recursively permute the rest, repeating for each character in different positions.