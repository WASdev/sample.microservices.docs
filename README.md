# About the sample application

This microservice sample application is a modified fork of the [Microprofile Showcase Application](https://github.com/eclipse/microprofile-conference). Like its parent it's a web application for managing a conference and is based on a number of discrete microservices. The front end is written in Angular; the backing microservices are in Java. All run on WebSphere Liberty, in Docker containers managed by Kubernetes. The sample application demonstrates various features:
- Microservices running as WebSphere Liberty Docker containers on Kubernetes
- ELK log stack integration
- Inbound HTTPS out-of-the-box

## Ways to use the sample application

The sample application can be used with or without a [Jenkins](https://jenkins.io/)-based deployment pipeline. It can be run on IBM Cloud Private, or on [minikube](https://github.com/kubernetes/minikube). Both of these are distributions of [Kubernetes](https://kubernetes.io/). Developers may wish to start testing the application by deploying its component microservices directly to minikube. Demonstrators might prefer to start with a Jenkins-based approach, deploying either to minikube or IBM Cloud Private.

The main installation steps are:

1. Install prerequisite tools
1. Install Kubernetes (minikube or IBM Cloud Private)
1. Install the sample application

The exact steps to be taken vary based on which Kubernetes you will be using. Here we will cover [direct deployment to minikube without Jenkins](dev_test_local_minikube.md).
