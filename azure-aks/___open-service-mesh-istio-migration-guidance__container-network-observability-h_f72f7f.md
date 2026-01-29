---
merged_at: 2026-01-29T15:23:36.557271
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-istio-migration-guidance -->

# Migration guidance for Open Service Mesh (OSM) configurations to Istio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article aims to provide a simplistic understanding of how to identify OSM configurations and translate them to equivalent Istio configurations for migrating workloads from OSM to Istio. This by no means, is considered to be an exhaustive detailed guide.

This article provides practical guidance for mapping OSM policies to the [Istio](https://istio.io/) policies to help migrate your microservices deployments managed by OSM over to being managed by Istio. We utilize the OSM [Bookstore sample application](https://docs.openservicemesh.io/docs/getting_started/install_apps/) as a base reference for current OSM users. The following walk-through deploys the Bookstore application. The same steps are followed and explain how to apply the OSM [SMI](https://smi-spec.io/) traffic policies using the Istio equivalent.

If you are not using OSM and are new to Istio, start with [Istio's own Getting Started guide](https://istio.io/latest/docs/setup/getting-started/) to learn how to use the Istio service mesh for your applications. If you are currently using OSM, make sure you are familiar with the OSM [Bookstore sample application](https://docs.openservicemesh.io/docs/getting_started/install_apps/) walk-through on how OSM configures traffic policies. The following walk-through does not duplicate the current documentation, and reference specific topics when relevant. You should be comfortable and fully aware of the bookstore application architecture before proceeding.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI installed](/en-us/cli/azure/install-azure-cli).- The OSM AKS add-on is uninstalled from your AKS cluster
- Any existing OSM Bookstore application, including namespaces, is uninstalled and deleted from your cluster
[Install the Istio AKS service mesh add-on](istio-deploy-addon)

## Modifications needed to the OSM Sample Bookstore Application

To allow for Istio to manage the OSM bookstore application, there are a couple of changes needed in the existing manifests. Those changes are with the bookstore and the mysql services.

### Bookstore Modifications

In the OSM Bookstore walk-through, the bookstore service is deployed along with another bookstore-v2 service to demonstrate how OSM provides traffic shifting. This deployed services allowed you to split the client (`bookbuyer`

) traffic between multiple service endpoints. The first new concept to understand how Istio handles what they refer to as [Traffic Shifting](https://istio.io/latest/docs/tasks/traffic-management/traffic-shifting/).

OSM implementation of traffic shifting is based on the [SMI Traffic Split specification](https://github.com/servicemeshinterface/smi-spec/blob/main/apis/traffic-split/v1alpha4/traffic-split.md). The SMI Traffic Split specification requires the existence of multiple top-level services that are added as backends with the desired weight metric to shift client requests from one service to another. Istio accomplishes traffic shifting using a combination of a [Virtual Service](https://istio.io/latest/docs/reference/config/networking/virtual-service/) and a [Destination Rule](https://istio.io/latest/docs/reference/config/networking/destination-rule/). It is highly recommended that you familiarize yourself with both the concepts of a virtual service and destination rule.

Put simply, the Istio virtual service defines routing rules for clients that request the host (service name). Virtual Services allows for multiple versions of a deployment to be associated to one virtual service hostname for clients to target. Multiple deployments can be labeled for the same service, representing different versions of the application behind the same hostname. The Istio virtual service can then be configured to weight the request to a specific version of the service. The available versions of the service are configured to use the `subsets`

attribute in an Istio destination rule.

The modification made to the bookstore service and deployment for Istio removes the need to have an explicit second service to target, which the SMI Traffic Split needs. There's no need for another service account for the bookstore v2 service as well, since it's to be consolidated under the bookstore service. The original OSM [traffic-access-v1.yaml](https://raw.githubusercontent.com/openservicemesh/osm-docs/release-v1.2/manifests/access/traffic-access-v1.yaml) manifest modification to Istio for both the bookstore v1 and v2 are shown in the below [Create Pods, Services, and Service Accounts](#create-pods-services-and-service-accounts) section. We demonstrate how we do traffic splitting, known as traffic shifting later in the walk-through:

### MySql Modifications

Changes to the mysql stateful set are only needed in the service configuration. Under the service specification, OSM needed the `targetPort`

and `appProtocol`

attributes. These attributes are not needed for Istio. The following updated service for the mysqldb looks like:

```
apiVersion: v1
kind: Service
metadata:
name: mysqldb
labels:
app: mysqldb
service: mysqldb
spec:
ports:
- port: 3306
name: tcp
selector:
app: mysqldb
```


## Deploy the Modified Bookstore Application

Similar to the OSM Bookstore walk-through, we start with a new install of the bookstore application.

### Create the Namespaces

```
kubectl create namespace bookstore
kubectl create namespace bookbuyer
kubectl create namespace bookthief
kubectl create namespace bookwarehouse
```


### Add a namespace label for Istio sidecar injection

For OSM, using the command `osm namespace add <namespace>`

created the necessary annotations to the namespace for the OSM controller to add automatic sidecar injection. With Istio, you only need to just label a namespace to allow the Istio controller to be instructed to automatically inject the Envoy sidecar proxies.

```
kubectl label namespace bookstore istio-injection=enabled
kubectl label namespace bookbuyer istio-injection=enabled
kubectl label namespace bookthief istio-injection=enabled
kubectl label namespace bookwarehouse istio-injection=enabled
```


### Deploy the Istio Virtual Service and Destination Rule for Bookstore

As mentioned earlier in the Bookstore Modification section, Istio handles traffic shifting utilizing a VirtualService weight attribute we configure later in the walk-through. We deploy the virtual service and destination rule for the bookstore service. We deploy only the bookstore version 1 even though the bookstore version 2 is deployed. The Istio virtual service is only supplying a route to the version 1 of bookstore. Different from how OSM handles traffic shifting (traffic split), OSM deployed another service for the bookstore version 2 application. OSM needed to set up traffic to be split between client requests using a TrafficSplit. When using traffic shifting with Istio, we can reference shifting traffic to multiple Kubernetes application deployments (versions) labeled for the same service.

In this walk-though, the deployment of both bookstore versions (v1 & v2) is deployed at the same time. Only the version 1 is reachable due to the virtual service configuration. There is no need to deploy another service for bookstore version 2, we enable a route to the bookstore version 2 later when we update the bookstore virtual service and provide the necessary weight attribute to do traffic shifting.

```
kubectl apply -f - <<EOF
# Create bookstore virtual service
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
name: bookstore-virtualservice
namespace: bookstore
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
---
# Create bookstore destination rule
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
name: bookstore-destination
namespace: bookstore
spec:
host: bookstore
subsets:
- name: v1
labels:
app: bookstore
version: v1
- name: v2
labels:
app: bookstore
version: v2
EOF
```


### Create Pods, Services, and Service Accounts

We use a single manifest file that contains the modifications discussed earlier in the walk-through to deploy the `bookbuyer`

, `bookthief`

, `bookstore`

, `bookwarehouse`

, and `mysql`

applications.

```
kubectl apply -f - <<EOF
##################################################################################################
# bookbuyer service
##################################################################################################
---
# Create bookbuyer Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookbuyer
namespace: bookbuyer
---
# Create bookbuyer Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookbuyer
namespace: bookbuyer
spec:
replicas: 1
selector:
matchLabels:
app: bookbuyer
version: v1
template:
metadata:
labels:
app: bookbuyer
version: v1
spec:
serviceAccountName: bookbuyer
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookbuyer
image: openservicemesh/bookbuyer:latest-main
imagePullPolicy: Always
command: ["/bookbuyer"]
env:
- name: "BOOKSTORE_NAMESPACE"
value: bookstore
- name: "BOOKSTORE_SVC"
value: bookstore
---
##################################################################################################
# bookthief service
##################################################################################################
---
# Create bookthief ServiceAccount
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookthief
namespace: bookthief
---
# Create bookthief Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookthief
namespace: bookthief
spec:
replicas: 1
selector:
matchLabels:
app: bookthief
template:
metadata:
labels:
app: bookthief
version: v1
spec:
serviceAccountName: bookthief
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookthief
image: openservicemesh/bookthief:latest-main
imagePullPolicy: Always
command: ["/bookthief"]
env:
- name: "BOOKSTORE_NAMESPACE"
value: bookstore
- name: "BOOKSTORE_SVC"
value: bookstore
- name: "BOOKTHIEF_EXPECTED_RESPONSE_CODE"
value: "503"
---
##################################################################################################
# bookstore service version 1 & 2
##################################################################################################
---
# Create bookstore Service
apiVersion: v1
kind: Service
metadata:
name: bookstore
namespace: bookstore
labels:
app: bookstore
spec:
ports:
- port: 14001
name: bookstore-port
selector:
app: bookstore
---
# Create bookstore Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookstore
namespace: bookstore
---
# Create bookstore-v1 Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookstore-v1
namespace: bookstore
spec:
replicas: 1
selector:
matchLabels:
app: bookstore
version: v1
template:
metadata:
labels:
app: bookstore
version: v1
spec:
serviceAccountName: bookstore
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookstore
image: openservicemesh/bookstore:latest-main
imagePullPolicy: Always
ports:
- containerPort: 14001
name: web
command: ["/bookstore"]
args: ["--port", "14001"]
env:
- name: BOOKWAREHOUSE_NAMESPACE
value: bookwarehouse
- name: IDENTITY
value: bookstore-v1
---
# Create bookstore-v2 Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookstore-v2
namespace: bookstore
spec:
replicas: 1
selector:
matchLabels:
app: bookstore
version: v2
template:
metadata:
labels:
app: bookstore
version: v2
spec:
serviceAccountName: bookstore
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookstore
image: openservicemesh/bookstore:latest-main
imagePullPolicy: Always
ports:
- containerPort: 14001
name: web
command: ["/bookstore"]
args: ["--port", "14001"]
env:
- name: BOOKWAREHOUSE_NAMESPACE
value: bookwarehouse
- name: IDENTITY
value: bookstore-v2
---
##################################################################################################
# bookwarehouse service
##################################################################################################
---
# Create bookwarehouse Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookwarehouse
namespace: bookwarehouse
---
# Create bookwarehouse Service
apiVersion: v1
kind: Service
metadata:
name: bookwarehouse
namespace: bookwarehouse
labels:
app: bookwarehouse
spec:
ports:
- port: 14001
name: bookwarehouse-port
selector:
app: bookwarehouse
---
# Create bookwarehouse Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookwarehouse
namespace: bookwarehouse
spec:
replicas: 1
selector:
matchLabels:
app: bookwarehouse
template:
metadata:
labels:
app: bookwarehouse
version: v1
spec:
serviceAccountName: bookwarehouse
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookwarehouse
image: openservicemesh/bookwarehouse:latest-main
imagePullPolicy: Always
command: ["/bookwarehouse"]
##################################################################################################
# mysql service
##################################################################################################
---
apiVersion: v1
kind: ServiceAccount
metadata:
name: mysql
namespace: bookwarehouse
---
apiVersion: v1
kind: Service
metadata:
name: mysqldb
labels:
app: mysqldb
service: mysqldb
spec:
ports:
- port: 3306
name: tcp
selector:
app: mysqldb
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
name: mysql
namespace: bookwarehouse
spec:
serviceName: mysql
replicas: 1
selector:
matchLabels:
app: mysql
template:
metadata:
labels:
app: mysql
spec:
serviceAccountName: mysql
nodeSelector:
kubernetes.io/os: linux
containers:
- image: mysql:5.6
name: mysql
env:
- name: MYSQL_ROOT_PASSWORD
value: mypassword
- name: MYSQL_DATABASE
value: booksdemo
ports:
- containerPort: 3306
name: mysql
volumeMounts:
- mountPath: /mysql-data
name: data
readinessProbe:
tcpSocket:
port: 3306
initialDelaySeconds: 15
periodSeconds: 10
volumes:
- name: data
emptyDir: {}
volumeClaimTemplates:
- metadata:
name: data
spec:
accessModes: [ "ReadWriteOnce" ]
resources:
requests:
storage: 250M
EOF
```


To view these resources on your cluster, run the following commands:

```
kubectl get pods,deployments,serviceaccounts -n bookbuyer
kubectl get pods,deployments,serviceaccounts -n bookthief
kubectl get pods,deployments,serviceaccounts,services,endpoints -n bookstore
kubectl get pods,deployments,serviceaccounts,services,endpoints -n bookwarehouse
```


### View the Application UIs

Similar to the original OSM walk-through, if you have the OSM repo cloned you can utilize the port forwarding scripts to view the UIs of each application [here](https://release-v1-2.docs.openservicemesh.io/docs/getting_started/install_apps/#view-the-application-uis). For now, we are only concerned to view the `bookbuyer`

and `bookthief`

UI.

```
cp .env.example .env
bash <<EOF
./scripts/port-forward-bookbuyer-ui.sh &
./scripts/port-forward-bookthief-ui.sh &
wait
EOF
```


In a browser, open up the following urls:

http://localhost:8080 - bookbuyer

http://localhost:8083 - bookthief

## Configure Istio's Traffic Policies

To maintain continuity with the original OSM Bookstore walk-through for the translation to Istio, we discuss [OSM's Permissive Traffic Policy Mode](https://release-v1-2.docs.openservicemesh.io/docs/getting_started/traffic_policies/#permissive-traffic-policy-mode). OSM's permissive traffic policy mode was a concept of allowing or denying traffic in the mesh without any specific [SMI Traffic Access Control rule](https://github.com/servicemeshinterface/smi-spec/blob/main/apis/traffic-access/v1alpha3/traffic-access.md) deployed. The permissive traffic mode configuration existed to allow users to onboard applications into the mesh, while gaining mTLS encryption, without requiring explicit rules to allow applications in the mesh to communicate. The permissive traffic mode feature was to avoid breaking the communications of your application as soon as OSM managed it, and provide time to define your rules while ensuring that application communications was mTLS encrypted. This setting could be set to `true`

or `false`

via OSM's MeshConfig.

Istio handles mTLS enforcement differently. Different from OSM, Istio's permissive mode automatically configures sidecar proxies to use mTLS but allow the service to accept both plaintext and mTLS traffic. The equivalent to OSM's permissive mode configuration is to utilize Istio's `PeerAuthentication`

settings. `PeerAuthentication`

can be done granularly at the namespace or for the entire mesh. For more information on Istio's enforcement of mTLS, read the [Istio Mutual TLS Migration article](https://istio.io/latest/docs/tasks/security/authentication/mtls-migration/).

### Enforce Istio Strict Mode on Bookstore Namespaces

It is important to remember, just like OSM's permissive mode, Istio's `PeerAuthentication`

configuration is only related to the use of mTLS enforcement. Actual layer-7 policies, much like those used in OSM's HTTPRouteGroups, is handled using Istio's AuthorizationPolicy configurations you see later in the walk-through.

We granularly put the `bookbuyer`

, `bookthief`

, `bookstore`

, and `bookwarehouse`

namespaces in Istio's mTLS strict mode.

```
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookbuyer
namespace: bookbuyer
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookthief
namespace: bookthief
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookstore
namespace: bookstore
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookwarehouse
namespace: bookwarehouse
spec:
mtls:
mode: STRICT
EOF
```


### Deploy Istio Access Control Policies

Similar to OSM's [SMI Traffic Target](https://github.com/servicemeshinterface/smi-spec/blob/v0.6.0/apis/traffic-access/v1alpha2/traffic-access.md) and [SMI Traffic Specs](https://github.com/servicemeshinterface/smi-spec/blob/v0.6.0/apis/traffic-specs/v1alpha4/traffic-specs.md) resources to define access control and routing policies for the applications to communicate, Istio accomplishes these similar fine-grain controls by using `AuthorizationPolicy`

configurations.

Let's walk through translating the bookstore TrafficTarget policy, which specifically allows the `bookbuyer`

to communicate to it, with only certain layer-7 path, headers, and methods. The following is a portion of the [traffic-access-v1.yaml](https://raw.githubusercontent.com/openservicemesh/osm-docs/release-v1.2/manifests/access/traffic-access-v1.yaml) manifest.

```
kind: TrafficTarget
apiVersion: access.smi-spec.io/v1alpha3
metadata:
name: bookstore
namespace: bookstore
spec:
destination:
kind: ServiceAccount
name: bookstore
namespace: bookstore
rules:
- kind: HTTPRouteGroup
name: bookstore-service-routes
matches:
- buy-a-book
- books-bought
sources:
- kind: ServiceAccount
name: bookbuyer
namespace: bookbuyer
---
apiVersion: specs.smi-spec.io/v1alpha4
kind: HTTPRouteGroup
metadata:
name: bookstore-service-routes
namespace: bookstore
spec:
matches:
- name: books-bought
pathRegex: /books-bought
methods:
- GET
headers:
- "user-agent": ".*-http-client/*.*"
- "client-app": "bookbuyer"
- name: buy-a-book
pathRegex: ".*a-book.*new"
methods:
- GET
```


If you notice under the TrafficTarget policy, in the spec is where you can explicitly define what source service can communicate with a destination service. We can see that we are allowing the source `bookbuyer`

to be authorized to communicate to the destination bookstore. If we translate the service-to-service authorization from an OSM `TrafficTarget`

configuration to an Istio `AuthorizationPolicy`

, it looks like this below:

```
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: bookstore
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
```


In the Istio's `AuthorizationPolicy`

, you notice how the OSM TrafficTarget policy destination service is mapped to the selector label match and the namespace the service resides in. The source service is shown under the rules section where there is a source/principles attribute that maps to the service account name for the `bookbuyer`

service.

In addition to just the source/destination configuration in the OSM TrafficTarget, OSM binds the use of an HTTPRouteGroup to further define the layer-7 authorization the source has access to. We can see in just the portion of the HTTPRouteGroup below. There are two `matches`

for the allowed source service.

```
apiVersion: specs.smi-spec.io/v1alpha4
kind: HTTPRouteGroup
metadata:
name: bookstore-service-routes
namespace: bookstore
spec:
matches:
- name: books-bought
pathRegex: /books-bought
methods:
- GET
headers:
- "user-agent": ".*-http-client/*.*"
- "client-app": "bookbuyer"
- name: buy-a-book
pathRegex: ".*a-book.*new"
methods:
- GET
```


There is a `match`

named `books-bought`

that allows the source to access path `/books-bought`

using a `GET`

method with host header user-agent and client-app information, and a `buy-a-book`

match that uses a regex express for a path containing `.*a-book.*new`

using a `GET`

method.

We can define these OSM HTTPRouteGroup configurations in the rules section of the Istio `AuthorizationPolicy`

shown below:

```
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
- source:
namespaces: ["bookbuyer"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
```


We can now deploy the OSM migrated traffic-access-v1.yaml manifest as understood by Istio below. There is not an `AuthorizationPolicy`

for the bookthief, so the bookthief UI should stop incrementing books from bookstore v1:

```
kubectl apply -f - <<EOF
##################################################################################################
# bookstore policy
##################################################################################################
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
- source:
namespaces: ["bookbuyer"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
---
##################################################################################################
# bookwarehouse policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "bookwarehouse"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: bookwarehouse
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookstore/sa/bookstore"]
- source:
namespaces: ["bookstore"]
to:
- operation:
methods: ["POST"]
---
##################################################################################################
# mysql policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "mysql"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: mysql
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookwarehouse/sa/bookwarehouse"]
- source:
namespaces: ["bookwarehouse"]
to:
- operation:
ports: ["3306"]
EOF
```


### Allowing the Bookthief Application to access Bookstore

Currently there is no `AuthorizationPolicy`

that allows for the bookthief to communicate with bookstore. We can deploy the following `AuthorizationPolicy`

to allow the bookthief to communicate to the bookstore. You notice the addition for the rule for the bookstore policy that allows the bookthief authorization.

```
kubectl apply -f - <<EOF
##################################################################################################
# bookstore policy
##################################################################################################
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer", "cluster.local/ns/bookthief/sa/bookthief"]
- source:
namespaces: ["bookbuyer", "bookthief"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
---
##################################################################################################
# bookwarehouse policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "bookwarehouse"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: bookwarehouse
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookstore/sa/bookstore"]
- source:
namespaces: ["bookstore"]
to:
- operation:
methods: ["POST"]
---
##################################################################################################
# mysql policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "mysql"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: mysql
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookwarehouse/sa/bookwarehouse"]
- source:
namespaces: ["bookwarehouse"]
to:
- operation:
ports: ["3306"]
EOF
```


The bookthief UI should now be incrementing books from bookstore v1.

## Configure Traffic Shifting between two Service Versions

To demonstrate how to balance traffic between two versions of a Kubernetes service, known as traffic shifting in Istio. As you recall in a previous section, OSM implementation of traffic shifting relied on two distinct services being deployed and adding those service names to the backend configuration of the `TrafficTarget`

policy. This deployment architecture is not needed for how Istio implements traffic shifting. With Istio, we can create multiple deployments that represent each version of the service application and shift traffic to those specific versions via the Istio `virtualservice`

configuration.

The currently deployed `virtualservice`

only has a route rule to the v1 version of the bookstore shown below:

```
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
```


We update the `virtualservice`

to shift 100% of the weight to the v2 version of the bookstore.

```
kubectl apply -f - <<EOF
# Create bookstore virtual service
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
name: bookstore-virtualservice
namespace: bookstore
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
weight: 0
- destination:
host: bookstore
subset: v2
weight: 100
EOF
```


You should now see both the `bookbuyer`

and `bookthief`

UI incrementing for the `bookstore`

v2 service only. You can continue to experiment by changing the `weigth`

attribute to shift traffic between the two `bookstore`

versions.

## Summary

We hope this walk-through provided the necessary guidance on how to migrate your current OSM policies to Istio policies. Take time and review the [Istio Concepts](https://istio.io/latest/docs/concepts/) and walking through [Istio's own Getting Started guide](https://istio.io/latest/docs/setup/getting-started/) to learn how to use the Istio service mesh to manage your applications.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-how-to -->

# Set up Container Network Observability for Azure Kubernetes Service (AKS) - Azure managed Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Container Network Observability for Azure Kubernetes Service (AKS) using Managed Prometheus and Grafana and BYO Prometheus and Grafana and to visualize the scraped metrics

You can use Container Network Observability to collect data about the network traffic of your AKS clusters. It enables a centralized platform for monitoring application and network health. Currently, metrics are stored in Prometheus and Grafana can be used to visualize them. Container Network Observability also offers the ability to enable Hubble. These capabilities are supported for both Cilium and non-Cilium clusters.

Container Network Observability is one of the features of Advanced Container Networking Services. For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see [What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview)

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- The minimum version of Azure CLI required for the steps in this article is 2.56.0. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.29 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Once you have Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Azure managed Prometheus and Grafana

Skip this Section if using BYO Prometheus and Grafana

Use the following example to install and enable Prometheus and Grafana for your AKS cluster.

### Create Azure Monitor resource

```
#Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export AZURE_MONITOR_NAME="<azure-monitor-name>"
# Create Azure monitor resource
az resource create \
--resource-group $RESOURCE_GROUP \
--namespace microsoft.monitor \
--resource-type accounts \
--name $AZURE_MONITOR_NAME \
--location eastus \
--properties '{}'
```


### Create Azure Managed Grafana instance

Use [az grafana create](/en-us/cli/azure/grafana#az-grafana-create) to create a Grafana instance. The name of the Grafana instance must be unique.

```
# Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export GRAFANA_NAME="<grafana-name>"
# Create Grafana instance
az grafana create \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP
```


### Place the Azure Managed Grafana and Azure Monitor resource IDs in variables

Use [az grafana show](/en-us/cli/azure/grafana#az-grafana-show) to place the Grafana resource ID in a variable. Use [az resource show](/en-us/cli/azure/resource#az-resource-show) to place the Azure Monitor resource ID in a variable. Replace **myGrafana** with the name of your Grafana instance.

```
grafanaId=$(az grafana show \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP \
--query id \
--output tsv)
azuremonitorId=$(az resource show \
--resource-group $RESOURCE_GROUP \
--name $AZURE_MONITOR_NAME \
--resource-type "Microsoft.Monitor/accounts" \
--query id \
--output tsv)
```


### Link Azure Monitor and Azure Managed Grafana to the AKS cluster

Use [az aks update](/en-us/cli/azure/aks#az-aks-update) to link the Azure Monitor and Grafana resources to your AKS cluster.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--enable-azure-monitor-metrics \
--azure-monitor-workspace-resource-id $azuremonitorId \
--grafana-resource-id $grafanaId
```


## Visualization

### Visualization using Azure Managed Grafana

Skip this step if using BYO Grafana

Note

The `hubble_flows_processed_total`

metric isn't scraped by default due to high metric cardinality in large scale clusters.
Because of this, the *Pods Flows* dashboards have panels with missing data. To enable this metric and populate the missing data, you need to modify the ama-metrics-settings-configmap. Specifically, update the default-targets-metrics-keep-list section. Follow the below steps to update the configmap:

- Get the latest ama-metrics-settings-configmap.(
[https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml)) - Locate the networkobservabilityHubble = ""
- Change it to networkobservabilityHubble = "hubble.*"
- Now the Pod flow metrics should populate.

To learn more about what minimal ingestion, see the [Minimal Ingestion Documentation](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Make sure the Azure Monitor pods are running using the

`kubectl get pods`

command.`kubectl get pods -o wide -n kube-system | grep ama-`

Your output should look similar to the following example output:

`ama-metrics-5bc6c6d948-zkgc9 2/2 Running 0 (21h ago) 26h ama-metrics-ksm-556d86b5dc-2ndkv 1/1 Running 0 (26h ago) 26h ama-metrics-node-lbwcj 2/2 Running 0 (21h ago) 26h ama-metrics-node-rzkzn 2/2 Running 0 (21h ago) 26h ama-metrics-win-node-gqnkw 2/2 Running 0 (26h ago) 26h ama-metrics-win-node-tkrm8 2/2 Running 0 (26h ago) 26h`

We have created sample dashboards. They can be found under the

**Dashboards > Azure Managed Prometheus**folder. They have names like**"Kubernetes / Networking /**. The suite of dashboards includes:`<name>`

"**Clusters:**shows Node-level metrics for your clusters.**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS).**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace).**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet).


### Visualization using BYO Grafana

Skip this step if using Azure managed Grafana

Add the following scrape job to your existing Prometheus configuration and restart your Prometheus server:

`- job_name: networkobservability-hubble kubernetes_sd_configs: - role: pod relabel_configs: - target_label: cluster replacement: myAKSCluster action: replace - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_pod_label_k8s_app] regex: kube-system;(retina|cilium) action: keep - source_labels: [__address__] action: replace regex: ([^:]+)(?::\d+)? replacement: $1:9965 target_label: __address__ - source_labels: [__meta_kubernetes_pod_node_name] target_label: instance action: replace metric_relabel_configs: - source_labels: [__name__] regex: '|hubble_dns_queries_total|hubble_dns_responses_total|hubble_drop_total|hubble_tcp_flags_total' # if desired, add |hubble_flows_processed_total action: keep`

In

**Targets**of Prometheus, verify the**network-obs-pods**are present.Sign in to Grafana and import following example dashboards using the following IDs:

**Clusters:**shows Node-level metrics for your clusters. (ID:[18814](https://grafana.com/grafana/dashboards/18814-kubernetes-networking-clusters/))**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.(ID:[20925](https://grafana.com/grafana/dashboards/20925-kubernetes-networking-dns-cluster/))**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS). (ID: [20926][https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/](https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/))**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).(ID:[20927](https://grafana.com/grafana/dashboards/20927-kubernetes-networking-drops-workload/)).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace). (ID:[20928](https://grafana.com/grafana/dashboards/20928-kubernetes-networking-pod-flows-namespace/))**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet). (ID:[20929](https://grafana.com/grafana/dashboards/20929-kubernetes-networking-pod-flows-workload/))

Note

- Depending on your Prometheus/Grafana instances' settings, some dashboard panels require specific tweaks to display all data.
- Cilium doesn't currently support DNS metrics/dashboards.


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable Container Network Observability for your AKS cluster.

For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).For more information on Container Network Security and its capabilities, see

[What is Container Network Security?](container-network-security-concepts).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-ip-address-planning -->

# IP address planning for your Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on IP address planning for Azure Kubernetes Service (AKS) clusters.

For specific guidance on IP address planning for individual CNI options, see the [next steps](#next-steps) section for links to plugin documentation.

## Subnet sizing

Your Azure VNet subnet must be large enough to accommodate your cluster, which depends on whether you're using an [overlay network](#overlay-networks) or a [flat network](#flat-networks).

### Overlay networks

With overlay networks, like [Azure CNI Overlay](concepts-network-azure-cni-overlay), your subnet needs to be large enough to assign IPs to your nodes. Pods are assigned IPs from a separate, private CIDR range and won't require VNet IPs. The VNet subnet you use for your cluster can be smaller than with flat networks.

It's important to ensure you allocate enough space in your private CIDR range for your pods to account for scaling. When planning your IP address range sizes, you should calculate your maximum pod count. Each node in your cluster is assigned a /24 (256 IP addresses) subnet for pods. You should plan your overlay network subnet to accommodate the maximum number of nodes you expect to run.

### Flat networks

Flat networks, like [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), require a large enough subnet to accommodate both nodes *and* pods. Since nodes and pods receive IPs from your VNet, you need to plan for the maximum number of nodes and pods you expect to run. Azure CNI Pod Subnet uses a subnet for your nodes and a separate subnet for your pods, so you need to plan for both.

## IP address sizing

### Upgrading and scaling considerations

When IP address planning for your AKS cluster, you should **consider the number of IP addresses required for upgrade and scaling operations**. If you set the IP address range to only support a fixed number of nodes, you won't be able to upgrade or scale your cluster.

When you **upgrade** your AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node, and an older node is removed from the cluster. This rolling upgrade process requires a minimum of one additional block of IP addresses to be available. Your node count is then `n + 1`

where `n`

is the number of nodes in your cluster.

When you **scale** an AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node. Your IP address range needs to take into considerations how you want to scale up the number of nodes and pods your cluster can support. A minimum of one additional node for upgrade operations or the number of nodes set by the [Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade) option should also be included. Your node count is then `n + number-of-additional-scaled-nodes-you-anticipate + max surge`

.

If you're using [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) and you expect your nodes to run the maximum number of pods and you regularly destroy and deploy pods, you should also factor in extra IP addresses per node. There can be few seconds latency required to delete a service and release its IP address for a new service to be deployed and acquire the address. The extra IP addresses account for this possibility.

The IP address plan for an AKS cluster consists of a virtual network, at least one subnet for nodes and pods, and a Kubernetes service address range.

| Azure Resource | Address Range | Limits and Sizing |
|---|---|---|
| Azure Virtual Network | Max size /8. 65,536 configured IP address limit. See
|

Use the following equation to calculate the minimum subnet size, including an extra node for upgrade operations: `(number of nodes + max surge nodes) + ((number of nodes + max surge nodes) * maximum pods per node that you configure)`


Example for a 50-node cluster: `(51) + (51 * 30 (default)) = 1,581`

(/21 or larger)

Example for a 50-node cluster, preparing to scale up an extra 10 nodes with the default max surge of 1 node: `(61) + (61 * 30 (default)) = 1,891`

(/21 or larger)

If you don't specify a maximum number of pods per node when you create your cluster, the maximum number of pods per node is set to 30. The minimum number of IP addresses required is based on that value. If you calculate your minimum IP address requirements on a different maximum value, see [Maximum pods per node](#maximum-pods-per-node) to set this value when you deploy your cluster.

*kubernetes.default.svc.cluster.local*address.## Maximum pods per node

The maximum number of pods per node in an AKS cluster is 250. The *default* maximum number of pods per node varies between *kubenet* and *Azure CNI* networking, and the method of cluster deployment.

| CNI | Default max pods | Configurable at deployment |
|---|---|---|
| Azure CNI Overlay | 250 | Yes (up to 250) |
| Azure CNI Pod subnet | 110 | Yes (up to 250) |
| Azure CNI (Legacy) | 30 | Yes (up to 250) |
| Kubenet | 110 | Yes (up to 250) |

## Configuring maximum pods per node for your clusters

You can configure the maximum number of pods per node either at cluster deployment time or as you add new node pools. You can set the maximum pods per node value as high as 250.

A minimum value for maximum pods per node is enforced to guarantee space for system pods critical to cluster health. The minimum value that can be set for maximum pods per node is 10 if and only if the configuration of each node pool has space for a minimum of 30 pods. For example, setting the maximum pods per node to the minimum of 10 requires each individual node pool to have a minimum of three nodes. This requirement applies for each new node pool created as well, so if 10 is defined as maximum pods per node each subsequent node pool added must have at least three nodes.

| Networking | Minimum | Maximum |
|---|---|---|
| Azure CNI | 10 | 250 |
| Kubenet | 10 | 250 |

Note

The minimum value in the previous table is strictly enforced by the AKS service. You cannot set a value for *maxPods* that is lower than the minimum shown, as doing so can prevent the cluster from starting.

### New clusters

You can define maximum pods per node when you create a new cluster using one of the following methods:

**Azure CLI**: Specify the`--max-pods`

argument when you deploy a cluster with thecommand.`az aks create`

**Azure Resource Manager template**: Specify the`maxPods`

property in the [ManagedClusterAgentPoolProfile] object when you deploy a cluster with an Azure Resource Manager template.**Azure portal**: Change the`Max pods per node`

field in the node pool settings when creating a cluster or adding a new node pool.

### Existing clusters

You can define maximum pods per node when you create a new node pool. If you need to increase the *maxPods* setting on an existing cluster, add a new node pool with the new desired *maxPods* count. After migrating your pods to the new pool, delete the node older pool.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-machine-learning-ops -->

# Concepts - Machine learning operations (MLOps) for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about machine learning operations (MLOps), including what types of practices and tools are involved, and how it can simplify and speed up your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What is MLOps?

Machine learning operations (MLOps) encompasses practices that facilitate collaboration between data scientists, IT operations, and business stakeholders, ensuring that machine learning models are developed, deployed, and maintained efficiently. MLOps applies DevOps principles to machine learning projects, aiming to automate and streamline the end-to-end machine learning lifecycle. This lifecycle includes training, packaging, validating, deploying, monitoring, and retraining models.

MLOps requires multiple roles and tools to work together effectively. Data scientists focus on tasks related to training the model, which is referred to as the * inner loop*. Machine learning engineers and IT operations teams handle the

*, where they apply DevOps practices to package, validate, deploy, and monitor models. When the model needs fine-tuning or retraining, the process loops back to the inner loop.*

**outer loop**### MLOps pipeline

Your MLOps pipeline may leverage various tools and microservices that are deployed sequentially or in parallel. Below are examples of key components in your pipeline that benefit from implementing the following best practices to reduce overhead and allow for faster iteration:

- Unstructured data store for new data flowing into your application
- Vector database to store and query structured, pre-processed data
- Data ingestion and indexing framework
- Vector ingestion and/or model retraining workflows
- Metrics collection and alerting tools (tracking model performance, volume of ingested data, etc.)
- Lifecycle management tools

## DevOps and MLOps

DevOps is a combination of tools and practices that enable you to create robust and reproducible applications. The goal of using DevOps is to quickly deliver value to your end users. Creating, deploying, and monitoring robust and reproducible models to deliver value to end users is the primary goal of MLOps.

There are *three* processes that are essential to MLOps:

**Machine learning workloads**for which a data scientist is responsible, including exploratory data analysis (EDA), feature engineering, and model training and tuning.**Software development practices**including planning, developing, testing, and packaging the model for deployment.**Operational aspects of deploying and maintaining the model in production**, including releasing, configuring resources, and monitoring the model.

### DevOps principles that apply to MLOps

MLOps leverages several principles from DevOps to enhance the machine learning lifecycle, such as *automation*, *continuous integration and delivery (CI/CD)*, *source control*, *Agile planning*, and *infrastructure as code (IaC)*.

#### Automation

By automating tasks, you can reduce manual errors, increase efficiency, and ensure consistency across the ML lifecycle. Automation can be applied to various stages, including data collection, model training, deployment, and monitoring. Through automation, you can also apply proactive measures in the AI pipeline to ensure data compliance with your organization's policies.

For example, your pipeline can automate:

- Model tuning/retraining at regular time intervals or when a certain amount of new data is collected in your application.
- Detection of performance degradation to kickstart fine-tuning or retraining on a different subset of data.
- Common vulnerability and exposure (CVE) scanning on base container images pulled from external container registries to ensure safe security practices.

#### Continuous integration (CI)

Continuous integration covers the *creating* and *verifying* aspects of the model development process. The goal of CI is to create the code and to verify the quality of the code and the model before deployment. This includes testing on a range of sample data sets to ensure that the model performs as expected and meets quality standards.

In MLOps, CI might involve:

- Refactoring exploratory code in Jupyter notebooks into Python or R scripts.
- Validating new input data for missing or error values.
- Unit testing and integration testing in the end-to-end pipeline.

To perform linting and unit testing, you can use automation tools like Azure Pipelines in Azure DevOps or GitHub Actions.

#### Continuous delivery (CD)

Continuous delivery involves the steps needed to safely deploy a model in production. The first step is to package and deploy the model in *pre-production environments*, such as dev and test environments. Portability of the parameters, hyperparameters, and other model artifacts is an important aspect to maintain as you promote the code through these environments. This portability is especially important when it comes to large language models (LLMs) and stable diffusion models. Once the model passes the unit tests and quality assurance (QA) tests, you can approve it for deployment in the *production environment*.

#### Source control

Source control, or *version control*, is essential for managing changes to code and models. In an ML system, this refers to data versioning, code versioning, and model versioning, which allow cross-functional teams to collaborate effectively and track changes over time. Using a Git-based source control system, like [ Azure Repos](https://azure.microsoft.com/products/devops/repos/#:%7E:text=Overview.%20Free%20private%20Git%20repositories,%20pull%20requests,%20and?msockid=182ea2d5e1ff6eb61ccbb1b8e5ff608a) in Azure DevOps or a

**GitHub repository**, enables you to programmatically maintain a history of changes, revert to previous versions, and manage branches for different experiments.

#### Agile planning

Agile planning involves isolating work into *sprints*, which are short time frames for completing specific tasks. This approach allows teams to adapt to changes quickly and deliver incremental improvements to the model. Model training can be an ongoing process, and Agile planning can help scope the project and enable better team alignment.

You can use tools like [ Azure Boards](/en-us/azure/devops/boards/get-started/what-is-azure-boards) in Azure DevOps or

**GitHub issues**to manage your Agile planning.

#### Infrastructure as code (IaC)

You use infrastructure as code to repeat and automate the infrastructure needed to train, deploy, and serve your models. In an ML system, IaC helps simplify and define the appropriate Azure resources needed for the specific job type in code, and the code is maintained in a repository. This allows you to version control your infrastructure and make changes for resource optimization, cost-effectiveness, etc. as needed.

## Next steps

Check out the following articles to learn about best practices for MLOps in your intelligent applications on AKS:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-managed-gpu-nodes -->

# Create a fully managed GPU node pool on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you run GPU workloads in Azure Kubernetes Service (AKS), you need to install and maintain several software components, including the GPU driver, Kubernetes device plugin, and GPU metrics exporter for telemetry. These components are essential for enabling GPU scheduling, container-level GPU access, observability of resource usage, and proper functioning of AKS GPU-enabled nodes. Previously, cluster operators had to either install these components manually or use open-source alternatives like the [NVIDIA GPU Operator](nvidia-gpu-operator), which can introduce complexity and operational overhead.

AKS now supports fully managed GPU nodes (preview) and installs the NVIDIA GPU driver, device plugin, and Data Center GPU Manager [(DCGM) metrics exporter](https://github.com/NVIDIA/dcgm-exporter/tree/main) by default. This feature enables one-step GPU node pool creation and makes the availability of GPU resources in AKS as simple as general purpose CPU nodes.

In this article, you learn how to provision a fully managed GPU node pool (preview) in your AKS cluster, including default installation of the NVIDIA GPU driver, device plugin, and metrics exporter.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need to
[install and upgrade to latest version of the](#install-the-aks-preview-cli-extension).`aks-preview`

extension - You need to
[register the](#register-the-managedgpuexperiencepreview-feature-flag-in-your-subscription).`ManagedGPUExperiencePreview`

feature flag in your subscription

## Limitations

- This feature currently supports
[NVIDIA GPU-enabled virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes-gpu)only. - Updating a general-purpose node pool to add a GPU VM size isn't supported on AKS.
- Windows node pools are not supported with this feature, because GPU metrics are not supported. When creating Windows GPU node pools, AKS automatically installs and manages the drivers and Directx device plugin. See
[AKS Windows GPU documentation](use-windows-gpu)for more information. - Migrating your existing
[multi-instance GPU](gpu-multi-instance)node pools to use this feature isn't supported. - In-place upgrades to use this feature on existing GPU-enabled nodes isn't supported.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

### Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `ManagedGPUExperiencePreview`

feature flag in your subscription

Register the

`ManagedGPUExperiencePreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ManagedGPUExperiencePreview`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create an AKS-managed GPU node pool (preview)

You can add a fully managed GPU node pool (preview) to an existing AKS cluster by specifying OS SKU and `--tags EnableManagedGPUExperience=true`

command. When you do this, AKS will install the GPU driver, GPU device plugin, and metrics exporter automatically.

To use the default Ubuntu operating system (OS) SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the

command with the`az aks nodepool add`

`--tags EnableManagedGPUExperience=true`

command.`az aks nodepool add \ --resource‐group MyResourceGroup \ --cluster‐name MyAKSCluster \ --name gpunp \ --node‐count 1 \ --node‐vm‐size Standard_NC6s_v3 \ --node‐taints sku=gpu:NoSchedule \ --enable‐cluster‐autoscaler \ --min‐count 1 \ --max‐count 3 \ --tags EnableManagedGPUExperience=true`

Confirm that the managed NVIDIA GPU software components are installed successfully:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \`

Your output should include the following values:

`... ... "gpuInstanceProfile": … "gpuProfile": { "driver": "Install" }, ... ...`


## Migrate existing GPU workloads to an AKS-managed GPU node pool

In-place upgrades from a standard NVIDIA GPU node pool to a fully managed NVIDIA GPU node pool (preview) on your AKS cluster isn't supported. We recommend cordoning and draining your existing GPU nodes, then redeploying your workloads to a new GPU-enabled node pool with this feature enabled. See [Resize node pools on AKS](resize-node-pool) to learn more.

## Bring your own (BYO) GPU driver

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can bypass the GPU driver installation during node pool creation. In this case, Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment. See [Skip GPU driver installation](use-nvidia-gpu#skip-gpu-driver-installation) for NVIDIA GPU-enabled nodes on AKS to learn more.

## Next steps

- Deploy a
[sample GPU workload](use-nvidia-gpu#run-a-gpu-enabled-workload)on your AKS-managed GPU-enabled nodes. - Learn about
[GPU utilization and performance metrics](monitor-gpu-metrics)from managed NVIDIA DCGM exporter on your GPU node pool.

## Related articles

- Learn about
[GPU health monitoring](gpu-health-monitoring)with Node Problem Detector (NPD) on AKS. - Run
[distributed inference on multiple AKS GPU nodes](https://blog.aks.azure.com/2025/07/08/kaito-inference-with-acstor).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/passive-cold-solution -->

# Passive-cold solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines a passive-cold solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic when the application is needed.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Passive-cold solution overview

In this approach, we have two independent AKS clusters being deployed in two Azure regions. When the application is needed, we activate the passive cluster to receive traffic. If the passive cluster goes down, we must manually activate the cold cluster to take over the flow of traffic. We can set this condition through a manual input every time or to specify a certain event.

## Scenarios and configurations

This solution is best implemented as a “use as needed” workload, which is useful for scenarios that require workloads to run at specific times of day or run on demand. Example use cases for a passive-cold approach include:

- A manufacturing company that needs to run a complex and resource-intensive simulation on a large dataset. In this case, the passive cluster is located in a cloud region that offers high-performance computing and storage services. The passive cluster is only used when the simulation is triggered by the user or by a schedule. If the cluster doesn’t work upon triggering, the cold cluster can be used as a backup and the workload can run on it instead.
- A government agency that needs to maintain a backup of its critical systems and data in case of a cyber attack or natural disaster. In this case, the passive cluster is located in a secure and isolated location that’s not accessible to the public.

## Components

The passive-cold disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. When the app is needed, the passive cluster is activated to receive network traffic.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If the passive cluster isn't functioning properly because of an issue in its specific Azure region, you can activate the cold cluster and redirect all traffic to that cluster's region. You can use this process while the passive cluster is deactivated until it starts working again. The cold cluster can take a couple minutes to come online, as it has been turned off and needs to complete the setup process. This approach isn't ideal for time-sensitive applications. In that case, we recommend considering an [active-active failover](active-active-solution#failover-process).

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac -->

# Use Kubernetes RBAC with Microsoft Entra ID in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you sign in to an AKS cluster using a Microsoft Entra authentication token. Once authenticated, you can use the built-in Kubernetes role-based access control (RBAC) to manage access to namespaces and cluster resources based on a user's identity or group membership.

This article shows you how to:

Control access using Kubernetes RBAC in an AKS cluster based on Microsoft Entra group membership.

Create example groups and users in Microsoft Entra ID.

Create Roles and RoleBindings in an AKS cluster granting the appropriate permissions, such as to create and view resources.


## Prerequisites

You have an existing AKS cluster with Microsoft Entra integration enabled. If you need an AKS cluster with this configuration, see

[Integrate Microsoft Entra ID with AKS](managed-azure-ad).Kubernetes RBAC is enabled by default during AKS cluster creation. To upgrade an existing cluster with Microsoft Entra integration and Kubernetes RBAC, see

[Enable Microsoft Entra integration on your existing AKS cluster](managed-azure-ad#use-an-existing-cluster).Make sure that Azure CLI version 2.0.61 or later is installed and configured. To find the version, run

`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If using Terraform, install

[Terraform](/en-us/azure/developer/terraform/overview)version 2.99.0 or later.

Use the Azure portal or Azure CLI to verify Microsoft Entra integration with Kubernetes RBAC is enabled.

To verify using the Azure portal:

- Sign-in to the
[Azure portal](https://portal.azure.com)and navigate to your AKS cluster resource. - In the service menu, under
**Settings**, select**Security configuration**. - Under the
**Authentication and Authorization**section, verify the**Microsoft Entra authentication with Kubernetes RBAC**option is selected.

## Create groups in Microsoft Entra ID

This section teaches you how to create two user roles to show how Kubernetes RBAC and Microsoft Entra ID control access cluster resources. The following two example roles are:

**Application developer**- A user named
*aksdev*that's part of the*appdev*group.

- A user named
**Site reliability engineer**(SRE)- A user named
*akssre*that's part of the*opssre*group.

- A user named

In production environments, you can use existing users and groups within a Microsoft Entra tenant.

First, get the resource ID of your AKS cluster using the

command. Then, assign the resource ID to a variable named`az aks show`

*AKS_ID*so it can be referenced in other commands.`AKS_ID=$(az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query id -o tsv)`

Create the first example group in Microsoft Entra ID for the application developers using the

command. The following example creates a group named`az ad group create`

*appdev*:`APPDEV_ID=$(az ad group create --display-name appdev --mail-nickname appdev --query id -o tsv)`

Create an Azure role assignment for the

*appdev*group using thecommand. This assignment lets any member of the group use`az role assignment create`

`kubectl`

to interact with an AKS cluster by granting them the*Azure Kubernetes Service Cluster User*Role.`az role assignment create \ --assignee $APPDEV_ID \ --role "Azure Kubernetes Service Cluster User Role" \ --scope $AKS_ID`

Important

The role name you specify must exactly match the Azure role definition name, including capitalization and spacing.

Tip

If you receive an error such as

`Principal 35bfec9328bd4d8d9b54dea6dac57b82 doesn't exist in the directory a5443dcd-cd0e-494d-a387-3039b419f0d5.`

, wait a few seconds for the Microsoft Entra group object ID to propagate through the directory then try the`az role assignment create`

command again.

## Create users in Microsoft Entra ID

After you create the example Microsoft Entra ID groups for application developers and SREs, the next step is to create two corresponding user accounts. These users are used to sign in to the AKS cluster and validate the Kubernetes RBAC integration described later in this article.

Before you begin, you must set the user principal name (UPN) and password for the application developers. The UPN must include the verified domain name of your tenant. For example, an application developer user, `aksdev@contoso.com`

. In order to figure out (or set) the verified domain names in your tenant, see [Managing custom domain names in your Microsoft Entra ID](/en-us/entra/identity/users/domains-manage).

The following command prompts you for the UPN and sets it to *AAD_DEV_UPN* so it can be used in a later command:

```
echo "Please enter the UPN for application developers: " && read AAD_DEV_UPN
```


The following command prompts you for the password and sets it to *AAD_DEV_PW* for use in a later command:

```
echo "Please enter the secure password for application developers: " && read AAD_DEV_PW
```


### Create user accounts

Create the first user account in Microsoft Entra ID using the

command. The following example creates a user with the display name`az ad user create`

*AKS Dev*, the UPN, and secure password using the values in*AAD_DEV_UPN*and*AAD_DEV_PW*:`AKSDEV_ID=$(az ad user create \ --display-name "AKS Dev" \ --user-principal-name $AAD_DEV_UPN \ --password $AAD_DEV_PW \ --query id -o tsv)`

Add the user to the

*appdev*group created in the previous section using thecommand:`az ad group member add`

`az ad group member add --group appdev --member-id $AKSDEV_ID`


## Create AKS cluster resources

We have our Microsoft Entra groups, users, and Azure role assignments created. Now, you configure the AKS cluster to allow these different groups access to specific resources.

Get the cluster admin credentials using the

command. In one of the following sections, you get the regular`az aks get-credentials`

*user*cluster credentials to see the Microsoft Entra authentication flow in action.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin`

Create a namespace in the AKS cluster using the

command. The following example creates a namespace name`kubectl create namespace`

*dev*:`kubectl create namespace dev`

Note

In Kubernetes,

*Roles*define the permissions to grant, and*RoleBindings*apply them to desired users or groups. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see[Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the

**UPN**. If the user is in a different Microsoft Entra tenant, query for and use the*objectId*property instead.Create a Role for the

*dev*namespace, which grants full permissions to the namespace. In production environments, you can specify more granular permissions for different users or groups. Create a file named`role-dev-namespace.yaml`

and paste the following YAML manifest:`kind: Role apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-full-access namespace: dev rules: - apiGroups: ["", "extensions", "apps"] resources: ["*"] verbs: ["*"] - apiGroups: ["batch"] resources: - jobs - cronjobs verbs: ["*"]`

Create the Role using the

command and specify the filename of your YAML manifest.`kubectl apply`

`kubectl apply -f role-dev-namespace.yaml`

Get the resource ID for the

*appdev*group using thecommand. This group is set as the subject of a RoleBinding in the next step.`az ad group show`

`az ad group show --group appdev --query id -o tsv`

Create a RoleBinding for the

*appdev*group to use the previously created Role for namespace access. Create a file named`rolebinding-dev-namespace.yaml`

and paste the following YAML manifest. On the last line, replace*groupObjectId*with the group object ID output from the previous command.`kind: RoleBinding apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-access namespace: dev roleRef: apiGroup: rbac.authorization.k8s.io kind: Role name: dev-user-full-access subjects: - kind: Group # Replace the placeholder below with the group's objectId (GUID) name: groupObjectId`

Tip

If you want to create the RoleBinding for a single user, specify

*kind: User*and replace*groupObjectId*with the UPN in the previous sample.Create the RoleBinding using the

command and specify the filename of your YAML manifest:`kubectl apply`

`kubectl apply -f rolebinding-dev-namespace.yaml`


## Access AKS cluster resources with Microsoft Entra identities

Now, test that the expected permissions work when you create and manage resources in an AKS cluster. In these examples, you schedule and view pods in the user's assigned namespace, and try to schedule and view pods outside of the assigned namespace.

Reset the

*kubeconfig*context using thecommand. In a previous section, you set the context using the cluster admin credentials. The admin user bypasses Microsoft Entra sign-in prompts. Without the`az aks get-credentials`

`--admin`

parameter, the user context is applied that requires all requests to be authenticated using Microsoft Entra ID.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule a basic NGINX pod using the

command in the`kubectl run`

*dev*namespace:`kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

Enter the credentials for the

*appdev*group account (enter*your*own credentials) at the sign-in prompt. Once you're successfully signed in, the account token is cached for future`kubectl`

commands. The NGINX is successfully scheduled as shown in the following example output:`$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code B24ZD6FP8 to authenticate. pod/nginx-dev created`

Use the

command to view pods in the`kubectl get pods`

*dev*namespace:`kubectl get pods --namespace dev`

Ensure the status of the NGINX pod is

*Running*. The output looks like the following output:`$ kubectl get pods --namespace dev NAME READY STATUS RESTARTS AGE nginx-dev 1/1 Running 0 4m`


### Test SRE access to AKS cluster resources

To confirm that our Microsoft Entra group membership and Kubernetes RBAC work correctly between different users and groups, try the previous commands when signed in as the *akssre* user.

Reset the

*kubeconfig*context using thecommand that clears the previously cached authentication token for the`az aks get-credentials`

*aksdev*user.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule and view pods in the assigned

*SRE*namespace. When prompted, sign in with the*opssre*group account credentials (enter*your*own credentials).`kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre kubectl get pods --namespace sre`

As shown in the following example output, you can successfully create and view the pods:

`$ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre`

To sign in, use a web browser to open the page

[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)and enter the code BM4RHP3FD to authenticate.`pod/nginx-sre created $ kubectl get pods --namespace sre NAME READY STATUS RESTARTS AGE nginx-sre 1/1 Running 0`

Try to view or schedule pods outside of assigned SRE namespace.

`kubectl get pods --all-namespaces kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

These

`kubectl`

commands fail, as shown in the following example output. The user's group membership and Kubernetes Role and RoleBindings don't grant permissions to create or manager resources in other namespaces.`$ kubectl get pods --all-namespaces Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot list pods at the cluster scope $ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create pods in the namespace "dev"`


### Create and view cluster resources outside of the assigned namespace

To view pods outside of the *dev* namespace. Use the [ kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command using

`--all-namespaces`

:```
kubectl get pods --all-namespaces
```


The user's group membership doesn't have a Kubernetes Role that allows this action, as shown in the following example output:

```
Error from server (Forbidden): pods is forbidden: User "aksdev@contoso.com" cannot list resource "pods" in API group "" at the cluster scope
```


In the same way, schedule a pod in a different namespace, such as the *SRE* namespace. The user's group membership doesn't align with a Kubernetes Role and RoleBinding to grant these permissions, as shown in the following example output:

```
$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre
Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create resource "pods" in API group "" in the namespace "sre"
```


### Clean up cluster resources

To clean up all of the resources, run the following commands:

```
# Get the admin kubeconfig context to delete the necessary cluster resources.
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
# Delete the dev and SRE namespaces. This also deletes the pods, Roles, and RoleBindings.
kubectl delete namespace dev
kubectl delete namespace sre
# Delete the Microsoft Entra ID user accounts for aksdev and akssre.
az ad user delete --upn-or-object-id $AKSDEV_ID
az ad user delete --upn-or-object-id $AKSSRE_ID
# Delete the Microsoft Entra ID groups for appdev and opssre. This also deletes the Azure role assignments.
az ad group delete --group appdev
az ad group delete --group opssre
```


## Next steps

For more information about how to secure Kubernetes clusters, see

[Access and identity options for AKS](concepts-identity#kubernetes-rbac).For best practices on identity and resource control, see

[Best practices for authentication and authorization in AKS](operator-best-practices-identity).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-portal -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and Azure Kubernetes Service (AKS) clusters. To provide this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). AKS clusters are created with *basic* networking (kubenet) by default.

This article shows you how to create a virtual network and subnets, and then deploy an AKS cluster that uses advanced networking using the Azure portal.

Note

For an overview of virtual node region availability and limitations, see [Use virtual nodes in AKS](virtual-nodes).

## Before you begin

You need the ACI service provider registered on your subscription.

Check the status of the ACI provider registration using the

command.`az provider list`

`az provider list --query "[?contains(namespace,'Microsoft.ContainerInstance')]" -o table`

The following example output shows the

*Microsoft.ContainerInstance*provider is*Registered*:`Namespace RegistrationState RegistrationPolicy --------------------------- ------------------- -------------------- Microsoft.ContainerInstance Registered RegistrationRequired`

If the provider is

*NotRegistered*, register it using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerInstance`


## Create an AKS cluster

- Navigate to the Azure portal home page.
- Select
**Create a resource**>**Containers**. - On the
**Azure Kubernetes Service (AKS)**resource, select**Create**. - On the
**Basics**page, configure the following options:*Project details*: Select an Azure subscription, then select or create an Azure resource group, such as*myResourceGroup*.*Cluster details*: Enter a**Kubernetes cluster name**, such as*myAKSCluster*. Select a region and Kubernetes version for the AKS cluster.

- Select
**Next: Node pools**and check **Enable virtual nodes*. - Select
**Review + create**. - After the validation completes, select
**Create**.

By default, this process creates a managed cluster identity, which is used for cluster communication and integration with other Azure services. For more information, see [Use managed identities](use-managed-identity). You can also use a service principal as your cluster identity.

This process configures the cluster for advanced networking and the virtual nodes to use their own Azure virtual network subnet. The subnet has delegated permissions to connect Azure resources between the AKS cluster. If you don't already have a delegated subnet, the Azure portal creates and configures an Azure virtual network and subnet with the virtual nodes.

## Connect to the cluster

The Azure Cloud Shell is a free interactive shell you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account. To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. The `kubectl`

client is pre-installed in the Azure Cloud Shell.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the cluster name`az aks get-credentials`

*myAKSCluster*in the resource group named*myResourceGroup*:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

.`kubectl get nodes`

`kubectl get nodes`

The following example output shows the single VM node created and the virtual Linux node named

*virtual-node-aci-linux*:`NAME STATUS ROLES AGE VERSION virtual-node-aci-linux Ready agent 28m v1.11.2 aks-agentpool-14693408-0 Ready agent 32m v1.11.2`


## Deploy a sample app

In the Azure Cloud Shell, create a file named

`virtual-node.yaml`

and copy in the following YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aci-helloworld spec: replicas: 1 selector: matchLabels: app: aci-helloworld template: metadata: labels: app: aci-helloworld spec: containers: - name: aci-helloworld image: mcr.microsoft.com/azuredocs/aci-helloworld ports: - containerPort: 80 nodeSelector: kubernetes.io/role: agent beta.kubernetes.io/os: linux type: virtual-kubelet tolerations: - key: virtual-kubelet.io/provider operator: Exists`

The YAML defines a

[nodeSelector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)and[toleration](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/), which allows the pod to be scheduled on the virtual node. The pod is assigned an internal IP address from the Azure virtual network subnet delegated for use with virtual nodes.Run the application using the

command.`kubectl apply`

`kubectl apply -f virtual-node.yaml`

View the pods scheduled on the node using the

command with the`kubectl get pods`

`-o wide`

argument.`kubectl get pods -o wide`

The following example output shows the

`virtual-node-helloworld`

pod scheduled on the`virtual-node-linux`

node.`NAME READY STATUS RESTARTS AGE IP NODE virtual-node-helloworld-9b55975f-bnmfl 1/1 Running 0 4m 10.241.0.4 virtual-node-aci-linux`


Note

If you use images stored in Azure Container Registry, [configure and use a Kubernetes secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/). A limitation of virtual nodes is you can't use integrated Microsoft Entra service principal authentication. If you don't use a secret, pods scheduled on virtual nodes fail to start and report the error `HTTP response status code 400 error code "InaccessibleImage"`

.

## Test the virtual node pod

To test the pod running on the virtual node, browse to the demo application with a web client. The pod is assigned an internal IP address, so you can easily test the connectivity from another pod on the AKS cluster.

Create a test pod and attach a terminal session to it using the following

`kubectl run`

command.`kubectl run -it --rm virtual-node-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

Install

`curl`

in the pod using the following`apt-get`

command.`apt-get update && apt-get install -y curl`

Access the address of your pod using the following

`curl`

command and provide your internal IP address.`curl -L http://10.241.0.4`

The following condensed example output shows the demo application.

`<html> <head> <title>Welcome to Azure Container Instances!</title> </head> [...]`

Close the terminal session to your test pod with

`exit`

, which also deletes the pod.`exit`


## Next steps

In this article, you scheduled a pod on the virtual node and assigned a private, internal IP address. If you want, you can instead create a service deployment and route traffic to your pod through a load balancer or ingress controller. For more information, see [Create a basic ingress controller in AKS](ingress-basic).

Virtual nodes are one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/what-is-aks -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler -->

# Use the cluster autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demands. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed.

This article shows you how to enable and manage the cluster autoscaler in AKS, which is based on the [open-source Kubernetes version](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).

## Before you begin

This article requires Azure CLI version 2.0.76 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Use the cluster autoscaler on an AKS cluster

Important

The cluster autoscaler is a Kubernetes component. Although the AKS cluster uses a virtual machine scale set for the nodes, don't manually enable or edit settings for scale set autoscaling. Let the Kubernetes cluster autoscaler manage the required scale settings. For more information, see [Can I modify the AKS resources in the node resource group?](faq)

### Enable the cluster autoscaler on a new cluster

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create an AKS cluster using the

command and enable and configure the cluster autoscaler on the node pool for the cluster using the`az aks create`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command creates a cluster with a single node backed by a virtual machine scale set, enables the cluster autoscaler, sets a minimum of one and maximum of three nodes:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --vm-set-type VirtualMachineScaleSets \ --load-balancer-sku standard \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --generate-ssh-keys`

It takes a few minutes to create the cluster and configure the cluster autoscaler settings.


### Enable the cluster autoscaler on an existing cluster

Update an existing cluster using the

command and enable and configure the cluster autoscaler on the node pool using the`az aks update`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command updates an existing AKS cluster to enable the cluster autoscaler on the node pool for the cluster and sets a minimum of one and maximum of three nodes:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

It takes a few minutes to update the cluster and configure the cluster autoscaler settings.


### Disable the cluster autoscaler on a cluster

Disable the cluster autoscaler using the

command and the`az aks update`

`--disable-cluster-autoscaler`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-cluster-autoscaler`

Nodes aren't removed when the cluster autoscaler is disabled.


Note

You can manually scale your cluster after disabling the cluster autoscaler using the [ az aks scale](/en-us/cli/azure/aks#az-aks-scale) command. If you use the horizontal pod autoscaler, it continues to run with the cluster autoscaler disabled, but pods might end up unable to be scheduled if all node resources are in use.

### Re-enable the cluster autoscaler on a cluster

You can re-enable the cluster autoscaler on an existing cluster using the [ az aks update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.## Use the cluster autoscaler on node pools

### Use the cluster autoscaler on multiple node pools

You can use the cluster autoscaler with [multiple node pools](create-node-pools) and can enable the cluster autoscaler on each individual node pool and pass unique autoscaling rules to them.

Update the settings on an existing node pool using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


### Disable the cluster autoscaler on a node pool

Disable the cluster autoscaler on a node pool using the

command and the`az aks nodepool update`

`--disable-cluster-autoscaler`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --disable-cluster-autoscaler`


### Re-enable the cluster autoscaler on a node pool

You can re-enable the cluster autoscaler on a node pool using the [ az aks nodepool update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview#enable-cluster-auto-scaler-for-a-node-pool) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.Note

If you plan on using the cluster autoscaler with node pools that span multiple zones and leverage scheduling features related to zones, such as volume topological scheduling, we recommend you have one node pool per zone and enable `--balance-similar-node-groups`

through the autoscaler profile. This ensures the autoscaler can successfully scale up and keep the sizes of the node pools balanced.

## Update the cluster autoscaler settings

As your application demands change, you might need to adjust the cluster autoscaler node count to scale efficiently.

Change the node count using the

command and update the cluster autoscaler using the`az aks update`

`--update-cluster-autoscaler`

parameter and specifying your updated node`--min-count`

and`--max-count`

.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

The cluster autoscaler enforces the minimum count in cases where the actual count drops below the minimum due to external factors, such as during a spot eviction or when changing the minimum count value from the AKS API.

## Use the cluster autoscaler profile

You can configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile. For example, a scale down event happens after nodes are under-utilized after 10 minutes. If you have workloads that run every 15 minutes, you might want to change the autoscaler profile to scale down under-utilized nodes after 15 or 20 minutes. When you enable the cluster autoscaler, a default profile is used unless you specify different settings.

Important

The cluster autoscaler profile affects **all node pools** that use the cluster autoscaler. You can't set an autoscaler profile per node pool. When you set the profile, any existing node pools with the cluster autoscaler enabled immediately start using the profile.

### Cluster autoscaler profile settings

The following table lists the available settings for the cluster autoscaler profile:

| Setting | Description | Default value |
|---|---|---|
`scan-interval` |
How often the cluster is reevaluated for scale up or down. | 10 seconds |
`scale-down-delay-after-add` |
How long after scale up that scale down evaluation resumes. | 10 minutes |
`scale-down-delay-after-delete` |
How long after node deletion that scale down evaluation resumes. | `scan-interval` |
`scale-down-delay-after-failure` |
How long after scale down failure that scale down evaluation resumes. | Three minutes |
`scale-down-unneeded-time` |
How long a node should be unneeded before it's eligible for scale down. | 10 minutes |
`scale-down-unready-time` |
How long an unready node should be unneeded before it's eligible for scale down. | 20 minutes |
`ignore-daemonsets-utilization` |
Whether DaemonSet pods will be ignored when calculating resource utilization for scale down. | `false` |
`daemonset-eviction-for-empty-nodes` |
Whether DaemonSet pods will be gracefully terminated from empty nodes. | `false` |
`daemonset-eviction-for-occupied-nodes` |
Whether DaemonSet pods will be gracefully terminated from non-empty nodes. | `true` |
`scale-down-utilization-threshold` |
The maximum value between the sum of CPU requests and sum of Memory requests of all pods running on the node divided by node's corresponding allocatable resource, below which a node can be considered for scale down. | 0.5 |
`max-graceful-termination-sec` |
Maximum number of seconds the cluster autoscaler waits for pod termination when trying to scale down a node. | 600 seconds |
`balance-similar-node-groups` |
Detects similar node pools and balances the number of nodes between them. | `false` |
`expander` |
Type of node pool
`most-pods` , `random` , `least-waste` , and `priority` . |

`random`

`skip-nodes-with-local-storage`

`true`

, cluster autoscaler doesn't delete nodes with pods with local storage, for example, EmptyDir or HostPath.`false`

`skip-nodes-with-system-pods`

`true`

, cluster autoscaler doesn't delete nodes with pods from kube-system (except for DaemonSet or mirror pods).`true`

`max-empty-bulk-delete`

`new-pod-scale-up-delay`

`max-total-unready-percentage`

`max-node-provision-time`

`ok-total-unready-count`

Note

The ignore-daemonsets-utilization, daemonset-eviction-for-empty-nodes, and daemonset-eviction-for-occupied-nodes parameters are GA from API version 2024-05-01. If you are using the CLI to update these flags, please ensure you are using version 2.63 or later.

### Set the cluster autoscaler profile on a new cluster

Create an AKS cluster using the

command and set the cluster autoscaler profile using the`az aks create`

`cluster-autoscaler-profile`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --cluster-autoscaler-profile scan-interval=30s \ --generate-ssh-keys`


### Set the cluster autoscaler profile on an existing cluster

Set the cluster autoscaler on an existing cluster using the

command and the`az aks update`

`cluster-autoscaler-profile`

parameter. The following example configures the scan interval setting as*30s*:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile scan-interval=30s`


### Configure cluster autoscaler profile for aggressive scale down

Note

Scaling down aggressively is not recommended for clusters experiencing frequent scale-outs and scale-ins within short intervals, as it could potentially result in extended node provisioning times under these circumstances. Increasing `scale-down-delay-after-add`

can help in these circumstances by keeping the node around longer to handle incoming workloads.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=30s,scale-down-delay-after-add=0m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=3m,scale-down-unready-time=3m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=1000,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Configure cluster autoscaler profile for bursty workloads

```
az aks update \
--resource-group "myResourceGroup" \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=20s,scale-down-delay-after-add=10m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=5m,scale-down-unready-time=5m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=100,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Reset cluster autoscaler profile to default values

Reset the cluster autoscaler profile using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile ""`


## Retrieve cluster autoscaler logs and status

You can retrieve logs and status updates from the cluster autoscaler to help diagnose and debug autoscaler events. AKS manages the cluster autoscaler on your behalf and runs it in the managed control plane. You can enable control plane node to see the logs and operations from the cluster autoscaler.

Set up a rule for resource logs to push cluster autoscaler logs to Log Analytics using the

[instructions here](monitor-aks#aks-control-plane-resource-logs). Make sure you check the box for`cluster-autoscaler`

when selecting options for**Logs**.Select the

**Log**section on your cluster.Enter the following example query into Log Analytics:

`AzureDiagnostics | where Category == "cluster-autoscaler"`

View cluster autoscaler scale-up not triggered events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,reason=NotTriggerScaleUp`

View cluster autoscaler warning events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,type=Warning`

The cluster autoscaler also writes out the health status to a

`configmap`

named`cluster-autoscaler-status`

. You can retrieve these logs using the following`kubectl`

command:`kubectl get configmap -n kube-system cluster-autoscaler-status -o yaml`


For more information, see the [Kubernetes/autoscaler GitHub project FAQ](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#ca-doesnt-work-but-it-used-to-work-yesterday-why).

## Cluster Autoscaler Metrics

You can enable [control plane metrics (Preview)](monitor-control-plane-metrics) to see the logs and operations from the [cluster autoscaler](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)

## Next steps

This article showed you how to automatically scale the number of AKS nodes. You can also use the horizontal pod autoscaler to automatically adjust the number of pods that run your application. For steps on using the horizontal pod autoscaler, see [Scale applications in AKS](tutorial-kubernetes-scale).

To further help improve cluster resource utilization and free up CPU and memory for other pods, see [Vertical Pod Autoscaler](vertical-pod-autoscaler).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/outbound-rules-control-egress -->

# Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides the necessary details that allow you to secure outbound traffic from your Azure Kubernetes Service (AKS). It contains the cluster requirements for a base AKS deployment and additional requirements for optional addons and features. You can apply this information to any outbound restriction method or appliance.

To see an example configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Background

AKS clusters are deployed on a virtual network. This network can either be customized and preconfigured by you or it can be created and managed by AKS. In either case, the cluster has **outbound**, or egress, dependencies on services outside of the virtual network.

For management and operational purposes, nodes in an AKS cluster need to access certain ports and fully qualified domain names (FQDNs). These endpoints are required for the nodes to communicate with the API server or to download and install core Kubernetes cluster components and node security updates. For example, the cluster needs to pull container images from Microsoft Artifact Registry (MAR).

The AKS outbound dependencies are almost entirely defined with FQDNs, which don't have static addresses behind them. The lack of static addresses means you can't use network security groups (NSGs) to lock down the outbound traffic from an AKS cluster.

By default, AKS clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. For outbound internet traffic, it's not recommended to set all deny rules in an NSG.

A [network isolated AKS cluster](concepts-network-isolated), provides the simplest and most secure solution for setting up outbound restrictions for a cluster out of the box. A network isolated cluster pulls the images for cluster components and add-ons from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint. The cluster operator can then incrementally set up allowed outbound traffic securely over a private network for each scenario they want to enable. This way the cluster operators have complete control over designing the allowed outbound traffic from their clusters right from the start, thus allowing them to reduce the risk of data exfiltration.

Another solution to securing outbound addresses is using a firewall device that can control outbound traffic based on domain names. Azure Firewall can restrict outbound HTTP and HTTPS traffic based on the FQDN of the destination. You can also configure your preferred firewall and security rules to allow these required ports and addresses.

Important

This document covers only how to lock down the traffic leaving the AKS subnet. AKS has no ingress requirements by default. Blocking **internal subnet traffic** using network security groups (NSGs) and firewalls isn't supported. To control and block the traffic within the cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

## Required outbound network rules and FQDNs for AKS clusters

The following network and FQDN/application rules are required for an AKS cluster. You can use them if you wish to configure a solution other than Azure Firewall.

- IP address dependencies are for non-HTTP/S traffic (both TCP and UDP traffic).
- FQDN HTTP/HTTPS endpoints can be placed in your firewall device.
- Wildcard HTTP/HTTPS endpoints are dependencies that can vary with your AKS cluster based on a number of qualifiers.
- AKS uses an admission controller to inject the FQDN as an environment variable to all deployments under kube-system and gatekeeper-system. This ensures all system communication between nodes and API server uses the API server FQDN and not the API server IP. You can get the same behavior on your own pods, in any namespace, by annotating the pod spec with an annotation named
`kubernetes.azure.com/set-kube-service-host-fqdn`

. If that annotation is present, AKS will set the KUBERNETES_SERVICE_HOST variable to the domain name of the API server instead of the in-cluster service IP. This is useful in cases where the cluster egress is via a layer 7 firewall. - If you have an app or solution that needs to talk to the API server, you must either add an
**additional**network rule to allow**TCP communication to port 443 of your API server's IP****OR**, if you have a layer 7 firewall configured to allow traffic to the API Server's domain name, set`kubernetes.azure.com/set-kube-service-host-fqdn`

in your pod specs. - On rare occasions, if there's a maintenance operation, your API server IP might change. Planned maintenance operations that can change the API server IP are always communicated in advance.
- You might notice traffic towards "md-*.blob.storage.azure.net" endpoint. This endpoint is used for internal components of Azure Managed Disks. Blocking access to this endpoint from your firewall should not cause any issues.
- You might notice traffic towards "umsa*.blob.core.windows.net" endpoint. This endpoint is used to store manifests for Azure Linux VM Agent & Extensions and is regularly checked to download new versions. You can find more details on
[VM Extensions](/en-us/azure/virtual-machines/extensions/features-linux?tabs=azure-cli#network-access).

### Azure Global required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. This isn't required for
konnectivity-agent enabled. |

`*:9000`

*Or*[ServiceTag](/en-us/azure/virtual-network/service-tags-overview#available-service-tags)-`AzureCloud.<Region>:9000`

*Or*[Regional CIDRs](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files)-`RegionCIDRs:9000`

*Or*`APIServerPublicIP:9000`

`(only known after cluster creation)`

[private clusters](private-clusters), or for clusters with the*konnectivity-agent*enabled.**or**`*:123`

**(if using Azure Firewall network rules)**`ntp.ubuntu.com:123`

`CustomDNSIP:53`

`(if using custom DNS servers)`

`APIServerPublicIP:443`

`(if running pods/deployments, like Ingress Controller, that access the API Server)`

[private clusters](private-clusters).### Azure Global required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.azmk8s.io` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. This is required for clusters with konnectivity-agent enabled. Konnectivity also uses Application-Layer Protocol Negotiation (ALPN) to communicate between agent and server. Blocking or rewriting the ALPN extension will cause a failure. This isn't required for
|
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
, `*.data.mcr.microsoft.com` `mcr-0001.mcr-msedge.net` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.azure.com` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

### Microsoft Azure operated by 21Vianet required network rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.Region:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
`*:22` Or
`AzureCloud.<Region>:22` Or
`RegionCIDRs:22` Or `APIServerPublicIP:22` `(only known after cluster creation)` |
TCP | 22 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pod/deployments would use the API IP. |

### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`*.tun.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure Content Delivery Network (CDN). |
`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.chinacloudapi.cn` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`*.azk8s.cn` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
, `mcr.azure.cn` `*.data.mcr.azure.cn` |
`HTTPS:443` |
Required to access images Microsoft Container Registry (MCR) in China Cloud (Mooncake). This registry serves as a cache for mcr.microsoft.com with improved reliability and performance. |

### Azure US Government required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pods/deployments would use the API IP. |

### Azure US Government required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.aks.containerservice.azure.us` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.usgovcloudapi.net` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

## Optional recommended FQDN / application rules for AKS clusters

The following FQDN / application rules aren't required, but are recommended for AKS clusters:

| Destination FQDN | Port | Use |
|---|---|---|
`security.ubuntu.com` , `azure.archive.ubuntu.com` , `changelogs.ubuntu.com` |
`HTTP:80` |
This address lets the Linux cluster nodes download the required security patches and updates. |
`snapshot.ubuntu.com` |
`HTTPS:443` |
This address lets the Linux cluster nodes download the required security patches and updates from ubuntu snapshot service. |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that node image upgrades also come with updated packages including security fixes.

## GPU enabled AKS clusters required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`nvidia.github.io` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`us.download.nvidia.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`download.docker.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |

## Windows Server based node pools required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`onegetcdn.azureedge.net, go.microsoft.com` |
`HTTPS:443` |
To install windows-related binaries |
`*.mp.microsoft.com, www.msftconnecttest.com, ctldl.windowsupdate.com` |
`HTTP:80` |
To install windows-related binaries |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that Node Image Upgrades also come with updated packages including security fixes.

## AKS features, addons, and integrations

### Workload identity

#### Required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
or `login.microsoftonline.com` or `login.chinacloudapi.cn` `login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |

### Microsoft Defender for Containers

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra Authentication. |
`*.ods.opinsights.azure.com` (Azure Government) `*.ods.opinsights.azure.us` (Azure operated by 21Vianet)`*.ods.opinsights.azure.cn` |
`HTTPS:443` |
Required for Microsoft Defender to upload security events to the cloud. |
`*.oms.opinsights.azure.com` (Azure Government) `*.oms.opinsights.azure.us` (Azure operated by 21Vianet)`*.oms.opinsights.azure.cn` |
`HTTPS:443` |
Required to authenticate with Log Analytics workspaces. |
`*.cloud.defender.microsoft.com` |
`HTTPS:443` |
NEW: Required for Microsoft Defender to upload security events to the cloud. |

### Azure Key Vault provider for Secrets Store CSI Driver

If using network isolated clusters, it's recommended to set up [private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service?tabs=portal).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`vault.azure.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server. |
`*.vault.usgovcloudapi.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server in Azure Government. |

### Azure Monitor - Managed Prometheus, Container Insights, and Azure Monitor Application Insights Autoinstrumentation

If using network isolated clusters, it's recommended to set up [private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link#container-insights-log-analytics-workspace), which is supported for Managed Prometheus (Azure Monitor workspace), Container insights (Log Analytics workspace), and Azure Monitor Application Insights Autoinstrumentation (Application Insights resource).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`AzureMonitor:443` |

#### Azure public cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.com` |
443 | |
`*.oms.opinsights.azure.com` |
443 | |
`dc.services.visualstudio.com` |
443 | |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`*.monitoring.azure.com` |
443 | |
`login.microsoftonline.com` |
443 | |
`global.handler.control.monitor.azure.com` |
Access control service | 443 |
`*.ingest.monitor.azure.com` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.com` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |
`<cluster-region-name>.handler.control.monitor.azure.com` |
Fetch data collection rules for specific cluster | 443 |

#### Microsoft Azure operated by 21Vianet cloud required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.cn` |
Data ingestion | 443 |
`*.oms.opinsights.azure.cn` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.cn` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.cn` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.cn` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.cn` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

#### Azure Government cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.us` |
Data ingestion | 443 |
`*.oms.opinsights.azure.us` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.us` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.us` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.us` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.us` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

### Azure Policy

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |
`dc.services.visualstudio.com` |
`HTTPS:443` |
Azure Policy add-on that sends telemetry data to applications insights endpoint. |

#### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

### AKS cost analysis add-on

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`management.azure.com` (Azure Government) `management.usgovcloudapi.net` (Azure operated by 21Vianet)`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra ID authentication. |

## Cluster extensions

### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.com` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |
`arcmktplaceprod.azurecr.io` |
`HTTPS:443` |
This address is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.centralindia.data.azurecr.io` |
`HTTPS:443` |
This address is for the Central India regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.japaneast.data.azurecr.io` |
`HTTPS:443` |
This address is for the East Japan regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westus2.data.azurecr.io` |
`HTTPS:443` |
This address is for the West US2 regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westeurope.data.azurecr.io` |
`HTTPS:443` |
This address is for the West Europe regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.eastus.data.azurecr.io` |
`HTTPS:443` |
This address is for the East US regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`*.ingestion.msftcloudes.com, *.microsoftmetrics.com` |
`HTTPS:443` |
This address is used to send agents metrics data to Azure. |
`marketplaceapi.microsoft.com` |
`HTTPS: 443` |
This address is used to send custom meter-based usage to the commerce metering API. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.us` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |

Note

For any addons that aren't explicitly stated here, the core requirements cover it.

### Istio-based service mesh add-on

In Istio=based service mesh add-on, if you are setting up istiod with a Plugin Certificate Authority (CA) or if you are setting up secure ingress gateway, Azure Key Vault provider for Secrets Store CSI Driver is required for these features. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

### Application routing add-on

Application routing add-on supports SSL termination at the ingress with certificates stored in Azure Key Vault. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

## Next steps

In this article, you learned what ports and addresses to allow if you want to restrict egress traffic for the cluster.

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster see [Secure traffic between pods using network policies in AKS](use-network-policies).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/intro-kubernetes -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster -->

# Tutorial - Create an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. With Azure Kubernetes Service (AKS), you can quickly create a production ready Kubernetes cluster.

In this tutorial, you deploy a Kubernetes cluster in AKS. You learn how to:

- Deploy an AKS cluster that can authenticate to an Azure Container Registry (ACR).
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

## Before you begin

In previous tutorials, you created a container image and uploaded it to an ACR instance. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- If you're using Azure CLI, this tutorial requires that you're running the Azure CLI version 2.35.0 or later. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this tutorial requires that you're running Azure PowerShell version 5.9.0 or later. Check your version with
`Get-InstalledModule -Name Az`

. To install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - If you're using Azure Developer CLI, this tutorial requires that you're running the Azure Developer CLI version 1.5.1 or later. Check your version with
`azd version`

. To install or upgrade, see[Install Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd).

## Create a Kubernetes cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. If a user is assigned multiple roles, permissions are combined. Permissions can be scoped to either a single namespace or across the whole cluster.

To learn more about AKS and Kubernetes RBAC, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra identities in AKS](azure-ad-rbac).

This tutorial requires Azure CLI version 2.35.0 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed.

## Install the Kubernetes CLI

You use the Kubernetes CLI, [ kubectl](https://kubernetes.io/docs/reference/kubectl/), to connect to your Kubernetes cluster. If you use the Azure Cloud Shell,

`kubectl`

is already installed. If you're running the commands locally, you can use the Azure CLI or Azure PowerShell to install `kubectl`

.Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`


## Create an AKS cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. Permissions are combined when users are assigned multiple roles. Permissions can be scoped to either a single namespace or across the whole cluster. For more information, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra ID in AKS](azure-ad-rbac).

For information about AKS resource limits and region availability, see [Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions).

Important

This tutorial creates a three-node cluster. To ensure your cluster operates reliably, you should run at least two nodes. A minimum of three nodes is required to use Azure Container Storage. If you get an error message when trying to create the cluster, then you might need to request a quota increase for your Azure subscription or try a different Azure region. Alternatively, you can omit the node VM size parameter to use the default VM size.

To allow an AKS cluster to interact with other Azure resources, the Azure platform automatically creates a cluster identity. In this example, the cluster identity is [granted the right to pull images](cluster-container-registry-integration) from the ACR instance you created in the previous tutorial. To execute the command successfully, you must have an **Owner** or **Azure account administrator** role in your Azure subscription.

Create an AKS cluster using the

command. The following example creates a cluster named`az aks create`

*myAKSCluster*in the resource group named*myResourceGroup*. This resource group was created in the[previous tutorial](tutorial-kubernetes-prepare-acr)in the*westus2*region. We'll continue to use the environment variable,`$ACRNAME`

, that we set in the[previous tutorial](tutorial-kubernetes-prepare-acr). If you don't have this environment variable set, set it now to the same value you used previously.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --node-vm-size standard_l8s_v3 \ --generate-ssh-keys \ --attach-acr $ACRNAME`

Note

If you already generated SSH keys, you might encounter an error similar to

`linuxProfile.ssh.publicKeys.keyData is invalid`

. To proceed, retry the command without the`--generate-ssh-keys`

parameter.

To avoid needing an **Owner** or **Azure account administrator** role, you can also manually configure a service principal to pull images from ACR. For more information, see [ACR authentication with service principals](/en-us/azure/container-registry/container-registry-auth-service-principal) or [Authenticate from Kubernetes with a pull secret](/en-us/azure/container-registry/container-registry-auth-kubernetes). Alternatively, you can use a [managed identity](use-managed-identity) instead of a service principal for easier management.

## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the AKS cluster named`az aks get-credentials`

*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify connection to your cluster using the

command, which returns a list of cluster nodes.`kubectl get nodes`

`kubectl get nodes`

The following example output shows a list of the cluster nodes:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-19366578-vmss000000 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000001 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000002 Ready agent 47h v1.30.9`


## Next step

In this tutorial, you deployed a Kubernetes cluster in AKS and configured `kubectl`

to connect to the cluster. You learned how to:

- Deploy an AKS cluster that can authenticate to an ACR.
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

In the next tutorial, you learn how to deploy Azure Container Storage on your cluster and create a generic ephemeral volume. If you're using Azure Developer CLI, or if you weren't able to use a storage optimized VM type due to quota issues, proceed directly to the [Deploy containerized application](tutorial-kubernetes-deploy-application) tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-security -->

# Security concepts for applications and clusters in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container security protects the entire end-to-end pipeline from build to the application workloads running in Azure Kubernetes Service (AKS).

The Secure Supply Chain includes the build environment and registry.

Kubernetes includes security components, such as *pod security standards* and *Secrets*. Azure includes components like Active Directory, Microsoft Defender for Containers, Azure Policy, Azure Key Vault, network security groups, and orchestrated cluster upgrades. AKS combines these security components to:

- Provide a complete authentication and authorization story.
- Apply AKS Built-in Azure Policy to secure your applications.
- End-to-End insight from build through your application with Microsoft Defender for Containers.
- Keep your AKS cluster running the latest OS security updates and Kubernetes releases.
- Provide secure pod traffic and access to sensitive credentials.

This article introduces the core concepts that secure your applications in AKS.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Build Security

As the entry point for the Supply Chain, it's important to conduct static analysis of image builds before they're promoted down the pipeline. This includes vulnerability and compliance assessment. It's not about failing a build because it has a vulnerability, as that breaks development. It's about looking at the **Vendor Status** to segment based on vulnerabilities that are actionable by the development teams. Also use **Grace Periods** to allow developers time to remediate identified issues.

## Registry Security

Assessing the vulnerability state of the image in the Registry detects drift and also catches images that didn't come from your build environment. Use [Notary V2](https://github.com/notaryproject/notaryproject) to attach signatures to your images to ensure deployments are coming from a trusted location.

## Cluster security

In AKS, the Kubernetes master components are part of the managed service provided, managed, and maintained by Microsoft. Each AKS cluster has its own single-tenanted, dedicated Kubernetes master to provide the API Server, Scheduler, etc. For more information, see [Vulnerability management for Azure Kubernetes Service](concepts-vulnerability-management).

By default, the Kubernetes API server uses a public IP address and a fully qualified domain name (FQDN). You can limit access to the API server endpoint using [authorized IP ranges](api-server-authorized-ip-ranges). You can also create a fully [private cluster](private-clusters) to limit API server access to your virtual network.

You can control access to the API server using Kubernetes role-based access control (Kubernetes RBAC) and Azure RBAC. For more information, see [Microsoft Entra integration with AKS](managed-azure-ad).

## Node security

AKS nodes are Azure virtual machines (VMs) that you manage and maintain.

- Linux nodes run optimized versions of Ubuntu or Azure Linux.
- Windows Server nodes run an optimized Windows Server release using the
`containerd`

container runtime.

When an AKS cluster is created or scaled up, the nodes are automatically deployed with the latest OS security updates and configurations.

Note

AKS clusters running:

- Kubernetes version 1.19 and higher - Linux node pools use
`containerd`

as its container runtime. Windows Server 2019 and Windows Server 2022 node pools use`containerd`

as its container runtime. For more information, see[Add a Windows Server node pool with](create-node-pools).`containerd`

- Kubernetes version 1.19 and earlier - Linux node pools use Docker as its container runtime.

For more information about the security upgrade process for Linux and Windows worker nodes, see [Security patching nodes](concepts-vulnerability-management#worker-nodes).

AKS clusters running Azure Generation 2 VMs include support for [Trusted Launch](use-trusted-launch). This feature protects against advanced and persistent attack techniques by combining technologies that you can enable independently, like secure boot and a virtualized version of the trusted platform module (vTPM). Administrators can deploy AKS worker nodes with verified and signed bootloaders, OS kernels, and drivers to ensure integrity of the entire boot chain of the underlying VM.

### Container and security optimized OS options

AKS released support for two new optimized Linux OS options. [Azure Linux OS Guard (preview)](https://aka.ms/aks/azure-linux-os-guard) is Microsoft-created and optimized for Azure. OS Guard is built on top of Azure Linux with specialized configuration to support containerized workloads with security optimizations. [Flatcar Container Linux for AKS (preview)](https://aka.ms/aks/flatcar) is a CNCF-based vendor-neutral container-optimized immutable OS, best suited for running on multicloud and on-premises environments. These OS options provide increased security when compared to other Linux OS options, such as:

- Both Azure Linux OS Guard and Flatcar Container Linux for AKS have an immutable operating system that you can't modify at runtime. All OS binaries, libraries and static configuration are read-only, and the bit-for-bit integrity is often cryptographically protected. These special purpose operating systems ship as self-contained images and come without any kind of package management or other traditional means of altering the OS. User workloads run in isolated environments like containers, sandboxed from the OS.
- Both Azure Linux OS Guard and Flatcar Container Linux for AKS use SELinux for Mandatory Access Control.
- Azure Linux OS Guard enforces
[FIPS](enable-fips-nodes)and[Trusted Launch](use-trusted-launch)enablement, providing improved compliance and protection against advanced and persistent attacks by combining secure boot and virtualized version of trusted platform module (vTPM).

When deciding between which container-optimized OS options to use, AKS recommends the following:

- Use
if you're looking for a vendor neutral immutable OS with cross-cloud support.**Flatcar Container Linux for AKS (preview)** - Use
if you're looking for an enterprise-ready immutable OS, recommended by Microsoft.**Azure Linux OS Guard (preview)** - Use
[Ubuntu](https://aka.ms/aks/supported-ubuntu-versions)if you're looking for a vendor neutral, general purpose OS with cross-cloud support. - Use
[Azure Linux](https://aka.ms/aks/use-azure-linux)if you're looking for an enterprise-ready, general purpose OS, recommended by Microsoft.


### Node authorization

Node authorization is a special-purpose authorization mode that specifically authorizes kubelet API requests to protect against East-West attacks. Node authorization is enabled by default on AKS 1.24 + clusters.

### Node deployment

Nodes are deployed onto a private virtual network subnet, with no public IP addresses assigned. For troubleshooting and management purposes, SSH is enabled by default and only accessible using the internal IP address. Disabling SSH during cluster and node pool creation, or for an existing cluster or node pool, is in preview. See [Manage SSH access](manage-ssh-node-access) for more information.

### Node storage

To provide storage, the nodes use Azure Managed Disks. For most VM node sizes, Azure Managed Disks are Premium disks backed by high-performance SSDs. The data stored on managed disks is automatically encrypted at rest within the Azure platform. To improve redundancy, Azure Managed Disks are securely replicated within the Azure datacenter.

### Hostile multitenant workloads

Currently, Kubernetes environments aren't safe for hostile multitenant usage. Extra security features, like *Pod Security Policies* or Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters. For more information on ways to isolate workloads, see [Best practices for cluster isolation in AKS](operator-best-practices-cluster-isolation).

### Compute isolation

Because of compliance or regulatory requirements, certain workloads may require a high degree of isolation from other customer workloads. For these workloads, Azure provides:

[Kernel isolated containers](/en-us/azure/confidential-computing/confidential-containers)to use as the agent nodes in an AKS cluster. These containers are completely isolated to a specific hardware type and isolated from the Azure Host fabric, the host operating system, and the hypervisor. They're dedicated to a single customer. Select[one of the isolated VMs sizes](/en-us/azure/virtual-machines/isolation)as the**node size**when creating an AKS cluster or adding a node pool.[Confidential Containers](confidential-containers-overview)(preview), also based on Kata Confidential Containers, encrypts container memory and prevents data in memory during computation from being in clear text, readable format, and tampering. It helps isolate your containers from other container groups/pods, and VM node OS kernel. Confidential Containers (preview) uses hardware based memory encryption (SEV-SNP).[Pod Sandboxing](use-pod-sandboxing)(preview) provides an isolation boundary between the container application and the shared kernel and compute resources (CPU, memory, and network) of the container host.

## Network security

For connectivity and security with on-premises networks, you can deploy your AKS cluster into existing Azure virtual network subnets. These virtual networks connect back to your on-premises network using Azure Site-to-Site VPN or Express Route. Define Kubernetes ingress controllers with private, internal IP addresses to limit services access to the internal network connection.

### Azure network security groups

To filter virtual network traffic flow, Azure uses network security group rules. These rules define the source and destination IP ranges, ports, and protocols allowed or denied access to resources. Default rules are created to allow TLS traffic to the Kubernetes API server. You create services with load balancers, port mappings, or ingress routes. AKS automatically modifies the network security group for traffic flow.

If you provide your own subnet for your AKS cluster (whether using Azure CNI or Kubenet), **do not** modify the NIC-level network security group managed by AKS. Instead, create more subnet-level network security groups to modify the flow of traffic. Make sure they don't interfere with necessary traffic managing the cluster, such as load balancer access, communication with the control plane, or [egress](limit-egress-traffic).

### Kubernetes network policy

To limit network traffic between pods in your cluster, AKS offers support for [Kubernetes network policies](use-network-policies). With network policies, you can allow or deny specific network paths within the cluster based on namespaces and label selectors.

## Application Security

To protect pods running on AKS, consider [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) to detect and restrict cyber attacks against your applications running in your pods. Run continual scanning to detect drift in the vulnerability state of your application and implement a "blue/green/canary" process to patch and replace the vulnerable images.

## Secure container access to resources

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access. Built-in Linux security features such as *AppArmor* and *seccomp* are recommended as [best practices](/en-us/azure/aks/operator-best-practices-cluster-security) to [secure container access to resources][secure-container-access].

## Kubernetes Secrets

With a Kubernetes *Secret*, you inject sensitive data into pods, such as access credentials or keys.

- Create a Secret using the Kubernetes API.
- Define your pod or deployment and request a specific Secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The Secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a Secret, the Secret is deleted from the node's
*tmpfs*.- Secrets are stored within a given namespace and are only accessible from pods within the same namespace.


Using Secrets reduces the sensitive information defined in the pod or service YAML manifest. Instead, you request the Secret stored in Kubernetes API Server as part of your YAML manifest. This approach only provides the specific pod access to the Secret.

Note

The raw secret manifest files contain the secret data in base64 format. For more information, see the [official documentation](https://kubernetes.io/docs/concepts/configuration/secret/#risks). Treat these files as sensitive information, and never commit them to source control.

Kubernetes secrets are stored in *etcd*, a distributed key-value store. AKS allows [encryption at rest of secrets in etcd using customer managed keys](use-kms-etcd-encryption).

## Next steps

To get started with securing your AKS clusters, see [Upgrade an AKS cluster](upgrade-cluster).

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

For more information on core Kubernetes and AKS concepts, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deployment-safeguards -->

# Use Deployment Safeguards to enforce best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Deployment Safeguards to enforce best practices on an Azure Kubernetes Service (AKS) cluster.

## Overview

Note

Deployment Safeguards is turned on by default in AKS Automatic.

Throughout the development lifecycle, it is common for bugs, issues, and other problems to arise if the initial deployment of your Kubernetes resources includes misconfigurations. To ease the burden of Kubernetes development, Azure Kubernetes Service (AKS) offers Deployment Safeguards. Deployment Safeguards enforce Kubernetes best practices in your AKS cluster through Azure Policy controls.

Deployment Safeguards offer two levels of configuration:

`Warn`

: Displays warning messages in the code terminal to alert you of any noncompliant cluster configurations but still allows the request to go through.`Enforce`

: Enforces compliant configurations by denying and mutating deployments if they don't follow best practices.

After you configure Deployment Safeguards for 'Warn' or 'Enforce', Deployment Safeguards programmatically assess your Kubernetes resources at creation or update time for compliance. Deployment Safeguards also display aggregated compliance information across your workloads at a per resource level via Azure Policy's compliance dashboard in the [Azure portal](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Compliance) or in your CLI or terminal. Running a noncompliant workload indicates that your cluster is not following best practices and that workloads on your cluster are at risk of experiencing issues caused by your cluster configuration.

## Prerequisites

Note

Cluster admins don't need Azure Policy permissions to enable or disable Deployment Safeguards. However, it's required to have the Azure Policy add-on installed.

- You need to enable the Azure Policy add-on for AKS. For more information, see
[Enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks). This includes registering the`Microsoft.PolicyInsights`

resource provider in your subscription.

## Deployment Safeguards policies

The following table lists the policies that become active and the Kubernetes resources they target when you enable Deployment Safeguards. You can view the [currently available Deployment Safeguards](https://portal.azure.com/#view/Microsoft_Azure_Policy/InitiativeDetail.ReactView/id/%2Fproviders%2FMicrosoft.Authorization%2FpolicySetDefinitions%2Fc047ea8e-9c78-49b2-958b-37e56d291a44/scopes/) in the Azure portal as an Azure Policy definition or at [Azure Policy built-in definitions for Azure Kubernetes Service](/en-us/azure/aks/policy-reference#policy-definitions). The intention behind this collection is to create a common and generic list of best practices applicable to most users and use cases.

| Deployment safeguard policy | Mutation outcome if available |
|---|---|
| Cannot Edit Individual Nodes | N/A |
| Kubernetes cluster containers CPU and memory resource limits shouldn't exceed the specified limits | Sets CPU resource limits to 500m if not set and sets memory limits to 500Mi if no path is present |
| Must Have Anti Affinity Rules or topologySpreadConstraintsSet | N/A |
| No AKS Specific Labels | N/A |
| Kubernetes cluster containers should only use allowed images | N/A |
| Reserved System Pool Taints | Removes the `CriticalAddonsOnly` taint from a user node pool if not set. AKS uses the `CriticalAddonsOnly` taint to keep customer pods away from the system pool. This configuration ensures a clear separation between AKS components and customer pods and prevents eviction of customer pods that don't tolerate the `CriticalAddonsOnly` taint. |
| Ensure cluster containers have readiness or liveness probes configured | N/A |
| Kubernetes clusters should use Container Storage Interface (CSI) driver StorageClass | N/A |
| Kubernetes cluster services should use unique selectors | N/A |
| Kubernetes cluster container images should not include latest image tag | N/A |

If you want to submit an idea or request for Deployment Safeguards, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

## Pod Security Standards in Deployment Safeguards

Note

Baseline Pod Security Standards are now turned on by default in AKS Automatic. The baseline Pod Security Standards in AKS Automatic can't be turned off.

Deployment Safeguards also supports the ability to turn on [Baseline, Restricted and Privileged Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/). To ensure your workloads deploy successfully, make sure each manifest complies with the Baseline or Restricted Pod Security requirements. By default, Azure Kubernetes Service uses Privileged Pod Security Standards.

| Policy | Error Message | Fix |
|---|---|---|
| AppArmor | `AppArmor annotation values must be undefined/nil, runtime/default, or localhost/*` or `AppArmor profile type must be one of: undefined/nil, RuntimeDefault, or Localhost` |
Remove any specification of AppArmor. Kubernetes by default applies apparmor settings. "On supported hosts, the RuntimeDefault AppArmor profile is applied by default". |
| Host Namespaces | `Host network namespaces are disallowed: spec.hostNetwork is set to true'` or `'Host PID namespaces are disallowed: spec.hostPID is set to true'` or `'Host IPC namespaces are disallowed: spec.hostIPC is set to true'` |
Set those values to false, or remove specifying the fields. |
| Privileged Containers | `'Privileged [ephemeral\|init\|N/A] containers are disallowed: spec.containers[*].securityContext.privileged is set to true'` |
Set the appropriate securityContext.privileged field to false, or remove the field. |
| Capabilities | Message will start with `'Disallowed capabilities detected` |
Remove the capability shown from the container's manifest. |
| HostPath volumes | `HostPath volumes are forbidden under restricted security policy unless containers mounting them are from allowed images` |
Remove the HostPath volume and volume mount. |
| Host Ports | HostPorts are forbidden under baseline security policy | Remove the host port specification from the offending container. |
| SELinux | `SELinux type must be one of: undefined/empty, container_t, container_init_t, container_kvm_t, or container_engine_t` |
Set the container's securityContext.seLinuxOptions.type field to one of the allowed values. |
| /proc Mount Type | ProcMount must be undefined/nil or 'Default' in spec.containers[*].securityContext.procMount | Set "* `spec.containers[*].securityContext.procMount` " to 'Default' or have it be undefined. |
| Seccomp | `Seccomp profile must not be explicitly set to Unconfined. Allowed values are: undefined/nil, RuntimeDefault, or Localhost` |
Set `securityContext.seccompProfile.type` on the pod or containers to one of the allowed values. |
| Sysctls | `Disallowed sysctl detected. Only baseline Kubernetes pod security standard sysctls are permitted` |
Remove the disallowed systctls( see the
|

`Only the following volume types are allowed under restricted policy: configMap, csi, downwardAPI, emptyDir, ephemeral, persistentVolumeClaim, projected, secret`

`Privilege escalation must be set to false under restricted policy`

`* `

spec.containers[*].securityContext.allowPrivilegeEscalation`` must explicitly be set to false for each container, initContainer, and ephemeralContainer.`Containers must not run as root user in spec.containers[*].securityContext.runAsNonRoot`

`'Containers must not run as root user: spec.securityContext.runAsUser is set to 0'`

`Seccomp profile must be "RuntimeDefault" or "Localhost" under restricted policy`

`securityContext.seccompProfile.type`

on the pod or containers to one of the allowed values. This differs from the baseline in the fact that the restricted policy doesn't allow an undefined value.`All containers must drop ALL capabilities under restricted policy`

or `Only NET_BIND_SERVICE may be added to capabilities under restricted policy`

## Enable Deployment Safeguards

Note

Using the Deployment Safeguards `Enforce`

level means you're opting in to deployments being blocked and mutated. Consider how these policies might work with your AKS cluster before enabling `Enforce`

.

### Enable Deployment Safeguards on an existing cluster

Enable Deployment Safeguards on an existing cluster that has the Azure Policy add-on enabled using the `az aks safeguard create`

command with the `--level`

flag. If you want to receive noncompliance warnings, set the `--level`

to `Warn`

. If you want to deny or mutate all noncompliant deployments, set it to `Enforce`

.

```
az aks safeguards create --resource-group <resource-group-name> --name <cluster-name> --level Enforce
```


You can also enable Deployment Safeguards by using the `--cluster`

flag and specifying the cluster resource ID.

```
az aks safeguards create --cluster <ID> --level Enforce
```


If you want to update the Deployment Safeguards level of an existing cluster, run the following command with the new value for `--level`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn
```


### Excluding namespaces

You can also exclude certain namespaces from Deployment Safeguards. When you exclude a namespace, activity in that namespace is unaffected by Deployment Safeguards warnings or enforcement.

For example, to exclude the namespaces `ns1`

and `ns2`

, use a space separated list of namespaces with the `--excluded-ns`

flag, as shown in the following example:

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --excluded-ns ns1 ns2
```


### Turn on Pod Security Standards

Note

Azure Kubernetes Service (AKS) uses `Privileged`

Pod Security Standards by default. If you want to revert to the default configuration, set the `--pss-level`

flag to `Privileged`

.

To enable Pod Security Standards in Deployment Safeguards, use the `--pss-level`

flag to select one of the following levels: `Baseline`

, `Restricted`

, or `Privileged`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --pss-level <Baseline|Restricted|Privileged>
```


### Update your Deployment Safeguard version

Deployment Safeguards adhere to the [AKS addon versioning scheme](supported-kubernetes-versions). Each new version of a Deployment Safeguard will be released as a new minor version in AKS. These updates will be communicated through the [AKS GitHub release notes](https://github.com/Azure/AKS/releases) and reflected in the "Deployment Safeguards Policies" table in our documentation.

To learn more about AKS versioning and addons, refer to the following documentation: [aks-component-versions](supported-kubernetes-versions) and [aks-versioning-for-addons](integrations#add-ons).

## Verify compliance across clusters

After deploying your Kubernetes manifest, you see warnings or a potential denial message in your CLI or terminal if the cluster isn't compliant with Deployment Safeguards, as shown in the following examples:

**Warn**

```
$ kubectl apply -f deployment.yaml
Warning: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
deployment.apps/simple-web created
```


**Enforce**

With Deployment Safeguard mutations, the `Enforce`

level mutates your Kubernetes resources when applicable. However, your Kubernetes resources still need to pass all safeguards to deploy successfully. If any safeguard policies fail, your resource is denied and won't be deployed.

```
$ kubectl apply -f deployment.yaml
Error from server (Forbidden): error when creating "deployment.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
```


If your Kubernetes resources comply with the applicable mutation safeguards and meet all other safeguard requirements, they'll be successfully deployed, as shown in the following example:

```
$ kubectl apply -f deployment.yaml
deployment.apps/simple-web created
```


## Verify compliance across clusters using the Azure Policy dashboard

To verify Deployment Safeguards have been applied and to check on your cluster's compliance, navigate to the Azure portal page for your cluster and select **Policies**, then select **go to Azure Policy**.

From the list of policies and initiatives, select the initiative associated with Deployment Safeguards. You see a dashboard showing compliance state across your AKS cluster.

Note

To properly assess compliance across your AKS cluster, the Azure Policy initiative must be scoped to your cluster's resource group.

## Disable Deployment Safeguards

To disable Deployment Safeguards on your cluster, use the `delete`

command.

```
az aks safeguards delete --resource-group <resource-group-name> --name <cluster-name>
```


## FAQ

#### Can I create my own mutations?

No. If you have an idea for a safeguard, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

#### Can I pick and choose which mutations I want in Enforcement?

No. Deployment Safeguards is all or nothing. Once you turn on Warn or Enforce, all safeguards are active.

#### Why did my deployment resource get admitted even though it wasn't following best practices?

Deployment Safeguards enforce best practice standards through Azure Policy controls and has policies that validate against Kubernetes resources. To evaluate and enforce cluster components, Azure Policy extends [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/). Gatekeeper enforcement also currently operates in a [ fail-open model](https://open-policy-agent.github.io/gatekeeper/website/docs/failing-closed/#considerations). As there's no guarantee that Gatekeeper responds to our networking call, we make sure that in that case, the validation is skipped so that the deny doesn't block your deployments.

To learn more, see [workload validation in Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/workload-resources/).

## Next steps

- Learn more about
[best practices](best-practices)for operating an AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-custom -->

# Customize CoreDNS for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses [CoreDNS](https://coredns.io/) for cluster DNS management and resolution with all *1.12.x* and higher clusters. AKS is a managed service, so you can't modify the main configuration for CoreDNS (a *CoreFile*). Instead, you use a Kubernetes *ConfigMap* to override the default settings. To see the default AKS CoreDNS ConfigMaps, use the `kubectl get configmaps --namespace=kube-system coredns --output yaml`

command.

This article shows you how to use ConfigMaps for basic CoreDNS customization options in Azure Kubernetes Service (AKS).

Note

Previously, AKS used `kube-dns`

for cluster DNS management and resolution, but it's now deprecated. `kube-dns`

offered different [customization options](https://www.danielstechblog.io/using-custom-dns-server-for-domain-specific-name-resolution-with-azure-kubernetes-service/) via a Kubernetes config map. CoreDNS is **not** backwards compatible with `kube-dns`

. You must update any previous customizations to work with CoreDNS.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Verify the version of CoreDNS you're running. The configuration values might change between versions.

## Plugin support

All built-in CoreDNS plugins are supported. No add-on/third party plugins are supported.

Important

When you create configurations like the ones in this article, the names you specify in the `data`

section must end in `.server`

or `.override`

. This naming convention is defined in the default AKS CoreDNS ConfigMap, which you can view using the `kubectl get configmaps --namespace=kube-system coredns --output yaml`

command.

## Configure DNS name rewrites

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to replace`<domain to be rewritten>`

with your own fully qualified domain name (FQDN).`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | <domain to be rewritten>.com:53 { log errors rewrite stop { name regex (.*)\.<domain to be rewritten>\.com {1}.default.svc.cluster.local answer name (.*)\.default\.svc\.cluster\.local {1}.<domain to be rewritten>.com } forward . /etc/resolv.conf # You can redirect this to a specific DNS server such as 10.0.0.10, but that server must be able to resolve the rewritten domain name }`

Important

If you redirect to a DNS server, such as the CoreDNS service IP, that DNS server must be able to resolve the rewritten domain name.

Create the ConfigMap using the

command and specify the name of your YAML manifest.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Verify the customizations were applied using the

command.`kubectl get configmaps`

`kubectl get configmaps --namespace=kube-system coredns-custom -o yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Specify a forward server for your network traffic

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to replace the`forward`

name and`<domain to be rewritten>`

with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | # You can select any name here, but it must end with the .server file extension <domain to be rewritten>.com:53 { forward foo.com 1.1.1.1 }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Use custom domains

You might want to configure custom domains that can only be resolved internally. For example, you might want to resolve the custom domain *puglife.local*, which isn't a valid top-level domain. Without a custom domain ConfigMap, the AKS cluster can't resolve the address.

Create a new file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to update the custom domain and IP address with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: puglife.server: | # You can select any name here, but it must end with the .server file extension puglife.local:53 { errors cache 30 forward . 192.11.0.1 # This is my test/dev DNS server }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Configure stub domains

Create a file named

`corednsms.yaml`

and paste the following example configuration. Make sure to update the custom domains and IP addresses with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | # You can select any name here, but it must end with the .server file extension abc.com:53 { errors cache 30 forward . 1.2.3.4 } my.cluster.local:53 { errors cache 30 forward . 2.3.4.5 }`

Create the ConfigMap using the

command and specify.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Add custom host-to-IP mappings

Create a file named

`corednsms.yaml`

and paste the following example configuration. Make sure to update the IP addresses and hostnames with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom # This is the name of the ConfigMap you can overwrite with your changes namespace: kube-system data: test.override: | # You can select any name here, but it must end with the .override file extension hosts { 10.0.0.1 example1.org 10.0.0.2 example2.org 10.0.0.3 example3.org fallthrough }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Next steps

- To troubleshoot CoreDNS issues, see
[Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)](coredns-troubleshoot). - To learn about CoreDNS autoscaling behavior, see
[Autoscaling CoreDNS in Azure Kubernetes Service (AKS)](coredns-autoscale).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/load-balancer-standard -->

# Use a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Load Balancer](/en-us/azure/load-balancer/load-balancer-overview) operates at layer 4 of the Open Systems Interconnection (OSI) model that supports both inbound and outbound scenarios. It distributes inbound flows that arrive at the load balancer's front end to the back end pool instances.

A **public** load balancer integrated with AKS serves two purposes:

- Provide outbound connections to the cluster nodes inside the AKS virtual network (VNet) by translating the private IP address to a public IP address part of its
*outbound pool*. - Provide access to applications via Kubernetes services of type
`LoadBalancer`

, enabling you to easily scale your applications and create highly available services.

This article covers integration with a public load balancer on AKS. For internal load balancer integration, see [Use an internal load balancer in AKS](internal-lb).

## Prerequisites

- Azure Load Balancer is available in two SKUs:
*Basic*and*Standard*. The*Standard*SKU is used by default when you create an AKS cluster. The*Standard*SKU gives you access to added functionality, such as a larger backend pool,[multiple node pools](create-node-pools),[Availability Zones](availability-zones), and is[secure by default](/en-us/azure/load-balancer/load-balancer-overview#securebydefault). It's the recommended load balancer SKU for AKS. For more information on the*Basic*and*Standard*SKUs, see[Azure Load Balancer SKU comparison](/en-us/azure/load-balancer/skus). - For a full list of the supported annotations for Kubernetes services with type
`LoadBalancer`

, see[LoadBalancer annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations). - This article assumes you have an AKS cluster with the
*Standard*SKU Azure Load Balancer. If you need an AKS cluster, you can create one using[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal).

Important

If you'd prefer to use your own gateway, firewall, or proxy to provide outbound connection, you can skip the creation of the load balancer outbound pool and respective frontend IP by using [ outbound type as UserDefinedRouting (UDR)](egress-outboundtype). The outbound type defines the egress method for a cluster and defaults to type

`LoadBalancer`

.## Limitations

The following limitations apply when you create and manage AKS clusters that support a load balancer with the *Standard* SKU:

AKS manages the lifecycle and operations of agent nodes. Modifying the IaaS resources associated with the agent nodes isn't supported. An example of an unsupported operation is making manual changes to the load balancer resource group.

At least one public IP or IP prefix is required for allowing egress traffic from the AKS cluster. The public IP or IP prefix is required to maintain connectivity between the control plane and agent nodes and to maintain compatibility with previous versions of AKS. You have the following options for specifying public IPs or IP prefixes with a

*Standard*SKU load balancer:- Provide your own public IPs.
- Provide your own public IP prefixes.
- Specify a number up to 100 to allow the AKS cluster to create that many
*Standard*SKU public IPs in the same resource group as the AKS cluster. This resource group is usually named with`MC_`

at the beginning. AKS assigns the public IP to the*Standard*SKU load balancer. By default, one public IP is automatically created in the same resource group as the AKS cluster if no public IP, public IP prefix, or number of IPs is specified. You also must allow public addresses and avoid creating any Azure policies that ban IP creation.

A public IP created by AKS can't be reused as a custom bring your own (BYO) public IP address. You must create and manage all custom IP addresses.

You can only define the load balancer SKU when you create an AKS cluster. You can't change the load balancer SKU after an AKS cluster has been created.

You can only use one type of load balancer SKU (

*Basic*or*Standard*) in a single cluster.*Standard*SKU load balancers only support*Standard*SKU IP addresses.[Private Link Service](/en-us/azure/private-link/private-link-service-overview)isn't supported when the load balancer backend pool type is set to`nodeIP`

.

## Create a load balancer service in AKS

After you create an AKS cluster with outbound type `LoadBalancer`

(default), your cluster is ready to use the load balancer to expose services.

Create a service manifest named

`public-svc.yaml`

, which creates a public service of type`LoadBalancer`

.`apiVersion: v1 kind: Service metadata: name: public-svc spec: type: LoadBalancer ports: - port: 80 selector: app: public-app`


## Specify the load balancer IP address

If you want to use a specific IP address with the load balancer, you have two options to specify the IP address:

**Set service annotations**(recommended): Use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.**Add the**: Add the*LoadBalancerIP*property to the load balancer YAML manifest`Service.Spec.LoadBalancerIP`

property to the load balancer YAML manifest. This field is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235), and it can't support dual-stack. Current usage remains the same and existing services are expected to work without modification.

## Deploy the load balancer service manifest

Deploy the public service manifest using

and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f public-svc.yaml`

The Azure Load Balancer is configured with a new public IP that fronts the new service. Since the Azure Load Balancer can have multiple frontend IPs, each new service that you deploy gets a new dedicated frontend IP to be uniquely accessed.

Confirm your service is created and the load balancer is configured using the

`kubectl get service`

command.`kubectl get service public-svc`

When you view the service details, the public IP address created for this service on the load balancer is shown in the

*EXTERNAL-IP*column of the output. It might take a few minutes for the IP address to change from*<pending>*to an actual public IP address. The following example output shows successful creation of the service:`NAMESPACE NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE default public-svc LoadBalancer 10.0.39.110 203.0.113.187 80:32068/TCP 52s`

Get more detailed information about your service using the

`kubectl describe service`

command.`kubectl describe service public-svc`

The following example output is a condensed version of the output after you run

`kubectl describe service`

.*LoadBalancer Ingress*shows the external IP address exposed by your service.*IP*shows the internal addresses.`Name: public-svc Namespace: default Labels: <none> Annotations: <none> Selector: app=public-app ... IP: 10.0.39.110 ... LoadBalancer Ingress: 203.0.113.187 ... TargetPort: 80/TCP NodePort: 32068/TCP ... Session Affinity: None External Traffic Policy: Cluster ...`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-os-version -->

# Upgrade operating system (OS) versions in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes OS versions available for Azure Kubernetes Service (AKS) nodes, and best practices for testing and upgrading your OS version.

Important

Starting on **March 17, 2027**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported OS versions

Each [node image](node-images) corresponds to an OS version, which you can specify using OS SKU. You can specify the following parameters when creating clusters and node pools:

**--os-type**: OS type, including Linux or Windows.*You can't specify the Windows OS type during cluster creation or update.***--os-sku**: Used to specify OS version or OS variant.*You can't specify the Windows OS SKU during cluster creation or update.*For more information for supported OS SKU options, see[Azure AKS CLI](/en-us/cli/azure/aks#az-aks-create)or[API](/en-us/rest/api/aks/agent-pools/create-or-update#ossku).**--kubernetes-version**: Version of Kubernetes to use for creating the node pool or cluster.


Best practice guidanceThe default OS version is the most recent validated version.


- For Ubuntu, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku Ubuntu`

. This will automatically update you to the latest default Ubuntu version based on your Kubernetes version.- For Azure Linux, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku AzureLinux`

. This will automatically update you to the latest default Azure Linux version based on your Kubernetes version.- For Windows, we recommend creating node pools while specifying
`--os-type Windows`

and`--os-sku Windows2022`

. You need to manually update node pools to the next OS version when it's released.

| OS type | OS SKU | Supported Kubernetes versions | Default versioning |
|---|---|---|---|
| Linux | Ubuntu | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Ubuntu 22.04 is default for Kubernetes versions 1.25 to 1.34. Ubuntu 24.04 is default for Kubernetes versions 1.35+. |
| Linux | Ubuntu2404 | This OS SKU will only be supported in Kubernetes 1.32 to 1.38. | We recommend this versioned OS SKU if you want to migrate to the new OS version without upgrading your Kubernetes version. Ubuntu 24.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.35+. |
| Linux | Ubuntu2204 | This OS SKU is supported in Kubernetes versions 1.25 to 1.36. | We recommend this versioned OS SKU if you need to roll back to Ubuntu 22.04. Ubuntu 22.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.25 to 1.35. |
| Linux | AzureLinux | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Azure Linux 2.0 is default for Kubernetes version 1.27 to 1.31. Azure Linux 3.0 is default for Kubernetes version 1.32+. When the `AzureLinuxV3Preview` feature flag is enabled on AKS 1.31, `--os-sku AzureLinux` defaults to 3.0. |
| Linux | AzureLinux3 | This OS SKU is supported in Kubernetes 1.28 to 1.36. | We recommend this OS SKU if you want to test out the new OS version without upgrading your Kubernetes version. You can also use this OS SKU to migrate from Azure Linux 2.0 to Azure Linux 3.0. |
| Linux | AzureLinuxOSGuard | This OS SKU is supported in Kubernetes versions 1.32 and above. | Azure Linux with OS Guard versions are upgraded through node image upgrades. For more information, see
|

[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).## Migrate to a new OS version

When a new OS version releases on AKS, it's initially supported in preview. After testing in preview for a few months, AKS makes the new OS version generally available (GA) and then updates the default OS SKU (`Ubuntu`

or `AzureLinux`

) to the latest GA OS version. This default update occurs with a new Kubernetes version release.

We recommend testing your nonproduction workloads with the new OS version when it becomes available in preview. In order to access preview functions, make sure you have the preview extension installed. You can install the extension using the `az extension add --name aks-preview`

command.

There are two ways to migrate to a new OS version:

**Default OS SKU**: If you're using a default OS SKU such as`Ubuntu`

or`AzureLinux`

, you automatically get the latest GA version when you[upgrade your Kubernetes version](manage-node-pools). There are no manual changes required to migrate to a new OS version.**Versioned OS SKU**: If you're using a versioned OS SKU such as`Ubuntu2404`

,`AzureLinux3`

, or`Windows2025`

, you need to manually migrate to a new OS version to avoid blocked Kubernetes upgrades. If you're using a Linux OS, you can update the OS SKU on an existing node pool to manually migrate.

### Update OS SKU on an existing node pool

Update the `os-sku`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. In cases where there's a new OS version available in preview, this functionality allows you to migrate your node pool to the new OS version without needing to upgrade your Kubernetes version.

Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Migrate to Ubuntu 24.04

Ubuntu 24.04 is the default for `--os-sku Ubuntu`

in Kubernetes versions 1.35+. You can also use Ubuntu 24.04 by specifying `--os-sku Ubuntu2404`

.

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2404`

:

[FIPS](enable-fips-nodes)is not supported.- Ubuntu 24.04 is supported in Kubernetes versions 1.32 to 1.38.
- You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.39+.
`--os-sku Ubuntu2404`

is an option and is intended for testing the new OS Linux version without requiring you to upgrade your Kubernetes version. - You need the preview Azure CLI version 18.0.0b5 or later for
*preview*and version 2.82.0 for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku Ubuntu2404`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2404 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


#### Migrate to Azure Linux 3.0

Azure Linux 3.0 is the default for `--os-sku AzureLinux`

in Kubernetes versions 1.32 to 1.36. You can also use Azure Linux 3.0 by specifying `--os-sku AzureLinux3`

.

Note

Keep the following information in mind when migrating to `--os-sku AzureLinux3`

:

`--os-sku AzureLinux3`

is supported in Kubernetes versions 1.28 to 1.36.`--os-sku AzureLinux3`

is intended for migrating to Azure Linux 3.0 without upgrading your Kubernetes version. You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.37+.- You need the Azure CLI version 18.0.0b36 or later for
*preview*and version 2.78.0 or later for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku AzureLinux3`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux3 \
--kubernetes-version 1.30.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Roll back your OS version

In Kubernetes versions where multiple OS versions are supported, you can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to roll back to a previous OS version.

You might want to roll back your OS version in the following scenarios:

- If you're testing a new OS version and you run into any issues.
- Once you upgrade to a Kubernetes version that supports the new OS version as default, you might want to roll back to the default
`Ubuntu`

or`AzureLinux`

OS SKU. This allows you to get future OS versions as a part of your Kubernetes upgrades instead of requiring a node pool update.

### Roll back your OS version to the default OS SKU

You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to update the

`os-sku`

on an existing node pool. In cases where there's a previous OS version supported in your Kubernetes version, this functionality can allow you to roll back your OS version.Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

| OS SKU | Default OS version |
|---|---|
| Ubuntu | When you have OS SKU `Ubuntu` , Ubuntu 22.04 is the default OS version if your Kubernetes version is 1.25 to 1.34. Ubuntu 24.04 is the default for Ubuntu in Kubernetes 1.35 to 1.37. |
| AzureLinux | When you have OS SKU `AzureLinux` , Azure Linux 2.0 is the default for AzureLinux in Kubernetes 1.26 to 1.31. Azure Linux 3.0 is the default for AzureLinux in Kubernetes 1.32 to 1.36. |

#### Update your OS SKU to Ubuntu on an existing node pool

When updating your node pool to use OS SKU `Ubuntu`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku Ubuntu`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Update your OS SKU to Azure Linux on an existing node pool

When updating your node pool to use OS SKU `AzureLinux`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku AzureLinux`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux \
--name $NODE_POOL_NAME \
--node-count 1
```


### Roll back to Ubuntu 22.04

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2204`

:

[FIPS](enable-fips-nodes)and[CVM](use-cvm)aren't supported.- Ubuntu 22.04 is supported in Kubernetes versions 1.25 to 1.35.
`--os-sku Ubuntu2204`

is intended for roll back to Ubuntu 22.04 on your current Kubernetes version. You need to update your OS SKU to a supported OS option to upgrade your Kubernetes version to 1.36 and above.

Roll back to `--os-sku Ubuntu2204`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2204 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler -->

# Vertical pod autoscaling in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of using the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS), which is based on the open source [Kubernetes](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler) version.

When configured, the VPA automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for other pods and helps ensure effective utilization of your AKS clusters. The Vertical Pod Autoscaler provides recommendations for resource usage over time. To manage sudden increases in resource usage, use the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler), which scales the number of pod replicas as needed.

## Benefits

The Vertical Pod Autoscaler offers the following benefits:

- Analyzes and adjusts processor and memory resources to
*right size*your applications. VPA isn't only responsible for scaling up, but also for scaling down based on their resource use over time. - A pod with a scaling mode set to
*auto*or*recreate*is evicted if it needs to change its resource requests. - You can set CPU and memory constraints for individual containers by specifying a resource policy.
- Ensures nodes have correct resources for pod scheduling.
- Offers configurable logging of any adjustments made to processor or memory resources made.
- Improves cluster resource utilization and frees up CPU and memory for other pods.

## Limitations and considerations

Consider the following limitations and considerations when using the Vertical Pod Autoscaler:

- VPA supports a maximum of 1,000 pods associated with
`VerticalPodAutoscaler`

objects per cluster. - VPA might recommend more resources than available in the cluster, which prevents the pod from being assigned to a node and run due to insufficient resources. You can overcome this limitation by setting the
*LimitRange*to the maximum available resources per namespace, which ensures pods don't ask for more resources than specified. You can also set maximum allowed resource recommendations per pod in a`VerticalPodAutoscaler`

object. The VPA can't completely overcome an insufficient node resource issue. The limit range is fixed, but the node resource usage is changed dynamically. - We don't recommend using VPA with the
[Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler), which scales based on the same CPU and memory usage metrics. - The VPA Recommender only stores up to
*eight days*of historical data. - VPA doesn't support JVM-based workloads due to limited visibility into actual memory usage of the workload.
- VPA doesn't support running your own implementation of VPA alongside it. Having an extra or customized recommender is supported.
- AKS Windows containers aren't supported.

## VPA overview

The VPA object consists of three components:

**Recommender**: The Recommender monitors current and past resource consumption, including metric history, Out of Memory (OOM) events, and VPA deployment specs, and uses the information it gathers to provide recommended values for container CPU and Memory requests/limits.**Updater**: The Updater monitors managed pods to ensure that their resource requests are set correctly. If not, it removes those pods so that their controllers can recreate them with the updated requests.**VPA Admission Controller**: The VPA Admission Controller sets the correct resource requests on new pods either created or recreated by their controller based on the Updater's activity.

### VPA admission controller

The VPA Admission Controller is a binary that registers itself as a *Mutating Admission Webhook*. When a new pod is created, the VPA Admission Controller gets a request from the API server and evaluates if there's a matching VPA configuration or finds a corresponding one and uses the current recommendation to set resource requests in the pod.

A standalone job, `overlay-vpa-cert-webhook-check`

, runs outside of the VPA Admission Controller. The `overlay-vpa-cert-webhook-check`

job creates and renews the certificates and registers the VPA Admission Controller as a `MutatingWebhookConfiguration`

.

### VPA object operation modes

A Vertical Pod Autoscaler resource, most commonly a *deployment*, is inserted for each controller that you want to have automatically computed resource requirements.

There are four modes in which the VPA operates:

`Auto`

: VPA assigns resource requests during pod creation and updates existing pods using the preferred update mechanism.`Auto`

, which is equivalent to`Recreate`

, is the default mode. Once restart-free, or*in-place*, updates of pod requests are available, it can be used as the preferred update mechanism by the`Auto`

mode. With the`Auto`

mode, VPA evicts a pod if it needs to change its resource requests. It might cause the pods to be restarted all at once, which can cause application inconsistencies. You can limit restarts and maintain consistency in this situation using a[PodDisruptionBudget](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/).`Recreate`

: VPA assigns resource requests during pod creation and updates existing pods by evicting them when the requested resources differ significantly from the new recommendations (respecting the PodDisruptionBudget, if defined). You should only use this mode if you need to ensure that the pods are restarted whenever the resource request changes. Otherwise, we recommend using`Auto`

mode, which takes advantage of restart-free updates once available.`Initial`

: VPA only assigns resource requests during pod creation. It doesn't update existing pods. This mode is useful for testing and understanding the VPA behavior without affecting the running pods.`Off`

: VPA doesn't automatically change the resource requirements of the pods. The recommendations are calculated and can be inspected in the VPA object.

## Deployment pattern for application development

If you're unfamiliar with VPA, we recommend the following deployment pattern during application development to identify its unique resource utilization characteristics, test VPA to verify it's functioning properly, and test alongside other Kubernetes components to optimize resource utilization of the cluster:

- Set
`UpdateMode = "Off"`

in your production cluster and run VPA in recommendation mode so you can test and gain familiarity with VPA.`UpdateMode = "Off"`

can avoid introducing a misconfiguration that can cause an outage. - Establish observability first by collecting actual resource utilization telemetry over a given period of time, which helps you understand the behavior and any signs of issues from container and pod resources influenced by the workloads running on them.
- Get familiar with the monitoring data to understand the performance characteristics. Based on this insight, set the desired requests/limits accordingly and then in the next deployment or upgrade.
- Set
`updateMode`

value to`Auto`

,`Recreate`

, or`Initial`

depending on your requirements.

## Next steps

To learn how to set up the Vertical Pod Autoscaler on your AKS cluster, see [Use the Vertical Pod Autoscaler in AKS](use-vertical-pod-autoscaler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/active-passive-solution -->

# Active-passive disaster recovery solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines an active-passive disaster recovery solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-passive solution overview

In this disaster recovery approach, we have two independent AKS clusters being deployed in two Azure regions. However, only one of the clusters is actively serving traffic at any one time. The secondary cluster (not actively serving traffic) contains the same configuration and application data as the primary cluster but doesn’t accept any traffic unless directed by Azure Front Door traffic manager.

## Scenarios and configurations

This solution is best implemented when hosting applications reliant on resources, such as databases, that actively serve traffic in one region. In scenarios where you need to host stateless applications deployed across both regions, such as horizontal scaling, we recommend considering an [active-active solution](active-active-solution), as active-passive involves added latency.

## Components

The active-passive disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, network traffic is routed to the primary AKS cluster set in the Azure Front Door configuration.

**Configured cluster prioritization**: You set a prioritization level between 1-5 for each cluster (with 1 being the highest priority and 5 being the lowest priority). You can set multiple clusters to the same priority level and specify the weight for each cluster. If the primary cluster becomes unavailable, traffic automatically routes to the next region selected in Azure Front Door. All traffic must go through Azure Front Door for this system to work.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to the [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance in the primary region (cluster must be marked with priority 1). In the event of a region failure, the service redirects traffic to the next cluster in the priority list.

For more information, see [Priority-based traffic-routing](/en-us/azure/frontdoor/routing-methods#priority-based-traffic-routing).

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If a service or service component becomes unavailable in one region, traffic should be routed to a region where that service is available. A multi-region architecture includes many different failure points. In this section, we cover the potential failure points.

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:
