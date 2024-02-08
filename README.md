#4 - Minikube and kubectl - Local Kubernetes Cluster

Installing minikube https://minikube.sigs.k8s.io/docs/start/

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

Starting minikube and checking for the status

    minikube start -driver docker

    minikube status

List kubectl components

    kubectl get pods
    kubectl get services
    kubectl get nodes
    ...

Creating an example deployment and checking its state

    kubectl create deployment nginx-depl --image=nginx
    kubectl get deployments #lists 0/1 READY, the deployment is not ready yet
    # did not work, because kubectl was not able to pull the image due to company proxy

Use proxy for starting minikube (https://minikube.sigs.k8s.io/docs/handbook/vpn_and_proxy/)

    export HTTP_PROXY=http://http-proxy.krones-deu.krones-group.com:3128
    export HTTPS_PROXY=http://http-proxy.krones-deu.krones-group.com:3128
    export NO_PROXY=localhost,127.0.0.1,10.96.0.0/12,192.168.59.0/24,192.168.49.0/24,192.168.39.0/24
    minikube start


    kubectl describe pod <podname>
    kubectl logs <podname>

    kubectl create deployment mongo-deployment --image=mongo
    # did not work at first, deleted the deployment and recreated it, then it worked
    kubectl delete deplyoment mongo-deployment

Connect into a pod

    kubectl exec -it mongo-deployment-64d449895-l9x8j -- bin/bash
    # QUESTION: how does that work with a deployment that is replicated multiple times? in which container am i connecting?

Apply a new file

    kubectl apply -f nginx-deployment.yaml

# 6 YAML Configuration File

    kubectl apply -f nginx-deployment.yaml
    kubectl apply -f nginx-service.yaml

    kubectl get services

Output with more information like IP address

    kubectl get pods -o wide

# 7 

Create base64 password in bash for usage in secrets.
This is still not secure and not encrypted!

    echo -n 'password' | base64

Prepared all the deployments, services, secret and configmap
When the application should be exposed and opened in the browser I had massive problems getting it to run.
On Linux (at least with the minikube docker driver) there was no automatic created tunnel from localhost to the cluster. This resulted in having to find the solution online.

Solution: Forward the port for the pod (mongo express)

    kubectl port-forward <podname> <localhostport>:<containerport>

I had an error in one of the service definitions, but it was really just coincidence that I found this typo.