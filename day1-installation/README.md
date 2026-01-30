# Day 1 — Installing Headlamp (Modern Kubernetes UI)

Headlamp is a modern, extensible, and user-friendly Kubernetes UI now maintained under Kubernetes SIG-UI. 
This guide covers how to install Headlamp on your Kubernetes cluster using Helm.

---

## Prerequisites

Before starting, ensure the following:

### 1. A running Kubernetes cluster  
You can use any cluster (cloud, on-prem, or local).  
To create a local cluster with Kind (Kubernetes in Docker), follow the official guide:  
https://kind.sigs.k8s.io/docs/user/quick-start/

### 2. Helm installed  
Helm is required to install Headlamp.

Official Helm installation guide:  
https://helm.sh/docs/intro/install/

---
  
## Installation Steps

### Step 1: Add the Headlamp Helm repository

```bash
helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/
```

This adds the official Headlamp chart to your local Helm repositories.

---

### Step 2: Install Headlamp into the kube-system namespace

```bash
helm install my-headlamp headlamp/headlamp --namespace kube-system
```

This deploys all Headlamp components into your cluster.

<img width="1206" height="313" alt="image" src="https://github.com/user-attachments/assets/500151f6-7b7d-4f9e-b945-71a45016ff37" />

---

## Verifying the Installation

Use the commands below to confirm Headlamp is installed correctly.

### Check Helm releases:

```bash
helm ls -n kube-system
```
<img width="1084" height="99" alt="image" src="https://github.com/user-attachments/assets/4c8438bf-742f-42f3-99b3-201d1dad02a1" />

### Check Kubernetes resources created by Headlamp:

```bash
kubectl get all --namespace kube-system -l app.kubernetes.io/instance=my-headlamp
```

<img width="1309" height="351" alt="image" src="https://github.com/user-attachments/assets/836d8995-080a-4b60-b818-9df36c99f8c8" />


You should be able to see all the resources created by the headlamp.

---
## Accessing the Headlamp UI

To quickly access the Headlamp UI locally, use port forwarding:

```bash
kubectl port-forward -n kube-system service/my-headlamp 8080:80
```

Open the following URL in your browser:

http://localhost:8080/

<img width="1919" height="1003" alt="image" src="https://github.com/user-attachments/assets/74259e52-ae95-4279-9e70-97efeb492548" />

If the UI loads successfully, Headlamp is installed and running.

---

## Success

If you are able to access the UI, you have successfully installed Headlamp and can begin exploring the modern Kubernetes Dashboard 
replacement.

---

