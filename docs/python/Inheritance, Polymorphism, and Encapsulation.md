---
id: inheritance-polymorphism-abstraction-and-encapsulation
title: Inheritance, Polymorphism, Abstraction and Encapsulation
---

# Inheritance, Polymorphism, Abstraction and Encapsulation

These are the four fundamental principles of Object-Oriented Programming (OOP) that form the foundation of object-oriented design and programming.

---

## 1. Inheritance

Inheritance is the mechanism by which one class (child/subclass) derives properties and methods from another class (parent/superclass). It promotes code reusability and establishes a hierarchical relationship between classes.

### Types of Inheritance

#### Single Inheritance
One child class inherits from one parent class.

```python
class Animal:
    def __init__(self, name, species):
        self.name = name
        self.species = species
    
    def make_sound(self):
        print(f"{self.name} makes a sound")
    
    def display_info(self):
        print(f"Name: {self.name}, Species: {self.species}")

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name, "Dog")
        self.breed = breed
    
    def make_sound(self):
        print(f"{self.name} barks: Woof! Woof!")
    
    def wag_tail(self):
        print(f"{self.name} wags their tail happily")

# Using single inheritance
dog = Dog("Buddy", "Golden Retriever")
dog.display_info()  # Output: Name: Buddy, Species: Dog
dog.make_sound()     # Output: Buddy barks: Woof! Woof!
dog.wag_tail()       # Output: Buddy wags their tail happily
```

#### Multiple Inheritance
One child class inherits from multiple parent classes.

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
        flying_status = "fly" if self.can_fly else "not fly"
        swimming_status = "swim" if self.can_swim else "not swim"
        print(f"I am {self.name}. I can {flying_status} and {swimming_status}")

# Using multiple inheritance
duck = Duck("Donald")
duck.fly()      # Output: I can fly!
duck.swim()     # Output: I can swim!
duck.describe() # Output: I am Donald. I can fly and swim
```

#### Multilevel Inheritance
A class inherits from another class, which in turn inherits from another class.

```python
class Vehicle:
    def __init__(self, brand):
        self.brand = brand
    
    def start(self):
        print(f"{self.brand} vehicle is starting")

class Car(Vehicle):
    def __init__(self, brand, model):
        super().__init__(brand)
        self.model = model
    
    def display_model(self):
        print(f"Model: {self.model}")

class SportsCar(Car):
    def __init__(self, brand, model, top_speed):
        super().__init__(brand, model)
        self.top_speed = top_speed
    
    def display_top_speed(self):
        print(f"Top Speed: {self.top_speed} km/h")

# Using multilevel inheritance
sports_car = SportsCar("Ferrari", "F8 Tributo", 340)
sports_car.start()           # Output: Ferrari vehicle is starting
sports_car.display_model()   # Output: Model: F8 Tributo
sports_car.display_top_speed()  # Output: Top Speed: 340 km/h
```

#### Hierarchical Inheritance
Multiple child classes inherit from the same parent class.

```python
class Shape:
    def __init__(self, name):
        self.name = name
    
    def area(self):
        raise NotImplementedError("Subclass must implement area method")
    
    def perimeter(self):
        raise NotImplementedError("Subclass must implement perimeter method")

class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__("Rectangle")
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        super().__init__("Circle")
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius * self.radius
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# Using hierarchical inheritance
rect = Rectangle(5, 3)
circle = Circle(4)

print(f"{rect.name} - Area: {rect.area()}, Perimeter: {rect.perimeter()}")
# Output: Rectangle - Area: 15, Perimeter: 16

print(f"{circle.name} - Area: {circle.area():.2f}, Perimeter: {circle.perimeter():.2f}")
# Output: Circle - Area: 50.27, Perimeter: 25.13
```

### The `super()` Function

The `super()` function allows you to call methods from the parent class.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def introduce(self):
        print(f"Hi, I'm {self.name} and I'm {self.age} years old")

class Employee(Person):
    def __init__(self, name, age, employee_id, salary):
        super().__init__(name, age)  # Call parent constructor
        self.employee_id = employee_id
        self.salary = salary
    
    def introduce(self):
        super().introduce()  # Call parent method
        print(f"I am employee #{self.employee_id}")
    
    def work(self):
        print(f"{self.name} is working hard!")

employee = Employee("Alice", 30, "E001", 75000)
employee.introduce()
# Output: 
# Hi, I'm Alice and I'm 30 years old
# I am employee #E001
employee.work()  # Output: Alice is working hard!
```

### Method Resolution Order (MRO)

Python uses a specific order to resolve method calls in case of multiple inheritance.

```python
class A:
    def method(self):
        print("Method from class A")

class B:
    def method(self):
        print("Method from class B")

class C(A, B):
    pass

class D(B, A):
    pass

# Checking MRO
print("MRO for C:", C.__mro__)
print("MRO for D:", D.__mro__)

c = C()
c.method()  # Output: Method from class A (first in MRO)

d = D()
d.method()  # Output: Method from class B (first in MRO)
```

---

## 2. Polymorphism

Polymorphism means "many forms" and allows objects of different types to be treated as objects of a common superclass. It enables the same interface to be used for different underlying data types.

### Method Overriding

Child classes can provide their own implementation of methods that are already defined in the parent class.

```python
class Animal:
    def make_sound(self):
        print("Some generic animal sound")

class Dog(Animal):
    def make_sound(self):
        print("Woof! Woof!")

class Cat(Animal):
    def make_sound(self):
        print("Meow! Meow!")

class Cow(Animal):
    def make_sound(self):
        print("Moo! Moo!")

# Polymorphic function
def animal_sound(animal):
    animal.make_sound()

# Using polymorphism
animals = [Dog(), Cat(), Cow()]

for animal in animals:
    animal_sound(animal)
# Output:
# Woof! Woof!
# Meow! Meow!
# Moo! Moo!
```

### Duck Typing

"If it walks like a duck and quacks like a duck, then it must be a duck."

```python
class Duck:
    def swim(self):
        print("Duck is swimming")
    
    def quack(self):
        print("Quack! Quack!")

class Person:
    def swim(self):
        print("Person is swimming")
    
    def quack(self):
        print("Person is pretending to quack")

def make_it_swim_and_quack(creature):
    creature.swim()
    creature.quack()

# Using duck typing
duck = Duck()
person = Person()

make_it_swim_and_quack(duck)   # Output: Duck is swimming\nQuack! Quack!
make_it_swim_and_quack(person) # Output: Person is swimming\nPerson is pretending to quack
```

### Operator Overloading

You can define how operators work with your custom objects.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"
    
    def __add__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x + other.x, self.y + other.y)
        return NotImplemented
    
    def __sub__(self, other):
        if isinstance(other, Vector):
            return Vector(self.x - other.x, self.y - other.y)
        return NotImplemented
    
    def __mul__(self, scalar):
        if isinstance(scalar, (int, float)):
            return Vector(self.x * scalar, self.y * scalar)
        return NotImplemented
    
    def __eq__(self, other):
        if isinstance(other, Vector):
            return self.x == other.x and self.y == other.y
        return False

# Using operator overloading
v1 = Vector(3, 4)
v2 = Vector(1, 2)

print(f"v1 = {v1}")           # Output: v1 = Vector(3, 4)
print(f"v2 = {v2}")           # Output: v2 = Vector(1, 2)
print(f"v1 + v2 = {v1 + v2}") # Output: v1 + v2 = Vector(4, 6)
print(f"v1 - v2 = {v1 - v2}") # Output: v1 - v2 = Vector(2, 2)
print(f"v1 * 2 = {v1 * 2}")   # Output: v1 * 2 = Vector(6, 8)
print(f"v1 == v2: {v1 == v2}") # Output: v1 == v2: False
```

### Abstract Methods and Polymorphism

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    def __init__(self, name):
        self.name = name
    
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass
    
    def describe(self):
        print(f"This is a {self.name}")
        print(f"Area: {self.area():.2f}")
        print(f"Perimeter: {self.perimeter():.2f}")

class Triangle(Shape):
    def __init__(self, base, height, side1, side2, side3):
        super().__init__("Triangle")
        self.base = base
        self.height = height
        self.side1 = side1
        self.side2 = side2
        self.side3 = side3
    
    def area(self):
        return 0.5 * self.base * self.height
    
    def perimeter(self):
        return self.side1 + self.side2 + self.side3

class Square(Shape):
    def __init__(self, side):
        super().__init__("Square")
        self.side = side
    
    def area(self):
        return self.side ** 2
    
    def perimeter(self):
        return 4 * self.side

# Using abstract classes for polymorphism
shapes = [Triangle(6, 4, 5, 5, 6), Square(4)]

for shape in shapes:
    shape.describe()
    print("-" * 20)
```

---

## 3. Encapsulation

Encapsulation is the concept of bundling data (attributes) and methods (functions) that operate on that data into a single unit (class) and restricting direct access to some of the object's components.

### Access Modifiers

Python uses naming conventions to indicate access levels:

- **Public**: Accessible from anywhere (no underscore prefix)
- **Protected**: Accessible within the class and subclasses (single underscore prefix `_`)
- **Private**: Accessible only within the class (double underscore prefix `__`)

```python
class BankAccount:
    def __init__(self, account_holder, initial_balance=0):
        self.account_holder = account_holder    # Public attribute
        self._account_number = self._generate_account_number()  # Protected
        self.__balance = initial_balance        # Private
        self.__transaction_history = []         # Private
    
    def _generate_account_number(self):
        import random
        return f"ACC{random.randint(100000, 999999)}"
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            self.__add_transaction(f"Deposit: +${amount}")
            return True
        return False
    
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            self.__add_transaction(f"Withdrawal: -${amount}")
            return True
        return False
    
    def __add_transaction(self, transaction):
        self.__transaction_history.append(transaction)
    
    def get_balance(self):
        return self.__balance
    
    def get_account_info(self):
        return {
            'holder': self.account_holder,
            'account_number': self._account_number,
            'balance': self.get_balance()
        }
    
    def get_transaction_history(self):
        return self.__transaction_history.copy()  # Return a copy to protect original

# Using encapsulation
account = BankAccount("Alice Smith", 1000)

# Accessing public attributes
print(f"Account Holder: {account.account_holder}")  # Output: Account Holder: Alice Smith

# Accessing protected attribute (not recommended but possible)
print(f"Account Number: {account._account_number}")  # Output: Account Number: ACC123456

# Cannot access private attributes directly
# print(account.__balance)  # This would raise AttributeError

# Using public methods to interact with private data
account.deposit(500)
account.withdraw(200)

print(f"Current Balance: ${account.get_balance()}")  # Output: Current Balance: $1300
print(f"Account Info: {account.get_account_info()}")  # Output: Account Info: {'holder': 'Alice Smith', 'account_number': 'ACC123456', 'balance': 1300}
print(f"Transactions: {account.get_transaction_history()}")  # Output: Transactions: ['Deposit: +$500', 'Withdrawal: -$200']
```

### Property Decorators

Properties allow you to create managed attributes with getter, setter, and deleter methods.

```python
class Student:
    def __init__(self, name, student_id):
        self.name = name
        self._student_id = student_id
        self._age = 0  # Default age
    
    @property
    def age(self):
        return self._age
    
    @age.setter
    def age(self, value):
        if 0 <= value <= 120:
            self._age = value
        else:
            raise ValueError("Age must be between 0 and 120")
    
    @property
    def student_id(self):
        return self._student_id
    
    @student_id.setter
    def student_id(self, value):
        if isinstance(value, str) and len(value) == 6:
            self._student_id = value
        else:
            raise ValueError("Student ID must be a 6-character string")
    
    @property
    def is_adult(self):
        return self._age >= 18

# Using property decorators
student = Student("John Doe", "S12345")

# Setting properties
student.age = 20
print(f"Student {student.name}, Age: {student.age}, Adult: {student.is_adult}")
# Output: Student John Doe, Age: 20, Adult: True

# Trying to set invalid age
try:
    student.age = 150
except ValueError as e:
    print(f"Error: {e}")  # Output: Error: Age must be between 0 and 120
```

### Private Methods and Name Mangling

```python
class Calculator:
    def __init__(self):
        self.history = []
    
    def add(self, a, b):
        result = a + b
        self.__save_to_history(f"{a} + {b} = {result}")
        return result
    
    def multiply(self, a, b):
        result = a * b
        self.__save_to_history(f"{a} * {b} = {result}")
        return result
    
    def __save_to_history(self, calculation):
        self.history.append(calculation)
        if len(self.history) > 10:  # Keep only last 10 calculations
            self.history.pop(0)
    
    def get_history(self):
        return self.history.copy()
    
    def clear_history(self):
        self.history.clear()

calc = Calculator()
print(calc.add(5, 3))     # Output: 8
print(calc.multiply(4, 7))  # Output: 28
print(calc.get_history())  # Output: ['5 + 3 = 8', '4 * 7 = 28']

# Cannot access private method directly
# calc.__save_to_history("test")  # This would raise AttributeError
```

---

## 4. Abstraction

Abstraction is the concept of hiding complex implementation details and showing only the necessary features of an object. It focuses on what an object does rather than how it does it.

### Abstract Classes and Methods

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
        self.is_running = False
    
    def start(self):
        if not self.is_running:
            self._start_engine()
            self.is_running = True
            print(f"{self.brand} {self.model} is now running")
        else:
            print(f"{self.brand} {self.model} is already running")
    
    def stop(self):
        if self.is_running:
            self._stop_engine()
            self.is_running = False
            print(f"{self.brand} {self.model} has been stopped")
        else:
            print(f"{self.brand} {self.model} is not running")
    
    @abstractmethod
    def _start_engine(self):
        pass
    
    @abstractmethod
    def _stop_engine(self):
        pass
    
    @abstractmethod
    def fuel_type(self):
        pass
    
    def display_info(self):
        print(f"{self.year} {self.brand} {self.model} - Fuel: {self.fuel_type()}")

class Car(Vehicle):
    def __init__(self, brand, model, year, doors=4):
        super().__init__(brand, model, year)
        self.doors = doors
    
    def _start_engine(self):
        print("Car engine started with key ignition")
    
    def _stop_engine(self):
        print("Car engine stopped")
    
    def fuel_type(self):
        return "Gasoline"

class ElectricCar(Vehicle):
    def __init__(self, brand, model, year, battery_capacity):
        super().__init__(brand, model, year)
        self.battery_capacity = battery_capacity
    
    def _start_engine(self):
        print("Electric motor started silently")
    
    def _stop_engine(self):
        print("Electric motor stopped")
    
    def fuel_type(self):
        return "Electricity"

# Using abstract classes
car = Car("Toyota", "Camry", 2022)
electric_car = ElectricCar("Tesla", "Model 3", 2023, 75)

car.display_info()           # Output: 2022 Toyota Camry - Fuel: Gasoline
car.start()                  # Output: Car engine started with key ignition
car.stop()                   # Output: Car engine stopped

electric_car.display_info()  # Output: 2023 Tesla Model 3 - Fuel: Electricity
electric_car.start()         # Output: Electric motor started silently

# Cannot instantiate abstract class
# vehicle = Vehicle("Generic", "Model", 2022)  # This would raise TypeError
```

### Interface-like Behavior

```python
class Drawable(ABC):
    @abstractmethod
    def draw(self):
        pass
    
    @abstractmethod
    def resize(self, factor):
        pass

class Circle(Drawable):
    def __init__(self, radius):
        self.radius = radius
    
    def draw(self):
        print(f"Drawing a circle with radius {self.radius}")
    
    def resize(self, factor):
        self.radius *= factor
        print(f"Circle resized. New radius: {self.radius}")

class Rectangle(Drawable):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def draw(self):
        print(f"Drawing a rectangle {self.width}x{self.height}")
    
    def resize(self, factor):
        self.width *= factor
        self.height *= factor
        print(f"Rectangle resized. New size: {self.width}x{self.height}")

# Using interface-like behavior
shapes = [Circle(5), Rectangle(4, 6)]

for shape in shapes:
    shape.draw()
    shape.resize(1.5)
    print("-" * 20)
```

### Abstract Properties

```python
from abc import ABC, abstractproperty

class Product(ABC):
    def __init__(self, name, base_price):
        self.name = name
        self.base_price = base_price
    
    @abstractproperty
    def category(self):
        pass
    
    @property
    def price(self):
        return self.calculate_price()
    
    @abstractmethod
    def calculate_price(self):
        pass

class Electronics(Product):
    def __init__(self, name, base_price, warranty_years):
        super().__init__(name, base_price)
        self.warranty_years = warranty_years
    
    @property
    def category(self):
        return "Electronics"
    
    def calculate_price(self):
        warranty_cost = self.warranty_years * 20
        return self.base_price + warranty_cost

class Clothing(Product):
    def __init__(self, name, base_price, size, material):
        super().__init__(name, base_price)
        self.size = size
        self.material = material
    
    @property
    def category(self):
        return "Clothing"
    
    def calculate_price(self):
        material_multiplier = 1.2 if self.material == "cotton" else 1.0
        return self.base_price * material_multiplier

# Using abstract properties
laptop = Electronics("MacBook Pro", 2000, 2)
shirt = Clothing("T-Shirt", 25, "M", "cotton")

print(f"{laptop.name} ({laptop.category}): ${laptop.price}")  # Output: MacBook Pro (Electronics): $2040
print(f"{shirt.name} ({shirt.category}): ${shirt.price:.2f}") # Output: T-Shirt (Clothing): $30.00
```

---

## Practical Examples

### Example 1: Library Management System

```python
from abc import ABC, abstractmethod
from datetime import datetime, timedelta

class LibraryItem(ABC):
    def __init__(self, item_id, title, author):
        self.item_id = item_id
        self.title = title
        self.author = author
        self.is_available = True
        self.due_date = None
    
    @abstractmethod
    def calculate_late_fee(self, days_late):
        pass
    
    def checkout(self, days=14):
        if self.is_available:
            self.is_available = False
            self.due_date = datetime.now() + timedelta(days=days)
            print(f"'{self.title}' checked out. Due: {self.due_date.date()}")
            return True
        return False
    
    def return_item(self):
        if not self.is_available:
            self.is_available = True
            self.due_date = None
            print(f"'{self.title}' returned")
            return True
        return False

class Book(LibraryItem):
    def __init__(self, item_id, title, author, pages):
        super().__init__(item_id, title, author)
        self.pages = pages
    
    def calculate_late_fee(self, days_late):
        return days_late * 0.50  # $0.50 per day

class DVD(LibraryItem):
    def __init__(self, item_id, title, director, duration):
        super().__init__(item_id, title, director)
        self.duration = duration  # in minutes
    
    def calculate_late_fee(self, days_late):
        return days_late * 1.00  # $1.00 per day

class Magazine(LibraryItem):
    def __init__(self, item_id, title, issue_number):
        super().__init__(item_id, title, "Magazine Publisher")
        self.issue_number = issue_number
    
    def calculate_late_fee(self, days_late):
        return days_late * 0.25  # $0.25 per day

# Using the library system
book = Book("B001", "Python Programming", "Guido van Rossum", 400)
dvd = DVD("D001", "The Matrix", "Wachowski Brothers", 136)
magazine = Magazine("M001", "Python Weekly", 150)

items = [book, dvd, magazine]
for item in items:
    item.checkout()
    print(f"Late fee (5 days): ${item.calculate_late_fee(5):.2f}")
    item.return_item()
    print("-" * 20)
```

### Example 2: Shape Drawing Application

```python
from abc import ABC, abstractmethod
import math

class Shape(ABC):
    def __init__(self, name, color):
        self.name = name
        self.color = color
    
    @abstractmethod
    def area(self):
        pass
    
    @abstractmethod
    def perimeter(self):
        pass
    
    def display_info(self):
        print(f"{self.name} ({self.color})")
        print(f"  Area: {self.area():.2f}")
        print(f"  Perimeter: {self.perimeter():.2f}")

class TwoDimensionalShape(Shape):
    def __init__(self, name, color):
        super().__init__(name, color)
        self.dimensions = 2

class ThreeDimensionalShape(Shape):
    def __init__(self, name, color):
        super().__init__(name, color)
        self.dimensions = 3
    
    @abstractmethod
    def volume(self):
        pass
    
    def display_info(self):
        super().display_info()
        print(f"  Volume: {self.volume():.2f}")

class Circle(TwoDimensionalShape):
    def __init__(self, radius, color="Red"):
        super().__init__("Circle", color)
        self.radius = radius
    
    def area(self):
        return math.pi * self.radius ** 2
    
    def perimeter(self):
        return 2 * math.pi * self.radius

class Rectangle(TwoDimensionalShape):
    def __init__(self, width, height, color="Blue"):
        super().__init__("Rectangle", color)
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

class Sphere(ThreeDimensionalShape):
    def __init__(self, radius, color="Green"):
        super().__init__("Sphere", color)
        self.radius = radius
    
    def area(self):
        return 4 * math.pi * self.radius ** 2
    
    def perimeter(self):
        return 2 * math.pi * self.radius  # Actually circumference
    
    def volume(self):
        return (4/3) * math.pi * self.radius ** 3

# Using the shape hierarchy
shapes = [
    Circle(5),
    Rectangle(4, 6),
    Sphere(3)
]

for shape in shapes:
    shape.display_info()
    print("-" * 30)
```

---

## Best Practices

### 1. Follow the Single Responsibility Principle
Each class should have only one reason to change.

```python
# Good: Separate responsibilities
class User:
    def __init__(self, username, email):
        self.username = username
        self.email = email

class UserRepository:
    def save(self, user):
        # Save user to database
        pass
    
    def find_by_id(self, user_id):
        # Find user by ID
        pass

class UserService:
    def __init__(self, repository):
        self.repository = repository
    
    def create_user(self, username, email):
        user = User(username, email)
        self.repository.save(user)
        return user
```

### 2. Use Composition Over Inheritance
```python
# Prefer composition
class Engine:
    def start(self):
        print("Engine started")

class Wheels:
    def rotate(self):
        print("Wheels rotating")

class Car:
    def __init__(self):
        self.engine = Engine()
        self.wheels = Wheels()
    
    def drive(self):
        self.engine.start()
        self.wheels.rotate()
        print("Car is driving")
```

### 3. Apply the Open/Closed Principle
Classes should be open for extension but closed for modification.

```python
# Good: Extensible design
class PaymentProcessor:
    def process_payment(self, amount, method):
        if method == "credit_card":
            return self.process_credit_card(amount)
        elif method == "paypal":
            return self.process_paypal(amount)
        # Adding new payment methods doesn't require modifying this class
    
    def process_credit_card(self, amount):
        print(f"Processing credit card payment: ${amount}")
    
    def process_paypal(self, amount):
        print(f"Processing PayPal payment: ${amount}")
```

### 4. Implement Proper Error Handling
```python
class BankAccount:
    def __init__(self, initial_balance=0):
        if initial_balance < 0:
            raise ValueError("Initial balance cannot be negative")
        self.__balance = initial_balance
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.__balance += amount
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient funds")
        self.__balance -= amount
    
    @property
    def balance(self):
        return self.__balance
```

---

## Summary

### Inheritance
- Enables code reuse through class hierarchies
- Supports single, multiple, multilevel, and hierarchical inheritance
- Uses `super()` to call parent class methods
- Follows Method Resolution Order (MRO) for multiple inheritance

### Polymorphism
- Allows objects of different types to be treated uniformly
- Achieved through method overriding and duck typing
- Supports operator overloading for custom behavior
- Enables flexible and extensible code design

### Encapsulation
- Bundles data and methods together
- Controls access through public, protected, and private attributes
- Uses property decorators for managed attributes
- Protects object integrity through controlled access

### Abstraction
- Hides complex implementation details
- Uses abstract classes and methods to define contracts
- Focuses on what an object does rather than how
- Promotes loose coupling and high cohesion

These four principles work together to create robust, maintainable, and extensible object-oriented software systems. Understanding and applying them correctly is essential for effective OOP programming.