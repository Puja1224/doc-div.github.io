---
title: Setting Up Python
description: A detailed guide to installing Python and writing your first program, perfect for beginners.
---

# Setting Up Python

This guide provides step-by-step instructions for setting up Python on your computer and writing your first simple program. It's designed for beginners and includes troubleshooting tips.

## Setting Up Python

### 1. Download Python
- Visit the official website: python.org
- Click Downloads and select the latest stable version (e.g., Python 3.12.x) for your operating system (Windows, macOS, or Linux)
- It's free and open-source. Download the installer file.

### 2. Install Python
- **On Windows**: Check the box for Add Python to PATH (this lets you run Python from any command prompt). Choose Install Now or customize if needed
- **On macOS**: Follow the installer prompts; it might require admin password
- **On Linux**: Use your package manager (e.g., sudo apt install python3 on Ubuntu) or download and compile from source if preferred
- Installation takes a few minutes. Restart your computer if prompted.

### 3. Verify Installation
- **On Windows**: Open Command Prompt
- **On macOS/Linux**: Open Terminal
- Type `python --version` or `python3 --version` and press Enter
- It should display the version number (e.g., Python 3.12.0)
- If it doesn't work, check your PATH settings or reinstall.

### 4. Optional Tools for Easier Coding
- **IDLE**: Comes with Python; it's a basic editor and interpreter
- **VS Code**: Free from code.visualstudio.com; install Python extension for features like debugging
- **PyCharm**: More advanced IDE (free Community edition available)
- These help with writing, running, and debugging code.

### 5. Troubleshooting
- If python command isn't recognized, add Python to your system's PATH manually
- Ensure no older versions conflict (uninstall if needed)

## Writing Your First Program

### 1. Choose an Editor
- Use a simple text editor like Notepad (Windows), TextEdit (macOS), or nano (Linux)
- Or an IDE like IDLE, VS Code, or PyCharm for syntax highlighting and error checking

### 2. Write the Code
- Open your editor and create a new file
- Type this basic program (it's a Hello, World! example):
```python
print("Hello, World!")
```
- `print()` is a built-in function that outputs text to the screen
- The text inside quotes is a string (a sequence of characters)

### 3. Save the File
- Save it as `hello.py` (the .py extension tells the system it's a Python file)
- Choose a location you can easily find, like your Desktop or a Python Projects folder

### 4. Run the Program
- **On Windows**: Open Command Prompt
- **On macOS/Linux**: Open Terminal
- Navigate to the file's folder using `cd` command (e.g., `cd Desktop`)
- Type `python hello.py` (or `python3 hello.py` on some systems) and press Enter
- **Output**: You'll see "Hello, World!" printed in the terminal

### 5. Expand and Experiment
- Add variables: `name = "Your Name"` then `print("Hello, " + name + "!")`
- Try math: `print(2 + 3)` outputs 5
- Fix errors: Python gives clear messages (e.g., syntax errors for missing quotes)
- Practice: Modify the code, save, and rerun. Learn from mistakes

### 6. Next Steps
- Explore Python docs at docs.python.org for more functions
- Install libraries via `pip install <library>` (e.g., `pip install requests` for web stuff)
- Join communities like Stack Overflow or Reddit's r/learnpython for help

This setup takes 10-30 minutes. Python is beginner-friendly and runs on almost any device. If you hit issues, search error messages online.