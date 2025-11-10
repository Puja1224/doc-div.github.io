---
id: functions-and-modules
title: Functions and Modules in Python
---

# Functions and Modules in Python

Functions and modules are fundamental concepts in Python that help organize and reuse code effectively.

---

## What is a Function?

A function is a reusable block of code that performs a specific task. Functions help in:
- Avoiding code repetition
- Making code more readable and maintainable
- Breaking complex problems into smaller parts

---

## Function Definition

### Basic Syntax

```python
def function_name(parameters):
    # code block
    return value  # optional
```

### Example

```python
def greet(name):
    return f"Hello, {name}!"

# Using the function
message = greet("Alice")
print(message)  # Output: Hello, Alice!
```

---

## Function Parameters

### Positional Parameters

```python
def add(a, b):
    return a + b

result = add(5, 3)  # result = 8
```

### Default Parameters

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("Bob"))        # Output: Hello, Bob!
print(greet("Alice", "Hi")) # Output: Hi, Alice!
```

### Keyword Parameters

```python
def describe_pet(animal, name):
    return f"I have a {animal} named {name}."

print(describe_pet(animal="dog", name="Buddy"))
print(describe_pet(name="Whiskers", animal="cat"))
```

### *args (Variable Positional Arguments)

```python
def sum_all(*args):
    return sum(args)

print(sum_all(1, 2, 3))        # Output: 6
print(sum_all(10, 20, 30, 40)) # Output: 100
```

### **kwargs (Variable Keyword Arguments)

```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="New York")
```

**Output:**
```
name: Alice
age: 25
city: New York
```

---

## Local vs Global Variables

```python
# Global variable
global_var = "I'm global"

def example_function():
    # Local variable
    local_var = "I'm local"
    print(global_var)  # Can access global variable
    
example_function()
# print(local_var)  # This would cause an error
```

---

## Return Statements

### Single Return Value

```python
def multiply(a, b):
    return a * b

result = multiply(4, 5)  # result = 20
```

### Multiple Return Values (Tuple)

```python
def get_name_age():
    name = "Alice"
    age = 25
    return name, age

person = get_name_age()  # person = ('Alice', 25)
name, age = get_name_age()  # Unpacking
```

### Early Return (Guard Clauses)

```python
def divide(a, b):
    if b == 0:
        return "Error: Division by zero"
    return a / b
```

---

## Lambda Functions

Anonymous functions using the `lambda` keyword:

```python
# Regular function
def square(x):
    return x ** 2

# Lambda function
square_lambda = lambda x: x ** 2

# Using with map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # Output: [1, 4, 9, 16, 25]
```

---

## Recursion

Functions that call themselves:

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```

### Fibonacci Sequence with Recursion

```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

# Print first 10 Fibonacci numbers
for i in range(10):
    print(fibonacci(i), end=" ")
```

**Output:** `0 1 1 2 3 5 8 13 21 34`

---

## Decorators

Functions that modify the behavior of other functions:

```python
def decorator_function(original_function):
    def wrapper_function():
        print("Before the function call")
        result = original_function()
        print("After the function call")
        return result
    return wrapper_function

@decorator_function
def say_hello():
    print("Hello!")

say_hello()
```

**Output:**
```
Before the function call
Hello!
After the function call
```

---

## What is a Module?

A module is a file containing Python definitions and statements. Modules help in:
- Organizing code into separate files
- Reusing code across different programs
- Avoiding name conflicts

---

## Creating and Using Modules

### Creating a Module

Create a file named `my_module.py`:

```python
# my_module.py
def greet(name):
    return f"Hello, {name}!"

def calculate_area(length, width):
    return length * width

PI = 3.14159
```

### Using a Module

```python
# Import the entire module
import my_module

print(my_module.greet("Alice"))           # Output: Hello, Alice!
area = my_module.calculate_area(5, 3)     # area = 15
print(f"PI value: {my_module.PI}")        # Output: PI value: 3.14159
```

### Importing Specific Items

```python
# Import specific functions
from my_module import greet, calculate_area, PI

print(greet("Bob"))      # Output: Hello, Bob!
area = calculate_area(4, 6)
print(f"Area: {area}")   # Output: Area: 24
print(f"PI: {PI}")       # Output: PI: 3.14159
```

### Import with Alias

```python
import my_module as mm
from my_module import greet as say_hello

print(mm.greet("Charlie"))     # Output: Hello, Charlie!
print(say_hello("David"))      # Output: Hello, David!
```

---

## Built-in Modules

Python comes with many built-in modules:

### Math Module

```python
import math

print(math.sqrt(16))     # Output: 4.0
print(math.pi)           # Output: 3.141592653589793
print(math.ceil(4.2))    # Output: 5
print(math.floor(4.8))   # Output: 4
```

### Random Module

```python
import random

print(random.randint(1, 10))       # Random integer between 1 and 10
print(random.choice(['a', 'b', 'c']))  # Random choice from list
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)            # Shuffle the list
print(numbers)
```

### Datetime Module

```python
import datetime

now = datetime.datetime.now()
print(f"Current date and time: {now}")

date = datetime.date(2023, 12, 25)
print(f"Christmas Day: {date}")
```

---

## Creating Packages

A package is a collection of modules in a directory:

```
my_package/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        module3.py
```

### Using Packages

```python
# Import from package
from my_package import module1
from my_package.subpackage import module3
```

---

## Best Practices

### Function Design
- Use descriptive function names
- Keep functions focused on a single task
- Add docstrings to document functions
- Use type hints for better code clarity

```python
def calculate_rectangle_area(length: float, width: float) -> float:
    """
    Calculate the area of a rectangle.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    """
    return length * width
```

### Module Organization
- Group related functions in modules
- Use meaningful module names
- Keep modules focused and not too large
- Use `__all__` to control what gets imported with `from module import *`

```python
# In my_module.py
__all__ = ['greet', 'calculate_area']  # Only these will be imported with *

def greet(name):
    return f"Hello, {name}!"

def calculate_area(length, width):
    return length * width

# This function won't be imported with 'from my_module import *'
def helper_function():
    pass
```

---

## Summary

- **Functions**: Reusable code blocks that perform specific tasks
- **Modules**: Files containing Python definitions that can be imported
- **Parameters**: Input values for functions (positional, keyword, *args, **kwargs)
- **Return**: Functions can return values using the `return` statement
- **Recursion**: Functions calling themselves for repetitive tasks
- **Decorators**: Functions that modify other functions
- **Packages**: Collections of modules in directories
- **Best Practices**: Clear naming, documentation, and organized code structure