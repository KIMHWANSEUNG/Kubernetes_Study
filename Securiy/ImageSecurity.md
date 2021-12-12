### What is the secret type we choose for the docker registry?
kubectl create secret --help

### Create a secret object with the credentials required to access the registry.
### Name: private-reg-cred
### Username: dock_user
### Password: dock_password
### Server: myprivateregistry.com:5000
### Email: dock_user@myprivateregistry.com
kubectl create secret docker-registry private-reg-cred --docker-username=dock_user --docker-password=dock_password --docker-server=myprivateregistry.com:5000 --docker-email=dock_user@myprivateregistry.com