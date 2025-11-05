---
title: Introduction to Java
---

# ☕ Introduction to Java

Java is a powerful, high-level, class-based, object-oriented programming language designed to have as few implementation dependencies as possible.  
Developed by **James Gosling** at **Sun Microsystems** and released in **1995**, Java has been a cornerstone of enterprise and mobile development for decades.

---

## 💡 What Makes Java Unique?

Java's enduring popularity is rooted in its core design principles:

### 🌍 Platform Independence — *"Write Once, Run Anywhere"*
This is Java's most famous feature.  
Java code is compiled into an intermediate form called **bytecode**.  
This bytecode can then be executed on any machine that has a **Java Virtual Machine (JVM)** installed, regardless of the operating system (Windows, macOS, Linux, etc.).

### 🧱 Object-Oriented Programming (OOP)
Java is purely object-oriented, meaning it models real-world entities into software objects.  
This makes the code **modular**, **reusable**, and **easier to maintain**.

### 🔒 Security
The JVM is designed to keep compiled code from causing damage to the system.  
It uses a **security manager** that governs access to resources, enhancing safety.

### 🛠️ Robustness
Java is a **strongly typed** language, meaning type checking is done at compile time.  
It also manages memory automatically through a **Garbage Collector**, reducing common programming errors.

---

## 🖥️ The "Hello, World!" Example

Every Java program starts with a class definition.  
Here is the classic **"Hello, World!"** program:

```java
public class HelloWorld {
    public static void main(String[] args) {
        // System.out.println is used to display output to the console
        System.out.println("Hello, World!");
    }
}
