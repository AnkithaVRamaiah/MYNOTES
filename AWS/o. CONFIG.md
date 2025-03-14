# **AWS Config – Complete Guide**  

## **📌 What is AWS Config?**  
AWS **Config** is a service that continuously monitors, records, and evaluates the **configuration of AWS resources**. It helps track changes, check compliance, and troubleshoot issues in your AWS environment.  

### **🚀 Why Use AWS Config?**  
✅ **Tracks AWS resource changes** over time.  
✅ **Ensures compliance** with security policies.  
✅ **Detects misconfigurations** in real time.  
✅ **Provides audit logs** for governance and troubleshooting.  

---

## **📌 How AWS Config Works?**  

1️⃣ **AWS Config records configuration changes** of AWS resources.  
2️⃣ **Stores configuration snapshots** in Amazon S3.  
3️⃣ **Evaluates changes against AWS Config rules** (e.g., security policies).  
4️⃣ **Sends alerts via Amazon SNS** if non-compliant configurations are detected.  

---

## **📌 AWS Config Features**  

| **Feature** | **Description** |
|------------|----------------|
| **Configuration Tracking** | Records changes in AWS resources over time. |
| **Compliance Checks** | Evaluates resource settings against defined rules. |
| **Historical Data** | Provides a history of all AWS resource configurations. |
| **Automated Remediation** | Fixes misconfigurations automatically. |
| **Integration** | Works with AWS Security Hub, CloudTrail, and Lambda. |

---

## **📌 How to Set Up AWS Config?**  

### **✅ Step 1: Enable AWS Config**
```bash
aws configservice put-configuration-recorder \
  --configuration-recorder name=default,roleARN=arn:aws:iam::123456789012:role/AWSConfigRole
```

### **✅ Step 2: Define AWS Config Rules**
```bash
aws configservice put-config-rule \
  --config-rule file://my-config-rule.json
```
Example JSON rule (checks if S3 buckets are encrypted):
```json
{
  "ConfigRuleName": "s3-bucket-encryption-check",
  "Scope": {
    "ComplianceResourceTypes": ["AWS::S3::Bucket"]
  },
  "Source": {
    "Owner": "AWS",
    "SourceIdentifier": "S3_BUCKET_SERVER_SIDE_ENCRYPTION_ENABLED"
  }
}
```

### **✅ Step 3: View Compliance Status**
```bash
aws configservice describe-compliance-by-config-rule
```

---

# **📌 AWS Config Interview Questions & Answers**  

### **1️⃣ What is AWS Config?**  
💬 **Answer:**  
AWS **Config** is a service that monitors, records, and audits AWS resource configurations to **detect misconfigurations and ensure compliance** with security policies.  

---

### **2️⃣ How does AWS Config help in compliance?**  
💬 **Answer:**  
- AWS Config **evaluates resources** against pre-defined rules.  
- If a resource is **non-compliant**, it sends alerts via SNS.  
- Maintains **historical configuration data** for audits.  

---

### **3️⃣ What are AWS Config Rules?**  
💬 **Answer:**  
AWS Config Rules are **pre-defined checks** that assess whether AWS resources comply with best practices.  
Example:  
✅ Ensuring **S3 bucket encryption**.  
✅ Checking if **EC2 instances have IAM roles attached**.  

---

### **4️⃣ How does AWS Config integrate with AWS Lambda?**  
💬 **Answer:**  
AWS Config can trigger **AWS Lambda** to **automatically remediate non-compliant resources**.  
Example: If an **S3 bucket is not encrypted**, a Lambda function can be triggered to **enable encryption automatically**.  

---

### **5️⃣ What is the difference between AWS Config and AWS CloudTrail?**  
💬 **Answer:**  
| **Feature** | **AWS Config** | **AWS CloudTrail** |
|------------|--------------|----------------|
| **Purpose** | Monitors resource configurations | Tracks API activity (who did what) |
| **Change Tracking** | ✅ Yes | ✅ Yes |
| **Compliance Checking** | ✅ Yes | ❌ No |
| **Real-time Alerts** | ✅ Yes | ❌ No |
| **Use Case** | Security & compliance | Auditing & governance |

---

### **6️⃣ How do you remediate non-compliant resources in AWS Config?**  
💬 **Answer:**  
✅ **Manual Fix** – Fix the resource manually.  
✅ **AWS Lambda Automation** – Use Lambda to fix misconfigurations.  
✅ **AWS Systems Manager Automation** – Run SSM documents for automated remediation.  

---

### **7️⃣ What is the pricing for AWS Config?**  
💬 **Answer:**  
- **$0.003 per configuration item recorded**.  
- **$2 per active AWS Config Rule per region per month**.  
- **$0.001 per evaluation of custom Config Rules**.  

---

### **8️⃣ How do you enable AWS Config in multiple accounts?**  
💬 **Answer:**  
- Use **AWS Organizations** to enable AWS Config in all accounts.  
- Store configuration snapshots in **a central S3 bucket**.  

Example:
```bash
aws configservice start-configuration-recorder \
  --configuration-recorder-name default
```

---

### **9️⃣ What types of AWS Config rules are available?**  
💬 **Answer:**  
✅ **Managed Rules** – Pre-defined AWS compliance rules.  
✅ **Custom Rules** – Custom rules using AWS Lambda.  

Example Managed Rule:
```json
{
  "SourceIdentifier": "S3_BUCKET_PUBLIC_READ_PROHIBITED"
}
```

---

### **🔟 What are best practices for AWS Config?**  
💬 **Answer:**  
✅ Enable **AWS Config across all AWS accounts**.  
✅ Store **config snapshots in S3** for auditing.  
✅ Set up **SNS alerts** for non-compliant resources.  
✅ Use **AWS Lambda for auto-remediation**.  
✅ Integrate AWS Config with **AWS Security Hub** for better security insights.  

---

## **📌 Summary of AWS Config**  

| **Feature** | **AWS Config** |
|------------|--------------|
| **Monitors AWS Resources** | ✅ Yes |
| **Tracks Changes Over Time** | ✅ Yes |
| **Ensures Compliance** | ✅ Yes |
| **Sends Alerts for Misconfigurations** | ✅ Yes |
| **Automated Remediation** | ✅ Yes |

🚀 **AWS Config is an essential service for tracking, auditing, and ensuring security compliance in AWS!**  

Would you like a **real-time demo** on setting up AWS Config?