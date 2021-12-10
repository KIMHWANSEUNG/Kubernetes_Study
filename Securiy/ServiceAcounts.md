### How many Service Accounts exist in the default namespace?
kubectl get serviceaccounts

### What is the secret token used by the default service account?
kubectl describe serviceaccount default

### We just deployed the Dashboard application. Inspect the deployment. What is the image used by the deployment?
kubectl describe deployment

### Inspect the Dashboard Application POD and identify the Service Account mounted on it.
kubectl describe pod

### At what location is the ServiceAccount credentials available within the pod?
kubectl describe pod

### The application needs a ServiceAccount with the Right permissions to be created to authenticate to Kubernetes. The 'default' ServiceAccount has limited access. Create a new ServiceAccount named 'dashboard-sa'.
kubectl create serviceaccount dashboard-sa