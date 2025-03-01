docker file create the conneting the backned serivce
docker login
docker build -t backend .
docker images
docker image tag backend:latest sanketnalage/backend:latest
docker images
docker push sanketnalage/backend

connecting the fronted service
docker build -t frontend .
docker image tag frontend:latest sanketnalage/frontend:latest
docker push sanketnalage/frontend

load the images in the kind cluster:
kind load docker-image sanketnalage/backend:latest --name todo-cluster
kind load docker-image sanketnalage/frontend:latest --name todo-cluster

how to see images has been loaded in KIND cluster:
Access the Node's Shell:
Use docker exec to access the shell of the KIND node (replace todo-cluster-control-plane with the name of your control-plane node):
```sh
docker exec -it todo-cluster-control-plane bash
```
List Loaded Images:
Inside the node's shell, list the Docker images:
crictl images

Output will be:
IMAGE                                           TAG                  IMAGE ID            SIZE
docker.io/kindest/kindnetd                      v20241023-a345ebe4   9ca7e41918271       38.6MB
docker.io/kindest/local-path-helper             v20230510-486859a6   be300acfc8622       3.05MB
docker.io/kindest/local-path-provisioner        v20240813-c6f155d6   3a195b56ff154       19.4MB
docker.io/sanketnalage/backend                  latest               0c77f39c943db       401MB
docker.io/sanketnalage/frontend                 latest               bf4828882f2de       49.3MB
registry.k8s.io/coredns/coredns                 v1.11.3              c69fa2e9cbf5f       18.6MB
registry.k8s.io/etcd                            3.5.15-0             2e96e5913fc06       56.9MB
registry.k8s.io/kube-apiserver-amd64            v1.31.2              1e64982a1c83f       95.3MB
registry.k8s.io/kube-apiserver                  v1.31.2              1e64982a1c83f       95.3MB
registry.k8s.io/kube-controller-manager-amd64   v1.31.2              9d92c1a108613       89.5MB
registry.k8s.io/kube-controller-manager         v1.31.2              9d92c1a108613       89.5MB
registry.k8s.io/kube-proxy-amd64                v1.31.2              afab5f24190a6       92.8MB
registry.k8s.io/kube-proxy                      v1.31.2              afab5f24190a6       92.8MB
registry.k8s.io/kube-scheduler-amd64            v1.31.2              1583a68d9a7ee       68.5MB
registry.k8s.io/kube-scheduler                  v1.31.2              1583a68d9a7ee       68.5MB
registry.k8s.io/pause                           3.10                 873ed75102791       320kB

Apply Kubernetes Manifests:
kubectl apply -f kubernetes/postgres-deployment.yml
kubectl apply -f flask-deployment.yml
kubectl apply -f frontend-deployment.yml

