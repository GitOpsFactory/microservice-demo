# microservice-demo
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/93b4c5a3-29a0-463f-b2b9-951b3b907695" />
Microservices Communication Project Overview

This project demonstrates a simple microservices architecture on Kubernetes using two Python services.

Architecture:

                +------------------+
                |   User Browser   |
                +------------------+
                         |
                         v
                +------------------+
                | Frontend Service |
                | Flask App        |
                +------------------+
                         |
      Internal Kubernetes Service Call
                         |
                         v
                +------------------+
                | Backend Service  |
                | Flask API        |
                +------------------+
Technologies Used
Component	Technology
Frontend App	Python Flask
Backend API	Python Flask
Containerization	Docker
Orchestration	Kubernetes
Local Cluster	Minikube
CI/CD Ready	GitHub Actions
Image Registry	Docker Hub
Frontend Service

The frontend service:

Accepts user requests
Calls backend API internally
Displays backend response in browser

Example:

BACKEND_URL = "http://backend-service:5000/api/data"

Important concept:

backend-service is Kubernetes internal DNS
No hardcoded IP required
Kubernetes automatically resolves service names
Backend Service

The backend service:

Exposes REST API
Returns JSON response
Works independently

Example response:

{
  "message": "Hello from Backend Service"
}

This simulates:

Order service
Payment service
User service
Inventory service
Notification service

used in real enterprise platforms.

Kubernetes Components Used
1. Deployment

Manages pods automatically.

Example:

kind: Deployment

Responsibilities:

Creates pods
Restarts failed containers
Supports scaling
Rolling updates
2. Service

Provides stable networking.

Example:

kind: Service

Responsibilities:

Internal communication
Load balancing
Stable DNS name
3. NodePort

Exposes frontend externally.

type: NodePort

Access from browser:

http://MINIKUBE-IP:30080
Internal Communication Flow

When user opens frontend:

Browser
   ↓
Frontend Pod
   ↓
backend-service
   ↓
Backend Pod

Kubernetes networking handles:

Service discovery
DNS resolution
Load balancing
Docker Flow

Each service has:

Source code
Dockerfile
Separate image

Example:

docker build -t bkuslapur/frontend-app:v1 .

Push images:

docker push bkuslapur/frontend-app:v1
docker push bkuslapur/backend-app:v1
Deployment Flow
Developer
   ↓
GitHub
   ↓
GitHub Actions
   ↓
Docker Build
   ↓
Docker Hub
   ↓
Kubernetes Deployment

This is how enterprise CI/CD pipelines work.
