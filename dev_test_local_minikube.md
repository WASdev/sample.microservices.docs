# Deploying the sample directly to a local minikube installation

This is the simplest way for a developer to get the sample up and running locally.

## Before you begin

* Install a Git client to obtain the sample code.
* Install [Maven](https://maven.apache.org/download.cgi) and a Java 8 JDK.
* Install a [Docker](https://docs.docker.com/engine/installation/) engine.
* Install and initialize the [Helm client](https://docs.helm.sh/using_helm/#installing-helm).

## Install the sample application

1. Install minikube.
1. Enable ingress with the command `minikube addons enable ingress`.
1. `git clone` the following projects:
   1. [sample.microservices.web-app](https://github.com/WASdev/sample.microservices.web-app)
   1. [sample.microservices.vote](https://github.com/WASdev/sample.microservices.vote)
   1. [sample.microservices.schedule](https://github.com/WASdev/sample.microservices.schedule)
   1. [sample.microservices.speaker](https://github.com/WASdev/sample.microservices.speaker)
   1. [sample.microservices.session](https://github.com/WASdev/sample.microservices.session)
1. `mvn clean package` in each ../sample.microservices.* projects except docs.
1. If you have not done so already, ensure that your Docker CLI is targeting the minikube Docker engine with `minikube docker-env`.
1. `docker build -t [name] .` in each ../sample.microservices.* projects except docs, where [name] is the image name given in the Chart.yaml file found in the relevant `chart` directory for the project. For reference, the image names are mapped as follows:
   * sample.microservices.web-app: `web-application`
   * sample.microservices.vote: `microservice-vote`
   * sample.microservices.schedule: `microservice-schedule`
   * sample.microservices.speaker: `microservice-speaker`
   * sample.microservices.session: `microservice-session`
1. Deploy each microservice from its root directory with the following helm install command.
   * sample.microservices.web-app: `helm install --name=web-app chart/web-application`
   * sample.microservices.vote: `helm install --name=vote chart/microservice-vote`
   * sample.microservices.schedule: `helm install --name=schedule chart/microservice-schedule`
   * sample.microservices.speaker: `helm install --name=speaker chart/microservice-speaker`
   * sample.microservices.session: `helm install --name=session chart/microservice-session`   
1. Use `kubectl get ing` to determine the address of the `web-application-ingress`. Open this location in a web browser to access the sample. 

## Modifying the sample

Once you've made changes to the source code you'll want to rebuild and redeploy the new modules. See [this topic](updating_the_app.md) for some notes about redeployment. You can also explore adding [security](adding_security.md) to the application with OpenID Connect and JSON Web Tokens (JWT).
