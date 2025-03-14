### **What is Docker?**  
Docker is a tool that helps developers **package, distribute, and run applications in lightweight containers**. Containers ensure that an application runs **consistently** across different environments, whether it's a developer’s laptop, a test server, or production.  

**Why use Docker?**  
- **Portability**: Works the same on any machine.  
- **Lightweight**: Uses fewer system resources than virtual machines.  
- **Fast Deployment**: Containers start quickly.  
- **Scalability**: Can easily scale applications.  
- **Consistency**: Works the same across different environments.  

---

### **Docker Lifecycle**  
The Docker container lifecycle involves the following stages:  

1. **Create**: Create a container from an image but don’t start it.  
   ```bash
   docker create nginx
   ```  
2. **Start**: Start a stopped container.  
   ```bash
   docker start <container_id>
   ```  
3. **Run**: Create and start a container in one step.  
   ```bash
   docker run nginx
   ```  
4. **Stop**: Stop a running container.  
   ```bash
   docker stop <container_id>
   ```  
5. **Restart**: Restart a stopped container.  
   ```bash
   docker restart <container_id>
   ```  
6. **Pause**/**Unpause**: Pause and resume a running container.  
   ```bash
   docker pause <container_id>
   docker unpause <container_id>
   ```  
7. **Kill**: Stop a container immediately.  
   ```bash
   docker kill <container_id>
   ```  
8. **Remove**: Delete a container permanently.  
   ```bash
   docker rm <container_id>
   ```  
9. **List Containers**: Show running or all containers.  
   ```bash
   docker ps  # Running containers  
   docker ps -a  # All containers (including stopped)  
   ```  

---

### **Common Docker Interview Questions and Answers**  

#### **1. What is Docker?**  
**Answer:** Docker is an open-source platform that allows developers to build, package, and run applications in containers. Containers ensure that applications run consistently across different environments.  

#### **2. What is the difference between a container and a virtual machine (VM)?**  
| Feature | Docker Container | Virtual Machine (VM) |
|---------|----------------|----------------|
| Size | Lightweight (MBs) | Heavy (GBs) |
| Performance | Faster | Slower |
| Boot Time | Seconds | Minutes |
| OS Dependency | Shares Host OS | Needs full OS per VM |

#### **3. What is a Docker Image?**  
**Answer:** A Docker image is a blueprint or template that contains everything needed to run an application (code, dependencies, libraries, etc.).  

#### **4. What is a Docker Container?**  
**Answer:** A Docker container is a running instance of a Docker image. It includes everything needed to execute an application.  

#### **5. How do you create and run a container?**  
```bash
docker run -d --name mycontainer nginx
```
- `-d`: Run in detached mode (background).  
- `--name mycontainer`: Assigns a name to the container.  
- `nginx`: Uses the Nginx image.  

#### **6. What is a Dockerfile?**  
**Answer:** A Dockerfile is a script that contains a set of instructions to build a Docker image.  

Example:
```dockerfile
FROM python:3.8  
WORKDIR /app  
COPY . /app  
RUN pip install -r requirements.txt  
CMD ["python", "app.py"]
```

#### **7. What is the difference between CMD and ENTRYPOINT?**  
| Feature | CMD | ENTRYPOINT |
|---------|-----|-----------|
| Purpose | Default command | Fixed command |
| Overridable? | Yes | No (unless `--entrypoint` is used) |

Example:
```dockerfile
CMD ["nginx", "-g", "daemon off;"]  
ENTRYPOINT ["nginx", "-g", "daemon off;"]  
```

#### **8. What is Docker Compose?**  
**Answer:** Docker Compose is a tool for defining and managing multi-container Docker applications using a YAML file (`docker-compose.yml`).  

Example:
```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```
Run with:
```bash
docker-compose up -d
```

#### **9. What is Docker Volume?**  
**Answer:** A Docker volume is used to persist data even if the container stops or is deleted.  

Example:
```bash
docker volume create myvolume
docker run -v myvolume:/data nginx
```

#### **10. How do you check logs of a running container?**  
```bash
docker logs <container_id>
```

#### **11. What is Docker Networking?**  
**Answer:** Docker provides different networking modes:  
- **Bridge (default)**: Containers communicate with each other on the same host.  
- **Host**: Uses the host network.  
- **None**: No networking.  
- **Overlay**: Used in multi-host environments.  

Example:
```bash
docker network create mynetwork
docker run --net=mynetwork nginx
```

#### **12. How do you build a Docker image?**  
```bash
docker build -t myimage .
```
- `-t myimage`: Assigns a name to the image.  
- `.`: Uses the current directory containing the Dockerfile.  

#### **13. What is the difference between Docker Swarm and Kubernetes?**  
| Feature | Docker Swarm | Kubernetes |
|---------|-------------|------------|
| Complexity | Simple | Complex |
| Scaling | Limited | Advanced |
| GUI | No | Yes (Dashboard) |
| Load Balancing | Automatic | Manual Configuration |

#### **14. How do you push an image to Docker Hub?**  
```bash
docker login
docker tag myimage mydockerhubusername/myimage
docker push mydockerhubusername/myimage
```

#### **15. How do you remove unused images and containers?**  
```bash
docker system prune -a
```
This removes:
- Stopped containers  
- Unused images  
- Unused networks  

---

### **Conclusion**  
Docker is essential for modern application deployment. Understanding its lifecycle and commands helps in automating deployments and managing applications efficiently.  

