### How many Labels exist on node node01?
kubectl get nodes node01 --show-labels

### What is the value set to the label beta.kubernetes.io/arch on node01?
amd64

### Apply a label color=blue to node node01
kubectl label nodes node01 color=blue

### Create a new deployment named blue with the nginx image and 3 replicas.
### Name: blue
### Replicas: 3
### Image: nginx
kubectl create deployment blue --image=nginx
kubectl scale deployment blue --replicas=3

### Which nodes can the pods for the blue deployment be placed on?
### Make sure to check taints on both nodes!
kubectl get pods -o wdie

### Set Node Affinity to the deployment to place the pods on node01 only.
### Name: blue
### Replicas: 3
### Image: nginx
### NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution
### Key: color
### values: blue

kubectl get deployments.apps blue -o yaml > blue.yaml

spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: color
            operator: In
            values:
            - blue 
작성하고 저장
kubectl delete deployments.apps blue
kubectl apply -f blue.yaml

### Which nodes are the pods placed on now?
kubectl get pods -o wide


### Create a new deployment named red with the nginx image and 2 replicas, and ensure it gets placed on the controlplane node only.
### Use the label - node-role.kubernetes.io/master - set on the controlplane no
### Name: red
### Replicas: 2
### Image: nginx
### NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution
### Key: node-role.kubernetes.io/master
### Use the right operator
kubectl create deployment red --image=nginx --dry-run -o yaml > red.yaml
vi red.yaml

replicas: 2

spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: node-role.kubernetes.io/master
            operator: Exists
작성하고 저장
kubectl apply -f red.yaml
