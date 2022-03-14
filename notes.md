# Install on Fedora 35
https://nextgentips.com/2021/12/18/how-to-install-and-configure-minikube-on-fedora-35/
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

# commands
- minikube start
Start minikube and kubernetes
- kubectl get pods
Your pods
- kubectl get pods --namespace=kube-system
System pods
- kubectl get nodes
Your nodes
- minikube -p minikube docker-env
Environmental variables
- eval $(minikube -p minikube docker-env)
Configure to use minikube! Everytime you start shell, do it!
- minikube dashboard
Dashboard
- 