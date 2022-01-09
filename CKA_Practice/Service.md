kubectl config use-context k8s

kubectl edit deployment front-end

container:
  ports:
  - containerPort: 80
    name: http
    protocol: TCP
    

kubectl expose deployment front-end --name=front-end-svc --tpye=Nodeport --port=90 --dry-run=client -o yaml > svc.yaml

vi svc.yaml

spec:
  ports:
    name: http

