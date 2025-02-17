# KIND Cluster Setup Guide

## 1. Installing KIND and kubectl

Install KIND and kubectl using the provided script:

```bash
#!/bin/bash

[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo cp ./kind /usr/local/bin/kind

VERSION="v1.30.0"
URL="https://dl.k8s.io/release/${VERSION}/bin/linux/amd64/kubectl"
INSTALL_DIR="/usr/local/bin"

curl -LO "$URL"
chmod +x kubectl
sudo mv kubectl $INSTALL_DIR/
kubectl version --client

rm -f kubectl
rm -rf kind

echo "kind & kubectl installation complete."
```

## 2. Installing Docker
```
sudo apt-get install docker.io
```

## 3. Check the version of Kubectl,KIND,Docker and see docker is instll or not.
```
kubectl version
kind --version
docker --version
docker ps
```

## 4. If docker does the connect or not install then we can add docker image to user.
```
sudo usermod -aG docker $USER && newgrp docker
```