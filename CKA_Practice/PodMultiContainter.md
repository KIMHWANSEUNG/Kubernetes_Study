kubectl run kucc1 --image=nginx --dry-run=client -o yaml > pod.yaml

vi pod.yaml

containers:
  name: nginx
- image: nginx
  name: consul
- image: consul


kubectl craete -f pod.yaml

kubectl get pods