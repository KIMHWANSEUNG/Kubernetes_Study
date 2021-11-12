### 서비스 갯수 가져오기
kubectl get services

### kubernets 라는 이름의 서비스의 type 이 무엇인가?
kubectl describe service kubernetes | grep -i type

### kubernets 라는 이름의 서비스의 target port가 무엇인가?
kubectl describe services kubernetes | grep -i targetPort

### kubernets 라는 이름의 서비스의 라벨 갯수는?
kubectl describe services kubernetes
Labels 갯수 세기 

### kubernets 라는 이름의 서비스의 엔드포인트 갯수는?
kubectl describe services kubernetes
endpoint 갯수 세기

### How many Deployments exist on the system now?
kubectl get deployments.apps

### What is the image used to create the pods in the deployment?
kubectl describe deployments.apps simple-webapp-deployment | grep -i image
### Create a new service to access the web application using the service-definition-1.yaml file
#### Name: webapp-service
#### Type: NodePort
#### targetPort: 8080
#### port: 8080
#### nodePort: 30080
#### selector: simple-webapp
kubectl expose deployment simple-webapp-deployment --name=webapp-service --target-port=8080 --type=NodePort --port=8080 --dry-run=client -o yaml > svc.yaml
vi svc.yaml 
ports에 nodePort:30080 을 추가하고 저장
kubectl apply -f svc.yaml