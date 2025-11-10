---
id: file-handling-reading-and-writing-files
title: File Handling — Reading and Writing Files in Python
---

# File Handling — Reading and Writing Files in Python

File handling is a crucial aspect of programming that allows you to read from and write to files on your system. Python provides powerful and intuitive tools for working with various types of files.

---

## What is File Handling?

File handling involves operations like:
- **Opening** files for reading or writing
- **Reading** data from files
- **Writing** data to files
- **Closing** files to free up system resources
- **Managing** file positions and navigation

Python treats files as sequences of bytes, which can be opened in different modes depending on your needs.

---

## Opening Files

### Basic File Opening

```python
# Open a file for reading (default mode)
file = open("example.txt")  # Opens in 'r' mode
content = file.read()
file.close()

# Specify encoding explicitly
file = open("example.txt", encoding="utf-8")
content = file.read()
file.close()

# Open with different modes
file = open("example.txt", "r")    # Read mode (default)
file = open("example.txt", "w")    # Write mode (overwrites existing content)
file = open("example.txt", "a")    # Append mode (adds to end)
file = open("example.txt", "r+")   # Read and write mode
```

### File Modes Overview

| Mode | Description | File Position | Creates if Missing | Truncates if Exists |
|------|-------------|---------------|-------------------|-------------------|
| `'r'` | Read only | Beginning | ❌ | ❌ |
| `'w'` | Write only | Beginning | ✅ | ✅ |
| `'a'` | Append only | End | ✅ | ❌ |
| `'r+'` | Read and write | Beginning | ❌ | ❌ |
| `'w+'` | Read and write | Beginning | ✅ | ✅ |
| `'a+'` | Read and write | End | ✅ | ❌ |
| `'rb'` | Binary read | Beginning | ❌ | ❌ |
| `'wb'` | Binary write | Beginning | ✅ | ✅ |

### Binary Mode

```python
# Read binary file
with open("image.jpg", "rb") as file:
    image_data = file.read()

# Write binary file
with open("copy.jpg", "wb") as file:
    file.write(image_data)

# Copy file
with open("source.jpg", "rb") as source:
    with open("destination.jpg", "wb") as dest:
        dest.write(source.read())
```

---

## Reading Files

### Reading Entire File

```python
# Read entire file
with open("example.txt", "r") as file:
    content = file.read()
    print(content)

# Read entire file as list of lines
with open("example.txt", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line.strip())
```

### Reading Line by Line

```python
# Method 1: Using readline()
with open("example.txt", "r") as file:
    while True:
        line = file.readline()
        if not line:  # Empty string means end of file
            break
        print(line.strip())

# Method 2: Using for loop (most common)
with open("example.txt", "r") as file:
    for line in file:
        print(line.strip())  # strip() removes newline character

# Method 3: Using enumerate for line numbers
with open("example.txt", "r") as file:
    for line_num, line in enumerate(file, 1):
        print(f"Line {line_num}: {line.strip()}")
```

### Reading Specific Amounts

```python
# Read specific number of characters
with open("example.txt", "r") as file:
    # Read first 100 characters
    content = file.read(100)
    print(content)
    
    # Read next 50 characters
    next_part = file.read(50)
    print(next_part)

# Read specific number of lines
with open("example.txt", "r") as file:
    # Read first 5 lines
    lines = []
    for i in range(5):
        line = file.readline()
        if not line:
            break
        lines.append(line.strip())
    print(lines)
```

### Reading Large Files Efficiently

```python
# Process large file line by line (memory efficient)
def process_large_file(filename):
    with open(filename, "r") as file:
        for line_num, line in enumerate(file, 1):
            # Process each line without loading entire file
            if line_num % 1000 == 0:
                print(f"Processed {line_num} lines")
            
            # Your processing logic here
            processed_line = line.strip().upper()
            
            # Optionally write to output file
            # with open("output.txt", "a") as output:
            #     output.write(processed_line + "\n")

# Example usage
process_large_file("large_data.txt")
```

---

## Writing Files

### Basic Writing

```python
# Write text to file (overwrites existing content)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a new line.")
    file.write("No automatic newline added.")

# Write list of lines
lines = ["Line 1", "Line 2", "Line 3"]
with open("output.txt", "w") as file:
    for line in lines:
        file.write(line + "\n")

# Using writelines()
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("output.txt", "w") as file:
    file.writelines(lines)
```

### Appending to Files

```python
# Add to end of existing file
with open("existing_file.txt", "a") as file:
    file.write("This line is appended.\n")
    file.write("Another appended line.\n")

# Create if doesn't exist, append if exists
# 'a' mode automatically creates the file
with open("new_or_existing.txt", "a") as file:
    file.write("This will be added to the file.\n")
```

### Writing with Format

```python
# Formatted writing
data = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

# Method 1: Using format strings
with open("formatted.txt", "w") as file:
    file.write(f"Name: {data['name']}\n")
    file.write(f"Age: {data['age']}\n")
    file.write(f"City: {data['city']}\n")

# Method 2: Using format() method
with open("formatted.txt", "w") as file:
    file.write("Name: {name}\n".format(name=data['name']))
    file.write("Age: {age}\n".format(age=data['age']))
    file.write("City: {city}\n".format(city=data['city']))
```

### Conditional Writing

```python
# Only write if data has changed
def save_data(data, filename="data.txt"):
    try:
        with open(filename, "r") as file:
            existing_data = file.read()
    except FileNotFoundError:
        existing_data = ""
    
    new_data = str(data)
    
    if existing_data != new_data:
        with open(filename, "w") as file:
            file.write(new_data)
        print(f"Data saved to {filename}")
    else:
        print("No changes to save")
```

---

## Context Managers (with Statement)

### Why Use Context Managers?

The `with` statement automatically handles file closing, even if exceptions occur:

```python
# Without context manager (risky)
file = open("example.txt", "r")
content = file.read()
file.close()  # Must remember to close

# With context manager (safe)
with open("example.txt", "r") as file:
    content = file.read()
    # File automatically closed when block exits
```

### Multiple Files

```python
# Open multiple files simultaneously
with open("input.txt", "r") as input_file, open("output.txt", "w") as output_file:
    for line in input_file:
        # Process each line
        processed_line = line.upper()
        output_file.write(processed_line)

# Nested context managers
with open("source.txt", "r") as source:
    with open("destination.txt", "w") as dest:
        dest.write(source.read())
```

### Custom Context Managers

```python
class FileHandler:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()
        return False  # Don't suppress exceptions

# Usage
with FileHandler("example.txt", "w") as f:
    f.file.write("Hello from custom context manager!")
```

---

## Working with CSV Files

### Reading CSV Files

```python
import csv

# Read CSV file
with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Read CSV with custom delimiter
with open("data.tsv", "r") as file:
    reader = csv.reader(file, delimiter='\t')
    for row in reader:
        print(row)

# Read CSV as dictionary
with open("employees.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(f"Name: {row['name']}, Age: {row['age']}")
```

### Writing CSV Files

```python
import csv

# Write CSV file
data = [
    ["Name", "Age", "City"],
    ["Alice", 30, "New York"],
    ["Bob", 25, "London"],
    ["Charlie", 35, "Paris"]
]

with open("output.csv", "w", newline='') as file:
    writer = csv.writer(file)
    writer.writerows(data)

# Write CSV with dictionary
data_dict = [
    {"name": "Alice", "age": 30, "city": "New York"},
    {"name": "Bob", "age": 25, "city": "London"},
    {"name": "Charlie", "age": 35, "city": "Paris"}
]

fieldnames = ["name", "age", "city"]
with open("output_dict.csv", "w", newline='') as file:
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(data_dict)
```

### Working with Large CSV Files

```python
import csv

# Process large CSV efficiently
def process_large_csv(input_filename, output_filename):
    with open(input_filename, "r") as input_file, \
         open(output_filename, "w", newline='') as output_file:
        
        reader = csv.DictReader(input_file)
        fieldnames = reader.fieldnames
        
        # Add new field for processing
        if "processed" not in fieldnames:
            fieldnames.append("processed")
        
        writer = csv.DictWriter(output_file, fieldnames=fieldnames)
        writer.writeheader()
        
        for row in reader:
            # Process each row
            row["processed"] = "Yes"
            writer.writerow(row)
```

---

## Working with JSON Files

### Reading JSON Files

```python
import json

# Read JSON file
with open("data.json", "r") as file:
    data = json.load(file)
    print(data)

# Read JSON with custom encoding
with open("data.json", "r", encoding="utf-8") as file:
    data = json.load(file)

# Read JSON line by line (JSONL format)
with open("data.jsonl", "r") as file:
    for line in file:
        data = json.loads(line)
        print(data)
```

### Writing JSON Files

```python
import json

# Write JSON file
data = {
    "name": "Alice",
    "age": 30,
    "city": "New York",
    "skills": ["Python", "JavaScript", "SQL"],
    "active": True
}

with open("output.json", "w") as file:
    json.dump(data, file, indent=4)  # indent for pretty formatting

# Write JSON with custom sorting
with open("output_sorted.json", "w") as file:
    json.dump(data, file, indent=4, sort_keys=True)

# Write JSONL (JSON Lines) format
data_list = [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"},
    {"id": 3, "name": "Charlie"}
]

with open("output.jsonl", "w") as file:
    for item in data_list:
        json.dump(item, file)
        file.write("\n")
```

### JSON Configuration Management

```python
import json
import os

class ConfigManager:
    def __init__(self, config_file="config.json"):
        self.config_file = config_file
        self.config = self.load_config()
    
    def load_config(self):
        """Load configuration from JSON file"""
        try:
            with open(self.config_file, "r") as file:
                return json.load(file)
        except FileNotFoundError:
            return self.get_default_config()
    
    def save_config(self):
        """Save configuration to JSON file"""
        with open(self.config_file, "w") as file:
            json.dump(self.config, file, indent=2)
    
    def get_default_config(self):
        """Return default configuration"""
        return {
            "database": {
                "host": "localhost",
                "port": 5432,
                "name": "default_db"
            },
            "logging": {
                "level": "INFO",
                "file": "app.log"
            }
        }
    
    def get(self, key, default=None):
        """Get configuration value by key path"""
        keys = key.split(".")
        value = self.config
        for k in keys:
            if isinstance(value, dict) and k in value:
                value = value[k]
            else:
                return default
        return value
    
    def set(self, key, value):
        """Set configuration value by key path"""
        keys = key.split(".")
        config = self.config
        for k in keys[:-1]:
            if k not in config:
                config[k] = {}
            config = config[k]
        config[keys[-1]] = value

# Usage
config = ConfigManager()
host = config.get("database.host")
config.set("database.port", 3306)
config.save_config()
```

---

## File Navigation and Positioning

### File Position Methods

```python
# Get current file position
with open("example.txt", "r") as file:
    print(f"Initial position: {file.tell()}")
    
    content = file.read(10)
    print(f"After reading 10 chars: {file.tell()}")
    print(f"Content: {content}")
    
    # Move to beginning
    file.seek(0)
    print(f"After seek(0): {file.tell()}")
    
    # Move to specific position
    file.seek(5)
    print(f"After seek(5): {file.tell()}")
```

### Random Access Reading

```python
# Read specific parts of a file
with open("large_file.txt", "r") as file:
    # Read first 100 characters
    file.seek(0)
    first_part = file.read(100)
    
    # Skip to middle and read 50 characters
    file.seek(1000)
    middle_part = file.read(50)
    
    # Read last 100 characters
    file.seek(-100, 2)  # Move 100 bytes from end
    last_part = file.read(100)
```

### Line-Based Random Access

```python
def read_specific_line(filename, line_number):
    """Read a specific line from file"""
    with open(filename, "r") as file:
        for current_line, line in enumerate(file, 1):
            if current_line == line_number:
                return line.strip()
    return None

# Read multiple specific lines
def read_multiple_lines(filename, line_numbers):
    """Read multiple specific lines from file"""
    lines = {}
    with open(filename, "r") as file:
        for current_line, line in enumerate(file, 1):
            if current_line in line_numbers:
                lines[current_line] = line.strip()
    return lines

# Usage
line5 = read_specific_line("example.txt", 5)
lines_2_4_7 = read_multiple_lines("example.txt", [2, 4, 7])
```

---

## Error Handling

### FileNotFoundError Handling

```python
# Basic error handling
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
    print(content)
except FileNotFoundError:
    print("File not found. Creating a new file.")
    with open("nonexistent.txt", "w") as file:
        file.write("New file created.")
except IOError as e:
    print(f"IO Error occurred: {e}")
except Exception as e:
    print(f"An error occurred: {e}")
```

### Robust File Operations

```python
import os
import shutil

def safe_file_operation(source_path, dest_path):
    """Safely copy file with error handling"""
    try:
        # Check if source file exists
        if not os.path.exists(source_path):
            raise FileNotFoundError(f"Source file '{source_path}' not found")
        
        # Create destination directory if it doesn't exist
        dest_dir = os.path.dirname(dest_path)
        if dest_dir and not os.path.exists(dest_dir):
            os.makedirs(dest_dir)
        
        # Copy file
        shutil.copy2(source_path, dest_path)
        print(f"File successfully copied from {source_path} to {dest_path}")
        
    except FileNotFoundError as e:
        print(f"Error: {e}")
    except PermissionError:
        print("Error: Permission denied")
    except Exception as e:
        print(f"Unexpected error: {e}")

# Usage
safe_file_operation("source.txt", "backup/source.txt")
```

### File Locking

```python
import fcntl  # Unix/Linux systems
import msvcrt  # Windows systems

def lock_file(file_handle):
    """Lock file for exclusive access"""
    try:
        # Unix/Linux
        fcntl.flock(file_handle.fileno(), fcntl.LOCK_EX)
        return True
    except (AttributeError, OSError):
        try:
            # Windows
            msvcrt.locking(file_handle.fileno(), msvcrt.LK_NBLCK, 1)
            return True
        except (AttributeError, OSError):
            return False

def unlock_file(file_handle):
    """Unlock file"""
    try:
        # Unix/Linux
        fcntl.flock(file_handle.fileno(), fcntl.LOCK_UN)
        return True
    except (AttributeError, OSError):
        try:
            # Windows
            msvcrt.locking(file_handle.fileno(), msvcrt.LK_UNLCK, 1)
            return True
        except (AttributeError, OSError):
            return False
```

---

## File Management Operations

### File Information

```python
import os
import datetime

# Get file information
def get_file_info(filename):
    if os.path.exists(filename):
        stat = os.stat(filename)
        info = {
            "size": stat.st_size,
            "modified": datetime.datetime.fromtimestamp(stat.st_mtime),
            "accessed": datetime.datetime.fromtimestamp(stat.st_atime),
            "created": datetime.datetime.fromtimestamp(stat.st_ctime)
        }
        return info
    return None

# Check file properties
def check_file_properties(filename):
    if not os.path.exists(filename):
        return "File does not exist"
    
    return {
        "exists": os.path.exists(filename),
        "is_file": os.path.isfile(filename),
        "is_dir": os.path.isdir(filename),
        "size": os.path.getsize(filename),
        "extension": os.path.splitext(filename)[1],
        "basename": os.path.basename(filename),
        "directory": os.path.dirname(filename)
    }
```

### File Operations

```python
import os
import shutil

# Rename file
def rename_file(old_name, new_name):
    try:
        os.rename(old_name, new_name)
        print(f"File renamed from {old_name} to {new_name}")
        return True
    except FileNotFoundError:
        print(f"File {old_name} not found")
        return False
    except Exception as e:
        print(f"Error renaming file: {e}")
        return False

# Copy file
def copy_file(source, destination):
    try:
        shutil.copy2(source, destination)  # Preserves metadata
        print(f"File copied from {source} to {destination}")
        return True
    except FileNotFoundError:
        print(f"Source file {source} not found")
        return False
    except Exception as e:
        print(f"Error copying file: {e}")
        return False

# Move file
def move_file(source, destination):
    try:
        shutil.move(source, destination)
        print(f"File moved from {source} to {destination}")
        return True
    except FileNotFoundError:
        print(f"Source file {source} not found")
        return False
    except Exception as e:
        print(f"Error moving file: {e}")
        return False

# Delete file
def delete_file(filename):
    try:
        os.remove(filename)
        print(f"File {filename} deleted")
        return True
    except FileNotFoundError:
        print(f"File {filename} not found")
        return False
    except Exception as e:
        print(f"Error deleting file: {e}")
        return False
```

### Directory Operations

```python
import os
import glob

# List files in directory
def list_files(directory, pattern="*"):
    """List files matching pattern in directory"""
    search_path = os.path.join(directory, pattern)
    return glob.glob(search_path)

# Find files recursively
def find_files(directory, pattern):
    """Find files matching pattern recursively"""
    matches = []
    for root, dirs, files in os.walk(directory):
        for file in files:
            if pattern in file:
                matches.append(os.path.join(root, file))
    return matches

# Create directory
def create_directory(path):
    try:
        os.makedirs(path, exist_ok=True)
        print(f"Directory {path} created")
        return True
    except Exception as e:
        print(f"Error creating directory: {e}")
        return False

# Clean directory
def clean_directory(directory, dry_run=False):
    """Remove all files in directory"""
    for filename in os.listdir(directory):
        file_path = os.path.join(directory, filename)
        try:
            if os.path.isfile(file_path):
                if dry_run:
                    print(f"[DRY RUN] Would delete: {file_path}")
                else:
                    os.remove(file_path)
                    print(f"Deleted: {file_path}")
        except Exception as e:
            print(f"Error deleting {file_path}: {e}")
```

---

## Best Practices

### File Handling Best Practices

```python
# 1. Always use context managers
def good_practice():
    # Good: Uses context manager
    with open("file.txt", "r") as file:
        content = file.read()
    
    # Bad: Manual closing (risky)
    # file = open("file.txt", "r")
    # content = file.read()
    # file.close()  # What if exception occurs?
    return content

# 2. Specify encoding explicitly
def explicit_encoding():
    # Good: Explicit encoding
    with open("file.txt", "r", encoding="utf-8") as file:
        return file.read()
    
    # Bad: Default encoding (system-dependent)
    # with open("file.txt", "r") as file:
    #     return file.read()

# 3. Handle different file sizes appropriately
def read_efficiently(filename, file_size):
    if file_size < 1024 * 1024:  # Less than 1MB
        # Read entire file
        with open(filename, "r", encoding="utf-8") as file:
            return file.read()
    else:
        # Read line by line
        lines = []
        with open(filename, "r", encoding="utf-8") as file:
            for line in file:
                lines.append(line)
        return lines
```

### Memory-Efficient File Processing

```python
# Process large files without loading entirely into memory
def process_large_log_file(log_filename, error_filename):
    """Process large log file and extract errors"""
    error_count = 0
    
    with open(log_filename, "r", encoding="utf-8") as log_file, \
         open(error_filename, "w", encoding="utf-8") as error_file:
        
        for line_num, line in enumerate(log_file, 1):
            if "ERROR" in line or "CRITICAL" in line:
                error_count += 1
                # Write error line with line number
                error_file.write(f"Line {line_num}: {line}")
            
            # Progress indicator for large files
            if line_num % 10000 == 0:
                print(f"Processed {line_num} lines, found {error_count} errors")
    
    print(f"Processing complete. Found {error_count} errors.")
    return error_count

# Streaming file processing
def stream_process_large_file(input_filename, output_filename):
    """Process file data without loading into memory"""
    def process_line(line):
        # Your processing logic here
        return line.upper().strip()
    
    with open(input_filename, "r") as input_file, \
         open(output_filename, "w") as output_file:
        
        for line in input_file:
            processed_line = process_line(line)
            output_file.write(processed_line + "\n")
```

### File Validation and Security

```python
import os
import tempfile
import hashlib

def validate_file_integrity(filename, expected_hash=None):
    """Validate file integrity using MD5 hash"""
    hasher = hashlib.md5()
    
    with open(filename, "rb") as file:
        # Read file in chunks to handle large files
        for chunk in iter(lambda: file.read(4096), b""):
            hasher.update(chunk)
    
    actual_hash = hasher.hexdigest()
    
    if expected_hash:
        return actual_hash == expected_hash, actual_hash
    return actual_hash

def safe_file_write(data, filename, backup=True):
    """Safely write data to file with backup"""
    # Create backup if file exists
    if os.path.exists(filename) and backup:
        backup_filename = f"{filename}.backup"
        shutil.copy2(filename, backup_filename)
        print(f"Backup created: {backup_filename}")
    
    # Write to temporary file first
    temp_filename = f"{filename}.tmp"
    with open(temp_filename, "w", encoding="utf-8") as temp_file:
        if isinstance(data, str):
            temp_file.write(data)
        elif isinstance(data, (list, tuple)):
            for item in data:
                temp_file.write(str(item) + "\n")
    
    # Atomic move
    shutil.move(temp_filename, filename)
    print(f"File written successfully: {filename}")
```

---

## Practical Examples

### Log File Processing

```python
import re
from datetime import datetime

def parse_log_file(log_filename, output_filename="parsed_log.txt"):
    """Parse log file and extract structured information"""
    log_pattern = re.compile(
        r'(\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}) \[(\w+)\] (.+)'
    )
    
    parsed_data = []
    
    with open(log_filename, "r", encoding="utf-8") as log_file:
        for line_num, line in enumerate(log_file, 1):
            match = log_pattern.match(line.strip())
            if match:
                timestamp_str, level, message = match.groups()
                try:
                    timestamp = datetime.strptime(timestamp_str, "%Y-%m-%d %H:%M:%S")
                    parsed_data.append({
                        "line": line_num,
                        "timestamp": timestamp,
                        "level": level,
                        "message": message
                    })
                except ValueError:
                    print(f"Invalid timestamp format at line {line_num}")
    
    # Write parsed data
    with open(output_filename, "w", encoding="utf-8") as output_file:
        for entry in parsed_data:
            output_file.write(
                f"{entry['timestamp']} [{entry['level']}] {entry['message']} (Line {entry['line']})\n"
            )
    
    return parsed_data

# Usage
logs = parse_log_file("app.log")
error_logs = [log for log in logs if log["level"] in ["ERROR", "CRITICAL"]]
print(f"Found {len(error_logs)} error logs")
```

### Configuration File Manager

```python
import json
import os
from configparser import ConfigParser

class ConfigFileManager:
    """Manager for different configuration file formats"""
    
    @staticmethod
    def read_json(filename):
        """Read JSON configuration file"""
        try:
            with open(filename, "r", encoding="utf-8") as file:
                return json.load(file)
        except FileNotFoundError:
            return {}
        except json.JSONDecodeError as e:
            print(f"Invalid JSON in {filename}: {e}")
            return {}
    
    @staticmethod
    def write_json(data, filename, pretty=True):
        """Write JSON configuration file"""
        with open(filename, "w", encoding="utf-8") as file:
            indent = 2 if pretty else None
            json.dump(data, file, indent=indent, ensure_ascii=False)
    
    @staticmethod
    def read_ini(filename):
        """Read INI configuration file"""
        config = ConfigParser()
        try:
            config.read(filename, encoding="utf-8")
            return config
        except FileNotFoundError:
            return ConfigParser()
        except Exception as e:
            print(f"Error reading INI file {filename}: {e}")
            return ConfigParser()
    
    @staticmethod
    def write_ini(config, filename):
        """Write INI configuration file"""
        with open(filename, "w", encoding="utf-8") as file:
            config.write(file)

# Usage
config_manager = ConfigFileManager()

# JSON configuration
app_config = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp"
    },
    "logging": {
        "level": "INFO",
        "file": "app.log"
    }
}
config_manager.write_json(app_config, "config.json")
loaded_config = config_manager.read_json("config.json")
```

### Data Backup System

```python
import os
import shutil
import tarfile
import zipfile
from datetime import datetime

class BackupSystem:
    """System for creating file backups"""
    
    def __init__(self, backup_dir="backups"):
        self.backup_dir = backup_dir
        os.makedirs(backup_dir, exist_ok=True)
    
    def create_file_backup(self, source_file):
        """Create timestamped backup of a file"""
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        filename = os.path.basename(source_file)
        backup_name = f"{filename}.{timestamp}.backup"
        backup_path = os.path.join(self.backup_dir, backup_name)
        
        shutil.copy2(source_file, backup_path)
        print(f"Backup created: {backup_path}")
        return backup_path
    
    def create_directory_backup(self, source_dir, compression="zip"):
        """Create backup of entire directory"""
        timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
        dirname = os.path.basename(source_dir)
        
        if compression == "zip":
            backup_name = f"{dirname}.{timestamp}.zip"
            backup_path = os.path.join(self.backup_dir, backup_name)
            
            with zipfile.ZipFile(backup_path, "w", zipfile.ZIP_DEFLATED) as zipf:
                for root, dirs, files in os.walk(source_dir):
                    for file in files:
                        file_path = os.path.join(root, file)
                        arcname = os.path.relpath(file_path, source_dir)
                        zipf.write(file_path, arcname)
        
        elif compression == "tar":
            backup_name = f"{dirname}.{timestamp}.tar.gz"
            backup_path = os.path.join(self.backup_dir, backup_name)
            
            with tarfile.open(backup_path, "w:gz") as tar:
                tar.add(source_dir, arcname=dirname)
        
        print(f"Directory backup created: {backup_path}")
        return backup_path
    
    def list_backups(self):
        """List all backups in backup directory"""
        backups = []
        for filename in os.listdir(self.backup_dir):
            backup_path = os.path.join(self.backup_dir, filename)
            if os.path.isfile(backup_path):
                stat = os.stat(backup_path)
                backups.append({
                    "filename": filename,
                    "path": backup_path,
                    "size": stat.st_size,
                    "created": datetime.fromtimestamp(stat.st_ctime)
                })
        return sorted(backups, key=lambda x: x["created"], reverse=True)

# Usage
backup_system = BackupSystem()

# Backup individual file
backup_system.create_file_backup("important_document.txt")

# Backup directory with compression
backup_system.create_directory_backup("project_folder", compression="zip")

# List all backups
all_backups = backup_system.list_backups()
for backup in all_backups:
    print(f"{backup['filename']}: {backup['size']} bytes, created {backup['created']}")
```

---

## Summary

- **File Operations**: Open, read, write, close files using Python's built-in functions
- **Context Managers**: Use `with` statement for safe file handling
- **File Modes**: Understand different modes (read, write, append, binary) and their behavior
- **Reading Methods**: Various ways to read files (entire, line by line, chunks, specific amounts)
- **Writing Methods**: Write text, lists, and formatted data to files
- **Specialized Formats**: Work with CSV, JSON, and other structured file formats
- **Error Handling**: Handle file-related exceptions gracefully
- **File Management**: Rename, copy, move, delete files and directories
- **Performance**: Handle large files efficiently with streaming and chunking
- **Best Practices**: Use context managers, explicit encoding, and proper error handling

File handling is essential for data persistence, configuration management, and data processing in Python applications.