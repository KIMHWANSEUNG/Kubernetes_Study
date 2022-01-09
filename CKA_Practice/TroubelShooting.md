kubectl config use-context wk8s

ssh wk8s-node-0

sudo -i

systemctl status kubelet

systemctl restart kubelet

systemctl status kubelet

exit

exit

kubectl get nodes 