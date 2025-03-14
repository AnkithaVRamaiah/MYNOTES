# **DevOps & System Administration Scripting with Python and Shell**  

DevOps and system administration scripting involve automating infrastructure management, configuration, deployments, and monitoring. This guide covers:  

1. **Introduction to DevOps & System Admin Scripting**  
2. **Common Scripting Languages in DevOps**  
3. **Infrastructure Automation with Python & Shell**  
4. **Server Monitoring & Log Management**  
5. **CI/CD Automation**  
6. **Cloud Automation (AWS, Azure, GCP)**  
7. **Security & User Management**  
8. **Backup & Disaster Recovery Automation**  
9. **Scheduling Scripts for Automation**  
10. **Real-World Use Cases & Projects**  

---

## **1. Introduction to DevOps & System Admin Scripting**  

### **Why Automate in DevOps & System Administration?**  

✅ Reduces manual effort & human errors  
✅ Improves efficiency & consistency  
✅ Enables faster deployments & scaling  
✅ Helps with continuous monitoring & logging  

**Key Tasks Automated:**  
✔️ Provisioning servers & infrastructure  
✔️ Managing system configurations  
✔️ Deploying applications  
✔️ Monitoring resources & logs  
✔️ Backup & disaster recovery  

---

## **2. Common Scripting Languages in DevOps**  

| **Language** | **Use Case** |
|-------------|-------------|
| **Bash** | System automation, cron jobs, server management |
| **Python** | Infrastructure automation, APIs, monitoring |
| **PowerShell** | Windows system administration, automation |
| **Ansible (YAML)** | Configuration management |
| **Terraform (HCL)** | Infrastructure as Code (IaC) |
| **Groovy** | Jenkins pipeline scripting |

---

## **3. Infrastructure Automation with Python & Shell**  

### **3.1 Managing Files & Directories (Shell & Python)**  

**Shell Script Example:**  
```bash
#!/bin/bash
mkdir /tmp/test_folder
touch /tmp/test_folder/file1.txt
echo "File created successfully!"
```

**Python Script Example:**  
```python
import os

os.makedirs("/tmp/test_folder", exist_ok=True)
with open("/tmp/test_folder/file1.txt", "w") as f:
    f.write("File created successfully!")
print("File created successfully!")
```

---

### **3.2 Server Provisioning & Configuration (Python with AWS Boto3)**  

```python
import boto3

ec2 = boto3.resource('ec2')

# Create a new EC2 instance
instance = ec2.create_instances(
    ImageId='ami-0abcdef1234567890', 
    InstanceType='t2.micro',
    MinCount=1, 
    MaxCount=1
)

print("EC2 instance created:", instance[0].id)
```

---

## **4. Server Monitoring & Log Management**  

### **4.1 Check CPU, Memory, and Disk Usage (Shell & Python)**  

**Shell Script:**  
```bash
#!/bin/bash
echo "CPU Usage:"
top -bn1 | grep "Cpu"

echo "Memory Usage:"
free -m

echo "Disk Usage:"
df -h
```

**Python Script:**  
```python
import psutil

print("CPU Usage:", psutil.cpu_percent(interval=1), "%")
print("Memory Usage:", psutil.virtual_memory().percent, "%")
print("Disk Usage:", psutil.disk_usage('/').percent, "%")
```

---

### **4.2 Log Monitoring & Analysis (Python & Shell)**  

**Shell Script to Monitor Logs in Real-Time:**  
```bash
tail -f /var/log/syslog
```

**Python Script to Search for Errors in Logs:**  
```python
with open("/var/log/syslog") as log_file:
    for line in log_file:
        if "ERROR" in line:
            print(line)
```

---

## **5. CI/CD Automation**  

### **5.1 Jenkins Pipeline Script (Groovy)**  
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest tests/'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
```

---

## **6. Cloud Automation (AWS, Azure, GCP)**  

### **6.1 Automating AWS with Python (Boto3)**  

**List all EC2 Instances:**  
```python
import boto3

ec2 = boto3.client('ec2')
instances = ec2.describe_instances()

for reservation in instances["Reservations"]:
    for instance in reservation["Instances"]:
        print(instance["InstanceId"], instance["State"]["Name"])
```

---

## **7. Security & User Management**  

### **7.1 User & Permission Management (Shell)**  
```bash
#!/bin/bash
# Create a new user
useradd devopsuser
echo "User devopsuser created!"

# Set password for the user
echo "devopsuser:password123" | chpasswd

# Grant sudo access
usermod -aG sudo devopsuser
```

---

## **8. Backup & Disaster Recovery Automation**  

### **8.1 Backup Files & Databases (Shell & Python)**  

**Shell Script to Backup Files:**  
```bash
#!/bin/bash
tar -czf /backup/files_backup.tar.gz /var/www/html
echo "Backup completed!"
```

**Python Script to Backup MySQL Database:**  
```python
import os

os.system("mysqldump -u root -p'password' mydb > /backup/db_backup.sql")
print("Database backup completed!")
```

---

## **9. Scheduling Scripts for Automation**  

### **9.1 Using Cron Jobs (Linux)**  
Schedule a script to run daily at midnight:  
```sh
crontab -e
0 0 * * * /usr/bin/python3 /scripts/monitoring.py
```

### **9.2 Using Task Scheduler (Windows)**  
1. Open **Task Scheduler**  
2. Click **Create Basic Task**  
3. Set **Trigger** → **Daily**  
4. Set **Action** → **Start a Program** → `python script.py`  

---

## **10. Real-World Use Cases & Projects**  

| **Use Case** | **Tools & Scripts** |
|--------------|--------------------|
| **Server provisioning** | Terraform, Ansible, Shell |
| **Automating deployments** | Jenkins, GitHub Actions |
| **Monitoring system health** | Python (psutil), Shell |
| **Log analysis & alerts** | Python, ELK Stack |
| **Backup & disaster recovery** | Shell, Python (Boto3) |
| **Security & access management** | Shell, Ansible |
| **Cloud resource management** | AWS Boto3, Azure CLI |

---

## **Conclusion**  
✅ **Automating DevOps & system admin tasks** improves efficiency & scalability  
✅ **Python & Shell scripting** are essential for automation  
✅ **Cloud automation (AWS, Azure, GCP)** reduces manual work  
✅ **CI/CD pipelines ensure smooth deployments**  
✅ **Monitoring & backup scripts** enhance security & stability  

Would you like hands-on examples for a specific automation task?