# **AWS CloudFront – Complete Guide**  

## **📌 What is AWS CloudFront?**  
AWS CloudFront is a **Content Delivery Network (CDN)** service that **delivers content faster** by caching it at **edge locations** worldwide.  

### **🚀 Why Use CloudFront?**  
✅ Reduces latency (loads content faster)  
✅ Improves website performance  
✅ Secure content delivery  
✅ Reduces load on the origin server  

---

## **📌 How AWS CloudFront Works?**  

1️⃣ **User Requests Content** → A user requests an image, video, or web page.  
2️⃣ **Nearest Edge Location** → CloudFront routes the request to the closest **edge location**.  
3️⃣ **Cache Check**:  
   - If the content is **cached**, it is delivered immediately.  
   - If not cached, CloudFront fetches it from the **origin server** (S3, EC2, ALB, etc.) and **caches** it for future requests.  
4️⃣ **Content is Delivered** → Faster and more efficiently!  

---

## **📌 CloudFront Key Components**  

| **Component**  | **Description**  |
|--------------|----------------|
| **Edge Locations**  | Servers worldwide that cache content closer to users.  |
| **Origin Server**  | The original source of content (S3, EC2, or external HTTP server).  |
| **Distribution**  | The setup in CloudFront that defines how content is delivered.  |
| **Cache Behavior**  | Controls how requests are processed (e.g., caching duration, HTTP methods).  |
| **TTL (Time to Live)**  | Determines how long an object stays cached.  |

---

## **📌 AWS CloudFront Use Cases**  

💡 **1. Website Acceleration** → Faster loading of web pages and APIs.  
💡 **2. Video Streaming** → Stream videos globally with reduced buffering.  
💡 **3. Security & DDoS Protection** → Protects websites from attacks.  
💡 **4. API Acceleration** → Reduces response times for API requests.  

---

## **📌 How to Create a CloudFront Distribution (Step-by-Step)**  

### **✅ Using AWS Management Console:**  
1️⃣ Go to **AWS CloudFront Console**.  
2️⃣ Click **"Create Distribution"**.  
3️⃣ Select **Origin Type** (S3, EC2, or Custom).  
4️⃣ Configure **Cache Settings** and **Distribution Settings**.  
5️⃣ Click **"Create"** → CloudFront will generate a **CDN URL**.  

### **✅ Using AWS CLI:**  
```bash
aws cloudfront create-distribution --origin-domain-name mybucket.s3.amazonaws.com \
--default-root-object index.html
```

---

## **📌 CloudFront Pricing**  

💰 **Pricing depends on:**  
- Data Transfer Out (higher usage = lower cost)  
- Number of HTTP/HTTPS requests  
- Edge location region  

💰 **Free Tier:**  
✅ 1 TB of data transfer per month  
✅ 10 million HTTP/HTTPS requests per month  

---

# **📌 CloudFront Interview Questions & Answers**  

### **1️⃣ What is AWS CloudFront?**  
💬 **Answer:**  
AWS CloudFront is a **content delivery network (CDN)** that caches content at **edge locations** worldwide to reduce latency and improve performance.  

---

### **2️⃣ What are the benefits of using CloudFront?**  
💬 **Answer:**  
✅ **Faster Content Delivery** → Low latency  
✅ **Caching & Cost Savings** → Reduces load on the origin server  
✅ **DDoS Protection** → Secure access and threat protection  
✅ **Streaming Support** → Delivers videos and live streams  

---

### **3️⃣ What is an Edge Location?**  
💬 **Answer:**  
Edge locations are **global data centers** where CloudFront **caches content** for faster delivery.  

---

### **4️⃣ What is the difference between CloudFront and S3?**  
💬 **Answer:**  
| **Feature** | **CloudFront** | **S3** |
|------------|--------------|------|
| **Purpose** | Content Delivery Network (CDN) | Storage Service |
| **Caching** | Yes, at Edge Locations | No |
| **Speed** | Faster due to caching | Slower for global access |
| **Security** | Supports Signed URLs & Access Controls | Supports Bucket Policies & IAM |

---

### **5️⃣ How does CloudFront improve website speed?**  
💬 **Answer:**  
CloudFront caches static and dynamic content at **edge locations**, reducing the distance between users and the content, which speeds up loading times.  

---

### **6️⃣ What are Signed URLs and Signed Cookies?**  
💬 **Answer:**  
They **restrict access** to content:  
✅ **Signed URLs** → Provide temporary access to specific files.  
✅ **Signed Cookies** → Allow access to multiple files via authentication.  

---

### **7️⃣ How does CloudFront handle cache expiration?**  
💬 **Answer:**  
CloudFront uses **TTL (Time to Live)** settings to define how long an object remains cached. You can set a custom TTL or use Cache-Control headers.  

---

### **8️⃣ How can CloudFront be secured?**  
💬 **Answer:**  
✅ **Use HTTPS** for secure data transfer.  
✅ **Enable AWS Shield** for DDoS protection.  
✅ **Restrict access** with Signed URLs and IAM policies.  

---

### **9️⃣ What are CloudFront Distributions?**  
💬 **Answer:**  
A **distribution** defines how content is delivered and includes:  
- **Web Distribution** → For websites, APIs, and HTTP content.  
- **RTMP Distribution (Deprecated)** → For streaming media.  

---

### **🔟 What happens if the content is not in the CloudFront cache?**  
💬 **Answer:**  
If the content is **not cached**, CloudFront fetches it from the **origin server**, delivers it to the user, and caches it for future requests.  

---

# **📌 Summary of AWS CloudFront**  

| **Feature** | **Description** |
|------------|----------------|
| **Content Delivery** | Caches content at global edge locations |
| **Reduces Latency** | Faster access to websites, videos, and APIs |
| **Security** | DDoS protection, signed URLs, HTTPS support |
| **Cost-Effective** | Reduces bandwidth costs with caching |
| **Scalability** | Automatically handles traffic spikes |

🚀 **CloudFront makes websites, APIs, and media streaming faster & more secure!** Do you need a **hands-on tutorial** to deploy CloudFront with S3?