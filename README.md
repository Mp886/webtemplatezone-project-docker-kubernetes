## Web Application Deployment with Kubernetes

- This repository contains the necessary files to deploy a simple web application using Kubernetes on Minikube. The application includes static HTML and CSS files, and the deployment is configured with Kubernetes manifests for Deployment, Service, and Ingress.

## Repository Structure
- Dockerfile: Dockerfile for building the Docker image.
- index.html: Main landing page of the web application.
- about.html: About page.
- contact.html: Contact page.
- styles.css: CSS file for styling the web application.
- deployment.yaml: Kubernetes Deployment manifest.
- service.yaml: Kubernetes Service manifest.
- ingress.yaml: Kubernetes Ingress manifest.

## Prerequisites
- Minikube: A local Kubernetes environment.
- kubectl: The Kubernetes command-line tool.
- Docker: Required for building and managing Docker images.

## Setup Instructions

1. Clone the Repository

- git clone https://github.com/yourusername/your-repository-name.git
cd your-repository-name

2. Build the Docker Image

- Navigate to the directory containing the Dockerfile and build the Docker image:

docker build -t beast106/webtemplatezone:latest .

3. Run the Docker Image to the container

- Use the below command to run the container from the image

docker run -it -d -p 8080:80 beast106/webtemplatezone:latest

4. Push the Docker Image to Docker Hub

- Ensure you are logged into Docker Hub:

 docker login

- Push the image to the registry(Docker Hub)

 docker push beast106/webtemplatezone:latest

5. Start Minikube

- Start Minikube with the necessary configurations:

 minikube start

6. Apply Kubernetes Manifests

- Apply the Kubernetes Deployment, Service, and Ingress configurations:

 kubectl apply -f deployment.yaml
 kubectl apply -f service.yaml
 kubectl apply -f ingress.yaml

7. Enable Ingress Controller

- Note: The Ingress resource will not work without an Ingress controller. Enable the Ingress controller in Minikube:

  minikube addons enable ingress

8. Verify the Deployment

- Check the status of the pods, service, and Ingress:

  kubectl get pods
  kubectl get services
  kubectl get ingress

9. Access the Web Application

- Local Access: To test locally, you may need to configure your /etc/hosts file or use Minikube’s IP and port. For example:

  minikube ip

- Add the following line to your /etc/hosts file:
  <minikube-ip> foo.bar.com

- Then access your application at http://foo.bar.com/bar.

- You can also check it in the terminal itself with the command : curl -L http://foo.bar.com/bar .

## Notes

- Ensure that the Docker image "your-docker-username/your-docker-image-name:tagname" is correctly built and available on Docker Hub.

- The Ingress resource routes traffic based on the host and path specified. Make sure your DNS or /etc/hosts configuration matches the Ingress rules.

- Ingress controllers must be enabled for the Ingress resource to function. Use the provided command to enable it in Minikube.

## Troubleshooting

- If pods are not running correctly or you see ImagePullBackOff errors, check the image URL and ensure it is correctly pushed to Docker Hub.

- Verify network connectivity and DNS resolution within Minikube if there are issues pulling images.
