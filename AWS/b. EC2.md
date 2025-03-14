---
# **AWS EC2 (Elastic Compute Cloud)**  
---

## **1. What is AWS EC2?**  
AWS **EC2 (Elastic Compute Cloud)** is a web service that provides **resizable, scalable virtual machines (VMs)** in the cloud. It allows users to launch and manage **instances (virtual servers)** on demand, eliminating the need for physical hardware.  

Example: Instead of buying a physical server, you can rent an EC2 instance and pay only for the time you use it.  

---

## **2. Key Features of EC2**  
✔ **Scalability** – Easily increase or decrease instances based on demand.  
✔ **Multiple Instance Types** – Choose instances optimized for computing, memory, storage, or GPU.  
✔ **Security** – Uses **IAM roles, Security Groups, and Key Pairs** to secure instances.  
✔ **Elastic Load Balancing (ELB)** – Distributes traffic across multiple instances.  
✔ **Elastic Block Store (EBS)** – Provides **persistent** storage for EC2 instances.  
✔ **Auto Scaling** – Automatically adjusts the number of instances based on demand.  
✔ **Pay-as-You-Go** – Billed based on usage, saving costs.  

---

## **3. EC2 Components & Concepts**  

### **3.1 AMI (Amazon Machine Image)**  
- A **pre-configured template** used to launch EC2 instances.  
- Contains OS, software, and configurations.  
- Example: Amazon Linux, Ubuntu, Windows Server AMIs.  

### **3.2 Instance Types**  
AWS offers different instance types optimized for:  
- **General Purpose** (T-series: t3, t2) – Balanced compute, memory, and networking.  
- **Compute Optimized** (C-series: c5, c6g) – For high-performance computing.  
- **Memory Optimized** (R-series: r5, r6g) – For RAM-intensive applications like databases.  
- **Storage Optimized** (I-series, D-series) – High-speed storage workloads.  
- **GPU Optimized** (P-series, G-series) – For AI/ML and graphics processing.  

### **3.3 Security Groups**  
- Acts as a **virtual firewall** to control inbound/outbound traffic.  
- Rules are defined for allowing/restricting access.  

### **3.4 Elastic IP (EIP)**  
- A **static public IP address** assigned to an EC2 instance.  
- Useful when you need a **permanent IP** for an application.  

### **3.5 Key Pairs**  
- Used for **SSH authentication** to access EC2 instances securely.  
- Includes a **private key (stored by the user)** and a **public key (stored in AWS)**.  

### **3.6 Elastic Block Store (EBS)**  
- **Persistent storage** for EC2 instances.  
- Data is retained even if the instance is stopped or restarted.  

### **3.7 Load Balancers & Auto Scaling**  
- **Load Balancer (ELB)** distributes traffic across multiple EC2 instances.  
- **Auto Scaling** adds/removes instances based on demand, improving cost-efficiency.  

---

## **4. EC2 Pricing Models**  
AWS EC2 offers different pricing models based on usage:  

### **1. On-Demand Instances**  
- Pay for what you use.  
- Best for short-term workloads or unpredictable demand.  
- Example: Running a development/test environment.  

### **2. Reserved Instances**  
- Up to **75% cheaper** than on-demand.  
- Requires a **1 or 3-year commitment**.  
- Best for predictable workloads.  

### **3. Spot Instances**  
- **Up to 90% discount** but can be **terminated by AWS anytime** if the capacity is needed.  
- Best for **batch jobs and fault-tolerant applications**.  

### **4. Dedicated Hosts**  
- A **physical server** dedicated to one customer.  
- Used for **compliance and licensing requirements**.  

### **5. Savings Plans**  
- Flexible pricing model with **commitment-based discounts**.  
- Covers **EC2, Fargate, and Lambda**.  

---

## **5. EC2 Interview Questions and Answers**  

### **Q1. What is AWS EC2?**  
✅ **Answer:** AWS EC2 (Elastic Compute Cloud) is a service that provides **scalable virtual servers** in the cloud, allowing users to run applications without managing physical hardware.  

### **Q2. What are the different EC2 instance types?**  
✅ **Answer:**  
EC2 instances are categorized into:  
- **General Purpose** (T3, T2) – Balanced workloads.  
- **Compute Optimized** (C5, C6g) – High CPU performance.  
- **Memory Optimized** (R5, X1e) – Large RAM-intensive applications.  
- **Storage Optimized** (I3, D2) – High-speed disk performance.  
- **GPU Optimized** (P3, G4) – AI/ML and graphics processing.  

### **Q3. What is an AMI (Amazon Machine Image)?**  
✅ **Answer:**  
An AMI is a **pre-configured template** containing an operating system, applications, and settings used to launch EC2 instances.  

### **Q4. What is the difference between security groups and NACLs?**  
✅ **Answer:**  
- **Security Groups** → Work at the instance level (allow rules only).  
- **Network ACLs (NACLs)** → Work at the subnet level (allow and deny rules).  

### **Q5. What happens when you stop and start an EC2 instance?**  
✅ **Answer:**  
- **Stopping**: Shuts down the instance, but data on EBS remains intact.  
- **Starting**: Assigns a new **public IP** (unless an Elastic IP is attached).  

### **Q6. What is the difference between Elastic Block Store (EBS) and Instance Store?**  
✅ **Answer:**  
- **EBS** → Persistent, retains data even if the instance stops.  
- **Instance Store** → Temporary storage, data is lost if the instance is stopped.  

### **Q7. How do you secure an EC2 instance?**  
✅ **Answer:**  
1. Use **IAM roles** instead of storing credentials.  
2. Enable **Security Groups** to allow only necessary traffic.  
3. Use **Key Pairs** for SSH authentication.  
4. Enable **MFA** for users.  
5. Keep software **updated** and apply security patches.  

### **Q8. What are Spot Instances? When should you use them?**  
✅ **Answer:**  
Spot Instances offer **up to 90% discount** but can be terminated anytime. Best for:  
- Batch processing  
- Big data analytics  
- Machine learning workloads  

### **Q9. What is an Elastic IP, and why would you use it?**  
✅ **Answer:**  
An Elastic IP is a **static public IP** that remains the same even if the instance is restarted. It is used when a **fixed IP is required** for applications.  

### **Q10. How does Auto Scaling work?**  
✅ **Answer:**  
Auto Scaling **automatically adjusts** the number of EC2 instances based on demand, ensuring **high availability** and **cost efficiency**.  

---

## **6. Real-World Scenario-Based Questions**  

### **Q11. You need to migrate an EC2 instance from one region to another. How do you do it?**  
✅ **Answer:**  
1. Create an **AMI (Amazon Machine Image)** of the instance.  
2. Copy the AMI to the target region.  
3. Launch a new instance from the copied AMI.  

### **Q12. Your EC2 instance is slow. How do you troubleshoot performance issues?**  
✅ **Answer:**  
1. Check **CPU, Memory, Disk, and Network usage** in **Amazon CloudWatch**.  
2. Optimize instance size/type (scale up if needed).  
3. Check application logs for errors.  
4. Use **Auto Scaling** for handling high traffic.  

---

## **7. Conclusion**  
AWS EC2 is a powerful cloud computing service that provides **scalable, flexible virtual servers**. Understanding **instance types, pricing models, security best practices, and troubleshooting techniques** is key for interviews and real-world applications.  