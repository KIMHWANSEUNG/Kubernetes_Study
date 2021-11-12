### A pod definition file nginx.yaml is given. Create a pod using the file.
### ls해보면 nginx.yaml이 있음
kubectl apply -f nginx.yaml

### What is the status of the created POD?
kubectl get pods

### Why is the POD in a pending state?
### 답: 스케줄이 되어 있지 않다
kubectl -n kube-system get pods

### Manually schedule the pod on node01.
### nginx pod 삭제
kubectl delete pod nginx 

vi nginx.yaml
### 이부분 추가
spec: 
    nodeName: node01 


### Now schedule the same pod on the controlplane node. Status: Running , Pod: nginx , Node: controlplane? (Delete and recreate the POD if necessary. )

vi nginx.yaml
### 이부분 수정
spec:
    nodeName: controlplane