# 🚀 Deploying a To-Do List App on KIND Cluster

---

## 📌 1️⃣ **Login to Docker**
```sh
docker login
```

---

## 🔧 2️⃣ **Build and Push Backend Image**
```sh
docker build -t backend .
docker images
docker tag backend:latest sanketnalage/backend:latest
docker push sanketnalage/backend
```

---

## 🎨 3️⃣ **Build and Push Frontend Image**
```sh
docker build -t frontend .
docker tag frontend:latest sanketnalage/frontend:latest
docker push sanketnalage/frontend
```

---

## 📦 4️⃣ **Load Docker Images into KIND Cluster**
```sh
kind load docker-image sanketnalage/backend:latest --name todo-cluster
kind load docker-image sanketnalage/frontend:latest --name todo-cluster
```

---

## 🔍 5️⃣ **Verify Loaded Images in KIND**
### 🖥️ Access the Node's Shell
```sh
docker exec -it todo-cluster-control-plane bash
```
### 📜 List Loaded Images
```sh
crictl images
```
**✅ Expected Output:**
```
docker.io/sanketnalage/backend                  latest               0c77f39c943db       401MB
docker.io/sanketnalage/frontend                 latest               bf4828882f2de       49.3MB
```

---

## 🚀 6️⃣ **Apply Kubernetes Manifests**
```sh
kubectl apply -f kubernetes/postgres-deployment.yml
kubectl apply -f flask-deployment.yml
kubectl apply -f frontend-deployment.yml
```

---

🎉 **Congratulations! Your To-Do List app is now deployed on your KIND cluster!** 🎉
