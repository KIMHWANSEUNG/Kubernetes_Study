### We have a working kubernetes cluster with a set of applications running. Let us first explore the setup.
kubectl get deployments.apps 

### What is the version of ETCD running on the cluster?
kubectl get pods -n kube-system
kubectl -n kube-system describe pod etcd-controlplane

### At what address can you reach the ETCD cluster from the controlplane node?
### Check the ETCD Service configuration in the ETCD POD
kubectl -n kube-system describe pod etcd-controlplane
 --listen-client-urls=https://127.0.0.1:2379
 (여기에 있는 URL)

### Where is the ETCD server certificate file located?
### Note this path down as you will need to use it later
kubectl -n kube-system describe pod etcd-controlplane
--cert-file=/etc/kubernetes/pki/etcd/server.crt
(여기에 있는 경로)

### Where is the ETCD CA Certificate file located?
kubectl -n kube-system describe pod etcd-controlplane
--trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
(여기에 있는 경로)

### The master nodes in our cluster are planned for a regular maintenance reboot tonight. While we do not anticipate anything to go wrong, we are required to take the necessary backups. Take a snapshot of the ETCD database using the built-in snapshot functionality.
### Store the backup file at location /opt/snapshot-pre-boot.db
### Backup ETCD to /opt/snapshot-pre-boot.db
 ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db

### Wake up! We have a conference call! After the reboot the master nodes came back online, but none of our applications are accessible. Check the status of the applications on the cluster. What's wrong?
kubectl get deployments.apps,svc

### Luckily we took a backup. Restore the original state of the cluster using the backup file.
ETCDCTL_API=3 etcdctl  --data-dir /var/lib/etcd-from-backup \
snapshot restore /opt/snapshot-pre-boot.db

 vi /etc/kubernetes/manifests/etcd.yaml

   volumes:
  - hostPath:
      path: /var/lib/etcd-from-backup
      type: DirectoryOrCreate
    name: etcd-data
docker ps | grep etcd
