kubectl config user-context ek8s

kubectl get nodes -o wide

kubectl cordon ek8s-node-1

kubectl drain ek8s-node-1 --ignore-daemonsets

