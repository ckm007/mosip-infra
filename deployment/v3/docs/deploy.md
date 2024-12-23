# Esignet and dependencies Deployment in Kubernetes cluster
## Overview
* Esignet and its dependent services will be deployed here in the form of microservices in k8 cluster.
* [Wireguard](https://www.wireguard.com/) is used as a trust network extension to access the observation plane and privately accessible backend services.
* Esignet uses Nginx server for:
  * SSL termination
  * Reverse Proxy
  * CDN/Cache management
  * Loadbalancing
* Kubernetes cluster is created and administered using the [Rancher](https://rancher.com/docs/rancher/v1.3/en/kubernetes/#rancher-ui) and [rke](https://www.rancher.com/products/rke) tools.
* In our ref-impl of Esignet deployment we need two k8 clusters.
  * One K8 cluster for observation plane:
    * This cluster is a part of the observation plane and it helps in administrative tasks.
    * By design, this is kept independent of the actual cluster as a good security practice and to ensure clear segregation of roles and responsibilities.
    * As a best practice, this cluster or it's services should be internal and should never be exposed to the external world.
    * This K8 cluster contains below mentioned services:
      * Rancher is used for managing the MOSIP cluster.
      * Keycloak in this cluster is used for cluster user access management.
      * It is recommended to configure log monitoring and network monitoring in this cluster.
      * In case you have an internal container registry, then it should run here.
  * One K8 cluster for Esignet and its dependent services deployment:
    * This cluster runs all the Esignet and its dependent components and certain third party components to secure the cluster, API’s and data.
    * All the components to be deployed as as follows:
      * K8's cluster configuration tools. (Istio, NFS CSI, Monitoring, logging etc).
      * Esignet pre-requisites services.
      * Esignet and dependent services.
## Architecture [TODO]
Add Architecture Diagram.
## Deployment Repos
* [k8s-infra](https://github.com/mosip/k8s-infra/tree/v1.2.0.1) : contains the scripts to install and configure Kubernetes cluster with required monitoring, logging and alerting tools.
* [Esignet](https://github.com/mosip/esignet/blob/release-1.5.x/) : Contains deployment scripts and source code for :
  * Esignet Pre-requisites services.
  * Esignet services.
  * Esignet Onboarding.
  * Esignet Api-testrig.
* [esignet-mock-services](https://github.com/mosip/esignet-mock-services/blob/release-0.10.x/) : Contains deployment script and source code for :
  * Esignet mock pre-requisites services.
  * Esignet mock services.
  * Esignet mock services onboarding.
* [esignet-signup](https://github.com/mosip/esignet-signup/tree/release-1.1.x) : Contains deployment script and source code for:
  * Esignet signup pre-requisites.
  * Esignet signup services.
  * Esignet signup onboarding pre-requisites.
  * Esignet signup onboarding.

