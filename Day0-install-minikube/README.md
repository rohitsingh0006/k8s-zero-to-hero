
# Day 0 : To create the practice environment and meet the prerequisites.

We will be using minikube on ubuntu linux. If you are using windows/mac system you may use VMware to create a VM of Ubuntu linux or Use Azure VM or any other cloud providers' VM.

Minikube : This is a software to facilitate kubernetes cluster on Ubuntu.




## Install docker & minikube and prepare k8s setup

Here are steps to install docker and minikube on ubuntu:

```bash
  install docker
    # apt update
    # sudo apt install apt-transport-https ca-certificates curl software-properties-common
    # curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    # sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    # sudo apt install docker-ce
    # usermod -aG docker <normal_user> 
```
```bash
  install minikube
    # curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
    # chmod +x kubectl
    # sudo mv kubectl /usr/local/bin/
    # curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    # sudo install minikube-linux-amd64 /usr/local/bin/minikube
    # minikube start --driver=docker
    - OR - 
    # minikube start --driver=docker --force
```
```bash
    verify with :
    # minikube status
    # kubectl get nodes
```


## Sample Output

<img width="1242" height="577" alt="Image" src="https://github.com/user-attachments/assets/9da7da4f-cd50-490a-b95d-ee7d9fa7b2b7" />
