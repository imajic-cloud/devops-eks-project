# AWS DevOps EKS Project

A DevOps project demonstrating automated infrastructure provisioning and containerized application deployment using AWS EKS, Terraform, and GitHub Actions.

## Architecture
```
Developer → GitHub → GitHub Actions → Docker → AWS ECR → kubectl → AWS EKS → LoadBalancer → End Users
```

## Technologies

| Category | Technology |
|----------|-----------|
| **Cloud Provider** | AWS (EKS, ECR, VPC, Load Balancer) |
| **Infrastructure as Code** | Terraform |
| **Container Runtime** | Docker |
| **Container Registry** | AWS ECR |
| **Orchestration** | Kubernetes (AWS EKS) |
| **CI/CD** | GitHub Actions |
| **Application** | Nginx web server |

## Project Structure
```
02-eks-terraform-github-actions/
│
├── infrastructure/
│   └── main.tf              # VPC and EKS cluster
│
├── app/
│   ├── Dockerfile           
│   └── app/index.html       
│
├── k8s/
│   ├── deployment.yaml      
│   └── service.yaml         
│
└── .github/
    └── workflows/
        └── deploy.yml       
```

## Getting Started

### 1. Create Infrastructure
```bash
cd infrastructure
terraform init
terraform plan
terraform apply
```

### 2. Connect kubectl to EKS
```bash
aws eks update-kubeconfig --name devops-eks --region us-east-1
kubectl get nodes
```

### 3. Trigger CI/CD Pipeline

Push any change to main branch — GitHub Actions will automatically:
- Build Docker image
- Push to ECR
- Deploy to EKS

### 4. Access the Application
```bash
kubectl get svc
```

Copy the EXTERNAL-IP and open in browser.

## Cleanup
```bash
cd infrastructure
terraform destroy
```

## GitHub Actions Secrets Required

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`