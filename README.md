Microservices CI/CD on EKS

An end-to-end DevOps project for deploying and monitoring a 13-microservice application on Amazon EKS, with infrastructure provisioning through Terraform, CI automation using Jenkins Multibranch Pipelines, containerization with Docker, Kubernetes deployment, RBAC-based access control, and observability using Prometheus and Grafana.

🏗️ Architecture

                         ┌──────────────┐
                         │    GitHub    │
                         │ 13 Services  │
                         └──────┬───────┘
                                │
                              Webhook
                                │
                                ▼
                    ┌─────────────────────┐
                    │ Jenkins Multibranch │
                    │      Pipeline       │
                    └──────────┬──────────┘
                               │
                     Docker Build & Push
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Docker Registry   │
                    └──────────┬──────────┘
                               │
                               ▼
              ┌─────────────────────────────────┐
              │         Amazon EKS              │
              │                                 │
              │  ┌────┐ ┌────┐ ┌────┐          │
              │  │MS1 │ │MS2 │ │... │ │MS13│    │
              │  └────┘ └────┘ └────┘          │
              │                                 │
              │        Kubernetes RBAC          │
              └──────────────┬──────────────────┘
                             │
                    Metrics & Monitoring
                             │
                   ┌─────────▼─────────┐
                   │    Prometheus     │
                   └─────────┬─────────┘
                             │
                   ┌─────────▼─────────┐
                   │      Grafana      │
                   └───────────────────┘

        Terraform
           │
           ▼
   AWS / EKS Infrastructure

🚀 Project Phases

Phase 1 — Infrastructure as Code

Provisioned the AWS infrastructure and Amazon EKS cluster using Terraform.

Key areas:

- Amazon EKS cluster
- VPC and networking
- Subnets
- IAM roles
- Security groups
- Worker nodes

Terraform makes the infrastructure reproducible and easier to manage.

---

Phase 2 — Jenkins Multibranch CI

Configured a Jenkins Multibranch Pipeline integrated with GitHub.

Each microservice has its own branch and Jenkins automatically discovers and builds the branches.

CI workflow:

GitHub
   ↓
Checkout
   ↓
Docker Image Build
   ↓
Docker Registry Push

The pipeline was implemented across 13 microservices.

---

Phase 3 — Containerization

Each microservice is packaged as a Docker image.

Microservice Source Code
        ↓
    Docker Build
        ↓
   Docker Image
        ↓
 Docker Registry

This provides consistent application packaging for Kubernetes deployment.

---

Phase 4 — Kubernetes Deployment

Created Kubernetes manifests for the microservices and deployed them to Amazon EKS.

Kubernetes resources include:

- Deployments
- Services
- ConfigMaps
- Secrets
- Ingress
- Persistent resources
- Network Policies

The application services run inside the "webapps" namespace.

Example verification:

kubectl get pods -n webapps

kubectl get svc -n webapps

---

Phase 5 — Authentication & Authorization

Implemented Kubernetes RBAC to control access to cluster resources.

Configured:

- ServiceAccounts
- Roles
- RoleBindings
- Namespace-level permissions

The objective was to follow the principle of least privilege and provide only the permissions required by specific workloads or users.

---

Phase 6 — Monitoring & Observability

Implemented Kubernetes monitoring using:

- Prometheus — metrics collection
- Grafana — visualization and dashboards

Monitoring includes:

- CPU utilization
- Memory utilization
- Pod metrics
- Container metrics
- Namespace-level resource usage
- Microservice resource consumption

Example:

Kubernetes / EKS
       ↓
   Prometheus
       ↓
     Grafana
       ↓
 Dashboards & Metrics

🧩 Microservices

The project contains 13 independently managed services, including examples such as:

- Ad Service
- Cart Service
- Checkout Service
- Currency Service
- Email Service
- Frontend
- Load Generator
- Payment Service
- Product Catalog Service
- Recommendation Service
- Shipping Service
- Redis Cart
- Additional supporting service

Each service can be independently built, containerized, and deployed.

🛠️ Technology Stack

Category| Technology
Cloud| AWS
Container Orchestration| Amazon EKS
Infrastructure as Code| Terraform
CI/CD| Jenkins
Source Control| GitHub
Containerization| Docker
Container Registry| Docker Registry
Orchestration| Kubernetes
Security| Kubernetes RBAC
Monitoring| Prometheus
Visualization| Grafana
Scripting / Automation| Bash

🔄 End-to-End Workflow

Developer
   │
   ▼
GitHub
   │
   ▼
Jenkins Multibranch Pipeline
   │
   ├── Checkout
   ├── Docker Build
   └── Push Image
           │
           ▼
    Docker Registry
           │
           ▼
      Amazon EKS
           │
    ┌──────┴──────┐
    │             │
13 Microservices  RBAC
    │
    ▼
Prometheus
    │
    ▼
Grafana

📊 Project Highlights

- Built CI automation for 13 microservices
- Provisioned Amazon EKS infrastructure using Terraform
- Implemented Jenkins Multibranch Pipelines
- Automated Docker image build and registry publishing
- Deployed microservices using Kubernetes
- Implemented Kubernetes RBAC
- Established Prometheus and Grafana monitoring
- Monitored cluster, namespace, pod, and container-level metrics
- Built a production-style cloud-native deployment workflow

📁 Repository Structure

microservices/
│
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── ...
│
├── kubernetes/
│   ├── namespace.yaml
│   ├── deployments/
│   ├── services/
│   ├── rbac/
│   └── ...
│
├── Jenkinsfile
│
├── service-1/
├── service-2/
├── service-3/
├── ...
├── service-13/
│
└── README.md

«Note: Update the repository structure above to match the actual folders and files in your repository.»

🎯 Key Learning Outcomes

This project provided hands-on experience with:

- Infrastructure as Code using Terraform
- Amazon EKS administration
- Jenkins Multibranch CI/CD
- Docker image lifecycle management
- Kubernetes application deployment
- Kubernetes RBAC
- Prometheus metrics collection
- Grafana dashboards
- Microservices architecture
- Cloud-native DevOps workflows

👨‍💻 Project

Microservices CI/CD on EKS

Built as a hands-on DevOps project to understand how infrastructure, CI/CD, containers, Kubernetes security, and observability work together in a real-world-style microservices environment.
