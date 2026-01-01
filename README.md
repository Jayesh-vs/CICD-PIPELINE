# 🚀 End-to-End CI/CD DevSecOps Pipeline on AWS

This project implements a **full-scale production-grade DevSecOps CI/CD pipeline** on AWS.
It automates **code build, test, security scanning, artifact management, containerization, Kubernetes deployment, and monitoring** using modern DevOps tools and best practices.

---

## 📌 Project Objectives

- Automate the entire software delivery lifecycle
- Enforce security & quality at every stage
- Provide consistent, reproducible infrastructure
- Achieve continuous deployment on Kubernetes
- Enable full system observability

---

## 🧱 High-Level Architecture
---

## 🛠️ Technology Stack

| Category | Tools |
|--------|------|
Source Control | GitHub |
CI/CD | Jenkins |
Build Tool | Maven |
Code Quality | SonarQube |
Security | Trivy |
Artifact Repository | Nexus |
Containerization | Docker |
Orchestration | Kubernetes (EKS) |
IaC | Terraform |
Monitoring | Prometheus, Blackbox Exporter, Grafana |
Cloud Platform | AWS |

---

## 🖥️ Infrastructure Design

### EC2 Instances

| Instance | Type | Purpose |
|---------|------|---------|
Jenkins | t2.large | CI/CD automation server |
SonarQube | t2.medium | Static code analysis |
Nexus | t2.medium | Artifact repository |
Terraform | t2.medium | Infrastructure provisioning |
Monitoring | t2.large | Prometheus + Grafana |

### Network & Security

**Single common Security Group**
- SSH (22)
- Jenkins (8080)
- SonarQube (9000)
- Nexus (8081)
- Grafana (3000)
- Prometheus (9090)
- Blackbox (9115)

---

## ⚙️ Jenkins Pipeline Details

### Pipeline Stages

| Stage | Description |
|-----|------------|
Checkout | Fetch source code from GitHub |
Compile | Compile using Maven |
Test | Execute unit tests |
Trivy FS Scan | Scan source code for vulnerabilities |
SonarQube Analysis | Static code analysis & quality gate |
Build | Package application |
Publish Artifact | Upload build to Nexus |
Docker Build | Create container image |
Trivy Image Scan | Scan image for vulnerabilities |
Docker Push | Push image to DockerHub |
K8s Deploy | Deploy application to EKS |
Verify | Validate deployment |

---

## 🛡️ Security & Quality Controls

- **SonarQube** enforces quality gates before build promotion
- **Trivy** scans:
- file system
- Docker images
- **RBAC** in Kubernetes
---

## ☸️ Kubernetes Deployment Architecture

- AWS EKS cluster
- Namespace: `webapps`
- Resources:
- Deployment
- Service
- Secret (Docker registry)
- ServiceAccount
- Role & RoleBinding

Jenkins authenticates to EKS using Kubernetes **service account token**.

---

## 📦 Artifact & Image Management

- **Nexus** stores:
- Snapshot artifacts
- Release artifacts
- **DockerHub** stores versioned container images
- Enables artifact traceability and rollback

---

## 🧾 Infrastructure as Code

All infrastructure is provisioned using **Terraform**:

```bash
terraform init
terraform plan
terraform apply
