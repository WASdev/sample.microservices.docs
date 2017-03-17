# Deploying the sample directly to a local minikube installation

This is the simplest way for a developer to get the sample up and running locally.

## Before you begin

* Install a Git client to obtain the sample code.
* Install [Maven](https://maven.apache.org/download.cgi) and a Java 8 JDK.
* Install a [Docker](https://docs.docker.com/engine/installation/) engine.

## Install the Microservice Builder Sample application

1. Install [minikube](https://microservicebuilder.mybluemix.net/docs/minikube.html).
1. Install the [Microservice Builder fabric](https://microservicebuilder.mybluemix.net/docs/installing_fabric_task.html) - these are various services that run on top of Kubernetes.
1. Enable ingress with the command `minikube addons enable ingress`.
1. `git clone` the following projects:
   1. [sample.microservicebuilder.web-app](https://github.com/WASdev/sample.microservicebuilder.web-app)
   1. [sample.microservicebuilder.vote](https://github.com/WASdev/sample.microservicebuilder.vote)
   1. [sample.microservicebuilder.schedule](https://github.com/WASdev/sample.microservicebuilder.schedule)
   1. [sample.microservicebuilder.speaker](https://github.com/WASdev/sample.microservicebuilder.speaker)
   1. [sample.microservicebuilder.session](https://github.com/WASdev/sample.microservicebuilder.session)
1. `mvn clean package` in each ../sample.microservicebuilder.* projects except docs.
1. If you have not done so already, ensure that your Docker CLI is targeting the minikube Docker engine with `minikube docker-env`.
1. `docker build -t [name] .` in each ../sample.microservicebuilder.* projects except docs, where [name] is the image name given in the deployment YAML in the `manifests` directory for the project. For reference, the image names are mapped as follows:
   * sample.microservicebuilder.web-app: `web-application`
   * sample.microservicebuilder.vote: `microservice-vote`
   * sample.microservicebuilder.schedule: `microservice-schedule`
   * sample.microservicebuilder.speaker: `microservice-speaker`
   * sample.microservicebuilder.session: `microservice-session`
1. Deploy each microservice from its root directory with the command `kubectl apply -f manifests`.
1. Use `kubectl get ing` to determine the address of the `web-application-ingress`. Open this location in a web browser to access the sample. 

## Modifying the sample

Once you've made changes to the source code you'll want to rebuild and redeploy the new modules. See [this topic](updating_the_app.md) for some notes about redeployment. You can also explore adding [security](adding_security.md) to the application with OpenID Connect and JSON Web Tokens (JWT).
