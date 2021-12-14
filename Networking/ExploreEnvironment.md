

ip a | grep -B2 10.1.92.3  (IP는 마스터 노드의 INTERNAL IP)

### What is the MAC address of the interface on the master node?
ip link show eth0

### What is the IP address assigned to node01?
kubectl get node -o wide

### What is the MAC address assigned to node01?
arp node01

