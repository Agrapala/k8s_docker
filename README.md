# Hello DevOps - Kubernetes & Docker Project

A simple web application demonstrating containerization with Docker and orchestration with Kubernetes.

## 📋 Project Overview

This project contains a lightweight NGINX-based web application that displays a "Hello DevOps" message. It is containerized using Docker and can be deployed to Kubernetes clusters.

## 🚀 Quick Start

### Prerequisites

- Docker installed and running
- Kubernetes cluster (Minikube, Kind, or cloud-based)
- kubectl configured to access your cluster

### Build the Docker Image

```bash
docker build -t samithaagrapala/hello-devops:v1 .
```

### Push to Docker Registry (Optional)

```bash
docker push samithaagrapala/hello-devops:v1
```

### Deploy to Kubernetes

1. **Apply the deployment:**
   ```bash
   kubectl apply -f k8s/deployment.yaml
   ```

2. **Apply the service:**
   ```bash
   kubectl apply -f k8s/service.yaml
   ```

3. **Verify deployment:**
   ```bash
   kubectl get pods
   kubectl get svc
   ```

### Access the Application

The service is exposed as a NodePort on port `30007`:

- **Local Kubernetes (Minikube):**
  ```bash
  minikube service hello-devops-service
  ```

- **Manual access:**
  ```
  http://<node-ip>:30007
  ```

## 📝 Configuration Details

### Docker Configuration
- **Base Image:** nginx:alpine (lightweight, ~40MB)
- **Port:** 80 (standard HTTP)
- **Content:** Static HTML file served by NGINX

### Kubernetes Configuration

**Deployment (deployment.yaml):**
- **Name:** hello-devops
- **Replicas:** 2 (for redundancy)
- **Image:** samithaagrapala/hello-devops:v1
- **Container Port:** 80

**Service (service.yaml):**
- **Type:** NodePort (accessible from outside the cluster)
- **Service Port:** 80
- **Target Port:** 80
- **Node Port:** 30007

## 🔧 Common Commands

```bash
# Check deployment status
kubectl describe deployment hello-devops

# View logs
kubectl logs -l app=hello-devops

# Scale replicas
kubectl scale deployment hello-devops --replicas=3

# Update image
kubectl set image deployment/hello-devops nginx=samithaagrapala/hello-devops:v2

# Delete deployment
kubectl delete deployment hello-devops
kubectl delete service hello-devops-service
```

