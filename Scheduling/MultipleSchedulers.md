### What is the name of the POD that deploys the default kubernetes scheduler in this environment?
kubectl -n kube-system get pods 

### What is the image used to deploy the kubernetes scheduler?
### Inspect the kubernetes scheduler pod and identify the image
kubectl -n kube-system describe pod kube-scheduler-controlplane | grep -i image

### Deploy an additional scheduler to the cluster following the given specification.
### (Use the manifest file used by kubeadm tool. Use a different port than the one used by the current one.)
### Namespace: kube-system
### Name: my-scheduler
### Status: Running
### Custom Scheduler Name
cd /etc/kubernetes/manifests 
cp kube-scheduler.yaml /root/my-scheduler.yaml
vi my-scheduler.yaml

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    component: kube-scheduler
    tier: control-plane
  name: my-scheduler
  namespace: kube-system
spec:
  containers:
  - command:
    - kube-scheduler
    - --authentication-kubeconfig=/etc/kubernetes/scheduler.conf
    - --authorization-kubeconfig=/etc/kubernetes/scheduler.conf
    - --bind-address=127.0.0.1
    - --kubeconfig=/etc/kubernetes/scheduler.conf
    - --leader-elect=false
    - --scheduler-name=my-scheduler
    image: k8s.gcr.io/kube-scheduler:v1.20.0
    imagePullPolicy: IfNotPresent
    livenessProbe:
      failureThreshold: 8
      httpGet:
        host: 127.0.0.1
        path: /healthz
        port: 10259
        scheme: HTTPS
      initialDelaySeconds: 10
      periodSeconds: 10
      timeoutSeconds: 15
    name: my-scheduler
    resources:
      requests:
        cpu: 100m
    startupProbe:
      failureThreshold: 24
      httpGet:
        host: 127.0.0.1
        path: /healthz
        port: 10259
        scheme: HTTPS
      initialDelaySeconds: 10
      periodSeconds: 10
      timeoutSeconds: 15
    volumeMounts:
    - mountPath: /etc/kubernetes/scheduler.conf
      name: kubeconfig
      readOnly: true
  hostNetwork: true
  priorityClassName: system-node-critical
  volumes:
  - hostPath:
      path: /etc/kubernetes/scheduler.conf
      type: FileOrCreate
    name: kubeconfig
status: {}
(이렇게 수정하고)
kubectl create -f my-scheduler.yaml


### A POD definition file is given. Use it to create a POD with the new custom scheduler.
### File is located at /root/nginx-pod.yaml
### Name: nginx
### Uses custom scheduler
### Status: Running
vi nginx.yaml

spec:
  schedulerName: nmy-scheduler

kubectl create -f nginx.yaml 