### A pod called rabbit is deployed. Identify the CPU requirements set on the Pod
### in the current(default) namespace
kubectl get pods 
kubectl describe pod rabbit

해당부분 확인
   Requests:
      cpu:        1

### Delete the rabbit Pod.
kubectl delete pod rabbit


### Another pod called elephant has been deployed in the default namespace. It fails to get to a running state.
### Inspect this pod and identify the Reason why it is not running.
kubectl get pods
kubectl describe pods elephant 
확인
    State:          Waiting
      Reason:       CrashLoopBackOff
    Last State:     Terminated
      Reason:       OOMKilled
      Exit Code:    1
      Started:      Tue, 16 Nov 2021 07:53:40 +0000
      Finished:     Tue, 16 Nov 2021 07:53:40 +0000
Last State에서 이유 발견(OOMKilled)

### The status OOMKilled indicates that it is failing because the pod ran out of memory. Identify the memory limit set on the POD.
kubectl get pods
kubectl describe pod elephant

### The elephant pod runs a process that consume 15Mi of memory. Increase the limit of the elephant pod to 20Mi.
### Pod Name: elephant
### Image Name: polinux/stress
### Memory Limit: 20Mi
kubectl get pod elephant -o yaml > pod.yaml
vi pod.yaml
파일 열어서 수정
    resources:
      limits:
        memory: 10mi >> 20mi 로수정
kubectl delete pod elephant
kubeclt apply -f pod.yaml

### delete thd pod 
kubectl delete pod elephant
