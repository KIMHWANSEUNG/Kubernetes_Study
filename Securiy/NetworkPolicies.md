### How many network policies do you see in the environment?
### We have deployed few web applications, services and network policies. Inspect the environment.
kubectl get networkpolicy


kubectl get po --show-labels | grep name=payroll


### What type of traffic is this Network Policy configured to handle?
kubectl describe networkpolicy

Policy Types: (여기를 보면된다.)


### What is the impact of the rule configured on this Network Policy?
Traffic From Internal to Payroll POD is allowed


### Create a network policy to allow traffic from the Internal application only to the payroll-service and db-service.
### Use the spec given on the below. You might want to enable ingress traffic to the pod to test your rules in the UI.


### Policy Name: internal-policy
### Policy Type: Egress
### Egress Allow: payroll
### Payroll Port: 8080
### Egress Allow: mysql
### MySQL Port: 3306

vi network.yaml

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP


kubectl create -f network.yaml 
