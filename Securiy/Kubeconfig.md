### Where is the default kubeconfig file located in the current environment?
### Find the current home directory by looking at the HOME environment variable.
/root/.kube/config

### How many clusters are defined in the default kubeconfig file?
kubectl config view 

### How many Users are defined in the default kubeconfig file?
kubectl config view 


### How many contexts are defined in the default kubeconfig file?
kubectl config view 

...전부 비슷한 문제

### A new kubeconfig file named my-kube-config is created. It is placed in the /root directory. How many clusters are defined in that kubeconfig file?
kubectl config view --kubeconfig my-kube-config

### What user is configured in the research context?
kubectl config view --kubeconfig my-kube-config

### What is the name of the client-certificate file configured for the aws-user?
kubectl config view --kubeconfig my-kube-config

### What is the current context set to in the my-kube-config file?
kubectl config current-context --kubeconfig my-kube-config


### would like to use the dev-user to access test-cluster-1. Set the current context to the right one so I can do that.
### Once the right context is identified, use the kubectl config use-context command.
### Current context set
kubectl config --kubeconfig=/root/my-kube-config use-context research
kubectl config --kubeconfig=/root/my-kube-config current-context


### We don't want to have to specify the kubeconfig file option on each command. Make the my-kube-config file the default kubeconfig.