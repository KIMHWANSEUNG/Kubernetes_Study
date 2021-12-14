### Let's fix that. Create a new PersistentVolumeClaim by the name of local-pvc that should bind to the volume local-pv.
### Inspect the pv local-pv for the specs.
### PVC: local-pvc
### Correct Access Mode?
### Correct StorageClass Used?
### PVC requests volume size = 500Mi?
vi pvc.yaml

kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: local-pvc
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: local-storage
  resources:
    requests:
      storage: 500Mi

kubectl create -f pvc.yaml

kubectl get pvc local-pvc

### Why is the PVC in a pending state despite making a valid request to claim the volume called local-pv?
kubectl describe pvc local-pvc


### Create a new pod called nginx with the image nginx:alpine. The Pod should make use of the PVC local-pvc and mount the volume at the path /var/www/html.
### The PV local-pv should in a bound state.
### Pod created with the correct Image?
### Pod uses PVC called local-pvc?
### local-pv bound?
### nginx pod running?
### Volume mounted at the correct path?

vi pvc1.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    volumeMounts:
    - name: local-persistent-storage
      mountPath: /var/www/html
  volumes:
    - name: local-persistent-storage
      persistentVolumeClaim:
        claimName: local-pvc

kubectl create -f pvc1.yaml

kubectl get pvc


### Create a new Storage Class called delayed-volume-sc that makes use of the below specs:
### provisioner: kubernetes.io/no-provisioner
### volumeBindingMode: WaitForFirstConsume

---
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: delayed-volume-sc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer