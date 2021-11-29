### What is the current color of the web application?
### Access the Webapp Portal.
kubectl get deployments.app 
kubectl get rs

sh curl-test.sh 
### Inspect the deployment and identify the number of PODs deployed by it
kubectl get pods

### What container image is used to deploy the applications?
kubectl get deployments.apps
kubectl describe deployments.apps frontend 

### Inspect the deployment and identify the current strategy
kubectl describe deployments.apps frontend 

### Let us try that. Upgrade the application by setting the image on the deployment to
### kodekloud/webapp-color:v2
### (Do not delete and re-create the deployment. Only set the new image name for the existing deployment.)
kubectl edit deployments.apps frontend

spec:
    container:
        image: kodecloud/webapp-color:v2 << 수정 
wq! 저장 후 
kubectl get pods로 상태 확인 후 check 버튼 클릭 


### Up to how many PODs can be down for upgrade at a time
### Consider the current strategy settings and number of PODs - 4
kubectl describe deployments.apps frontend

RollingUpdateStrategy:  25% max unavailable, 25% max surge(surge: 급등하다)
(4개의 pod중 25%만 가능 즉 1개의 pod만 가능 )

### Change the deployment strategy to Recreate
### Do not delete and re-create the deployment. Only update the strategy type for the existing deployment.
kubectl edit deployments.apps frontend

strategy: Recreate
(하위 옵션들 전부 삭제 )


### Upgrade the application by setting the image on the deployment to kodekloud/webapp-color:v3
### Do not delete and re-create the deployment. Only set the new image name for the existing deployment.
 kubectl edit deployments.apps frontend

spect:
    container:
            image: kodekloud/webapp-color:v3
            (수정)
wq!

