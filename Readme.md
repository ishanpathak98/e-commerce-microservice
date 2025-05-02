# ☁️ Microservices Deployment on Amazon EKS with Jenkins CI/CD

This project demonstrates a complete end-to-end DevOps pipeline for deploying a cloud-native **microservices-based application** on **Amazon EKS**, using **Jenkins multibranch pipelines**, **Docker**, **AWS ECR**, and **CloudWatch monitoring**.

Each microservice is containerized and has its own Git branch and pipeline. The CI/CD process automates building, testing, and deploying to a live EKS cluster, and includes observability using AWS CloudWatch for performance monitoring.

---

## 🔧 Technologies Used

- **Amazon EKS** – Managed Kubernetes Cluster
- **AWS CloudWatch** – For container insights & monitoring
- **Jenkins** – Multibranch pipeline setup for CI/CD
- **Docker** – For building microservice images
- **AWS ECR** – Container image repository
- **Kubernetes (kubectl)** – Managing deployments & services
- **Load Generator (`hey`)** – For stress testing and generating traffic

---

## 📂 Microservices Structure

Each microservice is maintained in its **own Git branch**:

| Microservice Branch       | Description                     |
|---------------------------|---------------------------------|
| `main`                    | Central config & manifests      |
| `productcatalogservice`   | Product catalog management      |
| `currencyservice`         | Currency conversion service     |
| `shippingservice`         | Shipping rate calculator        |
| `recommendationservice`   | Product recommendation engine   |
| `paymentservice`          | Payment gateway integration     |

---

## 🚀 CI/CD Flow

Each microservice follows this pipeline:

1. **Code Push to Branch** triggers Jenkins.
2. Jenkins uses a **multibranch pipeline** and respective `Jenkinsfile`.
3. Builds Docker image and pushes to **ECR**.
4. Deploys updated pods using **kubectl** and respective `deployment.yaml`.

---

## 📊 Monitoring Setup

We used **AWS CloudWatch Container Insights** to monitor metrics like:

- CPU & memory usage per pod
- Pod restarts & events
- Network traffic
- Disk I/O

**Steps to Enable Monitoring**:

1. Enabled CloudWatch agent via:
   ```bash
   kubectl apply -f https://raw.githubusercontent.com/aws/amazon-cloudwatch-agent-k8s/main/deployment/eks/cloudwatch-agent/quickstart/cwagent-fluentd.yaml
