### What is the name of the POD that deploys the default kubernetes scheduler in this environment?
kubectl -n kube-system get pods 

### What is the image used to deploy the kubernetes scheduler?
### Inspect the kubernetes scheduler pod and identify the image
kubectl -n kube-system describe pod kube-scheduler-controlplane | grep -i image

### Deploy an additional scheduler to the cluster following the given specification.
### (Use the manifest file used by kubeadm tool. Use a different port than the one used by the current one.)
### Namespace: kube-system
### Name: my-scheduler
### Status: Running
### Custom Scheduler Name
cd /etc/kubernetes/manifests 
cp kube-scheduler.yaml /root/my-scheduler.yaml