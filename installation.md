# 1. Installing the Ingress Controller

This document describes how to install the NGINX Ingress Controller in your Kubernetes cluster using the provided Kubernetes manifests.

### Clone the Ingress controller repo and change into the deployments folder:

$ git clone https://github.com/chirag01jain/kubernetes-ingress

$ cd kubernetes-ingress/

### 1. Configure RBAC

#### a) Create a namespace and a service account for the Ingress controller:

$ kubectl apply -f common/ns-and-sa.yaml

#### b) Create a cluster role and cluster role binding for the service account:

$ kubectl apply -f rbac/rbac.yaml

#### Note: To perform this step you must be a cluster admin
---------------------------------------------------------------------------------------
### 2. Create Common Resources

#### a) Create a secret with a TLS certificate and a key for the default server in NGINX:

$ kubectl apply -f common/default-server-secret.yaml

Note: For testing purposes we include a self-signed certificate and key that we generated. However, we recommend that you use your own certificate and key.

##### b) Create a config map for customizing NGINX configuration:

$ kubectl apply -f common/nginx-config.yaml
---------------------------------------------------------------------------------------

### 3. Deploy the Ingress Controller

*Using DaemonSet:* When you run the Ingress Controller by using a DaemonSet, Kubernetes will create an Ingress controller pod on every node of the cluster.

kubectl apply -f daemon-set/nginx-ingress.yaml
---------------------------------------------------------------------------------------

### 4. Deploy the Ingress Controller

kubectl apply -f daemon-set/nginx-ingress.yaml

#### Note: You can modify the hostPort in the configuration based on your requirement.
---------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------

# 2. Deploy Application, Service and Ingress for your websites

For testing, we have 2 application, one servicing Flipkart website and another Amazon website. 

We'll create deployment for each website, their respective services and Ingress resource to map the host with the service.

#### 1. Create deployment for Amazon and Flipkart

$ kubectl create -f deployment/amazon.yaml
$ kubectl create -f deployment/flipkart.yaml
---------------------------------------------------------------------------------------

#### 2. Create services both for amazon and flipkart

$ kubectl create -f service/flipkartsvc.yaml
$ kubectl create -f service/amazonsvc.yaml
---------------------------------------------------------------------------------------

#### 3. Create a Ingress resource

$ kubectl create -f ingress/ingress.yaml
---------------------------------------------------------------------------------------

Once all the resources are deployed, configure a DNS 'A' record for both your site, and point it to one IP running load balancer service. Configure the LB to listen on port 80 and forward the traffic to the hostport defined in the Ingress Controller Daemon set. 

Access both website on the browser and you will see, both opens up showing files within their respective document root.

#### Note: You can either use a custom Load balancer or you can use a cloud provider Load balancer service, say DigitalOcean LB service to load balance your website workload.

## Contacts

I’d love to hear your feedback! If you have any suggestions or experience issues with our setup, please create an issue or send a pull request on Github. You can contact me directly via [chirag01jain@gmail.com](mailto:chirag01jain@gmail.com).
