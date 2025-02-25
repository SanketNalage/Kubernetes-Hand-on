# Kubernetes Ingress: A Beginner's Guide

This guide explains the concept of **Ingress** in Kubernetes and demonstrates how to set up an Ingress resource to manage external access to your applications.

---

## What is Ingress?

**Ingress** is a Kubernetes resource that manages external HTTP/HTTPS access to services in a cluster. It acts as a **traffic router**, directing incoming requests to the appropriate backend services based on rules defined in the Ingress resource.

### Key Features:
- **Host-based routing**: Route traffic based on the domain name (e.g., `app1.example.com`, `app2.example.com`).
- **Path-based routing**: Route traffic based on the URL path (e.g., `/api`, `/web`).
- **TLS termination**: Support for HTTPS by terminating SSL/TLS at the Ingress level.

---

## Prerequisites

Before you begin, ensure you have the following:
- A running Kubernetes cluster.
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed and configured.
- An **Ingress Controller** installed (e.g., NGINX, Traefik, or AWS ALB Ingress Controller).

---

## Step 1: Install an Ingress Controller

An Ingress Controller is required to fulfill the Ingress resource. Here’s how to install the **NGINX Ingress Controller**:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```
## Step 2:  Deploy a Sample Application
```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
```
## Step 3:  Verify the Deployment and Service:
```sh 
kubectl get deployments
kubectl get services
```
## Step 4:   Create an Ingress Resource
```sh
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: my-app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

## Step 5: Apply the Ingress-Service:
```sh
kubectl apply -f ingress.yaml
```

## Step 6: Expose the path of ingress
```ssh
sudo -E kubectl port-forward service/nginx -n nginx 8080:80 --address=0.0.0.0
```

## if you wich to see then navigated to [django-notes-app-K8s](https://github.com/SanketNalage/Kubernetes-Hand-on/tree/main/django-notes-app-K8s) /k8s folder the file is available of ingress.

### Happy learning! 😊


