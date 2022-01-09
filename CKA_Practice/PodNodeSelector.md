kubectl run nginx-kusc00401 --image=nginx --dry-run=client -o yaml > pod1.yaml

vi pod1.yaml

spec:
  containers
  nodeSelector: 
    disk: ssd

kubectl get nodes -l disk=ssd