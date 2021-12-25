kubectl config use-context k8s

kubectl create clusterrole deployment-clusterrrole --verb=create --resource=Deployment,Statefulset,Daemonset

kubectl create sa cicd-token -n app-team1

kubectl create clusterrolebinding deployment-clusterrole --clusterrole=deployment-clusterrole --serviceaccount=app-team1:cicd-token
