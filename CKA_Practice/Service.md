kubectl config use-context k8s

kubectl edit deployment.apps front-end

container:
  ports:
    name: http
  - containerPort: 80
    protocol: TCP

wq!

kubectl expose deploy front-end --name=front-end-svc --type=Nodeport --port=80 --dry-run=client -o yaml > expose.yaml 

vi expose.yaml

ports:
  name: http