## **AWS CloudWatch – Complete Guide**  

### **📌 What is AWS CloudWatch?**  
AWS CloudWatch is a **monitoring and observability service** that helps you track the performance and health of AWS resources like EC2, S3, Lambda, RDS, and more.  

It allows you to:  
✅ Collect **metrics** (CPU usage, memory, disk, etc.)  
✅ Set up **alarms** for alerts  
✅ Monitor **logs** from applications  
✅ Automatically **respond** to changes  

---

### **📌 Key Features of AWS CloudWatch**  

| **Feature** | **Description** |
|------------|----------------|
| **CloudWatch Metrics** | Tracks performance (CPU, RAM, Network, etc.) |
| **CloudWatch Logs** | Collects, monitors, and stores logs |
| **CloudWatch Alarms** | Sends alerts based on thresholds |
| **CloudWatch Dashboards** | Visualizes metrics in graphs |
| **CloudWatch Events** | Automates actions based on events |
| **CloudWatch Logs Insights** | Queries and analyzes logs |

---

## **📌 AWS CloudWatch Components**  

### **1️⃣ CloudWatch Metrics**  
- **Definition**: Data points collected from AWS resources.  
- **Example Metrics**:  
  - EC2: CPU utilization, Network traffic  
  - RDS: Read/Write IOPS  
  - Lambda: Invocation count, Duration  

**Example Command:**  
```bash
aws cloudwatch list-metrics --namespace "AWS/EC2"
```

---

### **2️⃣ CloudWatch Alarms**  
- **Definition**: Triggers alerts when a metric crosses a threshold.  
- **Example Use Case**:  
  - Alert if **CPU usage > 80%** for 5 minutes.  
  - Automatically **stop EC2** if it is idle for long.  

**Example Alarm (CLI):**  
```bash
aws cloudwatch put-metric-alarm --alarm-name "HighCPU" \
--metric-name CPUUtilization --namespace AWS/EC2 \
--statistic Average --period 300 --threshold 80 \
--comparison-operator GreaterThanThreshold \
--evaluation-periods 2 --alarm-actions arn:aws:sns:us-east-1:123456789012:MyTopic
```

---

### **3️⃣ CloudWatch Logs**  
- **Definition**: Stores logs from applications and AWS services.  
- **Example Use Case**:  
  - Monitor **Lambda function logs**.  
  - Track **application errors** from EC2 instances.  

**Example Command to View Logs:**  
```bash
aws logs describe-log-groups
```

---

### **4️⃣ CloudWatch Events & EventBridge**  
- **Definition**: **Triggers actions** based on AWS events.  
- **Example Use Case**:  
  - **Auto-start an EC2 instance** when a user logs in.  
  - **Invoke a Lambda function** on an S3 event.  

**Example Rule for Stopping EC2 at 7 PM:**  
```bash
aws events put-rule --name "StopEC2AtNight" --schedule-expression "cron(0 19 * * ? *)"
```

---

## **📌 AWS CloudWatch Interview Questions & Answers**  

### **1️⃣ What is AWS CloudWatch?**  
💬 **Answer:**  
AWS CloudWatch is a monitoring service that collects logs, metrics, and events from AWS resources. It helps track performance, troubleshoot issues, and automate responses.

---

### **2️⃣ What are CloudWatch Metrics?**  
💬 **Answer:**  
CloudWatch Metrics are numerical data points that track the performance of AWS resources. Example metrics include CPUUtilization for EC2 and RequestCount for an ALB.

---

### **3️⃣ How do CloudWatch Alarms work?**  
💬 **Answer:**  
CloudWatch Alarms monitor metrics and trigger notifications when a threshold is exceeded. They can send alerts via SNS, trigger Lambda functions, or auto-scale instances.

---

### **4️⃣ What is the difference between CloudWatch Logs and CloudTrail?**  
💬 **Answer:**  
| **Feature** | **CloudWatch Logs** | **AWS CloudTrail** |
|------------|-----------------|----------------|
| **Purpose** | Stores logs from AWS services and apps | Records API calls and user activities |
| **Example** | Lambda execution logs | Track IAM user login |
| **Retention** | Configurable | 90 days (default) |

---

### **5️⃣ How do you monitor EC2 memory usage in CloudWatch?**  
💬 **Answer:**  
By default, CloudWatch **does not track EC2 memory usage**. You must:  
1️⃣ Install the **CloudWatch Agent** on the EC2 instance.  
2️⃣ Configure the agent to collect memory usage.  
3️⃣ Send metrics to CloudWatch.  

**Example Command to Install CloudWatch Agent:**  
```bash
sudo yum install -y amazon-cloudwatch-agent
```

---

### **6️⃣ What is CloudWatch Logs Insights?**  
💬 **Answer:**  
CloudWatch Logs Insights is a **log analysis tool** that allows you to run queries on CloudWatch Logs to find issues.  

**Example Query:**  
```sql
fields @timestamp, @message
| sort @timestamp desc
| limit 5
```

---

### **7️⃣ How do you automate actions in CloudWatch?**  
💬 **Answer:**  
Use **CloudWatch Events (EventBridge)** to trigger actions.  
Example: **Stop an EC2 instance** at night using a scheduled event.

---

### **8️⃣ What is the retention period of CloudWatch Logs?**  
💬 **Answer:**  
CloudWatch Logs retention can be set from **1 day to indefinitely**.

**Example Command to Set Retention to 7 Days:**  
```bash
aws logs put-retention-policy --log-group-name my-log-group --retention-in-days 7
```

---

## **📌 AWS CloudWatch Pricing**  
💰 **Free Tier:**  
- 1M free CloudWatch Logs per month  
- 5GB free CloudWatch Metrics per month  
- 10 free CloudWatch Alarms  

💰 **Paid Services:**  
- Metrics: $0.30 per metric/month  
- Logs: $0.50 per GB ingested  
- Alarms: $0.10 per alarm/month  

---

## **📌 Summary of AWS CloudWatch**  

| **Feature** | **Description** |
|------------|----------------|
| **CloudWatch Metrics** | Monitors CPU, Memory, Disk, etc. |
| **CloudWatch Alarms** | Sends alerts if thresholds are exceeded |
| **CloudWatch Logs** | Stores and analyzes logs |
| **CloudWatch Events** | Automates actions based on AWS events |
| **CloudWatch Dashboards** | Visualizes metrics in graphs |

🚀 **AWS CloudWatch is essential for AWS monitoring and automation!** Do you want a **CloudWatch hands-on lab** to practice creating alarms and logs?