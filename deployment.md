
### deployment 정보 가져오기
kubectl get deployments.apps

### deployment 이미지 정보 가져오기
kubectl describe deployments.apps frontend-deployment | grep -i image

### deployment 생성  spec : Name: httpd-frontend; Replicas: 3; Image: httpd:2.4-alpine
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine
kubectl scale deployment --replicas=3