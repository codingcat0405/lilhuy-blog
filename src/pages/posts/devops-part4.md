---
layout: ../../layouts/post.astro
title: '[DevOps Series] Part 4: K8s in a nutshell'
pubDate: 2025-08-07
description: 'K8s in a nutshell'
author: 'codingcat'
excerpt: K8s in a nutshell
image:
  src:
  alt:
tags: ['devops', 'devops-series']
---

# 📚 Series Table of Contents

1. 📖 [Chapter 0: Introduction and Stories](/posts/devops-part0)
2. 📚 [Chapter 1: Some concepts and terminologies](/posts/devops-part1)
3. 🚀 [Chapter 2: A noob guy deploy his web app](/posts/devops-part2)
4. 🐳 [Chapter 3: Docker and the world of containerization](/posts/devops-part3)
5. ☸️ [Chapter 4: K8s in a nutshell](/posts/devops-part4) (You are here) 🎯
6. 🔧 [Chapter 5: K8s in details](/posts/devops-part5) 🛠️
7. 🏠 [Chapter 6: Before go to the ground](/posts/devops-part6) 🏡
8. 🐧 [Chapter 7: Ubuntu server and the world of Linux](/posts/devops-part7) 🖥️
9. ⚡ [Chapter 8: MicroK8s the simple and powerful K8s](/posts/devops-part8) ⚙️
10. ☁️ [Chapter 9: Harvester HCI the native cloud](/posts/devops-part9) 🌐
11. 🏭 [Chapter 10: More about Harvester HCI](/posts/devops-part10) 🏢
12. 🖥️ [Chapter 11: Promox VE the best VM manager](/posts/devops-part11) 💾
13. 🌐 [Chapter 12: Turn a server into a router with Pfsense](/posts/devops-part12) 🔌
14. 🛠️ [Chapter 13: Some tools, services that you can installed for your devops pipeline](/posts/devops-part13) 🔧
15. 🌍 [Chapter 14: Hello Internet with Cloudflare Zero Trust](/posts/devops-part14) 🔒
16. 🎉 [Chapter 15: Maybe it the end of the series](/posts/devops-part15) 🏁

---

Welcome to the world of Kubernetes! If Docker is like learning to drive a car, then Kubernetes is like learning to manage a fleet of cars. In this chapter, we'll explore K8s basics by building on your Docker knowledge.

## From Docker to Kubernetes

Remember our Docker journey? We learned to containerize applications with `docker run`, `docker-compose`, and Dockerfiles. But what happens when you need to run hundreds or thousands of containers across multiple servers?

**Docker Limitations:**

```bash
# This works great for development
docker run -p 3000:3000 my-app
docker-compose up -d
```

But in production, you need:

- **Scaling**: How do you run 10, 100, or 1000 containers?
- **High Availability**: What if a server crashes?
- **Load Balancing**: How do you distribute traffic?
- **Service Discovery**: How do containers find each other?
- **Rolling Updates**: How do you update without downtime?
- **Resource Management**: How do you prevent one app from hogging resources?

**Kubernetes to the Rescue:**
K8s is like having a smart manager for your container fleet. It handles all the complex orchestration so you can focus on your applications.

## Why We Need Kubernetes

Think of it this way:

- **Docker** = Single container management
- **Docker Compose** = Multi-container on one machine
- **Kubernetes** = Multi-container across multiple machines with intelligence

## K8s Core Concepts (Overview)

### 🏗️ Cluster Architecture

- **Node**: A worker machine (physical or virtual)
- **Cluster**: A set of nodes running containerized applications
- **Pod**: The smallest deployable unit (usually 1 container, but can have multiple)
- **Deployment**: Manages pod replicas and updates
- **Service**: Stable network endpoint for pods
- **Secret**: Secure way to store sensitive data

### 📦 Key Resources

- **Pod**: One or more containers sharing resources
- **Service**: Network access to pods
- **Deployment**: Manages pod replicas and rolling updates
- **ConfigMap**: Configuration data
- **Secret**: Sensitive data (passwords, keys)

### K8s vs Docker

| Docker | Kubernetes |
|--------|------------|
| Single container | Multiple containers |
| One machine | Multiple machines |
| Manual management | Automated orchestration |
| Basic networking | Advanced networking |
| Simple scaling | Intelligent scaling |

## Install MicroK8s

MicroK8s is the simplest way to get Kubernetes running locally. It's perfect for learning and development.

```bash
# Install MicroK8s
sudo snap install microk8s --classic

# Add your user to the microk8s group
sudo usermod -a -G microk8s $USER
newgrp microk8s

# Check status
microk8s status

# Enable essential addons
microk8s enable dns dashboard storage

# Get kubectl alias
echo "alias kubectl='microk8s kubectl'" >> ~/.bashrc
source ~/.bashrc
```

## Your First K8s Deployment (Commands)

Let's deploy a simple nginx app using kubectl commands:

```bash
# Create a deployment
kubectl create deployment nginx-app --image=nginx:alpine

# Scale the deployment
kubectl scale deployment nginx-app --replicas=3

# Expose the deployment
kubectl expose deployment nginx-app --port=80 --type=LoadBalancer

# Check what we created
kubectl get pods
kubectl get services
kubectl get deployments

# Get detailed info
kubectl describe pod <pod-name>
kubectl describe service nginx-app

# View logs
kubectl logs <pod-name>
kubectl logs -f <pod-name>  # Follow logs

# Execute commands in pod
kubectl exec -it <pod-name> -- /bin/sh
```

## Inspect Your Deployment

```bash
# List all resources
kubectl get all

# Get pod details
kubectl get pods -o wide

# Describe a specific pod
kubectl describe pod <pod-name>

# Check pod logs
kubectl logs <pod-name>

# Check service endpoints
kubectl get endpoints

# View events
kubectl get events
```

## K8s Features in Action

### Rolling Updates

```bash
# Update the image
kubectl set image deployment nginx-app nginx=nginx:latest

# Check rollout status
kubectl rollout status deployment nginx-app

# Rollback if needed
kubectl rollout undo deployment nginx-app

# Check rollout history
kubectl rollout history deployment nginx-app
```

### Scaling

```bash
# Scale up
kubectl scale deployment nginx-app --replicas=5

# Scale down
kubectl scale deployment nginx-app --replicas=2

# Auto-scaling (if metrics-server is enabled)
kubectl autoscale deployment nginx-app --min=2 --max=10 --cpu-percent=50
```

## Deploy with YAML Files

Now let's create the same deployment using YAML files:

```yaml
# nginx-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-app
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
  type: LoadBalancer
```

Deploy with YAML:

```bash
# Apply the configuration
kubectl apply -f nginx-deployment.yaml

# Check status
kubectl get pods
kubectl get services

# Update the deployment
kubectl apply -f nginx-deployment.yaml

# Delete resources
kubectl delete -f nginx-deployment.yaml
```

## Working with Secrets

```bash
# Create a secret
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=secret123

# List secrets
kubectl get secrets

# Describe secret
kubectl describe secret my-secret

# Use secret in deployment
kubectl create deployment app-with-secret --image=nginx:alpine
kubectl set env deployment app-with-secret --from=secret/my-secret
```

## Essential kubectl Commands

```bash
# Cluster info
kubectl cluster-info
kubectl get nodes

# Pods
kubectl get pods
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl logs <pod-name>

# Deployments
kubectl get deployments
kubectl describe deployment <deployment-name>
kubectl rollout status deployment <deployment-name>

# Services
kubectl get services
kubectl describe service <service-name>

# Namespaces
kubectl get namespaces
kubectl create namespace my-namespace

# Delete resources
kubectl delete pod <pod-name>
kubectl delete deployment <deployment-name>
kubectl delete service <service-name>
```

## What's Next?

This is just the beginning! In the next chapter, we'll dive deeper into:

- Advanced K8s concepts
- Networking and storage
- Security and RBAC
- Monitoring and logging
- Production best practices

## Quick Summary

✅ **What we covered:**

- Docker to Kubernetes transition
- K8s core concepts overview
- MicroK8s installation
- First deployment with commands
- Pod inspection and management
- Rolling updates and scaling
- YAML file deployments
- Working with secrets

## Conclusion

Kubernetes might seem complex at first, but it's just a container orchestrator that makes your life easier. Start with the basics, practice locally with MicroK8s, and gradually explore advanced features. The best way to learn K8s is by doing - deploy applications, break things, and fix them!

---

## 📚 Series Navigation

| **[← Previous Chapter](/posts/devops-part3)**<br>**🐳 Docker and the world of containerization** | **DevOps Series**<br>**Chapter 4 of 16** | **[Next Chapter →](/posts/devops-part5)**<br>**🔧 K8s in details** |
