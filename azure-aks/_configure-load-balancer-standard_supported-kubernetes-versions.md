---
merged_at: 2026-01-25T12:25:33.981100
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-load-balancer-standard.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-load-balancer-standard -->

# Configure a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize different settings for your standard public load balancer at cluster creation time or by updating the cluster. These customization options allow you to create a load balancer that meets your workload needs. With the standard load balancer, you can:

[Change the inbound pool type](#change-the-inbound-pool-type).[Set or scale the number of managed outbound IPs](#scale-the-number-of-managed-outbound-public-ips).[Provide your own custom outbound IPs or outbound IP prefix](#provide-your-own-outbound-public-ips-or-prefixes).[Customize the number of allocated outbound ports to each node on the cluster](#configure-the-allocated-outbound-ports).[Configure the timeout setting for idle connections](#configure-the-load-balancer-idle-timeout).

Important

You can only use one outbound IP option (managed IPs, bring your own IP, or IP prefix) at a given time.

## Before you begin

- Follow the steps in
[Use a public standard load balancer in Azure Kubernetes Service (AKS)](load-balancer-standard)to create and deploy a load balancer service in AKS.

## Change the inbound pool type

You can reference AKS nodes in the load balancer backend pools by their IP configuration (Azure Virtual Machine Scale Sets based membership) or their IP address only. The IP address based backend pool membership provides higher efficiencies when updating services and provisioning load balancers, especially at high node counts. When combined with [NAT Gateway](nat-gateway) or [user-defined routing egress](egress-udr) types, provisioning of new nodes and services are more performant.

Two different pool membership types are available:

`nodeIPConfiguration`

: Legacy Virtual Machine Scale Sets IP configuration based pool membership type.`nodeIP`

: IP-based membership type.

### Requirements for changing the inbound pool type

Make sure you meet the following requirements before changing the inbound pool type:

- The AKS cluster must be version 1.23 or newer.
- The AKS cluster must be using standard load balancers and Virtual Machine Scale Sets.

-
[Create a new AKS cluster with IP-based inbound pool membership](#tabpanel_1_create-cluster-ip-based) -
[Update an existing AKS cluster to use IP-based inbound pool membership](#tabpanel_1_update-cluster-ip-based)

Create an AKS cluster with IP-based inbound pool membership using the

command with the`az aks create`

`--load-balancer-backend-pool-type=nodeIP`

parameter.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-backend-pool-type=nodeIP \ --generate-ssh-keys`


## Scale the number of managed outbound public IPs

Azure Load Balancer provides outbound and inbound connectivity from a VNet. Outbound rules make it simple to configure network address translation for the public standard load balancer.

Outbound rules follow the same syntax as load balancing and inbound NAT rules: *frontend IPs + parameters + backend pool*

An outbound rule configures outbound NAT for all virtual machines (VMs) identified by the backend pool to be translated to the frontend. Parameters provide more control over the outbound NAT algorithm.

While you can use an outbound rule with a single public IP address, outbound rules are great for scaling outbound NAT because they ease the configuration burden. You can use multiple IP addresses to plan for large-scale scenarios and outbound rules to mitigate SNAT exhaustion prone patterns. Each IP address provided by a frontend provides 64k ephemeral ports for the load balancer to use as SNAT ports.

When using a *Standard* SKU load balancer with managed outbound public IPs (which are created by default), you can scale the number of managed outbound public IPs using the `--load-balancer-managed-outbound-ip-count`

parameter.

Important

We don't recommend using the Azure portal to make any outbound rule changes. When making these changes, you should go through the AKS cluster and not directly on the Load Balancer resource.

Outbound rule changes made directly on the Load Balancer resource are removed whenever the cluster is reconciled, such as when it's stopped, started, upgraded, or scaled.

Use the Azure CLI, as shown in the examples. Outbound rule changes made using `az aks`

CLI commands are permanent across cluster downtime.

For more information, see [Azure Load Balancer outbound rules](/en-us/azure/load-balancer/outbound-rules).

### Set the number of managed outbound public IPs

-
[Create a new cluster with a specific number of managed outbound public IPs](#tabpanel_2_create-cluster-managed-outbound-ips) -
[Update an existing cluster to scale the number of managed outbound public IPs](#tabpanel_2_update-cluster-managed-outbound-ips)

Create a new AKS cluster with a specific number of managed outbound public IPs using the

command with the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter. The following example sets the number of managed outbound public IPs to*two*.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 2 \ --generate-ssh-keys`


## Provide your own outbound public IPs or prefixes

When you use a *Standard* SKU load balancer, the AKS cluster automatically creates a public IP in the AKS-managed infrastructure resource group and assigns it to the load balancer outbound pool by default.

A public IP created by AKS is an AKS-managed resource, meaning AKS manages the lifecycle of that public IP and doesn't require user action directly on the public IP resource. Alternatively, you can assign your own custom public IP or public IP prefix at cluster creation time. Your custom IPs can also be updated on an existing cluster's load balancer properties.

### Requirements for using your own outbound public IPs or prefixes

Make sure you meet the following requirements before providing your own outbound public IPs or prefixes:

- You must create and own custom public IP addresses. You can't reuse managed public IP addresses created by AKS as a "bring your own custom IP" because it can cause management conflicts.
- You must ensure the AKS cluster identity has permissions to access the outbound IP, as per the
[required public IP permissions list](kubernetes-service-principal#grant-access-to-networking-resources). - Make sure you meet the
[prerequisites and constraints](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix#limitations)necessary to configure outbound IPs or outbound IP prefixes.

### Provide your own outbound public IPs

-
[Provide your own outbound public IPs when creating a new cluster](#tabpanel_3_create-cluster-custom-ips) -
[Update an existing cluster to use your own outbound public IPs](#tabpanel_3_update-cluster-custom-ips)

Create a new AKS cluster with your own outbound public IPs using the

command with the`az aks create`

`--load-balancer-outbound-ips`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-outbound-ips $PUBLIC_IP_ID1,$PUBLIC_IP_ID2 \ --generate-ssh-keys`


### Provide your own outbound public IP prefixes

-
[Provide your own outbound public IP prefixes when creating a new cluster](#tabpanel_4_create-cluster-custom-ip-prefixes) -
[Update an existing cluster to use your own outbound public IP prefixes](#tabpanel_4_update-cluster-custom-ip-prefixes)

Create a new AKS cluster with your own outbound public IP prefixes using the

command with the`az aks create`

`--load-balancer-outbound-ip-prefixes`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --load-balancer-outbound-ip-prefixes $PUBLIC_IP_PREFIX_ID1,$PUBLIC_IP_PREFIX_ID2 \ --generate-ssh-keys`


## Configure the allocated outbound ports

Important

If you have applications on your cluster that can establish a large number of connections to small set of destinations on public IP addresses, like many instances of a frontend application connecting to a database, you might have a scenario susceptible to encounter SNAT port exhaustion. SNAT port exhaustion happens when an application runs out of outbound ports to use to establish a connection to another application or host. If you have a scenario susceptible to encounter SNAT port exhaustion, we highly recommend you increase the allocated outbound ports and outbound frontend IPs on the load balancer.

For more information on SNAT, see [Use SNAT for outbound connections](/en-us/azure/load-balancer/load-balancer-outbound-connections).

By default, AKS sets *AllocatedOutboundPorts* on its load balancer to `0`

, which enables [automatic outbound port assignment based on backend pool size](/en-us/azure/load-balancer/load-balancer-outbound-connections#preallocatedports) when creating a cluster. For example, if a cluster has 50 or fewer nodes, 1024 ports are allocated to each node. This value allows for scaling to cluster maximum node counts without requiring networking reconfiguration, but can make SNAT port exhaustion more common as more nodes are added. As the number of nodes in the cluster increases, fewer ports are available per node. Increasing the node counts across the boundaries in the chart (for example, going from 50 to 51 nodes or 100 to 101) might be disruptive to connectivity as the SNAT ports allocated to existing nodes are reduced to allow for more nodes. We recommend using an explicit value for *AllocatedOutboundPorts*.

### View the current allocated outbound ports

Get the

*AllocatedOutboundPorts*value for the AKS cluster load balancer using thecommand.`az network lb outbound-rule list`

`NODE_RG=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query nodeResourceGroup -o tsv) az network lb outbound-rule list --resource-group $NODE_RG --lb-name kubernetes -o table`

The following example output shows that automatic outbound port assignment based on backend pool size is enabled for the cluster:

`AllocatedOutboundPorts EnableTcpReset IdleTimeoutInMinutes Name Protocol ProvisioningState ResourceGroup ------------------------ ---------------- ---------------------- --------------- ---------- ------------------- ------------- 0 True 30 aksOutboundRule All Succeeded MC_myResourceGroup_myAKSCluster_eastus`


### Calculate and verify outbound ports and IPs needed

Before setting a specific value or increasing an existing value for either outbound ports or outbound IP addresses, you must calculate the appropriate number of outbound ports and IP addresses. Use the following equation for this calculation rounded to the nearest integer: `64,000 ports per IP / <outbound ports per node> * <number of outbound IPs> = <maximum number of nodes in the cluster>`

.

#### Considerations for calculating outbound ports and IPs

When calculating the number of outbound ports and IPs and setting the values, keep the following information in mind:

- The number of outbound ports per node is fixed based on the value you set.
- The value for outbound ports must be a multiple of 8.
- Adding more IPs doesn't add more ports to any node, but it provides capacity for more nodes in the cluster.
- You must account for nodes that might be added as part of upgrades, including the count of nodes specified via
and`maxCount`

values.`maxSurge`


#### Examples of calculating outbound ports and IPs

The following examples show how the values you set affect the number of outbound ports and IP addresses:

- If the default values are used and the cluster has 48 nodes, each node has 1024 ports available.
- If the default values are used and the cluster scales from 48 to 52 nodes, each node is updated from 1024 ports available to 512 ports available.
- If the number of outbound ports is set to 1,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 128 nodes:
`64,000 ports per IP / 1,000 ports per node * 2 IPs = 128 nodes`

. - If the number of outbound ports is set to 1,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 448 nodes:
`64,000 ports per IP / 1,000 ports per node * 7 IPs = 448 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 32 nodes:
`64,000 ports per IP / 4,000 ports per node * 2 IPs = 32 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 112 nodes:
`64,000 ports per IP / 4,000 ports per node * 7 IPs = 112 nodes`

.

Important

After calculating the number of outbound ports and IPs, verify you have extra outbound port capacity to handle node surge during upgrades. It's critical to allocate sufficient excess ports for extra nodes needed for upgrade and other operations. AKS defaults to *one* buffer node for upgrade operations. If you're using [ maxSurge values](upgrade-aks-cluster#customize-node-surge-upgrade), multiply the outbound ports per node by your

`maxSurge`

value to determine the number of ports required. For example, if you calculate that you need 4000 ports per node with 7 IP addresses on a cluster with a maximum of 100 nodes and a max surge of 2:- 2 surge nodes * 4000 ports per node = 8000 ports needed for node surge during upgrades.
- 100 nodes * 4000 ports per node = 400,000 ports required for your cluster.
- 7 IPs * 64000 ports per IP = 448,000 ports available for your cluster.

This example shows the cluster has an excess capacity of 48,000 ports, which is sufficient to handle the 8000 ports needed for node surge during upgrades.

### Set the allocated outbound ports and outbound IPs

Once the values have been calculated and verified, you can apply those values using `load-balancer-outbound-ports`

and either `load-balancer-managed-outbound-ip-count`

, `load-balancer-outbound-ips`

, or `load-balancer-outbound-ip-prefixes`

when creating or updating a cluster.

-
[Create a new cluster with specific outbound ports and IPs](#tabpanel_5_create-cluster-outbound-ports-ips) -
[Update an existing cluster with specific outbound ports and IPs](#tabpanel_5_update-cluster-outbound-ports-ips)

Create a new AKS cluster with specific outbound ports and IPs using the

command. The following example sets the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter to*7*and the`--load-balancer-outbound-ports`

parameter to*4000*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 7 \ --load-balancer-outbound-ports 4000 \ --generate-ssh-keys`


## Configure the load balancer idle timeout

When SNAT port resources are exhausted, outbound flows fail until existing flows release SNAT ports. Load balancer reclaims SNAT ports when the flow closes, and the AKS-configured load balancer uses a 30-minute idle timeout for reclaiming SNAT ports from idle flows. You can also use transport (for example, ** TCP keepalives** or

**) to refresh an idle flow and reset this idle timeout if necessary.**

`application-layer keepalives`

If you expect to have numerous short-lived connections and no long-lived connections that might have long times of idle, like using `kubectl proxy`

or `kubectl port-forward`

, consider using a low timeout value such as *4 minutes*. When using TCP keepalives, it's sufficient to enable them on one side of the connection. For example, it's sufficient to enable them on the server side only to reset the idle timer of the flow. It's not necessary for both sides to start TCP keepalives. Similar concepts exist for application layer, including database client-server configurations. Check the server side for what options exist for application-specific keepalives.

Important

AKS enables *TCP Reset* on idle by default. We recommend you keep this configuration and leverage it for more predictable application behavior on your scenarios. For more information, see [Azure load balancer TCP reset](/en-us/azure/load-balancer/load-balancer-tcp-reset).

When setting *IdleTimeoutInMinutes* to a different value than the default of 30 minutes, consider how long your workloads need an outbound connection. Also consider that the default timeout value for a *Standard* SKU load balancer used outside of AKS is *4 minutes*. An *IdleTimeoutInMinutes* value that more accurately reflects your specific AKS workload can help decrease SNAT exhaustion caused by tying up connections no longer being used.

Warning

Altering the values for *AllocatedOutboundPorts* and *IdleTimeoutInMinutes* might significantly change the behavior of the outbound rule for your load balancer and shouldn't be done lightly. See [Troubleshoot SNAT](troubleshoot-source-network-address-translation) and review the [Load balancer outbound rules](/en-us/azure/load-balancer/load-balancer-outbound-connections#outboundrules) and [outbound connections in Azure](/en-us/azure/load-balancer/load-balancer-outbound-connections) before updating these values to fully understand the impact of your changes.

-
[Create a new cluster with a specific idle timeout](#tabpanel_6_create-cluster-idle-timeout) -
[Update an existing cluster with a specific idle timeout](#tabpanel_6_update-cluster-idle-timeout)

Create a new AKS cluster with a specific idle timeout using the

command with the`az aks create`

`--load-balancer-idle-timeout`

parameter. The following example sets the idle timeout to*4 minutes*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-idle-timeout 4 \ --generate-ssh-keys`


## Restrict inbound traffic to specific IP ranges

The following manifest uses `loadBalancerSourceRanges`

to specify a new IP range for inbound external traffic:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-vote-front
loadBalancerSourceRanges:
- MY_EXTERNAL_IP_RANGE
```


This example updates the rule to allow inbound external traffic only from the `MY_EXTERNAL_IP_RANGE`

range. If you replace `MY_EXTERNAL_IP_RANGE`

with the internal subnet IP address, traffic is restricted to only cluster internal IPs. If traffic is restricted to cluster internal IPs, clients outside your Kubernetes cluster are unable to access the load balancer.

Note

Keep the following information in mind when restricting inbound traffic:

- When you need to allow both CIDR blocks and Azure service tags, remove the
`loadBalancerSourceRanges`

property and add the`service.beta.kubernetes.io/azure-allowed-ip-ranges`

and/or`service.beta.kubernetes.io/azure-allowed-service-tags`

Load Balancer annotations. This configuration applies filtering only at the NSG layer and skips host-level kube-proxy rules. If you set the`loadBalancerSourceRanges`

property together with the`azure-allowed-service-tags`

annotation, AKS will report an error when you attempt to apply the specification. - Inbound, external traffic flows from the load balancer to the VNet for your AKS cluster. The VNet has a network security group (NSG) which allows all inbound traffic from the load balancer. This NSG uses a
[service tag](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)of type*LoadBalancer*to allow traffic from the load balancer. - Pod CIDR should be added to
`loadBalancerSourceRanges`

if there are Pods needing to access the service's Load Balancer IP for clusters with Kubernetes version 1.25 or higher.

## Maintain the client's IP on inbound connections

By default, a service of type `LoadBalancer`

[in Kubernetes](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-type-loadbalancer) and in AKS doesn't persist the client's IP address on the connection to the pod. The source IP on the packet that's delivered to the pod becomes the private IP of the node. To maintain the client's IP address, you must set `service.spec.externalTrafficPolicy`

to `local`

in the service definition. The following manifest shows an example:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
externalTrafficPolicy: Local
ports:
- port: 80
selector:
app: azure-vote-front
```


## Customizations via Kubernetes Annotations

The following annotations are supported for Kubernetes services with type `LoadBalancer`

, and they only apply to **INBOUND** flows.

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-internal` |
`true` or `false` |
Specify whether the load balancer should be internal. If not set, it defaults to public. |
`service.beta.kubernetes.io/azure-load-balancer-internal-subnet` |
Name of the subnet | Specify which subnet the internal load balancer should be bound to. If not set, it defaults to the subnet configured in cloud config file. |
`service.beta.kubernetes.io/azure-dns-label-name` |
Name of the DNS label on Public IPs | Specify the DNS label name for the public service. If it's set to an empty string, the DNS entry in the Public IP isn't used. |
`service.beta.kubernetes.io/azure-shared-securityrule` |
`true` or `false` |
Specify exposing the service through a potentially shared Azure security rule to increase service exposure, utilizing Azure
|

`service.beta.kubernetes.io/azure-load-balancer-resource-group`

`service.beta.kubernetes.io/azure-allowed-service-tags`

[service tags](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)separated by commas.`service.beta.kubernetes.io/azure-allowed-ip-ranges`

`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

`true`

or `false`

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

`service.beta.kubernetes.io/azure-load-balancer-ipv6`

### Customize allowed IP ranges (preview)

You can use the `azure-allowed-service-tags`

and `azure-allowed-ip-ranges`

annotations to combine CIDR blocks and Azure service tags on the load balancer. Add `service.beta.kubernetes.io/azure-allowed-ip-ranges`

with a comma-separated list of IP prefixes, and add `service.beta.kubernetes.io/azure-allowed-service-tags`

with one or more Azure service tags. The AKS cloud provider merges both values into a single NSG rule, so traffic is filtered centrally at the NSG giving you a single, NSG-centric control plane for both IP addresses and service tags.

You can continue to use the `loadBalancerSourceRanges`

property for cases where you want CIDR-based restrictions enforced both in the NSG and the host. You can't use this property with the `azure-allowed-service-tags`

annotation. If both are specified, AKS reports an error when you try to apply the load balancer service specification.

### Customize the load balancer health probe

The following annotations are supported to customize the load balancer health probe behavior:

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
Health probe interval | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
The minimum number of unhealthy responses of health probe | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
Request path of the health probe | |
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
true/false | {port} is service port number. When set to `true` , no load balancer or health probe rules for this port are generated. Health check service shouldn't be exposed to the public internet. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
true/false | {port} is service port number. When set to `true` , no health probe rules for this port are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
Health probe protocol | {port} is service port number. Explicit protocol for the health probe for the service port {port}, overriding port.appProtocol if set. |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
port number or port name in service manifest | {port} is service port number. Explicit port for the health probe for the service port {port}, overriding the default value. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
Health probe interval | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
The minimum number of unhealthy responses of health probe | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
Request path of the health probe | {port} is service port number. |

Note

AKS now supports shared health probes for `externalTrafficPolicy: Cluster`

Services. To learn more, see [Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)](shared-health-probes).

#### Default health probe behavior

Currently, the default protocol of the health probe varies among services with different transport protocols, app protocols, annotation, and external traffic policies.

- For local services, HTTP and /healthz would be used. The health probe will query
`NodeHealthPort`

rather than actual backend service. - For cluster TCP services, TCP would be used.
- For cluster UDP services, no health probes.

Note

For local services with PLS integration and PLS proxy protocol enabled, the default HTTP and /healthz health probe doesn't work. Thus health probe can be customized the same way as cluster services to support this scenario.

##### Health probe request path annotation

Starting in Kubernetes version 1.20, the service annotation `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

was introduced to determine the health probe behavior.

- For clusters <=1.23,
`spec.ports.appProtocol`

would only be used as probe protocol when`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is also set. - For clusters >1.24,
`spec.ports.appProtocol`

would be used as probe protocol and`/`

would be used as default probe request path (`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

could be used to change to a different request path).

Note that the request path would be ignored when using TCP or the `spec.ports.appProtocol`

is empty. The following table summarizes the default health probe behavior:

| loadbalancer sku | `externalTrafficPolicy` |
spec.ports.Protocol | spec.ports.AppProtocol | `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
LB probe protocol | LB probe request path |
|---|---|---|---|---|---|---|
| standard | local | any | any | any | http | `/healthz` |
| standard | cluster | udp | any | any | null | null |
| standard | cluster | tcp | (ignored) | tcp | null | |
| standard | cluster | tcp | tcp | (ignored) | tcp | null |
| standard | cluster | tcp | http/https | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| standard | cluster | tcp | http/https | `/custom-path` |
http/https | `/custom-path` |
| standard | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |
| basic | local | any | any | any | http | `/healthz` |
| basic | cluster | tcp | (ignored) | tcp | null | |
| basic | cluster | tcp | tcp | (ignored) | tcp | null |
| basic | cluster | tcp | http | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| basic | cluster | tcp | http | `/custom-path` |
http | `/custom-path` |
| basic | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |

##### Health probe interval and number of probes annotations

Starting in Kubernetes version 1.21, two service annotations `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

and `load-balancer-health-probe-num-of-probe`

were introduced, which customize the configuration of health probe. If `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

isn't set, a default value of *5* is applied. If `load-balancer-health-probe-num-of-probe`

isn't set, a default value of *2* is applied.

### Custom Load Balancer health probe for port

Different ports in a service can require different health probe configurations. This could be because of service design (such as a single health endpoint controlling multiple ports), or Kubernetes features like the [MixedProtocolLBService](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancers-with-mixed-protocol-types).

The following table summarizes the port-specific annotations that can be used to override the global health probe annotations for a specific port in the service:

| Port-specific annotation | Global probe annotation | Behavior |
|---|---|---|
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
N/A (no equivalent globally) | If set to `true` , no load balancer or probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
N/A (no equivalent globally) | If set to `true` , no probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
N/A (no equivalent globally) | Sets the health probe protocol for this service port (for example: Http, Https, Tcp). |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
N/A (no equivalent globally) | Sets the health probe port for this service port (for example: 15021). |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
For Http or Https, sets the health probe request path (defaults to /). |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
Number of consecutive probe failures before the port is considered unhealthy. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
The amount of time between probe attempts. |

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

To learn more about using internal load balancer for inbound traffic, see the [AKS internal load balancer documentation](internal-lb).


---

<!-- DOCUMENTO FUSIONADO: supported-kubernetes-versions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/supported-kubernetes-versions -->

# Supported Kubernetes versions in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community [releases minor versions](https://kubernetes.io/releases/) roughly every four months.

Minor version releases include new features and improvements. Patch releases are more frequent (sometimes weekly) and are intended for critical bug fixes within a minor version. Patch releases include fixes for security vulnerabilities or major bugs.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Kubernetes versions

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme for each version:

```
[major].[minor].[patch]
Examples:
1.29.2
1.29.1
```


Each number in the version reflects compatibility with previous versions:

**Major versions**: Introduce incompatible API changes or break backward compatibility.**Minor versions**: Add new features while maintaining backward compatibility.**Patch versions**: Include backward-compatible bug fixes.

Always use the latest patch release for your current minor version. For example, if your production cluster is on ** 1.29.1** and

**is the latest available patch version available for the**

`1.29.2`

*1.29*minor version, you should upgrade to

**as soon as possible to ensure your cluster is fully patched and supported.**

`1.29.2`

## AKS Kubernetes release calendar

Check the AKS Kubernetes release calendar for upcoming version releases. To see real-time updates of region release status and version release notes, visit the [AKS release status webpage](https://releases.aks.azure.com/). To learn more about the release status webpage, see [AKS release tracker](release-tracker).

Note

Note

AKS follows a 12-month support policy for generally available (GA) Kubernetes versions. To learn more about our Kubernetes version support policy, see the [FAQ](supported-kubernetes-versions#faq). Unless an explicit date is provided, the End of Life (EOL) date is the last day of the specified month. For example, "Mar 2026" indicates March 31, 2026.

For the past release history, see [Kubernetes history](https://github.com/kubernetes/kubernetes/releases).

| K8s version | Upstream release | AKS preview | AKS GA | End of life | Platform support |
|---|---|---|---|---|---|
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Until 1.33 GA |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Until 1.34 GA |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Until 1.35 GA |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Until 1.36 GA |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Until 1.37 GA |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Until 1.38 GA |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Until 1.39 GA |

### LTS Versions

Long-term support (LTS) needs to be enabled in order to get extended support. You can find more information on [Enable long-term support](/en-us/azure/aks/long-term-support#enable-long-term-support).

Note

Azure Linux 2.0 goes End of Life during the LTS period of AKS v1.28–v1.31. For more information on upgrading to Azure Linux 3.0 on AKS v1.28–v1.31, read the [Azure Linux AKS LTS Releases](/en-us/azure/azure-linux/support-cycle#aks-lts-releases) section.

| K8s version | Upstream release | AKS preview | AKS GA | End of life | LTS End of life |
|---|---|---|---|---|---|
| 1.27 | Apr 2023 | Jun 2023 | Jul 2023 | Jul 2024 | Jul 2025 |
| 1.28 | Aug 2023 | Sep 2023 | Nov 2023 | Jan 2025 | Feb 2026 |
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Apr 2026 |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Jul 2026 |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Nov 2026 |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Mar 2027 |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Jun 2027 |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Nov 2027 |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Mar 2028 |

### AKS Kubernetes release schedule Gantt chart

If you prefer to see this information visually, here's a Gantt chart with all the current releases displayed:

## AKS components breaking changes by version

Note the following important changes before you upgrade to any of the available minor versions:

### Kubernetes 1.34

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| aci-connector-linux 1.6.2 | addon-override-manager master.251002.2 | Linux - Ubuntu 22.04 |
kube-egress-gateway-daemon v0.0.21 → v0.1.3 | |
| addon-resizer v1.8.23-7 | apiserver-network-proxy-server v0.31.4-3 | azure-acr-credential-provider-pmc 1.34.1-ubuntu22.04u3 | kube-egress-gateway-daemon-init v0.0.21 → v0.1.3 | |
| ai-toolchain-operator 0.6.0 | app-routing-operator 0.2.12 | containerd 1.7.29-ubuntu22.04u1 | kube-egress-gateway-cnimanager v0.0.21 → v0.1.3 | |
| aks-windows-gpu-device-plugin 0.0.19 | automatic-authz-webhook master.251112.4 | datacenter-gpu-manager-4-core 1:4.4.1-1 | kube-egress-gateway-cni v0.0.21 → v0.1.3 | |
| ama-logs-linux 3.1.31 | ccp-webhook master.251105.4 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | kube-egress-gateway-cni-ipam v0.0.21 → v0.1.3 | |
| ama-logs-win win-3.1.31 | cluster-autoscaler v1.33.1-aks-3 | kubectl 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-windows v1.33.3 → v1.34.0 | |
| app-routing-operator 0.0.3 | cost-analysis-scraper v0.0.25 | kubelet 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-linux v1.33.3 → v1.34.0 | |
| azure-monitor-metrics-cfg-reader 6.24.0-main | customer-net-probe master.250827.1 | kubernetes-cri-tools 1.32.0-ubuntu22.04u3 | metrics-server v0.7.2-10 → v0.8.0-4 | |
| azure-monitor-metrics-ksm v2.17.0 | envoy v1.35.6-master.251017.3 | nvidia-device-plugin 0.18.0-ubuntu22.04u2 | overlay-vpa v1.2.1-1 → v1.5.1-1 | |
| azure-monitor-metrics-linux 6.24.0-main | ingress-dispatcher v1.35.6-master.251017.3 | runc 1.3.3-ubuntu22.04u1 | coredns v1.12.1-7 → v1.13.1-2 | |
| azure-monitor-metrics-target-allocator | jwt-authenticator-egress master.250904.1 | Linux - AzureLinux 3.0 |
kube-egress-gateway-controller v0.0.21 → v0.1.3 | |
| azure-monitor-metrics-windows | kube-state-metrics v2.15.0-4 | azure-acr-credential-provider-pmc 1.34.1-1.azl3 | ||
| azure-npm-image v1.6.34 | kubeguard-guard v0.16.23 | containerd 2.0.0-14.azl3 | ||
| azure-npm-image-windows v1.5.5 | private-connect-balancer master.250731.2 | datacenter-gpu-manager-4-core 1:4.4.1-1 | ||
| azure-policy 1.15.1 | private-connect-router master.251105.2 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | ||
| azure-policy-audit 1.15.1 | gpu-provisioner 0.3.7 (plugin) | dcgm-exporter 4.6.0-1.azl3 | ||
| azure-policy-webhook 1.15.1 | karpenter 1.6.5-aks (plugin) | kubectl 1.34.1-4.azl3 | ||
| certgen v0.1.9 | kms-controller master.250811.2 (plugin) | kubelet 1.34.1-4.azl3 | ||
| cilium-agent 1.14.10-1 | kms-operator master.250814.1 (plugin) | kubernetes-cri-tools 1.32.0-3.azl3 | ||
| cilium-envoy v1.31.5-250218 | kms-plugin-v2-plus master.251114.2 (plugin) | nvidia-container-toolkit 1.17.3 | ||
| cilium-operator-generic 1.14.10 | kube-egress-gateway-controller v0.1.3 | nvidia-device-plugin 0.18.0-2.azl3 | ||
| cloud-provider-node-manager-linux v1.34.0 | kubelet-serving-csr-approver v0.0.7 | Windows - Windows2022 |
||
| cloud-provider-node-manager-windows v1.34.0 | live-patching-controller v0.0.16 | containerd v2.0.4-azure.1 | ||
| ... | secure-tls-bootstrap-server v0.0.9 |

### Kubernetes 1.33

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| * aci-connector-linux 1.6.2 * addon-resizer v1.8.23-2 * ai-toolchain-operator 0.4.5 * aks-windows-gpu-device-plugin 0.0.19 * ama-logs-linux 3.1.26 * ama-logs-win win-3.1.26 * app-routing-operator 0.0.3 * azure-monitor-metrics-cfg-reader 6.16.0-main-04-15-2025-d78050c6-cfg * azure-monitor-metrics-ksm v2.15.0-4 * azure-monitor-metrics-linux 6.16.0-main-04-15-2025-d78050c6 * azure-monitor-metrics-target-allocator 6.16.0-main-04-15-2025-d78050c6-targetallocator * azure-monitor-metrics-windows 6.16.0-main-04-15-2025-d78050c6-win * azure-npm-image v1.5.45 * azure-npm-image-windows v1.5.5 * azure-policy 1.10.1 * azure-policy-webhook 1.10.0 * certgen v0.1.9 * cilium-agent 1.14.10-1 * cilium-envoy v1.31.5-250218 * cilium-operator-generic 1.14.10 * cloud-provider-node-manager-linux v1.33.0 * cloud-provider-node-manager-windows v1.33.0 * cluster-proportional-autoscaler v1.9.0-1 * container-networking-cilium-agent v1.16.6-250129 * container-networking-cilium-operator-generic v1.16.6-250129 * coredns v1.12.1-1 * cost-analysis-agent v0.0.23 * cost-analysis-opencost v1.111.0 * cost-analysis-prometheus v2.54.1 * cost-analysis-victoria-metrics v1.103.0 * extension-config-agent 1.23.3 * extension-manager 1.23.3 * fqdn-policy v1.16.6-250129 * gpu-provisioner 0.3.3 * health-probe-proxy v1.29.1 * hubble-relay v1.15.0 * image-cleaner v1.3.1 * ingress-appgw 1.8.1 * ip-masq-agent-v2 v0.1.15-2 * ipv6-hp-bpf v0.0.1 * keda v2.16.1 * keda-admission-webhooks v2.16.1 * keda-metrics-apiserver v2.16.1 * kube-egress-gateway-cni v0.0.20 * kube-egress-gateway-cni-ipam v0.0.20 * kube-egress-gateway-cnimanager v0.0.20 * kube-egress-gateway-daemon v0.0.20 * kube-egress-gateway-daemon-init v0.0.20 * metrics-server v0.7.2-6 * microsoft-defender-admission-controller 20250325.2 * microsoft-defender-low-level-collector 2.0.205 * microsoft-defender-low-level-init 1.3.81 * microsoft-defender-old-file-cleaner 1.0.214 * microsoft-defender-pod-collector 1.0.177 * microsoft-defender-security-publisher 1.0.211 * open-policy-agent-gatekeeper v3.18.2-1 * osm-bootstrap v1.2.9 * osm-controller v1.2.9 * osm-crds v1.2.9 * osm-healthcheck v1.2.9 * osm-init v1.2.9 * osm-injector v1.2.9 * osm-sidecar v1.32.2-hotfix.20241216 * overlay-vpa 1.2.1 * overlay-vpa-webhook-generation master.250430.1 * ratify-base v1.2.3 * retina-agent v0.0.31 * retina-agent-enterprise v0.1.9 * retina-agent-win v0.0.31 * retina-operator v0.1.9 * secrets-store-csi-driver v1.4.8 * secrets-store-csi-driver-windows v1.4.8 * secrets-store-driver-registrar-linux v2.11.1 * secrets-store-driver-registrar-windows v2.11.1 * secrets-store-livenessprobe-linux v2.13.1 * secrets-store-livenessprobe-windows v2.13.1 * secrets-store-provider-azure v1.6.2 * secrets-store-provider-azure-windows v1.6.2 * sgx-attestation 3.3.1 * sgx-plugin 1.0.0 * sgx-webhook 1.2.2 * tigera-operator v1.36.7 * windows-gmsa-webhook-image v0.12.1-2 * workload-identity-webhook v1.5.0 |
* addon-override-manager master.250116.1 * apiserver-network-proxy-server v0.30.3-hotfix.20240819 * app-routing-operator 0.2.5 * ccp-webhook master.250509.3 * cluster-autoscaler v1.32.1-aks * cost-analysis-scraper v0.0.23 * customer-net-probe master.250430.1 * envoy v1.31.5-master.241218.3 * ingress-dispatcher v1.31.5-master.250126.7 * kube-state-metrics v2.15.0-4 * gpu-provisioner 0.3.3 * karpenter 0.7.3-aks * kube-egress-gateway-controller v0.0.20 * kubelet-serving-csr-approver v0.0.7 * live-patching-controller v0.0.8 |
* Linux - Ubuntu 22.04 * containerd 1.7.27-ubuntu22.04u1 * kubernetes-cri-tools 1.32.0-ubuntu22.04u3 * runc 1.2.6-ubuntu22.04u1 * Linux - AzureLinux 3.0 * containerd 2.0.0-4.azl3 * nvidia-container-toolkit 1.17.3 * Windows - Windows2022 * containerd v1.7.20-azure.1 |
* coredns v1.11.3-7 → v1.12.1-1 * cloud-provider-node-manager-windows v1.32.5 → v1.33.0 * cloud-provider-node-manager-linux v1.32.5 → v1.33.0 |
N/A |

### Kubernetes 1.32

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.17.0 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.34.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.31

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.16.6 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.30.11 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.30

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * App routing operator v0.2.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 *
|
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 | N/A |

### Kubernetes 1.29

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * csi-provisioner v4.0.0 * App routing operator v0.2.1 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 * azurefile-csi-driver 1.29.3 |
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 * csi-provisioner v4.0.0 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 |
N/A |

## Alias minor version

Note

Alias minor version requires Azure CLI version 2.37 or above and API version 20220401 or above. Use `az upgrade`

to install the latest version of the CLI.

You can create an AKS cluster without specifying a patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. For example, if you create a cluster with ** 1.29** and

**is the latest GA would patch available, your cluster is created with**

`1.29.2`

**. If you want to upgrade your patch version in the same minor version, use**

`1.29.2`

[autoupgrade](auto-upgrade-cluster).

To see what patch you're on, run the `az aks show --resource-group myResourceGroup --name myAKSCluster`

command. The `currentKubernetesVersion`

property shows the whole Kubernetes version.

```
{
"apiServerAccessProfile": null,
"autoScalerProfile": null,
"autoUpgradeProfile": null,
"azurePortalFqdn": "myaksclust-myresourcegroup.portal.hcp.eastus.azmk8s.io",
"currentKubernetesVersion": "1.29.2",
}
```


## Kubernetes version support policy

AKS defines a generally available (GA) version as a version available in all regions and enabled in all SLO or SLA measurements. AKS supports three GA minor versions of Kubernetes:

AKS supports three GA minor versions:

- The latest GA version (N).
- The two previous minor versions (N-1 and N-2).
- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the
[AKS release status webpage](release-tracker).

- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the

AKS might also support preview versions, which are explicitly labeled and subject to [preview terms and conditions](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

AKS provides platform support only for one GA minor version of Kubernetes after the regular supported versions. The platform support window of Kubernetes versions on AKS is known as "N-3". For more information, see [platform support policy](#platform-support-policy).

Note

AKS uses safe deployment practices that involve gradual region deployment. This means it might take up to 10 business days for a new release or a new version to be available in all regions.

The supported window of Kubernetes minor versions on AKS is known as "N-2", where N refers to the latest release, meaning that two previous minor releases are also supported.

For example, on the day that AKS introduces version 1.29, support is provided for the following versions:

| New minor version | Supported Minor Version List |
|---|---|
| 1.29 | 1.29, 1.28, 1.27 |

When a new minor version is introduced, the oldest minor version is deprecated and removed. For example, let's say the current supported minor version list is:

```
1.29
1.28
1.27
```


When AKS releases 1.30, all the 1.27 versions go out of support 30 days later.

AKS might support any number of **patches** based on upstream community release availability for a given minor version. AKS reserves the right to deprecate any of these patches at any given time due to a CVE or potential bug concern. You're always encouraged to use the latest patch for a minor version.

## Platform support policy

Platform support policy is a reduced support plan for certain unsupported Kubernetes versions. During platform support, customers only receive support from Microsoft for AKS/Azure platform related issues. Any issues related to Kubernetes functionality and components aren't supported.

Platform support policy applies to clusters in an n-3 version (where n is the latest supported AKS GA minor version), before the cluster drops to n-4. For example, Kubernetes v1.26 is considered platform support when v1.29 is the latest GA version. If you're a running an n-2 version, the moment it becomes n-3 , the version also becomes end of official support, and you enter into the platform support policy.

AKS relies on the releases and patches from [Kubernetes](https://kubernetes.io/releases/), which is an Open Source project that only supports a sliding window of three minor versions. AKS can only guarantee [full support](#kubernetes-version-support-policy) while those versions are being serviced upstream. Since there's no more patches being produced upstream, AKS can either leave those versions unpatched or fork. Due to this limitation, platform support doesn't support anything from relying on Kubernetes upstream.

This table outlines support guidelines for Community Support compared to Platform support.

| Support category | Community Support (N-2) | Platform Support (N-3) |
|---|---|---|
| Upgrades from N-3 to a supported version | Supported | Supported |
| Platform (Azure) availability | Supported | Supported |
| Node pool scaling | Supported | Supported |
| VM availability | Supported | Supported |
| Storage, Networking related issues | Supported | Supported except for bug fixes and retired components |
| Start/stop | Supported | Supported |
| Rotate certificates | Supported | Supported |
| Infrastructure SLA | Supported | Supported |
| Control Plane SLA | Supported | Supported |
| Platform (AKS) SLA | Supported | Not supported |
| Kubernetes components (including Add-ons) | Supported | Not supported |
| Component updates | Supported | Not supported |
| Component hotfixes | Supported | Not supported |
| Applying bug fixes | Supported | Not supported |
| Applying security patches | Supported | Not supported |
| Kubernetes API support | Supported | Not supported |
| Node pool creation | Supported | Supported |
| Cluster creation | Supported | Not Supported |
| Node pool snapshot | Supported | Not supported |
| Node image upgrade | Supported | Supported |

Note

The table is subject to change and outlines common support scenarios. Any scenarios related to Kubernetes functionality and components aren't supported for N-3. For further support, see [Support and troubleshooting for AKS](aks-support-help).

### Supported `kubectl`

versions

You can use a `kubectl`

version that is one minor version older or newer than your kube-apiserver version, [Kubernetes support policy for kubectl](https://kubernetes.io/docs/setup/release/version-skew-policy/#kubectl).

For example, if your *kube-apiserver* is at *1.28*, then you can use versions *1.27* to *1.29* of `kubectl`

with that *kube-apiserver*.

To install or update `kubectl`

to the latest version, run:

```
az aks install-cli
```


## Long Term Support (LTS)

AKS offers one year of Community Support and one year of Long Term Support (LTS), including backported security fixes from the upstream community. Our upstream LTS working group contributes efforts back to the community to provide our customers with a longer support window.

For more information on LTS, see [Long term support for Azure Kubernetes Service (AKS)](long-term-support).

## Release and deprecation process

You can reference upcoming version releases and deprecations on the [AKS Kubernetes release calendar](#aks-kubernetes-release-calendar).

For new **minor** versions of Kubernetes:

- AKS announces new version release dates and old version deprecation in the
[AKS Release notes](https://aka.ms/aks/releasenotes)at least 30 days before removal. - AKS uses
[Azure Advisor](/en-us/azure/advisor/advisor-overview)to alert you if a new version could cause issues in your cluster because of deprecated APIs. Azure Advisor also alerts you if you're out of support - AKS publishes a
[service health notification](/en-us/azure/service-health/service-health-overview)available to all users with AKS and portal access and sends an email to the subscription administrators with the planned version removal dates.Note

To find out who is your subscription administrators or to change it, refer to

[manage Azure subscriptions](/en-us/azure/cost-management-billing/manage/add-change-subscription-administrator#assign-a-subscription-administrator). - You have
**30 days**from version removal to upgrade to a supported minor version release to continue receiving support.

For new **patch** versions of Kubernetes:

- Because of the urgent nature of patch versions, they can be introduced into the service as they become available. Once available, patches have a two month minimum lifecycle.
- In general, AKS doesn't broadly communicate the release of new patch versions. However, AKS constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, AKS notifies you to upgrade to the newly available patch.
- You have
**30 days**from a patch release's removal from AKS to upgrade into a supported patch and continue receiving support. However, you'll**no longer be able to create clusters or node pools once the version is deprecated/removed.**

### Supported versions policy exceptions

AKS reserves the right to add or remove new/existing versions with one or more critical production-impacting bugs or security issues without advance notice.

Specific patch releases might be skipped or rollout accelerated, depending on the severity of the bug or security issue.

## Azure portal and CLI versions

If you deploy an AKS cluster with Azure portal, Azure CLI, Azure PowerShell, the cluster defaults to the N-1 minor version and latest patch. For example, if AKS supports *1.29.2*, *1.29.1*, *1.28.7*, *1.28.6*, *1.27.11*, and *1.27.10*, the default version selected is *1.28.7*.

To find out what versions are currently available for your subscription and region, use the
[ az aks get-versions](/en-us/cli/azure/aks#az-aks-get-versions) command. The following example lists the available Kubernetes versions for the

*EastUS*region:

```
az aks get-versions --location eastus --output table
```


## FAQ

### How does Microsoft notify me of new Kubernetes versions?

The AKS team announces new Kubernetes version release dates in our documentation, on [GitHub](https://github.com/Azure/AKS/releases), and via email to subscription administrators with clusters nearing end of support. AKS also uses [Azure Advisor](/en-us/azure/advisor/advisor-overview) to alert you inside the Azure portal if you're out of support and inform you of deprecated APIs that can affect your application or development process.

### How often should I expect to upgrade Kubernetes versions to stay in support?

Starting with Kubernetes 1.19, the [open source community expanded support to one year](https://kubernetes.io/blog/2020/08/31/kubernetes-1-19-feature-one-year-support/). AKS commits to enabling patches and support matching the upstream commitments. For AKS clusters on 1.19 and greater, you can upgrade at a minimum of once a year to stay on a supported version.

**What happens when you upgrade a Kubernetes cluster with a minor version that isn't supported?**

If you're on the *n-3* version or older, it means you're outside of support and need to upgrade. If your upgrade from version n-3 to n-2 succeeds, you're back within our support policies. For example:

- If the oldest supported AKS minor version is
*1.27*and you're on*1.26*or older, you're outside of support. - If you successfully upgrade from
*1.26*to*1.27*or higher, you're back within our support policies.

Downgrades aren't supported.

### What does 'Outside of Support' mean?

'Outside of Support' means that:

- The version you're running is outside of the supported versions list.
- You'll be asked to upgrade the cluster to a supported version when requesting support, unless you're within the 30-day grace period after version deprecation.

Additionally, AKS doesn't make any runtime or other guarantees for clusters outside of the supported versions list.

### What happens when you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### Can you stay on a Kubernetes version forever?

If a cluster is out of support for more than three minor versions and carries security risks, Azure proactively contacts you. They advise you to upgrade your cluster. If you don't take further action, Azure reserves the right to automatically upgrade your cluster on your behalf.

### What happens if you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### What version does the control plane support if the node pool isn't in one of the supported AKS versions?

The control plane must be within a window of versions from all node pools. For details on upgrading the control plane or node pools, visit documentation on [upgrading node pools](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools).

### What is the allowed difference in versions between control plane and node pool?

The [version skew policy](https://kubernetes.io/releases/version-skew-policy/) now allows a difference of up to three versions between control plane and agent pools. AKS follows this skew version policy change starting from version 1.28 onwards.

### Can I skip multiple AKS versions during cluster upgrade?

If you upgrade a supported AKS cluster, Kubernetes minor versions can't be skipped. Kubernetes control planes [version skew policy](https://kubernetes.io/releases/version-skew-policy/) doesn't support minor version skipping. For example, upgrades between:

*1.28.x*->*1.29.x*: allowed.*1.27.x*->*1.28.x*: allowed.*1.27.x*->*1.29.x*: not allowed.

For control plane version upgrades, you can go up to three minor versions for community supported versions in sequential fashion.

To upgrade from *1.27.x* -> *1.29.x*:

- Upgrade from
*1.27.x*->*1.28.x*. - Upgrade from
*1.28.x*->*1.29.x*.

Note starting from 1.28 version onwards, agentpool versions can be up to three versions older to control plane versions per [version skew policy](https://kubernetes.io/releases/version-skew-policy/). If your version is much behind the minimum supported version, you might have to do more than one control plane upgrade operation to get to the minimum supported version. For example, if your current control plane version is *1.23.x* and you intend to upgrade to a minimum supported version of *1.27.x* as an example. You might have to upgrade sequentially four times from *1.23.x* in order to get to *1.27.x*. Also note that Agent pool versions can be upgraded to the control plane minor version. In the previous example you can upgrade agentpool version twice, once from *1.23.x* to *1.25.x*, when the control plane version is at *1.25.x*. And then from *1.25.x* to *1.27.x*, when control plane version is at *1.27.x*. When you upgrade in-place, like control plane and agent pool together the same rules applicable to control plane upgrade applies.

If performing an upgrade from an *unsupported version* the upgrade is done without any guarantee of functionality and is excluded from the service-level agreements and limited warranty. Clusters running *unsupported version* has the flexibility of decoupling control plane upgrades with node pool upgrades. However if your version is out of date, we recommend that you re-create the cluster.

### Can I create a new 1.xx.x cluster during the platform support window?

No, Creation of new clusters isn't possible during Platform Support period.

### I'm on a freshly deprecated version that is out of platform support, can I still add new node pools? Or should I upgrade?

Yes, you can add agent pools as long as they're compatible with the control plane version.

## Next steps

For information on how to upgrade your cluster, see:
