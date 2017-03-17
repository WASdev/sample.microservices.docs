# Adding Security
Security can optionally be added to the backend services using OpenID Connect and JSON Web Tokens (JWT).

## Authentication Process Overview
- Web application contacts backend service.
- Backend service redirects web browser to OpenID Connect server (microservice-ssoserver).
- OpenID Connect server prompts for user id and password.  If successful, redirects the web browser back to the backend service, along with a JSON Web Token.
- The backend service examines the token, and if all is well, grants access.

## Deploying security

This demonstrates securing a single backend service, the schedule service, in a minikube environment.  Adding security to the other services would work the same way (not yet implemented). 


Deployment process:

1. Add a configMap to Kubernetes that will provide the external-facing IP address to the sso-service and schedule-service.  This is necessary so they can properly redirect calls from an external web browser.

    Run ``minikube ip``  to obtain minikube's external ip address.
    Add that to a configMap:
 
     ``kubectl create configmap ipaddr-config --from-literal=EXTERNAL_IP_ADDR=(your minikube ip)``
      
1. Clone or download the [sample.microservicebuilder.ssoserver](https://github.com/WASdev/sample.microservicebuilder.ssoserver) repository.       
      
1. In sample.microservicebuilder.ssoserver, ``edit src/main/liberty/userids.xml and set your desired userid(s) and password(s).``  A Kubernetes secret will be created from this file during the build. 

1. Uninstall web-application and schedule-service if they are present. 
```
  kubectl delete deployment microservice-schedule-sample
  kubectl delete deployment microservice-webapp-sample
  kubectl delete service schedule-service
  kubectl delete service webapp-service
  kubectl delete ingress schedule-ingress
  kubectl delete ingress web-application-ingress
```
1. Build and deploy the SSO service, schedule service and web application with security enabled.
```
  cd sample.microservicebuilder.ssoserver
  mvn clean package
  docker build -t microservice-ssoserver .
  kubectl apply -f target/manifests
  cd ../sample.microservicebuilder.schedule
  mvn clean package -P security
  docker build -t microservice-schedule -f DockerfileSecured .
  kubectl apply -f manifests-secure
  cd ../sample.microservicebuilder.web-app
  mvn clean package -P security
  docker build -t web-application .
  kubectl apply -f manifests-secure
```
To check that the service is running, run ``docker ps | grep sso`` should show a couple of running containers. 

Access the schedule service through the web application at http://(your_minikube_ip), then click on the "schedules" link at the top of the page.  You should be redirected to the sso-service and prompted for an id and password.  Enter the id and password you configured earlier.  You should be redirected back to the schedule service.

### Further work

Before using this in anything resembling production, some additional steps would be needed:

- Configure the ssoserver to use a database or LDAP to hold ids and passwords, or at minimum, encrypt the passwords in userids.xml


