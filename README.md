# This project is about how to setup Kubernets with minikube and docker containers

## You can run the docker-compose as well to start without Kubernetes cluster

### How to start for Kubernetes

Kindly follow this link https://kubernetes.io/docs/tasks/tools/install-kubectl/

### how to run

first build all container and images 

`docker-compose up --build -d`

`eval $(minikube docker-env)`

`docker build -f ./services/web/Dockerfile -t hello_flask:latest ./services/web`

can test with 

`docker run -p 5001:5000 \                           
    -e "FLASK_APP=project/__init__.py" -e "FLASK_ENV=development" \
    hello_flask gunicorn --bind 0.0.0.0:5000 manage:app`

### create Kubernets secrets with kubectl

already in this repo secrets.yml

### create Kubernetes persistence volumes

already in this repo persistent-volume.yml

### create Kubernetes deployment for both pgsql and web/flask

already in this repo pgsql-deployment.yml and webservice-deployment.yml

### run minikube and call other files, here deployment and service together in one yml file for each service

`minikube start`
`minikube dashboard`

`kubectl apply -f secrets.yml`
`kubectl apply -f persistent-volume.yml`
`kubectl apply -f pgsql-deployment.yml`
`kubectl apply -f webservice-deployment.yml`

Now check minikube dashboard





