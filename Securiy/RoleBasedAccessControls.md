### Inspect the environment and identify the authorization modes configured on the cluster.
### Check the kube-apiserver settings.
kubectl describe pod kube-apiserver-controlplane -n kube-system
--authorization-mode(여기 참고)

### How many roles exist in the default namespace?
kubectl get roles

### How many roles exist in all namespaces together?
kubectl get roles --all-namespaces

### What are the resources the kube-proxy role in the kube-system namespace is given access to?
kubectl describe role kube-proxy -n kube-system

### What actions can the kube-proxy role perform on configmaps?
kubectl describe role -n kube-system kube-proxy

### Which account is the kube-proxy role assigned to it?
kubectl describe rolebinding kube-proxy -n kube-system

### Which account is the kube-proxy role assigned to it?
kubectl describe rolebinding kube-proxy -n kube-system

### A user dev-user is created. User's details have been added to the kubeconfig file. Inspect the permissions granted to the user. Check if the user can list pods in the default namespace.
### use the --as dev-user option with kubectl to run commands as the dev-user.
kubectl describe rolebinding kube-proxy -n kube-system

### Create the necessary roles and role bindings required for the dev-user to create, list and delete pods in the default namespace.
### Use the given spec:
kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods
kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user

### The dev-user is trying to get details about the dark-blue-app pod in the blue namespace. Investigate and fix the issue.
### We have created the required roles and rolebindings, but something seems to be wrong.
kubectl edit role developer -n blue
resourceNames: dark-blue-app (이렇게 수정)

### Grant the dev-user permissions to create deployments in the blue namespace.
### Remember to add both groups "apps" and "extensions".

vi blue.yaml

---
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: blue
  name: deploy-role
rules:
- apiGroups: ["apps", "extensions"]
  resources: ["deployments"]
  verbs: ["create"]

---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: dev-user-deploy-binding
  namespace: blue
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: deploy-role
  apiGroup: rbac.authorization.k8s.io
  

kubectl create -f blue.yaml