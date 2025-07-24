# DevOps Node.js Project

### Features:
- GitHub repo with Jenkinsfile
- Dockerized Node.js app
- Jenkins CI pipeline
- Kubernetes deployment (Minikube)

### How to Run:
1. Clone repo
2. Build Docker image
3. Push to DockerHub
4. Deploy on K8s using:
```bash
kubectl apply -f k8s/
kubectl get svc

