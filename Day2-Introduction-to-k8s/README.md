
# Day 2 : Introduction to Kubernetes.

## What is Kubernetes

- Kubernetes is a **portable, extensible, open source platform** for managing containerized workloads and services that facilitate both declarative configuration and automation.

- It serves as a **robust orchestration tool** for organizing containers across multiple servers, ensuring high availability, load balancing, and self-healing.

- **Kubernetes = Tool** that runs, manages, and scales containerized apps automatically.


## ❓Why Kubernetes 

💡Kubernetes answers many question like following: 
 - Container Networking?
 - Resource Management
 - Security
 - High Availability
 - Fault Tolerance

with:
 - Service discovery and load balancing 
 - self healing, etc.

## Kubernetes Components ✔️

<img width="1402" height="882" alt="Image" src="https://github.com/user-attachments/assets/5596fe7b-aad4-4a72-92c4-bd42f13d79e1" />

### 🚀<mark>Core Components</mark> 

**kube-apiserver** : The core component server that exposes the Kubernetes HTTP API.

**etcd** : Consistent and highly-available key value store for all API server data.

**kube-scheduler** : Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node.

**kube-controller-manager** : Runs controllers to implement Kubernetes API behavior.

**cloud-controller-manager (optional)** : Integrates with underlying cloud provider(s).

### 🚀<mark>Node Components</mark> 

**kubelet** : Ensures that Pods are running, including their containers.

**kube-proxy** (optional) : Maintains network rules on nodes to implement Services.

**Container runtime** : Software responsible for running containers. Read Container Runtimes to learn more.

<img width="1120" height="1380" alt="Image" src="https://github.com/user-attachments/assets/f2d3d0d2-86d4-4a30-99a3-9375498a7f0e" />

## Documentation

[Documentation for Overview](https://kubernetes.io/docs/concepts/overview/)

[Documentation for Components](https://kubernetes.io/docs/concepts/overview/components/)
