kubectl config use-context k8s

kubectl get nodes

kubectl cordon mk8s-master-0

kubectl drain mk8s-master-0

ssh mk8s-master-0

sudo -i

apt-get update && apt-get install -y kubeadm=1.22.2-00

kubeadm upgrade node

kubeadm upgrade apply

apt-get update && apt-get install -y kubelet=1.22.2-00 kubectl=1.22.2-00

systemctl daemon-reload
systemctl restart kubelet

exit

exit

kubectl uncordon mk8s-master-0

