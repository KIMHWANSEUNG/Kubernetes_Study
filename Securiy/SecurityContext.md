### What is the user used to execute the sleep process within the ubuntu-sleeper pod?
### In the current(default) namespace.
kubectl exec ubuntu-sleeper -- whoami

### Edit the pod ubuntu-sleeper to run the sleep process with user ID 1010.
### Note: Only make the necessary changes. Do not modify the name or image of the pod.
kubectl delete po ubuntu-sleeper

vi po.yaml

---
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper
  namespace: default
spec:
  securityContext:
    runAsUser: 1010
  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    name: ubuntu-sleeper

kubectl apply -f po.yaml

### A Pod definition file named multi-pod.yaml is given. With what user are the processes in the web container started?
cat multi-pod.yaml 

### With what user are the processes in the sidecar container started?
cat multi-pod.yaml 
  securityContext:
    runAsUser: 1001

### Update pod ubuntu-sleeper to run as Root user and with the SYS_TIME capability.
### Pod Name: ubuntu-sleeper
### Image Name: ubuntu
### SecurityContext: Capability SYS_TIME
kubectl delete po ubuntu-sleeper

vi po1.yaml

---
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper
  namespace: default
spec:
  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    name: ubuntu-sleeper
    securityContext:
      capabilities:
        add: ["SYS_TIME"]
wq!

kubectl apply -f po1.yaml


### Now update the pod to also make use of the NET_ADMIN capability.
### Note: Only make the necessary changes. Do not modify the name of the pod.
### Pod Name: ubuntu-sleeper
### Image Name: ubuntu
### SecurityContext: Capability SYS_TIME
### SecurityContext: Capability NET_ADMIN

kubectl delete po ubuntu-sleeper

vi po2.yaml
---
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper
  namespace: default
spec:
  containers:
  - command:
    - sleep
    - "4800"
    image: ubuntu
    name: ubuntu-sleeper
    securityContext:
      capabilities:
        add: ["SYS_TIME", "NET_ADMIN"]

kubectl apply -f po2.yaml
