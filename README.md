# Kuberntes-Hands-on
This repository contains my hands-on practice and implementation of Kuberntes Container Orchestration.

# What is Kubernetes?

## Overview
Kubernetes (often abbreviated as **K8s**) is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. It groups containers into logical units for easy management and discovery.

## Key Features
- **Automated Rollouts and Rollbacks**: Easily update or revert application versions.
- **Scaling**: Automatically scale applications up or down based on demand.
- **Self-Healing**: Restarts failed containers, replaces them, and reschedules them when nodes die.
- **Load Balancing**: Distributes network traffic to ensure stable deployment.
- **Storage Orchestration**: Automatically mounts storage systems (e.g., local, cloud).
- **Secret and Configuration Management**: Securely manage sensitive information.

## Why Kubernetes?
- **Portability**: Run applications consistently across on-premises, hybrid, and multi-cloud environments.
- **Efficiency**: Optimize resource usage and reduce infrastructure costs.
- **Resilience**: Ensure high availability and fault tolerance for applications.
- **Extensibility**: Integrate with a wide range of tools and services.

## Core Concepts
- **Pods**: The smallest deployable units in Kubernetes, containing one or more containers.
- **Nodes**: Physical or virtual machines that run your applications.
- **Cluster**: A set of nodes that run containerized applications managed by Kubernetes.
- **Deployments**: Manage the desired state of your applications (e.g., scaling, updates).
- **Services**: Expose your application to the network.
- **Namespaces**: Organize and isolate resources within a cluster.

## Getting Started
To start using Kubernetes:
1. Set up a Kubernetes cluster (e.g., using [Minikube](https://minikube.sigs.k8s.io/docs/), [Kind](https://kind.sigs.k8s.io/), or a cloud provider like [GKE](https://cloud.google.com/kubernetes-engine), [EKS](https://aws.amazon.com/eks/), or [AKS](https://azure.microsoft.com/en-us/services/kubernetes-service/)).
2. Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/), the command-line tool for Kubernetes.
3. Deploy your first application using a YAML file:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: my-app
   spec:
     replicas: 3
     template:
       spec:
         containers:
         - name: my-container
           image: nginx:latest
    ```