---
merged_at: 2026-01-25T12:06:27.853687
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: control-plane-metrics-monitor.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-monitor -->

# Monitor Azure Kubernetes Service control plane metrics (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to monitor the Azure Kubernetes Service (AKS) control plane by using control plane metrics in Azure Monitor.

AKS supports a subset of control plane metrics free through [Azure Monitor platform metrics](monitor-aks#aks-monitoring-data-metrics-logs-integrations). The control plane metrics feature gives you visibility into the availability and performance of critical control plane components like the API server, etcd, the scheduler, the autoscaler, and the controller manager in AKS. The feature is also fully compatible with the managed service for Prometheus and Azure Managed Grafana. You can use these metrics to maximize overall observability and to maintain operational excellence for your AKS cluster.

## Control plane platform metrics

AKS offers some free control plane metrics for monitoring the API server and etcd. These metrics are automatically collected for all AKS clusters at no cost. You can analyze the metrics by using the [metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics) in the Azure portal. You can also create metrics-based alerts by using the metrics data.

To see the full list of supported control plane platform metrics, see the [AKS monitoring reference](monitor-aks-reference#metrics).

## Prerequisites and limitations

- The control plane metrics (preview) feature supports only the
[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor. [Azure Private Link](/en-us/azure/azure-monitor/logs/private-link-security)isn't supported.- You can customize only the default
configmap file. No other customization is supported.`ama-metrics-settings-configmap.yaml`

- Your AKS cluster must use
[managed identity authentication](use-managed-identity).

### Install the aks-preview extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the

`aks-preview`

Azure CLI extension by using theor`az extension add`

command:`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the AzureMonitorMetricsControlPlanePreview feature flag

Register the

`AzureMonitorMetricsControlPlanePreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

It takes a few minutes for the status to show as

**Registered**.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

When the status is

**Registered**, refresh the registration of the Microsoft.ContainerService resource provider by using thecommand:`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable control plane metrics on an AKS cluster

Enable control plane metrics by using the managed service for Prometheus add-on when you create a new cluster or update an existing cluster.

Note

Unlike the metrics that are collected from cluster nodes, control plane metrics are collected by a component that isn't part of the `ama-metrics`

add-on. Enabling the `AzureMonitorMetricsControlPlanePreview`

feature flag and the managed service for Prometheus add-on ensures that control plane metrics are collected. After you enable metrics collection, it can take several minutes for the data to appear in the workspace.

### New AKS cluster

To learn how to collect managed service for Prometheus metrics from your AKS cluster, see [Enable Prometheus and Grafana for AKS clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana). For an AKS cluster, complete the steps described on the **CLI** tab.

### Existing AKS cluster

If your cluster already has the managed service for Prometheus add-on, update the cluster to ensure that it collects control plane metrics by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command:

```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Query control plane metrics

Control plane metrics are stored in an Azure Monitor workspace in the cluster's region. You can query the metrics directly in the workspace or by using the Azure Managed Grafana instance that's connected to the workspace.

In the

[Azure portal](https://portal.azure.com), go to your AKS cluster resource.On the left menu, select

**Monitor**>**Monitor Settings**.Go to the Azure Monitor workspace that is linked to the cluster.

In the Azure Monitor workspace, under

**Managed Prometheus**, query the metrics by using the Prometheus explorer.

Note

AKS provides dashboard templates to help you view and analyze your control plane telemetry data in real time. If you use Azure Managed Grafana to visualize the data, you can import the following dashboards:

## Customize control plane metrics

AKS includes a preconfigured set of metrics to collect and store for each component. Metrics for the API server and etcd are collected by default. You can customize the list of metrics that are collected by modifying the [ ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) configmap file.

Default targets include the following values:

```
controlplane-apiserver = true
controlplane-cluster-autoscaler = false
controlplace-node-auto-provisioning = false
controlplane-kube-scheduler = false
controlplane-kube-controller-manager = false
controlplane-etcd = true
```


All configmap files should be applied to the `kube-system`

namespace for any cluster.

### Customize an ingestion profile

You can customize an ingestion file for collected metrics. For more information, see [Minimal ingestion profile for control plane metrics in managed service for Prometheus](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal#minimal-ingestion-for-default-on-targets).

#### Ingest only minimal metrics from default targets

- Set
`default-targets-metrics-keep-list.minimalIngestionProfile`

to`true`

, so it ingests only the minimal set of metrics for each of the default targets:`controlplane-apiserver`

and`controlplane-etcd`

.

#### Ingest all metrics from all targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplace-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest more than minimal metrics

Using the `minimalingestionprofile`

setting helps reduce the ingestion volume of metrics. If set to `true`

, only default recording rules, default alerts, and metrics that appear in the default dashboards are collected.

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`true`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest specific metrics from specific targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets that you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file:

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

## Troubleshoot control plane metrics issues

Make sure that the `AzureMonitorMetricsControlPlanePreview`

feature flag is enabled and that the `ama-metrics`

pods are running.

Note

The [troubleshooting methods](/en-us/azure/azure-monitor/containers/prometheus-metrics-troubleshoot) for the managed service for Prometheus don't apply directly in this scenario. The components that scrape the control plane aren't included in the managed service for Prometheus add-on.

**Configmap file formatting**: Make sure that you use the correct formatting in the configmap file. Verify that the fields`default-targets-metrics-keep-list`

,`minimal-ingestion-profile`

, and`default-scrape-settings-enabled`

and other fields are correctly populated with their intended values.**Isolate the control plane from the data plane**: Start by setting some of the[node-related metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)to`true`

, and then verify that the metrics are forwarded to the workspace. Completing these steps helps you determine whether an issue is specific to scraping control plane metrics.**A change in the number of events ingested**: After you apply the changes, you can open the metrics explorer in the Azure portal. Go to the Azure Monitor overview pane for the cluster or go to the**Monitoring**section of the selected cluster. Check for an increase or a decrease in the number of events ingested per minute. This information can help you determine whether a specific metric is missing or if all metrics are missing.**A specific metric isn't exposed**: In some scenarios, a metric is documented, but it isn't exposed from the target and isn't forwarded to the Azure Monitor workspace. In this case, it's necessary to verify that other metrics are forwarded to the workspace.Note

If you want to collect the

`apiserver_request_duration_seconds`

metric or another bucket metric, you must set the entire series in the histogram family:`controlplane-apiserver = "apiserver_request_duration_seconds_bucket|apiserver_request_duration_seconds_sum|apiserver_request_duration_seconds_count"`

**No access to the Azure Monitor workspace**: When you enable the add-on, you might specify an existing workspace that you can't access. In that scenario, it appears that metrics aren't collected and forwarded. Make sure that you create a new workspace to use to collect metrics when you enable the add-on or when you create the cluster.

## Disable control plane metrics on your AKS cluster

You can disable control plane metrics at any time by disabling the managed service for Prometheus add-on and unregistering the `AzureMonitorMetricsControlPlanePreview`

feature flag.

Remove the metrics add-on that scrapes Prometheus metrics by using the

command:`az aks update`

`az aks update --disable-azure-monitor-metrics --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`

To disable scraping control plane metrics on the AKS cluster, unregister the

`AzureMonitorMetricsControlPlanePreview`

feature flag via thecommand:`az feature unregister`

`az feature unregister "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`


## Frequently asked questions

### Can I scrape control plane metrics by using self-hosted Prometheus?

No. Currently, you can't scrape control plane metrics by using self-hosted Prometheus. Self-hosted Prometheus can scrape only a single instance, depending on the load balancer, so the metrics aren't reliable. Often, multiple replicas of the control plane metrics are visible only through the managed service for Prometheus.

### Why isn't the user agent available in the control plane metrics?

In AKS, [control plane metrics](https://kubernetes.io/docs/reference/instrumentation/metrics/) don't have the user agent. The user agent is available only through the control plane logs that you access in [diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings).


---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-network.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-network -->

# Best practices for network connectivity and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

As you create and manage clusters in Azure Kubernetes Service (AKS), you provide network connectivity for your nodes and applications. These network resources include IP address ranges, load balancers, and ingress controllers.

This best practices article focuses on network connectivity and security for cluster operators. In this article, you learn how to:

- Explain Azure Container Networking Interface (CNI) network mode in AKS.
- Plan for required IP addressing and connectivity.
- Distribute traffic using load balancers, ingress controllers, or a web application firewall (WAF).
- Securely connect to cluster nodes.

## Choose the appropriate network model


Best practice guidanceUse Azure CNI networking in AKS for integration with existing virtual networks or on-premises networks. This network model allows greater separation of resources and controls in an enterprise environment.


Virtual networks provide the basic connectivity for AKS nodes and customers to access your applications. There are two different ways to deploy AKS clusters into virtual networks:

**Azure CNI networking**: Deploys into a virtual network and uses the[Azure CNI](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)Kubernetes plugin. Pods receive individual IPs that can route to other network services or on-premises resources.

Azure CNI is a valid option for production deployments.

### CNI Networking

Azure CNI is a vendor-neutral protocol that lets the container runtime make requests to a network provider. It assigns IP addresses to pods and nodes, and provides IP address management (IPAM) features as you connect to existing Azure virtual networks. Each node and pod resource receives an IP address in the Azure virtual network. There's no need for extra routing to communicate with other resources or services.

Notably, Azure CNI networking for production allows for separation of control and management of resources. From a security perspective, you often want different teams to manage and secure those resources. With Azure CNI networking, you connect to existing Azure resources, on-premises resources, or other services directly via IP addresses assigned to each pod.

When you use Azure CNI networking, the virtual network resource is in a separate resource group to the AKS cluster. Delegate permissions for the AKS cluster identity to access and manage these resources. The cluster identity used by the AKS cluster must have at least [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) permissions on the subnet within your virtual network.

If you wish to define a [custom role](/en-us/azure/role-based-access-control/custom-roles) instead of using the built-in Network Contributor role, the following permissions are required:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


By default, AKS uses a managed identity for its cluster identity. However, you can use a service principal instead.

- For more information about AKS service principal delegation, see
[Delegate access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources). - For more information about managed identities, see
[Use managed identities](use-managed-identity).

As each node and pod receives its own IP address, plan out the address ranges for the AKS subnets. Keep the following criteria in mind:

- The subnet must be large enough to provide IP addresses for every node, pod, and network resource you deploy.
- With Azure CNI networking, each running node has default limits to the number of pods.

- Avoid using IP address ranges that overlap with existing network resources.
- It's necessary to allow connectivity to on-premises or peered networks in Azure.

- To handle scale-out events or cluster upgrades, you need extra IP addresses available in the assigned subnet.
- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see
[Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see

To calculate the IP address required, see [Configure Azure CNI networking in AKS](configure-azure-cni).

When creating a cluster with Azure CNI networking, you specify other address ranges for the cluster, such as the Docker bridge address, DNS service IP, and service address range. In general, make sure these address ranges don't overlap each other or any networks associated with the cluster, including any virtual networks, subnets, on-premises and peered networks.

For the specific details around limits and sizing for these address ranges, see [Configure Azure CNI networking in AKS](configure-azure-cni).

## Distribute ingress traffic


Best practice guidanceTo distribute HTTP or HTTPS traffic to your applications, use ingress resources and controllers. Compared to an Azure load balancer, ingress controllers provide extra features and can be managed as native Kubernetes resources.


While an Azure load balancer can distribute customer traffic to applications in your AKS cluster, it's limited in understanding that traffic. A load balancer resource works at *layer 4* and distributes traffic based on protocol or ports.

Most web applications using HTTP or HTTPS should use Kubernetes ingress resources and controllers, which work at *layer 7*. Ingress can distribute traffic based on the URL of the application and handle TLS/SSL termination. Ingress also reduces the number of IP addresses you expose and map.

With a load balancer, each application typically needs a public IP address assigned and mapped to the service in the AKS cluster. With an ingress resource, a single IP address can distribute traffic to multiple applications.

There are two components for ingress:

- An ingress
*resource* - An ingress
*controller*

### Ingress resource

The *ingress resource* is a YAML manifest of `kind: Ingress`

. It defines the host, certificates, and rules to route traffic to services running in your AKS cluster.

The following example YAML manifest distributes traffic for *myapp.com* to one of two services, *blogservice* or *storeservice*, and directs the customer to one service or the other based on the URL they access.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: myapp-ingress
spec:
ingressClassName: PublicIngress
tls:
- hosts:
- myapp.com
secretName: myapp-secret
rules:
- host: myapp.com
http:
paths:
- path: /blog
backend:
service:
name: blogservice
port: 80
- path: /store
backend:
service:
name: storeservice
port: 80
```


### Ingress controller

An *ingress controller* is a daemon that runs on an AKS node and watches for incoming requests. Traffic is then distributed based on the rules defined in the ingress resource. While the most common ingress controller is based on [NGINX](https://www.nginx.com/products/nginx/kubernetes-ingress-controller), AKS doesn't restrict you to a specific controller. You can use [Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), [Contour](https://github.com/heptio/contour), [HAProxy](https://www.haproxy.org), [Traefik](https://github.com/containous/traefik), etc.

Ingress controllers must be scheduled on a Linux node. Indicate that the resource should run on a Linux-based node using a node selector in your YAML manifest or Helm chart deployment. For more information, see [Use node selectors to control where pods are scheduled in AKS](concepts-clusters-workloads#node-selectors).

## Ingress with the application routing addon

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed, ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Secure traffic with a web application firewall (WAF)


Best practice guidanceTo scan incoming traffic for potential attacks, use a web application firewall (WAF) such as

[Barracuda WAF for Azure]or[Azure Application Gateway for Containers]. These more advanced network resources can also route traffic beyond just HTTP and HTTPS connections or basic TLS termination.

Typically, an ingress controller is a Kubernetes resource in your AKS cluster that distributes traffic to services and applications. The controller runs as a daemon on an AKS node, and consumes some of the node's resources, like CPU, memory, and network bandwidth. In larger environments, you may want to consider the following:

- Offload some of this traffic routing or TLS termination to a network resource outside of the AKS cluster.
- Scan incoming traffic for potential attacks.

For that extra layer of security, a web application firewall (WAF) filters the incoming traffic. With a set of rules, the Open Web Application Security Project (OWASP) watches for attacks like cross-site scripting or cookie poisoning. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) is a WAF that integrates with AKS clusters, locking in these security features before the traffic reaches your AKS cluster and applications.

Since other third-party solutions also perform these functions, you can continue to use existing investments or expertise in your preferred product.

Load balancer or ingress resources continually run in your AKS cluster and refine the traffic distribution. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) can be centrally managed as an ingress controller with a resource definition. To get started, [create an Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/quickstart-deploy-application-gateway-for-containers-alb-controller).

## Control traffic flow with network policies


Best practice guidanceUse network policies to allow or deny traffic to pods. By default, all traffic is allowed between pods within a cluster. For improved security, define rules that limit pod communication.


Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. Network policies are a cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

To use [network policies in AKS](use-network-policies), the feature can be enabled either during cluster creation or on an existing AKS cluster. If you are planning to use network policies, ensure the feature is enabled on your AKS cluster.

Note

Network policies could be used for Linux-based or Windows-based nodes and pods in AKS.

You create a network policy as a Kubernetes resource using a YAML manifest. Policies are applied to defined pods, with ingress or egress rules defining traffic flow.

The following example applies a network policy to pods with the *app: backend* label applied to them. The ingress rule only allows traffic from pods with the *app: frontend* label.

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
name: backend-policy
spec:
podSelector:
matchLabels:
app: backend
ingress:
- from:
- podSelector:
matchLabels:
app: frontend
```


To get started with policies, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Securely connect to nodes through a bastion host


Best practice guidanceDon't expose remote connectivity to your AKS nodes. Create a bastion host, or jump box, in a management virtual network. Use the bastion host to securely route traffic into your AKS cluster to remote management tasks.


You can complete most operations in AKS using the Azure management tools or through the Kubernetes API server. AKS nodes are only available on a private network and aren't connected to the public internet. To connect to nodes and provide maintenance and support, route your connections through a bastion host, or jump box. Verify this host lives in a separate, securely peered management virtual network to the AKS cluster virtual network.

You should also secure the management network for the bastion host. Use an [Azure ExpressRoute](/en-us/azure/expressroute/expressroute-introduction) or [VPN gateway](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways) to connect to an on-premises network and control access using network security groups.

## Next steps

This article focused on network connectivity and security. For more information about network basics in Kubernetes, see [Network concepts for applications in Azure Kubernetes Service (AKS)](concepts-network)
