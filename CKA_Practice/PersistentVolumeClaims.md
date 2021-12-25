kubectl config use-context 0k8s

vi pvc.yaml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-volume
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 10Mi
  storageClassName: csi-hostpath-sc

wq!

kubectl create -f pvc.yaml

kubectl run web-server --image=nginx --dry-run=client -o yaml > pod1.yaml

spec:
  containers:
    - name: web-server
      image: nginx
      volumeMounts:
      - mountPath: "/usr/share/nginx/html"
        name: mypd
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: pv-volume

kubectl create -f pod1.yaml

kubectl edit pv-volume -record
