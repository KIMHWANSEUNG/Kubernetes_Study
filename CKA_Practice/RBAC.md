### RBAC 

kubectl create clusterrole deployment-clusterrole —verb=create —resource=Deployment,Statefulset,Daemonset -n app-team1

kubectl create sa cicd-token -n app-team1

kubectl create clusterrolebinding deployment-clusterrole —clusterrole=deployment-clusterrole —serviceaccount=app-team1:cicd-token

kubectl auth can-i create Deployment --as=system:serviceaccount:app-team1:cicd-token

kubectl auth can-i create Statefulset --as=system:serviceaccount:app-team1:cicd-token

kubectl auth can-i create Daemonset --as=system:serviceaccount:app-team1:cicd-token