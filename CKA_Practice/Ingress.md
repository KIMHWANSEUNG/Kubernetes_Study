kubectl config use-context k8s

vi ig.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ping
  namespace: ing-internal
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /hello
        pathType: Prefix
        backend:
          service:
            name: hello
            port:
              number: 5678

kubectl create -f ig.yaml

kubectl get pods -n ing-internal -o wide

kubectl get nodes -o wdie

kubectl get svc hello -n ing-internal






