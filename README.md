# Udagram
This cloud web application allows user registration, post pictures for registered users  and everyone to view pictures.

## About the Project 
Project utilizes microservice containerized architecture that can be deployed and managed in Kubernetes

## Components/Services

1. Frontend
- Web based user interface that allows users to view existing pictures, register, login and to post pictures
- Developed in node.js, typescript, Ionic web framework

2. Reverseproxy
- Nginx orchestrating backend services running on different containers

2. User
- User registration and login RestAPI microservice
- Developed in node.js, express, typescript, sequalize, AWS Postgress for user meta data

4. Feed

- Post pictures, retrieve pictures RestAPI microservice
- Developed in node.js, express, typescript, sequalize, AWS Postgress for image meta data and S3 bucket to store images

## Build & Deployment

* Travis CI/CD to build images


            * [Travis Link](https://travis-ci.com/github/Kannankani)

            * Docker YAML files are in [link](https://github.com/Kannankani/cloud-ms-with-k8/tree/master/01-deployment/docker)


* Kubernetes 

    * Entire project can be delpoyed in Kubernetes to manage the Docker containers and to perform rolling updates.

    * Configuration Files: [link](https://github.com/Kannankani/cloud-ms-with-k8/tree/master/01-deployment/k8s)


## Deployment Steps
1. Create K8 cluster using MiniKube
2. Apply secret files: aws-secret.yaml, env-secret.yaml, env-configmap.yaml. 
    *Note: These files are ingored in the repository*
    `kubectl apply -f ./aws-secret.yaml`
    `kubectl apply -f ./env-secret.yaml`
    `kubectl apply -f ./env-configmap.yaml`
    
3. Deploy deployment sets and services

    `kubectl apply -f backend-feed-deployment.yaml` 
    `kubectl apply -f backend-feed-service.yaml`
    
    `kubectl apply -f backend-user-deployment.yaml`
    `kubectl apply -f backend-user-service.yaml`

    `kubectl apply -f frontend-deployment.yaml `
    `kubectl apply -f frontend-service.yaml`

    `kubectl apply -f reverseproxy-deployment.yaml`
    `kubectl apply -f reverseproxy-service.yaml`

4. Portford 8100 will expose UI and 8080 will connect fronend to backend services.

5. Deployment and Services can be stopped using 
    `kubectl delete deployment <name>`
    `kubectl delete service <name>`
