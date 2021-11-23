git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git

kubectl create -f .

kubectl get pods 

### It takes a few minutes for the metrics server to start gathering data.
### Run the kubectl top node command and wait for a valid output.
watch kubectl top node 