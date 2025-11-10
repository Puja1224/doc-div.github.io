---
id: operators-and-expressions
title: Operators and Expressions in Python
---

# Operators and Expressions in Python

Operators are special symbols that carry out operations on operands (variables or values). An expression is a combination of operators and operands that computes to a value.

---

## Arithmetic Operators

Arithmetic operators are used to perform mathematical operations.

### Addition (+)
```python
a = 10 + 5  # 15
print(a)
```

### Subtraction (-)
```python
a = 10 - 5  # 5
print(a)
```

### Multiplication (*)
```python
a = 10 * 5  # 50
print(a)
```

### Division (/)
```python
a = 10 / 5  # 2.0
print(a)
```

### Floor Division (//)
```python
a = 10 // 3  # 3 (returns integer)
print(a)
```

### Modulus (%)
```python
a = 10 % 3  # 1 (remainder)
print(a)
```

### Exponentiation (**)
```python
a = 2 ** 3  # 8 (2 to the power of 3)
print(a)
```

---

## Comparison Operators

Comparison operators compare values and return True or False.

### Equal to (==)
```python
a = 5
b = 5
result = a == b  # True
print(result)
```

### Not equal to (!=)
```python
a = 5
b = 3
result = a != b  # True
print(result)
```

### Greater than (&gt;)
```python
a = 5
b = 3
result = a > b  # True
print(result)
```

### Less than (&lt;)
```python
a = 5
b = 3
result = a < b  # False
print(result)
```

### Greater than or equal to (&gt;=)
```python
a = 5
b = 5
result = a >= b  # True
print(result)
```

### Less than or equal to (&lt;=)
```python
a = 5
b = 3
result = a <= b  # False
print(result)
```

---

## Logical Operators

Logical operators are used to combine conditional statements.

### and
```python
a = True
b = False
result = a and b  # False
print(result)
```

### or
```python
a = True
b = False
result = a or b  # True
print(result)
```

### not
```python
a = True
result = not a  # False
print(result)
```

---

## Assignment Operators

Assignment operators are used to assign values to variables.

### =
```python
a = 5
print(a)
```

### +=
```python
a = 5
a += 3  # Same as: a = a + 3
print(a)  # 8
```

### -=
```python
a = 5
a -= 3  # Same as: a = a - 3
print(a)  # 2
```

### *=
```python
a = 5
a *= 3  # Same as: a = a * 3
print(a)  # 15
```

### /=
```python
a = 15
a /= 3  # Same as: a = a / 3
print(a)  # 5.0
```

### //=
```python
a = 10
a //= 3  # Same as: a = a // 3
print(a)  # 3
```

### %=
```python
a = 10
a %= 3  # Same as: a = a % 3
print(a)  # 1
```

### **=
```python
a = 2
a **= 3  # Same as: a = a ** 3
print(a)  # 8
```

---

## Identity Operators

Identity operators compare the memory locations of two objects.

### is
```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x
result1 = x is z  # True (same object)
result2 = x is y  # False (different objects with same content)
print(result1, result2)
```

### is not
```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x
result1 = x is not z  # False (same object)
result2 = x is not y  # True (different objects with same content)
print(result1, result2)
```

---

## Membership Operators

Membership operators test if a sequence is present in an object.

### in
```python
fruits = ["apple", "banana", "cherry"]
result = "banana" in fruits  # True
print(result)
```

### not in
```python
fruits = ["apple", "banana", "cherry"]
result = "orange" not in fruits  # True
print(result)
```

---

## Bitwise Operators

Bitwise operators work on bits and perform bit-by-bit operations.

### &amp; (AND)
```python
a = 12  # 1100 in binary
b = 10  # 1010 in binary
result = a & b  # 8 (1000 in binary)
print(result)
```

### &vert; (OR)
```python
a = 12  # 1100 in binary
b = 10  # 1010 in binary
result = a | b  # 14 (1110 in binary)
print(result)
```

### &circ; (XOR)
```python
a = 12  # 1100 in binary
b = 10  # 1010 in binary
result = a ^ b  # 6 (0110 in binary)
print(result)
```

### &tilde; (NOT)
```python
a = 12  # 1100 in binary
result = ~a  # -13 (two's complement)
print(result)
```

### &lt;&lt; (Left Shift)
```python
a = 12  # 1100 in binary
result = a << 2  # 48 (110000 in binary)
print(result)
```

### &gt;&gt; (Right Shift)
```python
a = 12  # 1100 in binary
result = a >> 2  # 3 (11 in binary)
print(result)
```

---

## Operator Precedence

Operator precedence determines the order in which operators are evaluated.

### Highest to Lowest Precedence:
1. `()` - Parentheses
2. `**` - Exponentiation
3. `+x`, `-x`, `~x` - Unary plus, unary minus, bitwise NOT
4. `*`, `/`, `//`, `%` - Multiplication, division, floor division, modulus
5. `+`, `-` - Addition, subtraction
6. `<<`, `>>` - Bitwise left shift, bitwise right shift
7. `&` - Bitwise AND
8. `^` - Bitwise XOR
9. `|` - Bitwise OR
10. `==`, `!=`, `>`, `>=`, `<`, `<=` - Comparison operators
11. `is`, `is not` - Identity operators
12. `in`, `not in` - Membership operators
13. `not` - Logical NOT
14. `and` - Logical AND
15. `or` - Logical OR

### Example of Precedence
```python
result = 10 + 5 * 2  # 20 (not 30)
print(result)

# With parentheses
result = (10 + 5) * 2  # 30
print(result)
```

---

## Complex Expressions

### Combining Multiple Operators
```python
# Complex logical expression
age = 25
is_student = True
has_discount = False

eligible = (age >= 18 and age <= 65) and (is_student or has_discount)
print(eligible)
```

### Ternary Operator
```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

### Chained Comparisons
```python
# Multiple comparisons
result = 10 < x < 20
print(result)
```

---

## Practical Examples

### Simple Calculator
```python
def calculator():
    num1 = float(input("Enter first number: "))
    operator = input("Enter operator (+, -, *, /): ")
    num2 = float(input("Enter second number: "))
    
    if operator == '+':
        result = num1 + num2
    elif operator == '-':
        result = num1 - num2
    elif operator == '*':
        result = num1 * num2
    elif operator == '/':
        result = num1 / num2
    else:
        result = "Invalid operator"
    
    print(f"Result: {result}")

calculator()
```

### Check Even or Odd
```python
number = int(input("Enter a number: "))

if number % 2 == 0:
    print(f"{number} is even")
else:
    print(f"{number} is odd")
```

### Age Group Classification
```python
age = int(input("Enter your age: "))

if age < 13:
    category = "Child"
elif age < 20:
    category = "Teenager"
elif age < 65:
    category = "Adult"
else:
    category = "Senior"

print(f"You are a {category}")
```

---

## Best Practices

1. **Use parentheses for clarity**: Even when not required, parentheses make expressions easier to understand.

2. **Choose meaningful variable names**: This makes expressions more readable.

3. **Avoid complex nested expressions**: Break down complex expressions into simpler parts.

4. **Use comparison operators appropriately**: Be careful with `=` (assignment) and `==` (comparison).

5. **Consider operator precedence**: Use parentheses to make the intended order clear.

---

✅ **Summary:**

- Python provides various types of operators: arithmetic, comparison, logical, assignment, identity, membership, and bitwise
- Operator precedence determines evaluation order
- Expressions combine operators and operands to compute values
- Use parentheses to control evaluation order and improve readability
- Different operators work with different data types (numbers, strings, booleans, etc.)