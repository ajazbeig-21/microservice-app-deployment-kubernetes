# 🗳️ Example Voting App on Kubernetes

A simple distributed voting application deployed on Kubernetes, demonstrating microservices, service discovery, and persistent storage. This project uses **Pods** and **Services** for each component and is designed for local development with **Minikube**.

---

## 📦 Architecture

```
[ Vote App ] ---> [ Redis ] ---> [ Worker ] ---> [ Postgres DB ] ---> [ Result App ]
      |               |               |                |                   |
   Service         Service         Pod/Job         Service             Service
```

- **Vote App**: Frontend for voting (Python/Flask)
- **Result App**: Frontend for results (Node.js)
- **Worker**: Background processor (C#/.NET)
- **Redis**: Queue for votes
- **Postgres**: Stores results

---

## 🚀 Getting Started

### 1. Start Minikube

```sh
minikube start
```

### 2. Deploy All Components

Apply all YAML files in the `voting-app-kubernetes` directory:

```sh
kubectl apply -f voting-app-kubernetes/
```

### 3. Check Pods and Services

```sh
kubectl get pods
kubectl get svc
```

### 4. Access the Apps

Get the Minikube IP:

```sh
minikube ip
```

- **Vote App:** [http://<minikube-ip>:31000](http://<minikube-ip>:31000)
- **Result App:** [http://<minikube-ip>:31001](http://<minikube-ip>:31001)

Or use Minikube’s service command:

```sh
minikube service vote
minikube service result
```

---

## 📁 Project Structure

```
voting-app-kubernetes/
├── db-pod.yaml
├── db-service.yaml
├── redis-pod.yaml
├── redis-service.yaml
├── result-app-pod.yaml
├── result-service.yaml
├── vote-service.yaml
├── voting-app-pod.yaml
├── worker-pod.yaml
```

---

## 🛠️ Useful Commands

- View logs:  
  `kubectl logs <pod-name>`
- Port forward (for debugging):  
  `kubectl port-forward svc/vote 8080:8080`
- Delete all resources:  
  `kubectl delete -f voting-app-kubernetes/`

---

## ❤️ Credits

- [Docker Samples: Example Voting App](https://github.com/dockersamples/example-voting-app)
- Kubernetes & Minikube

---

## 📜 License

MIT License