## **AWS CI/CD – Complete Guide**  

AWS CI/CD (Continuous Integration and Continuous Deployment) is a **set of AWS services** that help developers **automate software development, testing, and deployment**. It ensures that code changes are tested and deployed efficiently.  

---

## **📌 What is CI/CD?**  

✅ **Continuous Integration (CI)**  
- Developers frequently merge their code into a shared repository.  
- Automated tests run to detect errors early.  

✅ **Continuous Deployment (CD)**  
- Code is automatically deployed to production after passing all tests.  
- Ensures faster delivery and fewer manual interventions.  

**Example**:  
A developer pushes code to GitHub → AWS CI/CD pipeline tests & deploys the code → Application updates automatically.

---

## **📌 AWS CI/CD Services**  

| **Service** | **Purpose** |
|------------|-------------|
| **AWS CodeCommit** | Git repository for version control |
| **AWS CodeBuild** | Builds and tests code automatically |
| **AWS CodeDeploy** | Automates application deployment |
| **AWS CodePipeline** | Orchestrates CI/CD workflows |
| **AWS CodeArtifact** | Stores and manages dependencies |
| **AWS CodeStar** | Manages CI/CD projects in one place |

---

## **📌 How AWS CI/CD Works?**  

1️⃣ **Developer pushes code** to **AWS CodeCommit / GitHub / Bitbucket**.  
2️⃣ **AWS CodePipeline** detects changes and starts the CI/CD process.  
3️⃣ **AWS CodeBuild** compiles code and runs automated tests.  
4️⃣ **AWS CodeDeploy** deploys the tested code to AWS services (EC2, Lambda, ECS, etc.).  
5️⃣ **Deployment is completed**, and the application is updated.  

---

## **📌 AWS CI/CD Pipeline Example (CodePipeline)**  

### **1️⃣ Define a CI/CD Pipeline in CloudFormation (YAML)**  

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyPipeline:
    Type: AWS::CodePipeline::Pipeline
    Properties:
      RoleArn: arn:aws:iam::123456789012:role/service-role/AWSCodePipelineServiceRole
      ArtifactStore:
        Type: S3
        Location: my-artifact-bucket
      Stages:
        - Name: Source
          Actions:
            - Name: SourceAction
              ActionTypeId:
                Category: Source
                Owner: AWS
                Provider: CodeCommit
                Version: '1'
              Configuration:
                RepositoryName: my-repo
                BranchName: main
              OutputArtifacts:
                - Name: SourceOutput
        - Name: Build
          Actions:
            - Name: BuildAction
              ActionTypeId:
                Category: Build
                Owner: AWS
                Provider: CodeBuild
                Version: '1'
              Configuration:
                ProjectName: my-build-project
              InputArtifacts:
                - Name: SourceOutput
              OutputArtifacts:
                - Name: BuildOutput
```

---

## **📌 AWS CI/CD Interview Questions & Answers**  

### **1️⃣ What is AWS CodePipeline?**  
💬 **Answer:**  
AWS CodePipeline is a **CI/CD orchestration service** that automates code building, testing, and deployment. It connects AWS CodeCommit, CodeBuild, and CodeDeploy to create an automated CI/CD workflow.

---

### **2️⃣ What is AWS CodeCommit?**  
💬 **Answer:**  
AWS CodeCommit is a **managed Git repository** for storing and managing source code securely. It integrates with AWS CI/CD services to trigger automatic builds and deployments.

---

### **3️⃣ What is AWS CodeBuild?**  
💬 **Answer:**  
AWS CodeBuild is a **managed build service** that compiles code, runs tests, and produces deployable artifacts. It removes the need to manage build servers manually.

**Example Build Command**  
```bash
aws codebuild start-build --project-name my-build-project
```

---

### **4️⃣ What is AWS CodeDeploy?**  
💬 **Answer:**  
AWS CodeDeploy automates code deployment to **EC2, Lambda, ECS, or On-Prem servers**. It supports **rolling, blue-green, and canary deployments** to minimize downtime.

**Example Deployment Command**  
```bash
aws deploy create-deployment --application-name MyApp --deployment-group-name MyDeploymentGroup --s3-location bucket=my-bucket,key=my-app.zip,bundleType=zip
```

---

### **5️⃣ What are the deployment strategies in AWS CodeDeploy?**  
💬 **Answer:**  
AWS CodeDeploy supports different **deployment types**:

| **Strategy** | **Description** |
|-------------|----------------|
| **In-Place (Rolling)** | Updates instances one at a time |
| **Blue-Green** | Deploys new version to a separate group before switching |
| **Canary** | Deploys to a small percentage first, then the rest |

---

### **6️⃣ What is an AWS CI/CD Pipeline?**  
💬 **Answer:**  
An AWS CI/CD pipeline is an **automated workflow** that integrates, tests, and deploys code using services like **CodePipeline, CodeCommit, CodeBuild, and CodeDeploy**.

---

### **7️⃣ How do you trigger a pipeline in AWS CodePipeline?**  
💬 **Answer:**  
A pipeline can be triggered automatically by **code changes in CodeCommit/GitHub** or manually using:  

```bash
aws codepipeline start-pipeline-execution --name my-pipeline
```

---

### **8️⃣ What is a BuildSpec file in AWS CodeBuild?**  
💬 **Answer:**  
A `buildspec.yml` file defines **build commands** for AWS CodeBuild.

Example `buildspec.yml`:  
```yaml
version: 0.2
phases:
  install:
    commands:
      - echo "Installing dependencies..."
      - npm install
  build:
    commands:
      - echo "Building the project..."
      - npm run build
artifacts:
  files:
    - '**/*'
```

---

### **9️⃣ What is Blue-Green Deployment in AWS CodeDeploy?**  
💬 **Answer:**  
Blue-Green Deployment creates **two environments**:  
🔹 **Blue**: The existing version  
🔹 **Green**: The new version  
After testing, AWS **switches traffic** to the Green environment, ensuring zero downtime.

---

### **🔟 How do you monitor an AWS CI/CD pipeline?**  
💬 **Answer:**  
AWS provides monitoring through:  
✅ **AWS CloudWatch Logs** – Logs of builds & deployments  
✅ **AWS CloudTrail** – Tracks API calls & changes  
✅ **AWS SNS Notifications** – Alerts on pipeline failures  

---

## **📌 Summary of AWS CI/CD**  

| **Feature** | **Description** |
|------------|----------------|
| **CodeCommit** | Secure Git repository |
| **CodeBuild** | Builds and tests code |
| **CodeDeploy** | Automates deployment |
| **CodePipeline** | Orchestrates CI/CD workflow |
| **Deployment Types** | Rolling, Blue-Green, Canary |

🚀 **AWS CI/CD automates software delivery, ensuring fast and error-free deployments!** Would you like a **hands-on CI/CD lab** to practice AWS CodePipeline?