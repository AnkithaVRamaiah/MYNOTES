## **AWS CloudFormation (CFT) – Complete Guide**  

AWS **CloudFormation (CFT)** is a service that allows you to **create and manage AWS resources using code**. Instead of manually setting up resources in the AWS console, you can define them in a template file and deploy them as a **stack**.  

---

## **📌 Why Use CloudFormation?**  
✅ **Infrastructure as Code (IaC)** – Automate and version control infrastructure  
✅ **Consistency** – Deploy the same setup across multiple environments  
✅ **Scalability** – Easily create, update, and delete AWS resources  
✅ **Cost Management** – Track and manage AWS resources efficiently  

---

## **📌 Key Components of CloudFormation**  

| **Component** | **Description** |
|--------------|----------------|
| **Template** | YAML or JSON file defining AWS resources |
| **Stack** | A collection of AWS resources deployed using a template |
| **Parameters** | User-defined values passed during stack creation |
| **Outputs** | Useful values (e.g., API URLs, instance IDs) returned after stack creation |
| **Mappings** | Define key-value pairs for different environments |
| **Conditions** | Deploy resources based on conditions (e.g., deploy in Prod but not Dev) |

---

## **📌 CloudFormation Template Structure**  

A basic **CloudFormation template** has the following sections:  

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: "AWS CloudFormation Example"

Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-cloudformation-bucket
```

### **🔹 Breakdown of the Template**
- `AWSTemplateFormatVersion` – Specifies the template version  
- `Description` – Describes what the template does  
- `Resources` – Defines AWS resources (like S3, EC2, VPC, etc.)  
- `Properties` – Specifies configurations for each resource  

---

## **📌 How to Deploy a CloudFormation Stack?**  

### **1️⃣ Using AWS Console**
1. Go to **AWS Console → CloudFormation**
2. Click **Create Stack → With New Resources**
3. Upload the **YAML/JSON template**
4. Enter parameters (if required)
5. Click **Create Stack**  

---

### **2️⃣ Using AWS CLI**  
Run this command to create a stack:  
```bash
aws cloudformation create-stack --stack-name MyStack --template-body file://template.yaml
```

To check stack status:  
```bash
aws cloudformation describe-stacks --stack-name MyStack
```

To delete a stack:  
```bash
aws cloudformation delete-stack --stack-name MyStack
```

---

## **📌 CloudFormation Features**  

| **Feature** | **Description** |
|------------|----------------|
| **Stack Update** | Modify existing resources without downtime |
| **Stack Deletion** | Deletes all resources in a stack |
| **Drift Detection** | Detects changes made outside CloudFormation |
| **Nested Stacks** | Reuse stacks within other stacks |
| **Change Sets** | Preview stack changes before applying |

---

## **📌 CloudFormation Interview Questions & Answers**  

### **1️⃣ What is AWS CloudFormation?**  
💬 **Answer:**  
AWS CloudFormation is an **Infrastructure as Code (IaC)** service that automates the provisioning of AWS resources using **YAML or JSON** templates. It helps in managing infrastructure efficiently by defining resources in a structured way.

---

### **2️⃣ What are the benefits of using CloudFormation?**  
💬 **Answer:**  
✔ **Automation** – Deploy AWS resources using templates  
✔ **Consistency** – Same setup across multiple environments  
✔ **Version Control** – Store templates in Git for tracking changes  
✔ **Time-Saving** – No need for manual resource creation  

---

### **3️⃣ What are CloudFormation stacks?**  
💬 **Answer:**  
A **stack** is a collection of AWS resources that are created, updated, and deleted **together** using a CloudFormation template.  

Example: If a template defines **EC2, S3, and RDS**, deploying the stack will create all three resources at once.

---

### **4️⃣ What are the different sections of a CloudFormation template?**  
💬 **Answer:**  
A CloudFormation template includes:
- **AWSTemplateFormatVersion** – Specifies template version  
- **Description** – Describes the template  
- **Resources** – Defines AWS resources  
- **Parameters** – Accepts user input for customization  
- **Mappings** – Stores key-value data  
- **Outputs** – Returns useful values after deployment  
- **Conditions** – Controls resource creation based on conditions  

---

### **5️⃣ What is a Nested Stack in CloudFormation?**  
💬 **Answer:**  
A **nested stack** is a **CloudFormation stack inside another stack**. It allows you to reuse templates, making management easier.  

Example: Instead of defining the same **VPC** in multiple templates, you can create a **VPC nested stack** and reuse it.

---

### **6️⃣ How do you update a CloudFormation stack?**  
💬 **Answer:**  
To update a stack, modify the template and run:  
```bash
aws cloudformation update-stack --stack-name MyStack --template-body file://updated_template.yaml
```
🔹 **Tip:** Always use **Change Sets** before updating to preview the impact.

---

### **7️⃣ What is Drift Detection in CloudFormation?**  
💬 **Answer:**  
Drift Detection checks if AWS resources have changed **outside CloudFormation**. It helps maintain consistency between actual resources and the template.

Run Drift Detection:  
```bash
aws cloudformation detect-stack-drift --stack-name MyStack
```

---

### **8️⃣ How do you pass parameters in CloudFormation?**  
💬 **Answer:**  
Parameters allow **user input** when creating stacks.

Example:  
```yaml
Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
```

Run with CLI:  
```bash
aws cloudformation create-stack --stack-name MyStack --template-body file://template.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.medium
```

---

### **9️⃣ How do you delete a CloudFormation stack?**  
💬 **Answer:**  
Deleting a stack removes **all AWS resources** created by the template.  

```bash
aws cloudformation delete-stack --stack-name MyStack
```

🚨 **Warning:** This action **cannot be undone**!

---

### **🔟 What is a Change Set in CloudFormation?**  
💬 **Answer:**  
A **Change Set** shows what will happen before updating a stack.

To create a change set:  
```bash
aws cloudformation create-change-set --stack-name MyStack --template-body file://updated_template.yaml --change-set-name MyChangeSet
```

To apply the change set:  
```bash
aws cloudformation execute-change-set --change-set-name MyChangeSet
```

---

## **📌 Summary of AWS CloudFormation**  

| **Feature** | **Description** |
|------------|----------------|
| **Infrastructure as Code (IaC)** | Automates AWS resource creation using YAML/JSON |
| **Stacks** | Group of AWS resources managed as one unit |
| **Drift Detection** | Detects manual changes outside CloudFormation |
| **Nested Stacks** | Reuse templates inside other stacks |
| **Change Sets** | Preview changes before updating a stack |

🚀 **CloudFormation helps DevOps teams automate AWS resource deployment efficiently!** Would you like a **hands-on lab** to practice CloudFormation?