# **Advanced Python Scripting Concepts**  

Advanced Python scripting involves techniques and tools that enhance performance, maintainability, and scalability of Python programs. These concepts are widely used in DevOps, automation, data analysis, and system administration.  

---

## **1. Decorators in Python**  

A **decorator** is a function that modifies another function without changing its actual code.  

### **1.1 Basic Decorator**  
```python
def my_decorator(func):
    def wrapper():
        print("Before function execution")
        func()
        print("After function execution")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```
**Output:**  
```
Before function execution  
Hello!  
After function execution  
```

### **1.2 Decorators with Arguments**  
```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

greet("Ankita")
```

---

## **2. Generators and Iterators**  

### **2.1 Generators (`yield`)**  
Generators are memory-efficient and used for iterating large datasets.  

```python
def count_up(n):
    for i in range(n):
        yield i  # Suspends and resumes function execution

gen = count_up(5)
print(next(gen))  # Output: 0
print(next(gen))  # Output: 1
```

### **2.2 Custom Iterators**  
```python
class Counter:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.current < self.limit:
            self.current += 1
            return self.current
        else:
            raise StopIteration

counter = Counter(3)
for num in counter:
    print(num)  # Output: 1, 2, 3
```

---

## **3. Context Managers (`with` statement)**  
Used to manage resources like files and database connections.  

```python
class FileHandler:
    def __init__(self, filename, mode):
        self.file = open(filename, mode)

    def __enter__(self):
        return self.file

    def __exit__(self, exc_type, exc_value, traceback):
        self.file.close()

with FileHandler("example.txt", "w") as file:
    file.write("Hello, Python!")
```

---

## **4. Metaclasses**  
A **metaclass** is a class that defines the behavior of other classes.  

```python
class Meta(type):
    def __new__(cls, name, bases, class_dict):
        print(f"Creating class {name}")
        return super().__new__(cls, name, bases, class_dict)

class MyClass(metaclass=Meta):
    pass  # This triggers the metaclass

# Output: Creating class MyClass
```

---

## **5. Asynchronous Programming (`async` and `await`)**  
Used for non-blocking I/O operations, useful in web scraping, APIs, and databases.  

```python
import asyncio

async def say_hello():
    print("Hello")
    await asyncio.sleep(1)  # Simulate delay
    print("World!")

asyncio.run(say_hello())
```

---

## **6. Threading and Multiprocessing**  

### **6.1 Using Threads for Concurrency**  
```python
import threading

def task(name):
    print(f"Task {name} is running...")

threads = [threading.Thread(target=task, args=(i,)) for i in range(3)]

for thread in threads:
    thread.start()
for thread in threads:
    thread.join()
```

### **6.2 Using Multiprocessing for Parallel Execution**  
```python
import multiprocessing

def worker(n):
    print(f"Worker {n} is running...")

if __name__ == "__main__":
    processes = [multiprocessing.Process(target=worker, args=(i,)) for i in range(3)]
    
    for p in processes:
        p.start()
    
    for p in processes:
        p.join()
```

---

## **7. Logging and Debugging**  

### **7.1 Basic Logging**  
```python
import logging

logging.basicConfig(level=logging.DEBUG, format="%(asctime)s - %(levelname)s - %(message)s")
logging.info("This is an info message")
logging.warning("This is a warning")
```

### **7.2 Debugging with `pdb` (Python Debugger)**  
```python
import pdb

def buggy_function():
    x = 10
    y = 0
    pdb.set_trace()  # Debugging breakpoint
    result = x / y  # This will cause ZeroDivisionError
    return result

buggy_function()
```

---

## **8. Python and Database Integration**  

### **8.1 SQLite Example**  
```python
import sqlite3

conn = sqlite3.connect("data.db")
cursor = conn.cursor()

cursor.execute("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)")
cursor.execute("INSERT INTO users (name) VALUES ('Ankita')")
conn.commit()

cursor.execute("SELECT * FROM users")
print(cursor.fetchall())

conn.close()
```

---

## **9. Web Scraping with `BeautifulSoup` and `requests`**  
```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

print(soup.title.text)
```

---

## **10. Working with APIs (RESTful Services)**  
```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/todos/1")
print(response.json())  # Output JSON response
```

---

## **11. Cryptography and Security**  
### **11.1 Hashing Passwords with `hashlib`**  
```python
import hashlib

password = "securepassword".encode()
hashed = hashlib.sha256(password).hexdigest()
print(hashed)  # Securely store passwords
```

### **11.2 Encrypting Data with `cryptography`**  
```python
from cryptography.fernet import Fernet

key = Fernet.generate_key()
cipher = Fernet(key)

encrypted = cipher.encrypt(b"Secret Message")
print(encrypted)

decrypted = cipher.decrypt(encrypted)
print(decrypted.decode())
```

---

# **Conclusion**  

Advanced Python scripting improves efficiency, security, and automation.  

✅ **Use decorators to modify functions dynamically**  
✅ **Use generators and iterators for efficient data handling**  
✅ **Use multithreading/multiprocessing for concurrency and parallelism**  
✅ **Use context managers for resource management**  
✅ **Use async programming for high-performance applications**  
✅ **Use logging and debugging for maintaining applications**  
✅ **Use APIs, web scraping, and databases for data management**  

Would you like an advanced **Python scripting project** for hands-on practice?