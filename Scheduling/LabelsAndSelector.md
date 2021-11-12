### We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment? (Use selectors to filter the output)
### pod의 라벨을 보는 명령어
kubectl get pods --show-labels
kubectl get pods -l env=dev 
### 갯수 세기
kubectl get pods -l env=dev --no-headers | wc -l

### How many PODs are in the finance business unit (bu)?
kubectl get pods -l bu=finance
### 갯수 세기
kubectl get pods -l bu=finance --no-headers | wc -l

### How many objects are in the prod environment including PODs, ReplicaSets and any other objects?
### 답: 7
kubectl get all -l env=prod

### Identify the POD which is part of the prod environment, the finance BU and of frontend tier?
kubectl get pods -l env=prod,bu=finance,tier=frontend

### A ReplicaSet definition file is given replicaset-definition-1.yaml. Try to create the replicaset. There is an issue with the file. Try to fix it.( ReplicaSet: replicaset-1 Replicas: 2)
kubectl apply -f replicaset-definition-1.yaml
#### 에러내용
#### The ReplicaSet "replicaset-1" is invalid: spec.template.metadata.labels: Invalid value: map[string]string{"tier":"nginx"}: `selector` does not match template `labels`
template:
    metadata:
        matchLabels:
            tier: frontend  ==> 수정
### 수정 후에 
kubectl apply -f replicaset_defination-1.yaml
