### Identify the pod that has an initContainer configured.
kubectl get pods

### What is the state of the initContainer on pod blue
kubectl describe pod blue

### What is the state of the initContainer on pod blue
kubectl describe pod blue

### Why is the initContainer terminated? What is the reason?
kubectl describe pod blue

### We just created a new app named purple. How many initContainers does it have?
kubectl get pods

### What is the state of the POD?
kubectl describe pod purple

### How long after the craete of the POD will the application come up and be available to user?
kubectl describe pod purple
(initContainer쪽에 Commands에 있는 sleep 시간들의 합)


### Update the pod red to use an initContainer that uses the busybox image and sleeps for 20 seconds
### Pod: red
### initContainer Configured Correctly
kubectl get pods red -o yaml > red.yaml
kubectl delete pod red
vi red.yaml

apiVersion: v1
kind: Pod
metadata:
  name: red
  namespace: default
spec:
  containers:
  - command:
    - sh
    - -c
    - echo The app is running! && sleep 3600
    image: busybox:1.28
    imagePullPolicy: IfNotPresent
    name: red-container
  initContainers:
  - image: busybox
    name: red-initcontainer
    command: ["sleep","20"]
(이렇게 수정)

kubectl apply -f red.yaml

### A new application orange is deployed. There is something wrong with it. Identify and fix the issue.
kubectl get pod orange -o yaml > orange.yaml
kubectl delete pod orange
vi orange.yaml

apiVersion: v1
kind: Pod
metadata:
  name: orange
  namespace: default
spec:
  containers:
  - command:
    - sh
    - -c
    - echo The app is running! && sleep 3600
    image: busybox:1.28
    imagePullPolicy: IfNotPresent
    name: orange-container
  initContainers:
  - command:
    - sh
    - -c
    - sleep 2; (이부분 수정만 하면 댐)
    image: busybox
    imagePullPolicy: Always
    name: init-myservice
(이렇게 수정)

kubectl apply -f orange.yaml
