# DevOps EKS Project

## Overview

This project demonstrates a complete cloud-native deployment workflow using:

- Terraform (Infrastructure as Code)
- AWS EKS (Kubernetes)
- Docker
- Amazon ECR
- Kubernetes Deployment & Service
- AWS Load Balancer

The infrastructure is fully reproducible and disposable.

---

## Architecture

Terraform provisions:

- VPC
- Public Subnets
- Internet Gateway
- EKS Cluster
- Managed Node Group

Application flow:

Docker → ECR → Kubernetes Deployment → LoadBalancer → Public Access

---

## Project Structure

devops-eks-project/

infrastructure/   → Terraform configuration  
app/              → Dockerfile + static app  
k8s/              → Kubernetes manifests  
README.md  

---

## Deployment Steps

1) Provision Infrastructure

cd infrastructure  
terraform init  
terraform apply  

2) Build & Push Docker Image

docker build -t devops-project1:1.0 .  
docker tag devops-project1:1.0 <ECR_URI>:1.0  
docker push <ECR_URI>:1.0  

3) Deploy to Kubernetes

kubectl apply -f k8s/deployment.yaml  
kubectl apply -f k8s/service.yaml  

4) Destroy Infrastructure

cd infrastructure  
terraform destroy  

---

## Key Learnings

- Infrastructure lifecycle management with Terraform  
- EKS networking configuration  
- IAM authentication with kubectl  
- Kubernetes desired vs actual state  
- AWS LoadBalancer integration  
- Cloud cost awareness  

---

## Notes

- This setup is minimal-cost and not production-grade HA.  
- The cluster is intended to be ephemeral (create → test → destroy).