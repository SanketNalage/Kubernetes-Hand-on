# Django Project with Kubernetes (KinD)

This project demonstrates how to containerize a small Django application and deploy it to a Kubernetes cluster using **KinD** (Kubernetes in Docker).

---

## Prerequisites

Before you begin, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [KinD (Kubernetes in Docker)](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

---

## Installation
1. Build the app
```
docker build -t notes-app .
docker images
```
2. Tag the create image in the docker hub
```
docker image tag notes-apps"latest sanketnalage/notes-app
```
3. Push the tag image to docker hub
```
docker push sanketnalage/notes-apps
```

4. Run the app
```
docker run -d -p 8000:8000 notes-app:latest
```

