### How many secrets exist on the system?
kubectl get secrets

### How many secrets are defined in the default-token secret?
kubectl describe secrets default-token-wtdn2

(data 섹션아래에 3개의 항목이 있기 때문에 답은 3개 )

### what is type of scret?
kubectl describe secrets default-token-wtdn2


### Which of the following is not a secret data defined in default-token secret?
kubectl describe secrets default-token-wtdn2


### The reason the application is failed is because we have not created the secrets yet. Create a new secret named db-secret with the data given below.
### Secret Name: db-secret
### Secret 1: DB_Host=sql01
### Secret 2: DB_User=root
### Secret 3: DB_Password=password123
kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123


### Configure webapp-pod to load environment variables from the newly created secret.
### Pod name: webapp-pod
### Image name: kodekloud/simple-webapp-mysql
### Env From: Secret=db-secret
kubectl get pods
kubectl get pod webapp-pod -o yaml > pod.yaml

vi pod.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2021-12-02T07:35:04Z"
  labels:
    name: webapp-pod
  name: webapp-pod
  namespace: default
spec:
  containers:
  - image: kodekloud/simple-webapp-mysql
    imagePullPolicy: Always
    name: webapp
(이렇게 수정함)
wq! 
kubectl explain pods --recursive | grep -A8 envFrom
(envFrom 형태 복사)

vi.pod.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2021-12-02T07:35:04Z"
  labels:
    name: webapp-pod
  name: webapp-pod
  namespace: default
spec:
  containers:
  - image: kodekloud/simple-webapp-mysql
    imagePullPolicy: Always
    name: webapp
    envFrom:
    - secretRef:
        name: db-secret
(이렇게 수정)

wq!

kubectl apply -f pod.yaml



