kubectl config use-contest k8s

kubectl create clusterrole deployment-cluserrole --verb=create --resource=Deployment,Statefulset,Daemonset

kubectl craete sa cicd-token -n app-team1

kubectl create clusterrolebinding deployment-clusterrole --clusterrole=deployment-clusterrole --serviceaccount=appteam-1:cicd-token

kubectl auth can-i create Deployment --as=system:serviceaccount:app-team1:cicd-token