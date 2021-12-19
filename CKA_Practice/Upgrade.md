k get node
k cordon mk8s-master-0
k drain mk8s-master-0

ssh mk8s-master-0
sudo -i

apt update
apt-get update && apt-get install -y kubeadm= 1.22.2-00

kubeadm upgrade apply v1.22.2

apt-get update && apt-get install -y kubelet=1.22.2-00 kubectl=1.22.2-00

systemctl daemon-reload
systemctl restart kubelet
exit

k uncordon mk8s-master-0

k get nodes

