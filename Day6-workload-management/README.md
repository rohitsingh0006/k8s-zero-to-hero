
# Day 5 : Workload Management

Kubernetes provides several built-in APIs for declarative management of your workloads and the components of those workloads.
🚀The built-in APIs for managing workloads are:
- ✔️Replication conlroller
- ✔️Replica Set
- ✔️Deployment
- ✔️Daemonset
- ✔️statefulset

## 🚀Replication Controller

✔️Typically we want to replicate our containers i.e. our application, for several reasons which include reliability, load balancing, and scaling. By having multiple versions of the application we prevent problems of one or more pods fail.

✔️The Replication Controller is the original form of Replication in Kubernetes. It is been replaced by Replica sets. But, as the Replication Controller is widely used it is worth understanding what is it and how it works.

✔️Replication Controller enables us to easily create multiple pods. If we make sure that a number of pods always exists. If a pod crashes, the Replication Controller replaces it with a new pod. The Replication Controller also provides other benefits such as the ability to scale the number of pods and to update or delete multiple pods with a single command.

✔️The Replication Controller can have an optional selector and spec, where we can provide the labels used in the pods which is used to label query over the pods that should match with the replica count. When the selector is not provided it will assume that the provided template labels will be used as the selector.

Here is an example:

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: rc-test
  namespace: test-rc
  labels:
    type: replica-set
    env: demo
spec:
  template:
    metadata:
      labels:
        type: replica-set
        env: demo
    spec:
      containers:
      - name: nginx-container
        image: nginx
        ports:
        - containerPort: 80
  replicas: 3
```

Now let's run it:

```bash
kubectl apply -f test-rc.yaml
```
To check:
```bash
kubectl get pods -o wide
```

## 🚀Replica-set
✔️Replica Sets are declared in the same way as Replication Controller **except that they have more options for the selectors**. The Selector is mandatory for Replica sets as match labels you can provide the pod labels to query the pods to match with the replica count.
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rc-test
  namespace: test-rs
  labels:
    type: replica-set
    env: demo
spec:
  template:
    metadata:
      labels:
        type: replica-set
        env: demo
    spec:
      containers:
      - name: nginx-container
        image: nginx
        ports:
        - containerPort: 80
  replicas: 3
  selector:
    matchLabels:
      env: demo
```

☑️Now let's run it:
```bash
kubectl apply -f test-rs.yaml
```

To check:
```bash
kubectl get replicaset
```
\- OR -
```bash
kubectl get rs
```
```bash
kubectl get po
```
✔️another example of replicaset with match-expression
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-rs
spec:
  replicas: 3
  selector:
    matchExpressions:
    - key: app
      operator: In
      values:
      - nginx
    - key: env
      operator: NotIn
      values:
      - prod
  template:
    metadata:
      labels:
        app: nginx
        env: dev
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```
☑️Now let's run it:
```bash
kubectl apply -f test-rs.yml
```
Check it:
```bash
kubectl get rs
```
```bash
kubectl get po
```

## 🚀Deployment
✔️A Deployment manages a set of Pods to run an application workload, usually one that doesn't maintain state. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate.


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
  namespace: devops
  labels:
    env: demo
spec:
  template:
    metadata:
      name: nginx
      namespace: devops
      labels:
        env: demo
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
  replicas: 3
  selector:
    matchLabels:
      env: demo
```
☑️Now let's run it:
```bash
kubectl apply -f deploy.yml
```
Check it:
```bash
kubectl get deploy
```
```bash
kubectl get po
```






## Documentation

[Documentation for Overview](https://kubernetes.io/docs/concepts/overview/)

[Documentation for Components](https://kubernetes.io/docs/concepts/overview/components/)
