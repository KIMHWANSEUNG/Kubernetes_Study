### A user - USER5 - has expressed concerns accessing the application. Identify the cause of the issue.
### Inspect the logs of the POD
kubectl get pods
kubectl logs webapp-1 


### A user is reporting issues while trying to purchase an item. Identify the user and the cause of the issue.
### Inspect the logs of the webapp in the POD
kubectl logs webapp-2 -c simple-webapp