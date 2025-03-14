## **AWS Lambda – Complete Guide**  

### **📌 What is AWS Lambda?**  
AWS Lambda is a **serverless compute service** that allows you to run code **without provisioning or managing servers**. You just upload your code, and AWS handles execution, scaling, and maintenance.  

🚀 **Key Benefits:**  
✅ No servers to manage  
✅ Auto-scales based on demand  
✅ Pay only for execution time  

---

## **📌 How AWS Lambda Works?**  
1️⃣ **Trigger** → An event from S3, API Gateway, DynamoDB, etc.  
2️⃣ **Execute** → AWS runs the function with allocated resources.  
3️⃣ **Scale** → AWS automatically scales the function.  
4️⃣ **Terminate** → The function stops when execution is complete.  

---

## **📌 AWS Lambda Components**  

| **Component** | **Description** |
|--------------|----------------|
| **Function** | The code that gets executed |
| **Trigger** | The AWS service that invokes the function (S3, API Gateway, etc.) |
| **Execution Role** | IAM Role that grants permission to access other AWS services |
| **Concurrency** | Number of executions happening at the same time |
| **Timeout** | Max time (default: 3 sec, max: 15 min) |
| **Memory** | Adjustable from 128MB to 10GB |

---

## **📌 Supported Programming Languages**  
AWS Lambda supports:  
✅ **Python**  
✅ **Node.js**  
✅ **Java**  
✅ **Go**  
✅ **C#**  
✅ **Ruby**  

---

## **📌 AWS Lambda Use Cases**  
💡 **1. Image Processing** → Trigger Lambda when an image is uploaded to S3.  
💡 **2. API Backend** → Use Lambda with API Gateway for a **serverless API**.  
💡 **3. Event Processing** → Process logs from CloudWatch, DynamoDB streams.  
💡 **4. Automation** → Auto-start EC2 when an IAM user logs in.  

---

## **📌 Example: Creating a Lambda Function**  

### **Using AWS CLI**  
```bash
aws lambda create-function --function-name MyLambdaFunction \
--runtime python3.8 --role arn:aws:iam::123456789012:role/lambda-execution-role \
--handler lambda_function.lambda_handler --zip-file fileb://function.zip
```

### **Python Example (S3 Triggered Lambda)**  
```python
import json

def lambda_handler(event, context):
    print("Event received:", json.dumps(event))
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

---

## **📌 AWS Lambda Pricing**  
💰 **Free Tier:**  
- 1M requests/month free  
- 400,000 GB-seconds free  

💰 **Paid Services:**  
- $0.20 per **1 million requests**  
- $0.00001667 per GB-second  

---

## **📌 AWS Lambda Interview Questions & Answers**  

### **1️⃣ What is AWS Lambda?**  
💬 **Answer:**  
AWS Lambda is a **serverless compute service** that automatically runs code in response to events without managing servers.  

---

### **2️⃣ What are the advantages of AWS Lambda?**  
💬 **Answer:**  
✅ No need to manage servers  
✅ Auto-scaling  
✅ Pay-per-use pricing  
✅ Supports multiple languages  

---

### **3️⃣ What triggers AWS Lambda?**  
💬 **Answer:**  
AWS Lambda can be triggered by:  
- S3 (Object Uploads)  
- API Gateway (HTTP Requests)  
- DynamoDB Streams (Data Changes)  
- CloudWatch Events (Scheduled Jobs)  

---

### **4️⃣ What is the maximum execution time of AWS Lambda?**  
💬 **Answer:**  
The **default timeout is 3 seconds**, and the **maximum timeout is 15 minutes**.  

---

### **5️⃣ How is AWS Lambda billed?**  
💬 **Answer:**  
Lambda charges based on:  
- **Requests:** $0.20 per million requests  
- **Duration:** $0.00001667 per GB-second  

---

### **6️⃣ How does AWS Lambda scale?**  
💬 **Answer:**  
Lambda **scales automatically** by running multiple instances **in parallel**.  

---

### **7️⃣ What is AWS Lambda cold start?**  
💬 **Answer:**  
A **cold start** occurs when AWS spins up a new instance of a Lambda function, which **adds latency** to the first request.  

✅ **Ways to Reduce Cold Starts:**  
- Use **provisioned concurrency**  
- Keep functions **small & optimized**  
- Use **lighter runtime (Python, Node.js)**  

---

### **8️⃣ Can AWS Lambda connect to a VPC?**  
💬 **Answer:**  
Yes, Lambda can run inside a **VPC** to access private resources like RDS, EC2, or internal APIs.  

✅ Enable VPC access when configuring Lambda.  

---

### **9️⃣ How do you monitor AWS Lambda?**  
💬 **Answer:**  
You can use:  
- **CloudWatch Logs** → To view execution logs  
- **CloudWatch Metrics** → To monitor execution time, memory usage, and errors  
- **AWS X-Ray** → For tracing function execution  

---

### **🔟 What is Lambda@Edge?**  
💬 **Answer:**  
Lambda@Edge allows Lambda functions to run at **AWS CloudFront locations** to process content closer to users (e.g., caching, modifying requests).  

---

## **📌 Summary of AWS Lambda**  

| **Feature** | **Description** |
|------------|----------------|
| **Serverless** | No need to manage servers |
| **Auto-Scaling** | Scales automatically based on traffic |
| **Multiple Triggers** | S3, API Gateway, DynamoDB, CloudWatch |
| **Supports Multiple Languages** | Python, Node.js, Java, Go, C#, Ruby |
| **Cost-Efficient** | Pay only for execution time |

🚀 **AWS Lambda is a game-changer for cloud automation!** Do you want a **hands-on lab** to practice Lambda function creation?