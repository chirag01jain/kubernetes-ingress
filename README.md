# Application deployment using NGINX Ingress 

This repo provides an implementation of an Ingress controller for NGINX, and 2 deployments are exposed to access via ingress resource.

## Resource Involved in this Repo:

1) Deployments:

a) amazon
b) flipkart

2) Service:

amazon-svc
flipkart-svc

3) Ingress Resource 

4) Ingress controller:

a) Namespace
B) ServiceAccount
c) Secret
d) ConfigMap
e) RBAC
e) Daemon set

## What is the Ingress?

The Ingress is a Kubernetes resource that lets you configure an HTTP load balancer for applications running on Kubernetes, represented by one or more [Services](https://kubernetes.io/docs/concepts/services-networking/service/). Such a load balancer is necessary to deliver those applications to clients outside of the Kubernetes cluster.

The Ingress resource supports the following features:
* **Content-based routing**:
    * *Host-based routing*. For example, routing requests with the host header `flipkart.testlinux.tech` to one group of services and the host header `amazon.testlinux.tech` to another group.
    * *Path-based routing*. For example, routing requests with the URI that starts with `/serviceA` to service A and requests with the URI that starts with `/serviceB` to service B.
* **TLS/SSL termination** for each hostname, such as `flipkart.testlinux.tech`.

See the [Ingress User Guide](https://kubernetes.io/docs/user-guide/ingress/) to learn more about the Ingress resource.

## What is the Ingress Controller?

The Ingress controller is an application that runs in a cluster and configures an HTTP load balancer according to Ingress resources. The load balancer can be a software load balancer running in the cluster or a hardware or cloud load balancer running externally. Different load balancers require different Ingress controller implementations. 

In the case of NGINX, the Ingress controller is deployed in a pod along with the load balancer.

## Contacts

I’d love to hear your feedback! If you have any suggestions or experience issues with our Ingress controller, please create an issue or send a pull request on Github. You can contact us directly via [chirag01jain@gmail.com](mailto:chirag01jain@gmail.com).
