
sudo -i

ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/opt/KUIN00601/ca.crt --cert=/opt/KUIN00601/etcd-client.crt--key=/opt/KUIN00601/etcd-client.key\
  snapshot save /var/lib/backup/etcd-snapshot.db

  ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/opt/KUIN00601/ca.crt --cert=/opt/KUIN00601/etcd-client.crt--key=/opt/KUIN00601/etcd-client.key\
  snapshot restore /data/backup/etcd-snapshot-previous.db

  exit