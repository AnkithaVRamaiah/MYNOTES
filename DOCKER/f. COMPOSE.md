# **Docker Compose - Everything You Need to Know**  

Docker Compose is a tool that helps **manage multiple containers** using a **single YAML file**. Instead of running multiple `docker run` commands manually, **Docker Compose automates the process** with `docker-compose.yml`.  

---

## **1️⃣ What is Docker Compose?**  

✅ **Docker Compose** allows you to:  
✔ Define multi-container applications using a **single file** (`docker-compose.yml`).  
✔ Start all containers with **one command** (`docker-compose up`).  
✔ Simplify **networking, volumes, and environment variables**.  

**💡 Why Use Docker Compose?**  
- When you need **multiple services working together** (e.g., Web + Database).  
- Makes **development, testing, and deployment easier**.  
- Works in **local environments and CI/CD pipelines**.  

---

## **2️⃣ Installing Docker Compose**  
### **📌 On Linux & macOS**  
```sh
sudo apt install docker-compose -y   # Ubuntu/Debian
brew install docker-compose          # macOS (Homebrew)
```
### **📌 Verify Installation**  
```sh
docker-compose --version
```

---

## **3️⃣ Basic Docker Compose Example**  

Let’s create a **simple app** with **Nginx (web) and MySQL (database)**.  

### **📌 Step 1: Create a `docker-compose.yml` File**
```yaml
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
```

### **📌 Step 2: Start Containers**
```sh
docker-compose up -d
```
✅ This **automatically pulls images** and runs **both containers** together.  

### **📌 Step 3: Check Running Containers**
```sh
docker ps
```

### **📌 Step 4: Stop and Remove Containers**
```sh
docker-compose down
```
✅ This **stops and removes** all containers **without deleting volumes**.  

---

## **4️⃣ Understanding Docker Compose File (`docker-compose.yml`)**  

| Key | Description |
|------|------------|
| `version:` | Defines the **Compose file version** (e.g., `"3.8"`). |
| `services:` | Defines different **containers** in the application. |
| `image:` | Specifies the **Docker image** to use. |
| `ports:` | Maps **host ports to container ports** (`host:container`). |
| `depends_on:` | Ensures services **start in the correct order**. |
| `environment:` | Sets **environment variables** inside containers. |

---

## **5️⃣ Docker Compose with Volumes & Networks**  

### **📌 Example: Using Volumes & Networks**  
```yaml
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - web_data:/usr/share/nginx/html
    networks:
      - my_network

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - my_network

volumes:
  web_data:
  db_data:

networks:
  my_network:
```

✅ **This setup ensures:**  
✔ Persistent **data storage** using **volumes**.  
✔ Containers can **communicate** via a custom **network**.  

---

## **6️⃣ Useful Docker Compose Commands**  

| Command | Description |
|---------|------------|
| `docker-compose up` | Starts containers (foreground mode). |
| `docker-compose up -d` | Starts containers **in the background**. |
| `docker-compose down` | Stops & removes all containers. |
| `docker-compose ps` | Lists running services. |
| `docker-compose logs` | Shows logs of all services. |
| `docker-compose restart` | Restarts all containers. |
| `docker-compose exec <service> bash` | Access a running container’s shell. |

---

## **7️⃣ Docker Compose in Production**  

### **📌 Scaling Services (Multiple Containers)**  
```sh
docker-compose up --scale web=3 -d
```
✅ This runs **3 instances** of the `web` service.  

### **📌 Running Compose with an `.env` File**  
```yaml
version: "3.8"

services:
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_PASSWORD}
```
✅ **.env file example:**  
```
DB_PASSWORD=mysecretpassword
```
✅ **Run the app:**  
```sh
docker-compose up -d
```

---

## **8️⃣ Interview Questions & Answers**  

### **1. What is Docker Compose?**  
✅ **Answer:** Docker Compose is a tool for **defining and managing multi-container applications** using a single `docker-compose.yml` file. It simplifies running and linking multiple containers together.  

### **2. What is the difference between `docker run` and `docker-compose up`?**  
✅ **Answer:**  
| Feature | `docker run` | `docker-compose up` |
|---------|-------------|----------------------|
| Command Usage | Used for **single containers** | Used for **multi-container** applications |
| File Required | No (`docker run` runs containers directly) | Yes (`docker-compose.yml` required) |
| Dependency Management | Manual | Handles dependencies (`depends_on`) |
| Scalability | Difficult | Easy (`--scale`) |

### **3. How do you stop and remove all containers in Docker Compose?**  
✅ **Answer:**  
```sh
docker-compose down
```
This stops and **removes all running containers**, networks, and temporary volumes.  

### **4. What is `depends_on` in Docker Compose?**  
✅ **Answer:** The `depends_on` option ensures that **one service starts only after another service**. However, it **does not** wait for the service to be **fully ready** (use health checks for that).  

### **5. How do you persist data in Docker Compose?**  
✅ **Answer:** Use **volumes** in `docker-compose.yml`:
```yaml
volumes:
  db_data:
```
This prevents data loss when containers are stopped or removed.  

### **6. How do you scale services in Docker Compose?**  
✅ **Answer:**  
```sh
docker-compose up --scale web=3 -d
```
This starts **3 instances** of the `web` service.  

### **7. Can you use environment variables in Docker Compose?**  
✅ **Answer:** Yes, you can define them in an `.env` file or directly in `docker-compose.yml`:
```yaml
environment:
  - MYSQL_USER=${DB_USER}
```

### **8. What is the difference between Docker Compose and Kubernetes?**  
✅ **Answer:**  
| Feature | Docker Compose | Kubernetes |
|---------|---------------|------------|
| Purpose | Manages **multi-container apps** | Manages **container orchestration** |
| Scalability | Limited | Highly scalable |
| Load Balancing | Not built-in | Supports **load balancing** |
| Self-healing | No | Yes |

### **9. How do you check logs of a service in Docker Compose?**  
✅ **Answer:**  
```sh
docker-compose logs -f web
```
This **follows logs** of the `web` service in real time.  

### **10. How do you access a running container's shell in Docker Compose?**  
✅ **Answer:**  
```sh
docker-compose exec web sh
```
or  
```sh
docker-compose exec web bash
```
This opens a **shell inside the container**.  

---

## **🔟 Best Practices for Docker Compose**  

✅ **Use environment variables** (`.env` file) to manage configurations.  
✅ **Use volumes** for data persistence.  
✅ **Use networks** for better isolation and communication.  
✅ **Use health checks** to ensure dependencies are ready before starting.  
✅ **Don’t use `latest` tags** (specify versions for stability).  

---

### **🎯 Summary**  
- **Docker Compose** simplifies multi-container application management.  
- Define everything in **`docker-compose.yml`**.  
- Start all services using **`docker-compose up -d`**.  
- Supports **volumes, networking, environment variables, and scaling**.  
- Ideal for **local development and small-scale production deployments**.  

Would you like a **real-world project example** using Docker Compose? 🚀