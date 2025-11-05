---
title: Python Basics — Variables, Data Types, and Input/Output
description: A detailed guide to understanding variables, data types, and input/output in Python, explained simply for beginners.
---

# Python Basics: Variables, Data Types, and Input/Output

This chapter covers the fundamentals of Python programming. We'll break it down into three main parts: variables, data types, and input/output. Everything is explained in simple, easy-to-understand language with examples. Think of Python as a friendly tool that lets you store, manipulate, and display information.

## 1. Variables
Variables are like labeled boxes where you store data. You can put something in the box, change it, or use it later. In Python, you don't need to declare the type upfront—it's flexible!

- **How to Create a Variable**: Use a name (like `age` or `name`) followed by `=` and the value.  
  Example: `age = 25` (stores the number 25 in `age`).

- **Rules for Names**: 
  - Start with a letter or underscore (_), not a number.
  - No spaces; use underscores for multi-word names (e.g., `my_age`).
  - Case-sensitive: `Age` and `age` are different.
  - Avoid Python keywords like `if`, `for`.

- **Changing Values**: You can update a variable anytime.  
  Example: `age = 25` then `age = 30` (now `age` is 30).

- **Why Use Them?**: Variables make code reusable. Instead of repeating values, store them once and reference the variable.

- **Quick Tip**: Print a variable with `print(age)` to see its value.

## 2. Data Types
Data types tell Python what kind of information you're working with. Python automatically figures it out, but knowing types helps you use data correctly. There are built-in types like numbers, text, and lists.

- **Integers (int)**: Whole numbers, positive or negative.  
  Example: `score = 100` (no decimals).

- **Floats (float)**: Numbers with decimals.  
  Example: `price = 19.99`.

- **Strings (str)**: Text, enclosed in quotes.  
  Example: `name = "Alice"` or `message = 'Hello!'`.  
  - You can combine strings: `"Hi" + " there"` becomes `"Hi there"`.

- **Booleans (bool)**: True or False values, used for decisions.  
  Example: `is_student = True`.

- **Lists**: Collections of items in square brackets. Can hold mixed types.  
  Example: `fruits = ["apple", "banana", 5]` (a list with strings and a number).

- **Other Types**: Tuples (like lists but unchangeable: `(1, 2, 3)`), dictionaries (key-value pairs: `{"name": "Bob", "age": 25}`).

- **Checking Type**: Use `type(variable)` to see what it is.  
  Example: `type(score)` returns `<class 'int'>`.

- **Converting Types**: Change one type to another.  
  Example: `str(25)` turns 25 into "25"; `int("10")` turns "10" into 10.

- **Why It Matters**: Operations depend on types (e.g., you can't add a string to a number directly without converting).

## 3. Input/Output
Input lets your program get data from users; output shows results. This makes programs interactive.

- **Output (Printing)**: Use `print()` to display things on the screen.  
  Example: `print("Hello, World!")` outputs "Hello, World!".  
  - Print variables: `print(name)` shows the value of `name`.  
  - Multiple items: `print("Your age is", age)` (adds a space automatically).

- **Input (Getting User Data)**: Use `input()` to ask for user input. It always returns a string.  
  Example: `name = input("Enter your name: ")` (prompts user, stores response in `name`).  
  - Convert if needed: `age = int(input("Enter age: "))` (turns string into number).

- **Combining Them**: Input something, process it, and output the result.  
  Example:  
  ```python
  name = input("What's your name? ")
  print("Nice to meet you,", name + "!")