# Day 4 — Kubernetes RBAC & Dashboard Access Control
*(5‑Day Kubernetes Headlamp Series · Post 4/5)*

Day 4 focuses on **Kubernetes Role‑Based Access Control (RBAC)** and how it directly impacts **what users can see and do inside Headlamp**.

This walkthrough covers two parts:

1. **Exploring RBAC inside Headlamp** (Access Control section)
2. **Restricting Headlamp access** using a **ServiceAccount token** + **Role/RoleBinding** (least‑privilege)

---

## ✅ Part 1 — Explore RBAC in Headlamp (UI)

Headlamp provides a dedicated **Security** area that helps you understand RBAC visually instead of scanning YAML.

### 1. Navigate to RBAC views
In Headlamp, open:

- **Security → ServiceAccounts**
- **Security → Roles**
- **Security → RoleBindings**

These pages help you quickly answer:
- Which identity is being used? (ServiceAccount)
- Which permissions are granted? (Role/ClusterRole)
- How are they attached? (RoleBinding/ClusterRoleBinding)

<img width="1917" height="954" alt="image" src="https://github.com/user-attachments/assets/6849e8a2-ded0-4766-adde-4c8bbd2eba10" />



### 2. Trace access: ServiceAccount → Binding → Role
A useful workflow inside Headlamp:

1. Open **ServiceAccounts** and select your ServiceAccount (example: `headlamp-readonly`)
2. Check which **RoleBindings** refer to it
3. Open the referenced **Role** and validate:
   - allowed resources (pods, deployments, etc.)
   - allowed verbs (`get`, `list`, `watch`)

<img width="1919" height="959" alt="image" src="https://github.com/user-attachments/assets/c93c010d-2145-4038-a300-a4b70fcdf57c" />

<img width="1919" height="960" alt="image" src="https://github.com/user-attachments/assets/0f6ecae5-5217-4b6c-b5cc-4323f8599a44" />



---

## 🔒 Part 2 — Restrict Headlamp Access Using ServiceAccount Token

### Goal
Create a **restricted dashboard user** that:

- ✅ Can **view** Pods, Deployments, Services (read‑only)
- ✅ Can view **Events** (optional but useful)
- ❌ Cannot **edit** workloads
- ❌ Cannot view **Secrets**
- ✅ Restricted to **one namespace** (`default`)

### Approach
We will create:

- `ServiceAccount`: **headlamp-readonly**
- `Role`: read-only permissions in **default** namespace
- `RoleBinding`: bind the Role to the ServiceAccount

---

## 🧾 Apply RBAC Manifest

A single multi‑doc manifest is provided:

- `./day4-rbac-manifest.yaml`

Apply it:

```bash
kubectl apply -f day4-rbac-manifest.yaml
```

📌 **What this creates**
- ServiceAccount: `headlamp-readonly` (namespace `default`)
- Role: `headlamp-readonly-role` (read-only on pods/services/deployments/replicasets + events)
- RoleBinding: `headlamp-readonly-binding`

---
<img width="798" height="123" alt="image" src="https://github.com/user-attachments/assets/8198d44c-f685-446d-8948-0108ce2e766c" />


## 🔑 Generate Token for Headlamp Login

Generate a token for the restricted ServiceAccount:

```bash
kubectl -n default create token headlamp-readonly
```

Copy the token and use it on the Headlamp login screen.

<img width="1919" height="957" alt="image" src="https://github.com/user-attachments/assets/956fa105-dd3a-40d5-96fd-6115d3318e16" />


---

## 🔎 Validate Restricted Access in Headlamp

After logging in with the restricted token, observe the UI differences:

- ✅ Workloads in `default` namespace are visible
- ✅ You can inspect Pods/Deployments and view YAML (read-only)
- ✅ Events are visible (helps troubleshooting)
- ❌ Edit/Apply actions are not available (or fail with Forbidden)
- ❌ Secrets are not visible / access denied
- ❌ Other namespaces are not accessible

<img width="1919" height="953" alt="image" src="https://github.com/user-attachments/assets/178fe747-beed-4ecb-9f6f-f7fcb862541b" />

<img width="1915" height="951" alt="image" src="https://github.com/user-attachments/assets/c3e09582-a4d6-4c5b-a67a-47ad94c5132e" />




## 🧹 Cleanup

Remove the demo resources:

```bash
kubectl delete -f day4-rbac-manifest.yaml
```


## 🧭 Next (Day 5)
Day 5 will wrap up the series with advanced usage and best practices.
