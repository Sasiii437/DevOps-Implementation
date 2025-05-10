📌 Complete Workflow to Execute (on Windows)
📌 Install Tools:
Install Docker Desktop
Install Jenkins via Docker
Install Terraform
Install AWS CLI
Install kubectl

📌 Commands to Run
1️⃣ Start Jenkins
bash

docker volume create jenkins-data
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins-devops -v jenkins-data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock jenkins/jenkins:lts

Unlock and setup Jenkins via http://localhost:8080

2️⃣ Install Plugins
Docker

AWS CLI Plugin

Kubernetes CLI

Terraform

Prometheus Metrics

3️⃣ Build EKS infra via Terraform
In terraform/:

bash

terraform init
terraform apply

Set your subnet IDs in variables.tf before.

4️⃣ Build, Push Docker Image to ECR
In Jenkins pipeline (or manually)

bash

aws ecr create-repository --repository-name devops-node-app
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <your-ecr-url>
docker build -t devops-node-app ./app
docker tag devops-node-app:latest <your-ecr-url>:latest
docker push <your-ecr-url>:latest


5️⃣ Deploy to EKS
Update kubectl config:

bash

aws eks --region ap-south-1 update-kubeconfig --name devops-eks-cluster
kubectl get svc

Apply your app deployment YAML (to be added)

6️⃣ Start Monitoring Stack
In monitoring/:

bash

docker-compose up -d
Prometheus: localhost:9090
Grafana: localhost:3001


Implementations done:
✅ Node.js app in Docker
✅ CI/CD via Jenkins
✅ AWS EKS via Terraform
✅ Metrics via Prometheus & Grafana
✅ Fully integrated DevOps pipeline
