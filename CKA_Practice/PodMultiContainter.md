kubectl run kucc1 --image=nginx --dry-run=client -o yaml > multi.yaml

vi multi.yaml

spec:
  containters:
  - image: nginx
    name: nginx
  - image: consul
    name: consul

kubectl create -f multi.yaml 