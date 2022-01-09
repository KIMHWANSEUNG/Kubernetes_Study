kubectl config use-context ok8s

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

kubectl create -f pvc.yaml

kubectl get pvc

vi pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: web-server
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - mountPath: "/usr/share/nginx/html"
        name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
        claimName: pv-volume

kubectl create -f pod.yaml

kubectl edit pvc pv-volume -record

storage: 70Mi

wq!

