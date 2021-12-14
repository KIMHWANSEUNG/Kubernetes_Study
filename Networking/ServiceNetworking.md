### What network range are the nodes in the cluster part of?
ip a | grep eth0

### What is the range of IP addresses configured for PODs on this cluster?
kubectl -n kube-system get pods
kubectl logs <weave-pod-name> weave -n kube-system

### What is the IP Range configured for the services within the cluster?
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep cluster-ip-range

### What type of proxy is the kube-proxy configured to use?
kubectl logs <kube-proxy-pod-name> -n kube-system

kubectl get ds -n kube-system
