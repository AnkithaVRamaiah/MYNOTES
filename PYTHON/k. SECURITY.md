# **Security in Python Scripting**  

Security is a critical aspect of Python scripting, especially in applications that deal with sensitive data, user authentication, APIs, databases, or networking. This guide covers key security concepts, common vulnerabilities, and best practices in Python.

---

## **1. Common Security Vulnerabilities in Python**  
Here are some common security risks in Python applications:  

### **1.1 Code Injection (Command Injection, SQL Injection, etc.)**  
- **Example of Command Injection:**
```python
import os
user_input = input("Enter a command: ")  
os.system(user_input)  # Dangerous! Allows execution of any command
```
**Fix:** Use `subprocess.run()` with argument lists to prevent arbitrary command execution.
```python
import subprocess
subprocess.run(["ls", "-l"])
```

- **Example of SQL Injection:**  
```python
import sqlite3
conn = sqlite3.connect("test.db")
cursor = conn.cursor()

user_input = "admin' OR 1=1 --"  # SQL Injection Payload
query = f"SELECT * FROM users WHERE username = '{user_input}'"  
cursor.execute(query)  # Dangerous!

print(cursor.fetchall())
```
**Fix:** Use parameterized queries.
```python
cursor.execute("SELECT * FROM users WHERE username = ?", (user_input,))
```

---

### **1.2 Hardcoded Secrets and Credentials**  
Storing sensitive information like API keys or passwords in scripts is dangerous.  

**Bad Practice:**  
```python
API_KEY = "12345-SECRET-KEY"
```
**Fix:** Use environment variables or secret management tools.
```python
import os
API_KEY = os.getenv("API_KEY")
```

---

### **1.3 Insecure Deserialization**  
Using `pickle` to load untrusted data can execute arbitrary code.  
```python
import pickle
data = pickle.loads(untrusted_input)  # Dangerous!
```
**Fix:** Use safer alternatives like `json` or `marshal`.
```python
import json
data = json.loads(untrusted_input)
```

---

## **2. Secure Authentication and Authorization**  
Ensuring users are properly authenticated and authorized is essential.

### **2.1 Password Hashing (Avoid Storing Plaintext Passwords)**  
Use `bcrypt` or `hashlib` for secure password hashing.  
```python
import bcrypt

password = "mypassword".encode()
hashed = bcrypt.hashpw(password, bcrypt.gensalt())

print(hashed)
```

To verify a password:
```python
if bcrypt.checkpw("mypassword".encode(), hashed):
    print("Password is correct")
```

---

### **2.2 Secure Token-Based Authentication (JWT)**  
Use JSON Web Tokens (JWT) for secure API authentication.  
```python
import jwt
import datetime

SECRET_KEY = "my_secret"
payload = {"user": "admin", "exp": datetime.datetime.utcnow() + datetime.timedelta(hours=1)}

token = jwt.encode(payload, SECRET_KEY, algorithm="HS256")
print(token)

decoded = jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
print(decoded)
```

---

## **3. Secure Data Handling and Encryption**  

### **3.1 Hashing Data (`hashlib`)**  
Hashing is used for verifying data integrity.  
```python
import hashlib

data = "important data".encode()
hash_value = hashlib.sha256(data).hexdigest()

print(hash_value)
```

---

### **3.2 Encrypting and Decrypting Data (`cryptography` Library)**  
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

## **4. Secure API Development**  

### **4.1 Input Validation to Prevent Injection Attacks**  
```python
import re

def validate_username(username):
    if not re.match("^[a-zA-Z0-9_]+$", username):
        raise ValueError("Invalid username")

validate_username("safe_user")  # ✅ Safe
validate_username("admin; DROP TABLE users")  # ❌ Dangerous
```

---

### **4.2 Rate Limiting to Prevent DDoS Attacks**  
Use Flask-Limiter to limit API requests.  
```python
from flask import Flask
from flask_limiter import Limiter

app = Flask(__name__)
limiter = Limiter(app, key_func=lambda: "global")

@app.route("/api")
@limiter.limit("10 per minute")
def api():
    return "API Response"

if __name__ == "__main__":
    app.run()
```

---

### **4.3 Secure HTTP with SSL/TLS (`requests` Library)**  
Use HTTPS instead of HTTP.  
```python
import requests

response = requests.get("https://example.com", verify=True)
print(response.text)
```

---

## **5. Secure File Handling**  

### **5.1 Avoid Using `eval()` on Untrusted Input**  
```python
user_input = "print('Hello!')"  
eval(user_input)  # Dangerous!
```
**Fix:** Use `ast.literal_eval()`
```python
import ast
safe_input = ast.literal_eval("{'key': 'value'}")
print(safe_input)
```

---

### **5.2 Validate File Uploads (Avoid Arbitrary File Execution)**  
```python
import os

filename = "user_input.txt"
allowed_extensions = {".txt", ".csv"}

if os.path.splitext(filename)[1] not in allowed_extensions:
    raise ValueError("Invalid file type")
```

---

## **6. Secure Network Programming**  

### **6.1 Use Secure Sockets (`ssl`)**  
```python
import ssl
import socket

context = ssl.create_default_context()
with socket.create_connection(("example.com", 443)) as sock:
    with context.wrap_socket(sock, server_hostname="example.com") as secure_sock:
        secure_sock.sendall(b"GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
        print(secure_sock.recv(1024).decode())
```

---

## **7. Secure Dependencies and Environment**  

### **7.1 Keep Dependencies Updated**  
Check for security vulnerabilities with:  
```bash
pip install --upgrade pip  
pip list --outdated
```

Use `pip-audit` to check for security issues:  
```bash
pip install pip-audit  
pip-audit
```

---

### **7.2 Use Virtual Environments to Isolate Dependencies**  
```bash
python -m venv myenv  
source myenv/bin/activate  # (Linux/macOS)
myenv\Scripts\activate  # (Windows)
```

---

### **7.3 Use Docker for Secure Execution**  
```dockerfile
FROM python:3.9
COPY app.py /app/
WORKDIR /app
CMD ["python", "app.py"]
```
Run it securely in an isolated container:  
```bash
docker build -t secure_app .
docker run --rm secure_app
```

---

## **8. Logging and Monitoring for Security**  

### **8.1 Use Secure Logging**  
```python
import logging

logging.basicConfig(filename="secure.log", level=logging.INFO)
logging.info("User logged in")
```

### **8.2 Monitor Logs for Security Events**  
Use `fail2ban` to detect brute-force attacks:  
```bash
sudo apt install fail2ban  
sudo systemctl start fail2ban
```

---

## **Conclusion**  
Security in Python scripting is essential for preventing attacks and ensuring data integrity.  

✅ **Sanitize user inputs (avoid injections)**  
✅ **Hash and encrypt sensitive data**  
✅ **Use secure authentication methods (JWT, bcrypt)**  
✅ **Use HTTPS and SSL/TLS for communication**  
✅ **Monitor and log security events**  
✅ **Keep dependencies updated and isolate environments**  

Would you like a **Python security project** for hands-on practice?