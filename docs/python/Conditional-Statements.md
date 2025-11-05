---
title: Conditional Statements
description: A detailed guide to understanding conditional statements in Python, explained simply for beginners.
---

# Conditional Statements

This chapter explains how to make decisions in Python programs using conditional statements. These allow your code to choose different actions based on different conditions, making your programs smart and responsive.

## What are Conditional Statements?

Conditional statements are like asking questions in your program. Based on the answer, your program decides what to do next. Think of them as "if this happens, then do this" rules.

## 1. The if Statement

The most basic conditional statement is `if`. It checks a condition and runs code only if that condition is true.

```python
age = 18

if age >= 18:
    print("You are an adult")
```

**How it works:**
- The `if` keyword starts the condition
- `age >= 18` is the condition being checked
- If the condition is `True`, the indented code runs
- If `False`, the code is skipped

## 2. The else Statement

The `else` clause provides an alternative when the `if` condition is `False`.

```python
age = 15

if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

**What happens:**
- If `age >= 18` is True → prints "You are an adult"
- If `age >= 18` is False → executes the `else` block

## 3. The elif Statement

`elif` (short for "else if") allows you to check multiple conditions in sequence.

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

**How it works:**
- Checks conditions in order from top to bottom
- Stops at the first `True` condition
- If none are True, executes the `else` block

## 4. Comparison Operators in Conditions

Conditional statements rely on comparison operators:

- **Equal to `==`**: Checks if two values are the same. Example: `5 == 5` returns True
- **Not equal to `!=`**: Checks if different. Example: `5 != 3` returns True
- **Greater than `>`**: Compares sizes. Example: `10 > 5` returns True
- **Less than `<`**: Compares sizes. Example: `3 < 7` returns True
- **Greater than or equal `>=`**: Includes equality. Example: `5 >= 5` returns True
- **Less than or equal `<=`**: Includes equality. Example: `3 <= 5` returns True

## 5. Logical Operators

Combine multiple conditions:

```python
# Using 'and' - both conditions must be True
if age >= 18 and has_license:
    print("You can drive")

# Using 'or' - at least one condition must be True
if weather == "rain" or weather == "snow":
    print("Stay inside")

# Using 'not' - flips the result
if not is_weekend:
    print("It's a workday")
```

## 6. Indentation and Code Blocks

Python uses indentation (spaces) to define code blocks:

```python
if condition:
    print("This line runs if condition is True")
    print("This also runs if condition is True")
    print("All these lines are indented the same amount")

print("This line always runs - it's not indented")
```

**Important Rules:**
- Use consistent indentation (4 spaces is standard)
- All lines in a block must have the same indentation
- Don't mix tabs and spaces

## 7. Practical Examples

### Example 1: Simple Age Checker
```python
age = int(input("Enter your age: "))

if age < 0:
    print("Invalid age")
elif age < 13:
    print("You are a child")
elif age < 20:
    print("You are a teenager")
elif age < 65:
    print("You are an adult")
else:
    print("You are a senior citizen")
```

### Example 2: Simple Calculator
```python
num1 = float(input("Enter first number: "))
operator = input("Enter operator (+, -, *, /): ")
num2 = float(input("Enter second number: "))

if operator == "+":
    result = num1 + num2
    print(f"{num1} + {num2} = {result}")
elif operator == "-":
    result = num1 - num2
    print(f"{num1} - {num2} = {result}")
elif operator == "*":
    result = num1 * num2
    print(f"{num1} * {num2} = {result}")
elif operator == "/":
    if num2 != 0:
        result = num1 / num2
        print(f"{num1} / {num2} = {result}")
    else:
        print("Cannot divide by zero")
else:
    print("Invalid operator")
```

### Example 3: Password Checker
```python
password = input("Enter your password: ")

if len(password) < 8:
    print("Password too short")
elif len(password) < 12:
    print("Password is okay")
else:
    print("Strong password")

# Check for numbers
if any(char.isdigit() for char in password):
    print("Contains numbers")
else:
    print("Should contain numbers")

# Check for letters
if any(char.isalpha() for char in password):
    print("Contains letters")
else:
    print("Should contain letters")
```

## 8. Common Mistakes to Avoid

### Mistake 1: Using = instead of ==
```python
# Wrong - this assigns instead of compares
if age = 18:  # Syntax error

# Correct - this compares
if age == 18:
```

### Mistake 2: Incorrect Indentation
```python
# Wrong - mixed indentation
if condition:
print("This will cause an IndentationError")

# Correct - consistent indentation
if condition:
    print("This works correctly")
```

### Mistake 3: Forgetting the Colon
```python
# Wrong
if age > 18
    print("Adult")

# Correct
if age > 18:
    print("Adult")
```

## 9. Ternary Conditional Operator

A shorthand way to write simple if-else statements:

```python
# Traditional way
if age >= 18:
    status = "Adult"
else:
    status = "Minor"

# Shorter way
status = "Adult" if age >= 18 else "Minor"
```

## 10. Nested Conditionals

You can put conditionals inside other conditionals:

```python
if age >= 18:
    if has_license:
        print("You can drive")
    else:
        print("You need a license to drive")
else:
    print("You are too young to drive")
```

## Summary

- **if**: Basic decision making
- **elif**: Additional conditions to check
- **else**: Alternative when no conditions are true
- **Comparison operators**: equal to, not equal to, greater than, less than, etc.
- **Logical operators**: and, or, not
- **Indentation**: Use 4 spaces consistently
- **Common mistakes**: equals vs double equals, incorrect indentation, missing colons

Practice by creating programs that make decisions based on user input. This is fundamental to creating intelligent, responsive applications!