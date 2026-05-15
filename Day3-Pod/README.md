
# Day 3 : Pods

Pods are the <mark>**smallest deployable**</mark> units of computing that you can create and manage in Kubernetes.

We have two methods to create pods or any object in kubernetes, i.e. <mark>**imperative way and declarative way**</mark>.





## 🚀Here is how we create a pod using imperative way: 

```bash
kubectl apply -f https://k8s.io/examples/pods/simple-pod.yaml
```
## 🚀Here is how we create a pod using declarative way:

```bash  
apiVersion: v1          < Which version of Kubernetes API you are talking to >
kind: Pod               < What type of object you want to create >
metadata:               < Basic information (identity) about the object >
  name: mypod
spec:                   < The actual desired state (what you want Kubernetes to run) >
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

✔️How to run the above mentioned sample yaml manifest. Save the file as pod.yaml 

```bash
kubectl apply -f pod.yaml
```
OR
```bash
kubectl create -f pod.yaml
```

✔️How to check status
```bash
kubectl get pod
```

✔️How to delete this pod 
```bash
kubectl delete pod/mypod
```
✔️How to access a pod or get into a pod
```bash
kubectl exec -it pod/mypod
```

✔️How to do a prot-forward for a pod and run it in browser
```bash
kubectl port-forward pod/mypod 8080:80
then you may run it in bowser with URL http://localhost:8080
```

## Multi-container pod
We can create **more than one containers** in a pod as well, if required, but we keep one container per pod for good manageability 

🚀Here is a sample manifest 
```bash
apiServer: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: con1
    image: nginx
	ports:
	- containerPort: 80
  - name: con2
    image: linuxserver/firefox
	ports:
	- containerPort: 3000
```

Here, how to run and check
```bash
kubectl apply -f pod.yaml
```

How to access a particular container in this pod 
```bash
kubectl exec -it pod/mypod -c con1
```
OR
```bash
kubectl exec -it pod/mypod -c con2
```

☑️What if, you run this exec command without container name
```bash
kubectl exec -it pod/mypod -n devops -- bash
Defaulted container "con1" out of: con1, con2
```

## Lifecycle of a Pod
While a Pod is running, the kubelet is able to restart containers to handle some kind of faults. Within a Pod, Kubernetes tracks different container states and determines what action to take to make the Pod healthy again. This is done in a polling loop that periodically reconciles the desired state (a Pod spec) with the actual state of the running containers.

### Pod Phases

**Pending** : The Pod has been accepted by the Kubernetes cluster, but one or more of the containers has not been set up and made ready to run. This includes time a Pod spends waiting to be scheduled as well as the time spent downloading container images over the network.

**Running** : The Pod has been bound to a node, and all of the containers have been created. At least one container is still running, or is in the process of starting or restarting.

**Succeeded** : All containers in the Pod have terminated in success, and will not be restarted.

**Failed** : All containers in the Pod have terminated, and at least one container has terminated in failure. That is, the container either exited with non-zero status or was terminated by the system, and is not set for automatic restarting.

**Unknown** : For some reason the state of the Pod could not be obtained. This phase typically occurs due to an error in communicating with the node where the Pod should be running.
