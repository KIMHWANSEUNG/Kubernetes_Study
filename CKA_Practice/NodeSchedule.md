k get nodes
kubectl cordon ek8s-node01
k drain ek8s-node-01 --ignore-daemonsets
k get nodes

### Label 제시어가 나왔을 경우 (Node Name 없음)
k get nodes -l name=label


