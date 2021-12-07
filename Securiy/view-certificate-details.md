### Identify the certificate file used for the kube-api server
cat /etc/kubernetes/manifests/kube-apiserver.yaml
 --tls-cert-file(여기 URL을 살펴보자)

 ### Identify the Certificate file used to authenticate kube-apiserver as a client to ETCD Server
cat /etc/kubernetes/manifests/kube-apiserver.yaml
 etcd-certfile (여기 URL을 살펴보자)

### Identify the key used to authenticate kubeapi-server to the kubelet server
cat /etc/kubernetes/manifests/kube-apiserver.yaml
 kubelet-client-key (여기 URL을 살펴보자)

### Identify the ETCD Server Certificate used to host ETCD server
cat /etc/kubernetes/manifests/kube-apiserver.yaml
cert-file(여기 URL을 살펴보자)

### Identify the ETCD Server CA Root Certificate used to serve ETCD Server
### ETCD can have its own CA. So this may be a different CA certificate than the one used by kube-api server.
cat /etc/kubernetes/manifests/etcd.yaml 
trusted=ca=file(여기 URL을 살펴보자)

### What is the Common Name (CN) configured on the Kube API Server Certificate?
### OpenSSL Syntax: openssl x509 -in file-path.crt -text -noout
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text
Subject CN(여기 URL)

### What is the name of the CA who issued the Kube API Server Certificate?
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text
Issuer(여기 URL)

### Which of the below alternate names is not configured on the Kube API Server Certificate?
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text
Alternative Names(여기 URL)

### What is the Common Name (CN) configured on the ETCD Server certificate?
openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text
Subject CN(여기 URL)

### How long, from the issued date, is the Root CA Certificate valid for?
openssl x509 -in /etc/kubernetes/pki/ca.crt -text
validity 
