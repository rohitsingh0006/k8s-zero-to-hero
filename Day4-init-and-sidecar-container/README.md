
# Day 4 : Init & Sidecar containers in Kubernetes.

## Init container

A Pod can have multiple containers running apps within it, but it can also have **one or more init containers**, which are run before the app containers are started.

🚀**Init containers are exactly like regular containers, except:** 
- Init containers always run to completion.
- Each init container must complete successfully before the next one starts.
- If a Pod's init container fails, the kubelet repeatedly restarts that init container until it succeeds. However, if the Pod has a `restartPolicy` of Never, and an init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
  labels:
    name: myapp-pod
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    env:
    - name: FIRSTNAME
      value: "rohit"
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
  initContainers:
  - name: init-myservice
    image: busybox:1.28
    command: ['sh' , '-c']
    args: ['until nslookup myservice.default.svc.cluster.local; do echo waiting for myservice; sleep 2; done']
```

Now run the pod:
```bash
kubectl apply -f initpod.yml
```
It will wait for init container to complete, init container is waiting service to be started, as mentioned in the manifest.
```bash
kubectl get pods
NAME    READY   STATUS     RESTARTS   AGE
myapp   0/1     Init:0/1   0          9s
```

Create the service and pod starts main caintainer:
```bash
kubectl create service clusterip myservice --tcp=80:80
```

<img width="597" height="190" alt="Image" src="https://github.com/user-attachments/assets/3185f134-0cae-435c-8976-716f6a145480" />

## Sidecar container

Sidecar containers are the secondary containers that **run along with the main application container** within the same Pod. These containers are used to enhance or to extend the functionality of the primary app container by providing additional services, or functionality such as logging, monitoring, security, or data synchronization, without directly altering the primary application code.

🚀<mark>**Setting `restartPolicy: Always` makes init container a sidecar container**</mark>

🚀Here is an exampl:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
  labels:
    name: myapp-pod
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    env:
    - name: FIRSTNAME
      value: "rohit"
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
  initContainers:
  - name: init-myservice
    # Setting restartPolicy: Always makes this a sidecar container.
    restartPolicy: Always
    image: busybox:1.28
    command: ['sh' , '-c']
    args: ['until nslookup myservice.default.svc.cluster.local; do echo waiting for myservice; sleep 2; done']
```

## Documentation
Refer to the official Kubernetes documentation for [Init Containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/).

Refer to the official Kubernetes documentation for [sidecar Containers](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/).

