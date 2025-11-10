---
id: dictionaries-in-python
title: Dictionaries in Python
---

# Dictionaries in Python

Dictionaries are one of the most powerful and frequently used data structures in Python. They store data in key-value pairs, providing fast lookups and flexible data organization.

---

## What is a Dictionary?

A dictionary is an unordered collection of key-value pairs. Each key must be unique and hashable (typically strings, numbers, or tuples), while values can be of any data type.

### Key Characteristics:
- **Unordered**: No guaranteed order of elements (Python 3.7+ maintains insertion order)
- **Mutable**: Can be modified after creation
- **Keys must be unique**: Duplicate keys will overwrite previous values
- **Keys must be hashable**: Cannot use lists, sets, or dictionaries as keys
- **Values can be any type**: Including other dictionaries, lists, functions, etc.

---

## Creating Dictionaries

### Basic Creation

```python
# Empty dictionary
empty_dict = {}

# Dictionary with key-value pairs
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Using the dict() constructor
person2 = dict(name="Bob", age=30, city="London")

# From a list of tuples
items = [("apple", 1.5), ("banana", 0.8), ("orange", 2.0)]
prices = dict(items)

# Using zip() function
keys = ["name", "age", "city"]
values = ["Charlie", 28, "Paris"]
person3 = dict(zip(keys, values))

# Dictionary with mixed value types
mixed_dict = {
    "name": "Alice",
    "age": 25,
    "scores": [85, 90, 78],
    "active": True,
    "balance": 1500.50
}
```

### Using fromkeys() Method

```python
# Create dictionary with default values
default_dict = dict.fromkeys(["name", "age", "city"], "Unknown")
# {'name': 'Unknown', 'age': 'Unknown', 'city': 'Unknown'}

# Create dictionary with list values
list_dict = dict.fromkeys(["item1", "item2", "item3"], [])
list_dict["item1"].append("value")
print(list_dict)  # All lists will have the same reference!
```

---

## Accessing Dictionary Elements

### Basic Access

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Using keys
print(person["name"])      # Output: Alice
print(person.get("name"))  # Output: Alice

# Accessing non-existent keys
# person["email"]      # Raises KeyError
print(person.get("email"))        # Returns None
print(person.get("email", "N/A")) # Returns "N/A" as default
```

### Getting All Keys, Values, and Items

```python
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# Get all keys
print(person.keys())        # dict_keys(['name', 'age', 'city'])

# Get all values
print(person.values())      # dict_values(['Alice', 25, 'New York'])

# Get all items (key-value pairs)
print(person.items())       # dict_items([('name', 'Alice'), ('age', 25), ('city', 'New York')])

# Convert to list
keys_list = list(person.keys())
values_list = list(person.values())
items_list = list(person.items())
```

### Conditional Access

```python
def get_user_info(user_dict, key, default=None):
    """Safely get value with default"""
    return user_dict.get(key, default)

# Usage
user = {"name": "Bob", "age": 30}
email = get_user_info(user, "email", "No email provided")
print(email)  # Output: No email provided
```

---

## Modifying Dictionaries

### Adding and Updating Elements

```python
person = {"name": "Alice", "age": 25}

# Add new key-value pair
person["city"] = "New York"
person["email"] = "alice@example.com"

# Update multiple values
person.update({
    "age": 26,
    "phone": "123-456-7890"
})

# Add or update using setdefault()
person.setdefault("country", "USA")  # Adds if key doesn't exist
person.setdefault("age", 30)         # Doesn't change existing value

# Add using |= operator (Python 3.9+)
person |= {"status": "active", "level": 2}
```

### Removing Elements

```python
person = {"name": "Alice", "age": 25, "city": "New York", "email": "alice@example.com"}

# Remove and return value
email = person.pop("email")           # Returns "alice@example.com", removes the key

# Remove arbitrary item
item = person.popitem()               # Removes last added item (Python 3.7+)

# Remove specific key (raises KeyError if not found)
del person["city"]

# Remove all items
person.clear()
```

### Copying Dictionaries

```python
original = {"name": "Alice", "age": 25}

# Shallow copy
copy1 = original.copy()
copy2 = dict(original)

# Deep copy for nested dictionaries
import copy
original_nested = {"user": {"name": "Alice", "settings": {"theme": "dark"}}}
deep_copy = copy.deepcopy(original_nested)
```

---

## Dictionary Methods

### Essential Methods

```python
person = {"name": "Alice", "age": 25, "city": "New York"}

# get() - Safe access with default
name = person.get("name", "Unknown")
email = person.get("email", "No email")

# pop() - Remove and return value
age = person.pop("age", 0)

# popitem() - Remove and return arbitrary item
item = person.popitem()

# setdefault() - Get value or set default
country = person.setdefault("country", "USA")

# update() - Update with another dictionary
person.update({"age": 26, "phone": "123-456-7890"})
```

### Advanced Methods

```python
# Check if key exists
if "name" in person:
    print("Name found")

# Get all keys, values, items
keys = person.keys()
values = person.values()
items = person.items()

# Dictionary length
length = len(person)

# Create from keys
from collections import defaultdict

# defaultdict - automatically creates missing keys
scores = defaultdict(int)
scores["math"] += 10  # Creates "math": 0, then adds 10

# OrderedDict - maintains insertion order (Python 3.7+ maintains order by default)
from collections import OrderedDict
ordered = OrderedDict([("first", 1), ("second", 2), ("third", 3)])
```

---

## Dictionary Comprehensions

### Basic Dictionary Comprehension

```python
# Create dictionary from iterable
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# Create dictionary from two lists
keys = ["a", "b", "c", "d"]
values = [1, 2, 3, 4]
combined = {k: v for k, v in zip(keys, values)}
# {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

### Conditional Dictionary Comprehension

```python
# With condition
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# Filter existing dictionary
scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "Diana": 95}
high_scores = {name: score for name, score in scores.items() if score >= 90}
# {'Bob': 92, 'Diana': 95}

# Transform values
uppercase_names = {name.upper(): score for name, score in scores.items()}
# {'ALICE': 85, 'BOB': 92, 'CHARLIE': 78, 'DIANA': 95}
```

### Nested Dictionary Comprehensions

```python
# Create nested dictionary
matrix = {i: {j: i*j for j in range(1, 4)} for i in range(1, 4)}
# {1: {1: 1, 2: 2, 3: 3}, 2: {1: 2, 2: 4, 3: 6}, 3: {1: 3, 2: 6, 3: 9}}
```

---

## Nested Dictionaries

### Creating and Accessing Nested Dictionaries

```python
# Create nested dictionary
student = {
    "personal": {
        "name": "Alice",
        "age": 20,
        "id": "S12345"
    },
    "academic": {
        "major": "Computer Science",
        "year": "Sophomore",
        "gpa": 3.8
    },
    "contact": {
        "email": "alice@university.edu",
        "phone": "123-456-7890"
    }
}

# Access nested values
name = student["personal"]["name"]
gpa = student["academic"]["gpa"]

# Safe access to nested values
def safe_get_nested(dict_obj, *keys, default=None):
    """Safely access nested dictionary values"""
    for key in keys:
        if isinstance(dict_obj, dict) and key in dict_obj:
            dict_obj = dict_obj[key]
        else:
            return default
    return dict_obj

# Usage
name = safe_get_nested(student, "personal", "name")
emergency_contact = safe_get_nested(student, "personal", "emergency_contact", default="Not provided")
```

### Working with Nested Structures

```python
# Update nested dictionary
student["academic"]["gpa"] = 3.9

# Add new nested value
student["extracurricular"] = {"sports": ["tennis", "swimming"], "clubs": ["programming", "chess"]}

# Remove from nested dictionary
del student["contact"]["phone"]

# Merge dictionaries
def merge_dicts(*dicts):
    """Merge multiple dictionaries"""
    result = {}
    for d in dicts:
        if isinstance(d, dict):
            result.update(d)
    return result

# Usage
details = {"country": "USA", "state": "California"}
student.update(merge_dicts(student["personal"], details))
```

---

## Dictionary Operations and Patterns

### Merging Dictionaries

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

# Python 3.9+ merge operator
merged = dict1 | dict2  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Update method
dict1_copy = dict1.copy()
dict1_copy.update(dict2)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Dictionary unpacking
merged2 = {**dict1, **dict2}
```

### Dictionary Iteration

```python
person = {"name": "Alice", "age": 25, "city": "New York"}

# Iterate over keys
for key in person:
    print(f"Key: {key}")

# Iterate over values
for value in person.values():
    print(f"Value: {value}")

# Iterate over items
for key, value in person.items():
    print(f"{key}: {value}")
```

### Dictionary Grouping

```python
# Group items by category
items = [("fruit", "apple"), ("fruit", "banana"), ("vegetable", "carrot"), ("fruit", "orange")]

# Group by first element
grouped = {}
for category, item in items:
    if category not in grouped:
        grouped[category] = []
    grouped[category].append(item)

# Using defaultdict for cleaner code
from collections import defaultdict
grouped_dd = defaultdict(list)
for category, item in items:
    grouped_dd[category].append(item)
```

### Dictionary to/from Other Types

```python
# Dictionary to JSON
import json
person = {"name": "Alice", "age": 25, "city": "New York"}
json_string = json.dumps(person)
print(json_string)  # {"name": "Alice", "age": 25, "city": "New York"}

# JSON to dictionary
parsed = json.loads(json_string)

# Dictionary to string representation
string_repr = str(person)
print(string_repr)

# List to dictionary
keys = ["name", "age", "city"]
values = ["Bob", 30, "London"]
person_dict = dict(zip(keys, values))
```

---

## Advanced Dictionary Types

### defaultdict

```python
from collections import defaultdict

# Automatically creates missing keys with default values
scores = defaultdict(int)      # Default: 0
names = defaultdict(list)      # Default: []
details = defaultdict(lambda: "Unknown")  # Custom default

# Usage
scores["Alice"] += 10  # Creates "Alice": 0, then adds 10
print(scores)          # defaultdict(<class 'int'>, {'Alice': 10})
```

### OrderedDict

```python
from collections import OrderedDict

# Maintains insertion order
ordered = OrderedDict()
ordered["first"] = 1
ordered["second"] = 2
ordered["third"] = 3

# Can move items to different positions
ordered.move_to_end("first")  # Move to end
ordered.move_to_end("first", last=False)  # Move to beginning

# Remove last inserted item
ordered.popitem()
```

### ChainMap

```python
from collections import ChainMap

# Combine multiple dictionaries
dict1 = {"name": "Alice", "age": 25}
dict2 = {"city": "New York", "country": "USA"}
dict3 = {"email": "alice@example.com"}

# Chain them together
combined = ChainMap(dict1, dict2, dict3)

# Accessing looks through all dictionaries
print(combined["name"])     # Alice (from dict1)
print(combined["country"])  # USA (from dict2)

# Updates affect the first dictionary
combined["new_key"] = "value"
print(dict1)  # Includes the new key
```

### Counter

```python
from collections import Counter

# Count occurrences of elements
text = "hello world"
letter_count = Counter(text)
print(letter_count)  # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

# Most common elements
most_common = letter_count.most_common(3)
print(most_common)  # [('l', 3), ('o', 2), ('h', 1)]

# Update count
letter_count.update("world")
print(letter_count)  # Updated counts
```

---

## Performance and Best Practices

### When to Use Dictionaries

```python
# Good use cases:
# 1. Fast lookups by key
# 2. Key-value mapping
# 3. Counting occurrences
# 4. Configuration settings
# 5. Sparse data (many zero/false values)

# Example: Configuration
config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp"
    },
    "logging": {
        "level": "INFO",
        "format": "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
    }
}
```

### Performance Considerations

```python
# Dictionary lookups are O(1) average case
user_cache = {"user1": "data1", "user2": "data2", "user3": "data3"}

# Fast membership testing
if "user1" in user_cache:  # O(1)
    # Do something

# Slower membership testing in list
user_list = ["user1", "user2", "user3"]
if "user1" in user_list:  # O(n)
    # Do something

# Memory efficient for sparse data
sparse_data = {}
for i in range(1000):
    if i % 100 == 0:  # Only store 1% of the data
        sparse_data[i] = f"value_{i}"
```

### Memory Management

```python
# Avoid creating many small dictionaries in loops
# Bad:
results = []
for i in range(1000):
    item = {"id": i, "value": f"item_{i}"}
    results.append(item)

# Good: Reuse dictionary structure
template = {"id": 0, "value": ""}
results = []
for i in range(1000):
    item = template.copy()  # or template | {"id": i, "value": f"item_{i}"}
    results.append(item)

# Use __slots__ for memory efficiency in classes
class Person:
    __slots__ = ["name", "age", "city"]
    def __init__(self, name, age, city):
        self.name = name
        self.age = age
        self.city = city
```

---

## Common Patterns and Use Cases

### Configuration Management

```python
class Config:
    def __init__(self, config_dict):
        self._config = config_dict
    
    def get(self, key, default=None):
        keys = key.split(".")
        value = self._config
        for k in keys:
            if isinstance(value, dict) and k in value:
                value = value[k]
            else:
                return default
        return value
    
    def set(self, key, value):
        keys = key.split(".")
        config = self._config
        for k in keys[:-1]:
            if k not in config:
                config[k] = {}
            config = config[k]
        config[keys[-1]] = value

# Usage
settings = Config({
    "database": {
        "host": "localhost",
        "port": 5432
    }
})

host = settings.get("database.host")  # "localhost"
settings.set("database.port", 3306)
```

### Caching and Memoization

```python
def memoize(func):
    cache = {}
    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return wrapper

@memoize
def expensive_calculation(n):
    print(f"Calculating for {n}...")
    return n * n * n
```

### Data Processing Pipeline

```python
# Process data through a pipeline
def process_user_data(raw_data):
    processed = {}
    
    # Clean and standardize
    processed["name"] = raw_data.get("name", "").strip().title()
    processed["email"] = raw_data.get("email", "").lower().strip()
    
    # Validate and convert
    try:
        processed["age"] = int(raw_data.get("age", 0))
    except (ValueError, TypeError):
        processed["age"] = 0
    
    # Add metadata
    processed["processed_at"] = "2023-01-01"
    processed["status"] = "processed"
    
    return processed
```

---

## Summary

- **Dictionaries**: Powerful key-value data structures with O(1) average lookup time
- **Creation**: Multiple ways including literals, dict() constructor, and comprehensions
- **Access**: Safe access with get() and conditional checking
- **Modification**: Add, update, remove elements with various methods
- **Advanced Types**: defaultdict, OrderedDict, ChainMap, and Counter for specific use cases
- **Nested Dictionaries**: Handle complex data structures with proper access patterns
- **Performance**: Choose dictionaries for fast lookups and efficient memory usage
- **Patterns**: Use dictionaries for configuration, caching, and data processing

Dictionaries are fundamental to Python programming and essential for efficient data management and organization.