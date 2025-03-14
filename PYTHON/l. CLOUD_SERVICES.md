# **Working with Cloud Services and Containers in Python**  

Python is widely used for cloud computing and containerization due to its extensive libraries and frameworks. This guide covers cloud services (AWS, Azure, GCP) and containerization using Docker and Kubernetes.

---

# **1. Cloud Services in Python**  

Cloud services allow scalable computing, storage, networking, and automation. Python interacts with cloud platforms using SDKs and APIs.

## **1.1 Working with AWS (Amazon Web Services) using Boto3**  
Boto3 is the official AWS SDK for Python.

### **1.1.1 Setting Up Boto3**  
Install Boto3 and configure AWS credentials:
```bash
pip install boto3
aws configure
```
Set up credentials (`~/.aws/credentials`):  
```plaintext
[default]
aws_access_key_id=YOUR_ACCESS_KEY
aws_secret_access_key=YOUR_SECRET_KEY
region=us-east-1
```

### **1.1.2 Managing S3 Buckets**  
Create an S3 bucket:
```python
import boto3

s3 = boto3.client("s3")
bucket_name = "my-python-bucket"
s3.create_bucket(Bucket=bucket_name)
```
Upload a file:
```python
s3.upload_file("localfile.txt", bucket_name, "uploadedfile.txt")
```
List all buckets:
```python
buckets = s3.list_buckets()
for bucket in buckets["Buckets"]:
    print(bucket["Name"])
```

---

### **1.1.3 Managing EC2 Instances**  
Launch an EC2 instance:
```python
ec2 = boto3.resource("ec2")
instance = ec2.create_instances(
    ImageId="ami-0abcdef1234567890",
    MinCount=1,
    MaxCount=1,
    InstanceType="t2.micro",
)
print(instance[0].id)
```
Stop an instance:
```python
ec2.instances.filter(InstanceIds=["i-1234567890abcdef0"]).stop()
```

---

### **1.1.4 Managing IAM Users**  
Create an IAM user:
```python
iam = boto3.client("iam")
iam.create_user(UserName="newuser")
```
List IAM users:
```python
users = iam.list_users()
for user in users["Users"]:
    print(user["UserName"])
```

---

## **1.2 Working with Azure Using Azure SDK**  
Install the Azure SDK:  
```bash
pip install azure-storage-blob azure-mgmt-compute azure-identity
```

### **1.2.1 Managing Azure Blob Storage**  
```python
from azure.storage.blob import BlobServiceClient

connection_string = "your_connection_string"
blob_service_client = BlobServiceClient.from_connection_string(connection_string)

container_client = blob_service_client.create_container("mycontainer")
blob_client = container_client.get_blob_client("myfile.txt")

with open("localfile.txt", "rb") as data:
    blob_client.upload_blob(data)
```

---

## **1.3 Working with Google Cloud (GCP) Using Google Cloud SDK**  
Install the Google Cloud SDK:  
```bash
pip install google-cloud-storage google-cloud-compute
```
Authenticate with GCP:  
```bash
gcloud auth application-default login
```

### **1.3.1 Managing Google Cloud Storage (GCS)**
```python
from google.cloud import storage

client = storage.Client()
bucket = client.create_bucket("my-python-bucket")
blob = bucket.blob("file.txt")
blob.upload_from_filename("localfile.txt")
```

---

## **2. Working with Containers in Python**  
Containers allow applications to run in isolated environments.

### **2.1 Docker Basics**  
Install Docker and check version:
```bash
docker --version
```
Create a simple Python application (`app.py`):
```python
print("Hello, Docker!")
```
Create a Dockerfile:
```dockerfile
FROM python:3.9
COPY app.py /app/
WORKDIR /app
CMD ["python", "app.py"]
```
Build and run the container:
```bash
docker build -t my-python-app .
docker run my-python-app
```

---

## **2.2 Managing Containers Using Python (`docker` SDK)**  
Install the Docker SDK for Python:
```bash
pip install docker
```

### **2.2.1 Running Containers with Python**  
```python
import docker

client = docker.from_env()
container = client.containers.run("ubuntu", "echo Hello from Python", detach=True)
print(container.logs().decode())
```
List running containers:
```python
for container in client.containers.list():
    print(container.name)
```

Stop a container:
```python
container.stop()
```

---

## **3. Working with Kubernetes (K8s) in Python**  
Kubernetes automates container deployment, scaling, and management.

Install `kubectl` and `python-kubernetes`:
```bash
pip install kubernetes
```
Configure `kubectl` to connect to the cluster:
```bash
kubectl config view
```

### **3.1 Deploying a Pod Using Python**
```python
from kubernetes import client, config

config.load_kube_config()
v1 = client.CoreV1Api()

pod = client.V1Pod(
    metadata=client.V1ObjectMeta(name="python-pod"),
    spec=client.V1PodSpec(containers=[client.V1Container(name="python-container", image="python:3.9", command=["sleep", "3600"])]),
)

v1.create_namespaced_pod(namespace="default", body=pod)
```

### **3.2 Listing Pods**  
```python
pods = v1.list_pod_for_all_namespaces()
for pod in pods.items:
    print(f"Pod Name: {pod.metadata.name}, Namespace: {pod.metadata.namespace}")
```

### **3.3 Deploying a Service**  
```python
service = client.V1Service(
    metadata=client.V1ObjectMeta(name="python-service"),
    spec=client.V1ServiceSpec(
        selector={"app": "python-pod"},
        ports=[client.V1ServicePort(port=80, target_port=5000)],
    ),
)
v1.create_namespaced_service(namespace="default", body=service)
```

---

## **4. CI/CD with Containers in DevOps**  
Automating container deployments using Python.

### **4.1 Using Jenkins to Build and Deploy a Docker Image**  
Jenkinsfile:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-python-app .'
            }
        }
        stage('Push') {
            steps {
                sh 'docker tag my-python-app myrepo/my-python-app:latest'
                sh 'docker push myrepo/my-python-app:latest'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
```

---

## **5. Infrastructure as Code (IaC) with Python**  
Manage cloud infrastructure using Terraform and Ansible.

### **5.1 Terraform with Python (`python-terraform`)**  
Install Terraform and the Python module:
```bash
pip install python-terraform
```
Apply a Terraform script from Python:
```python
from python_terraform import Terraform

tf = Terraform(working_dir="./terraform")
tf.init()
tf.apply(skip_plan=True)
```

### **5.2 Ansible Automation with Python**  
Run an Ansible playbook from Python:
```python
import ansible_runner

result = ansible_runner.run(private_data_dir="/path/to/playbook", playbook="site.yml")
print(result.status)
```

---

## **Conclusion**  
Python is a powerful tool for cloud automation, containerization, and DevOps.

✅ **Cloud Services:** AWS (Boto3), Azure, GCP  
✅ **Containers:** Docker SDK, Python-based container management  
✅ **Kubernetes:** Automating container orchestration with Python  
✅ **CI/CD:** Automating deployments using Jenkins and Terraform  

Would you like a **hands-on project** using Python with cloud services and containers?