# **✅ 3. Dockerfile – Everything You Need to Know** 🚀  

A **Dockerfile** is a text file containing a set of instructions to **automate the creation of a Docker image**. Instead of manually setting up environments, a Dockerfile ensures **repeatability and consistency** across different systems.  

---

## **✔ What is a Dockerfile?**  

A **Dockerfile** is a blueprint for creating a Docker image. It contains a series of instructions that define:  
✅ The **base image** (OS)  
✅ The **dependencies** (libraries, software)  
✅ The **application code**  
✅ How to **run the application**  

### **📌 Example Dockerfile**
```dockerfile
# Use the official Python base image
FROM python:3.9  

# Set the working directory
WORKDIR /app  

# Copy application files into the container
COPY . .  

# Install dependencies
RUN pip install -r requirements.txt  

# Define environment variables
ENV PORT=5000  

# Specify the command to run the application
CMD ["python", "app.py"]
```
✅ This Dockerfile creates a **Python environment** with dependencies and runs `app.py`.  

---

## **✔ Dockerfile Instructions**  

Each Dockerfile has **instructions** that define what happens inside the image. Let’s go through the most important ones.  

### **1️⃣ `FROM` (Base Image)**  
The `FROM` instruction specifies the **base image** for the container.  
```dockerfile
FROM ubuntu:latest
```
✅ This uses the latest **Ubuntu** as the base.  
✅ **Every Dockerfile must start with `FROM`**.  

---

### **2️⃣ `WORKDIR` (Set Working Directory)**  
Defines the directory **inside the container** where commands will run.  
```dockerfile
WORKDIR /app
```
✅ Equivalent to `cd /app`.  

---

### **3️⃣ `COPY` (Copy Files from Host to Container)**  
Used to copy files/directories from the **host machine** to the **container**.  
```dockerfile
COPY source destination
```
✅ Example:  
```dockerfile
COPY app.py /app/app.py
```
✅ Copies `app.py` from the **host machine** to the **container's `/app/` directory**.  

---

### **4️⃣ `ADD` (Copy Files & Extract Archives)**  
Similar to `COPY`, but also supports:  
✔ Downloading files from URLs  
✔ Extracting compressed files (`.tar`, `.zip`)  
```dockerfile
ADD myfile.tar.gz /data
```
✅ Extracts `myfile.tar.gz` into `/data`.  

---

### **5️⃣ `RUN` (Execute Commands During Build)**  
Executes shell commands **during image creation** (when `docker build` runs).  
```dockerfile
RUN apt-get update && apt-get install -y nginx
```
✅ Installs `nginx` inside the container.  

---

### **6️⃣ `CMD` (Default Command to Run the Container)**  
Defines the **default command** executed when the container starts.  
```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```
✅ Runs `nginx` when the container starts.  
✅ **Only one `CMD` is allowed per Dockerfile**.  
✅ Can be **overridden** when running a container:  
```sh
docker run myapp bash
```
✅ This runs `bash` instead of `CMD`.  

---

### **7️⃣ `ENTRYPOINT` (Define Executable for the Container)**  
Similar to `CMD`, but **cannot be overridden**.  
```dockerfile
ENTRYPOINT ["python", "app.py"]
```
✅ Runs `python app.py` every time the container starts.  

🛑 **Difference Between CMD & ENTRYPOINT**  
| Feature | `CMD` | `ENTRYPOINT` |
|---------|------|-------------|
| Can be overridden? | ✅ Yes | ❌ No |
| Default usage | Running a command | Enforcing a command |

Example:  
```sh
docker run myimage echo "Hello"
```
✔ If `CMD ["python", "app.py"]` is used → **Overridden**  
✔ If `ENTRYPOINT ["python", "app.py"]` is used → **Not overridden**  

---

### **8️⃣ `EXPOSE` (Specify Ports)**  
Declares the **port number** the container listens on.  
```dockerfile
EXPOSE 5000
```
✅ This **does not** publish the port; it just documents it.  
✅ You still need to map it using `-p`:  
```sh
docker run -p 5000:5000 myapp
```
✅ Maps **port 5000 inside the container** to **port 5000 on the host**.  

---

### **9️⃣ `ENV` (Set Environment Variables)**  
Defines **environment variables** inside the container.  
```dockerfile
ENV APP_ENV=production
```
✅ Can be accessed inside the container:  
```sh
echo $APP_ENV
```
✅ **Can be overridden** when running the container:  
```sh
docker run -e APP_ENV=development myapp
```

---

### **🔟 `VOLUME` (Persistent Storage)**  
Creates a **mount point** for storing data persistently.  
```dockerfile
VOLUME /data
```
✅ Ensures that data in `/data` is **not lost** when the container stops.  
✅ Volumes **must be explicitly mounted** when running the container:  
```sh
docker run -v mydata:/data myapp
```

---

### **1️⃣1️⃣ `ARG` (Build-Time Variables)**  
Used for **passing values at build time** (not at runtime like `ENV`).  
```dockerfile
ARG APP_VERSION=1.0
```
✅ Can be set during build:  
```sh
docker build --build-arg APP_VERSION=2.0 -t myapp .
```
✅ Unlike `ENV`, `ARG` is **not available at runtime**.  

---

### **1️⃣2️⃣ `HEALTHCHECK` (Check if Container is Running Properly)**  
Defines a **health check** to monitor container status.  
```dockerfile
HEALTHCHECK --interval=30s --timeout=10s \
  CMD curl -f http://localhost:5000 || exit 1
```
✅ If the container is **unhealthy**, Docker can restart it.  

---

### **🛠 Full Example: Dockerfile for a Web App**  
```dockerfile
# Base image
FROM node:16

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy application files
COPY . .

# Set environment variable
ENV PORT=3000

# Expose port
EXPOSE 3000

# Start application
CMD ["node", "server.js"]
```
✅ **Creates a Node.js app**  
✅ **Installs dependencies**  
✅ **Runs `server.js` on port 3000**  

---

## **📌 Dockerfile Best Practices**  
✅ **Use a lightweight base image** (e.g., `alpine`, `slim` versions)  
✅ **Minimize the number of layers** (combine `RUN` commands)  
✅ **Use `.dockerignore`** to exclude unnecessary files  
✅ **Use multi-stage builds** to keep images small  

---

## **🔥 Interview Questions & Answers**  

### **1️⃣ What is a Dockerfile?**  
✅ **Answer:** A **Dockerfile** is a script containing instructions to **automate the creation of a Docker image**.  

### **2️⃣ What is the difference between `COPY` and `ADD`?**  
✅ **Answer:**  
- `COPY` **only copies files**  
- `ADD` **copies and extracts** compressed files (`.tar.gz`, `.zip`)  

### **3️⃣ What is the difference between `CMD` and `ENTRYPOINT`?**  
✅ **Answer:**  
| Feature | `CMD` | `ENTRYPOINT` |
|---------|------|-------------|
| Can be overridden? | ✅ Yes | ❌ No |
| Default usage | Running a command | Enforcing a command |

### **4️⃣ What is the purpose of `WORKDIR`?**  
✅ **Answer:** It sets the **working directory** inside the container.  

### **5️⃣ How do you reduce Docker image size?**  
✅ **Answer:**  
- Use **multi-stage builds**  
- Use **alpine** base images  
- Remove unnecessary files with `.dockerignore`  

---

## **🚀 Summary**  
✔ Dockerfile **automates image creation**  
✔ Contains **instructions** like `FROM`, `RUN`, `CMD`, `COPY`, etc.  
✔ **CMD vs ENTRYPOINT**: CMD can be overridden, ENTRYPOINT cannot  
✔ **Best practices**: Use **small base images**, minimize layers, and optimize builds  
