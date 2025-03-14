# **AWS EKS (Elastic Kubernetes Service) – Complete Guide**  

## **📌 What is AWS EKS?**  
AWS **Elastic Kubernetes Service (EKS)** is a **fully managed Kubernetes service** that allows you to run, manage, and scale **Kubernetes clusters** on AWS without managing the control plane.  

### **🚀 Why Use AWS EKS?**  
✅ **Removes the need for managing Kubernetes control plane**  
✅ **Supports high availability and scalability**  
✅ **Integrates with AWS services like IAM, VPC, CloudWatch, and ALB**  
✅ **Compatible with standard Kubernetes tools (kubectl, Helm, etc.)**  

---

## **📌 AWS EKS Architecture**  

1️⃣ **EKS Control Plane** → Fully managed by AWS, responsible for managing cluster state.  
2️⃣ **Worker Nodes** → EC2 instances running Kubernetes worker nodes.  
3️⃣ **EKS Node Groups** → Groups of EC2 instances that automatically scale.  
4️⃣ **VPC & Networking** → Uses AWS VPC, security groups, and subnets.  
5️⃣ **Ingress & Load Balancing** → Uses AWS ALB/NLB for traffic routing.  
6️⃣ **IAM Authentication** → Integrates with AWS IAM for access control.  

---

## **📌 How AWS EKS Works? (Step-by-Step)**  

1️⃣ **Create an EKS Cluster** → AWS manages the control plane.  
2️⃣ **Launch Worker Nodes (EC2 Instances)** → Worker nodes register with the cluster.  
3️⃣ **Deploy Applications Using kubectl** → Deploy pods, services, and workloads.  
4️⃣ **Monitor and Scale** → Use CloudWatch, Prometheus, and Auto Scaling.  

---

## **📌 How to Deploy an EKS Cluster (Step-by-Step)**  

### **✅ 1. Create an EKS Cluster**
```bash
aws eks create-cluster --name my-cluster --role-arn arn:aws:iam::123456789012:role/EKS-Role --resources-vpc-config subnetIds=subnet-abcde12345,securityGroupIds=sg-01234abcd56789
```

### **✅ 2. Create a Node Group**
```bash
aws eks create-nodegroup --cluster-name my-cluster --nodegroup-name my-nodegroup --subnets subnet-abcde12345 --instance-types t3.medium
```

### **✅ 3. Configure kubectl to Access the Cluster**
```bash
aws eks update-kubeconfig --region us-east-1 --name my-cluster
```

### **✅ 4. Deploy an Application**
```bash
kubectl create deployment nginx-deployment --image=nginx
```

### **✅ 5. Expose the Deployment**
```bash
kubectl expose deployment nginx-deployment --type=LoadBalancer --port=80
```

---

## **📌 AWS EKS Pricing**  
💰 **EKS Control Plane Pricing** → **$0.10 per hour** for the cluster.  
💰 **EC2 Worker Nodes Pricing** → Pay for EC2 instances and EBS storage.  
💰 **Fargate Pricing** → Pay for CPU and memory usage per pod.  

---

# **📌 AWS EKS Interview Questions & Answers**  

### **1️⃣ What is AWS EKS?**  
💬 **Answer:**  
AWS **Elastic Kubernetes Service (EKS)** is a **fully managed Kubernetes service** that allows you to run containerized applications using Kubernetes on AWS.  

---

### **2️⃣ How does AWS EKS differ from ECS?**  
💬 **Answer:**  

| Feature | EKS (Kubernetes) | ECS (AWS Proprietary) |
|---------|-----------------|----------------------|
| **Orchestration** | Kubernetes-based | AWS native |
| **Flexibility** | Works across multiple cloud providers | AWS-specific |
| **Ease of Use** | Complex (Kubernetes required) | Simple and managed |
| **Best For** | Kubernetes workloads | AWS-only container workloads |

---

### **3️⃣ What is the difference between EKS and self-managed Kubernetes?**  
💬 **Answer:**  

| Feature | EKS | Self-Managed Kubernetes |
|---------|----|----------------------|
| **Control Plane** | Managed by AWS | You must manage it |
| **Scalability** | Auto scales | Manual scaling required |
| **Maintenance** | AWS handles updates | You handle updates |
| **Networking** | AWS VPC integration | Requires manual setup |

---

### **4️⃣ What are the components of AWS EKS?**  
💬 **Answer:**  
✅ **EKS Control Plane** – Managed by AWS, handles API requests and scaling.  
✅ **Worker Nodes** – EC2 instances that run Kubernetes workloads.  
✅ **EKS Node Groups** – Groups of EC2 instances for auto-scaling.  
✅ **VPC & Security Groups** – Manages networking and security.  
✅ **IAM Integration** – Uses IAM roles for access control.  

---

### **5️⃣ What is the difference between EKS on EC2 vs. EKS on Fargate?**  
💬 **Answer:**  

| Feature | EKS on EC2 | EKS on Fargate |
|---------|-----------|---------------|
| **Infrastructure Management** | Requires managing EC2 instances | Fully managed by AWS |
| **Cost** | Pay for EC2 instances | Pay per pod (CPU/memory) |
| **Scaling** | Manual or Auto Scaling | Auto scales with demand |
| **Use Case** | Best for large workloads | Best for microservices |

---

### **6️⃣ How does networking work in AWS EKS?**  
💬 **Answer:**  
- Uses **Amazon VPC** for networking.  
- Each pod gets a private **ENI (Elastic Network Interface)**.  
- Supports **AWS ALB, NLB, and Service Mesh** for communication.  
- **Security Groups and IAM roles** manage access.  

---

### **7️⃣ How does IAM authentication work in EKS?**  
💬 **Answer:**  
- EKS uses **IAM roles** to control access to Kubernetes resources.  
- IAM users and roles are mapped to **Kubernetes RBAC (Role-Based Access Control)**.  
- Use **aws-auth ConfigMap** to map IAM roles to Kubernetes users.  

Example:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: aws-auth
  namespace: kube-system
data:
  mapRoles: |
    - rolearn: arn:aws:iam::123456789012:role/KubernetesAdmin
      username: admin
      groups:
        - system:masters
```

---

### **8️⃣ What tools can be used to monitor EKS?**  
💬 **Answer:**  
✅ **Amazon CloudWatch** – Monitors cluster logs.  
✅ **AWS X-Ray** – Traces application requests.  
✅ **Prometheus & Grafana** – Open-source monitoring.  
✅ **AWS CloudTrail** – Tracks API calls.  

---

### **9️⃣ How does EKS Auto Scaling work?**  
💬 **Answer:**  
AWS EKS supports multiple types of auto-scaling:  
- **Cluster Auto Scaling (CAS)** → Adjusts EC2 nodes based on demand.  
- **Horizontal Pod Autoscaler (HPA)** → Adjusts the number of pods.  
- **Vertical Pod Autoscaler (VPA)** → Adjusts CPU/memory for pods.  

Example: Enable HPA for a deployment:
```bash
kubectl autoscale deployment nginx-deployment --cpu-percent=50 --min=1 --max=10
```

---

### **🔟 What are the best practices for deploying applications on EKS?**  
💬 **Answer:**  
✅ Use **Fargate** for serverless applications.  
✅ Use **IAM roles** for security and least privilege.  
✅ Implement **autoscaling** with HPA and CAS.  
✅ Use **CloudWatch and Prometheus** for monitoring.  
✅ Use **Network Policies** to control traffic between pods.  

---

## **📌 Summary of AWS EKS**  

| **Feature** | **Description** |
|------------|----------------|
| **Fully Managed** | AWS manages Kubernetes control plane |
| **Highly Scalable** | Auto scales based on demand |
| **Secure** | Integrates with IAM, VPC, and Security Groups |
| **Works with AWS Services** | Supports ALB, CloudWatch, IAM, and more |
| **Multi-Cloud Compatible** | Works across AWS, on-prem, and hybrid |

🚀 **AWS EKS is the best choice for running Kubernetes workloads on AWS without managing infrastructure!**  

Would you like a **hands-on demo** on deploying an application on EKS?