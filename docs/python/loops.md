---
id: loops
title: Loops in Python
---

# Loops in Python

Loops are a fundamental concept in programming that allows us to execute a block of code repeatedly.  
Python provides two types of loops: for loop and while loop.

---

## For Loop

The for loop is used to iterate over a sequence (such as a list, tuple, or string) or other iterable objects.

### Syntax
```python
for variable in iterable:
    # code to be executed
```

### Example

```python
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)
```

**Output:**
```
apple
banana
cherry
```

---

### Range Function

The range() function is used to generate a sequence of numbers.

```python
for i in range(5):
    print(i)
```

**Output:**
```
0
1
2
3
4
```

---

### Range Function with Start, Stop, and Step

```python
for i in range(1, 10, 2):
    print(i)
```

**Output:**
```
1
3
5
7
9
```

---

## While Loop

The while loop is used to execute a block of code as long as a certain condition is true.

### Syntax

```python
while condition:
    # code to be executed
```

### Example

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

**Output:**
```
0
1
2
3
4
```

---

## Loop Control Statements

Python provides special statements to control the flow of loops.

---

### Break Statement

The break statement is used to exit the loop.

```python
for i in range(5):
    if i == 3:
        break
    print(i)
```

**Output:**
```
0
1
2
```

---

### Continue Statement

The continue statement is used to skip the current iteration and move to the next iteration.

```python
for i in range(5):
    if i == 3:
        continue
    print(i)
```

**Output:**
```
0
1
2
4
```

---

### Pass Statement

The pass statement is used to do nothing (a placeholder statement).

```python
for i in range(5):
    if i == 3:
        pass
    print(i)
```

**Output:**
```
0
1
2
3
4
```

---

### Nested Loops

We can use loops inside other loops.

```python
for i in range(3):
    for j in range(3):
        print(i, j)
```

**Output:**
```
0 0
0 1
0 2
1 0
1 1
1 2
2 0
2 1
2 2
```

---

## Loop Else Clause

The else clause is executed when the loop finishes normally (without a break statement).

```python
for i in range(5):
    print(i)
else:
    print("Loop finished")
```

**Output:**
```
0
1
2
3
4
Loop finished
```

---

### Note:

The else clause is not executed if the loop is terminated by a break statement.

```python
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("Loop finished")
```

**Output:**
```
0
1
2
```

---

✅ Summary:

- Use for loops to iterate over sequences.
- Use while loops when you need to repeat code while a condition remains true.
- Control loops using break, continue, and pass.
- Use the else clause to execute code after normal loop completion.
