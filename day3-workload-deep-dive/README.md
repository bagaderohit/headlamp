
# Day 3 — Creating, Modifying & Debugging Workloads
*(5‑Day Kubernetes Headlamp Series · Post 3/5)*

In Day 3, we focus on **practical workload operations** using Headlamp:

1. Creating a new workload (BusyBox)
2. Modifying an existing workload
3. Debugging workloads using logs & events


---

## 🆕 1. Create a New Workload (BusyBox)
Deploy a minimal BusyBox app that prints messages and sleeps.

### 1.1 Deployment YAML
Create the file:

```
vi test-busybox-deploy.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-busybox
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-busybox
  template:
    metadata:
      labels:
        app: demo-busybox
    spec:
      containers:
      - name: busybox
        image: busybox:1.36
        command: ["sh", "-c"]
        args:
        - |
          echo "Starting BusyBox Demo";
          echo "Processing...";
          sleep 30;
          echo "Done!";
```

### 1.2 Apply the workload
```bash
kubectl apply -f test-busybox-deploy.yaml
```
<img width="532" height="52" alt="image" src="https://github.com/user-attachments/assets/4055d2dc-8e07-4833-be39-3f1b6ef1198a" />


### 1.3 View in Headlamp
Open Headlamp → **Workloads → Deployments → demo-busybox** to inspect:
- Pod status
- ReplicaSet details
- YAML
- Events
- Logs
<img width="1163" height="611" alt="image" src="https://github.com/user-attachments/assets/d4ae8ec7-74a1-4a18-9db5-c8024bacb219" />




---

## 🔧 2. Modify an Existing Workload
Update the BusyBox Deployment by scaling replicas and changing echo messages.

### 2.1 Modify via Headlamp UI
Navigate to **Workloads → Deployments → demo-busybox → Edit YAML** and update:

```yaml
spec:
  replicas: 2
```
<img width="966" height="510" alt="image" src="https://github.com/user-attachments/assets/74b2275f-4c2f-4a49-a5a4-6f88a5a51513" />


### 2.2 Apply changes
Click **Apply**.
Headlamp reflects:
- New ReplicaSet creation
- Pod rollout in real time
- Termination of old Pods

<img width="1160" height="614" alt="image" src="https://github.com/user-attachments/assets/94701e72-83b9-45a7-8482-8b707573ccae" />



---

## 🐞 3. Debug a Workload (Logs + Events)
Use Headlamp’s built‑in logs and events to diagnose issues (e.g., CrashLoopBackOff, bad commands, missing files).
Use the deployment manifest day3-workload-deep-dive/wrong-busybox-deploy.yaml and deploy it on the cluster. The manifest has a wrong command "echox" which will throw error during the execution.
```yaml
command: ["sh", "-c"]
args:
  - |
    set -e # <--For exiting the shell immediately if a command fails
    echo "Starting BusyBox Debug Demo";
    echox "This will fail";   # <-- wrong command on purpose
    echo "You will never see this";
```

### 1.2 Apply the workload
```bash
kubectl apply -f wrong-busybox-deploy.yaml
```


### 3.1 Navigate to the Pod
Go to **Workloads → Deployments → Pods → demo-busybox-xxxxx**.

<img width="1919" height="999" alt="image" src="https://github.com/user-attachments/assets/64d4e020-21c9-404c-977c-33947d9e7b11" />


### 3.2 Check Events
Events reveal:
- Scheduling problems
- Image pull errors
- Command failures
- Container restarts

<img width="1919" height="1000" alt="image" src="https://github.com/user-attachments/assets/4ccb81da-bd34-4925-b382-915f97eb8954" />


### 3.3 View Live Logs
Click **Logs**.
<img width="959" height="472" alt="image" src="https://github.com/user-attachments/assets/e0e43ffb-c65a-4c94-b998-209640498f72" />

Expected output:
```
Starting BusyBox Demo
Processing...
Done!
```
Example error output:
```
sh: echox: not found
```
Helpful for diagnosing:
- CrashLoopBackOff
- Startup failures
- Bad commands
- Permission issues

<img width="1919" height="997" alt="image" src="https://github.com/user-attachments/assets/dc10eaa9-4fcf-4805-9ec5-9a2eaad475db" />



---

## 📘 Summary
By completing Day 3, you can:
- Deploy workloads to Kubernetes
- Modify workloads directly in Headlamp
- Debug Pods using logs & events
- Understand rollout behavior and ReplicaSets

**Day 4 (Next):** RBAC — visualizing Roles, RoleBindings, ClusterRoles, and ServiceAccounts.

---

## 📁 Repo Structure for Day 3
```
day3/
 ├── README.md
 ├── test-busybox-deploy.yaml
 ├── wrong-busybox-deploy.yaml
```


