# Deploy a python app at scale with Kubernetes
In this project, we will be using Minikube (a local installation of Kubernetes) to deploy a Python app at scale.

## Steps
- Fork this git (as usual) and cd into the git directory
- Build the docker image of the application  
```docker build  -t flask-k8s .```
- (if not already started,) start minikube  
```minikube start```
- Push the docker image to your minikube repository   
```minikube image load flask-k8s```
- Enable minikube ingress addon  
``` minikube addons enable ingress```
- Deploy the k8s deployment and service  
```kubectl apply -f k8s/deployment.yml```
- Deploy the k8s ingress resource  
```kubectl apply -f k8s/ingress.yml```
- Port-forward the service on any port you want (in our case, port 8001)  
```kubectl port-forward services/flask-app-service 8001:80```
- Visit `http://localhost:8001/` to see your app work

You can scale the deployment (to 10 pods, for example) by running `kubectl scale deployment flask-k8s-app --replicas=10`

## Cleanup
To cleanup, run  
`kubectl delete -f k8s/ingress.yml`  
`kubectl delete -f k8s/deployment.yml`  
`minikube image rm flask-k8s`

