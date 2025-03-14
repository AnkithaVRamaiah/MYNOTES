# **Automating Tasks with Python**  

Python is a powerful language for automation, allowing you to automate repetitive tasks like file handling, web scraping, email sending, and more. This guide covers:  

1. **Basics of Automation**  
2. **File and Folder Automation**  
3. **Web Scraping with Python**  
4. **Automating Emails**  
5. **Working with APIs**  
6. **Automating Excel and PDFs**  
7. **Scheduling Python Scripts**  
8. **Real-world Examples**  

---

## **1. Basics of Automation**  

Python provides several built-in libraries and external modules to automate tasks:  

| **Task**               | **Python Module**  |
|------------------------|-------------------|
| File handling         | `os`, `shutil`   |
| Web scraping         | `requests`, `BeautifulSoup`, `selenium` |
| Sending emails       | `smtplib`, `email` |
| Working with APIs    | `requests` |
| Automating Excel     | `openpyxl`, `pandas` |
| Automating PDFs      | `PyPDF2`, `reportlab` |
| Scheduling tasks     | `schedule`, `cron`, `task scheduler` |

---

## **2. File and Folder Automation**  

### **2.1 Working with Files (`os` and `shutil`)**  

```python
import os

# Create a new folder
os.mkdir("test_folder")

# List all files in a directory
files = os.listdir(".")
print(files)

# Rename a file
os.rename("old_name.txt", "new_name.txt")

# Delete a file
os.remove("new_name.txt")
```

### **2.2 Copy, Move, and Delete Files (`shutil`)**  

```python
import shutil

# Copy a file
shutil.copy("source.txt", "destination.txt")

# Move a file
shutil.move("source.txt", "new_folder/source.txt")

# Delete a folder
shutil.rmtree("test_folder")
```

---

## **3. Web Scraping with Python**  

Web scraping is extracting data from websites.  

### **3.1 Using `requests` and `BeautifulSoup`**  

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")
title = soup.find("title").text  # Extracts the page title

print(title)
```

---

## **4. Automating Emails**  

### **4.1 Sending Emails with `smtplib`**  

```python
import smtplib
from email.mime.text import MIMEText

sender = "your_email@gmail.com"
receiver = "recipient@example.com"
password = "your_password"

message = MIMEText("Hello, this is an automated email!")
message["Subject"] = "Automated Email"
message["From"] = sender
message["To"] = receiver

# Sending the email
with smtplib.SMTP_SSL("smtp.gmail.com", 465) as server:
    server.login(sender, password)
    server.sendmail(sender, receiver, message.as_string())

print("Email sent successfully!")
```

---

## **5. Working with APIs**  

APIs allow automation by interacting with web services.  

### **5.1 Making API Requests with `requests`**  

```python
import requests

url = "https://api.github.com/users/octocat"
response = requests.get(url)

data = response.json()
print(data["login"])  # Output: octocat
```

---

## **6. Automating Excel and PDFs**  

### **6.1 Reading and Writing Excel Files (`openpyxl`)**  

```python
import openpyxl

# Create a new Excel file
wb = openpyxl.Workbook()
ws = wb.active
ws.title = "Sheet1"

# Add data
ws["A1"] = "Name"
ws["B1"] = "Age"
ws.append(["Alice", 25])
ws.append(["Bob", 30])

# Save the file
wb.save("data.xlsx")
```

### **6.2 Extracting Text from PDFs (`PyPDF2`)**  

```python
import PyPDF2

with open("sample.pdf", "rb") as pdf_file:
    reader = PyPDF2.PdfReader(pdf_file)
    page = reader.pages[0]
    text = page.extract_text()

print(text)
```

---

## **7. Scheduling Python Scripts**  

Python scripts can be scheduled to run automatically.  

### **7.1 Using `schedule` Library**  

```python
import schedule
import time

def task():
    print("Task running...")

# Run every 5 minutes
schedule.every(5).minutes.do(task)

while True:
    schedule.run_pending()
    time.sleep(1)
```

### **7.2 Using `cron` (Linux) or Task Scheduler (Windows)**  

#### **Linux (Cron Job Example)**  
Run script every day at 10 AM:  
```sh
crontab -e
0 10 * * * /usr/bin/python3 /path/to/script.py
```

#### **Windows Task Scheduler**  
1. Open **Task Scheduler**  
2. Click **Create Basic Task**  
3. Set **Trigger** (Daily, Weekly, etc.)  
4. Set **Action** → **Start a Program** → `python script.py`  

---

## **8. Real-World Automation Examples**  

| **Task** | **Tools Used** |
|----------|--------------|
| Rename thousands of files | `os`, `shutil` |
| Backup files to the cloud | `shutil`, `boto3` (AWS) |
| Auto-fill Google Forms | `selenium` |
| Send daily reports via email | `smtplib`, `pandas` |
| Monitor websites for changes | `requests`, `BeautifulSoup` |
| Automate social media posts | `requests`, API (Twitter, Facebook) |

---

## **Conclusion**  
✅ Python is powerful for **automating repetitive tasks**.  
✅ Libraries like **`os`, `shutil`, `requests`, `schedule`** help automate processes.  
✅ Automation improves **productivity and efficiency**.  

Would you like hands-on projects or a detailed tutorial on any specific task?