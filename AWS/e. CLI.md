
## **AWS CLI (Command Line Interface) – Complete Guide**  

AWS CLI (Command Line Interface) is a tool that allows you to interact with AWS services using commands instead of the AWS Management Console. It helps automate tasks, manage AWS resources, and run scripts for efficient cloud operations.  

---

## **📌 Why Use AWS CLI?**  
✅ **Automation** – Run scripts to automate repetitive tasks.  
✅ **Faster Operations** – Perform actions without navigating the AWS Console.  
✅ **Manage Multiple AWS Services** – EC2, S3, IAM, Lambda, RDS, and more.  
✅ **Access AWS from Anywhere** – Works on Linux, macOS, and Windows.  

---

## **📌 Installing AWS CLI**  

1️⃣ **Windows:** Download and install from [AWS CLI Installer](https://aws.amazon.com/cli/)  
2️⃣ **Linux/macOS:** Run:  
   ```bash
   curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
   sudo installer -pkg AWSCLIV2.pkg -target /
   ```
3️⃣ **Verify Installation:**  
   ```bash
   aws --version
   ```
   **Output Example:**  
   ```
   aws-cli/2.10.0 Python/3.9.11 Linux/x86_64
   ```

---

## **📌 Configuring AWS CLI**  

Before using AWS CLI, you need to **set up AWS credentials**:  

```bash
aws configure
```
You will be prompted to enter:  
```
AWS Access Key ID [None]: XXXXXXXXXX
AWS Secret Access Key [None]: XXXXXXXXXX
Default region name [None]: us-east-1
Default output format [None]: json
```

✅ **Where to get AWS credentials?** – In AWS Console → **IAM → Users → Security Credentials**  

---

## **📌 Basic AWS CLI Commands**  

### **1️⃣ S3 (Simple Storage Service)**
- **List all S3 buckets:**  
  ```bash
  aws s3 ls
  ```
- **Create a new S3 bucket:**  
  ```bash
  aws s3 mb s3://my-new-bucket
  ```
- **Upload a file to S3 bucket:**  
  ```bash
  aws s3 cp myfile.txt s3://my-new-bucket/
  ```
- **Download a file from S3:**  
  ```bash
  aws s3 cp s3://my-new-bucket/myfile.txt .
  ```
- **Delete an S3 bucket:**  
  ```bash
  aws s3 rb s3://my-new-bucket --force
  ```

---

### **2️⃣ EC2 (Elastic Compute Cloud)**
- **List all EC2 instances:**  
  ```bash
  aws ec2 describe-instances
  ```
- **Start an EC2 instance:**  
  ```bash
  aws ec2 start-instances --instance-ids i-0abcd1234efgh5678
  ```
- **Stop an EC2 instance:**  
  ```bash
  aws ec2 stop-instances --instance-ids i-0abcd1234efgh5678
  ```
- **Terminate an EC2 instance:**  
  ```bash
  aws ec2 terminate-instances --instance-ids i-0abcd1234efgh5678
  ```

---

### **3️⃣ IAM (Identity & Access Management)**
- **List all IAM users:**  
  ```bash
  aws iam list-users
  ```
- **Create a new IAM user:**  
  ```bash
  aws iam create-user --user-name devops-user
  ```
- **Attach policy to IAM user:**  
  ```bash
  aws iam attach-user-policy --user-name devops-user --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
  ```

---

### **4️⃣ VPC (Virtual Private Cloud)**
- **List all VPCs:**  
  ```bash
  aws ec2 describe-vpcs
  ```
- **Create a new VPC:**  
  ```bash
  aws ec2 create-vpc --cidr-block 10.0.0.0/16
  ```

---

### **5️⃣ Lambda (Serverless Functions)**
- **List all Lambda functions:**  
  ```bash
  aws lambda list-functions
  ```
- **Invoke a Lambda function:**  
  ```bash
  aws lambda invoke --function-name MyLambdaFunction output.json
  ```

---

## **📌 AWS CLI Interview Questions & Answers**  

### **1️⃣ What is AWS CLI?**  
💬 **Answer:**  
AWS CLI (Command Line Interface) is a tool that helps users manage AWS services through commands instead of the AWS Console. It enables automation, faster execution, and integration with scripts.  

---

### **2️⃣ How do you install AWS CLI?**  
💬 **Answer:**  
- **Windows:** Download and install from AWS CLI official website.  
- **Linux/macOS:** Use the `curl` command to download and install.  
- **Verify installation:** Run `aws --version`.  

---

### **3️⃣ How do you configure AWS CLI?**  
💬 **Answer:**  
Run the command:  
```bash
aws configure
```
Enter **Access Key, Secret Key, Region, and Output Format (JSON, Table, or Text)**.  

---

### **4️⃣ What are the output formats available in AWS CLI?**  
💬 **Answer:**  
- **json** (default)  
- **table** (human-readable format)  
- **text** (plain text format)  

Example usage:  
```bash
aws ec2 describe-instances --output table
```

---

### **5️⃣ What is the difference between AWS CLI and SDK?**  
| Feature | AWS CLI | AWS SDK |
|---------|--------|--------|
| **Usage** | Command-line based | Code-based (Python, Java, etc.) |
| **Best For** | Quick automation, scripting | Application development |
| **Languages** | Bash, Shell | Python (Boto3), Java, Node.js |

---

### **6️⃣ How do you list all running EC2 instances using AWS CLI?**  
💬 **Answer:**  
```bash
aws ec2 describe-instances --query "Reservations[].Instances[?State.Name=='running'].InstanceId"
```
This command filters only **running** instances.  

---

### **7️⃣ How do you copy a file from your local system to S3?**  
💬 **Answer:**  
```bash
aws s3 cp myfile.txt s3://my-bucket-name/
```
This uploads `myfile.txt` to the specified S3 bucket.  

---

### **8️⃣ How do you delete an S3 bucket using AWS CLI?**  
💬 **Answer:**  
```bash
aws s3 rb s3://my-bucket-name --force
```
🚨 **Warning:** `--force` permanently deletes the bucket **and all its contents**!  

---

### **9️⃣ How do you create an IAM user using AWS CLI?**  
💬 **Answer:**  
```bash
aws iam create-user --user-name devops-user
```
This creates a new IAM user named `devops-user`.  

---

### **🔟 What is the difference between `aws s3 cp` and `aws s3 sync`?**  
| Command | Purpose |
|---------|---------|
| `aws s3 cp` | Copies a single file/folder to S3 |
| `aws s3 sync` | Syncs entire directories (only new/changed files) |

✅ Example:  
```bash
aws s3 sync ./local-folder s3://my-bucket-name/
```
This **syncs** all files in `local-folder` to S3.  

---

## **📌 Summary**  

| **Feature** | **Details** |
|------------|------------|
| **Purpose** | Manage AWS services via command line |
| **Installation** | Windows, macOS, Linux |
| **Configuration** | `aws configure` (access key, region, output format) |
| **Common Services** | S3, EC2, IAM, VPC, Lambda |
| **Automation** | Can be used in shell scripts |
| **Security** | Uses IAM roles and credentials |