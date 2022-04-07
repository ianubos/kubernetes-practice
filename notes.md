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
- kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.10
- kubectl get deployments
- kubectl expose deployment hello-minikube --type=NodePort --port=8080
- kubectl get services -o wide
- kubectl delete services hello-minikube
- kubectl delete deployments hello-minikube

### Kubectl API
- cd recipe-api
- eval $(minikube -p minikube docker-env)
- docker build -t recipe-api:v1 .
- kubectl apply -f recipe-api/recipe-api-deployment.yml
- kubectl apply -f recipe-api/recipe-api-network.yml


### Service Discovery
- minikube addons enable ingress
- kubectl get pods --namespace kube-system | grep ingress

- eval $(minikube -p minikube docker-env)
- docker build -t web-api:v1 .
- kubectl apply -f web-api-deployment.yml
- kubectl apply -f web-api-network.yml  
networking.k8s.io/v1 is correct version.  See this artice
https://docs.konghq.com/kubernetes-ingress-controller/1.3.x/concepts/ingress-versions/  
- kubectl get ingress web-api-ingress # Request via ingress
- curl -H "Host: example.org" http://<INGRESS_IP>/

### Modifying Deployments
- kubectl scale deployment.apps/recipe-api --replicas=10
- kubectl get pods -l app=recipe-api
- kubectl apply -f recipe-api/recipe-api-deployment.yml # Back down to 5

- echo "server.get('/hello', async () => 'Hello');" >> consumer-http-basic.js
- docker build -t web-api:v2 .
- nano web-api-deployment.yml
- kubectl apply -f web-api-deployment.yml
- kubectl get pods -w -l app=web-api
- curl `minikube service web-api-service --url`/hello
- kubectl get rs -l app=web-api

- echo "server.get('/kill', async () => { process.exit(42); });" >> consumer-http-basic.js
- docker build -t web-api:v3 .
- nano web-api-deployment.yml
- kubectl apply -f web-api-deployment.yml --record=true
- curl `minikube service web-api-service --url`/kill
- kubectl get pods -l app=web-api
- kubectl rollout history deployment.v1.apps/web-api
- kubectl rollout undo deployment.v1.apps/web-api --to-revision=<RELEASE_NUMBER>

### Delete all of them
- kubectl delete services recipe-api-service
- kubectl delete services web-api-service
- kubectl delete deployment recipe-api
- kubectl delete deployment web-api
- kubectl delete ingress web-api-ingress
- minikube stop
- minikube delete
