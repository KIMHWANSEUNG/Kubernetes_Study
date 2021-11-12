### Replicaset 갯수 구하기
kubectl get replicasets.apps

### Replicaset image 알아내기
kubectl describe replicasets.apps new-replica-set | grep -i image

### Replicaset pod 동작 갯수 알아내기
kubectl describe replicasets.apps new-replica-set

## pod 동작 안하는 이유 
### pod 이름 찾아서
kubectl get pods 

### describe로 세부 원인 찾기
kubectl describe pod pod이름 

### error: unable to recognize "replicaset-definition-1.yaml": no matches for kind "ReplicaSet" in version "v1"
### vi로 열어서 version:apps/v1 으로 고치고 실행시키기
kubectl apply -f replicaset-definition-1.yaml

### The ReplicaSet "replicaset-2" is invalid: spec.template.metadata.labels: Invalid value: map[string]string{"tier":"nginx"}: `selector` does not match template `labels`
### frontend로 변경
kubectl apply -f replicaset-definition-2.yaml

### replicaset 삭제
kubectl delete replicasets.apps replicaset-1

### replicaset 이미지 수정 
kubectl edit replicasets.apps new-replica-set

### replicaset scale up 하기 (replicaset 이름 = new-replica-set )
kubectl scale replicaset --replicas=5 new-replica-set

### replicaset scale down 하기 (replicaset 이름 = new-replica-set )
kubectl scale replicaset --replicas=2 new-replica-set

