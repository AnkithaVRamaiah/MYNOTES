# **Database Handling in Python**  

## **Overview**  
Database handling in Python involves:  
✔️ Connecting to databases  
✔️ Running SQL queries (SELECT, INSERT, UPDATE, DELETE)  
✔️ Fetching and manipulating data  
✔️ Handling transactions  
✔️ Working with relational (MySQL, PostgreSQL) and NoSQL (MongoDB) databases  

---

## **1. Types of Databases in Python**  

| **Database** | **Type** | **Python Library** |
|-------------|---------|--------------------|
| SQLite | Relational | `sqlite3` |
| MySQL | Relational | `mysql-connector-python`, `PyMySQL` |
| PostgreSQL | Relational | `psycopg2` |
| MongoDB | NoSQL | `pymongo` |
| Redis | Key-Value Store | `redis` |

---

## **2. SQLite (Lightweight Built-in Database)**  

SQLite is a lightweight database that comes with Python.  

### **2.1 Connecting to SQLite**  
```python
import sqlite3

conn = sqlite3.connect("mydatabase.db")  # Creates or connects to a database
cursor = conn.cursor()
print("Database connected successfully!")
```

### **2.2 Creating a Table**  
```python
cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY,
    name TEXT,
    age INTEGER
)
""")
conn.commit()
```

### **2.3 Inserting Data**  
```python
cursor.execute("INSERT INTO users (name, age) VALUES (?, ?)", ("Alice", 25))
conn.commit()
```

### **2.4 Fetching Data**  
```python
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### **2.5 Updating Data**  
```python
cursor.execute("UPDATE users SET age = 26 WHERE name = 'Alice'")
conn.commit()
```

### **2.6 Deleting Data**  
```python
cursor.execute("DELETE FROM users WHERE name = 'Alice'")
conn.commit()
```

### **2.7 Closing the Connection**  
```python
conn.close()
```

---

## **3. MySQL Database Handling**  

MySQL is a widely used relational database.  

### **3.1 Installing MySQL Connector**  
```sh
pip install mysql-connector-python
```

### **3.2 Connecting to MySQL**  
```python
import mysql.connector

conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="mydatabase"
)
cursor = conn.cursor()
print("Connected to MySQL database!")
```

### **3.3 Creating a Table in MySQL**  
```python
cursor.execute("""
CREATE TABLE IF NOT EXISTS employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    salary FLOAT
)
""")
conn.commit()
```

### **3.4 Inserting Data into MySQL**  
```python
cursor.execute("INSERT INTO employees (name, salary) VALUES (%s, %s)", ("John", 50000))
conn.commit()
```

### **3.5 Fetching Data from MySQL**  
```python
cursor.execute("SELECT * FROM employees")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

### **3.6 Updating Data in MySQL**  
```python
cursor.execute("UPDATE employees SET salary = 60000 WHERE name = 'John'")
conn.commit()
```

### **3.7 Deleting Data from MySQL**  
```python
cursor.execute("DELETE FROM employees WHERE name = 'John'")
conn.commit()
```

---

## **4. PostgreSQL Database Handling**  

PostgreSQL is an advanced relational database system.  

### **4.1 Installing PostgreSQL Driver**  
```sh
pip install psycopg2
```

### **4.2 Connecting to PostgreSQL**  
```python
import psycopg2

conn = psycopg2.connect(
    dbname="mydatabase",
    user="postgres",
    password="password",
    host="localhost"
)
cursor = conn.cursor()
print("Connected to PostgreSQL database!")
```

### **4.3 Creating a Table in PostgreSQL**  
```python
cursor.execute("""
CREATE TABLE IF NOT EXISTS customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50)
)
""")
conn.commit()
```

### **4.4 Inserting Data into PostgreSQL**  
```python
cursor.execute("INSERT INTO customers (name, city) VALUES (%s, %s)", ("Mike", "New York"))
conn.commit()
```

### **4.5 Fetching Data from PostgreSQL**  
```python
cursor.execute("SELECT * FROM customers")
rows = cursor.fetchall()
for row in rows:
    print(row)
```

---

## **5. MongoDB (NoSQL Database Handling)**  

MongoDB stores data in **JSON-like** documents.  

### **5.1 Installing MongoDB Driver**  
```sh
pip install pymongo
```

### **5.2 Connecting to MongoDB**  
```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017/")
db = client["mydatabase"]
collection = db["users"]
print("Connected to MongoDB!")
```

### **5.3 Inserting Data into MongoDB**  
```python
data = {"name": "Alice", "age": 30}
collection.insert_one(data)
print("Data inserted successfully!")
```

### **5.4 Fetching Data from MongoDB**  
```python
for user in collection.find():
    print(user)
```

### **5.5 Updating Data in MongoDB**  
```python
collection.update_one({"name": "Alice"}, {"$set": {"age": 31}})
print("Data updated successfully!")
```

### **5.6 Deleting Data from MongoDB**  
```python
collection.delete_one({"name": "Alice"})
print("Data deleted successfully!")
```

---

## **6. Handling Transactions in Databases**  

Transactions help maintain **data integrity** by ensuring that multiple queries are executed together.  

### **6.1 Using Transactions in MySQL**  
```python
try:
    conn.start_transaction()
    cursor.execute("INSERT INTO employees (name, salary) VALUES ('Alice', 40000)")
    cursor.execute("INSERT INTO employees (name, salary) VALUES ('Bob', 50000)")
    conn.commit()  # Commit the transaction
    print("Transaction successful!")
except:
    conn.rollback()  # Rollback in case of error
    print("Transaction failed!")
```

---

## **7. Database Connection Best Practices**  

✅ **Always close connections** after use:  
```python
cursor.close()
conn.close()
```

✅ **Use connection pooling** for better performance in web apps  

✅ **Handle exceptions properly**:  
```python
try:
    conn = sqlite3.connect("database.db")
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM users")
except Exception as e:
    print("Error:", e)
finally:
    conn.close()
```

---

## **8. Real-World Use Cases of Database Handling**  

✔️ **Web Applications** → Storing user data, authentication  
✔️ **E-Commerce Apps** → Managing products, orders, payments  
✔️ **Logging Systems** → Storing and analyzing logs  
✔️ **Monitoring Systems** → Storing metrics  

---

## **Conclusion**  
✅ **SQLite** – Lightweight, built-in database  
✅ **MySQL/PostgreSQL** – Powerful relational databases  
✅ **MongoDB** – NoSQL, best for flexible data storage  
✅ **Transactions ensure data integrity**  
✅ **Always handle errors and close connections**  

Would you like a **real-world database project** example?