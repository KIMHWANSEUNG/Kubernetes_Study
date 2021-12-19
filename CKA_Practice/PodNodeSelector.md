kubectl run nginx-kusc00401 --image=nginx --dry-run=client -o yaml > kus.yaml
vi kus.yaml

spec:
  containers:
   ...
  nodeSelector:
    disk: ssd

kubectl create -f kus.yaml

  