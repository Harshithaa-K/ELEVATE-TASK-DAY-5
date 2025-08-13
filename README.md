# ELEVATE-TASK-DAY-5
# Task 5: Build a Kubernetes Cluster Locally with Minikube

## Objective
Deploy and manage applications in a local Kubernetes cluster using **Minikube**, **kubectl**, and **Docker**.

---

## Tools & Requirements
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Docker](https://www.docker.com/)

---

## Steps

### 1️⃣ Install Minikube and Start the Cluster

# Start Minikube using Docker driver
minikube start --driver=docker

### Verify the cluster is running using command :
minikube status

## create deployment.yaml file
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx:latest
        ports:
        - containerPort: 80

Apply the deployment:

kubectl apply -f deployment.yaml

## Create a service.yaml file to expose the deployment.
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30007

## Apply the service:
kubectl apply -f service.yaml

## Verify the deployment
kubectl get pods
kubectl get svc

## Access the application using below command
minikube ip

Open the app in the browser:
http://<minikube-ip>:30007





