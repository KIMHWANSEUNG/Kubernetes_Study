### Deploy a pod named nginx-pod using the nginx:alpine image. Name: nginx-pod , Image: nginx:alpine
kubectl run nginx-pod --image=nginx:alpine

### Deploy a redis pod using the redis:alpine image with the labels set to tier=db. ,Pod Name: redis Image: redis:alpine Labels: tier=db
kubectl run redis --image=redis:alpine --labels=tier=db

### Create a service redis-service to expose the redis application within the cluster on port 6379
kubectl expose pod redis --name redis-service --port 6379 --target-port 6379
### svc== service의 줄임말 
kubectl describe svc redis-service

### Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas.  Name: webapp , Image: kodekloud/webapp-color ,Replicas: 3
kubectl create deployment webapp --image=kodekloud/webapp-color

kubectl scale deployment --replicas=3 webapp

### Create a new pod called custom-nginx using the nginx image and expose it on container port 8080.
kubectl run custom-nginx --image=nginx --port 8080

### Create a new namespace called dev-ns.
kubectl create ns dev-ns

### Create a new deployment called redis-deploy in the dev-ns namespace with the redis image. It should have 2 replicas
kubectl create deployment redis-deploy --image=redis --namespace=dev-ns --dry-run=client -o yaml > redis.yaml
vi redis.yaml
### 파일 열어서 replicaset : 2 로 수정 
kubectl apply -f redis.yaml

### dev-ns 조회 
kubectl get deployments.apps -n dev-ns

### Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.
kubectl run httpd --image=httpd:alpine --port 80 --expose --dry-run=client -o yaml
### 이걸로 실행
kubectl run httpd --image=httpd:alpine --port 80 --expose
