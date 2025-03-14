# **AWS Load Balancer – Complete Guide**  

## **📌 What is a Load Balancer?**  
A **Load Balancer** is a service that automatically distributes incoming traffic across multiple servers (EC2 instances) to ensure **high availability, fault tolerance, and scalability** of applications.  

### **🚀 Why Use a Load Balancer?**  
✅ **Distributes traffic** to prevent overloading a single server.  
✅ **Improves availability** by rerouting traffic if a server fails.  
✅ **Enhances security** by hiding backend servers.  
✅ **Supports auto-scaling** by adjusting to traffic spikes.  

---

## **📌 Types of AWS Load Balancers**  

AWS provides **three types of Load Balancers** under **Elastic Load Balancing (ELB):**  

| **Type** | **Use Case** | **Protocol Supported** |
|----------|-------------|------------------------|
| **Application Load Balancer (ALB)** | Best for HTTP/HTTPS applications | HTTP, HTTPS |
| **Network Load Balancer (NLB)** | Best for high-performance TCP/UDP traffic | TCP, UDP, TLS |
| **Classic Load Balancer (CLB)** | Legacy load balancer (not recommended for new applications) | HTTP, HTTPS, TCP |

---

## **📌 How AWS Load Balancer Works?**  

1️⃣ **Client sends a request** → Hits the Load Balancer.  
2️⃣ **Load Balancer distributes traffic** → Based on health and rules.  
3️⃣ **Traffic reaches healthy EC2 instances** → Based on the chosen load-balancing algorithm.  
4️⃣ **EC2 instances process requests** and send responses back via the Load Balancer.  

---

## **📌 Key Features of AWS Load Balancers**  

| **Feature** | **Description** |
|------------|----------------|
| **Auto Scaling Integration** | Works with Auto Scaling to handle increased traffic. |
| **Health Checks** | Routes traffic only to healthy instances. |
| **Sticky Sessions** | Sends requests from the same client to the same instance. |
| **SSL Termination** | Handles HTTPS encryption to reduce the burden on backend servers. |
| **Cross-Zone Load Balancing** | Distributes traffic across multiple Availability Zones. |

---

## **📌 How to Set Up an AWS Load Balancer?**  

### **✅ Step 1: Create an Application Load Balancer (ALB)**
```bash
aws elbv2 create-load-balancer \
  --name my-alb \
  --subnets subnet-abc123 subnet-def456 \
  --security-groups sg-12345678 \
  --type application
```

### **✅ Step 2: Create a Target Group**
```bash
aws elbv2 create-target-group \
  --name my-target-group \
  --protocol HTTP --port 80 \
  --vpc-id vpc-12345678
```

### **✅ Step 3: Register EC2 Instances**
```bash
aws elbv2 register-targets \
  --target-group-arn arn:aws:elasticloadbalancing:region:account-id:targetgroup/my-target-group \
  --targets Id=i-12345678 Id=i-87654321
```

### **✅ Step 4: Create a Listener Rule**
```bash
aws elbv2 create-listener \
  --load-balancer-arn arn:aws:elasticloadbalancing:region:account-id:loadbalancer/app/my-alb \
  --protocol HTTP --port 80 \
  --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:region:account-id:targetgroup/my-target-group
```

---

# **📌 AWS Load Balancer Interview Questions & Answers**  

### **1️⃣ What is a Load Balancer?**  
💬 **Answer:**  
A **Load Balancer** is a networking service that **distributes incoming traffic** across multiple servers to ensure high availability, performance, and fault tolerance.  

---

### **2️⃣ What are the types of AWS Load Balancers?**  
💬 **Answer:**  
- **Application Load Balancer (ALB)** – Best for web applications using HTTP/HTTPS.  
- **Network Load Balancer (NLB)** – Best for high-speed, low-latency TCP/UDP traffic.  
- **Classic Load Balancer (CLB)** – Legacy load balancer (not recommended for new applications).  

---

### **3️⃣ How does an Application Load Balancer (ALB) work?**  
💬 **Answer:**  
- **ALB operates at Layer 7 (HTTP/HTTPS).**  
- **Routes requests based on URL paths** (e.g., `/api` → Backend A, `/images` → Backend B).  
- **Supports host-based routing** (e.g., `app.example.com` → Service A, `api.example.com` → Service B).  

---

### **4️⃣ What is the difference between ALB, NLB, and CLB?**  
💬 **Answer:**  

| **Feature** | **ALB** | **NLB** | **CLB** |
|------------|--------|--------|--------|
| **Protocol** | HTTP, HTTPS | TCP, UDP, TLS | HTTP, HTTPS, TCP |
| **Layer** | Layer 7 | Layer 4 | Layer 4 & 7 |
| **Use Case** | Web applications | High-performance apps | Legacy applications |
| **Routing** | Path-based, Host-based | Direct TCP routing | Basic routing |

---

### **5️⃣ What is a Target Group in AWS Load Balancer?**  
💬 **Answer:**  
A **Target Group** is a collection of backend servers (EC2 instances, Lambda functions, IPs) that **receive traffic** from the Load Balancer.  

---

### **6️⃣ What is the difference between Cross-Zone Load Balancing and Multi-AZ Load Balancing?**  
💬 **Answer:**  
✅ **Cross-Zone Load Balancing** – Distributes traffic **evenly** across all available instances in different **Availability Zones**.  
✅ **Multi-AZ Load Balancing** – Spreads traffic across instances in **different AWS regions** for **disaster recovery**.  

---

### **7️⃣ What is SSL Termination in Load Balancing?**  
💬 **Answer:**  
SSL Termination is when the Load Balancer **decrypts HTTPS traffic** before forwarding it to backend servers, reducing their CPU workload.  

---

### **8️⃣ What is Sticky Session in Load Balancing?**  
💬 **Answer:**  
A Sticky Session ensures that a user’s requests are always **sent to the same backend instance**, improving session persistence.  

Example:  
If a user logs in to an app, their session remains **on the same server** rather than jumping between instances.  

---

### **9️⃣ What happens if all EC2 instances behind an ALB fail health checks?**  
💬 **Answer:**  
- The Load Balancer **stops routing traffic** to unhealthy instances.  
- If **Auto Scaling** is enabled, AWS launches new instances.  
- If no healthy instances exist, the **Load Balancer returns a 503 error (Service Unavailable)**.  

---

### **🔟 How do you troubleshoot issues in an AWS Load Balancer?**  
💬 **Answer:**  
✅ **Check Target Group Health**  
```bash
aws elbv2 describe-target-health --target-group-arn <target-group-arn>
```
✅ **Verify Load Balancer Logs** in Amazon S3.  
✅ **Ensure Security Groups allow inbound traffic**.  
✅ **Check Route Tables** if using internal Load Balancers.  

---

## **📌 Summary of AWS Load Balancer**  

| **Feature** | **AWS Load Balancer** |
|------------|------------------|
| **Traffic Distribution** | ✅ Yes |
| **Auto Scaling Support** | ✅ Yes |
| **Health Checks** | ✅ Yes |
| **SSL Termination** | ✅ Yes |
| **Cross-Zone Balancing** | ✅ Yes |

🚀 **AWS Load Balancers are essential for handling high traffic, ensuring availability, and securing applications!**  

Would you like a **hands-on demo** on setting up an ALB?