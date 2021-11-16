### How many DaemonSets are created in the cluster in all namespaces
kubectl get ds --all-namespaces

### Which namespace are the DaemonSets created in?
kubectl get ds --all-namespaces(namespace)

### Which of the below is a DaemonSet?
kubectl get ds --all-namespaces(name)

### On how many nodes are the pods scheduled by the DaemonSet kube-proxy
kubectl -n kube-system get pods -o wide | grep proxy

### What is the image used by the POD deployed by the kube-flannel-ds DaemonSet?
kubectl -n kube-system describe ds kube-flannel-ds | grep -i image

### Deploy a DaemonSet for FluentD Logging.
### Use the given specifications.
### Name: elasticsearch
### Namespace: kube-system
### Image: k8s.gcr.io/fluentd-elasticsearch:1.20
kubectl create deployment elasticsearch --image=k8s.gcr.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml > elasetic.yaml

apiVersion: apps/v1
kind: DaemonSet
metadata:
  creationTimestamp: null
  labels:
    app: elasticsearch
  name: elasticsearch
###   namespace: kube-system <<  이부분 추가
spec:
  selector:
    matchLabels:
      app: elasticsearch
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: elasticsearch
    spec:
      containers:
      - image: k8s.gcr.io/fluentd-elasticsearch:1.20
        name: fluentd-elasticsearch
이외에 해당 형태로 yaml 작성 (몇몇부분 요소를 삭제해야함)
kubectl apply -f elastic.yaml
