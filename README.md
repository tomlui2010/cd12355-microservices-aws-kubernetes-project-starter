# Coworking Space Service Extension
The Coworking Space Service is a set of APIs that enables users to request one-time tokens and administrators to authorize access to a coworking space. This service follows a microservice pattern and the APIs are split into distinct services that can be deployed and managed independently of one another.


## Getting Started

### Overview
Application is containerized using Docker and deployed to a Kubernetes cluster managed by Amazon EKS (Elastic Kubernetes Service).

### Key Technologies
- Docker: Containerization tool that packages the application and its dependencies into a container image.
- Kubernetes: Orchestrates the deployment, scaling, and management of containerized applications.
- Amazon EKS: Managed Kubernetes service by AWS, used to deploy and manage the Kubernetes clusters.
- AWS CodeBuild: A CI/CD service that builds and tests the Docker image.
- AWS ECR: Amazon Elastic Container Registry, where Docker images are stored.
- AWS CloudWatch - monitor activity and logs in EKS
- GitHub - pull and clone code

### Deployment Process
#### 1. Build and Push Docker Image
The first step in the deployment process is to build a Docker image of the application and push it to AWS ECR.

Dockerfile: The Dockerfile defines the environment and the steps needed to set up the application. It installs necessary dependencies, sets up a virtual environment, and configures the Flask app to run on port 5153.

AWS CodeBuild: A build project is configured in AWS CodeBuild to automate the build process (refer buildspec.yml at the root folder). It uses the docker build command to create the image and then pushes it to an ECR repository.

#### 2. Deployment to Kubernetes
Once the Docker image is built and pushed, application is deployed to a Kubernetes cluster using Kubernets Deployment files.

Kubernetes Manifests: These are YAML files that describe the desired state of the application in the Kubernetes cluster. 

##### Sequence of deployment: 
- kubectl apply -f deployment/configmap.yaml
- kubectl apply -f deployment/pv.yaml
- kubectl apply -f deployment/pvc.yaml
- kubectl apply -f deployment/postgresql-deployment.yaml
- kubectl apply -f deployment/postgresql-service.yaml
- kubectl apply -f deployment/coworking.yaml

#### 3. Monitoring and Logs
Kubernetes Dashboard: Use the Kubernetes dashboard or kubectl commands to monitor the state of the deployment.
CloudWatch Logs: Logs from the application can be monitored in Amazon CloudWatch if the logging driver is configured to send logs to AWS.
 
