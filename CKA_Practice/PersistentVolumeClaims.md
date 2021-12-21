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

kubectl get pvc

kubectl run web-server --image=nginx --dry-run=client -o yaml > pod2.yaml

vi po2.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: web-server
  name: web-server
spec:
  containers:
  - image: nginx
    name: web-server
    resources: {}
    volumeMounts
      - mountPath: "/usr/share/nginx/html"
        name: task-pv-storage
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes: 
  -  name: task-pv-storage
     persistentVolumeClaim:
       claimName: pv-volume
status: {}

kubectl edit pv-volume -record

resources:
  requests:
    sotrage: 70Mi
storageClassName: csi-hostpath-sc
