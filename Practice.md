kubectl config use-context k8s

kubectl cordon mk8s-matser-0

kubectl drain mk8s-master-0 --ignore-daemonsets

ssh mk8s-master-0

sudo -i

apt-get update && apt-get install -y kubeadm=1.22.2-00

kubeadm upgrade apply v1.22.2

apt-get update && apt-get install -y kubelet=1.22.2-00 kubectl=1.22.2-00ㅇ