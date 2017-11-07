# Deploying the sample via a pipeline to IBM Cloud private 

This method presents the sample with a Jenkins-based devOps pipeline.

## Before you begin

* Install a Git client to obtain the sample code.
* Install [Maven](https://maven.apache.org/download.cgi) and a Java 8 JDK if you wish to build changes locally.
* Install a [Docker](https://docs.docker.com/engine/installation/) engine if you wish to fully test changes locally.

## Install the Microservice Builder Sample application and the Jenkins-based pipeline

1. Fork the `WASdev/sample.microservicebuilder.*` projects into your own Git organisation.
1. Install [IBM Cloud private](https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/W1559b1be149d_43b0_881e_9783f38faaff) - see the product [documentation](https://www.ibm.com/support/knowledgecenter/SSBS6K_1.2.0/kc_welcome_containers.html).
1. [Install the Microservice Builder fabric](https://www.ibm.com/support/knowledgecenter/SS5PWC/installing_fabric_task.html) - these are various services that run on top of Kubernetes.
1. [Install the Microservice Builder ELK Sample](https://github.com/WASdev/sample.microservicebuilder.helm.elk) - Elasticsearch, Logstash, and Kibana stack used for monitoring metrics. (This is optional, the sample application will still function correctly without the ELK installation.)
1. [Install the Microservice Builder pipeline](https://www.ibm.com/support/knowledgecenter/SS5PWC/pipeline.html), adding your organisation organisation to the list of GitHub organisations that Jenkins will monitor.
1. Check that the sample repositories have built and deployed correctly.
1. Use `kubectl get ing` to determine the address of the `web-application-ingress`. Open this location in a web browser to access the sample.

## Modifying the sample

Once you've made changes to the source code you'll want to rebuild and redeploy the new modules. See [this topic](updating_the_app.md) for some notes about redeployment. In general, make your changes in a branch and use `git push` to trigger the build pipeline once you have webhooks set up.
