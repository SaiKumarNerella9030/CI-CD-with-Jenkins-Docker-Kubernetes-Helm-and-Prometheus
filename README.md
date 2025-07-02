# 🛠️ CI/CD Pipeline with Jenkins, Docker, Kubernetes (EKS), Helm, and Prometheus

This project demonstrates a **complete DevOps pipeline** that automates the build, test, deployment, and monitoring of a simple microservices-based application using the following tools:

* Jenkins
* Docker
* Kubernetes (Amazon EKS)
* Helm
* Prometheus + Grafana

---

## 📌 Project Overview

The pipeline is triggered when a new change is pushed to the GitHub repository. Jenkins automatically:

1. Clones the repository
2. Builds Docker images for frontend & backend
3. Pushes images to DockerHub
4. Deploys applications to **Amazon EKS** using **Helm**
5. Exposes services via **NGINX Ingress**
6. Monitors pods using **Prometheus & Grafana**

---

## 🔧 Technologies Used

| Tool                 | Purpose                                |
| -------------------- | -------------------------------------- |
| **Jenkins**          | CI/CD server                           |
| **Docker**           | Containerization                       |
| **Kubernetes (EKS)** | Container orchestration on AWS         |
| **Helm**             | Kubernetes package manager             |
| **Prometheus**       | Monitoring solution for Kubernetes     |
| **Grafana**          | Visualization of metrics               |
| **AWS**              | Infrastructure provisioning (EKS, IAM) |

---

## 📁 Project Structure

```
CI-CD-with-Jenkins-Docker-Kubernetes-Helm-and-Prometheus/
├── ci-cd-microservices/
│   ├── frontend/
│   │   ├── index.html
│   │   ├── Dockerfile
│   │   └── helm/
│   │       ├── templates/
│   │       └── values.yaml
│   ├── backend/
│   │   ├── app.js
│   │   ├── Dockerfile
│   │   └── helm/
│   │       ├── templates/
│   │       └── values.yaml
│   └── Jenkinsfile
```

---

## 🚀 Pipeline Workflow

### Trigger:

Push to GitHub triggers Jenkins pipeline.

### Jenkins Pipeline Steps:

1. **Clone GitHub Repo**
2. **Build Docker Images**

   ```bash
   docker build -t <dockerhub_user>/frontend .
   docker build -t <dockerhub_user>/backend .
   ```
3. **Push Images to DockerHub**
4. **Deploy to Kubernetes using Helm**
5. **Expose via NGINX Ingress**
6. **Monitor via Prometheus**

---

## ⚙️ Setup & Installation

### ✅ Jenkins Installation on EC2:

* Installed on Ubuntu EC2 with Docker & Helm
* Jenkins user added to Docker group:

  ```bash
  sudo usermod -aG docker jenkins
  ```

### ✅ Kubernetes Setup (EKS):

* Provisioned using Terraform
* Configured `~/.kube/config` for access

### ✅ Helm Installed:

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

### ✅ AWS CLI Installed:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws configure
```

### ✅ kubectl Installed:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

---

## 🧪 Issues Faced & Fixes

| Issue                                           | Solution                                              |
| ----------------------------------------------- | ----------------------------------------------------- |
| **EKS Node Group creation failed**              | Enabled `Auto-Assign Public IP` in subnet settings    |
| **Terraform lock error**                        | Deleted lock manually via AWS CLI                     |
| **Helm Ingress error**                          | Added correct Helm annotations/labels                 |
| **Jenkins permission denied for Docker**        | Added Jenkins to Docker group                         |
| **kubectl not found in Jenkins**                | Installed & added to Jenkins user PATH                |
| **Helm command not found**                      | Installed Helm manually                               |
| **"nginx default page" instead of custom HTML** | Fixed Dockerfile and image paths                      |
| **AWS CLI exec plugin errors**                  | Installed AWS CLI correctly and configured in Jenkins |

---

## 🌐 Accessing the Application

### 🔗 Frontend

After deployment, access the app using the Ingress LoadBalancer DNS:

```bash
kubectl get ingress
```

Or via:

```
http://<elb-hostname>/
```

### 📈 Monitoring

* **Prometheus:** http\://<load-balancer>:9090
* **Grafana:** http\://<load-balancer>:3000 (admin / admin)

---

## 📤 Docker Images

| Service  | Docker Image                        |
| -------- | ----------------------------------- |
| Frontend | `saikumarnerella90/frontend:latest` |
| Backend  | `saikumarnerella90/backend:latest`  |

---

## ✅ Completed Milestones

* [x] Setup Jenkins on EC2
* [x] Setup Docker, kubectl, and Helm
* [x] Configure GitHub webhook
* [x] Push Docker images to DockerHub
* [x] Deploy to AWS EKS
* [x] Use Helm for deployment
* [x] Setup Ingress for external access
* [x] Install Prometheus and Grafana

---

## Final Output

* CI/CD fully automated via Jenkins
* Dockerized microservices
* Helm-based deployment to EKS
* Monitoring stack live
* Application accessible via public DNS

---
