### How many PODs exist on the system?
kubectl get pods

### What is the command used to run the pod ubuntu-sleeper?
kubectl describe pod ubunt-sleeper


### Create a pod with the ubuntu image to run a container to sleep for 5000 seconds. Modify the file ubuntu-sleeper-2.yaml.
### Note: Only make the necessary changes. Do not modify the name. 
vi ubuntu-sleeper-2.yaml

spec:
    container:
          ...
          command: ["sleep", "5000" ]
wq!
kubectl apply -f ubuntu-sellper-2.yaml

### Create a pod using the file named ubuntu-sleeper-3.yaml. There is something wrong with it. Try to fix it!
### Note: Only make the necessary changes. Do not modify the name.
vi ubuntu-sellper-3.yaml

...
command:
   - "sleep"
   - "1200" (수정)
wq!
kubectl apply -f ubuntu-sleeper-3.yaml

### Update pod ubuntu-sleeper-3 to sleep for 2000 seconds.
### Note: Only make the necessary changes. Do not modify the name of the pod. Delete and recreate the pod if necessary
kubectl delete pod ubuntu-sleeper-3
vi ubuntu-sellper-3.yaml

...
command:
   - "sleep"
   - "2000" (수정)
wq!
kubectl apply -f ubuntu-sleeper-3.yaml

### Inspect the file Dockerfile given at /root/webapp-color. What command is run at container startup?
cd /webapp-color
cat Dockerfile

### Inspect the file Dockerfile2 given at /root/webapp-color. What command is run at container startup?
cat Dockerfile2

### Inspect the two files given at /root/webapp-color-2. What command is run at container startup?
cat Dokcerfile2
cat webapp-color-pod.yaml
(yaml에 써져있는 형태가 Dockerfile2에 써져있는것을 override할것이기 때문에 yaml에 선언된 형태의 pod가 됨)

### Inspect the two files under directory webapp-color-3. What command is run at container startup?
cat Dokcerfile2
cat webapp-color-pod.yaml
(yaml에 써져있는 형태가 Dockerfile2에 써져있는것을 override할것이기 때문에 yaml에 선언된 형태의 pod가 됨)


### Create a pod with the given specifications. By default it displays a blue background. Set the given command line arguments to change it to green

### Pod Name: webapp-green
### Image: kodekloud/webapp-color
### Command line arguments: --color=green
kubectl run webapp-green --image=kodekloud/webapp-color --dry-run=client -o yaml > pod.yaml
vi pod.yaml

spec:
    container:
        args: ["--color=green"]
wq!
kubectl apply -f pod.yaml
        
