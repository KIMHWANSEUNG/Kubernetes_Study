kubectl config use-context k8s

kubectl run kucc1 --image=nginx --dry-run=client -o yaml > pod3.yaml

vi pod3.yaml

spec:
  containers:
  - image: nginx
    name: nginx
  - image: consul
    name: consul

kubectl create -f pod3.yaml

