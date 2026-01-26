---
merged_at: 2026-01-26T23:04:05.998894
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dns-concepts -->

# DNS Resolution in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Domain Name System (DNS) resolution is a critical component in Azure Kubernetes Service (AKS), enabling pods and services to communicate using human-readable names instead of IP addresses. AKS provides built-in DNS services to ensure seamless name resolution for both internal cluster resources and external endpoints. Understanding how DNS works in AKS helps cluster operators and developers ensure reliable connectivity, optimize performance, and troubleshoot networking issues effectively.

## CoreDNS in Azure Kubernetes Service

[CoreDNS](https://coredns.io/) is the default DNS service in Azure Kubernetes Service (AKS), providing internal name resolution and service discovery for workloads running in the cluster. It operates as a set of pods in the kube-system namespace and is tightly integrated with Kubernetes networking.

When a pod in AKS issues a DNS query—such as resolving the name of another service—the request is routed to the CoreDNS pods. These pods process the query and return the appropriate IP address or forward the request to an upstream DNS server for external domains.

This architecture ensures a balance between flexibility and operational safety in a managed environment. For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

## LocalDNS in Azure Kubernetes Service

Note

This document provides an overview of what LocalDNS is and its benefits in AKS. It doesn't include setup instructions. For guidance on enabling and configuring LocalDNS, see the [LocalDNS how-to guide](localdns-custom).

### Overview

LocalDNS is an advanced feature in Azure Kubernetes Service (AKS) that deploys a Domain Name System (DNS) proxy on each node to provide highly resilient, low-latency DNS resolution. By handling DNS queries locally, this proxy reduces traffic to the CoreDNS addon pods, improving overall DNS reliability and performance in the cluster. LocalDNS is especially beneficial in large clusters or environments with high DNS query volumes, where centralized DNS resolution can become a bottleneck.

When LocalDNS is enabled, AKS deploys a local DNS cache as a `systemd`

service on each node. Pods on the node send their DNS queries to this local cache, enabling faster resolution by reducing network hops. This approach also minimizes `conntrack`

table usage, lowering the risk of table exhaustion. Additionally, if upstream DNS becomes unavailable, LocalDNS can continue serving cached responses for a configurable duration, helping maintain pod connectivity and service reliability.

### Key capabilities

**Reduced DNS resolution latency:**Each AKS node runs a LocalDNS`systemd`

service. Workloads running on the node send DNS queries to this service, which resolves them locally, reducing network hops and speeding up DNS lookups.**Customizable DNS behavior:**You can use`kubeDNSOverrides`

and`vnetDNSOverrides`

to control DNS behavior in the cluster.**Avoid conntrack races and conntrack table exhaustion:**Pods send DNS queries to the LocalDNS service on the same node without creating new`conntrack`

table entries. Skipping the connection tracking helps reduce[conntrack races](https://github.com/kubernetes/kubernetes/issues/56903)and avoids User Datagram Protocol (UDP) DNS entries from filling up`conntrack`

tables. This optimization prevents dropped and rejected connections caused by`conntrack`

table exhaustion and race conditions.**Connection upgraded to TCP:**The connection from the`localdns`

cache to the cluster’s CoreDNS service uses Transmission Control Protocol (TCP). TCP allows for connection rebalancing and removes`conntrack`

table entries when the server closes the connection (in contrast to UDP connections, which have a default 30-second timeout). Applications don't need changes, because the`localdns`

service still listens for UDP traffic.**Caching:**The LocalDNS cache plugin can be configured with serveStale and Time to Live (TTL) settings.`serveStale`

,`serveStaleDurationInSeconds`

, and`cacheDurationInSeconds`

parameters can be configured to achieve DNS resiliency, even during an upstream DNS outage.**Protocol control:**You can set the DNS query protocol (such as PreferUDP or ForceTCP) for each domain. This flexibility lets you optimize DNS traffic for specific domains or meet network requirements.

### Other benefits and considerations

| Benefits | Considerations |
|---|---|
Better scalability: Reduces load on centralized CoreDNS pods |
Minimal resource overhead: Uses a small amount of CPU and memory on each node |
Seamless integration: Does not require changes to existing application connections |
Configuration changes: Updates require node image upgrades, which can cause temporary disruptions |
Block invalid search domains: Prevents invalid DNS queries at the node level |

By using LocalDNS, you get faster and more reliable DNS resolution for your workloads, reduce the risk of DNS-related outages, and gain more control over DNS traffic in your AKS environment.

## Next steps

To learn how to enable LocalDNS and configure its settings in your AKS cluster, see the [LocalDNS how-to guide](localdns-custom).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-concepts -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways:

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports health probe annotations for ports 80 and 443. Learn more about the usage of ports [here](/en-us/azure/aks/load-balancer-standard#customize-the-load-balancer-health-probe).

### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic -->

# Limit network traffic with Azure Firewall in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) to control egress traffic using Azure Firewall. To simplify this configuration, Azure Firewall provides an Azure Kubernetes Service (`AzureKubernetesService`

) FQDN tag that restricts outbound traffic from the AKS cluster.

## Firewall frontend IP requirements

**Production minimum**: Use at least 20 frontend IPs on Azure Firewall to avoid source network address translation (SNAT) port exhaustion.**High-traffic clusters**: If your cluster creates many outbound connections to the same destinations, you might need more frontend IPs to avoid maxing out ports per IP**API server protection**: Add the firewall's public frontend IP to[API server authorized IP ranges](api-server-authorized-ip-ranges)for enhanced security**Developer access**: When using authorized IP ranges, either use a jumpbox in the firewall's virtual network (VNet) or add developer endpoint IPs to the authorized range

This guidance applies throughout the configuration process described in this article.

Note

The FQDN tag contains all the FQDNs listed in [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) and is automatically updated.

## Architecture overview

The following diagram illustrates the architecture of an AKS cluster with restricted egress traffic using Azure Firewall:

Key components of this architecture include:

**Public ingress is forced to flow through firewall filters**:- AKS agent nodes are isolated in a dedicated subnet.
[Azure Firewall](/en-us/azure/firewall/overview)is deployed in its own subnet.- A DNAT rule translates the firewall public IP into the load balancer frontend IP.

**Outbound requests start from agent nodes to the Azure Firewall internal IP using a**:[user-defined route (UDR)](egress-outboundtype)- Requests from AKS agent nodes follow a UDR that has been placed on the subnet the AKS cluster was deployed into.
- Azure Firewall egresses out of the VNet from a public IP frontend.
- Access to the public internet or other Azure services flows to and from the firewall frontend IP address.
- You can protect access to the AKS control plane using
[API server authorized IP ranges](api-server-authorized-ip-ranges), including the firewall public frontend IP address.

**Internal traffic**:- You can use an
[internal load balancer](internal-lb)for internal traffic, which you could isolate on its own subnet, instead of or alongside a[public load balancer](load-balancer-standard).

- You can use an

## Configure environment variables

The following table lists the environment variables used in this article. Set these variables in your shell before proceeding, or modify the commands to use your own values.

| Variable | Description | Example value |
|---|---|---|
`PREFIX` |
Prefix for resource names | `aks-egress` |
`RESOURCE_GROUP` |
Name of the resource group | `aks-egress-rg` |
`LOCATION` |
Azure region for resources | `eastus` |
`PLUGIN` |
Network plugin for AKS | `azure` |
`CLUSTER_NAME` |
Name of the AKS cluster | `aks-egress` |
`VNET_NAME` |
Name of the virtual network | `aks-egress-vnet` |
`AKS_SUBNET_NAME` |
Name of the subnet for AKS | `aks-subnet` |
`FW_SUBNET_NAME` |
Name of the subnet for Azure Firewall | `AzureFirewallSubnet` |
`FW_NAME` |
Name of the Azure Firewall | `aks-egress-fw` |
`FW_PUBLICIP_NAME` |
Name of the public IP for Azure Firewall | `aks-egress-fwpublicip` |
`FW_IPCONFIG_NAME` |
Name of the IP configuration for Azure Firewall | `aks-egress-fwconfig` |
`FW_ROUTE_TABLE_NAME` |
Name of the route table for Azure Firewall | `aks-egress-fwrt` |
`FW_ROUTE_NAME_1` |
Name of the route for Azure Firewall | `aks-egress-fwrn` |
`FW_ROUTE_NAME_2` |
Name of the internet route for Azure Firewall | `aks-egress-fwrn-internet` |

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a virtual network with multiple subnets

Provision a VNet with two separate subnets: one for the cluster and one for the firewall. Optionally, you can create one for internal service ingress. The following diagram illustrates the empty network topology before deploying any resources:

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --resource-group $RESOURCE_GROUP \ --name $VNET_NAME \ --location $LOCATION \ --address-prefixes 10.42.0.0/16 \ --subnet-name $AKS_SUBNET_NAME \ --subnet-prefix 10.42.1.0/24`

Create a subnet for Azure Firewall using the

command.`az network vnet subnet create`

`# Dedicated subnet for Azure Firewall (subnet must be named "AzureFirewallSubnet") az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $FW_SUBNET_NAME \ --address-prefix 10.42.2.0/24`


## Create a public IP for Azure Firewall

Create a standard SKU public IP resource using the

command. This resource is used as the frontend IP address for the Azure Firewall.`az network public-ip create`

`az network public-ip create --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --location $LOCATION --sku "Standard"`


## Install the Azure Firewall CLI extension

Register the

[Azure Firewall CLI extension](https://github.com/Azure/azure-cli-extensions/tree/main/src/azure-firewall)to create an Azure Firewall using thecommand.`az extension add`

`az extension add --name azure-firewall`


## Create an Azure Firewall and enable DNS proxy

Note

For high-traffic scenarios, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

For more information on how to create an Azure Firewall with multiple IPs, see [Create an Azure Firewall with multiple public IP addresses using Bicep](/en-us/azure/firewall/quick-create-multiple-ip-bicep).

Create an Azure Firewall and enable DNS proxy using the

command with`az network firewall create`

`--enable-dns-proxy`

set to`true`

.`az network firewall create --resource-group $RESOURCE_GROUP --name $FW_NAME --location $LOCATION --enable-dns-proxy true`

Setting up the public IP address to the Azure Firewall might take a few minutes. Once it's ready, you can assign the IP address to the firewall front end.

Note

To use FQDN on network rules, you need DNS proxy enabled. When DNS proxy is enabled, the firewall listens on port 53 and forwards DNS requests to the DNS server you specify. This setting allows the firewall to automatically translate the FQDN.


## Create an IP configuration for Azure Firewall

Create an Azure Firewall IP configuration using the

command.`az network firewall ip-config create`

`az network firewall ip-config create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --name $FW_IPCONFIG_NAME --public-ip-address $FW_PUBLICIP_NAME --vnet-name $VNET_NAME`


## Get the Azure Firewall IP addresses

Save the public and private firewall frontend IP addresses for configuration later using the following commands:

`export FW_PUBLIC_IP=$(az network public-ip show --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --query "ipAddress" -o tsv) export FW_PRIVATE_IP=$(az network firewall show --resource-group $RESOURCE_GROUP --name $FW_NAME --query "ipConfigurations[0].privateIPAddress" -o tsv)`

Note

For API server security, see the

[firewall frontend IP requirements](#firewall-frontend-ip-requirements)section.

## UDR configuration for AKS egress through Azure Firewall

Azure automatically routes traffic between Azure subnets, VNets, and on-premises networks. To modify default routing, create a route table with the following requirements:

**Required route parameters**:

**Route destination**:`0.0.0.0/0`

(all traffic)**Next hop type**: Network virtual appliance (NVA)**Next hop IP**: Azure Firewall private IP address**Association**: One route table per subnet (*zero*or*one*allowed)

**UDR constraints**:

- Default internet route (
`0.0.0.0/0`

) already exists but requires public IP for SNAT. - Route must point to gateway/NVA, not directly to internet.
- AKS validates route configuration and prevents direct internet routes.
- Each subnet supports maximum of
*one*associated route table.

**Outbound type impact**:

**UDR (**: No load balancer public IP created for outbound requests.`userDefinedRouting`

)**Load Balancer public IP**: Only created for inbound requests with`LoadBalancer`

service type.**SNAT configuration**: Requires proper public IP configuration for outbound connectivity.

For more information, see [Outbound rules for Azure Load Balancer](/en-us/azure/load-balancer/outbound-rules#scenario6out).

## Create a route with a hop to Azure Firewall

Create an empty route table using the

command. The route table defines the Azure Firewall as the next hop. Each subnet can have`az network route-table create`

*zero*or*one*route table associated to it.`az network route-table create --resource-group $RESOURCE_GROUP --location $LOCATION --name $FW_ROUTE_TABLE_NAME`

Create routes in the route table for the subnets using the

command.`az network route-table route create`

`az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_1 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FW_PRIVATE_IP az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_2 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix $FW_PUBLIC_IP/32 --next-hop-type Internet`


For information on how to override Azure's default system routes or add more routes to a subnet's route table, see the [Virtual network route table documentation](/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined).

## Azure Firewall outbound rules for AKS

Note

For applications outside of the `kube-system`

or `gatekeeper-system`

namespaces that need to talk to the API server, an extra network rule to allow TCP communication to port 443 for the API server IP in addition to adding application rule for `fqdn-tag`

of `AzureKubernetesService`

is required.

The following network rules are required for AKS egress traffic control through Azure Firewall:

- The first network rule allows access to port 9000 via TCP.
- The second network rule allows access to port 1194 via UDP. If you're deploying to Microsoft Azure operated by 21Vianet, see the
[Azure operated by 21Vianet required network rules](outbound-rules-control-egress#microsoft-azure-operated-by-21vianet-required-network-rules). In this article, the commands use the`AzureCloud.$LOCATION`

service tag as the destination address. Service tags represent groups of IP address prefixes for Azure services in specific regions. This automatically includes the appropriate CIDR ranges for Azure services without requiring manual IP range specification. - The third network rule opens port 123 to
`ntp.ubuntu.com`

FQDN via UDP. Adding an FQDN as a network rule is one of the specific features of Azure Firewall, so you need to adapt it when using your own options. - The fourth and fifth network rules allow access to pull containers from GitHub Container Registry (
`ghcr.io`

) and Docker Hub (`docker.io`

).

## Create network rules on Azure Firewall

Create the network rules using the following

commands.`az network firewall network-rule create`

`az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 9000 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 1194 --action allow --priority 100 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'ghcr' --protocols 'TCP' --source-addresses '*' --destination-fqdns ghcr.io pkg-containers.githubusercontent.com --destination-ports '443' az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'docker' --protocols 'TCP' --source-addresses '*' --destination-fqdns docker.io registry-1.docker.io production.cloudflare.docker.com --destination-ports '443'`


## Create application rules on Azure Firewall

Create the application rule using the

command.`az network firewall application-rule create`

`az network firewall application-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwar' --name 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100`


To learn more about Azure Firewall, see the [Azure Firewall documentation](/en-us/azure/firewall/overview).

## Associate the route table to AKS

To associate the cluster with the firewall, the dedicated subnet for the cluster's subnet must reference the route table.

Associate the route table to AKS using the

command.`az network vnet subnet update`

`az network vnet subnet update --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --route-table $FW_ROUTE_TABLE_NAME`


## Deploy an AKS cluster that follows your outbound rules

You can now deploy an AKS cluster into the existing VNet. You use the [ userDefinedRouting outbound type](egress-outboundtype), which ensures that any outbound traffic is forced through the firewall and no other egress paths exist. You can also use the

[.](egress-outboundtype#outbound-type-of-loadbalancer)

`loadBalancer`

outbound typeSet an environment variable for the subnet ID of the target subnet using the following command:

`SUBNET_ID=$(az network vnet subnet show --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --query id -o tsv)`


You define the outbound type to use the UDR that already exists on the subnet. This configuration enables AKS to skip the setup and IP provisioning for the load balancer.

Tip

You can add extra features to the cluster deployment, such as [ private clusters](private-clusters).

For API server authorized IP ranges setup and developer access considerations, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

## Create an AKS cluster with system-assigned identities

Note

AKS creates a system-assigned kubelet identity in the node resource group if you don't [specify your own kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity).

For user-defined routing, system-assigned identity only supports the CNI network plugin.

Create an AKS cluster using a system-assigned managed identity with the CNI network plugin using the

command.`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION \ --node-count 3 \ --network-plugin azure \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --generate-ssh-keys`


## Create user-assigned identities

If you don't have user-assigned identities, follow the steps in this section. If you already have user-assigned identities, skip to [Create an AKS cluster with user-assigned identities](#create-an-aks-cluster-with-user-assigned-identities).

Create a managed identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "eastus", "name": "myIdentity", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Create a kubelet managed identity using the

command.`az identity create`

`az identity create --name myKubeletIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myKubeletIdentity", "location": "eastus", "name": "myKubeletIdentity", ... "resourceGroup": "aks-egress-rg", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


Note

If you create your own VNet and route table where the resources are outside of the worker node resource group, the CLI automatically adds the role assignment. If you're using an ARM template or other method, you need to use the principal ID of the cluster managed identity to perform a [role assignment](use-managed-identity#add-a-role-assignment-for-a-system-assigned-managed-identity).

## Create an AKS cluster with user-assigned identities

Create an AKS cluster with your existing user-assigned managed identities in the subnet using the

command. Provide the resource ID of the managed identity for the control plane and the resource ID of the kubelet identity.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --node-count 3 \ --network-plugin kubenet \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`


## Enable developer access to the API server

If you used authorized IP ranges for your cluster in the previous step, you need to add your developer tooling IP addresses to the AKS cluster list of approved IP ranges so you access the API server from there. You can also configure a jumpbox with the needed tooling inside a separate subnet in the firewall's VNet.

Retrieve your IP address using the following command:

`CURRENT_IP=$(dig @resolver1.opendns.com ANY myip.opendns.com +short)`

Add the IP address to the approved ranges using the

command.`az aks update`

`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --api-server-authorized-ip-ranges $CURRENT_IP/32`


## Connect to the AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Deploy a public service on AKS

You can now start exposing services and deploying applications to this cluster. This example exposes a public service, but you also might want to expose an internal service using an [internal load balancer](internal-lb).

Review the

[AKS Store Demo quickstart](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-quickstart.yaml)manifest to understand the deployed components.Deploy the service using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-quickstart.yaml`


## Get the load balancer internal IP and service IP

Get the internal IP address assigned to the load balancer using the

`kubectl get services`

command.`kubectl get services`

The IP address should be listed in the

`EXTERNAL-IP`

column, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 9m10s order-service ClusterIP 10.0.104.144 <none> 3000/TCP 11s product-service ClusterIP 10.0.237.60 <none> 3002/TCP 10s rabbitmq ClusterIP 10.0.161.128 <none> 5672/TCP,15672/TCP 11s store-front LoadBalancer 10.0.89.139 20.39.18.6 80:32271/TCP 10s`

Get the service IP using the

`kubectl get svc store-front`

command.`SERVICE_IP=$(kubectl get svc store-front -o jsonpath='{.status.loadBalancer.ingress[*].ip}')`


## Create a DNAT rule on Azure Firewall

Important

When you use Azure Firewall to restrict egress traffic and create a UDR to force all egress traffic, make sure you create an appropriate DNAT rule in Azure Firewall to correctly allow ingress traffic. Using Azure Firewall with a UDR breaks the ingress setup due to asymmetric routing. The issue occurs if the AKS subnet has a default route that goes to the firewall's private IP address, but you're using a public load balancer - ingress or Kubernetes service of type `loadBalancer`

. In this case, the incoming load balancer traffic is received via its public IP address, but the return path goes through the firewall's private IP address. Because the firewall is stateful, it drops the returning packet because the firewall isn't aware of an established session. To learn how to integrate Azure Firewall with your ingress or service load balancer, see [Integrate Azure Firewall with Azure Standard Load Balancer](/en-us/azure/firewall/integrate-lb).

To configure inbound connectivity, you need to write a DNAT rule to the Azure Firewall. To test connectivity to your cluster, a rule is defined for the firewall frontend public IP address to route to the internal IP exposed by the internal service. You can customize the destination address. The translated address must be the IP address of the internal load balancer. The translated port must be the exposed port for your Kubernetes service. You also need to specify the internal IP address assigned to the load balancer created by the Kubernetes service.

Add the NAT rule using the

command.`az network firewall nat-rule create`

`az network firewall nat-rule create --collection-name exampleset --destination-addresses $FW_PUBLIC_IP --destination-ports 80 --firewall-name $FW_NAME --name inboundrule --protocols Any --resource-group $RESOURCE_GROUP --source-addresses '*' --translated-port 80 --action Dnat --priority 100 --translated-address $SERVICE_IP`


## Validate connectivity

Navigate to the Azure Firewall frontend IP address in a browser to validate connectivity. You should see the AKS store app. In this example, the firewall public IP was

`52.253.228.132`

:, you can view products, add them to your cart, and then place an order.


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring future costs.

Delete the AKS resource group using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-oidc-issuer -->

# Create an OpenID Connect provider on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to create and manage an OpenID Connect (OIDC) provider for your Azure Kubernetes Service (AKS) cluster. The OIDC issuer allows your AKS cluster to integrate with identity providers like Microsoft Entra ID, enabling secure authentication and single sign-on (SSO) capabilities for applications running within the cluster.

## About OpenID Connect (OIDC) on AKS

[OpenID Connect](/en-us/azure/active-directory/fundamentals/auth-oidc) (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol issued by Microsoft Entra ID. You can use OIDC to enable single sign-on (SSO) between OAuth-enabled applications on your Azure Kubernetes Service (AKS) cluster using a security token called an ID token. You can enable the OIDC issuer on your AKS clusters, which allows Microsoft Entra ID (or another cloud provider's identity and access management platform) to discover the API server's public signing keys.

## Prerequisites

**Platform requirements**:

- Azure CLI version 2.42.0+ (
`az --version`

to check version,[install or upgrade Azure CLI](/en-us/cli/azure/install-azure-cli)if needed) - Minimum Kubernetes version is 1.22+

**Version-specific behavior**:

- OIDC issuer enabled by default (no
`--enable-oidc-issuer`

flag needed) for Kubernetes version 1.34+ - Token auto-extension disabled (
`--service-account-extend-token-expiration=false`

) for Kubernetes version 1.30.0+ - Manual enablement required if not previously configured for Kubernetes version earlier than 1.34

**Important considerations**:

- You can't disable OIDC issuer once enabled
- Enabling OIDC issuer on existing clusters requires API server restart (brief downtime)
- Maximum token lifetime is 24 hours (one day)
- Projected service account tokens required for Kubernetes 1.30+ clusters

## Create an AKS cluster with the OIDC issuer

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster with OIDC issuer enabled (OIDC issuer enabled by default for Kubernetes 1.34+) az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --enable-oidc-issuer \ --generate-ssh-keys`


## Enable the OIDC issuer on an existing AKS cluster

Enable the OIDC issuer on an existing AKS cluster using the

command with the`az aks update`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Enable the OIDC issuer on the existing AKS cluster az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-oidc-issuer`


## Get the OIDC issuer URL

Get the OIDC issuer URL using the

command.`az aks show`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Get the OIDC issuer URL az aks show \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --query "oidcIssuerProfile.issuerUrl" \ -o tsv`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com`

, where the value for`{region}`

matches the location the AKS cluster is deployed in.

## Rotate the OIDC key

Important

Keep the following considerations in mind when rotating the OIDC key:

- If you want to invalidate the old key immediately after key rotation, you must rotate the OIDC key twice and restart the pods using projected service account tokens.
- Both old and new keys remain valid for 24 hours after rotation.
- Manual token refresh required every 24 hours (unless using
[Azure Identity SDK](workload-identity-overview#azure-identity-client-libraries), which rotates automatically).

Rotate the OIDC key using the

command.`az aks oidc-issuer`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Rotate the OIDC signing keys az aks oidc-issuer rotate-signing-keys \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP`


## Get the discovery document

Navigate to your

[OIDC issuer URL](#get-the-oidc-issuer-url)in your browser and append`/.well-known/openid-configuration`

to the URL. For example:`https://eastus.oic.prod-aks.azure.com/.well-known/openid-configuration`

.Your output should resemble the following example output:

`{ "issuer": "https://eastus.oic.prod-aks.azure.com/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/00000000-0000-0000-0000-000000000000/", "jwks_uri": "https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks", "response_types_supported": [ "id_token" ], "subject_types_supported": [ "public" ], "id_token_signing_alg_values_supported": [ "RS256" ] }`


## Get the JWK Set document

Navigate to the

in your browser. For example:**jwks_uri**from the discovery document`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks`

.Your output should resemble the following example output:

`{ "keys": [ { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" }, { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" } ] }`

Note

During key rotation, there's one other key present in the discovery document.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-isolated -->

# Create a network isolated Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable. This article walks you through the steps of creating a network isolated cluster.

## Before you begin

- Read the
[conceptual overview of this feature](concepts-network-isolated), which provides an explanation of how network isolated clusters work. The overview article also:- Explains two options for private Azure Container Registry (ACR) resource used for cluster bootstrapping - AKS-managed ACR or bring-your-own ACR.
- Explains two private cluster modes for creating private access to API server -
[private link-based](private-clusters)or[API Server Vnet Integration](api-server-vnet-integration). - Explains the two outbound types for cluster egress control -
`none`

or`block`

(preview). - Describes the
[current limitations of network isolated clusters](concepts-network-isolated#limitations).


Note

Outbound type `none`

is generally available.
Outbound type`block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.71.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You should install the
`aks-preview`

Azure CLI extension version*9.0.0b2*or later if you are using outbound type`block`

(preview).- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
- Network isolated clusters are supported on AKS clusters using Kubernetes version 1.30 or higher.
- If you're choosing to use the Bring your own (BYO) Azure Container Registry (ACR) option, you need to ensure the ACR is
[Premium SKU service tier](/en-us/azure/container-registry/container-registry-skus). - If you are using a network isolated cluster configured with API Server VNet Integration, you should follow the prerequisites and guidance in this
[document](api-server-vnet-integration).

## Deploy a network isolated cluster with AKS-managed ACR

AKS creates, manages, and reconciles an ACR resource in this option. You don't need to assign any permissions or manage the ACR. AKS manages the cache rules, private link, and private endpoint used in the network isolated cluster.

### Create a network isolated cluster

When creating a network isolated AKS cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct MAR (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

Create a network isolated cluster configured with API Server VNet Integration by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, `--enable-apiserver-vnet-integration`

and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster --enable-apiserver-vnet-integration
```


### Update an existing AKS cluster to network isolated type

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

## Deploy a network isolated cluster with bring your own ACR

AKS supports bringing your own (BYO) ACR. To support the BYO ACR scenario, you have to configure an ACR private endpoint and a private DNS zone before you create the AKS cluster.

The following steps show how to prepare these resources:

- Custom virtual network and subnets for AKS and ACR.
- ACR, ACR cache rule, private endpoint, and private DNS zone.
- Custom control plane identity and kubelet identity.

### Step 1: Create the virtual network and subnets

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az network vnet create --resource-group ${RESOURCE_GROUP} --name ${VNET_NAME} --address-prefixes 192.168.0.0/16
az network vnet subnet create --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.1.0/24
SUBNET_ID=$(az network vnet subnet show --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' --output tsv)
az network vnet subnet create --name ${ACR_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.2.0/24 --private-endpoint-network-policies Disabled
```


### Step 2: Disable virtual network outbound connectivity (Optional)

There are multiple ways to [disable the virtual network outbound connectivity](/en-us/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access).

### Step 3: Create the ACR and enable artifact cache

Create the ACR with the private link.

`az acr create --resource-group ${RESOURCE_GROUP} --name ${REGISTRY_NAME} --sku Premium --public-network-enabled false REGISTRY_ID=$(az acr show --name ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --query 'id' --output tsv)`

Create an ACR cache rule following the below command to allow users to cache MAR container images and binaries in the new ACR, note the cache rule name and repo names must be strictly aligned with the guidance below.

`az acr cache create -n aks-managed-mcr -r ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --source-repo "mcr.microsoft.com/*" --target-repo "aks-managed-repository/*"`


Note

With BYO ACR, it is your responsibility to ensure the ACR cache rule is created and maintained correctly as above. This step is critical to cluster creation, functioning and upgrading. This cache rule should NOT be modified.

### Step 4: Create a private endpoint for the ACR

```
az network private-endpoint create --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --subnet ${ACR_SUBNET_NAME} --private-connection-resource-id ${REGISTRY_ID} --group-id registry --connection-name myConnection
NETWORK_INTERFACE_ID=$(az network private-endpoint show --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --query 'networkInterfaces[0].id' --output tsv)
REGISTRY_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry'].privateIPAddress" --output tsv)
DATA_ENDPOINT_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry_data_$LOCATION'].privateIPAddress" --output tsv)
```


### Step 5: Create a private DNS zone and add records

Create a private DNS zone named `privatelink.azurecr.io`

. Add the records for the registry REST endpoint `{REGISTRY_NAME}.azurecr.io`

, and the registry data endpoint `{REGISTRY_NAME}.{REGISTRY_LOCATION}.data.azurecr.io`

.

```
az network private-dns zone create --resource-group ${RESOURCE_GROUP} --name "privatelink.azurecr.io"
az network private-dns link vnet create --resource-group ${RESOURCE_GROUP} --zone-name "privatelink.azurecr.io" --name MyDNSLink --virtual-network ${VNET_NAME} --registration-enabled false
az network private-dns record-set a create --name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${REGISTRY_PRIVATE_IP}
az network private-dns record-set a create --name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${DATA_ENDPOINT_PRIVATE_IP}
```


### Step 6: Create control plane and kubelet identities

#### Control plane identity

```
az identity create --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
CLUSTER_IDENTITY_RESOURCE_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
CLUSTER_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Kubelet identity

```
az identity create --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
KUBELET_IDENTITY_RESOURCE_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
KUBELET_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Grant AcrPull permissions for the Kubelet identity

```
az role assignment create --role AcrPull --scope ${REGISTRY_ID} --assignee-object-id ${KUBELET_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


After you configure these resources, you can proceed to create the network isolated AKS cluster with BYO ACR.

### Step 7: Create network isolated cluster using BYO ACR

When creating a network isolated cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct Microsoft Artifact Registry (MAR) (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster that accesses your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

For a network isolated cluster configured with API server VNet integration, first create a subnet and assign the correct role with the following commands:

```
az network vnet subnet create --name ${APISERVER_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.3.0/24
export APISERVER_SUBNET_ID=$(az network vnet subnet show --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --name ${APISERVER_SUBNET_NAME} --query id -o tsv)
```


```
az role assignment create --scope ${APISERVER_SUBNET_ID} --role "Network Contributor" --assignee-object-id ${CLUSTER_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


Create a network isolated cluster configured with API Server VNet Integration and access your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-apiserver-vnet-integration --apiserver-subnet-id ${APISERVER_SUBNET_ID}
```


### Update an existing AKS cluster

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

When creating the private endpoint and private DNS zone for the BYO ACR, use the existing virtual network and subnets of the existing AKS cluster. When you assign the **AcrPull** permission to the kubelet identity, use the existing kubelet identity of the existing AKS cluster.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID}
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

### Update your ACR ID

It's possible to update the private ACR used with a network isolated cluster. To identify the ACR resource ID, use the `az aks show`

command.

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


Updating the ACR ID is performed by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--bootstrap-container-registry-resource-id`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id <New BYO ACR resource ID>
```


When you update the ACR ID on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you enable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Validate that network isolated cluster is enabled

To validate the network isolated cluster feature is enabled, use the `[az aks show](/en-us/cli/azure/aks#az-aks-show) command

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


The following output shows that the feature is enabled, based on the values of the `outboundType`

property (none or blocked) and `artifactSource`

property (Cached).

```
"kubernetesVersion": "1.30.3",
"name": "myAKSCluster"
"type": "Microsoft.ContainerService/ManagedClusters"
"properties": {
...
"networkProfile": {
...
"outboundType": "none",
...
},
...
"bootstrapProfile": {
"artifactSource": "Cache",
"containerRegistryId": "/subscriptions/my-subscription-id/my-node-resource-group-name/providers/Microsoft.ContainerRegistry/registries/my-registry-name"
},
...
}
```


## Disable network isolated cluster

Disable the network isolated cluster feature by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Direct --outbound-type LoadBalancer
```


When you disable the feature on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you disable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Troubleshooting

If you're experiencing issues, such as image pull fails, see [Troubleshoot network isolated Azure Kubernetes Service (AKS) clusters issues](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-network-isolated-cluster).

## Next steps

If you want to set up outbound restriction configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).
