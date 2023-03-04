# Reddit Clone App on Kubernetes with Ingress
This project demonstrates how to deploy a Reddit clone app on Kubernetes with Ingress and expose it to the world using Minikube as the cluster.

## Prerequisites
Before you begin, you should have the following tools installed on your local machine: 

- Docker
- Minikube cluster ( Running )
- kubectl
- Git



## Installation
Follow these steps to install and run the Reddit clone app on your local machine:

1) Clone this repository to your local machine: `git clone <github repo URL>`
2) Navigate to the project directory: `cd reddit-clone-k8s-ingress`
3) Build the Docker image for the Reddit clone app: `docker build -t reddit-clone-app .`
4) Deploy the app to Kubernetes: `kubectl apply -f deployment.yaml`
5) Deploy the Service for deployment to Kubernetes: `kubectl apply -f service.yaml`
6) Expose the app as a Kubernetes service: `kubectl expose deployment reddit-deployment --type=NodePort --port=5000`


##Deployment.yml file in kubernetes

apiVersion: apps/v1

kind: Deployment

metadata:

name: reddit-clone-deployment
  
  labels:
    
    app: reddit-clone

spec:
  
  replicas: 2
  
  selector:
    
    matchLabels:
      
      app: reddit-clone
  
  template:
    
    metadata:
      
      labels:
        
        app: reddit-clone
    
    spec:
      
      containers:
      
      - name: reddit-clone
        
        image: sunnyb636/reddit-clone
        
        ports:
        
        - containerPort: 3000



##service.yml file in kubernetes:


apiVersion: v1

kind: Service

metadata:
  
  name: reddit-clone-service
  
  labels:
    
    app: reddit-clone

spec:
  
  type: NodePort
  
  ports:
  
  - port: 3000
    
    targetPort: 3000
    
    nodePort: 31000
  
  selector:
    
    app: reddit-clone




## Contributing
If you'd like to contribute to this project, please open an issue or submit a pull request.


