# Day 1 : Minikube Commands.

Default profile for minikube is "minikube" which is created at the time you run "minikube start" with one node, which acts as both control-plane and worker-node.





## Here are commands to manage profile in minikube:

how to check status for default profile
```bash
    # minikube status
```

how to check status for non-default profile
```bash
    # minikube status -p multinode-demo
where multinode-demo is your non-default profile
```

how to create a non-default profile with specific number of nodes
```bash
    # minikube start --nodes=3 -p multinode-demo
here you will creating new profile as multinode-demo with 3 nodes
```

how to delete a profile in minikube
```bash
    # minikube delete --profile=minikube
```

how to add a node in existing cluser
```bash
    # minikube node add -p minikube
```

how to delete a node from exesting profile
```bash
    # minikube node delete minikube-m02 -p minikube
```

## Here are commands to manage cluster using kubectl

Profile in minikube is same as cluster in kubernetes. Hence, you create a profile in minikube is equivalent to creating a new cluster.



how to check how many clusters are there in current configuration
```bash
    # kubectl config get-contexts
```

how to change context or cluster, you want to work upon
```bash
    #  kubectl config use-context my-cluster-name
  where my-cluster-name is same as minikube profile
  e.g.
    # kubectl config use-context multinode-demo
```
