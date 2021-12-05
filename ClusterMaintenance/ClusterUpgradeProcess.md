### This lab tests your skills on upgrading a kubernetes cluster. We have a production cluster with applications running on it. Let us explore the setup first.
kubectl get nodes
kubectl version --short
### How many nodes in the pod ?
kubectl get pods -o wide

### How many nodes can host workloads in this cluster?
kubeclt get pod -o wide 
(node의 종류 개수를 묻는듯)

### How many applications are hosted on the cluster?
kubectl get deployments.apps 

### What nodes are the pods hosted on?
kubeclt get pod -o wide 

### You are tasked to upgrade the cluster. User's accessing the applications must not be impacted. And you cannot provision new VMs. What strategy would you use to upgrade the cluster?
Upgrade one node at a time while moving the workloads to the other


### What is the latest stable version available for upgrade?
### Use the kubeadm tool
kubeadm upgrade plan

### We will be upgrading the master node first. Drain the master node of workloads and mark it UnSchedulable
### Master Node: SchedulingDisabled
kubectl drain controlplane 

### Upgrade the controlplane components to exact version v1.20.0
### Upgrade kubeadm tool (if not already), then the master components, and finally the kubelet. Practice referring to the kubernetes documentation page. Note: While upgrading kubelet, if you hit dependency issue while running the apt-get upgrade kubelet command, use the apt install kubelet=1.20.0-00 command instead
### controlplane Upgraded to v1.20.0
### controlplane Kubelet Upgraded to v1.20.0
apt update

apt install kubeadm=1.20.0-00

kubeadm upgrade apply v1.20.0

apt install kubelet=1.20.0-00

systemctl restart kubelet

### schedulable controlplane node
kubectl uncordon controlplane

### Next is the worker node. Drain the worker node of the workloads and mark it UnSchedulable
kubectl drain node01 --ignore-daemonsets

### Upgrade the worker node to the exact version v1.20.0
ssh node01
apt update

apt install kubeadm=1.20.0-00

kubeadm upgrade node

apt install kubelet=1.20.0-00 

systemctl restart kubelet

ctrl+d

kubectl get nodes

### Remove the restriction and mark the worker node as schedulable again.
kubectl uncordon node01