# 🚀 Voting App Kubernetes Deployment Guide

This guide explains how to deploy the voting app using Kubernetes **Deployment** resources for each component. Deployments provide self-healing, rolling updates, and easy scaling for your pods.

---

## 📦 Components Deployed

- **vote**: Voting frontend
- **result**: Results frontend
- **worker**: Background processor
- **redis**: In-memory queue
- **db**: PostgreSQL database

---

## 📝 Prerequisites

- [Minikube](https://minikube.sigs.k8s.io/docs/) installed and running
- [kubectl](https://kubernetes.io/docs/tasks/tools/) installed

---

## 🛠️ Deployment Steps

### 1. Start Minikube

```sh
minikube start
```

### 2. Deploy All Components

Apply all deployment and service YAML files:

```sh
kubectl apply -f .
```

> Make sure you are in the `deployment` directory containing all the YAML files.

### 3. Verify Deployments and Pods

```sh
kubectl get deployments
kubectl get pods
kubectl get svc
```

---

## 🌐 Accessing the Applications

Get the Minikube IP:

```sh
minikube ip
```

- **Vote App:** `http://<minikube-ip>:31000`
- **Result App:** `http://<minikube-ip>:31001`

Or open services directly:

```sh
minikube service vote
minikube service result
```

---

## 📁 Files in This Directory

- `vote-deployment.yaml`
- `vote-service.yaml`
- `result-deployment.yaml`
- `result-service.yaml`
- `worker-deployment.yaml`
- `redis-deployment.yaml`
- `redis-service.yaml`
- `db-deployment.yaml`
- `db-service.yaml`
- `ingress.yaml`

---

## 🌐 Exposing Services with Ingress

You can use the provided `ingress.yaml` to expose your services via a single external endpoint and custom paths.

### 1. Enable Ingress in Minikube

```sh
minikube addons enable ingress
```

### 2. Apply the Ingress Resource

```sh
kubectl apply -f ingress.yaml
```

### 3. Update Your Hosts File (Optional)

Add the following line to your `/etc/hosts` file to map the custom domain to Minikube's IP:

```
<minikube-ip> vote-result.com
```

Replace `<minikube-ip>` with the output of `minikube ip`.

### 4. Access the Vote App

Open in your browser:

```
http://vote-result.com/lets-vote
```

---

## 🔄 Scaling Deployments

To scale any component (e.g., vote app to 3 replicas):

```sh
kubectl scale deployment vote --replicas=3
```

---

## 🧹 Cleanup

To remove all resources:

```sh
kubectl delete -f .
```

---

## 📚 References

- [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)

---