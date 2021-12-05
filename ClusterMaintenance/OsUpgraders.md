### Let us explore the environment first. How many nodes do you see in the cluster?
kubectl get nodes

### How many applications do you see hosted on the cluster?
kubectl get deployments.apps


### Which nodes are the applications hosted on?
kubectl get pod -o wide

### We need to take node01 out for maintenance. Empty the node of all applications and mark it unschedulable.
kubectl drain node01 --ignore-daemonsets 

### What nodes are the apps on now?
kubectl get pod -o wide

### The maintenance tasks have been completed. Configure the node node01 to be
kubectl uncordon node01

### How many pods are scheduled on node01 now?
kubectl get pod -o wdie
(0)

### Why are there no pods on node01?
Only when new pods are created they will be scheduled

### Why are the pods placed on the controlplane node?
kubectl describe nodes controlplane | grep -i taint

....(간단한 문제는 넘김)

### What would happen to hr-app if node01 is drained forcefully?
hr-app will be lost forever


### hr-app is a critical app and we do not want it to be removed and we do not want to schedule any more pods on node01.
### Mark node01 as unschedulable so that no new pods are scheduled on this node.
### Make sure that hr-app is not affected.
### Node01 Unschedulable
### hr-app still running on node01?
kubectl cordon node01 