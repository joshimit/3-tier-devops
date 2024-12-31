MERN To-Do List Application - Cloud Deployment with Kubernetes
This repository hosts a MERN To-Do List Application deployed on AWS EKS using a 3-tier architecture. The project showcases containerization, orchestration, and cloud deployment principles with features such as Auto Scaling and Load Balancing.

Project Overview
Architecture
Frontend: Built with React.js, containerized using Docker.
Backend: Node.js application, also containerized using Docker.
Database: MongoDB for storing tasks.
The architecture follows a 3-tier pattern:

Frontend Tier: Handles the user interface.
Backend Tier: Handles business logic and API services.
Database Tier: Stores persistent data.
Deployment Highlights
Containers are built from the source code pulled from GitHub.
Docker images are pushed to AWS Elastic Container Registry (ECR).
Kubernetes cluster is created using AWS EKS.
Auto Scaling and Load Balancing ensure high availability and scalability.
Ingress Controller manages external traffic to the application.
Project Workflow
Step-by-Step Flow
Source Code Management:

The frontend and backend source code is hosted in this GitHub repository.
Containerization:

Dockerfiles (DF) are used to create Docker images for the frontend and backend.
Images are pushed to AWS ECR for storage and versioning.
Cluster Setup:

An AWS EKS Cluster is created using EC2 worker nodes.
Cluster configurations include namespaces for isolating frontend, backend, and database services.
Deployment:

Kubernetes manifests (Deployment, Service, Ingress) are used to deploy:
Frontend Service.
Backend Service.
MongoDB Service.
Load Balancer automatically distributes traffic across multiple nodes.
Scaling and High Availability:

Auto Scaling ensures that the application scales up or down based on traffic.
Kubernetes Horizontal Pod Autoscaler (HPA) manages scaling for pods.
Traffic Management:

An Ingress Controller routes traffic to appropriate services in the cluster.
Prerequisites
Ensure you have the following tools installed:

Docker
AWS CLI
kubectl
eksctl
Deployment Steps
Clone the Repository:

bash
Copy code
git clone https://github.com/your-repo-name.git
cd your-repo-name
Build Docker Images:

Frontend:
bash
Copy code
docker build -t your-frontend-image .
Backend:
bash
Copy code
docker build -t your-backend-image .
Push Images to AWS ECR:

Authenticate with ECR:
bash
Copy code
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <ecr_repository_url>
Push images:
bash
Copy code
docker tag your-frontend-image <ecr_repository_url>/frontend:latest
docker push <ecr_repository_url>/frontend:latest

docker tag your-backend-image <ecr_repository_url>/backend:latest
docker push <ecr_repository_url>/backend:latest
Set Up EKS Cluster:

Create the EKS cluster:
bash
Copy code
eksctl create cluster --name mern-cluster --region <region> --nodegroup-name mern-nodes
Deploy Application to Kubernetes:

Apply Kubernetes manifests:
bash
Copy code
kubectl apply -f k8s-frontend.yaml
kubectl apply -f k8s-backend.yaml
kubectl apply -f k8s-mongo.yaml
kubectl apply -f k8s-ingress.yaml
Verify Deployment:

Check running pods:
bash
Copy code
kubectl get pods
Get application endpoint:
bash
Copy code
kubectl get ingress
Key AWS Services Used
Elastic Kubernetes Service (EKS): For orchestrating the cluster.
Elastic Container Registry (ECR): For storing Docker images.
EC2: Worker nodes for the Kubernetes cluster.
Load Balancer: For distributing traffic.
IAM: For managing permissions.
Features
Fully containerized MERN stack application.
Cloud-native deployment using AWS.
Auto-scaling and load balancing for high availability.
CI/CD-ready for future enhancements.
