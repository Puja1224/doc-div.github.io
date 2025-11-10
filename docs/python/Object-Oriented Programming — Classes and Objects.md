---
id: object-oriented-programming-classes-and-objects
title: Object-Oriented Programming — Classes and Objects
---

# Object-Oriented Programming — Classes and Objects

Object-Oriented Programming (OOP) is a programming paradigm that uses objects and classes to design programs. It organizes code into objects that contain both data (attributes) and code (methods).

---

## What is Object-Oriented Programming?

Object-Oriented Programming is a method of programming that emphasizes:

- **Objects**: Real-world entities with properties and behaviors
- **Classes**: Blueprints for creating objects
- **Encapsulation**: Bundling data and methods together
- **Inheritance**: Creating new classes from existing ones
- **Polymorphism**: Using objects of different types through a common interface
- **Abstraction**: Hiding complex implementation details

---

## Classes and Objects

### What is a Class?

A class is a blueprint or template for creating objects. It defines the attributes (data) and methods (functions) that objects of that class will have.

### What is an Object?

An object is an instance of a class. It represents a specific entity created from the class blueprint.

---

## Creating Classes and Objects

### Basic Class Definition

```python
class Car:
    # Class attribute (shared by all instances)
    wheels = 4
    
    # Constructor method (initializer)
    def __init__(self, brand, model, year):
        # Instance attributes (unique to each object)
        self.brand = brand
        self.model = model
        self.year = year
        self.is_running = False
    
    # Instance method
    def start_engine(self):
        self.is_running = True
        print(f"The {self.brand} {self.model} engine is now running!")
    
    def stop_engine(self):
        self.is_running = False
        print(f"The {self.brand} {self.model} engine is now stopped!")
    
    def get_info(self):
        return f"{self.year} {self.brand} {self.model} (Running: {self.is_running})"
```

### Creating Objects

```python
# Creating objects (instances of the Car class)
my_car = Car("Toyota", "Camry", 2022)
friend_car = Car("Honda", "Civic", 2021)

# Accessing attributes
print(my_car.brand)  # Output: Toyota
print(my_car.wheels)  # Output: 4

# Calling methods
my_car.start_engine()  # Output: The Toyota Camry engine is now running!
print(my_car.get_info())  # Output: 2022 Toyota Camry (Running: True)

my_car.stop_engine()
print(my_car.get_info())  # Output: 2022 Toyota Camry (Running: False)
```

---

## The `self` Parameter

The `self` parameter represents the instance of the class. It allows access to instance attributes and methods within the class.

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance attribute
        self.age = age
    
    def introduce(self):
        # Using self to access instance attributes
        print(f"Hi, I'm {self.name} and I'm {self.age} years old.")
    
    def birthday(self):
        # Using self to modify instance attributes
        self.age += 1
        print(f"Happy birthday! Now I'm {self.age} years old.")

person = Person("Alice", 25)
person.introduce()  # Output: Hi, I'm Alice and I'm 25 years old.
person.birthday()   # Output: Happy birthday! Now I'm 26 years old.
```

---

## Constructor and Destructor

### Constructor (`__init__`)

The constructor is called automatically when an object is created.

```python
class Student:
    def __init__(self, name, student_id):
        print(f"Creating new student: {name}")
        self.name = name
        self.student_id = student_id
        self.grades = []
    
    def add_grade(self, grade):
        self.grades.append(grade)
        print(f"Grade {grade} added to {self.name}'s record")
    
    def get_average(self):
        if self.grades:
            return sum(self.grades) / len(self.grades)
        return 0

student = Student("John", "S12345")  # Output: Creating new student: John
```

### Destructor (`__del__`)

The destructor is called when an object is about to be destroyed.

```python
class DatabaseConnection:
    def __init__(self, database_name):
        self.database_name = database_name
        print(f"Connecting to database: {database_name}")
    
    def __del__(self):
        print(f"Closing connection to database: {self.database_name}")
    
    def query(self, sql):
        print(f"Executing query on {self.database_name}: {sql}")

# Creating and using the object
db = DatabaseConnection("MyDatabase")
db.query("SELECT * FROM users")
# When the object goes out of scope, __del__ is called automatically
```

---

## Class Attributes vs Instance Attributes

### Class Attributes

Class attributes are shared by all instances of the class.

```python
class Circle:
    # Class attribute
    pi = 3.14159
    
    def __init__(self, radius):
        self.radius = radius  # Instance attribute
    
    def area(self):
        return Circle.pi * self.radius * self.radius
    
    def circumference(self):
        return 2 * Circle.pi * self.radius

# All circles share the same pi value
circle1 = Circle(5)
circle2 = Circle(10)

print(circle1.area())  # Output: 78.53975
print(circle2.area())  # Output: 314.159
print(Circle.pi)       # Output: 3.14159
```

### Instance Attributes

Instance attributes are unique to each object.

```python
class Book:
    # Class attribute
    total_books = 0
    
    def __init__(self, title, author):
        self.title = title
        self.author = author
        Book.total_books += 1  # Accessing class attribute
        self.book_id = Book.total_books
    
    def display_info(self):
        print(f"Book {self.book_id}: {self.title} by {self.author}")

book1 = Book("1984", "George Orwell")
book2 = Book("To Kill a Mockingbird", "Harper Lee")

book1.display_info()  # Output: Book 1: 1984 by George Orwell
book2.display_info()  # Output: Book 2: To Kill a Mockingbird by Harper Lee
print(f"Total books: {Book.total_books}")  # Output: Total books: 2
```

---

## Methods

### Instance Methods

Instance methods operate on instance attributes and can access both instance and class attributes.

```python
class BankAccount:
    def __init__(self, owner, initial_balance=0):
        self.owner = owner
        self.balance = initial_balance
    
    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            print(f"Deposited ${amount}. New balance: ${self.balance}")
        else:
            print("Deposit amount must be positive!")
    
    def withdraw(self, amount):
        if amount <= self.balance and amount > 0:
            self.balance -= amount
            print(f"Withdrew ${amount}. New balance: ${self.balance}")
        elif amount <= 0:
            print("Withdrawal amount must be positive!")
        else:
            print("Insufficient funds!")

account = BankAccount("Alice", 1000)
account.deposit(500)   # Output: Deposited $500. New balance: $1500
account.withdraw(200)  # Output: Withdrew $200. New balance: $1300
```

### Class Methods

Class methods operate on class attributes and are defined using the `@classmethod` decorator.

```python
class Employee:
    # Class attribute
    company_name = "Tech Corp"
    employees = []
    
    def __init__(self, name, position):
        self.name = name
        self.position = position
        Employee.employees.append(self)
        self.employee_id = len(Employee.employees)
    
    @classmethod
    def get_company_name(cls):
        return cls.company_name
    
    @classmethod
    def get_total_employees(cls):
        return len(cls.employees)
    
    @classmethod
    def list_employees(cls):
        print(f"Employees of {cls.company_name}:")
        for emp in cls.employees:
            print(f"  {emp.employee_id}. {emp.name} - {emp.position}")
    
    def display_info(self):
        print(f"Employee {self.employee_id}: {self.name} - {self.position}")

# Using class methods
emp1 = Employee("John Doe", "Software Engineer")
emp2 = Employee("Jane Smith", "Data Scientist")

print(Employee.get_company_name())  # Output: Tech Corp
print(Employee.get_total_employees())  # Output: 2
Employee.list_employees()
```

### Static Methods

Static methods don't operate on instance or class attributes and are defined using the `@staticmethod` decorator.

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def multiply(a, b):
        return a * b
    
    @staticmethod
    def is_even(number):
        return number % 2 == 0
    
    @staticmethod
    def factorial(n):
        if n <= 1:
            return 1
        return n * MathUtils.factorial(n - 1)

# Using static methods
print(MathUtils.add(5, 3))        # Output: 8
print(MathUtils.multiply(4, 7))   # Output: 28
print(MathUtils.is_even(10))      # Output: True
print(MathUtils.factorial(5))     # Output: 120
```

---

## Encapsulation

Encapsulation restricts direct access to some of an object's components, which is a fundamental concept of OOP.

### Public, Protected, and Private Attributes

```python
class Person:
    def __init__(self, name, age, ssn):
        self.name = name           # Public attribute
        self._age = age            # Protected attribute (convention)
        self.__ssn = ssn           # Private attribute (name mangling)
    
    def get_age(self):
        return self._age
    
    def get_ssn(self):
        return self.__ssn
    
    def set_age(self, new_age):
        if new_age > 0:
            self._age = new_age
        else:
            print("Invalid age!")
    
    def __display_private_info(self):
        print(f"Private info: {self.__ssn}")

person = Person("Alice", 30, "123-45-6789")

# Accessing public attribute
print(person.name)  # Output: Alice

# Accessing protected attribute (not recommended but possible)
print(person._age)  # Output: 30

# Accessing private attribute through methods
print(person.get_ssn())  # Output: 123-45-6789

# Modifying protected attribute through method
person.set_age(31)
print(person.get_age())  # Output: 31

# Trying to access private attribute directly (will fail)
# print(person.__ssn)  # AttributeError

# Calling private method (will fail)
# person.__display_private_info()  # AttributeError
```

---

## Inheritance

Inheritance allows a class to inherit attributes and methods from another class.

### Single Inheritance

```python
# Parent class
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        print(f"{self.name} makes a sound")
    
    def describe(self):
        print(f"This is {self.name}, a {self.species}")

# Child class inheriting from Animal
class Dog(Animal):
    def __init__(self, name, breed):
        # Calling parent class constructor
        super().__init__(name, "Dog")
        self.breed = breed
    
    # Overriding parent method
    def make_sound(self):
        print(f"{self.name} barks: Woof! Woof!")
    
    def wag_tail(self):
        print(f"{self.name} wags their tail happily")
    
    def describe(self):
        # Calling parent method and adding more info
        super().describe()
        print(f"Breed: {self.breed}")

# Creating instances
animal = Animal("Generic", "Unknown")
dog = Dog("Buddy", "Golden Retriever")

animal.describe()  # Output: This is Generic, a Unknown
animal.make_sound()  # Output: Generic makes a sound

dog.describe()  # Output: This is Buddy, a Dog\nBreed: Golden Retriever
dog.make_sound()  # Output: Buddy barks: Woof! Woof!
dog.wag_tail()  # Output: Buddy wags their tail happily
```

### Multiple Inheritance

```python
class Flyer:
    def __init__(self):
        self.can_fly = True
    
    def fly(self):
        print("I can fly!")

class Swimmer:
    def __init__(self):
        self.can_swim = True
    
    def swim(self):
        print("I can swim!")

class Duck(Flyer, Swimmer):
    def __init__(self, name):
        super().__init__()  # Calls first parent (Flyer) constructor
        self.name = name
    
    def describe(self):
        print(f"I am {self.name}. I can {'fly' if self.can_fly else 'not fly'} and {'swim' if self.can_swim else 'not swim'}")

duck = Duck("Donald")
duck.fly()      # Output: I can fly!
duck.swim()     # Output: I can swim!
duck.describe() # Output: I am Donald. I can fly and swim
```

### Method Resolution Order (MRO)

```python
class A:
    def method(self):
        print("Method from class A")

class B:
    def method(self):
        print("Method from class B")

class C(A, B):
    pass

# Check method resolution order
print(C.__mro__)
# Output: (<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)

c = C()
c.method()  # Output: Method from class A (first in MRO)
```

---

## Polymorphism

Polymorphism allows objects of different classes to be treated as objects of a common superclass.

### Method Overriding

```python
class Shape:
    def area(self):
        raise NotImplementedError("Subclass must implement area method")
    
    def perimeter(self):
        raise NotImplementedError("Subclass must implement perimeter method")

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius * self.radius
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# Polymorphic function
def calculate_total_area(shapes):
    total = 0
    for shape in shapes:
        total += shape.area()
    return total

# Using polymorphism
shapes = [Rectangle(5, 3), Circle(4)]
print(f"Total area: {calculate_total_area(shapes)}")  # Output: Total area: 65.2744
```

### Duck Typing

```python
class Bird:
    def fly(self):
        print("Bird is flying")

class Airplane:
    def fly(self):
        print("Airplane is flying")

class Person:
    def fly(self):
        print("Person is pretending to fly")

def make_it_fly(flying_object):
    flying_object.fly()  # Doesn't care about the type, only that it has a fly method

# Using duck typing
bird = Bird()
airplane = Airplane()
person = Person()

make_it_fly(bird)      # Output: Bird is flying
make_it_fly(airplane)  # Output: Airplane is flying
make_it_fly(person)    # Output: Person is pretending to fly
```

---

## Abstract Classes

Abstract classes cannot be instantiated and are meant to be subclassed.

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
    
    @abstractmethod
    def start_engine(self):
        pass
    
    @abstractmethod
    def stop_engine(self):
        pass
    
    def display_info(self):
        print(f"{self.brand} {self.model}")

class Car(Vehicle):
    def start_engine(self):
        print(f"{self.brand} {self.model} car engine started with key ignition")
    
    def stop_engine(self):
        print(f"{self.brand} {self.model} car engine stopped")

class Motorcycle(Vehicle):
    def start_engine(self):
        print(f"{self.brand} {self.model} motorcycle engine started with kick/button")
    
    def stop_engine(self):
        print(f"{self.brand} {self.model} motorcycle engine stopped")

# Creating objects
car = Car("Toyota", "Camry")
motorcycle = Motorcycle("Harley-Davidson", "Sportster")

car.start_engine()      # Output: Toyota Camry car engine started with key ignition
motorcycle.start_engine()  # Output: Harley-Davidson Sportster motorcycle engine started with kick/button

# Cannot create abstract class instance
# vehicle = Vehicle("Generic", "Model")  # This would raise an error
```

---

## Special Methods (Magic Methods)

Special methods allow you to define how objects behave with built-in Python operations.

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    def __str__(self):
        return f"'{self.title}' by {self.author}"
    
    def __repr__(self):
        return f"Book('{self.title}', '{self.author}', {self.pages})"
    
    def __len__(self):
        return self.pages
    
    def __eq__(self, other):
        if not isinstance(other, Book):
            return False
        return (self.title == other.title and 
                self.author == other.author)
    
    def __lt__(self, other):
        return self.pages < other.pages
    
    def __add__(self, other):
        if isinstance(other, Book):
            return f"{self.pages + other.pages} pages total"
        return NotImplemented

# Using special methods
book1 = Book("1984", "George Orwell", 328)
book2 = Book("Animal Farm", "George Orwell", 112)

print(str(book1))      # Output: '1984' by George Orwell
print(repr(book1))     # Output: Book('1984', 'George Orwell', 328)
print(len(book1))      # Output: 328
print(book1 < book2)   # Output: False (328 > 112)
print(book1 == book2)  # Output: True (same author)
print(book1 + book2)   # Output: 440 pages total
```

---

## Property Decorators

Properties allow you to define methods that can be accessed like attributes.

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature cannot be below absolute zero!")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5/9

# Using properties
temp = Temperature(25)
print(temp.celsius)      # Output: 25
print(temp.fahrenheit)   # Output: 77.0

temp.fahrenheit = 86
print(temp.celsius)      # Output: 30.0
print(temp.fahrenheit)   # Output: 86.0
```

---

## Practical Example: Library Management System

```python
from datetime import datetime, timedelta

class Book:
    def __init__(self, isbn, title, author, copies=1):
        self.isbn = isbn
        self.title = title
        self.author = author
        self.copies = copies
        self.available_copies = copies
    
    def is_available(self):
        return self.available_copies > 0
    
    def borrow(self):
        if self.is_available():
            self.available_copies -= 1
            return True
        return False
    
    def return_book(self):
        if self.available_copies < self.copies:
            self.available_copies += 1
            return True
        return False
    
    def __str__(self):
        status = "Available" if self.is_available() else "Not Available"
        return f"{self.title} by {self.author} ({status})"

class Member:
    def __init__(self, member_id, name, email):
        self.member_id = member_id
        self.name = name
        self.email = email
        self.borrowed_books = []
        self.borrow_dates = {}
    
    def can_borrow(self):
        return len(self.borrowed_books) < 5
    
    def borrow_book(self, book, library):
        if self.can_borrow() and book.borrow():
            self.borrowed_books.append(book)
            self.borrow_dates[book.isbn] = datetime.now()
            print(f"{self.name} borrowed '{book.title}'")
            return True
        return False
    
    def return_book(self, book, library):
        if book in self.borrowed_books:
            self.borrowed_books.remove(book)
            del self.borrow_dates[book.isbn]
            book.return_book()
            print(f"{self.name} returned '{book.title}'")
            return True
        return False
    
    def get_overdue_books(self, days=14):
        overdue = []
        for book in self.borrowed_books:
            borrow_date = self.borrow_dates[book.isbn]
            if datetime.now() - borrow_date > timedelta(days=days):
                overdue.append(book)
        return overdue

class Library:
    def __init__(self, name):
        self.name = name
        self.books = []
        self.members = []
    
    def add_book(self, book):
        self.books.append(book)
        print(f"Added '{book.title}' to {self.name}")
    
    def register_member(self, member):
        self.members.append(member)
        print(f"Registered member: {member.name}")
    
    def find_book(self, title):
        for book in self.books:
            if book.title.lower() == title.lower():
                return book
        return None
    
    def find_member(self, member_id):
        for member in self.members:
            if member.member_id == member_id:
                return member
        return None

# Using the library system
library = Library("City Library")

# Adding books
book1 = Book("978-0-452-28423-4", "1984", "George Orwell", 3)
book2 = Book("978-0-06-112008-4", "To Kill a Mockingbird", "Harper Lee", 2)

library.add_book(book1)
library.add_book(book2)

# Registering members
member1 = Member("M001", "Alice Johnson", "alice@email.com")
member2 = Member("M002", "Bob Smith", "bob@email.com")

library.register_member(member1)
library.register_member(member2)

# Borrowing books
member1.borrow_book(book1, library)
member1.borrow_book(book2, library)
member2.borrow_book(book1, library)

# Checking availability
print(f"\nBook availability:")
for book in library.books:
    print(f"{book.title}: {book.available_copies}/{book.copies} available")

# Returning books
member1.return_book(book1, library)

print(f"\nFinal availability:")
for book in library.books:
    print(f"{book.title}: {book.available_copies}/{book.copies} available")
```

---

## Best Practices

1. **Follow naming conventions**: Use PascalCase for class names, snake_case for attributes and methods
2. **Use properties for computed attributes**: Instead of direct attribute access when calculation is involved
3. **Implement `__str__` and `__repr__`**: For better debugging and display
4. **Use inheritance wisely**: Don't over-engineer with unnecessary inheritance
5. **Favor composition over inheritance**: When possible, use object composition instead of inheritance
6. **Document your classes**: Use docstrings to explain class purpose and usage
7. **Handle exceptions gracefully**: Provide meaningful error messages
8. **Keep classes focused**: Each class should have a single, well-defined responsibility

---

✅ **Summary:**

- Classes are blueprints for creating objects with attributes and methods
- Objects are instances of classes with unique data
- Encapsulation bundles data and methods together
- Inheritance allows code reuse through class hierarchies
- Polymorphism enables different objects to respond to the same interface
- Abstract classes enforce implementation contracts
- Special methods customize object behavior with built-in operations
- Properties provide controlled attribute access
- OOP promotes code organization, reusability, and maintainability