
# Day 2 — Headlamp UI Login & Dashboard Exploration
*(5‑Day Kubernetes Headlamp Series · Post 2/5)*

This guide covers:

1. Logging into Headlamp using a Kubernetes token
2. Navigating the primary dashboards (Overview, Workloads, Nodes, Networking, RBAC, Config & Storage)
3. Browsing **Custom Resource Definitions (CRDs)**
4. Exploring **Gateway API resources** using Headlamp’s **beta** support


---

## 🔐 1. Logging Into Headlamp

Headlamp supports authentication via your **kubeconfig** or a **ServiceAccount token**. To keep the steps portable across clusters, this guide uses a ServiceAccount.

### 1.1 Create a ServiceAccount
```bash
kubectl create serviceaccount headlamp-user -n kube-system
```

### 1.2 Bind RBAC Permissions
> For demonstration purposes we grant cluster‑admin. In production, use minimal permissions.
```bash
kubectl create clusterrolebinding headlamp-user-binding \
  --clusterrole=cluster-admin \
  --serviceaccount=kube-system:headlamp-user
```

### 1.3 Generate an Authentication Token
```bash
kubectl -n kube-system create token headlamp-user
```
Copy the token for login.

<img width="1125" height="586" alt="image" src="https://github.com/user-attachments/assets/ff7027c9-2401-482c-8a22-b9cf7a8ea38a" />


---

## 📊 2. Exploring the Dashboards

After login, Headlamp presents a modern, structured UI grouped into logical sections.

### 2.1 Overview
A quick cluster summary:
- Node & workload counts
- Namespace distribution
- Health/status indicators
- Real‑time status updates

<img width="1125" height="588" alt="image" src="https://github.com/user-attachments/assets/27366289-532a-4d7f-8c1f-bb5f7a8f59cd" />


### 2.2 Workloads
Application‑level resources:
- Deployments, StatefulSets, DaemonSets, ReplicaSets
- Jobs, CronJobs, Pods

Each resource view provides:
- Live logs & events
- YAML viewer
- Metadata & labels
- Linked/owner references

<img width="791" height="390" alt="image" src="https://github.com/user-attachments/assets/2e526ea2-8779-47b1-812a-49e88f233806" />



### 2.3 Nodes
Node insights for performance and scheduling:
- Conditions (Ready, DiskPressure, etc.)
- CPU/Memory usage; allocatable vs. used
- Pod placement per node
- Labels & taints

<img width="1125" height="589" alt="image" src="https://github.com/user-attachments/assets/6c6467e4-ef3c-43fe-95ae-3dc615e370f1" />


### 2.4 Networking
Traffic and connectivity constructs:
- Services, Ingresses
- Endpoints, Network Policies

Visual navigation helps trace service routing and policy effects.

<img width="1125" height="587" alt="image" src="https://github.com/user-attachments/assets/0149e9a4-90c0-4d9b-8075-b5e2260c80ce" />


### 2.5 Access Control (RBAC)
Security and permissions made visual:
- Roles & ClusterRoles
- RoleBindings & ClusterRoleBindings
- ServiceAccounts

<img width="1125" height="587" alt="image" src="https://github.com/user-attachments/assets/3aa41a83-aa56-4897-b67c-c4d7f95d5109" />


### 2.6 Configuration & Storage
Operational building blocks:
- ConfigMaps, Secrets
- PersistentVolumes (PV), PersistentVolumeClaims (PVC)
- StorageClasses

<img width="1125" height="586" alt="image" src="https://github.com/user-attachments/assets/d18ac245-79ad-44e7-b8fb-c9ba2227c99c" />


---

### 🧩 2.6. Custom Resource Definitions (CRDs)

Headlamp includes a dedicated CRD viewer for extended Kubernetes APIs installed by operators and controllers.

**What you can do:**
- List **all CRDs** present in the cluster
- Browse **instances** of each CRD
- Inspect **YAML**, **events**, **conditions**, and **metadata**
- View CRD **schemas/validation** (when provided)
- Filter and search CRDs by group/version/kind

**Common CRD sources:** Flux, ArgoCD, Prometheus Operator, Istio/Linkerd, storage providers, and **Gateway API**.

<img width="1125" height="585" alt="image" src="https://github.com/user-attachments/assets/c26a3432-13fc-47c1-8084-ce61b1c00861" />


---

### 🚦 2.7. Gateway API Exploration (Beta)

If your cluster includes **Gateway API CRDs**, Headlamp’s **beta** views help you understand modern traffic routing beyond classic Ingress.

**Supported objects (varies by cluster install):**
- **GatewayClasses**, **Gateways**
- **HTTPRoutes**, **TLSRoutes**, **GRPCRoutes**
- **TCPRoutes**, **UDPRoutes**

**What you can explore:**
- Gateway **listeners** and their protocols
- Route‑to‑Gateway **relationships**
- Backend **Service** references
- Rule **matches**, **filters**, and TLS settings
- Multi‑layer routing configuration at a glance

<img width="1125" height="586" alt="image" src="https://github.com/user-attachments/assets/e57af99a-8b4e-4b3f-8571-a4b8208274dd" />


> Note: Feature availability depends on the Gateway API version and controllers installed in your cluster.

---

## 📘 Summary
By completing Day 2, you can:
- Authenticate into Headlamp with a Kubernetes token
- Navigate core dashboards for quick insights
- Inspect workloads, nodes, networking, RBAC, and configs/storage
- Browse **CRDs** installed by operators
- Explore **Gateway API** resources using Headlamp’s **beta** support

**Next (Day 3):** Deep‑dive into workloads, logs, events, YAML editing, and practical troubleshooting workflows.

---


