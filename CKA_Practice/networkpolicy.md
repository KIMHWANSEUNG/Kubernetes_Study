//다시 풀어보기 

kubectl config use-context hk8s

vi np.yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-rom-namespace
  namespace: fubar
spec:
  podSelector:
    matchLabels:
  policyTypes:
  - Ingress
  ingress:
    - namespaceSelector:
        matchLabels:
          app: my-app
    ports:
    - protocol: TCP
      port: 9000

wq!
kubectl get ns --show-labels

kubectl label ns my-app app=my-app

kubectl create -f np.yaml



