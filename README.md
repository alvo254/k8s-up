# k8s-up
## You can ssh into you minikube node by
    - get minikube ip with minikube ip
    - ssh docker@<minikube ip> : password=tcuser
    - or use minikube ssh if driver=docker 

# I dockerized one of my react projects
 - Link for project: https://github.com/alvo254/fitness-hero-V2.git
 - Docker image: docker pull alvin254/k8s-up
 - docker run -p 3000:3000 alvin254/k8s-up
