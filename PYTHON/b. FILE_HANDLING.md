Sure! Let's go step by step and cover everything about **File Handling** and **OS Interaction** in Python in a simple and easy-to-understand way.

---

# **1. File Handling in Python**  

**File handling** is used to **read, write, modify, and delete files** using Python. Python provides built-in functions to work with files.  

## **1.1 Opening and Closing Files**  
To work with a file, you must first **open** it.  
Syntax:  
```python
file = open("filename.txt", "mode")  
```
When done, **close** the file:  
```python
file.close()
```

✅ **Modes to Open a File**  

| Mode  | Description |
|--------|------------|
| `"r"`  | Read mode (default) - Opens file for reading, error if file doesn’t exist |
| `"w"`  | Write mode - Creates a new file or overwrites if it exists |
| `"a"`  | Append mode - Adds data to the end of a file without deleting existing content |
| `"x"`  | Create mode - Creates a new file, error if it already exists |
| `"r+"` | Read & Write mode |

---

## **1.2 Reading a File**  
✅ **Read the entire file content**  
```python
file = open("sample.txt", "r")  
content = file.read()  
print(content)  
file.close()
```

✅ **Read first N characters**  
```python
file = open("sample.txt", "r")  
content = file.read(10)  # Reads first 10 characters  
print(content)  
file.close()
```

✅ **Read line by line**  
```python
file = open("sample.txt", "r")  
for line in file:
    print(line.strip())  # Removes extra newline characters
file.close()
```

✅ **Read all lines as a list**  
```python
file = open("sample.txt", "r")  
lines = file.readlines()  # Reads all lines as a list  
print(lines)  
file.close()
```

---

## **1.3 Writing to a File**  
✅ **Write content (overwrites existing file)**  
```python
file = open("sample.txt", "w")  
file.write("Hello, Python!\n")  
file.write("This is a new file.")  
file.close()
```
✔ If `sample.txt` exists, it **overwrites** the content.  
✔ If it **does not exist**, it creates a new file.  

✅ **Append content (without overwriting)**  
```python
file = open("sample.txt", "a")  
file.write("\nThis is an added line.")  
file.close()
```
✔ Adds text at the **end** of the file.  

---

## **1.4 Using `with open()` (Best Practice)**  
Using `with open()` automatically closes the file.  

✅ **Reading a file**  
```python
with open("sample.txt", "r") as file:
    content = file.read()
    print(content)  # File closes automatically after this block
```

✅ **Writing to a file**  
```python
with open("sample.txt", "w") as file:
    file.write("Hello from Python!")
```

✅ **Appending to a file**  
```python
with open("sample.txt", "a") as file:
    file.write("\nAppending another line.")
```

---

## **1.5 File Handling Example (Combining Read & Write)**  
This script reads `sample.txt`, counts the number of lines, and writes the count to a new file.  
```python
with open("sample.txt", "r") as file:
    lines = file.readlines()
    print(f"Total lines: {len(lines)}")

with open("count.txt", "w") as file:
    file.write(f"Total lines in sample.txt: {len(lines)}")
```

---

## **1.6 Deleting a File**  
✅ **Delete a file using `os` module**  
```python
import os
os.remove("sample.txt")
```

✅ **Check if file exists before deleting**  
```python
if os.path.exists("sample.txt"):
    os.remove("sample.txt")
else:
    print("File does not exist!")
```

✅ **Delete an empty folder**  
```python
os.rmdir("empty_folder")
```

✅ **Delete a non-empty folder**  
```python
import shutil
shutil.rmtree("folder_name")
```

---

# **2. OS Interaction in Python**  
Python’s **`os` module** helps interact with the operating system (Windows/Linux/Mac).  

## **2.1 Working with Directories**  
✅ **Check current directory**  
```python
import os
print(os.getcwd())  # Prints current working directory
```

✅ **Change directory**  
```python
os.chdir("/home/user/documents")  # Change directory (Linux/Mac)
os.chdir("C:\\Users\\Ankita\\Documents")  # Change directory (Windows)
```

✅ **List files in a directory**  
```python
print(os.listdir())  # List files in current directory
print(os.listdir("/home/user/"))  # List files in a specific directory
```

✅ **Create a new directory**  
```python
os.mkdir("new_folder")  # Creates a folder in the current directory
```

✅ **Create multiple directories**  
```python
os.makedirs("parent/child/grandchild")  # Creates all folders if they don't exist
```

✅ **Rename a file or folder**  
```python
os.rename("old_name.txt", "new_name.txt")  # Rename file
os.rename("old_folder", "new_folder")  # Rename folder
```

✅ **Check if a file or folder exists**  
```python
if os.path.exists("sample.txt"):
    print("File exists")
else:
    print("File does not exist")
```

✅ **Get file details (size, modification time, etc.)**  
```python
file_info = os.stat("sample.txt")
print(file_info.st_size)  # File size in bytes
print(file_info.st_mtime)  # Last modification time
```

---

## **2.2 Running System Commands from Python**  
The `os` module allows running system commands like `ls`, `mkdir`, `rm`, etc.

✅ **Run a command using `os.system()`**  
```python
os.system("ls")  # List files (Linux/Mac)
os.system("dir")  # List files (Windows)
```

✅ **Run a command using `subprocess.run()`**  
```python
import subprocess
output = subprocess.run(["ls", "-l"], capture_output=True, text=True)
print(output.stdout)
```

✅ **Check disk usage (Linux only)**  
```python
os.system("df -h")
```

✅ **Check CPU information**  
```python
os.system("lscpu")  # Linux
os.system("wmic cpu get caption")  # Windows
```

---

## **3. Practical Python Script (Combining File Handling & OS Interaction)**  
This script:  
✔ Checks if `log.txt` exists,  
✔ Creates it if not,  
✔ Writes system info to the file,  
✔ Appends new logs.  

```python
import os
import datetime

file_name = "log.txt"

# Check if file exists, else create it
if not os.path.exists(file_name):
    with open(file_name, "w") as file:
        file.write("System Log File\n")
        file.write("="*20 + "\n")

# Append system information to log file
with open(file_name, "a") as file:
    file.write(f"\nLog Entry: {datetime.datetime.now()}\n")
    file.write("Current Directory: " + os.getcwd() + "\n")
    file.write("Files in Directory: " + str(os.listdir()) + "\n")
```
✔ Creates a log file and records system details.  
✔ Useful for monitoring and automation tasks.  

---

## **Conclusion**  
✔ **File Handling**: Read, write, append, delete files.  
✔ **OS Interaction**: Work with directories, system commands, automation.  
✔ **Best Practice**: Use `with open()` for handling files safely.  

Would you like **more hands-on exercises** to practice?