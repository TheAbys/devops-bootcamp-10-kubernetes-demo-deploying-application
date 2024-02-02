#4 - Minikube and kubectl - Local Kubernetes Cluster

Installing minikube https://minikube.sigs.k8s.io/docs/start/

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

Starting minikube and checking for the status

    minikube start -driver docker

    minikube status