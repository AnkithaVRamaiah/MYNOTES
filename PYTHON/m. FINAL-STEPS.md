# **Final Steps: Projects & Practice**  

To solidify your Python scripting skills, work on practical projects that involve automation, cloud interaction, system monitoring, and data extraction. These projects align well with DevOps, cloud computing, and system administration roles.

---

## **1. Automated Log File Analyzer**  

### **Project Overview**  
- Parse system or application log files.  
- Extract errors, warnings, and other key insights.  
- Generate a summary report for quick analysis.  

### **Technologies Used**  
✅ Python  
✅ Regular Expressions (`re` module)  
✅ File Handling (`open()`, `read()`, `write()`)  
✅ Logging (`logging` module)  

---

### **1.1 Code Implementation**  

```python
import re
import os

LOG_FILE_PATH = "/var/log/syslog"  # Change as needed

def analyze_logs(log_file):
    error_count = 0
    warning_count = 0

    with open(log_file, "r") as file:
        for line in file:
            if re.search(r"ERROR", line):
                error_count += 1
            elif re.search(r"WARNING", line):
                warning_count += 1

    print(f"Total Errors: {error_count}")
    print(f"Total Warnings: {warning_count}")

if __name__ == "__main__":
    if os.path.exists(LOG_FILE_PATH):
        analyze_logs(LOG_FILE_PATH)
    else:
        print("Log file not found!")
```

---

### **1.2 Interview Questions & Answers**  

❓ **Q1: How can you efficiently parse large log files in Python?**  
✅ **A:** Use a generator (`yield`) to process the file line by line, reducing memory usage.

❓ **Q2: How do you filter specific log entries using regex?**  
✅ **A:** Use `re.search(r"pattern", line)` to match error codes, timestamps, or keywords.

❓ **Q3: How would you automate log analysis?**  
✅ **A:** Use a cron job to run the script periodically and send alerts via email or Slack.

---

## **2. AWS Resource Tracker**  

### **Project Overview**  
- Monitor AWS resources (EC2 instances, S3 buckets, IAM users).  
- Generate a report on resource usage.  
- Automate cost tracking and cleanup.  

### **Technologies Used**  
✅ Python  
✅ Boto3 (AWS SDK)  
✅ AWS CLI (`aws configure`)  
✅ JSON / CSV (for report generation)  

---

### **2.1 Code Implementation**  

```python
import boto3

def list_ec2_instances():
    ec2 = boto3.client("ec2")
    instances = ec2.describe_instances()
    for reservation in instances["Reservations"]:
        for instance in reservation["Instances"]:
            print(f"Instance ID: {instance['InstanceId']}, State: {instance['State']['Name']}")

def list_s3_buckets():
    s3 = boto3.client("s3")
    buckets = s3.list_buckets()
    for bucket in buckets["Buckets"]:
        print(f"Bucket Name: {bucket['Name']}")

def list_iam_users():
    iam = boto3.client("iam")
    users = iam.list_users()
    for user in users["Users"]:
        print(f"User Name: {user['UserName']}")

if __name__ == "__main__":
    list_ec2_instances()
    list_s3_buckets()
    list_iam_users()
```

---

### **2.2 Interview Questions & Answers**  

❓ **Q1: How do you authenticate Python scripts to access AWS resources?**  
✅ **A:** Use `aws configure` to set up credentials or use IAM roles.

❓ **Q2: What is the difference between `boto3.client` and `boto3.resource`?**  
✅ **A:** `client` provides low-level API access, while `resource` provides high-level, object-oriented access.

❓ **Q3: How can you schedule this script to run automatically?**  
✅ **A:** Use a cron job (`crontab -e`) or AWS Lambda with a CloudWatch event trigger.

---

## **3. Python Web Scraper**  

### **Project Overview**  
- Extract data from websites.  
- Store data in a structured format (CSV, JSON).  
- Automate web data collection for analytics.  

### **Technologies Used**  
✅ Python  
✅ `requests` (for HTTP requests)  
✅ `BeautifulSoup` (for HTML parsing)  
✅ `pandas` (for data processing)  

---

### **3.1 Code Implementation**  

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

URL = "https://example.com/news"

def scrape_news():
    response = requests.get(URL)
    soup = BeautifulSoup(response.text, "html.parser")
    
    news_titles = [title.text for title in soup.find_all("h2", class_="news-title")]
    news_data = pd.DataFrame(news_titles, columns=["Title"])
    
    news_data.to_csv("news.csv", index=False)
    print("Scraped data saved to news.csv")

if __name__ == "__main__":
    scrape_news()
```

---

### **3.2 Interview Questions & Answers**  

❓ **Q1: What is the difference between `requests.get()` and `urllib`?**  
✅ **A:** `requests` is a high-level library with better usability than `urllib`.

❓ **Q2: How do you handle websites that block scrapers?**  
✅ **A:** Use headers (`User-Agent`), proxies, and rotating IPs.

❓ **Q3: How do you store scraped data efficiently?**  
✅ **A:** Use databases like MySQL, SQLite, or NoSQL (MongoDB).

---

## **4. Database Backup Script**  

### **Project Overview**  
- Backup MySQL or PostgreSQL databases.  
- Automate the backup and cleanup process.  
- Store backups on local disk or AWS S3.  

### **Technologies Used**  
✅ Python  
✅ MySQL/PostgreSQL (`mysqldump` or `pg_dump`)  
✅ Boto3 (optional, for S3 storage)  

---

### **4.1 Code Implementation**  

```python
import os
import datetime

DB_NAME = "mydatabase"
BACKUP_DIR = "/backup"

def backup_db():
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    backup_file = f"{BACKUP_DIR}/backup_{DB_NAME}_{timestamp}.sql"

    os.system(f"mysqldump -u root -pPASSWORD {DB_NAME} > {backup_file}")
    print(f"Database backup saved to {backup_file}")

if __name__ == "__main__":
    backup_db()
```

---

### **4.2 Interview Questions & Answers**  

❓ **Q1: How can you automate database backups?**  
✅ **A:** Use a cron job to run the script daily.

❓ **Q2: How do you restore a backup?**  
✅ **A:** Use `mysql -u root -pPASSWORD mydatabase < backup.sql`.

❓ **Q3: How do you optimize database backups?**  
✅ **A:** Use incremental backups and compress files (`gzip`).

---

## **5. DevOps Monitoring Script**  

### **Project Overview**  
- Monitor system health (CPU, memory, disk usage).  
- Identify running processes and high resource consumption.  

### **Technologies Used**  
✅ Python  
✅ `psutil` (for system monitoring)  
✅ Logging  

---

### **5.1 Code Implementation**  

```python
import psutil

def check_system_health():
    print(f"CPU Usage: {psutil.cpu_percent()}%")
    print(f"Memory Usage: {psutil.virtual_memory().percent}%")
    print(f"Disk Usage: {psutil.disk_usage('/').percent}%")

def list_processes():
    for proc in psutil.process_iter(attrs=["pid", "name", "cpu_percent"]):
        print(proc.info)

if __name__ == "__main__":
    check_system_health()
    list_processes()
```

---

### **5.2 Interview Questions & Answers**  

❓ **Q1: How do you automate system monitoring?**  
✅ **A:** Use a cron job to run the script periodically and send alerts.

❓ **Q2: How do you monitor a remote server?**  
✅ **A:** Use SSH (`paramiko`) or monitoring tools like Prometheus.

❓ **Q3: What tool would you use for real-time monitoring?**  
✅ **A:** `htop`, `top`, or Prometheus + Grafana.

---

## **Conclusion**  
These **Python projects** help in mastering DevOps, system administration, and automation skills. Let me know if you need **hands-on guidance**! 🚀