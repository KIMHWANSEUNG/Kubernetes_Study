### Identify the number of containers created in the red pod.
kubectl get pods

### Identify the name of the containers running in the blue pod.
kubectl describe pod blue

### Create a multi-container pod with 2 containers.
### Use the spec given below.
### If the pod goes into the crashloopbackoff then add sleep 1000 in the lemon container.
### Name: yellow
### Container 1 Name: lemon
### Container 1 Image: busybox
### Container 2 Name: gold
### Container 2 Image: redis
kubectl run yellow --image=busybox --restart=Never --dry-run=client -o yaml > yellow.yaml

vi yellow.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: yellow
  name: yellow
spec:
  containers:
  - image: busybox
    name: lemon
  - image: redis
    name: gold
(이렇게 수정)


### Inspect the app pod and identify the number of containers in it.
### It is deployed in the elastic-stack namespace.
kubectl -n elastic-stack get pod,svc


### The application outputs logs to the file /log/app.log. View the logs and try to identify the user having issues with Login
kubectl -n elastic-stack logs app


### Search. Mount the log volume to the sidecar container.
### Only add a new container. Do not modify anything else. Use the spec provided below.
### Name: app
### Container Name: sidecar
### Container Image: kodekloud/filebeat-configured
### Volume Mount: log-volume
### Mount Path: /var/log/event-simulator/
### Existing Container Name: app
### Existing Container Image: kodekloud/event-simulator
kubectl -n elastic-stack get pod app -o yaml > app.yaml
kubectl delete pod app -n elastic-stack

vi app.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2021-12-03T06:16:20Z"
  labels:
    name: app
  name: app
  namespace: elastic-stack
spec:
  containers:
  - image: kodekloud/event-simulator
    imagePullPolicy: Always
    name: app
    volumeMounts:
    - mountPath: /log
      name: log-volume
  - image: kodekloud/filebeat-configured
    name: sidecar
    volumeMounts:
    - mountPath:  /var/log/event-simulator/
      name: log-volume
  volumes:
  - hostPath:
      path: /var/log/webapp
      type: DirectoryOrCreate
    name: log-volume
(이렇게 수정함)

kubectl apply -f app.yaml