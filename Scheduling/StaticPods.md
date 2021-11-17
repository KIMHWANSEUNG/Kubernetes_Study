### How many static pods exist in this cluster in all namespaces?
static pods == controlplane 이라는 네임스페이스를 가진 pods
kubectl get pods --all-namespaces | grep "\-controlplane" 

### Which of the below components is NOT deployed as a static pod?
kubectl get pods --all-namespaces | grep "\-controlplane" 

### Which of the below components is NOT deployed as a static POD?
kubectl get pods --all-namespaces | grep "\-controlplane" 

### On which nodes are the static pods created currently?
kubectl get pods --all-namespaces -o wide | grep "\-controlplane"

### What is the path of the directory holding the static pod definition files?
ps -ef | grep kubelet
에서 /var/lib/kubelet/config.yaml 파일에서 
grep -i | static /etc/kubernetes/kubelet.conf 검색

### How many pod definition files are present in the manifests folder?
cd /etc/kubernetes/manifets
ls

### What is the docker image used to deploy the kube-api server as a static pod?
grep -i image kube-apiserver.yaml


### Create a static pod named static-busybox that uses the busybox image and the command sleep 1000
kubectl run static-busybox --image=busybox --command sleep 1000 --restart=Never --dry-run=client -o yaml > static-busybox.yaml


### Edit the image on the static pod to use busybox:1.28.4