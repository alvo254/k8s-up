# k8s-up
## Best practice
 - It is better to create pods declarative i.e with config files than imperative with kubectl command
## You can ssh into you minikube node by
    - get minikube ip with minikube ip
    - ssh docker@<minikube ip> : password=tcuser
    - or use minikube ssh if driver=docker 

# I dockerized one of my react projects
 - Link for project: https://github.com/alvo254/fitness-hero-V2.git
 - Docker image: docker pull alvin254/k8s-up
 - docker run -p 3000:3000 alvin254/k8s-up

So far everything i am doing is using the kubectl to create deployments and services

## Updating deployment and rolling back to previous deployment
 - kubectl set image deployment <deploymnent-name> <deployment-pod "same as deployment-name">=<image-to-replace-deployment>
 - kubectl set image deployment nginx-app nginx-app=nginx:1.16.4

If you want more details about a particular revisio ass to --revision flag
 - kubectl rollout history deployment fitness --revision=2

To select a version you want to role back to 
 - kubectl rollout undo deployment fitness --to-revision=3

To role back to the lets call it latest tag which is pulled by default if you dont specify the image tag
 - kubectl rollout undo deployment fitness


## Create deployment
kubectl create deployment <name-of-deployment> --image=<image> 
kubectl create deployment fitness --image=alvin254/k8s-up


## Create service
kubectl expose deployment <name-of-deployment> --type=<type-of-service> --port=<port-to-expose>
kubectl expose deployment fitness --type=NodePort --port=3000

## To see service 
You can use minikube service <service-name>
    - minikube service fitness
    or
    - kubectl get svc

# Strategy to rollout updates
 - There are 2 strategies to supported by deployment 
    - Recreate
    - RollingUpdate

 - kubectl rollout history deployment fitness
 - kubectl rollout status deployment fitness

## Namespaces
 - kubectl get deployment -n default or kubectl get deployment --namespace=dev
 - kubectl apply -f <service.yaml> --namespace=<name-of-namespace>

This can also be done by specifying the namespace in the configuration file metadata
NB: You can use a tool called kubens to chose the default namespace to work with instead of back and forth 
 - kubens :- this will display the current namespace
 - kubens dev :- this will make dev the default namespaces without providing the --namespace option
 
 
## Isolavent
