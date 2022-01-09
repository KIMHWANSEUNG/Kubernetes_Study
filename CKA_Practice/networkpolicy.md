kubectl config use-context hk8s

kubectl get ns --show-labels

kubectl label ns my-app app=my-app 

vi np.yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-rom-namespace
  namespace: fubar
spec:
  podSelector:
    matchLabels: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          app: my-app
    - podSelector:
        matchLabels: {}
    ports:
    - protocol: TCP
      port: 9000


