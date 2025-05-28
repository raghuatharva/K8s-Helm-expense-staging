
# Helm Charts for Expense Application

This repository contains Helm charts for deploying the `expense-app` microservices including **frontend** and **backend** components on a Kubernetes cluster.

## 🛠️ Components

- `expense-backend`: Node.js-based backend connected to MongoDB.
- `expense-frontend`: React-based frontend served over NGINX.
- Uses NGINX Ingress Controller, ConfigMaps, Secrets, and Horizontal Pod Autoscaler.

---

## 📁 Directory Structure

```bash
helm/
├── expense-backend/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
├── expense-frontend/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
````

---

## 📦 Prerequisites

* Kubernetes Cluster (v1.21+)
* Helm 3.x installed
* NGINX Ingress Controller (for production use)
* Docker registry access for images

---

## 🚀 Installation

```bash
helm repo add expense-app https://your-domain.com/helm-charts
helm install expense-backend ./helm/expense-backend
helm install expense-frontend ./helm/expense-frontend
```

To install in a specific namespace:

```bash
kubectl create namespace expense
helm install expense-backend ./helm/expense-backend -n expense
helm install expense-frontend ./helm/expense-frontend -n expense
```

---

## 🔁 Upgrade Charts

```bash
helm upgrade expense-backend ./helm/expense-backend
helm upgrade expense-frontend ./helm/expense-frontend
```

---

## 🧾 Configuration

Override the default `values.yaml` using `--values` or `--set` flags.

```bash
helm install expense-backend ./helm/expense-backend --set image.tag=v2
```

---

## 🗃️ values.yaml (Backend)

```yaml
replicaCount: 2

image:
  repository: your-registry/expense-backend
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 8080


resources:
  limits:
    cpu: 500m
    memory: 256Mi
```

---

## 🗃️ values.yaml (Frontend)

```yaml
replicaCount: 2

image:
  repository: your-registry/expense-frontend
  tag: latest
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80

env:
  REACT_APP_BACKEND_URL: http://expense-backend:8080

resources:
  limits:
    cpu: 250m
    memory: 128Mi
```

---

## 🔒 Secrets and ConfigMaps

* Secrets: DB credentials, JWT secrets (injected via `values.yaml`)
* ConfigMaps: environment variables

---

## 📈 Monitoring

* Integrated readiness and liveness probes
* Can be extended to support Prometheus annotations


---

## 📜 License

MIT License

---

## 👨‍💻 Maintainers

* [Raghu.H](https://github.com/raghuatharva)
* Email: [raghu.rohan95@gmail.com](mailto:yourname@example.com)
