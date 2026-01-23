# Headlamp – Modern Kubernetes UI (5-Day Learning Series)

<img width="1536" height="1024" alt="85ea801394" src="https://github.com/user-attachments/assets/7c0a9697-82d3-40c6-a5d1-b115ff4c6a85" />


## About
Headlamp is a modern, user‑friendly, and extensible Kubernetes UI developed under Kubernetes SIG‑UI.
With the Kubernetes Dashboard reaching end‑of‑life, Headlamp has emerged as the recommended, community‑supported replacement — offering improved performance, plugin capabilities, better UX, and long‑term sustainability.
This repository contains a 5‑Day hands‑on learning series, designed to help you understand, install, configure, and extend Headlamp in real Kubernetes environments.

## Repository Structure
Each day has its own dedicated directory containing detailed guides, examples, commands, and screenshots.
```
.
├── day1-installation/
├── day2-ui-overview/
├── day3-rbac-configuration/
├── day4-deep-dive/
├── day5-plugins-extensions/
└── README.md
```
## 5‑Day Headlamp Learning Series

### Day 1 — Installing Headlamp
Learn how to install Headlamp using Helm, verify resources, and access the UI.
```
 day1-installation/
```
### Day 2 - UI-Overview
A complete walkthrough of the UI, menus, workload views, cluster insights, and comparisons with Kubernetes Dashboard.
```
day2-ui-overview/
```
### Day 3 - RBAC Configuration
Learn how Headlamp handles authentication, permissions, kubeconfig usage, and how to secure access in production environments.
```
day3-rbac-configuration/
```
### Day 4 - Deep Dive into Features
Explore advanced functionalities:
- Workloads & resource management
- Logs & metrics visualization
- Events, nodes, and storage views
- Real‑time updates
```
day4-deep-dive/
```
### Day 5 — Plugins, GitOps & Extensions
Extend Headlamp with plugins and enhance workflows, including Flux GitOps plugin usage.
```
day5-plugins-extensions/
```


## Prerequisites for the Entire Series
- A working Kubernetes cluster (Kind, Minikube, cloud provider, or on-prem)
- kubectl installed and configured
- helm installed
- Basic understanding of Kubernetes resources

## Quick Start
- Start with `day1-installation/` to install Headlamp via Helm and access the UI.
- Proceed through each day sequentially.

## License
This repository is provided for educational purposes. Refer to individual directories for any additional licensing notes.
