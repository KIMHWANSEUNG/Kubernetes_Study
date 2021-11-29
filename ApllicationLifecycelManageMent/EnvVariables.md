### How many PODs exist on the system?
### in the current(default) namespace
kubectl get pods

### What is the environment variable name set on the container in the pod?
kubectl describe pod webapp-color
APP_COLOR = pink
(APP_COLOR)

### What is the value set on the environment variable APP_COLOR on the container in the pod?
kubectl describe pod webapp-color
APP_COLOR = pink
(pink)

### Update the environment variable on the POD to display a green background
### Note: Delete and recreate the POD. Only make the necessary changes. Do not modify the name of the Pod.
kubectl get pod webapp-color -o yaml > pod.yaml
kubectl delete pod webapp-color 
vi pod.yaml

...
env:
    value: green
wq!
kubectl apply -f pod.yaml

### How many ConfigMaps exists in the default namespace?
kubectl get cm

### Identify the database host from the config map db-config
kubectl describe cm db-config

### Create a new ConfigMap for the webapp-color POD. Use the spec given below.
### ConfigName Name: webapp-config-map
### Data: APP_COLOR=darkblue
kubectl create cm webapp-config-map --from-literal=APP_COLOR=darkblue


### Update the environment variable on the POD to use the newly created ConfigMap
### Note: Delete and recreate the POD. Only make the necessary changes. 
### Do not modify the name of the Pod.
### Pod Name: webapp-color
### EnvFrom: webapp-config-map
kubectl delete pod webapp-color

vi pod.yaml
...
 containers:
  - envFrom:
    - configMapRef:
                name: webapp-config-map
wq!
kubectl apply -f pod.yaml