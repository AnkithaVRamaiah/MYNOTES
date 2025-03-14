# **Networking and Multithreading in Python**  

Networking and multithreading are crucial concepts in system programming, web applications, and real-time data processing.  

---

# **1. Networking in Python**  

Networking in Python is handled using the **`socket`** module, which allows communication between computers using TCP/IP or UDP.  

## **1.1 Understanding Sockets**  
A **socket** is an endpoint for communication between two devices.  

- **Types of Sockets**:
  - **TCP (Transmission Control Protocol)** – Reliable, connection-oriented (e.g., web browsing)
  - **UDP (User Datagram Protocol)** – Faster, connectionless (e.g., video streaming)

---

## **1.2 Creating a Simple TCP Server and Client**  

### **1.2.1 TCP Server**  
```python
import socket

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("localhost", 12345))  # Bind to IP and port
server_socket.listen(5)  # Listen for connections
print("Server is listening on port 12345...")

while True:
    client_socket, addr = server_socket.accept()  # Accept connection
    print(f"Connection from {addr} established")
    client_socket.send(b"Hello from server!")  # Send data
    client_socket.close()
```

### **1.2.2 TCP Client**  
```python
import socket

client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client_socket.connect(("localhost", 12345))  # Connect to server
data = client_socket.recv(1024)  # Receive data
print("Received:", data.decode())
client_socket.close()
```

---

## **1.3 UDP Communication**  

### **1.3.1 UDP Server**  
```python
import socket

udp_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp_server.bind(("localhost", 12345))
print("UDP Server is running...")

while True:
    data, addr = udp_server.recvfrom(1024)
    print(f"Received '{data.decode()}' from {addr}")
    udp_server.sendto(b"Message received", addr)
```

### **1.3.2 UDP Client**  
```python
import socket

udp_client = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
udp_client.sendto(b"Hello, UDP Server!", ("localhost", 12345))
data, addr = udp_client.recvfrom(1024)
print("Received:", data.decode())
```

---

## **1.4 Working with HTTP Requests using `requests`**  
```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/todos/1")
print(response.json())  # Print JSON response
```

---

# **2. Multithreading in Python**  

Multithreading allows a program to run multiple tasks concurrently, improving performance in **I/O-bound** tasks like file handling, network requests, and database operations.  

## **2.1 Creating a Simple Thread**  
```python
import threading

def print_numbers():
    for i in range(5):
        print(i)

thread = threading.Thread(target=print_numbers)
thread.start()
thread.join()  # Wait for thread to complete
```

---

## **2.2 Multithreading with Multiple Threads**  
```python
import threading

def task(name):
    print(f"Task {name} is running...")

threads = []
for i in range(5):
    thread = threading.Thread(target=task, args=(i,))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()
```

---

## **2.3 Thread Synchronization using Locks**  

When multiple threads access shared data, race conditions can occur. **Locks** prevent multiple threads from modifying data simultaneously.  

```python
import threading

counter = 0
lock = threading.Lock()

def increment():
    global counter
    with lock:  # Ensures only one thread modifies counter at a time
        for _ in range(1000):
            counter += 1

threads = [threading.Thread(target=increment) for _ in range(5)]

for thread in threads:
    thread.start()
for thread in threads:
    thread.join()

print("Final Counter Value:", counter)
```

---

## **2.4 Using ThreadPoolExecutor (Better Performance)**  
Instead of manually managing threads, we can use `ThreadPoolExecutor`.  

```python
from concurrent.futures import ThreadPoolExecutor

def fetch_data(n):
    print(f"Fetching data {n}...")

with ThreadPoolExecutor(max_workers=3) as executor:
    executor.map(fetch_data, range(5))
```

---

## **3. Combining Networking and Multithreading**  

### **3.1 Multi-Client TCP Server**  
```python
import socket
import threading

def handle_client(client_socket):
    data = client_socket.recv(1024)
    print("Received:", data.decode())
    client_socket.send(b"Hello from Server!")
    client_socket.close()

server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.bind(("localhost", 12345))
server_socket.listen(5)
print("Server is listening...")

while True:
    client_socket, addr = server_socket.accept()
    thread = threading.Thread(target=handle_client, args=(client_socket,))
    thread.start()
```

---

## **4. Best Practices for Networking & Multithreading**  

✅ **Use `threading.Thread` for lightweight tasks**  
✅ **Use `ThreadPoolExecutor` for managing multiple threads**  
✅ **Use locks to prevent race conditions in shared resources**  
✅ **Always close sockets after use**  
✅ **Handle exceptions properly to avoid crashes**  

Would you like a real-world project example on **networking + multithreading**?