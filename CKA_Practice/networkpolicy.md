### CASE 1: my-app
k get ns --show-labels
라벨 이름 생성
kubectl label ns my-app app=my-app  
라벨 이름 체크
kubectl get ns --show-labels

vi np.yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-port-rom-namespace
  namespace: fubar
spec:
  podSelector: {}
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
wq!

kubectl create -f np.yaml
k get networkpolicy.networking.k8s.io/allow-port-rom-namespace -n fubar

### CASE 2: internal
kubectl create ns internal

kubectl label ns internal type=internal

kubectl get ns --show-labels

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metatdat:
   name: allow-port-from-namespace
   namespace: internal
spec:
   podSelector:
     matchLabels: {}
   policyTypes:
   - Ingress
   ingress:
   - from:
     - namespaceSelector:
         matchLabels:
           type: internal
     ports:
     - port: 9000
