### Namespace 갯수 가져오기 
kubectl get ns

### research 라는 이름의 네임스페이스를 가진 pod
kubectl -n research get pods --no-headers

### finance 라는 네임스페이스를 가진 pod 만들기
kubectl run redis --image=redis --dry-run=client -o yaml > pod.yaml
vi pod.yaml 
에디터 열어서
name=redis 
namespace=finance << 추가

## finance 라는 네임스페이스를 가진 pod 정보 가져오기
kubectl -n finance get pod redis

### blue라는 이름의 namespace를 가진 pod
kubectl get pods --all-namespaces | grep blue

### svc = service 의 shortcut(줄임말) 
kubectl -n dev get svc 