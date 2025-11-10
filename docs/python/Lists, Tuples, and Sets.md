---
id: lists-tuples-and-sets
title: Lists, Tuples, and Sets in Python
---

# Lists, Tuples, and Sets in Python

Python provides several built-in data structures for storing collections of items. Lists, tuples, and sets are three fundamental collection types, each with unique characteristics and use cases.

---

## Lists

Lists are ordered, mutable collections that can contain elements of different data types. They are one of the most commonly used data structures in Python.

### Creating Lists

```python
# Empty list
empty_list = []

# List with elements
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]

# Mixed data types
mixed = [1, "hello", 3.14, True]

# Using list() constructor
list_from_string = list("hello")  # ['h', 'e', 'l', 'l', 'o']
list_from_range = list(range(5))  # [0, 1, 2, 3, 4]
```

### Accessing List Elements

```python
fruits = ["apple", "banana", "cherry", "orange"]

# Indexing
print(fruits[0])     # Output: apple
print(fruits[-1])    # Output: orange (last element)

# Slicing
print(fruits[1:3])   # Output: ['banana', 'cherry']
print(fruits[:2])    # Output: ['apple', 'banana']
print(fruits[2:])    # Output: ['cherry', 'orange']
print(fruits[::2])   # Output: ['apple', 'cherry'] (step of 2)
print(fruits[::-1])  # Output: ['orange', 'cherry', 'banana', 'apple'] (reverse)
```

### List Operations

```python
# Concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2  # [1, 2, 3, 4, 5, 6]

# Repetition
repeated = [1, 2] * 3  # [1, 2, 1, 2, 1, 2]

# Length
print(len(combined))  # Output: 6

# Membership testing
print(3 in list1)     # Output: True
print(7 in list1)     # Output: False
```

### Modifying Lists

```python
fruits = ["apple", "banana", "cherry"]

# Adding elements
fruits.append("orange")       # Add to end: ["apple", "banana", "cherry", "orange"]
fruits.insert(1, "mango")    # Insert at index: ["apple", "mango", "banana", "cherry"]
fruits.extend(["grape", "kiwi"])  # Add multiple: ["apple", "mango", "banana", "cherry", "grape", "kiwi"]

# Removing elements
fruits.remove("mango")       # Remove by value
fruits.pop()                 # Remove and return last element
fruits.pop(0)                # Remove and return element at index
del fruits[0]                # Delete element at index
fruits.clear()               # Remove all elements
```

### List Methods

```python
numbers = [3, 1, 4, 1, 5, 9, 2]

# Counting occurrences
print(numbers.count(1))      # Output: 2

# Finding index
print(numbers.index(4))      # Output: 2

# Sorting
numbers.sort()               # [1, 1, 2, 3, 4, 5, 9]
numbers.sort(reverse=True)   # [9, 5, 4, 3, 2, 1, 1]

# Reversing
numbers.reverse()            # [2, 9, 5, 4, 1, 3, 1]

# Copying
new_numbers = numbers.copy()  # Creates a shallow copy
```

### List Comprehension

```python
# Basic list comprehension
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With condition
even_squares = [x**2 for x in range(10) if x % 2 == 0]
# [0, 4, 16, 36, 64]

# Nested loops
coordinates = [(x, y) for x in range(3) for y in range(3)]
# [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]

# Complex example
words = ["hello", "world", "python", "programming"]
uppercase_long = [word.upper() for word in words if len(word) > 5]
# ['PYTHON', 'PROGRAMMING']
```

---

## Tuples

Tuples are ordered, immutable collections. They are similar to lists but cannot be modified after creation, making them useful for data that shouldn't change.

### Creating Tuples

```python
# Empty tuple
empty_tuple = ()

# Single element tuple (note the comma)
single_element = (42,)
multiple_elements = (1, 2, 3, 4, 5)

# Without parentheses (comma-separated values)
tuple_without_parens = 1, 2, 3, 4, 5

# Mixed data types
mixed_tuple = (1, "hello", 3.14, True)

# Using tuple() constructor
tuple_from_list = tuple([1, 2, 3, 4, 5])
tuple_from_string = tuple("hello")  # ('h', 'e', 'l', 'l', 'o')
tuple_from_range = tuple(range(3))  # (0, 1, 2)
```

### Accessing Tuple Elements

```python
coordinates = (10, 20, 30)

# Indexing
print(coordinates[0])     # Output: 10
print(coordinates[-1])    # Output: 30

# Slicing (returns a new tuple)
print(coordinates[1:])    # Output: (20, 30)
print(coordinates[:2])    # Output: (10, 20)
print(coordinates[::-1])  # Output: (30, 20, 10)
```

### Tuple Operations

```python
# Concatenation
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)
combined = tuple1 + tuple2  # (1, 2, 3, 4, 5, 6)

# Repetition
repeated = (1, 2) * 3  # (1, 2, 1, 2, 1, 2)

# Length
print(len(combined))  # Output: 6

# Membership testing
print(3 in tuple1)    # Output: True
print(7 in tuple1)    # Output: False

# Count occurrences
numbers = (1, 2, 3, 1, 4, 1, 5)
print(numbers.count(1))  # Output: 3

# Find index
print(numbers.index(3))  # Output: 2
```

### Tuple Unpacking

```python
# Basic unpacking
x, y, z = (1, 2, 3)
print(f"x={x}, y={y}, z={z}")  # Output: x=1, y=2, z=3

# Unpacking with extended syntax
first, *middle, last = (1, 2, 3, 4, 5)
print(f"first={first}, middle={middle}, last={last}")
# Output: first=1, middle=[2, 3, 4], last=5

# Swapping variables
a, b = 1, 2
a, b = b, a
print(f"a={a}, b={b}")  # Output: a=2, b=1

# Function return values
def get_name_age():
    return "Alice", 25

name, age = get_name_age()
print(f"Name: {name}, Age: {age}")  # Output: Name: Alice, Age: 25
```

### Named Tuples

```python
from collections import namedtuple

# Define a named tuple
Person = namedtuple('Person', ['name', 'age', 'city'])

# Create instances
person1 = Person('Alice', 25, 'New York')
person2 = Person('Bob', 30, 'London')

# Access fields
print(person1.name)    # Output: Alice
print(person2.age)     # Output: 30

# Convert to dictionary
person_dict = person1._asdict()
print(person_dict)     # Output: {'name': 'Alice', 'age': 25, 'city': 'New York'}

# Create new instance with some fields changed
person3 = person1._replace(age=26)
print(person3)         # Output: Person(name='Alice', age=26, city='New York')
```

---

## Sets

Sets are unordered collections of unique elements. They don't allow duplicates and provide mathematical set operations.

### Creating Sets

```python
# Empty set (note: {} creates an empty dictionary, not a set)
empty_set = set()

# Set with elements
fruits = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 4, 5}

# Sets automatically remove duplicates
duplicates = {1, 2, 2, 3, 3, 3, 4, 4, 4, 4, 5}
print(duplicates)      # Output: {1, 2, 3, 4, 5}

# Using set() constructor
set_from_list = set([1, 2, 3, 4, 5])
set_from_string = set("hello")  # {'h', 'e', 'l', 'o'}
set_from_range = set(range(5))  # {0, 1, 2, 3, 4}

# Set comprehension
squares = {x**2 for x in range(5)}  # {0, 1, 4, 9, 16}
```

### Set Operations

```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

# Union (all elements from both sets)
union = set1 | set2
union = set1.union(set2)
print(union)           # Output: {1, 2, 3, 4, 5, 6, 7, 8}

# Intersection (elements in both sets)
intersection = set1 & set2
intersection = set1.intersection(set2)
print(intersection)    # Output: {4, 5}

# Difference (elements in first set but not in second)
difference = set1 - set2
difference = set1.difference(set2)
print(difference)      # Output: {1, 2, 3}

# Symmetric difference (elements in either set but not both)
sym_diff = set1 ^ set2
sym_diff = set1.symmetric_difference(set2)
print(sym_diff)        # Output: {1, 2, 3, 6, 7, 8}
```

### Set Methods

```python
numbers = {1, 2, 3, 4, 5}

# Adding elements
numbers.add(6)         # {1, 2, 3, 4, 5, 6}
numbers.update([7, 8]) # {1, 2, 3, 4, 5, 6, 7, 8}

# Removing elements
numbers.remove(1)      # Raises KeyError if element not found
numbers.discard(2)     # Doesn't raise error if element not found
popped = numbers.pop() # Remove and return an arbitrary element

# Membership testing
print(3 in numbers)    # Output: True
print(10 in numbers)   # Output: False

# Set comparisons
set_a = {1, 2, 3}
set_b = {1, 2}
set_c = {4, 5}

print(set_a.issuperset(set_b))  # Output: True
print(set_b.issubset(set_a))    # Output: True
print(set_a.isdisjoint(set_c))  # Output: True (no common elements)
```

### Advanced Set Operations

```python
# Finding unique elements
def find_unique_elements(list1, list2):
    return set(list1) ^ set(list2)

# Removing duplicates while preserving order
def remove_duplicates_preserve_order(sequence):
    seen = set()
    result = []
    for item in sequence:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return result

# Set operations with comprehensions
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
even_squares = {x**2 for x in numbers if x % 2 == 0}
# {4, 16, 36, 64, 100}
```

---

## Comparing Lists, Tuples, and Sets

### Key Differences

| Feature | List | Tuple | Set |
|---------|------|-------|-----|
| **Mutability** | Mutable (can be changed) | Immutable (cannot be changed) | Mutable (can be changed) |
| **Order** | Ordered (indexed) | Ordered (indexed) | Unordered |
| **Duplicates** | Allowed | Allowed | Not allowed |
| **Syntax** | `[1, 2, 3]` | `(1, 2, 3)` or `1, 2, 3` | `{1, 2, 3}` |
| **Methods** | `append()`, `extend()`, `sort()`, etc. | `count()`, `index()` | `add()`, `union()`, `intersection()`, etc. |
| **Use Cases** | Collections that need modification | Fixed collections, function returns | Unique collections, mathematical operations |
| **Performance** | Slower for membership testing | Slower for membership testing | Fast membership testing |

### When to Use Each

```python
# Use Lists when:
# - You need an ordered collection
# - You need to modify the collection
# - You need to allow duplicates
# - You need to access elements by index

shopping_list = ["milk", "bread", "eggs", "milk"]  # Duplicates allowed, mutable

# Use Tuples when:
# - You have fixed data that shouldn't change
# - You want to ensure data integrity
# - You need to use as dictionary keys
# - You want memory efficiency

coordinates = (10.5, 20.3)  # Fixed data, can be dictionary key
user_info = ("Alice", 25, "alice@example.com")  # Fixed user data

# Use Sets when:
# - You need unique elements
# - You need fast membership testing
# - You need mathematical set operations
# - Order doesn't matter

unique_ids = {101, 102, 103, 104}  # Unique values, fast lookups
```

---

## Common Patterns and Best Practices

### Working with Nested Collections

```python
# List of tuples (common pattern)
students = [("Alice", 95), ("Bob", 87), ("Charlie", 92)]

# Sort by second element
students_sorted = sorted(students, key=lambda x: x[1])
# [('Bob', 87), ('Charlie', 92), ('Alice', 95)]

# Tuple of lists
matrix = ([1, 2, 3], [4, 5, 6], [7, 8, 9])

# Dictionary with list values and tuple keys
gradebook = {
    ("Alice", "Math"): 95,
    ("Alice", "Science"): 87,
    ("Bob", "Math"): 92
}
```

### Functional Programming with Collections

```python
# Using map(), filter(), and reduce() with lists
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Map (transform each element)
squared = list(map(lambda x: x**2, numbers))
# [1, 4, 9, 16, 25]

# Filter (keep elements that meet condition)
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
# [2, 4]

# Reduce (combine all elements into single value)
product = reduce(lambda x, y: x * y, numbers)
# 120
```

### Performance Considerations

```python
# Lists: Good for random access, slower for membership testing
# Use 'in' operator for membership: O(n) time complexity

# Sets: Excellent for membership testing, good for uniqueness
# Use 'in' operator for membership: O(1) average time complexity

# Tuples: Similar to lists but immutable and more memory efficient
# Use when data shouldn't change

# Example: Finding unique elements vs. list conversion
def unique_elements_performance(items):
    # Method 1: Using set (efficient)
    unique_set = set(items)
    return unique_set
    
    # Method 2: Using list comprehension (less efficient for large datasets)
    unique_list = []
    for item in items:
        if item not in unique_list:
            unique_list.append(item)
    return unique_list
```

### Memory and Performance Tips

```python
# 1. Choose the right data structure for the task
# 2. Use set() for membership testing when you have many elements
# 3. Use tuples for data that won't change (more memory efficient)
# 4. Use list comprehensions instead of loops when possible (faster)
# 5. Be careful with nested structures (memory usage)

# Example: Efficient string processing
import string

# Bad: Creating intermediate lists
text = "Hello, World!"
words_bad = [word.strip(string.punctuation) for word in text.lower().split()]
words_bad = list(set(words_bad))  # Unnecessary conversion to list

# Good: Direct set creation
words_good = {word.strip(string.punctuation) for word in text.lower().split()}
```

---

## Summary

- **Lists**: Ordered, mutable collections with indexing and many methods
- **Tuples**: Ordered, immutable collections useful for fixed data
- **Sets**: Unordered collections of unique elements with fast operations
- **Choose based on needs**: Mutability, uniqueness, order, and performance
- **Advanced patterns**: List comprehensions, set operations, and functional programming
- **Best practices**: Select the right structure for the specific use case

Each collection type has its strengths, and understanding when to use each will make your Python code more efficient and readable.