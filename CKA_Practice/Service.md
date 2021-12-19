kubectl get deployments.apps

k edit deployment front-end

spec:
  containers: 
    ...
    ports:
    - containerPort: 80
      name: http
      protocol: TCP

k expose deploy front-end --name=front-end-svc --type=NodePort --port=80 --dry-run=client -o yaml > sv.yaml

vi sv.yaml

spec:
  ports:
  - port: 80
    protocol: tCp
    targetPort: 80
    name: http

kubectl create -f sv.yaml

kubectl get svc