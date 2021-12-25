kubectl config use-context k8s

kubectl run nginx-kusc00401 --image=nginx --dry-run=client -o yaml > pod2.yaml

vi pod2.yaml


spec:
  containers:
  - name: nginx-kusc00401 
    image: nginx
  nodeSelector:
    disk: ssd
  
wq!

kubectl create -f pod2.yaml

kubectl get pods 

