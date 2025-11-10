---
id: exception-handling
title: Exception Handling in Python
---

# Exception Handling in Python

Exception handling is a crucial aspect of Python programming that allows you to handle errors gracefully and maintain program flow when unexpected situations occur. Python provides a robust mechanism for handling exceptions using the try, except, else, and finally statements.

---

## What is Exception Handling?

An exception is an event that occurs during program execution that disrupts the normal flow of instructions. Instead of crashing when an error occurs, exception handling allows you to:
- **Catch** and handle errors gracefully
- **Recover** from error conditions
- **Log** errors for debugging
- **Clean up** resources properly
- **Provide** meaningful error messages to users

---

## Basic Exception Handling

### Simple Try-Except Block

```python
try:
    # Code that might cause an exception
    result = 10 / 0
    print("This won't be executed")
except ZeroDivisionError:
    # Code to handle the exception
    print("Error: Cannot divide by zero!")

# Output: Error: Cannot divide by zero!
```

### Try-Except with Exception Variable

```python
try:
    number = int("not_a_number")
except ValueError as e:
    print(f"Error occurred: {e}")
    print(f"Exception type: {type(e).__name__}")

# Output: 
# Error occurred: invalid literal for int() with base 10: 'not_a_number'
# Exception type: ValueError
```

### Try-Except with Multiple Operations

```python
try:
    # Multiple operations that might fail
    numbers = [1, 2, 3]
    print(numbers[5])  # IndexError
    result = 10 / 0    # This won't be reached
except IndexError:
    print("Error: List index out of range")
except ZeroDivisionError:
    print("Error: Cannot divide by zero")

# Output: Error: List index out of range
```

---

## Multiple Exception Types

### Handling Multiple Specific Exceptions

```python
try:
    value = int("hello")
    result = 10 / 0
    numbers = [1, 2, 3]
    print(numbers[10])
except ValueError:
    print("Error: Invalid value provided")
except ZeroDivisionError:
    print("Error: Division by zero")
except IndexError:
    print("Error: Index out of range")
except (TypeError, AttributeError) as e:
    print(f"Type or attribute error: {e}")
```

### Catching All Exceptions

```python
try:
    # Risky operation
    risky_operation()
except Exception as e:
    print(f"An error occurred: {e}")
    # Log the error for debugging
    logging.error(f"Exception details: {e}")
```

### Catching All Exceptions with Specific Types

```python
try:
    # Some operation
    data = process_data()
except (ValueError, TypeError) as e:
    # Handle data-related errors
    print(f"Data error: {e}")
except (FileNotFoundError, PermissionError) as e:
    # Handle file-related errors
    print(f"File error: {e}")
except Exception as e:
    # Handle any other unexpected errors
    print(f"Unexpected error: {e}")
```

---

## The Else Clause

The `else` clause executes only if no exceptions are raised in the `try` block:

```python
try:
    number = int("42")
    result = number * 2
except ValueError:
    print("Error: Invalid number format")
else:
    # Only executed if no exception occurred
    print(f"Success! Result: {result}")

# Output: Success! Result: 84
```

### Practical Example with Else

```python
def divide_numbers(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
        return None
    else:
        # Only return if no exception occurred
        print("Division successful")
        return result

# Usage
answer = divide_numbers(10, 2)  # Prints "Division successful", returns 5
error_answer = divide_numbers(10, 0)  # Prints error message, returns None
```

---

## The Finally Clause

The `finally` clause always executes, whether an exception occurred or not:

```python
try:
    file = open("example.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    # This always executes
    print("Cleaning up resources")
    if 'file' in locals():
        file.close()
```

### Database Connection Example

```python
import sqlite3

def query_database(query):
    conn = None
    try:
        conn = sqlite3.connect("database.db")
        cursor = conn.cursor()
        cursor.execute(query)
        result = cursor.fetchall()
        return result
    except sqlite3.Error as e:
        print(f"Database error: {e}")
        return None
    finally:
        # Always close the connection
        if conn:
            conn.close()
            print("Database connection closed")
```

### File Operations with Finally

```python
def read_file_safely(filename):
    file = None
    try:
        file = open(filename, 'r', encoding='utf-8')
        content = file.read()
        return content
    except FileNotFoundError:
        print(f"File {filename} not found")
        return None
    except IOError as e:
        print(f"I/O error: {e}")
        return None
    finally:
        if file:
            file.close()
            print("File closed successfully")
```

---

## Raising Exceptions

### Raising Built-in Exceptions

```python
def withdraw_money(balance, amount):
    if amount > balance:
        raise ValueError("Insufficient funds")
    if amount <= 0:
        raise ValueError("Amount must be positive")
    return balance - amount

# Usage
try:
    new_balance = withdraw_money(100, 150)
except ValueError as e:
    print(f"Transaction failed: {e}")
```

### Raising with Custom Messages

```python
def calculate_sqrt(number):
    if number < 0:
        raise ValueError(f"Cannot calculate square root of negative number: {number}")
    import math
    return math.sqrt(number)

try:
    result = calculate_sqrt(-4)
except ValueError as e:
    print(f"Calculation error: {e}")
```

### Raising Exceptions in Validation

```python
def validate_age(age):
    if not isinstance(age, int):
        raise TypeError("Age must be an integer")
    if age < 0:
        raise ValueError("Age cannot be negative")
    if age > 150:
        raise ValueError("Age seems unrealistic")
    return True

def validate_user(name, age):
    try:
        if not name or len(name.strip()) == 0:
            raise ValueError("Name cannot be empty")
        validate_age(age)
        print(f"User {name}, age {age} is valid")
    except (TypeError, ValueError) as e:
        print(f"Validation error: {e}")
```

---

## Custom Exceptions

### Creating Custom Exception Classes

```python
class BankAccountError(Exception):
    """Base exception for bank account operations"""
    pass

class InsufficientFundsError(BankAccountError):
    """Raised when attempting to withdraw more than available balance"""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Insufficient funds: balance={balance}, amount={amount}")

class InvalidAmountError(BankAccountError):
    """Raised when amount is invalid"""
    pass

class BankAccount:
    def __init__(self, balance=0):
        if balance < 0:
            raise ValueError("Initial balance cannot be negative")
        self.balance = balance
    
    def withdraw(self, amount):
        if amount <= 0:
            raise InvalidAmountError("Amount must be positive")
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount
        return self.balance
    
    def deposit(self, amount):
        if amount <= 0:
            raise InvalidAmountError("Amount must be positive")
        self.balance += amount
        return self.balance
```

### Using Custom Exceptions

```python
try:
    account = BankAccount(100)
    account.withdraw(150)
except InsufficientFundsError as e:
    print(f"Transaction failed: {e}")
    print(f"Requested: {e.amount}, Available: {e.balance}")
except InvalidAmountError as e:
    print(f"Invalid amount: {e}")
except BankAccountError as e:
    print(f"Account error: {e}")
```

### Custom Exception with Additional Data

```python
class APIError(Exception):
    def __init__(self, message, status_code=None, response=None):
        super().__init__(message)
        self.status_code = status_code
        self.response = response

def make_api_request(url):
    try:
        import requests
        response = requests.get(url)
        if response.status_code >= 400:
            raise APIError(
                f"API request failed with status {response.status_code}",
                status_code=response.status_code,
                response=response.text
            )
        return response.json()
    except requests.RequestException as e:
        raise APIError(f"Network error: {e}")

try:
    data = make_api_request("https://api.example.com/data")
except APIError as e:
    print(f"API Error: {e}")
    if e.status_code:
        print(f"Status Code: {e.status_code}")
    if e.response:
        print(f"Response: {e.response}")
```

---

## Exception Hierarchy

### Understanding Python's Exception Hierarchy

```python
# Exception hierarchy examples
try:
    result = 1 / 0
except ArithmeticError:  # Parent of ZeroDivisionError
    print("Arithmetic error caught")

try:
    result = int("abc")
except ValueError:  # Parent of various value-related errors
    print("Value error caught")

try:
    my_list = [1, 2, 3]
    print(my_list[10])
except LookupError:  # Parent of IndexError and KeyError
    print("Lookup error caught")

try:
    my_dict = {"key": "value"}
    print(my_dict["missing"])
except KeyError:  # Specific lookup error
    print("Key not found")
```

### Catching Parent vs Child Exceptions

```python
# Bad: Catching parent exception first
try:
    result = 1 / 0
except Exception:  # Too broad
    print("Some error occurred")

# Good: Most specific exceptions first
try:
    result = 1 / 0
except ZeroDivisionError:  # Most specific
    print("Cannot divide by zero")
except ArithmeticError:    # More general
    print("Arithmetic error")
except Exception:          # Catch-all (should be last)
    print("Some other error")
```

---

## Practical Exception Handling Patterns

### Context Managers and Exception Handling

```python
# Using context managers for automatic resource cleanup
class DatabaseConnection:
    def __init__(self, connection_string):
        self.connection_string = connection_string
        self.connection = None
    
    def __enter__(self):
        try:
            self.connection = self.connect()
            return self.connection
        except Exception as e:
            print(f"Failed to connect: {e}")
            raise
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.connection:
            self.connection.close()
            print("Database connection closed")

# Usage
try:
    with DatabaseConnection("postgresql://...") as conn:
        # Database operations
        cursor = conn.cursor()
        cursor.execute("SELECT * FROM users")
        results = cursor.fetchall()
except Exception as e:
    print(f"Database operation failed: {e}")
```

### Retry Mechanism

```python
import time
import random

def retry_with_backoff(func, max_retries=3, base_delay=1):
    """
    Retry a function with exponential backoff
    """
    for attempt in range(max_retries + 1):
        try:
            return func()
        except Exception as e:
            if attempt == max_retries:
                print(f"Max retries reached. Final error: {e}")
                raise
            
            delay = base_delay * (2 ** attempt) + random.uniform(0, 1)
            print(f"Attempt {attempt + 1} failed: {e}. Retrying in {delay:.2f}s...")
            time.sleep(delay)

# Example usage
def unstable_operation():
    if random.random() < 0.7:  # 70% chance of failure
        raise ConnectionError("Network connection failed")
    return "Success!"

try:
    result = retry_with_backoff(unstable_operation, max_retries=3)
    print(f"Result: {result}")
except Exception as e:
    print(f"Operation failed after retries: {e}")
```

### Exception Logging and Monitoring

```python
import logging
import traceback

# Configure logging
logging.basicConfig(
    level=logging.ERROR,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('app.log'),
        logging.StreamHandler()
    ]
)

def safe_divide(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError as e:
        logging.error(f"Division by zero: {a} / {b}")
        logging.debug(f"Traceback: {traceback.format_exc()}")
        return None
    except TypeError as e:
        logging.error(f"Type error: {e}")
        return None
    except Exception as e:
        logging.error(f"Unexpected error: {e}")
        return None

# Usage with logging
result = safe_divide(10, 0)  # Will log the error
```

### Input Validation with Exceptions

```python
def get_valid_input(prompt, input_type=float, min_value=None, max_value=None):
    """
    Get valid input from user with exception handling
    """
    while True:
        try:
            user_input = input(prompt)
            value = input_type(user_input)
            
            if min_value is not None and value < min_value:
                print(f"Error: Value must be at least {min_value}")
                continue
            
            if max_value is not None and value > max_value:
                print(f"Error: Value must be at most {max_value}")
                continue
            
            return value
            
        except ValueError as e:
            print(f"Error: Please enter a valid {input_type.__name__}")
            print(f"Details: {e}")
        except KeyboardInterrupt:
            print("\nOperation cancelled by user")
            return None
        except Exception as e:
            print(f"Unexpected error: {e}")

# Usage examples
age = get_valid_input("Enter your age: ", int, 0, 120)
temperature = get_valid_input("Enter temperature: ", float, -273.15)
```

---

## Best Practices

### When to Use Exception Handling

```python
# Good: Use exceptions for exceptional circumstances
def divide_safe(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

# Bad: Don't use exceptions for normal control flow
def get_item_safe(items, index):
    try:
        return items[index]
    except IndexError:
        return None  # Should use if statement instead

# Better: Normal control flow
def get_item_better(items, index):
    if 0 <= index < len(items):
        return items[index]
    return None
```

### Exception Handling Best Practices

```python
# 1. Be specific about exception types
try:
    risky_operation()
except ValueError:  # Good: Specific
    handle_error()
except Exception:  # Bad: Too broad
    handle_error()

# 2. Keep try blocks small
try:
    # Just the risky operation
    result = process_data()
except SpecificError as e:
    handle_error()

# Don't do this:
try:
    # Multiple operations
    data = load_data()
    processed = process_data(data)
    save_data(processed)
except Error:  # Hard to know which operation failed
    handle_error()

# 3. Always clean up resources
try:
    file = open("data.txt")
    content = file.read()
finally:
    file.close()  # Always executed

# Better: Use context managers
with open("data.txt") as file:
    content = file.read()  # Automatic cleanup
```

### Custom Exception Design

```python
# Good: Inherit from appropriate base exception
class ValidationError(Exception):
    """Base class for validation errors"""
    pass

class AgeValidationError(ValidationError):
    """Raised when age validation fails"""
    def __init__(self, age, reason):
        self.age = age
        self.reason = reason
        super().__init__(f"Age {age} is invalid: {reason}")

# Usage
def validate_age(age):
    if not isinstance(age, int):
        raise AgeValidationError(age, "Must be an integer")
    if age < 0:
        raise AgeValidationError(age, "Must be non-negative")
    if age > 150:
        raise AgeValidationError(age, "Unrealistic age")
    return True
```

---

## Common Exception Types

### Built-in Exception Reference

```python
# ValueError - Invalid value for type
try:
    number = int("not_a_number")
except ValueError as e:
    print(f"ValueError: {e}")

# TypeError - Wrong type for operation
try:
    result = "string" + 5
except TypeError as e:
    print(f"TypeError: {e}")

# IndexError - List index out of range
try:
    my_list = [1, 2, 3]
    print(my_list[10])
except IndexError as e:
    print(f"IndexError: {e}")

# KeyError - Dictionary key not found
try:
    my_dict = {"a": 1, "b": 2}
    print(my_dict["c"])
except KeyError as e:
    print(f"KeyError: {e}")

# FileNotFoundError - File doesn't exist
try:
    with open("nonexistent.txt") as f:
        content = f.read()
except FileNotFoundError as e:
    print(f"FileNotFoundError: {e}")

# ZeroDivisionError - Division by zero
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"ZeroDivisionError: {e}")

# AttributeError - Object doesn't have attribute
try:
    my_string = "hello"
    my_string.non_existent_method()
except AttributeError as e:
    print(f"AttributeError: {e}")
```

### Exception Chaining

```python
# Exception chaining - Python 3+
def read_config_file(filename):
    try:
        with open(filename) as f:
            return f.read()
    except FileNotFoundError as e:
        # Chain the exception with additional context
        raise ConfigFileError(f"Configuration file '{filename}' not found") from e

class ConfigFileError(Exception):
    pass

try:
    config = read_config_file("config.txt")
except ConfigFileError as e:
    print(f"Config error: {e}")
    print(f"Original exception: {e.__cause__}")
```

---

## Advanced Patterns

### Exception Groups (Python 3.11+)

```python
# Multiple exceptions in a group
try:
    # Some operations that might fail
    raise ExceptionGroup("Multiple errors", [
        ValueError("Invalid value"),
        TypeError("Wrong type"),
        ZeroDivisionError("Division by zero")
    ])
except* ValueError as e:
    print(f"Value errors: {e.exceptions}")
except* TypeError as e:
    print(f"Type errors: {e.exceptions}")
except* ZeroDivisionError as e:
    print(f"Division errors: {e.exceptions}")
```

### Suppressing Exceptions

```python
# Suppress specific exceptions
try:
    risky_operation()
except ValueError:
    pass  # Silently ignore ValueError
except Exception as e:
    print(f"Other error: {e}")

# Better: Be explicit about suppression
try:
    result = optional_operation()
except OptionalOperationError:
    pass  # Operation is optional, continue normally
```

---

## Summary

- **Exception Handling**: Use try-except blocks to handle errors gracefully
- **Multiple Exceptions**: Handle different exception types with specific except blocks
- **Else Clause**: Execute code only when no exceptions occur in try block
- **Finally Clause**: Always execute cleanup code regardless of exceptions
- **Raising Exceptions**: Use `raise` to create and trigger exceptions
- **Custom Exceptions**: Create specific exception classes for your application
- **Best Practices**: Be specific about exception types, keep try blocks small, clean up resources
- **Exception Hierarchy**: Understand parent-child relationships between exception types
- **Practical Patterns**: Use context managers, retry mechanisms, logging, and input validation

Exception handling is essential for writing robust, reliable Python applications that can handle unexpected situations gracefully.