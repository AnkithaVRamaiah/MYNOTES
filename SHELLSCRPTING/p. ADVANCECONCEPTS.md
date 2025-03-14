# **Advanced Shell Scripting Concepts & DevOps Use Cases**  

## **16. Advanced Shell Scripting Concepts**  

As you advance in shell scripting, you’ll work with **parallel processing**, **daemon scripts**, and **named pipes** to improve efficiency, performance, and automation.  

---

### **1️⃣ Parallel Processing in Shell Scripting (`&`, `wait`, `xargs -P`)**  

Parallel processing allows scripts to **execute multiple tasks simultaneously**, improving performance when dealing with large data or multiple processes.  

#### **Basic Parallel Execution using `&` and `wait`**
✅ **Example:** Running multiple tasks in the background  
```bash
#!/bin/bash

task1() { sleep 2; echo "Task 1 completed"; }
task2() { sleep 3; echo "Task 2 completed"; }
task3() { sleep 1; echo "Task 3 completed"; }

task1 &  # Runs in the background
task2 &  # Runs in the background
task3 &  # Runs in the background

wait  # Waits for all background tasks to complete
echo "All tasks completed!"
```
➡ `&` runs processes in the background, and `wait` ensures all are finished before proceeding.  

---

#### **Using `xargs -P` for Parallel Execution**
✅ **Example: Compressing multiple files in parallel**  
```bash
ls *.log | xargs -P 4 -I {} gzip {}
```
➡ `-P 4` allows 4 processes to run in parallel.  
➡ `xargs -I {}` processes each file independently.  

---

### **2️⃣ Creating Daemon Scripts (Background Services)**  

A **daemon script** is a shell script that runs continuously in the background, often used for monitoring tasks.  

#### **Creating a Simple Daemon**
✅ **Example: A script that monitors system logs in the background**  
```bash
#!/bin/bash

while true; do
  echo "$(date): Checking logs..." >> /var/log/custom_daemon.log
  sleep 10
done &
```
➡ Runs in the background and writes log entries every 10 seconds.  
➡ Use `nohup` to keep it running even after logout:  
```bash
nohup ./daemon_script.sh &
```

---

### **3️⃣ Working with Named Pipes (`mkfifo`)**  

Named pipes (`mkfifo`) allow inter-process communication by creating a **persistent communication channel** between processes.  

#### **Creating and Using a Named Pipe**  
✅ **Example:** Sending messages between processes  
```bash
mkfifo mypipe  # Create named pipe

# Process 1 (Runs in one terminal)
echo "Hello from process 1" > mypipe  

# Process 2 (Runs in another terminal)
cat < mypipe  # Output: Hello from process 1
```
➡ Named pipes allow two processes to communicate in real-time.  

---

## **17. Shell Scripting for DevOps**  

Shell scripting plays a crucial role in **DevOps** by automating tasks like **deployments, monitoring, and infrastructure management**.  

---

### **1️⃣ Automating Deployments with Shell Scripts**  

DevOps teams use shell scripts to **deploy applications** by automating steps like pulling code, building artifacts, and restarting services.  

✅ **Example: Deploying a web application**  
```bash
#!/bin/bash

echo "Pulling latest code..."
git pull origin main

echo "Building Docker image..."
docker build -t myapp:latest .

echo "Restarting application..."
docker stop myapp
docker run -d --name myapp -p 80:80 myapp:latest

echo "Deployment successful!"
```
➡ This script pulls the latest code, builds a Docker image, and redeploys the application.  

---

### **2️⃣ Monitoring System Health using Shell Scripts**  

A **system health check script** helps **monitor CPU, memory, and disk usage** to prevent failures.  

✅ **Example: System Health Check Script**  
```bash
#!/bin/bash

echo "System Health Report - $(date)"

echo "CPU Usage:"
top -b -n1 | grep "Cpu(s)"

echo "Memory Usage:"
free -h

echo "Disk Usage:"
df -h

echo "Uptime:"
uptime
```
➡ This script gathers system metrics and can be scheduled using **cron jobs**.  

---

### **3️⃣ Infrastructure Automation with Shell Scripts**  

Shell scripts can provision **servers, configure networks, and automate system setup**.  

✅ **Example: Creating an EC2 instance using AWS CLI**  
```bash
#!/bin/bash

aws ec2 run-instances \
    --image-id ami-12345678 \
    --instance-type t2.micro \
    --count 1 \
    --key-name my-key \
    --security-groups my-security-group \
    --region us-east-1

echo "EC2 instance launched!"
```
➡ Automates EC2 instance creation on AWS.  

---

## **Interview Questions & Answers**  

### **Parallel Processing**  
**Q1: What is the difference between `&` and `wait` in shell scripting?**  
✅ **A:** `&` runs a command in the background, while `wait` ensures all background tasks finish before continuing.  

**Q2: How does `xargs -P` improve parallel processing?**  
✅ **A:** `xargs -P` allows multiple tasks to run in parallel, increasing performance when processing large numbers of files.  

---

### **Daemon Scripts**  
**Q3: What is a daemon script, and how is it different from a regular script?**  
✅ **A:** A daemon script runs continuously in the background, whereas a regular script runs and exits.  

**Q4: How do you keep a daemon running after logging out?**  
✅ **A:** Use `nohup script.sh &` or `systemd` services for persistent execution.  

---

### **Named Pipes**  
**Q5: What is the purpose of `mkfifo` in shell scripting?**  
✅ **A:** `mkfifo` creates a named pipe that enables communication between processes.  

**Q6: How can you send and receive data through a named pipe?**  
✅ **A:** Write data using `echo "Message" > pipe_name` and read it using `cat < pipe_name`.  

---

### **DevOps Automation**  
**Q7: How can shell scripts be used in CI/CD pipelines?**  
✅ **A:** Shell scripts can automate build, test, and deployment tasks in Jenkins, GitHub Actions, or GitLab CI/CD.  

**Q8: What is a real-world example of using shell scripting for monitoring?**  
✅ **A:** A script that checks CPU, memory, and disk usage, then sends alerts if resource usage exceeds thresholds.  

---

## **Summary**  

✅ **Parallel Processing (`&`, `wait`, `xargs -P`)** improves script execution speed.  
✅ **Daemon Scripts** run continuously in the background for tasks like logging and monitoring.  
✅ **Named Pipes (`mkfifo`)** enable inter-process communication.  
✅ **Shell scripts automate deployments, monitor system health, and manage infrastructure.**  

Would you like a **real-world DevOps automation script** example?