
# Day 1 : Introduction to Kubernetes.

## What is Kubernetes

- Kubernetes is a portable, extensible, open source platform for   managing containerized workloads and services that facilitate both declarative configuration and automation.

- It serves as a robust orchestration tool for organizing containers across multiple servers, ensuring high availability, load balancing, and self-healing.

- Kubernetes = Tool that runs, manages, and scales containerized apps automatically.


## Why Kubernetes

Kubernetes answers many question like following:
 - Container Networking?
 - Resource Management
 - Security
 - High Availability
 - Fault Tolerance

with:
 - Service discovery and load balancing 
 - self healing, etc.

## Kubernetes Components
<img width="4225" height="2028" alt="Image" src="https://github.com/user-attachments/assets/827946c1-f1f2-4370-a3da-d7adf7e58053" />

kube-apiserver : The core component server that exposes the Kubernetes HTTP API.

etcd : Consistent and highly-available key value store for all API server data.

kube-scheduler : Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node.

kube-controller-manager : Runs controllers to implement Kubernetes API behavior.

cloud-controller-manager (optional) : Integrates with underlying cloud provider(s).

Node Components :

kubelet : Ensures that Pods are running, including their containers.

kube-proxy (optional) : Maintains network rules on nodes to implement Services.

Container runtime : Software responsible for running containers. Read Container Runtimes to learn more.

## Pods
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

## Sample yaml

- Imparative way 
```bash
kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml
```

- Declarative way

```bash
apiVersion: v1  < Which version of Kubernetes API you are talking to >
kind: Pod  < What type of object you want to create >
metadata:  < Basic information (identity) about the object >
  name: nginx
spec:  < The actual desired state (what you want Kubernetes to run) >
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```
## Documentation

[Documentation for Overview](https://kubernetes.io/docs/concepts/overview/)

[Documentation for Components](https://kubernetes.io/docs/concepts/overview/components/)
