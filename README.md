# **GitHubActions_CI_CD_Pipeline_Java_AWS_EKS**  
### 🚀 CI/CD Pipeline for Java Application with GitHub Actions, Docker, and AWS EKS  

This repository automates the **Continuous Integration (CI) and Continuous Deployment (CD)** process for a **Java Spring Boot application** using **GitHub Actions, Docker, AWS EKS (Elastic Kubernetes Service), and `eksctl`**.

---

## **🛠 Tech Stack**
- **Programming Language:** Java (Spring Boot)
- **CI/CD Tool:** GitHub Actions
- **Containerization:** Docker
- **Cloud Provider:** AWS
- **Orchestration:** Kubernetes (EKS)
- **Infrastructure Provisioning:** `eksctl`
- **Build Tool:** Maven

---

## **📌 Features**
✅ **Automated CI/CD Pipeline:** Fully automated build, test, containerization, and deployment process.  
✅ **GitHub Actions Workflows:** Includes separate **CI (Continuous Integration)** and **CD (Continuous Deployment)** workflows.  
✅ **Docker & Kubernetes Deployment:** Uses Docker for containerization and Kubernetes for orchestration on **AWS EKS**.  
✅ **Secure AWS Authentication:** Uses GitHub Secrets to store AWS credentials securely.  
✅ **AWS EKS Cluster Management:** Uses **`eksctl`** for cluster creation and management.  

---

## **📂 Folder Structure**
```plaintext
GitHubActions_CI_CD_Pipeline_Java_AWS_EKS/
│── .github/workflows/        # GitHub Actions workflows
│   ├── ci.yml                # CI workflow (Build & Test)
│   ├── cd.yml                # CD workflow (Docker & EKS Deployment)
│
│── k8s/                      # Kubernetes Deployment Files
│   ├── deployment.yaml        # K8s deployment manifest
│   ├── service.yaml           # K8s service manifest
│
│── src/                      # Java Spring Boot source code
│
│── pom.xml                   # Maven configuration file
│── Dockerfile                # Docker build configuration
│── Jenkinsfile               # Jenkins pipeline configuration
│── commands.sh               # Deployment script
│── .gitignore                # Git ignore file
│── README.md                 # Documentation
```

---

## **🚀 Getting Started**
### **1️⃣ Clone the Repository**
```bash
git clone https://github.com/YOUR_USERNAME/GitHubActions_CI_CD_Pipeline_Java_AWS_EKS.git
cd GitHubActions_CI_CD_Pipeline_Java_AWS_EKS
```

---

### **2️⃣ Install Required Tools**
Ensure you have the following installed:
- **AWS CLI**: Authenticate with AWS using:
  ```bash
  aws configure
  ```
- **eksctl**: Install `eksctl` for managing EKS clusters:
  ```bash
  curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /usr/local/bin
  eksctl version
  ```
- **kubectl**: Install Kubernetes CLI:
  ```bash
  sudo apt install kubectl
  ```

---

### **3️⃣ Create an AWS EKS Cluster Using `eksctl`**
To create an **AWS EKS cluster**, use the following command:

```bash
eksctl create cluster \
  --name eks-cluster \
  --region eu-north-1 \
  --version 1.32 \
  --node-type t3.micro \
  --nodes 2 \
  --nodes-min 1 \
  --nodes-max 3 \
  --managed
```

This will:
- Create an **EKS cluster** named `eks-cluster` in **`eu-north-1`**.
- Use **`t3.micro`** instances for worker nodes.
- Provision **2 worker nodes**, scaling between **1 to 3 nodes** as needed.
- Enable **AWS-managed node provisioning**.

---

### **4️⃣ Configure Kubernetes Context**
Once the cluster is created, configure `kubectl` to interact with the cluster:

```bash
aws eks update-kubeconfig --name eks-cluster --region eu-north-1
kubectl get nodes
```

This ensures that **`kubectl`** can communicate with the cluster.

---

### **5️⃣ Setup GitHub Secrets**
Add the following **Secrets** in **GitHub Repository → Settings → Secrets and Variables → Actions**:
| Secret Name            | Value Example                     |
|------------------------|----------------------------------|
| `DOCKERHUB_USERNAME`   | `your_dockerhub_username`       |
| `DOCKERHUB_PASSWORD`   | `your_dockerhub_password`       |
| `AWS_ACCESS_KEY_ID`    | `your_aws_access_key`           |
| `AWS_SECRET_ACCESS_KEY`| `your_aws_secret_key`           |

---

## **📌 CI/CD Pipeline**
### ✅ **CI Workflow (`ci.yml`)**
- Runs on every **Pull Request** to `main`
- **Builds** and **tests** the Java application using Maven.

📌 **CI Steps:**
1. **Checkout code**
2. **Build the application** using `mvn clean package`
3. **Run unit tests** using `mvn test`

---

### ✅ **CD Workflow (`cd.yml`)**
- Runs on every **push to `main`**.
- **Builds a Docker image**, pushes it to **Docker Hub**, and deploys it to **AWS EKS**.

📌 **CD Steps:**
1. **Checkout code**
2. **Build & Push Docker Image** to Docker Hub
3. **Authenticate with AWS**
4. **Deploy to Kubernetes on EKS**

---

## **🚀 Running Manually**
### **Test CI Workflow**
```bash
git checkout -b test-ci
echo "## CI/CD Pipeline Setup" >> README.md
git add .
git commit -m "Test CI workflow"
git push origin test-ci
```
- Create a **Pull Request** and check the CI pipeline.

### **Test CD Workflow**
```bash
git checkout main
git merge test-ci
git push origin main
```
- This triggers the **CD workflow** to deploy the app.

---

## **⚙️ Kubernetes Deployment**
Once the application is deployed, verify the running pods:
```bash
kubectl get pods
kubectl get services
```

If using **port forwarding**:
```bash
kubectl port-forward service/java-app-service 8080:80
```
Now, you can access the application at `http://localhost:8080`.

---

## **🛑 Destroy Resources**
To delete the EKS cluster and free resources:

```bash
eksctl delete cluster --name eks-cluster --region eu-north-1
```

This command will:
- **Delete the EKS cluster**
- Remove all **worker nodes, node groups, networking components**

---

## **📧 Contact**
If you have any questions, reach out via:
- **Author:** `Moamen Ahmed`
- **Email:** `moamenahmed800@gmail.com`

---

### 🎉 **Happy Coding! 🚀**

