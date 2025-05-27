# SIT323/737 Task 6C – Kubernetes Application Deployment

(Since unfamiliar with writing markdown files, the format has been optimized by ai tools）

This repository contains the necessary configuration files and instructions to deploy a Node.js microservice application to a Kubernetes cluster using Minikube.

---

## Project Structure

```

.
├── app/                    # Node.js application source code
├── Dockerfile              # Dockerfile for building the image
├── deployment.yaml         # Kubernetes Deployment configuration
├── service.yaml            # Kubernetes Service configuration
└── README.md               # Deployment instructions (this file)

````

---

## Prerequisites

Before starting, ensure you have the following tools installed:

- [Docker](https://www.docker.com/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Node.js](https://nodejs.org/)
- [Git](https://git-scm.com/)

Check tool versions using:

```bash
docker --version
minikube version
kubectl version --client
node -v
````

---

## Deployment Steps

### Step 1: Clone the Repository

```bash
git clone https://github.com/<your-username>/sit323-2025-prac6c.git
cd sit323-2025-prac6c
```

### Step 2: Start Minikube

```bash
minikube start --driver=docker
```

You can check if Minikube is running:

```bash
minikube status
```

---

### Step 3: Build Docker Image

If you're pushing to Docker Hub:

```bash
docker build -t <your-dockerhub-username>/node-app .
```

### Step 4: Push Docker Image

```bash
docker login
docker push <your-dockerhub-username>/node-app
```

Ensure `deployment.yaml` uses the same image name, e.g.:

```yaml
containers:
  - name: node-app
    image: <your-dockerhub-username>/node-app
```

---

### Step 5: Deploy the Application

Apply the Kubernetes configuration files:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

### Step 6: Verify the Deployment

Check Pods and Services:

```bash
kubectl get pods
kubectl get services
```

Wait until the pod is in `Running` state.

---

### Step 7: Access the Application

#### Option 1: Use `minikube service` (Recommended)

```bash
minikube service node-app-service
```

This will open the app in your default browser.

#### Option 2: Use `kubectl port-forward`

```bash
kubectl port-forward service/node-app-service 8080:3000
```

Then visit: [http://localhost:8080](http://localhost:8080)
