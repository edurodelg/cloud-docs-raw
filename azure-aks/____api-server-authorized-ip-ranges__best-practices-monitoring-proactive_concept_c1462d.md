---
merged_at: 2026-01-26T20:54:26.187426
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __api-server-authorized-ip-ranges__best-practices-monitoring-proactive_concepts-_eac95b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _api-server-authorized-ip-ranges__best-practices-monitoring-proactive_concepts-n_b2a4ed.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: api-server-authorized-ip-ranges.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges -->

# Secure access to the API server using authorized IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use API server authorized IP address ranges to limit which IP addresses and CIDRs can access control plane endpoints for your Azure Kubernetes Service (AKS) workloads.

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To learn what IP addresses to include when integrating your AKS cluster with Azure DevOps, see
[Allowed IP addresses and domain URLs](/en-us/azure/devops/organizations/security/allow-list-ip-url).

Tip

From the Azure portal, you can use Azure Copilot to make changes to the IP addresses that can access your cluster. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#enable-ip-address-authorization).

## Limitations and considerations

- This feature is only supported on the Standard SKU load balancer for clusters created after October 2019. Any existing clusters on the Basic SKU load balancer with the feature enabled should continue to work properly if the Kubernetes version and control plane are upgraded. However, you can't migrate these clusters to the Standard SKU load balancer.
- You can't use this feature with
[private clusters](private-clusters). - When using this feature with clusters that use
[Node public IPs](use-node-public-ips), the node pools using the Node public IPs must use public IP prefixes. You must add the public IP prefixes as authorized ranges. - You can specify up to 200 authorized IP ranges. To go beyond this limit, consider using
[API Server VNet Integration](api-server-vnet-integration), which supports up to 2,000 authorized IP ranges.

## Overview of API server authorized IP ranges

The Kubernetes API server exposes underlying Kubernetes APIs and provides the interaction for management tools like `kubectl`

and the Kubernetes dashboard. AKS provides a single-tenant cluster control plane with a dedicated API server. The API server is assigned a public IP address by default. You can control access using Kubernetes role-based access control (Kubernetes RBAC) or Azure RBAC.

To secure access to the otherwise publicly accessible AKS control plane / API server, you can enable and use authorized IP ranges. These authorized IP ranges only allow defined IP address ranges to communicate with the API server. Any requests made to the API server from an IP address that isn't part of these authorized IP ranges is blocked. The rules can take up to two minutes to propagate. Allow up to that time when testing the connection.

## Recommended IP ranges to allow

We recommend including the following IP address ranges in your API server authorized IP ranges configuration:

- The cluster egress IP address (firewall, NAT gateway, or other address, depending on your
[outbound type](egress-outboundtype)). - Any range that represents networks that you'll administer the cluster from.

## Create an AKS cluster with API server authorized IP ranges enabled

Note

When you enable API server authorized IP ranges during cluster creation, both the API server public IP and the outbound public IP of the [Standard SKU load balancer](load-balancer-standard) are automatically allowed by default, in addition to any ranges you specify.

**Special case - 0.0.0.0/32**: This is a special value that tells AKS to allow only the outbound public IP of the Standard SKU load balancer to access the API server. The

`0.0.0.0/32`

value acts as a placeholder that:- Disables the default behavior of allowing extra client IP ranges.
- Restricts API server access to only the cluster's own outbound IP.
- Is useful for scenarios where you want the cluster to self-manage but block external access.

When creating a cluster with API server authorized IP ranges enabled, you provide a list of authorized public IP address ranges. When you specify a CIDR range, you must use the network address (first IP address in the range). For example, if you want to allow the range `137.117.106.88`

to `137.117.106.95`

, you must specify `137.117.106.88/29`

.

Create an AKS cluster with API server authorized IP ranges enabled using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled using the

cmdlet with the`New-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '73.140.245.0/24' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter the IP address ranges you want to authorize to access the API server. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Specify outbound IPs for a Standard SKU load balancer

When creating a cluster with API server authorized IP ranges enabled, you can also specify the outbound IP addresses or prefixes for the cluster using the `--load-balancer-outbound-ips`

or `--load-balancer-outbound-ip-prefixes`

parameters. All IPs provided in the parameters are allowed along with the IPs in the `--api-server-authorized-ip-ranges`

parameter.

Create an AKS cluster with API server authorized IP ranges enabled and specify the outbound IP addresses for the Standard SKU load balancer using the

`--load-balancer-outbound-ips`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*, allows the IP address range`73.140.245.0/24`

to access the API server, and specifies two outbound IP addresses for the Standard SKU load balancer. Make sure to replace the placeholders`<public-ip-id-1>`

and`<public-ip-id-2>`

with the actual resource IDs of your public IP addresses.`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --load-balancer-outbound-ips <public-ip-id-1>,<public-ip-id-2> --generate-ssh-keys`


## Allow only the outbound public IP of the Standard SKU load balancer

Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 0.0.0.0/32 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '0.0.0.0/32' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter`0.0.0.0/32`

. This setting allows only the outbound public IP of the Standard SKU load balancer. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Update the API server authorized IP ranges on an existing cluster

Update an existing cluster's API server authorized IP ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24`


## Allow multiple IP address ranges

To allow multiple IP address ranges, you can list several IP addresses, separated by commas.

Update an existing cluster's API server authorized IP ranges to allow multiple IP address ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows multiple IP address ranges:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24,193.168.1.0/24,194.168.1.0/24`


Update an existing cluster's API server authorized IP ranges using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '73.140.245.0/24'`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, update the**Authorized IP ranges**as needed. - When you're done, select
**Save**.

## Disable API server authorized IP ranges on an existing cluster

Disable API server authorized IP ranges using the

command and specify an empty range`az aks update`

`""`

for the`--api-server-authorized-ip-ranges`

parameter.`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges ""`


Disable API server authorized IP ranges using the

cmdlet and specify an empty range`Set-AzAksCluster`

`''`

for the`-ApiServerAccessAuthorizedIpRange`

parameter.`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange ''`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, deselect the**Set authorized IP ranges**checkbox. - Select
**Save**.

## Find existing API server authorized IP ranges

Find existing API server authorized IP ranges using the

command with the`az aks show`

`--query`

parameter set to`apiServerAccessProfile.authorizedIpRanges`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query apiServerAccessProfile.authorizedIpRanges`

Example output:

`[ "73.140.245.0/24" ]`


Find existing API server authorized IP ranges using the

cmdlet.`Get-AzAksCluster`

`Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster | Select-Object -ExpandProperty ApiServerAccessProfile`

Example output:

`AuthorizedIPRanges: {73.140.245.0/24} ...`


Navigate to the Azure portal and select your AKS cluster.

From the service menu, under

**Settings**, select**Networking**. The existing API server authorized IP ranges are listed under**Resource settings**.

## Access the API server from your development machine, tooling, or automation

You must add your development machines, tooling, or automation IP addresses to the AKS cluster list of approved IP ranges to access the API server from there.

Another option is to configure a jumpbox with the necessary tooling inside a separate subnet in the firewall's virtual network. This option assumes your environment has a firewall with the respective network and that you added the firewall IPs to authorized ranges. Similarly, if you forced tunneling from the AKS subnet to the firewall subnet, having the jumpbox in the cluster subnet also works.

Note

The following example adds another IP address to the approved ranges. It still includes the existing IP address. If you don't include your existing IP address, this command replaces it with the new one instead of adding it to the authorized ranges.

Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges $CURRENT_IP/24,73.140.245.0/24`


Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '$CURRENT_IP/24,73.140.245.0/24'`


Another option is to use the following command on Windows systems to get the public IPv4 address:

```
Invoke-RestMethod http://ipinfo.io/json | Select -exp ip
```


You can also follow the steps in [Find your IP address](https://support.microsoft.com/help/4026518/windows-10-find-your-ip-address) or search on *what is my IP address?* in an internet browser.

## Related content

To learn more about security in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _best-practices-monitoring-proactive_concepts-network-azure-cni-pod-subnet.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: best-practices-monitoring-proactive.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-monitoring-proactive -->

# Proactive monitoring best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers the best practices for proactive monitoring on Azure Kubernetes Service (AKS) and provides a comprehensive list of the key signals AKS recommends for you to monitor.

Proactively monitoring your AKS clusters is crucial for reducing downtime and saving business interruptions for your applications. This process involves identifying and monitoring key indicators of abnormal behavior in your cluster that might lead to major issues or downtime.

## Monitoring and alerting overview

Monitoring on AKS involves using metrics, logs, and events to ensure the health and performance of your cluster. Common scenarios to monitor include node performance, pod status, and overall resource utilization in your cluster. Logs provide insights into system events and cluster operations and activity. For more information about the methods and signals AKS provides for monitoring, see [Monitor Azure Kubernetes Service (AKS)](monitor-aks).

The best way to proactively monitor your cluster is to configure [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview). Alerts act as proactive measures to notify you of potential issues or anomalies before they escalate into critical problems. By defining thresholds for key metrics and logs, you receive immediate alerts when these signals exceed predefined limits, indicating potential issues like resource exhaustion or application failures. We highly recommend defining [service-level objectives (SLOs)](/en-us/azure/well-architected/reliability/metrics) for your application to measure the performance and reliability of your service. Configuring alerts on the key signals for your SLOs allows you to quickly detect any degradation of your application's quality of service that your customers receive. Overall, setting timely alerts enables you to quickly investigate and remediate problems, minimizing downtime and ensuring high availability of applications running on your AKS cluster.

## How to configure alerts on specific metric types

| Metric type | Where to find these metrics | How to configure alerts |
|---|---|---|
| AKS Platform Metric | View
|

[Create a metric alert for an Azure resource](/en-us/azure/azure-monitor/alerts/tutorial-metric-alert).[Azure Monitor and Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).[Azure Monitor managed service for Prometheus rule groups](/en-us/azure/azure-monitor/essentials/prometheus-rule-groups).[Azure activity logs for AKS](monitor-aks#azure-activity-log).[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts).**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**Virtual Machine Scale Set instance**that matches the name of your node pool you're creating alerts for.4. Navigate to the

**Alerts**blade to create your metric alert.**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**load balancer instance**to bring up the Azure portal page for load balancer.4. Navigate to the

**Alerts**page to create your load balancer metric alert.[Azure Monitor resource logs](monitor-aks#azure-monitor-resource-logs).[Create log search alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).## Critical signals for configuring alerts

To get holistic coverage of your AKS environment, you need to configure alerts on the three main components of your cluster:

**Cluster infrastructure**: Alerts targeting the underlying infrastructure of your cluster such as nodes, disks, and networking.**Application health**: Alerts for monitoring the health of your pods and applications. Some common indicators of unhealthy applications include out-of-memory kills (OOMKills) of your pods, pods in not ready state, etc.**Kubernetes control plane**: Alerts on AKS control plane to monitor the health and performance of the API server, etcd, and other components.

The following sections contain the key signals which we recommend all AKS customers monitor closely. The AKS team is working to add all critical signals to the existing [Recommended Alerts](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts) feature, which allows you to easily enable alerts for all signals with a one-click experience. The Prometheus metrics alerts are available in Public Preview today, and the remaining alerts are estimated to be available in early 2025. For now, you can manually configure alerts on the critical signals.

### Cluster infrastructure alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| Cluster is in a failed state | Azure Activity Logs | Create or update managed cluster | Status of the log is Failed, indicating that the cluster upgrade or creation action failed. |
| Node pool is in a failed state | Azure Activity Logs | Create or update agent pool | Status of the log is Failed, indicating that the node pool is in a Failed state due to a failed Create, Read, Upgrade, or Delete (CRUD) operation. |
| High Node OS Disk Bandwidth Usage | Virtual Machine Scale Set Metric | OS Disk Bandwidth Consumed Percentage | Node OS disk bandwidth utilization is above 95%. |
| High Node OS Disk IOPS Usage | Virtual Machine Scale Set Metric | OS Disk IOPS Consumed Percentage | Node OS disk IOPS utilization is above 95%. |
| High Node OS Disk Space Usage | AKS Platform Metric | Disk Used Percentage | Node OS disk space percentage utilization is above 90%. |
| High Node CPU Usage | AKS Platform Metric | CPU Usage Percentage | Node CPU Usage is greater than 90%. |
| High Node Memory Usage | AKS Platform Metric | Memory Working Set Percentage | Node Memory Usage is greater than 90%. |
| Node is in NotReady state | AKS Platform Metric | Status for various node conditions | Node is in NotReady state for >20 minutes. |
| SNAT port exhaustion | Load Balancer (LB) Metric | SNAT Connection Count | Filter for Connection State = "Failed" |

### Application health alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| High number of unhealthy pods | Azure Managed Prometheus Metric | Alert name: KubePodReadyStateLow | Available as an AKS recommended alert. To enable this alert, see
|

[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).### Kubernetes control plane alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| ETCD is Filled Up | Azure Managed Prometheus Metric | etcd_mvcc_db_total_size_in_use_in_bytes | ETCD utilization is greater than 2 GB |
| API Server Too Many Requests Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error code 429 |
| API Server Webhook and Tunnel Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error codes 500 and 503 |

## Next steps

For more information about monitoring on AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: concepts-network-azure-cni-pod-subnet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-azure-cni-pod-subnet -->

# Azure Container Networking Interface (CNI) Pod Subnet

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Pod Subnet assigns IP addresses to pods from a separate subnet from your cluster Nodes. This feature is available in two modes: Dynamic IP Allocation and Static Block Allocation.

## Prerequisites

Note

When using Static Block Allocation of CIDRs, exposing an application as a Private Link Service using a Kubernetes Load Balancer Service isn't supported.

- Review the
[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article. - Review the
[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply. - AKS Engine and DIY clusters aren't supported.
- Azure CLI version
`2.37.0`

or later and the`aks-preview`

extension version`2.0.0b2`

or later. - Register the subscription-level feature flag for your subscription: 'Microsoft.ContainerService/AzureVnetScalePreview'.

## Dynamic IP allocation mode

Dynamic IP allocation helps mitigate pod IP address exhaustion issues by allocating pod IPs from a subnet that's separate from the subnet hosting the AKS cluster.

The Dynamic IP Allocation mode offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned VNet IPs, they have direct connectivity to other cluster pods and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios, such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using network security groups (NSGs) to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this mode.

### Plan IP addressing

With Dynamic IP Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster, as the nodes request 16 IPs on startup and request another batch of 16 anytime there are <8 IPs unallocated in their allotment.

IP address planning for Kubernetes services and Docker Bridge remain unchanged.

## Static block allocation mode

Static block allocation helps mitigate potential pod subnet sizing and Azure address mapping limitations by assigning CIDR blocks to nodes rather than individual IPs.

The Static Block Allocation mode offers the following benefits:

**Better IP scalability**: CIDR blocks are statically allocated to the cluster nodes and are present for the lifetime of the node, as opposed to the traditional dynamic allocation of individual IPs with traditional CNI. This enables routing based on CIDR blocks and helps scale the cluster limit up to 1 million pods from the traditional 65K pods per cluster. Your Azure Virtual Network must be large enough to accommodate the scale of your cluster.**Flexibility**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pods and resources in the VNet.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Cilium, Azure NPM, and Calico work with this solution.

### Limitations

Below are some of the limitations of using Azure CNI Static Block allocation:

- Minimum Kubernetes Version required is 1.28.
- Maximum subnet size supported is x.x.x.x/12 ~ 1 million IPs.
- Only a single mode of operation can be used per subnet. If a subnet uses Static Block allocation mode, it cannot use Dynamic IP allocation mode in a different cluster or node pool with the same subnet and vice versa.
- Only supported in new clusters or when adding node pools with a different subnet to existing clusters. Migrating or updating existing clusters or node pools is not supported.
- Across all the CIDR blocks assigned to a node in the node pool, one IP will be selected as the primary IP of the node. Thus, for network administrators selecting the
`--max-pods`

value try to use the calculation below to best serve your needs and have optimal usage of IPs in the subnet:

`max_pods = (N * 16) - 1`

where `N`

is any positive integer and `N`

> 0

### Plan IP addressing

With Static Block Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

CIDR blocks of /28 (16 IPs) are allocated to nodes based on your `--max-pods`

configuration for your node pool, which defines the maximum number of pods per node. 1 IP is reserved on each node from all the available IPs on that node for internal purposes.

While planning your IPs, it's important to define your `--max-pods`

configuration using the following calculation: `max_pods_per_node = (16 * N) - 1`

, where `N`

is any positive integer greater than `0`

.

Ideal values with no IP wastage would require the max pods value to conform to the above expression.

See the following example cases:

Note

The examples assume /28 CIDR blocks (16 IPs each).

| Example case | `max_pods` |
CIDR Blocks allocated per node | Total IP available for pods | IP wastage for node |
|---|---|---|---|---|
| Low wastage (acceptable) | 30 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 30 = 1 |
| Ideal case | 31 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 31 = 0 |
| High wastage (not recommended) | 32 | 3 | (16 * 3) - 1 = 48 - 1 = 47 | 47 - 32 = 15 |

IP address planning for Kubernetes services remains unchanged.

Note

Ensure your VNet has a sufficiently large and contiguous address space to support your cluster's scale.


---

<!-- DOCUMENTO FUSIONADO: __spark-job_integrations_custom-node-configuration.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _spark-job_integrations.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: spark-job.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/spark-job -->

# Add-ons, extensions, and other integrations with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides extra functionality for your clusters using add-ons and extensions. Open-source projects and third parties provide by more integrations that are commonly used with AKS. The [AKS support policy](support-policies) doesn't support the open-source and third-party integrations.

## Add-ons

Add-ons are a fully supported way to provide extra capabilities for your AKS cluster. The installation, configuration, and lifecycle of add-ons are managed on AKS. You can use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command to install an add-on or manage the add-ons for your cluster.

AKS uses the following rules for applying updates to installed add-ons:

- Only an add-on's patch version can be upgraded within a Kubernetes minor version. The add-on's major/minor version isn't upgraded within the same Kubernetes minor version.
- The major/minor version of the add-on is only upgraded when moving to a later Kubernetes minor version.
- Any breaking or behavior changes to the add-on are announced well before, usually 60 days, for a GA minor version of Kubernetes on AKS.
- You can patch add-ons weekly with every new release of AKS, which is announced in the release notes. You can control AKS releases using the
[maintenance windows](planned-maintenance)and[release tracker](release-tracker).

### Exceptions

- Add-ons are upgraded to a new major/minor version (or breaking change) within a Kubernetes minor version if either the cluster's Kubernetes version or the add-on version are in preview.
- There can be unavoidable circumstances, such as CVE security patches or critical bug fixes, when you need to update an add-on within a GA minor version.

### Available add-ons

| Name | Description | Articles | GitHub |
|---|---|---|---|
| ingress-appgw | Use Application Gateway Ingress Controller with your AKS cluster. |
|

[GitHub](https://github.com/Azure/application-gateway-kubernetes-ingress)[Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)[GitHub](https://github.com/Azure-Samples/aks-keda-addon-workload-identity)[Container insights overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[Managed Prometheus overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[GitHub](https://github.com/Azure/AKS)[GitHub](https://github.com/Azure/prometheus-collector)[Understand Azure Policy for Kubernetes clusters](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks)[GitHub](https://github.com/Azure/azure-policy)[Use the Azure Key Vault Provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[GitHub](https://github.com/Azure/secrets-store-csi-driver-provider-azure)[Use virtual nodes](virtual-nodes)[GitHub](https://github.com/virtual-kubelet/virtual-kubelet)[Open Service Mesh AKS add-on (retired)](open-service-mesh-about)[GitHub](https://github.com/Azure/osm-azure)## Extensions

Cluster extensions build on top of certain Helm charts and provide an Azure Resource Manager-driven experience for installation and lifecycle management of different Azure capabilities on top of your Kubernetes cluster.

- For more information on the specific cluster extensions for AKS, see
[Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)](cluster-extensions?tabs=azure-cli). - For more information on available cluster extensions, see
[Currently available extensions](cluster-extensions?tabs=azure-cli#currently-available-extensions).

### Difference between extensions and add-ons

Extensions and add-ons are both supported ways to add functionality to your AKS cluster. When you install an add-on, the functionality is added as part of the AKS resource provider in the Azure API. When you install an extension, the functionality is added as part of a separate resource provider in the Azure API.

## GitHub Actions

GitHub Actions help you automate your software development workflows from within GitHub.

- For more information on using GitHub Actions with Azure, see
[GitHub Actions for Azure](/en-us/azure/developer/github/github-actions). - For an example of using GitHub Actions with an AKS cluster, see
[Build, test, and deploy containers to Azure Kubernetes Service using GitHub Actions](kubernetes-action).

## Open-source and third-party integrations

There are many open-source and third-party integrations you can install on your AKS cluster. The [AKS support policy](support-policies) doesn't cover self-managed installations of the following projects. Some of these projects have managed experiences built on top of them (for example in the case of Prometheus, Grafana, and Istio). These managed experiences are noted in the 'More Details' column.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

| Name | Description | More details |
|---|---|---|
|

[Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm](quickstart-helm)[Prometheus](https://prometheus.io/)[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview); Self-managed experience -[Prometheus operator](https://github.com/prometheus-operator/kube-prometheus)[Grafana](https://grafana.com/)[Azure Managed Grafana](/en-us/azure/managed-grafana/overview); Self-managed experience -[Deploy Grafana on Kubernetes](https://grafana.com/docs/grafana/latest/installation/kubernetes/).[Couchbase](https://www.couchbase.com/)[Install Couchbase and the Operator on AKS](https://docs.couchbase.com/operator/2.4/tutorial-aks.html)[OpenFaaS](https://www.openfaas.com/)[Use OpenFaaS with AKS](openfaas)[Apache Spark](https://spark.apache.org/)*Standard_D3_v2*. For more information on running Spark jobs on Kubernetes, see the[running Spark on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html)guide.[Istio](https://istio.io/)[Istio add-on for AKS](istio-about); Self-managed experience -[Istio open-source installation](https://istio.io/latest/docs/setup/install/)[Linkerd](https://linkerd.io/)[Linkerd Getting Started](https://linkerd.io/2.16/getting-started/)[Consul](https://www.consul.io/)[Getting Started with Consul Service Mesh for Kubernetes](https://learn.hashicorp.com/tutorials/consul/service-mesh-deploy)### Third-party integrations for Windows containers

Microsoft collaborates with partners to ensure the build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

For more information, see [Windows AKS partner solutions](windows-aks-partner-solutions).


---

<!-- DOCUMENTO FUSIONADO: integrations.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/integrations -->

# Add-ons, extensions, and other integrations with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides extra functionality for your clusters using add-ons and extensions. Open-source projects and third parties provide by more integrations that are commonly used with AKS. The [AKS support policy](support-policies) doesn't support the open-source and third-party integrations.

## Add-ons

Add-ons are a fully supported way to provide extra capabilities for your AKS cluster. The installation, configuration, and lifecycle of add-ons are managed on AKS. You can use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command to install an add-on or manage the add-ons for your cluster.

AKS uses the following rules for applying updates to installed add-ons:

- Only an add-on's patch version can be upgraded within a Kubernetes minor version. The add-on's major/minor version isn't upgraded within the same Kubernetes minor version.
- The major/minor version of the add-on is only upgraded when moving to a later Kubernetes minor version.
- Any breaking or behavior changes to the add-on are announced well before, usually 60 days, for a GA minor version of Kubernetes on AKS.
- You can patch add-ons weekly with every new release of AKS, which is announced in the release notes. You can control AKS releases using the
[maintenance windows](planned-maintenance)and[release tracker](release-tracker).

### Exceptions

- Add-ons are upgraded to a new major/minor version (or breaking change) within a Kubernetes minor version if either the cluster's Kubernetes version or the add-on version are in preview.
- There can be unavoidable circumstances, such as CVE security patches or critical bug fixes, when you need to update an add-on within a GA minor version.

### Available add-ons

| Name | Description | Articles | GitHub |
|---|---|---|---|
| ingress-appgw | Use Application Gateway Ingress Controller with your AKS cluster. |
|

[GitHub](https://github.com/Azure/application-gateway-kubernetes-ingress)[Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)[GitHub](https://github.com/Azure-Samples/aks-keda-addon-workload-identity)[Container insights overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[Managed Prometheus overview](/en-us/azure/azure-monitor/containers/container-insights-overview)[GitHub](https://github.com/Azure/AKS)[GitHub](https://github.com/Azure/prometheus-collector)[Understand Azure Policy for Kubernetes clusters](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks)[GitHub](https://github.com/Azure/azure-policy)[Use the Azure Key Vault Provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[GitHub](https://github.com/Azure/secrets-store-csi-driver-provider-azure)[Use virtual nodes](virtual-nodes)[GitHub](https://github.com/virtual-kubelet/virtual-kubelet)[Open Service Mesh AKS add-on (retired)](open-service-mesh-about)[GitHub](https://github.com/Azure/osm-azure)## Extensions

Cluster extensions build on top of certain Helm charts and provide an Azure Resource Manager-driven experience for installation and lifecycle management of different Azure capabilities on top of your Kubernetes cluster.

- For more information on the specific cluster extensions for AKS, see
[Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)](cluster-extensions?tabs=azure-cli). - For more information on available cluster extensions, see
[Currently available extensions](cluster-extensions?tabs=azure-cli#currently-available-extensions).

### Difference between extensions and add-ons

Extensions and add-ons are both supported ways to add functionality to your AKS cluster. When you install an add-on, the functionality is added as part of the AKS resource provider in the Azure API. When you install an extension, the functionality is added as part of a separate resource provider in the Azure API.

## GitHub Actions

GitHub Actions help you automate your software development workflows from within GitHub.

- For more information on using GitHub Actions with Azure, see
[GitHub Actions for Azure](/en-us/azure/developer/github/github-actions). - For an example of using GitHub Actions with an AKS cluster, see
[Build, test, and deploy containers to Azure Kubernetes Service using GitHub Actions](kubernetes-action).

## Open-source and third-party integrations

There are many open-source and third-party integrations you can install on your AKS cluster. The [AKS support policy](support-policies) doesn't cover self-managed installations of the following projects. Some of these projects have managed experiences built on top of them (for example in the case of Prometheus, Grafana, and Istio). These managed experiences are noted in the 'More Details' column.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

| Name | Description | More details |
|---|---|---|
|

[Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm](quickstart-helm)[Prometheus](https://prometheus.io/)[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview); Self-managed experience -[Prometheus operator](https://github.com/prometheus-operator/kube-prometheus)[Grafana](https://grafana.com/)[Azure Managed Grafana](/en-us/azure/managed-grafana/overview); Self-managed experience -[Deploy Grafana on Kubernetes](https://grafana.com/docs/grafana/latest/installation/kubernetes/).[Couchbase](https://www.couchbase.com/)[Install Couchbase and the Operator on AKS](https://docs.couchbase.com/operator/2.4/tutorial-aks.html)[OpenFaaS](https://www.openfaas.com/)[Use OpenFaaS with AKS](openfaas)[Apache Spark](https://spark.apache.org/)*Standard_D3_v2*. For more information on running Spark jobs on Kubernetes, see the[running Spark on Kubernetes](https://spark.apache.org/docs/latest/running-on-kubernetes.html)guide.[Istio](https://istio.io/)[Istio add-on for AKS](istio-about); Self-managed experience -[Istio open-source installation](https://istio.io/latest/docs/setup/install/)[Linkerd](https://linkerd.io/)[Linkerd Getting Started](https://linkerd.io/2.16/getting-started/)[Consul](https://www.consul.io/)[Getting Started with Consul Service Mesh for Kubernetes](https://learn.hashicorp.com/tutorials/consul/service-mesh-deploy)### Third-party integrations for Windows containers

Microsoft collaborates with partners to ensure the build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

For more information, see [Windows AKS partner solutions](windows-aks-partner-solutions).


---

<!-- DOCUMENTO FUSIONADO: custom-node-configuration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/custom-node-configuration -->

# Customize the node configuration for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Customizing your node configuration allows you to adjust operating system (OS) settings or kubelet parameters to match the needs of your workloads. When you create an AKS cluster or add a node pool to your cluster, you can customize a subset of commonly used OS and kubelet settings. To configure settings beyond this subset, you can [use a daemon set to customize your needed configurations without losing AKS support for your nodes](support-policies#shared-responsibility).

## Create custom node configuration files for AKS node pools

OS and kubelet configuration changes require you to create a new configuration file with the parameters and your desired settings. If a value for a parameter isn't specified, then the value is set to the default.

Note

The following examples show common configuration settings. You can modify the settings to meet your workload requirements. For a full list of supported custom configuration parameters, see the [Supported custom configuration parameters](#supported-custom-configuration-parameters) section.

### Kubelet configuration

Create a `linuxkubeletconfig.json`

file with the following contents:

```
{
"cpuManagerPolicy": "static",
"cpuCfsQuota": true,
"cpuCfsQuotaPeriod": "200ms",
"imageGcHighThreshold": 90,
"imageGcLowThreshold": 70,
"topologyManagerPolicy": "best-effort",
"allowedUnsafeSysctls": [
"kernel.msg*",
"net.*"
],
"failSwapOn": false
}
```


### OS configuration

Create a `linuxosconfig.json`

file with the following contents:

```
{
"transparentHugePageEnabled": "madvise",
"transparentHugePageDefrag": "defer+madvise",
"swapFileSizeMB": 1500,
"sysctls": {
"netCoreSomaxconn": 163849,
"netIpv4TcpTwReuse": true,
"netIpv4IpLocalPortRange": "32000 60000"
}
}
```


## Create an AKS cluster using custom configuration files

Note

Keep the following information in mind when using custom configuration files when creating a new AKS cluster:

- If you specify a configuration when creating a cluster, the configuration applies only to the nodes in the initial node pool. Any settings not configured in the JSON file retain their default values.
`CustomLinuxOsConfig`

isn't supported for the Windows OS type.

Create a new cluster using custom configuration files using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new cluster with the custom `./linuxkubeletconfig.json`

and `./linuxosconfig.json`

files:```
az aks create --name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json --linux-os-config ./linuxosconfig.json
```


## Add a node pool using custom configuration files

Note

Keep the following information in mind when using custom configuration files when adding a new node pool to an existing AKS cluster:

- When you add a Linux node pool to an existing cluster, you can specify the kubelet configuration, OS configuration, or both. When you add a Windows node pool to an existing cluster, you can only specify the kubelet configuration. If you specify a configuration when adding a node pool, the configuration applies only to the nodes in the new node pool. Any settings not configured in the JSON file retain their default values.
`CustomKubeletConfig`

is supported for Linux and Windows node pools.

Create a new Linux node pool using the [ az aks nodepool add](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new Linux node pool with the custom `./linuxkubeletconfig.json`

file:```
az aks nodepool add --name <node-pool-name> --cluster-name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json
```


## Confirm settings were applied

After you apply custom node configuration, you can confirm the settings were applied to the nodes by [connecting to the host](node-access) and verifying `sysctl`

or configuration changes were made on the filesystem.

## Supported custom configuration parameters

### Linux kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`cpuManagerPolicy` |
none, static | none | The static policy allows containers in
|

`cpuCfsQuota`

`cpuCfsQuotaPeriod`

`100ms`

`imageGcHighThreshold`

`imageGcLowThreshold`

`imageGcHighThreshold`

*can*trigger garbage collection.`topologyManagerPolicy`

[Control Topology Management Policies on a node](https://kubernetes.io/docs/tasks/administer-cluster/topology-manager/).`allowedUnsafeSysctls`

`kernel.shm*`

, `kernel.msg*`

, `kernel.sem`

, `fs.mqueue.*`

, `net.*`

`containerLogMaxSizeMB`

`containerLogMaxFiles`

`podMaxPids`

`seccompDefault`

`Unconfined`

, `RuntimeDefault`

`Unconfined`

`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls fail. `Unconfined`

places no restrictions on syscalls, allowing all system calls and reducing security. For more information, see the [containerd default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51). This parameter is in preview.[Register](/en-us/azure/azure-resource-manager/management/preview-features?tabs=azure-cli#register-preview-feature)the "KubeletDefaultSeccompProfilePreview" feature flag using the[command with](/en-us/cli/azure/feature#az-feature-register)`az feature register`

`--namespace "Microsoft.ContainerService"`

.### Windows kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`imageGcHighThreshold` |
0-100 | 85 | The percent of disk usage after which image garbage collection is always run. Minimum disk usage that triggers garbage collection. To disable image garbage collection, set to 100. |
`imageGcLowThreshold` |
0-100, no higher than `imageGcHighThreshold` |
80 | The percent of disk usage before which image garbage collection is never run. Minimum disk usage that can trigger garbage collection. |
`containerLogMaxSizeMB` |
Size in megabytes (MB) | 10 | The maximum size (for example, 10 MB) of a container log file before it gets rotated. |
`containerLogMaxFiles` |
≥ 2 | 5 | The maximum number of container log files that can be present for a container. |

## Linux custom OS configuration settings

Important

To simplify search and readability, the OS settings are displayed in this article by their name, but they should be added to the configuration JSON file or AKS API using the [camelCase capitalization convention](/en-us/dotnet/standard/design-guidelines/capitalization-conventions).

For example, if you modify the `vm.max_map_count setting`

, you should reformat to `vmMaxMapCount`

in the configuration JSON file.

### Linux file handle limits

When serving high amounts of traffic, that traffic commonly comes from a large number of local files. You can adjust the following kernel settings and built-in limits to allow you to handle more, at the cost of some system memory.

The following table lists the file handle limits that you can customize per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`fs.file-max` |
8192 - 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | Maximum number of file-handles that the Linux kernel allocates. This value is set to the maximum possible value (2^63-1) to prevent file descriptor exhaustion and ensure unlimited system-wide file handles for containerized workloads. |
`fs.inotify.max_user_watches` |
781250 - 2097152 | 1048576 | 1048576 | 1048576 | Maximum number of file watches allowed by the system. Each watch is roughly 90 bytes on a 32-bit kernel, and roughly 160 bytes on a 64-bit kernel. |
`fs.aio-max-nr` |
65536 - 6553500 | 65536 | 65536 | 65536 | The aio-nr shows the current system-wide number of asynchronous io requests. aio-max-nr allows you to change the maximum value aio-nr can grow to. |
`fs.nr_open` |
8192 - 20000500 | 1048576 | 1048576 | 1073741816 | The maximum number of file-handles a process can allocate. |

Note

The `fs.file-max`

parameter is set to 9223372036854775807 (the maximum value for a signed 64-bit integer) across Ubuntu and Azure Linux based on upstream defaults. This configuration:

**Prevents denial-of-service attacks**based on system-wide file descriptor exhaustion.**Ensures container workloads**are never bottlenecked by system-wide file handle limits.**Maintains security**through per-process limits (`fs.nr_open`

and`ulimit`

) which still apply to individual processes.**Optimizes for container platforms**where many containers might run simultaneously, each potentially opening many files and network connection.

### Linux socket and network tuning

For agent nodes, which are expected to handle large numbers of concurrent sessions, you can use following TCP and network options and adjust them per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`net.core.somaxconn` |
4096 - 3240000 | 16384 | 16384 | 16384 | Maximum number of connection requests that can be queued for any given listening socket. An upper limit for the value of the backlog parameter passed to the
`somaxconn` , then it's silently truncated to this limit. |

`net.core.netdev_max_backlog`

`net.core.rmem_max`

`net.core.wmem_max`

`net.core.optmem_max`

`net.ipv4.tcp_max_syn_backlog`

`net.ipv4.tcp_max_tw_buckets`

`timewait`

sockets held by system simultaneously. If this number is exceeded, time-wait socket is immediately destroyed and warning is printed.`net.ipv4.tcp_fin_timeout`

`net.ipv4.tcp_keepalive_time`

`keepalive`

messages when `keepalive`

is enabled.`net.ipv4.tcp_keepalive_probes`

`keepalive`

probes TCP sends out, until it decides that the connection is broken.`net.ipv4.tcp_keepalive_intvl`

`tcp_keepalive_probes`

it makes up the time to kill a connection that isn't responding, after probes started.`net.ipv4.tcp_tw_reuse`

`TIME-WAIT`

sockets for new connections when it's safe from protocol viewpoint.`net.ipv4.ip_local_port_range`

`net.ipv4.neigh.default.gc_thresh1`

`net.ipv4.neigh.default.gc_thresh2`

`net.ipv4.neigh.default.gc_thresh3`

`net.netfilter.nf_conntrack_max`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_max`

is the maximum number of nodes in the hash table, that is, the maximum number of connections supported by the `nf_conntrack`

module or the size of connection tracking table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

(or `RAM_in_MB * 64`

). For example, a VM with 8 GB RAM has a default of approximately 524,288 connections. Actual values vary based on the VM size and available memory.`net.netfilter.nf_conntrack_buckets`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_buckets`

is the size of hash table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

, with a minimum of 1,024 buckets and a maximum of 262,144 buckets. The default `nf_conntrack_max`

is typically set to `nf_conntrack_buckets * 4`

. Actual values vary based on the VM size and available memory.### Linux worker limits

Like file descriptor limits, the number of workers or threads that a process can create are limited by both a kernel setting and user limits. The user limit on AKS is unlimited. The following table lists the kernel setting that you can customize per node pool:

| Setting | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|
`kernel.threads-max` |
Dynamically calculated | Dynamically calculated | Dynamically calculated | Processes can spin up worker threads. The maximum number of all threads that can be created is set with the kernel setting `kernel.threads-max` . Default value is dynamically calculated based on system memory using the formula: `total_ram_pages / 4` (where each page is typically 4 KB). Actual values vary based on the VM size and available memory. |

### Linux virtual memory

The following table lists the kernel settings that you can customize per node pool to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the `writeout`

of dirty data to disk:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`vm.max_map_count` |
65530 | 1048576 | 1048576 | This file contains the maximum number of memory map areas a process can have. Memory map areas are used as a side-effect of calling `malloc` , directly by `mmap` , `mprotect` , and `madvise` , and also when loading shared libraries. |
|
`vm.vfs_cache_pressure` |
1 - 100 | 100 | 100 | 100 | This percentage value controls the tendency of the kernel to reclaim the memory, which is used for caching of directory and inode objects. |
`vm.swappiness` |
0 - 100 | 60 | 60 | 60 | This control is used to define how aggressively the kernel swaps memory pages. Higher values increase aggressiveness, lower values decrease the amount of swap. A value of 0 instructs the kernel not to initiate swap until the amount of free and file-backed pages is less than the high water mark in a zone. |
`swapFileSizeMB` |
1 MB - Size of the
|

`transparentHugePageEnabled`

`always`

, `madvise`

, `never`

`always`

`always`

`madvise`

[Transparent Hugepages](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html#admin-guide-transhuge)is a Linux kernel feature intended to improve performance by making more efficient use of your processor's memory-mapping hardware. When enabled the kernel attempts to allocate`hugepages`

whenever possible and any Linux process receives 2-MB pages if the `mmap`

region is 2 MB naturally aligned. In certain cases when `hugepages`

are enabled system wide, applications might end up allocating more memory resources. An application might `mmap`

a large region but only touch 1 byte of it, in that case a 2-MB page might be allocated instead of a 4k page for no good reason. This scenario is why it's possible to disable `hugepages`

system-wide or to only have them inside `MADV_HUGEPAGE madvise`

regions.`transparentHugePageDefrag`

`always`

, `defer`

, `defer+madvise`

, `madvise`

, `never`

`madvise`

`madvise`

`madvise`

`hugepages`

available.## Related content

- Learn
[how to configure your AKS cluster](concepts-clusters-workloads). - Learn how
[upgrade the node images](node-image-upgrade)in your cluster. - See
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-cluster)to learn how to upgrade your cluster to the latest version of Kubernetes. - See the list of
[Frequently asked questions about AKS](faq)to find answers to some common AKS questions.


---

<!-- DOCUMENTO FUSIONADO: __planned-maintenance__configure-static-egress-gateway_ai-toolchain-operator-mon_61d994.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _planned-maintenance__configure-static-egress-gateway_ai-toolchain-operator-moni_11fcd9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: planned-maintenance.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/planned-maintenance -->

# Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use planned maintenance to schedule and control cluster and node image upgrades in Azure Kubernetes Service (AKS).

Regular maintenance is performed on your AKS cluster automatically. There are two types of maintenance operations:

**AKS-initiated maintenance**involves the weekly releases that AKS performs to keep your cluster up to date with the latest features and fixes.**User-initiated maintenance**includes[cluster auto-upgrades](upgrade-cluster)and[node operating system (OS) automatic security updates](auto-upgrade-node-image).

When you use the feature of planned maintenance in AKS, you can run both types of maintenance in a cadence of your choice to minimize workload impact.

Note

You can use planned maintenance to schedule the timing of automatic upgrades, but enabling or disabling planned maintenance doesn't enable or disable automatic upgrades.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, see
[Create an AKS cluster](learn/quick-kubernetes-deploy-cli). - If you're using the Azure CLI, upgrade to the latest version using the
command.`az upgrade`


## Considerations

When you use planned maintenance, the following considerations apply:

- AKS reserves the right to break planned maintenance windows for unplanned, reactive maintenance operations that are urgent or critical. These maintenance operations might even run during the
`notAllowedTime`

or`notAllowedDates`

periods defined in your configuration. - Maintenance operations are considered
*best effort only*and aren't guaranteed to occur within a specified window.

## Schedule configuration types for planned maintenance

Three schedule configuration types are available for planned maintenance:

`default`

is a basic configuration for controlling AKS releases, which covers control plane components and system add-ons upgrade. The releases can take up to two weeks to roll out to all regions from the initial time of shipping, because of Azure safe deployment practices.Choose

`default`

to schedule these updates in a manner that's least disruptive for you. You can monitor the status of an ongoing AKS release by region with the[weekly release tracker](release-tracker).`aksManagedAutoUpgradeSchedule`

controls when to perform cluster upgrades scheduled by your designated auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on cluster auto-upgrade, see[Automatically upgrade an Azure Kubernetes Service cluster](upgrade-cluster).`aksManagedNodeOSUpgradeSchedule`

controls when to perform the node OS security patching scheduled by your node OS auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on node OS auto-upgrade channels, see[Automatically patch and update AKS cluster node images](auto-upgrade-node-image).

We recommend using `aksManagedAutoUpgradeSchedule`

for all cluster Kubernetes version upgrade scenarios and `aksManagedNodeOSUpgradeSchedule`

for all node OS security patching scenarios.

The `default`

option is meant exclusively for AKS weekly releases. Use `default`

if you want to control the upgrade schedule for AKS control plane components (such as API Server, ETCD, etc.) and add-ons (such as CoreDNS, Metrics Server, etc.).

All three types of configurations can coexist.

## Create a maintenance window

Note

When you're using auto-upgrade, to ensure proper functionality, use a maintenance window with a duration of four hours or more.

Note

From the 2023-05-01 API version onwards, use the properties in the following table for `default`

configuration.

An `aksManagedAutoUpgradeSchedule`

or `aksManagedNodeOSUpgradeSchedule`

maintenance window and `default`

configuration from 2023-05-01 API version onwards has the following properties:

| Name | Description | Default value |
|---|---|---|
`utcOffset` |
The time zone for cluster maintenance. | `+00:00` |
`startDate` |
The date on which the maintenance window begins to take effect. | The current date at creation time |
`startTime` |
The time for maintenance to begin, based on the time zone determined by `utcOffset` . |
Not applicable |
`schedule` |
The upgrade frequency. Three types are available: `Weekly` , `AbsoluteMonthly` , and `RelativeMonthly` . |
Not applicable |
`intervalDays` |
The interval in days for maintenance runs. It's applicable only to `aksManagedNodeOSUpgradeSchedule` . |
Not applicable |
`intervalWeeks` |
The interval in weeks for maintenance runs. | Not applicable |
`intervalMonths` |
The interval in months for maintenance runs. | Not applicable |
`dayOfWeek` |
The specified day of the week for maintenance to begin. | Not applicable |
`durationHours` |
The duration of the window for maintenance to run. | Not applicable |
`notAllowedDates` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. It's applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Deprecated properties

Note

If you create a `default`

configuration with the following deprecated properties, it migrates automatically to the new properties shown in the previous table.

**[Deprecated]** A `default`

maintenance window has the following legacy properties:

| Name | Description | Default value |
|---|---|---|
`timeInWeek` |
In a `default` configuration, this property contains the `day` and `hourSlots` values that define a maintenance window. |
Not applicable |
`timeInWeek.day` |
The day of the week to perform maintenance in a `default` configuration. |
Not applicable |
`timeInWeek.hourSlots` |
A list of hour-long time slots to perform maintenance on a particular day in a `default` configuration. |
Not applicable |
`notAllowedTime` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. This property is applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Schedule types

Four schedule types are supported: `Daily`

, `Weekly`

, `AbsoluteMonthly`

, and `RelativeMonthly`

.

The following table shows which types are available for each maintenance-configuration option:

| Schedule type | `default` |
`aksManagedClusterAutoUpgradeSchedule` |
`aksManagedNodeOSUpgradeSchedule` |
|---|---|---|---|
| Daily | Unsupported ❌ | Supported ✅ (after Jun 2025) | Supported ✅ |
| Weekly | Supported ✅ | Supported ✅ | Supported ✅ |
| AbsoluteMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |
| RelativeMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |

All of the fields shown for each schedule type are required.

A `Daily`

schedule might look like "every three days":

```
"schedule": {
"daily": {
"intervalDays": 3
}
}
```


A `Weekly`

schedule might look like "every two weeks on Friday":

```
"schedule": {
"weekly": {
"intervalWeeks": 2,
"dayOfWeek": "Friday"
}
}
```


An `AbsoluteMonthly`

schedule might look like "every three months on the first day of the month":

```
"schedule": {
"absoluteMonthly": {
"intervalMonths": 3,
"dayOfMonth": 1
}
}
```


A `RelativeMonthly`

schedule might look like "every two months on the last Monday":

```
"schedule": {
"relativeMonthly": {
"intervalMonths": 2,
"dayOfWeek": "Monday",
"weekIndex": "Last"
}
}
```


Valid values for `weekIndex`

include `First`

, `Second`

, `Third`

, `Fourth`

, and `Last`

.

## Add a maintenance window configuration

Add a maintenance window configuration to an AKS cluster using the [ az aks maintenanceconfiguration add](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-add) command.

The first example adds a new `default`

configuration that schedules maintenance to run from 1:00 AM to 5:00 AM every Monday in the `UTC`

time zone. The second example adds a new `aksManagedAutoUpgradeSchedule`

configuration that schedules maintenance to run every third Friday between 12:00 AM and 8:00 AM in the `UTC+5:30`

time zone.

```
# Add a new default configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Monday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 01:00
# Add a new aksManagedAutoUpgradeSchedule configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule --schedule-type Weekly --day-of-week Friday --interval-weeks 3 --duration 8 --utc-offset +05:30 --start-time 00:00
```


## Update an existing maintenance window

Update an existing maintenance configuration using the [ az aks maintenanceconfiguration update](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-update) command.

The following example updates the `default`

configuration to schedule maintenance to run from 2:00 AM to 6:00 AM every Friday:

```
az aks maintenanceconfiguration update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Friday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 02:00
```


## List all maintenance windows in an existing cluster

List the current maintenance configuration windows in your AKS cluster using the [ az aks maintenanceconfiguration list](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-list) command:

```
az aks maintenanceconfiguration list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Show a specific maintenance configuration window in an existing cluster

View a specific maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration show](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-show) command with the

`--name`

parameter:```
az aks maintenanceconfiguration show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule
```


The following example output shows the maintenance window for `aksManagedAutoUpgradeSchedule`

:

```
{
"id": "/subscriptions/<subscription>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/maintenanceConfigurations/aksManagedAutoUpgradeSchedule",
"maintenanceWindow": {
"durationHours": 4,
"notAllowedDates": [
{
"end": "2024-01-05",
"start": "2023-12-23"
}
],
"schedule": {
"absoluteMonthly": {
"dayOfMonth": 1,
"intervalMonths": 3
},
"daily": null,
"relativeMonthly": null,
"weekly": null
},
"startDate": "2023-01-20",
"startTime": "09:00",
"utcOffset": "-08:00"
},
"name": "aksManagedAutoUpgradeSchedule",
"notAllowedTime": null,
"resourceGroup": "myResourceGroup",
"systemData": null,
"timeInWeek": null,
"type": null
}
```


## Delete a maintenance configuration window in an existing cluster

Delete a maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration delete](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-delete) command.

The following example deletes the `autoUpgradeSchedule`

maintenance configuration:

```
az aks maintenanceconfiguration delete --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name autoUpgradeSchedule
```


## Frequently asked questions (FAQ)

### How can I check the existing maintenance configurations in my cluster?

Use the `az aks maintenanceconfiguration show`

command.

### Can reactive, unplanned maintenance happen during the `notAllowedDates`

periods too?

Yes. AKS reserves the right to break these windows for unplanned, reactive maintenance operations that are urgent or critical.

### How can I tell if a maintenance event occurred?

For releases, check your cluster's region and look up information in [weekly releases](release-tracker) to see if it matches your maintenance schedule. To view the status of your automatic upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events, as mentioned in [Upgrade an AKS cluster](upgrade-cluster).

AKS also emits upgrade-related Azure Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I use more than one maintenance configuration at the same time?

Yes, you can run all three configurations simultaneously: `default`

, `aksManagedAutoUpgradeSchedule`

, and `aksManagedNodeOSUpgradeSchedule`

. If the windows overlap, AKS decides the running order.

### I configured a maintenance window, but the upgrade didn't happen. Why?

AKS auto-upgrade needs a certain amount of time, usually not more than 15 minutes, to take the maintenance window into consideration. We recommend at least 15 minutes between the creation or update of a maintenance configuration and the scheduled start time.

Also, ensure that your cluster is started when the planned maintenance window starts. If the cluster is stopped, its control plane is deallocated and no operations can be performed.

### Why was one of my agent pools upgraded outside the maintenance window?

If an agent pool isn't upgraded (for example, because pod disruption budgets prevented it), it might be upgraded later, outside the maintenance window. This scenario is referred to as a *catch-up upgrade*. It avoids letting agent pools be upgraded with a different version from the AKS control plane.

Another reason why an agent pool could be upgraded unexpectedly is when there's no defined maintenance configuration or if it was deleted. In that case, a cluster with auto-upgrade *but without a maintenance configuration* is upgraded at random times (*fallback schedule*), which might be an undesired timeframe.

### Are there any best practices for the maintenance configurations?

We recommend setting the [node OS security updates](auto-upgrade-node-image) schedule to a weekly cadence if you're using the `NodeImage`

channel, because a new node image is shipped every week. You can also opt in for the `SecurityPatch`

channel to receive daily security updates.

You can set the [auto-upgrade](auto-upgrade-cluster) schedule to a monthly cadence to stay current with the Kubernetes N-2 [support policy](support-policies).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

### Can I configure all my clusters in a single subscription to use the same maintenance configuration?

We don't recommend using the same maintenance configuration for multiple clusters in a single subscription, as doing so can lead to ARM throttling errors causing cluster upgrades to fail. Instead, we recommend staggering the maintenance windows for each cluster to avoid these errors.

### Why did my node pools get upgraded twice during the same maintenance window?

If a newer version of the node image becomes available during the maintenance window, AKS performs a second upgrade to ensure that your node pools are running the latest version. This behavior is normal and doesn't indicate an issue.

## Related content

To get started with upgrading your AKS cluster, see [Upgrade options for AKS clusters](upgrade-cluster).


---

<!-- DOCUMENTO FUSIONADO: _configure-static-egress-gateway_ai-toolchain-operator-monitoring.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-static-egress-gateway.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-static-egress-gateway -->

# Configure Static Egress Gateway in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Static Egress Gateway in AKS provides a streamlined solution for configuring fixed source IP addresses for outbound traffic from your AKS workloads. This feature allows you to route egress traffic through a dedicated "gateway node pool". By using the Static Egress Gateway, you can efficiently manage and control outbound IP addresses and ensure that your AKS workloads can communicate with external systems securely and consistently, using predefined IPs.

This article provides step-by-step instructions to set up a Static Egress Gateway node pool in your AKS cluster, enabling you to configure fixed source IP addresses for outbound traffic from your Kubernetes workloads.

## Limitations and considerations

Static Egress Gateway isn't supported in clusters with

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet).Kubernetes network policies won't apply to traffic leaving the cluster through the gateway node pool.

- This shouldn't affect cluster traffic control as
**only**egress traffic from annotated pods**routed to the gateway node pool**are affected.

- This shouldn't affect cluster traffic control as
The gateway node pool isn't intended for general-purpose workloads and should be used for egress traffic only.

Windows node pools can't be used as gateway node pools.

hostNetwork pods

**cannot**be annotated to use the gateway node pool.Pods can only use a gateway node pool if they are in the same namespace as the

`StaticGatewayConfiguration`

resource.

## Create or update an AKS cluster with Static Egress Gateway

Before you can create and manage gateway node pools, you must enable the Static Egress Gateway feature for your AKS cluster. You can do this when creating a new cluster or by updating an existing cluster using `az aks update`

.

```
az aks create -n <cluster-name> -g <resource-group> --enable-static-egress-gateway
```


## Create a Gateway Node pool

After enabling the feature, create a dedicated gateway node pool. This node pool handles the egress traffic through the specified public IP prefix. The `--gateway-prefix-size`

is the size of the public IP prefix to be applied to the gateway node pool nodes. The allowed range is `28`

-`31`

.

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--gateway-prefix-size <prefix-size>
```


Note

- The number of nodes must fit within the capacity allowed by the selected prefix size. For example, a /30 prefix supports up to 4 nodes, and at least 2 nodes are required for high availability. Since you can’t adjust the node count dynamically, plan your nodes according to the fixed limit set by the prefix size.
- You can define the SKU of the VM to use in your gateway node pool with the
`--vm-size`

parameter. You should understand your specific needs and plan accordingly to ensure the right performance and cost balance.

## Scale the Gateway Node pool (Optional)

If necessary, you can resize the gateway node pool within the limits defined by the prefix size but it doesn't support autoscaling.

```
az aks nodepool scale --cluster-name <cluster-name> -n <nodepool-name> --node-count <desired-node-count>
```


## Create a Static Gateway Configuration

Define the gateway configuration by creating a `StaticGatewayConfiguration`

custom resource. This configuration specifies which node pool and public IP prefix to use.

```
apiVersion: egressgateway.kubernetes.azure.com/v1alpha1
kind: StaticGatewayConfiguration
metadata:
name: <gateway-config-name>
namespace: <namespace>
spec:
gatewayNodepoolName: <nodepool-name>
excludeCidrs: # Optional
- 10.0.0.0/8
- 172.16.0.0/12
- 169.254.169.254/32
publicIpPrefixId: /subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Network/publicIPPrefixes/<prefix-name> # Optional
```


Tip

If you don't set `publicIpPrefixId`

, a public IP prefix will be created for you automatically. When running `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, you can see the "Egress Ip Prefix" in the status. This is the newly created public IP prefix. You can also use an existing public IP prefix by specifying its resource ID in the `publicIpPrefixId`

argument. You need to grant "Network Contributor" role to AKS cluster's identity in this case.

### Static Private IP Support (Preview)

Important

Static private IP support requires clusters running Kubernetes version 1.34 or later and a subscription with the `Microsoft.ContainerService/StaticEgressGatewayPreview`

Azure Feature Exposure Control (AFEC) flag enabled. Follow [Register preview feature](/en-us/azure/azure-resource-manager/management/preview-features#register-preview-feature) to request the feature flag before creating the Gateway VirtualMachines node pool.

If you must keep egress traffic on private addresses, enable private IP support on the gateway node pool. Use the same `az aks nodepool add`

command and set the node pool to use the VirtualMachines VM set type while disabling public IP provisioning:

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--vm-set-type VirtualMachines \
--gateway-prefix-size <prefix-size>
```


In this configuration, the `provisionPublicIps=false`

setting keeps the private IPs allocated to the gateway nodes for the lifetime of the `StaticGatewayConfiguration`

. When you run `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, the `egressIpPrefix`

field shows a comma-separated list of those static private IPs. You continue to use the same APIs and manifests for the rest of the workflow, including the `StaticGatewayConfiguration`

resource and the pod annotations.

## Annotate Pods to Use the Gateway Configuration

To route traffic from specific pods through the gateway node pool, annotate the pod template in the deployment configuration.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: <deployment-name>
namespace: <namespace>
spec:
template:
metadata:
annotations:
kubernetes.azure.com/static-gateway-configuration: <gateway-config-name>
```


Note

The CNI plugin on each node will automatically configure the pod to route its traffic through the selected gateway nodepool.

## Monitor and Manage Gateway Configurations

Once deployed, you can monitor the status of your gateway configurations through the AKS cluster. The status section in the `StaticGatewayConfiguration`

resource is updated with details such as assigned IPs and WireGuard configurations.

## Delete a Gateway Node pool (Optional)

To remove a gateway node pool, ensure all associated configurations are appropriately handled before deletion.

```
az aks nodepool delete --cluster-name <cluster-name> -n <nodepool-name>
```


## Disable the Static Egress Gateway Feature (Optional)

If you no longer need the Static Egress Gateway, you can disable the feature and uninstall the operator. Ensure all gateway node pools are deleted first.

```
az aks update -n <cluster-name> -g <resource-group> --disable-static-egress-gateway
```


By following these steps, you can effectively set up and manage Static Egress Gateway configurations in your AKS cluster, enabling controlled and consistent egress traffic from your workloads.


---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator-monitoring.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-monitoring -->

# Monitor and visualize AI inference metrics on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Monitoring and observability play a key role in maintaining high performance and low cost of your AI workload deployments in Azure Kubernetes Service (AKS). Visibility into system and performance metrics can indicate the limits of your underlying infrastructure and motivate real-time adjustments and optimizations to reduce workload interruptions. Monitoring also provides valuable insights into resource utilization for cost-effective management of computational resources and accurate provisioning.

The Kubernetes AI Toolchain Operator (KAITO) is a managed add-on for AKS that simplifies deployment and operations for AI models in your AKS cluster.

In [KAITO version 0.4.4](https://github.com/kaito-project/kaito/releases/tag/v0.4.4) and later versions, the vLLM inference runtime is enabled by default in the AKS managed add-on. [vLLM](https://docs.vllm.ai/en/latest/) is a library for language model inference and serving. It surfaces key system performance, resource usage, and request processing for [Prometheus metrics](https://docs.vllm.ai/en/latest/design/v1/metrics.html) that you can use to evaluate your KAITO inference deployments.

In this article, you'll learn how to monitor and visualize vLLM inference metrics using the AI toolchain operator add-on with Azure Managed Prometheus and Azure Managed Grafana on your AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Install and configure Azure CLI version 2.47.0 or later. To find your version, run
`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- Install and configure kubectl, the Kubernetes command-line client. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Enable the
[AI toolchain operator add-on](ai-toolchain-operator)in your AKS cluster. - If you already have the AI toolchain operator add-on enabled, update your AKS cluster to the latest version to run KAITO v0.4.4 or later.
- Enable
[the managed service for Prometheus and Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable)in your AKS cluster. - Have permissions to
[create or update Azure Managed Grafana instances](/en-us/azure/managed-grafana/how-to-manage-access-permissions-users-identities)in your Azure subscription.

## Deploy a KAITO inference service

In this example, you collect metrics for the [Qwen-2.5-coder-7B-instruct language model](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).

Start by applying the following KAITO workspace custom resource to your cluster:

`kubectl apply -f https://raw.githubusercontent.com/Azure/kaito/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml`

Track the live resource changes in your KAITO workspace:

`kubectl get workspace workspace-qwen-2-5-coder-7b-instruct -w`

Note

Machine readiness can take up to 10 minutes, and workspace readiness can take up to 20 minutes depending on the size of your language model.

Confirm that your inference service is running and get the service IP address:

`export SERVICE_IP=$(kubectl get svc workspace-qwen-2-5-coder-7b-instruct -o jsonpath='{.spec.clusterIP}') echo $SERVICE_IP`


## Surface KAITO inference metrics to the managed service for Prometheus

Prometheus metrics are collected by default at the KAITO [ /metrics endpoint](https://github.com/kaito-project/kaito/tree/main).

Add the following label to your KAITO inference service so that a Kubernetes

`ServiceMonitor`

deployment can detect it:`kubectl label svc workspace-qwen-2-5-coder-7b-instruct App=qwen-2-5-coder`

Create a

`ServiceMonitor`

resource to define the inference service endpoints and the required configurations to scrape the vLLM Prometheus metrics. Export these metrics to the managed service for Prometheus by deploying the following`ServiceMonitor`

YAML manifest in the`kube-system`

namespace:`cat <<EOF | kubectl apply -n kube-system -f - apiVersion: azmonitoring.coreos.com/v1 kind: ServiceMonitor metadata: name: prometheus-kaito-monitor spec: selector: matchLabels: App: qwen-2-5-coder endpoints: - port: http interval: 30s path: /metrics scheme: http EOF`

Check for the following output to verify that

`ServiceMonitor`

is created:`servicemonitor.azmonitoring.coreos.com/prometheus-kaito-monitor created`

Verify that your

`ServiceMonitor`

deployment is running successfully:`kubectl get servicemonitor prometheus-kaito-monitor -n kube-system`

In the Azure portal, verify that vLLM metrics are successfully collected in the managed service for Prometheus.

In your Azure Monitor workspace, go to

**Managed Prometheus**>**Prometheus explorer**.Select the

**Grid**tab and confirm that a metrics item is associated with the job named`workspace-qwen-2-5-coder-7b-instruct`

.Note

The

`up`

value of this item should be`1`

. A value of`1`

indicates that Prometheus metrics are successfully being scraped from your AI inference service endpoint.


## Visualize KAITO inference metrics in Azure Managed Grafana

The vLLM project provides a Grafana dashboard configuration named

[grafana.json](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)for inference workload monitoring. Navigate to the bottom of this[page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file.Go to the bottom of the

[examples page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file:Complete the steps to

[import the Grafana configurations into a new dashboard](/en-us/azure/managed-grafana/how-to-create-dashboard#import-a-json-dashboard)in Azure Managed Grafana.Go to your Managed Grafana endpoint, view the available dashboards, and select the

**vLLM**dashboard.To begin collecting data for your selected model deployment, confirm that the

**datasource**value shown at the top left of the Grafana dashboard is your instance of the managed service for Prometheus you created for this example.Copy the inference preset name defined in your KAITO workspace to the

**model_name**field in the Grafana dashboard. In this example, the model name is[qwen2.5-coder-7b-instruct](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).In a few moments, verify that the metrics for your KAITO inference service appear in the vLLM Grafana dashboard.

Note

The value of these inference metrics remains

**0**until the requests are submitted to the model inference server.

## Related content

[Monitor and visualize](monitor-aks)your AKS deployments at scale.- Test and monitor
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling)on your cluster. [Fine-tune an AI model](ai-toolchain-operator-fine-tune)by using the AI toolchain operator add-on in AKS.- Learn about AKS GPU workload deployment options on
[Linux](gpu-cluster)and[Windows](use-windows-gpu)nodes.


---

<!-- DOCUMENTO FUSIONADO: __artifact-streaming_quickstart-dapr__keda-deploy-add-on-arm_app-routing.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _artifact-streaming_quickstart-dapr.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: artifact-streaming.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/artifact-streaming -->

# Reduce image pull time with Artifact Streaming on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

High performance compute workloads often involve large images, which can cause long image pull times and slow down your workload deployments. Artifact Streaming on AKS allows you to stream container images from Azure Container Registry (ACR) to AKS. AKS only pulls the necessary layers for initial pod startup, reducing the time it takes to pull images and deploy your workloads.

Artifact Streaming can reduce time to pod readiness by over 15%, depending on the size of the image, and it works best for images <30GB. Based on our testing, we saw reductions in pod start-up times for images <10GB from minutes to seconds. If you have a pod that needs access to a large file (>30GB), then you should mount it as a volume instead of building it as a layer. This is because if your pod requires that file to start, it congests the node. Artifact Streaming isn't ideal for read heavy images from your filesystem if you need that on startup. With Artifact Streaming, pod start-up becomes concurrent, whereas without it, pods start in serial.

This article describes how to enable the Artifact Streaming feature on your AKS node pools to stream artifacts from ACR.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Artifact Streaming (preview) is a suggested alternative for customers previously using Teleport (preview).
[Teleport (preview)](https://github.com/Azure/acr/blob/main/docs/teleport/aks-getting-started.md) on AKS will be retired on 15 July 2025. Please migrate to Artifact Streaming (preview) on AKS or update your node pools to set `--aks-custom-headers EnableACRTeleport=false`

.
Azure Container Registry removed the Teleport API, meaning that any nodes with Teleport enabled will pull images from Azure Container Registry like any other AKS node without Teleport.
After 15 July 2025, AKS node pools with Teleport enabled might experience breakage and node provisioning failures. For more information, see [aka.ms/aks/teleport-retirement](https://aka.ms/aks/teleport-retirement).

## Limitations

- Artifact Steaming isn't supported for the following OS options:
[Windows Server versions](windows-best-practices),[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

## Prerequisites

- You need an existing AKS cluster with ACR integration. If you don't have one, you can create one using
[Authenticate with ACR from AKS](cluster-container-registry-integration). [Enable Artifact Streaming on ACR](#enable-artifact-streaming-on-acr).- This feature requires Kubernetes version 1.25 or later. To check your AKS cluster version, see
[Check for available AKS cluster upgrades](upgrade-cluster).

Note

Artifact Streaming is only supported on Ubuntu 22.04, Ubuntu 20.04, and Azure Linux node pools. Windows node pools aren't supported.

## Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the `ArtifactStreamingPreview`

feature flag in your subscription

Register the

`ArtifactStreamingPreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ArtifactStreamingPreview`


## Enable Artifact Streaming on ACR

Enablement on ACR is a prerequisite for Artifact Streaming on AKS. For more information, see [Artifact Streaming on ACR](https://aka.ms/acr/artifact-streaming).

Create an Azure resource group to hold your ACR instance using the

command.`az group create`

`az group create --name myStreamingTest --location westus`

Create a new premium SKU Azure Container Registry using the

command with the`az acr create`

`--sku Premium`

flag.`az acr create --resource-group myStreamingTest --name mystreamingtest --sku Premium`

Configure the default ACR instance for your subscription using the

command.`az configure`

`az configure --defaults acr="mystreamingtest"`

Push or import an image to the registry using the

command.`az acr import`

`az acr import --source docker.io/jupyter/all-spark-notebook:latest --repository jupyter/all-spark-notebook:latest`

Create a streaming artifact from the image using the

command.`az acr artifact-streaming create`

`az acr artifact-streaming create --image jupyter/all-spark-notebook:latest`

Verify the generated Artifact Streaming using the

command.`az acr manifest list-referrers`

`az acr manifest list-referrers --name jupyter/all-spark-notebook:latest`


## Enable Artifact Streaming on AKS

### Enable Artifact Streaming on a new node pool

Create a new node pool with Artifact Streaming enabled using the

command with the`az aks nodepool add`

`--enable-artifact-streaming`

.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


### Enable Artifact Streaming on an existing node pool

Update an existing node pool to enable Artifact Streaming using the

command with the`az aks nodepool update`

`--enable-artifact-streaming`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


## Check if Artifact Streaming is enabled

Now that you enabled Artifact Streaming on a premium ACR and connected that to an AKS node pool with Artifact Streaming enabled, any new pod deployments on this cluster with an image pull from the ACR with Artifact Streaming enabled will see reductions in image pull times.

Check if your node pool has Artifact Streaming enabled using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name myNodePool --query artifactStreamingProfile`

In the output, check that the

`Enabled`

field is set to`true`

.

## Next steps

This article described how to enable Artifact Streaming on your AKS node pools to stream artifacts from ACR and reduce image pull time. To learn more about working with container images in AKS, see [Best practices for container image management and security in AKS](operator-best-practices-container-image-management).


---

<!-- DOCUMENTO FUSIONADO: quickstart-dapr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/quickstart-dapr -->

# Quickstart: Deploy an application using the Dapr cluster extension for Azure Kubernetes Service (AKS) or Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the [Dapr cluster extension](dapr-overview) in an AKS or Arc-enabled Kubernetes cluster. You deploy [a hello world example](https://github.com/Azure-Samples/dapr-aks-extension-quickstart), which consists of a Python application that generates messages and a Node.js application that consumes and persists the messages.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.- An AKS Cluster with:
[Workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)enabled[Managed identity](workload-identity-deploy-cluster#create-a-managed-identity)created in the same subscription[A Kubernetes service account](workload-identity-deploy-cluster#create-a-kubernetes-service-account)[Federated identity credential](workload-identity-deploy-cluster#create-the-federated-identity-credential)[Dapr cluster extension](dapr-overview)installed on the AKS cluster

[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)installed locally.

## Clone the repository

Clone the

[Dapr quickstarts repository](https://github.com/Azure-Samples/dapr-aks-extension-quickstart)using the`git clone`

command.`git clone https://github.com/Azure-Samples/dapr-aks-extension-quickstart.git`

Change to the

`dapr-aks-extension-quickstart`

directory.

## Create and configure a Redis store

Open the [Azure portal](https://portal.azure.com/#create/Microsoft.Cache) to start the Azure Cache for Redis creation flow.

- Fill out the recommended information according to
[the "Create an open-source Redis cache" quickstart instructions](/en-us/azure/azure-cache-for-redis/quickstart-create-redis). - Select
**Create**to start the Redis instance deployment.

### Verify resource information

- Once the Redis resource is deployed, navigate to its overview page.
- Take note of:
- The hostname, found in the
**Essentials**section of the cache overview page. The hostname format looks similar to:`xxxxxx.redis.cache.windows.net`

. - The SSL port, found in the cache's
**Advanced Settings**blade. The default value is`6380`

.

- The hostname, found in the
- Navigate to the
**Authentication**blade and verify Microsoft Entra Authentication is enabled on your resource.

### Add managed identity

In the

**Authentication**blade, type the name of the[Managed Identity you created as a prerequisite](#prerequisites)in the field under**Enable Microsoft Entra Authentication**checkbox.Verify your managed identity is added as a Redis User assigned Data Owner Access Policy permissions.


### Enable public network access

For this scenario, your Redis cache uses public network access. Be sure to [clean up resources](#clean-up-resources) when you're finished with this quickstart.

- Navigate to the
**Private Endpoint**blade. - Click
**Enable public network access**from the top menu.

## Configure the Dapr components

In `redis.yaml`

, the component is configured to use Entra ID Authentication using workload identity enabled for AKS cluster. No access keys are required.

```
- name: useEntraID
value: "true"
- name: enableTLS
value: true
```


In your preferred code editor, navigate to the

`deploy`

directory in the sample and open`redis.yaml`

.For

`redisHost`

, replace the placeholder`<REDIS_HOST>:<REDIS_PORT>`

value with the Redis cache hostname and SSL port[you saved earlier from Azure portal](#verify-resource-information).`- name: redisHost value: <your-cache-name>.redis.cache.windows.net:6380`


### Apply the configuration

Apply the

`redis.yaml`

file using the`kubectl apply`

command.`kubectl apply -f ./deploy/redis.yaml`

Verify your state store was successfully configured using the

`kubectl get components.redis`

command.`kubectl get components.redis -o yaml`

**Expected output**`component.dapr.io/statestore created`


## Deploy the Node.js app with the Dapr sidecar

### Configure the Node.js app

In `node.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`node.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Apply the Node.js app deployment to your cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/node.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/nodeapp`

Access your service using the

`kubectl get svc`

command.`kubectl get svc nodeapp`

Make note of the

`EXTERNAL-IP`

in the output.

### Verify the Node.js service

Using

`curl`

, call the service with your`EXTERNAL-IP`

.`curl $EXTERNAL_IP/ports`

**Example output**`{"DAPR_HTTP_PORT":"3500","DAPR_GRPC_PORT":"50001"}`

Submit an order to the application.

`curl --request POST --data "@sample.json" --header Content-Type:application/json $EXTERNAL_IP/neworder`

Confirm the order.

`curl $EXTERNAL_IP/order`

**Expected output**`{ "orderId": "42" }`


## Deploy the Python app with the Dapr sidecar

### Configure the Python app

In `python.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`python.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Deploy the Python app to your Kubernetes cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/python.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/pythonapp`


## Observe messages and confirm persistence

Now that both the Node.js and Python applications are deployed, you can watch messages come through.

Get the logs of the Node.js app using the

`kubectl logs`

command.`kubectl logs --selector=app=node -c node --tail=-1`

**Expected output**`Got a new order! Order ID: 1 Successfully persisted state Got a new order! Order ID: 2 Successfully persisted state Got a new order! Order ID: 3 Successfully persisted state`

Using

`curl`

, call the Node.js app's order endpoint to get the latest order.`curl $EXTERNAL_IP/order`

You should see the latest JSON output in the response.


## Clean up resources

If you no longer plan to use the resources from this quickstart, you can delete all associated resources by removing the resource group.

Remove the resource group, cluster, namespace, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name MyResourceGroup
```


---

<!-- DOCUMENTO FUSIONADO: _keda-deploy-add-on-arm_app-routing.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: keda-deploy-add-on-arm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-arm -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to deploy the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using an [ARM template](/en-us/azure/azure-resource-manager/templates/).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - This article assumes you have an existing Azure resource group. If you don't have an existing resource group, you can create one using the
command.`az group create`

- Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules). [Create an SSH key pair](#create-an-ssh-key-pair).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Create an SSH key pair

Navigate to the

[Azure Cloud Shell](https://shell.azure.com/).Create an SSH key pair using the

command.`az sshkey create`

`az sshkey create --name <sshkey-name> --resource-group <resource-group-name>`


## Enable the KEDA add-on with an ARM template

Deploy the

[ARM template for an AKS cluster](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.kubernetes%2Faks%2Fazuredeploy.json).Select

**Edit template**.Enable the KEDA add-on by specifying the

`workloadAutoScalerProfile`

field in the ARM template, as shown in the following example:`"workloadAutoScalerProfile": { "keda": { "enabled": true } }`

Select

**Save**.Update the required values for the ARM template:

**Subscription**: Select the Azure subscription to use for the deployment.**Resource group**: Select the resource group to use for the deployment.**Region**: Select the region to use for the deployment.**Dns Prefix**: Enter a unique DNS name to use for the cluster.**Linux Admin Username**: Enter a username for the cluster.**SSH public key source**: Select**Use existing key stored in Azure**.**Store Keys**: Select the key pair you created earlier in the article.

Select

**Review + create**>**Create**.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local device, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client.

If you use the Azure Cloud Shell, `kubectl`

is already installed. You can also install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

- Configure
`kubectl`

to connect to your Kubernetes cluster, use the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following example gets credentials for the AKS cluster named*MyAKSCluster*in the*MyResourceGroup*:

```
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```


## Example deployment

The following snippet is a sample deployment that creates a cluster with KEDA enabled with a single node pool comprised of three `DS2_v5`

nodes.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"resources": [
{
"apiVersion": "2023-03-01",
"dependsOn": [],
"type": "Microsoft.ContainerService/managedClusters",
"location": "westcentralus",
"name": "myAKSCluster",
"properties": {
"kubernetesVersion": "1.27",
"enableRBAC": true,
"dnsPrefix": "myAKSCluster",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": 200,
"count": 3,
"enableAutoScaling": false,
"vmSize": "Standard_D2S_v5",
"osType": "Linux",
"type": "VirtualMachineScaleSets",
"mode": "System",
"maxPods": 110,
"availabilityZones": [],
"nodeTaints": [],
"enableNodePublicIP": false
}
],
"networkProfile": {
"loadBalancerSku": "standard",
"networkPlugin": "kubenet"
},
"workloadAutoScalerProfile": {
"keda": {
"enabled": true
}
}
},
"identity": {
"type": "SystemAssigned"
}
}
]
}
```


## Start scaling apps with KEDA

You can autoscale your apps with KEDA using custom resource definitions (CRDs). For more information, see the [KEDA documentation](https://keda.sh/docs/scalers/).

## Remove resources

Remove the resource group and all related resources using the

command.`az group delete`

`az group delete --name <resource-group-name>`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster, and then verify that it's installed and running. With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).


---

<!-- DOCUMENTO FUSIONADO: app-routing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One way to route Hypertext Transfer Protocol (HTTP) and secure (HTTPS) traffic to applications running on an Azure Kubernetes Service (AKS) cluster is to use the [Kubernetes Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/). When you create an Ingress object that uses the application routing add-on NGINX Ingress classes, the add-on creates, configures, and manages one or more Ingress controllers in your AKS cluster.

This article shows you how to deploy and configure a basic Ingress controller in your AKS cluster.

## Application routing add-on with NGINX features

The application routing add-on with NGINX delivers the following:

- Easy configuration of managed NGINX Ingress controllers based on
[Kubernetes NGINX Ingress controller](https://kubernetes.github.io/ingress-nginx/). - Integration with
[Azure DNS](/en-us/azure/dns/dns-overview)for public and private zone management - SSL termination with certificates stored in Azure Key Vault.

For other configurations, see:

[DNS and SSL configuration](app-routing-dns-ssl)[Application routing add-on configuration](app-routing-nginx-configuration)[Configure internal NGIX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).

With the retirement of [Open Service Mesh](https://release-v1-2.docs.openservicemesh.io/) (OSM) by the Cloud Native Computing Foundation (CNCF), using the application routing add-on with OSM is not recommended.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.54.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- The application routing add-on supports up to five Azure DNS zones.
- The application routing add-on can only be enabled on AKS clusters with
[managed identity](use-managed-identity). - All global Azure DNS zones integrated with the add-on have to be in the same resource group.
- All private Azure DNS zones integrated with the add-on have to be in the same resource group.
- Editing the ingress-nginx
`ConfigMap`

in the`app-routing-system`

namespace isn't supported. - The following snippet annotations are blocked and will prevent an Ingress from being configured:
`load_module`

,`lua_package`

,`_by_lua`

,`location`

,`root`

,`proxy_pass`

,`serviceaccount`

,`{`

,`}`

,`'`

.

## Enable application routing using Azure CLI

### Enable on a new cluster

To enable application routing on a new cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command, specifying the

`--enable-app-routing`

flag.```
az aks create \
--resource-group <ResourceGroupName> \
--name <ClusterName> \
--location <Location> \
--enable-app-routing \
--generate-ssh-keys
```


### Enable on an existing cluster

To enable application routing on an existing cluster, use the [ az aks approuting enable](/en-us/cli/azure/aks/approuting#az-aks-approuting-enable) command.

```
az aks approuting enable --resource-group <ResourceGroupName> --name <ClusterName>
```


## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
```


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest will create the necessary deployments and services for the AKS store application.

### Create the Ingress object

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the `kubectl get ingress`

command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front webapprouting.kubernetes.azure.com * 51.8.10.109 80 110s
```


You can verify that the AKS store works pointing your browser to the public IP address of the Ingress controller. Find the IP address with kubectl:

```
kubectl get service -n app-routing-system nginx -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```


## Remove the application routing add-on

To remove the associated namespace, use the `kubectl delete namespace`

command.

```
kubectl delete namespace aks-store
```


To remove the application routing add-on from your cluster, use the [ az aks approuting disable](/en-us/cli/azure/aks/approuting#az-aks-approuting-disable) command.

```
az aks approuting disable --name <ClusterName> --resource-group <ResourceGroupName>
```


Note

To avoid potential disruption of traffic into the cluster when the application routing add-on is disabled, some Kubernetes resources, including *configMaps*, *secrets*, and the *deployment* that runs the controller, will remain on the cluster. These resources are in the *app-routing-system* namespace. You can remove these resources if they're no longer needed by deleting the namespace with `kubectl delete ns app-routing-system`

.

## Next steps

[Configure custom ingress configurations](app-routing-nginx-configuration)shows how to create an advanced Ingress configuration and[configure a custom domain using Azure DNS to manage DNS zones and setup a secure ingress](app-routing-dns-ssl).To integrate with an Azure internal load balancer and configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains, see

[Configure internal NGINX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with

[with Prometheus in Grafana](app-routing-nginx-prometheus)(preview) as part of analyzing the performance and usage of your application.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/openfaas -->

# Use OpenFaaS on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[OpenFaaS](https://www.openfaas.com/) is a framework that uses containers to build serverless functions. As an open source project, it has gained large-scale adoption within the community. This document details installing and using OpenFaas on an Azure Kubernetes Service (AKS) cluster.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - You need an active Azure subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - You need an AKS cluster. If you don't have an existing cluster, you can create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - You need to install the OpenFaaS CLI. For installation options, see the
[OpenFaaS CLI documentation](https://github.com/openfaas/faas-cli).

## Add the OpenFaaS helm chart repo

Navigate to

[Azure Cloud Shell](https://shell.azure.com).Add the OpenFaaS helm chart repo and update to the latest version using the following

`helm`

commands.`helm repo add openfaas https://openfaas.github.io/faas-netes/ helm repo update`


## Deploy OpenFaaS

As a good practice, OpenFaaS and OpenFaaS functions should be stored in their own Kubernetes namespace.

Create a namespace for the OpenFaaS system and functions using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/openfaas/faas-netes/master/namespaces.yml`

Generate a password for the OpenFaaS UI Portal and REST API using the following commands. The helm chart uses this password to enable basic authentication on the OpenFaaS Gateway, which is exposed to the Internet through a cloud LoadBalancer.

`# generate a random password PASSWORD=$(head -c 12 /dev/urandom | shasum| cut -d' ' -f1) kubectl -n openfaas create secret generic basic-auth \ --from-literal=basic-auth-user=admin \ --from-literal=basic-auth-password="$PASSWORD"`

Important

Using a username and password for authentication is an insecure pattern. If you have an OpenFaaS enterprise license, we recommend using

[Identity and Access Management (IAM) for OpenFaaS](https://www.openfaas.com/blog/walkthrough-iam-for-openfaas/)instead.Get the value for your password using the following

`echo`

command.`echo $PASSWORD`

Deploy OpenFaaS into your AKS cluster using the

`helm upgrade`

command.`helm upgrade openfaas --install openfaas/openfaas \ --namespace openfaas \ --set basic_auth=true \ --set functionNamespace=openfaas-fn \ --set serviceType=LoadBalancer`

Your output should look similar to the following condensed example output:

`NAME: openfaas LAST DEPLOYED: Tue Aug 29 08:26:11 2023 NAMESPACE: openfaas STATUS: deployed ... NOTES: To verify that openfaas has started, run: kubectl --namespace=openfaas get deployments -l "release=openfaas, app=openfaas" ...`

A public IP address is created for accessing the OpenFaaS gateway. Get the IP address using the

command.`kubectl get service`

`kubectl get service -l component=gateway --namespace openfaas`

Your output should look similar to the following example output:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gateway ClusterIP 10.0.156.194 <none> 8080/TCP 7m gateway-external LoadBalancer 10.0.28.18 52.186.64.52 8080:30800/TCP 7m`

Test the OpenFaaS system by browsing to the external IP address on port 8080,

`http://52.186.64.52:8080`

in this example, where you're prompted to log in. The default user is`admin`

and your password can be retrieved using`echo $PASSWORD`

.Set

`$OPENFAAS_URL`

to the URL of the external IP address on port 8080 and log in with the Azure CLI using the following commands.`export OPENFAAS_URL=http://52.186.64.52:8080 echo -n $PASSWORD | ./faas-cli login -g $OPENFAAS_URL -u admin --password-stdin`


## Create first function

Navigate to the OpenFaaS system using your OpenFaaS URL.

Create a function using the OpenFaas portal by selecting

**Deploy A New Function**and search for**Figlet**.Select the

**Figlet**function, and then select**Deploy**.Invoke the function using the following

`curl`

command. Make sure you replace the IP address in the following example with your OpenFaaS gateway address.`curl -X POST http://52.186.64.52:8080/function/figlet -d "Hello Azure"`

Your output should look similar to the following example output:

`_ _ _ _ _ | | | | ___| | | ___ / \ _____ _ _ __ ___ | |_| |/ _ \ | |/ _ \ / _ \ |_ / | | | '__/ _ \ | _ | __/ | | (_) | / ___ \ / /| |_| | | | __/ |_| |_|\___|_|_|\___/ /_/ \_\/___|\__,_|_| \___|`


## Create second function

### Configure your Azure Cosmos DB instance

Navigate to

[Azure Cloud Shell](https://shell.azure.com).Create a new resource group for the Azure Cosmos DB instance using the

command.`az group create`

`az group create --name serverless-backing --location eastus`

Deploy an Azure Cosmos DB instance of kind

`MongoDB`

using thecommand. Replace`az cosmosdb create`

`openfaas-cosmos`

with your own unique instance name.`az cosmosdb create --resource-group serverless-backing --name openfaas-cosmos --kind MongoDB`

Get the Azure Cosmos DB database connection string and store it in a variable using the

command. Make sure you replace the value for the`az cosmosdb keys list`

`--resource-group`

argument with the name of your resource group, and the`--name`

argument with the name of your Azure Cosmos DB instance.`COSMOS=$(az cosmosdb keys list \ --type connection-strings \ --resource-group serverless-backing \ --name openfaas-cosmos \ --output tsv)`

Populate the Azure Cosmos DB with test data by creating a file named

`plans.json`

and copying in the following json.`{ "name" : "two_person", "friendlyName" : "Two Person Plan", "portionSize" : "1-2 Person", "mealsPerWeek" : "3 Unique meals per week", "price" : 72, "description" : "Our basic plan, delivering 3 meals per week, which will feed 1-2 people.", "__v" : 0 }`


### Create the function

Install the MongoDB tools. The following example command installs these tools using brew. For more installation options, see the

[MongoDB documentation](https://docs.mongodb.com/manual/installation/).`brew install mongodb`

Load the Azure Cosmos DB instance with data using the

*mongoimport*tool.`mongoimport --uri=$COSMOS -c plans < plans.json`

Your output should look similar to the following example output:

`2018-02-19T14:42:14.313+0000 connected to: localhost 2018-02-19T14:42:14.918+0000 imported 1 document`

Create the function using the

`faas-cli deploy`

command. Make sure you update the value of the`-g`

argument with your OpenFaaS gateway address.`faas-cli deploy -g http://52.186.64.52:8080 --image=shanepeckham/openfaascosmos --name=cosmos-query --env=NODE_ENV=$COSMOS`

Once deployed, your output should look similar to the following example output:

`Deployed. 202 Accepted. URL: http://52.186.64.52:8080/function/cosmos-query`

Test the function using the following

`curl`

command. Make sure you update the IP address with the OpenFaaS gateway address.`curl -s http://52.186.64.52:8080/function/cosmos-query`

Your output should look similar to the following example output:

`[{"ID":"","Name":"two_person","FriendlyName":"","PortionSize":"","MealsPerWeek":"","Price":72,"Description":"Our basic plan, delivering 3 meals per week, which will feed 1-2 people."}]`

Note

You can also test the function within the OpenFaaS UI:


## Next steps

Continue to learn with the [OpenFaaS workshop](https://github.com/openfaas/workshop), which includes a set of hands-on labs that cover topics such as how to create your own GitHub bot, consuming secrets, viewing metrics, and autoscaling.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux-os-guard -->

# Azure Linux with OS Guard (preview) for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Azure Linux with OS Guard (preview) on Azure Kubernetes Service (AKS), including key features, region availability, and resources to get started.

## What is Azure Linux with OS Guard?

Azure Linux with OS Guard is a hardened, immutable variant of Azure Linux. It provides strong runtime integrity, tamper resistance, and enterprise-grade security for container hosts on AKS. OS Guard is built on Azure Linux and adds kernel and runtime features that enforce code integrity, protect the root file system from unauthorized changes, and apply mandatory access controls.

You can deploy Azure Linux with OS Guard node pools in a new cluster, add Azure Linux with OS Guard node pools to your existing Azure Linux or Ubuntu clusters, or migrate your Azure Linux or Ubuntu nodes to Azure Linux with OS Guard nodes.

To learn more about Azure Linux with OS Guard, see the [Azure Linux with OS Guard documentation](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

## Why use Azure Linux with OS Guard on AKS?

Azure Linux with OS Guard on AKS builds on the benefits of [Azure Linux](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-key-benefits) by adding enhanced security features that help protect your container workloads from advanced threats. OS Guard provides:

**Immutability**: The`/usr`

directory is mounted as a read-only volume protected by dm-verity, preventing execution of tampered or untrusted code.**Code integrity**: OS Guard integrates the[Integrity Policy Enforcement (IPE) Linux Security Module](https://docs.kernel.org/next/admin-guide/LSM/ipe.html)to ensure that only binaries from trusted, signed volumes are allowed to execute. (**IPE is running in audit mode during Public Preview**.)**Mandatory access controls**: OS Guard integrates SELinux to limit which processes can access sensitive resources in the system. (**SELinux is operating in permissive mode during Public Preview**.)**Integration with Azure security features**: Native support for[Trusted Launch](/en-us/azure/aks/use-trusted-launch)and Secure Boot provides measured boot protections and attestation.**Verified container layers**: Container images and layers are validated using signed dm-verity hashes. This ensures that only verified layers are used at runtime, reducing the risk of container escape or tampering.**Sovereign Supply Chain Security**: OS Guard inherits Azure Linux’s secure build pipelines, signed Unified Kernel Images (UKIs) and Software Bill of Materials (SBOMs).

Learn more about the [key features of Azure Linux with OS Guard](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

## Regional availability

Azure Linux with OS Guard is available for use in the same [regions](/en-us/azure/aks/quotas-skus-regions) as AKS.

## Get started with Azure Linux with OS Guard on AKS

Get started with Azure Linux with OS Guard on AKS using the following resources:

[Creating a cluster with Azure Linux with OS Guard](/en-us/azure/azure-linux/quickstart-os-guard-azure-cli)[How to upgrade Azure Linux with OS Guard clusters](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-upgrade)[Add an Azure Linux with OS Guard node pool to your existing cluster](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-add-node-pool)[Migrate to Azure Linux with OS Guard](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-migration)[Enable telemetry and monitoring on an Azure Linux with OS Guard cluster](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-telemetry-monitor)

## Next steps

To learn more about Azure Linux with OS Guard, see the [Azure Linux with OS Guard documentation](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-hpc -->

# Use Windows HostProcess containers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

HostProcess / Privileged containers extend the Windows container model to enable a wider range of Kubernetes cluster management scenarios. HostProcess containers run directly on the host and maintain behavior and access similar to that of a regular process. HostProcess containers allow users to package and distribute management operations and functionalities that require host access while retaining versioning and deployment methods provided by containers.

A privileged DaemonSet can carry out changes or monitor a Linux host on Kubernetes but not Windows hosts. HostProcess containers are the Windows equivalent of host elevation.

## Limitations

- HostProcess containers require Kubernetes 1.23 or greater.
- HostProcess containers require
`containerd`

1.6 or higher container runtime. - HostProcess pods can only contain HostProcess containers due to a limitation on the Windows operating system. Non-privileged Windows containers can't share a vNIC with the host IP namespace.
- HostProcess containers run as a process on the host. The only isolation those containers have from the host is the resource constraints imposed on the HostProcess user account.
- Filesystem isolation and Hyper-V isolation aren't supported for HostProcess containers.
- Volume mounts are supported and are mounted under the container volume. See Volume Mounts.
- A limited set of host user accounts are available for Host Process containers by default. See Choosing a User Account.
- Resource limits such as disk, memory, and cpu count, work the same way as fashion as processes on the host.
- Named pipe mounts and Unix domain sockets aren't directly supported, but can be accessed on their host path, for example
`\\.\pipe\*`

.

## Run a HostProcess workload

To use HostProcess features with your deployment, set *hostProcess: true* and *hostNetwork: true*:

```
spec:
...
securityContext:
windowsOptions:
hostProcess: true
...
hostNetwork: true
containers:
...
```


To run an example workload that uses HostProcess features on an existing AKS cluster with Windows nodes, create `hostprocess.yaml`

with the following contents:

```
apiVersion: apps/v1
kind: DaemonSet
metadata:
name: privileged-daemonset
namespace: kube-system
labels:
app: privileged-daemonset
spec:
selector:
matchLabels:
app: privileged-daemonset
template:
metadata:
labels:
app: privileged-daemonset
spec:
nodeSelector:
kubernetes.io/os: windows
securityContext:
windowsOptions:
hostProcess: true
runAsUserName: "NT AUTHORITY\\SYSTEM"
hostNetwork: true
containers:
- name: powershell
image: mcr.microsoft.com/windows/nanoserver:ltsc2019 # or nanoserver:ltsc2022
command:
- powershell.exe
- -Command
- Start-Sleep -Seconds 2147483
terminationGracePeriodSeconds: 0
```


Use `kubectl`

to run the example workload:

```
kubectl apply -f hostprocess.yaml
```


You should see the following output:

```
$ kubectl apply -f hostprocess.yaml
daemonset.apps/privileged-daemonset created
```


Verify that your workload uses the features of HostProcess containers by viewing the pod's logs.

Use `kubectl`

to find the name of the pod in the `kube-system`

namespace.

```
$ kubectl get pods --namespace kube-system
NAME READY STATUS RESTARTS AGE
...
privileged-daemonset-12345 1/1 Running 0 2m13s
```


Use `kubectl log`

to view the logs of the pod and verify the pod has administrator rights:

```
$ kubectl logs privileged-daemonset-12345 --namespace kube-system
InvalidOperation: Unable to find type [Security.Principal.WindowsPrincipal].
Process has admin rights:
```


## Next steps

For more information on HostProcess containers and Microsoft's contribution to Kubernetes upstream, see the [Alpha in v1.22: Windows HostProcess Containers](https://kubernetes.io/blog/2021/08/16/windows-hostprocess-containers/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-ad-integration-cli -->

# Integrate Microsoft Entra ID with Azure Kubernetes Service (AKS) using the Azure CLI (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Warning

The feature described in this document, Microsoft Entra Integration (legacy) was **deprecated on June 1st, 2023**. At this time, no new clusters can be created with Microsoft Entra Integration (legacy).

AKS has a new improved [AKS-managed Microsoft Entra ID](managed-azure-ad) experience that doesn't require you to manage server or client applications. If you want to migrate follow the instructions [here](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration).

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you can log into an AKS cluster using a Microsoft Entra authentication token. Cluster operators can also configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership.

This article shows you how to create the required Microsoft Entra components, then deploy a Microsoft Entra ID-enabled cluster and create a basic Kubernetes role in the AKS cluster.

## Limitations

- Microsoft Entra ID can only be enabled on Kubernetes RBAC-enabled cluster.
- Microsoft Entra legacy integration can only be enabled during cluster creation.

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Go to [https://shell.azure.com](https://shell.azure.com) to open Cloud Shell in your browser.

For consistency and to help run the commands in this article, create a variable for your desired AKS cluster name. The following example uses the name *myakscluster*:

```
aksname="myakscluster"
```


## Microsoft Entra authentication overview

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc).

From inside of the Kubernetes cluster, Webhook Token Authentication is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster. For more information on Webhook token authentication, see the [webhook authentication documentation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication).

Note

When configuring Microsoft Entra ID for AKS authentication, two Microsoft Entra applications are configured. This operation must be completed by an Azure tenant administrator.

## Create Microsoft Entra server component

To integrate with AKS, you create and use a Microsoft Entra application that acts as an endpoint for the identity requests. The first Microsoft Entra application you need gets Microsoft Entra group membership for a user.

Create the server application component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command, then update the group membership claims using the [az ad app update](/en-us/cli/azure/ad/app#az-ad-app-update) command. The following example uses the *aksname* variable defined in the [Before you begin](#before-you-begin) section, and creates a variable

```
# Create the Azure AD application
serverApplicationId=$(az ad app create \
--display-name "${aksname}Server" \
--identifier-uris "https://${aksname}Server" \
--query appId -o tsv)
# Update the application group membership claims
az ad app update --id $serverApplicationId --set groupMembershipClaims=All
```


Now create a service principal for the server app using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command. This service principal is used to authenticate itself within the Azure platform. Then, get the service principal secret using the [az ad sp credential reset](/en-us/cli/azure/ad/sp/credential#az-ad-sp-credential-reset) command and assign to the variable named *serverApplicationSecret* for use in one of the following steps:

```
# Create a service principal for the Azure AD application
az ad sp create --id $serverApplicationId
# Get the service principal secret
serverApplicationSecret=$(az ad sp credential reset \
--name $serverApplicationId \
--credential-description "AKSPassword" \
--query password -o tsv)
```


The Microsoft Entra service principal needs permissions to perform the following actions:

- Read directory data
- Sign in and read user profile

Assign these permissions using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command:

```
az ad app permission add \
--id $serverApplicationId \
--api 00000003-0000-0000-c000-000000000000 \
--api-permissions e1fe6dd8-ba31-4d61-89e7-88639da4683d=Scope 06da0dbc-49e2-44d2-8312-53f166ab848a=Scope 7ab1d382-f21e-4acd-a863-ba3e13f7da61=Role
```


Finally, grant the permissions assigned in the previous step for the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command. This step fails if the current account is not a tenant admin. You also need to add permissions for Microsoft Entra application to request information that may otherwise require administrative consent using the [az ad app permission admin-consent](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-admin-consent):

```
az ad app permission grant --id $serverApplicationId --api 00000003-0000-0000-c000-000000000000
az ad app permission admin-consent --id $serverApplicationId
```


## Create Microsoft Entra client component

The second Microsoft Entra application is used when a user logs to the AKS cluster with the Kubernetes CLI (`kubectl`

). This client application takes the authentication request from the user and verifies their credentials and permissions. Create the Microsoft Entra app for the client component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command:

```
clientApplicationId=$(az ad app create \
--display-name "${aksname}Client" \
--native-app \
--reply-urls "https://${aksname}Client" \
--query appId -o tsv)
```


Create a service principal for the client application using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command:

```
az ad sp create --id $clientApplicationId
```


Get the oAuth2 ID for the server app to allow the authentication flow between the two app components using the [az ad app show](/en-us/cli/azure/ad/app#az-ad-app-show) command. This oAuth2 ID is used in the next step.

```
oAuthPermissionId=$(az ad app show --id $serverApplicationId --query "oauth2Permissions[0].id" -o tsv)
```


Add the permissions for the client application and server application components to use the oAuth2 communication flow using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command. Then, grant permissions for the client application to communication with the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command:

```
az ad app permission add --id $clientApplicationId --api $serverApplicationId --api-permissions ${oAuthPermissionId}=Scope
az ad app permission grant --id $clientApplicationId --api $serverApplicationId
```


## Deploy the cluster

With the two Microsoft Entra applications created, now create the AKS cluster itself. First, create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command. The following example creates the resource group in the *EastUS* region:

Create a resource group for the cluster:

```
az group create --name myResourceGroup --location EastUS
```


Get the tenant ID of your Azure subscription using the [az account show](/en-us/cli/azure/account#az-account-show) command. Then, create the AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The command to create the AKS cluster provides the server and client application IDs, the server application service principal secret, and your tenant ID:

```
tenantId=$(az account show --query tenantId -o tsv)
az aks create \
--resource-group myResourceGroup \
--name $aksname \
--node-count 1 \
--generate-ssh-keys \
--aad-server-app-id $serverApplicationId \
--aad-server-app-secret $serverApplicationSecret \
--aad-client-app-id $clientApplicationId \
--aad-tenant-id $tenantId
```


Finally, get the cluster admin credentials using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. In one of the following steps, you get the regular *user* cluster credentials to see the Microsoft Entra authentication flow in action.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --admin
```


## Create Kubernetes RBAC binding

Before a Microsoft Entra account can be used with the AKS cluster, a role binding or cluster role binding needs to be created. *Roles* define the permissions to grant, and *bindings* apply them to desired users. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see [Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).

Get the user principal name (UPN) for the user currently logged in using the [az ad signed-in-user show](/en-us/cli/azure/ad/signed-in-user#az-ad-signed-in-user-show) command. This user account is enabled for Microsoft Entra integration in the next step.

```
az ad signed-in-user show --query userPrincipalName -o tsv
```


Important

If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the *userPrincipalName*. If the user is in a different Microsoft Entra tenant, query for and use the *objectId* property instead.

Create a YAML manifest named `basic-azure-ad-binding.yaml`

and paste the following contents. On the last line, replace *userPrincipalName_or_objectId* with the UPN or object ID output from the previous command:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
name: contoso-cluster-admins
roleRef:
apiGroup: rbac.authorization.k8s.io
kind: ClusterRole
name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
kind: User
name: userPrincipalName_or_objectId
```


Create the ClusterRoleBinding using the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify the filename of your YAML manifest:

```
kubectl apply -f basic-azure-ad-binding.yaml
```


## Access cluster with Microsoft Entra ID

Now let's test the integration of Microsoft Entra authentication for the AKS cluster. Set the `kubectl`

config context to use regular user credentials. This context passes all authentication requests back through Microsoft Entra ID.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --overwrite-existing
```


Now use the [kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to view pods across all namespaces:

```
kubectl get pods --all-namespaces
```


You receive a sign in prompt to authenticate using Microsoft Entra credentials using a web browser. After you've successfully authenticated, the `kubectl`

command displays the pods in the AKS cluster, as shown in the following example output:

```
kubectl get pods --all-namespaces
```


```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code BYMK7UXVD to authenticate.
NAMESPACE NAME READY STATUS RESTARTS AGE
kube-system coredns-754f947b4-2v75r 1/1 Running 0 23h
kube-system coredns-754f947b4-tghwh 1/1 Running 0 23h
kube-system coredns-autoscaler-6fcdb7d64-4wkvp 1/1 Running 0 23h
kube-system heapster-5fb7488d97-t5wzk 2/2 Running 0 23h
kube-system kube-proxy-2nd5m 1/1 Running 0 23h
kube-system kube-svc-redirect-swp9r 2/2 Running 0 23h
kube-system kubernetes-dashboard-847bb4ddc6-trt7m 1/1 Running 0 23h
kube-system metrics-server-7b97f9cd9-btxzz 1/1 Running 0 23h
kube-system tunnelfront-6ff887cffb-xkfmq 1/1 Running 0 23h
```


The authentication token received for `kubectl`

is cached. You are only reprompted to sign in when the token has expired or the Kubernetes config file is re-created.

If you see an authorization error message after you've successfully signed in using a web browser as in the following example output, check the following possible issues:

```
error: You must be logged in to the server (Unauthorized)
```


- You defined the appropriate object ID or UPN, depending on if the user account is in the same Microsoft Entra tenant or not.
- The user is not a member of more than 200 groups.
- Secret defined in the application registration for server matches the value configured using
`--aad-server-app-secret`

- Be sure that only one version of kubectl is installed on your machine at a time. Conflicting versions can cause issues during authorization. To install the latest version, use
[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli).

## Frequently asked questions about migration from Microsoft Entra Integration to AKS-managed Microsoft Entra ID

**1. What is the plan for migration?**

Microsoft Entra Integration (legacy) will be deprecated on 1st June 2023. After this date, you won't be able to create new clusters with Microsoft Entra ID (legacy). We'll migrate all Microsoft Entra Integration (legacy) AKS clusters to AKS-managed Microsoft Entra ID automatically starting from 1st August 2023. We send notification emails to impacted subscription admins biweekly to remind them of migration.

**2. What will happen if I don't take any action?**

Your Microsoft Entra Integration (legacy) AKS clusters will continue working after 1st June 2023. We'll automatically migrate your clusters to AKS-managed Microsoft Entra ID starting from 1st August 2023. You may experience API server downtime during the migration.

The kubeconfig content changes after the migration. You need to merge the new credentials into the kubeconfig file using the `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

.

We recommend updating your AKS cluster to [AKS-managed Microsoft Entra ID](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration) manually before 1st August. This way you can manage the downtime during non-business hours when it's more convenient.

**3. Why do I still receive the notification email after manual migration?**

It takes several days for the email to send. If your cluster wasn't migrated before we initiate the email-sending process, you may still receive a notification.

**4. How can I check whether my cluster my cluster is migrated to AKS-managed Microsoft Entra ID?**

Confirm your AKS cluster is migrated to the AKS-managed Microsoft Entra ID using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command.

```
az aks show -g <RGName> -n <ClusterName> --query "aadProfile"
```


If your cluster is using the AKS-managed Microsoft Entra ID, the output shows `managed`

is `true`

. For example:

```
{
"adminGroupObjectIDs": [
"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
],
"adminUsers": null,
"clientAppId": null,
"enableAzureRbac": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


## Next steps

For the complete script that contains the commands shown in this article, see the [Microsoft Entra integration script in the AKS samples repo][complete-script].

To use Microsoft Entra users and groups to control access to cluster resources, see [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

For more information about how to secure Kubernetes clusters, see [Access and identity options for AKS)](concepts-identity#kubernetes-rbac).

For best practices on identity and resource control, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-app-cluster-reliability -->

# Deployment and cluster reliability best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides best practices for cluster reliability implemented both at a deployment and cluster level for your Azure Kubernetes Service (AKS) workloads. The article is intended for cluster operators and developers who are responsible for deploying and managing applications in AKS.

The best practices in this article are organized into the following categories:

## Deployment level best practices

The following deployment level best practices help ensure high availability and reliability for your AKS workloads. These best practices are local configurations that you can implement in the YAML files for your pods and deployments.

Note

Make sure you implement these best practices every time you deploy an update to your application. If not, you might experience issues with your application's availability and reliability, such as unintentional application downtime.

### Pod CPU and memory limits


Best practice guidanceSet pod CPU and memory limits for all pods to ensure that pods don't consume all resources on a node and to provide protection during service threats, such as DDoS attacks.


Pod CPU and memory limits define the maximum amount of CPU and memory a pod can use. When a pod exceeds its defined limits, it gets marked for removal. For more information, see [CPU resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu) and [Memory resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory).

Setting CPU and memory limits helps you maintain node health and minimizes impact to other pods on the node. Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. If you set a pod limit higher than the node can support, your application might try to consume too many resources and negatively impact other pods on the node. Cluster administrators need to set resource quotas on a namespace that requires setting resource requests and limits. For more information, see [Enforce resource quotas in AKS](operator-best-practices-scheduler#enforce-resource-quotas).

In the following example pod definition file, the `resources`

section sets the CPU and memory limits for the pod:

```
kind: Pod
apiVersion: v1
metadata:
name: mypod
spec:
containers:
- name: mypod
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
```


Tip

You can use the `kubectl describe node`

command to view the CPU and memory capacity of your nodes, as shown in the following example:

```
kubectl describe node <node-name>
# Example output
Capacity:
cpu: 8
ephemeral-storage: 129886128Ki
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 32863116Ki
pods: 110
Allocatable:
cpu: 7820m
ephemeral-storage: 119703055367
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 28362636Ki
pods: 110
```


For more information, see [Assign CPU Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) and [Assign Memory Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/).

### Vertical Pod Autoscaler (VPA)


Best practice guidanceUse Vertical Pod Autoscaler (VPA) to automatically adjust CPU and memory requests for your pods based on their actual usage.


While not directly implemented through the pod YAML, the Vertical Pod Autoscaler (VPA) helps optimize resource allocation by automatically adjusting the CPU and memory requests for your pods. This ensures that your applications have the resources they need to run efficiently without overprovisioning or underprovisioning.

VPA operates in three modes:

**Off**: Only provides recommendations without applying changes.**Auto**: Automatically updates pod resource requests during pod restarts.**Initial**: Sets resource requests only during pod creation.

The following example shows how to configure a VPA resource in Kubernetes:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: my-vpa
spec:
targetRef:
apiVersion: "apps/v1"
kind: Deployment
name: my-deployment
updatePolicy:
updateMode: "Auto" # Options: Off, Auto, Initial
```


For more information, see [Vertical Pod Autoscaler documentation](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler).

### Pod Disruption Budgets (PDBs)


Best practice guidanceUse Pod Disruption Budgets (PDBs) to ensure that a minimum number of pods remain available during

voluntary disruptions, such as upgrade operations or accidental pod deletions.

[Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets) allow you to define how deployments or replica sets respond during voluntary disruptions, such as upgrade operations or accidental pod deletions. Using PDBs, you can define a minimum or maximum unavailable resource count. PDBs only affect the Eviction API for voluntary disruptions.

For example, let's say you need to perform a cluster upgrade and already have a PDB defined. Before performing the cluster upgrade, the Kubernetes scheduler ensures that the minimum number of pods defined in the PDB are available. If the upgrade would cause the number of available pods to fall below the minimum defined in the PDBs, the scheduler schedules extra pods on other nodes before allowing the upgrade to proceed. If you don't set a PDB, the scheduler doesn't have any constraints on the number of pods that can be unavailable during the upgrade, which can lead to a lack of resources and potential cluster outages.

In the following example PDB definition file, the `minAvailable`

field sets the minimum number of pods that must remain available during voluntary disruptions. The value can be an absolute number (for example, *3*) or a percentage of the desired number of pods (for example, *10%*).

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: mypdb
spec:
minAvailable: 3 # Minimum number of pods that must remain available during voluntary disruptions
selector:
matchLabels:
app: myapp
```


For more information, see [Plan for availability using PDBs](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets) and [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

### Graceful termination for pods


Best practice guidanceUtilize

`PreStop`

hooks and configure an appropriate`terminationGracePeriodSeconds`

value to ensure pods are terminated gracefully.

Graceful termination ensures that pods are given enough time to clean up resources, complete ongoing tasks, or notify dependent services before being terminated. This is particularly important for stateful applications or services that require proper shutdown procedures.

#### Using `PreStop`

hooks

A `PreStop`

hook is called immediately before a container is terminated due to an API request or management event, such as preemption, resource contention, or a liveness/startup probe failure. The `PreStop`

hook allows you to define custom commands or scripts to execute before the container is stopped. For example, you can use it to flush logs, close database connections, or notify other services of the shutdown.

The following example pod definition file shows how to use a `PreStop`

hook to ensure graceful termination of a container:

```
apiVersion: v1
kind: Pod
metadata:
name: lifecycle-demo
spec:
containers:
- name: lifecycle-demo-container
image: nginx
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "nginx -s quit; while killall -0 nginx; do sleep 1; done"]
```


#### Configuring `terminationGracePeriodSeconds`


The `terminationGracePeriodSeconds`

field specifies the amount of time Kubernetes waits before forcefully terminating a pod. This period includes the time taken to execute the `PreStop`

hook. If the `PreStop`

hook doesn't complete within the grace period, the pod is forcefully terminated.

For example, the following pod definition sets a termination grace period of 30 seconds:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
terminationGracePeriodSeconds: 30
containers:
- name: example-container
image: nginx
```


For more information, see [Container lifecycle hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks) and [Termination of Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination).

### High availability during upgrades

#### Using `maxSurge`

for faster updates


Best practice guidanceConfigure the

`maxSurge`

field to allow additional pods to be created during rolling updates, enabling faster updates with minimal downtime.

The `maxSurge`

field specifies the maximum number of additional pods that can be created beyond the desired number of pods during a rolling update. This allows new pods to be created and become ready before old pods are terminated, ensuring faster updates and reducing the risk of downtime.

The following example deployment manifest demonstrates how to configure `maxSurge`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxSurge: 33% # Maximum number of additional pods created during the update
```


By setting `maxSurge`

to 3, this configuration ensures that up to three additional pods can be created during the rolling update, speeding up the deployment process while maintaining availability of your application.
For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

#### Using `maxUnavailable`

for controlled updates


Best practice guidanceConfigure the

`maxUnavailable`

field to limit the number of pods that can be unavailable during rolling updates, ensuring your application remains operational with minimal disruption.

The `maxUnavailable`

field is particularly useful for applications that require are compute intensive or have specific infrastructure needs. It specifies the maximum number of pods that can be unavailable at any given time during a rolling update. This ensures that a portion of your application remains functional while new pods are being deployed and old ones are terminated.

You can set `maxUnavailable`

as an absolute number (e.g., `1`

) or a percentage of the desired number of pods (e.g., `25%`

). For example, if your application has four replicas and you set `maxUnavailable`

to `1`

, Kubernetes ensures that at least three pods remain available during the update process.

The following example deployment manifest demonstrates how to configure `maxUnavailable`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 4
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxUnavailable: 1 # Maximum number of pods that can be unavailable during the update
```


In this example, setting `maxUnavailable`

to `1`

ensures that no more than one pod is unavailable at any given time during the rolling update. This configuration is ideal for applications which require specialized compute, where maintaining a minimum level of service availability is critical.

For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

### Pod topology spread constraints


Best practice guidanceUse pod topology spread constraints to ensure that pods are spread across different nodes or zones to improve availability and reliability.


You can use pod topology spread constraints to control how pods are spread across your cluster based on the topology of the nodes and spread pods across different nodes or zones to improve availability and reliability.

The following example pod definition file shows how to use the `topologySpreadConstraints`

field to spread pods across different nodes:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
# Configure a topology spread constraint
topologySpreadConstraints:
- maxSkew: <integer>
minDomains: <integer> # optional
topologyKey: <string>
whenUnsatisfiable: <string>
labelSelector: <object>
matchLabelKeys: <list> # optional
nodeAffinityPolicy: [Honor|Ignore] # optional
nodeTaintsPolicy: [Honor|Ignore] # optional
```


For more information, see [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/).

### Readiness, liveness, and startup probes


Best practice guidanceConfigure readiness, liveness, and startup probes when applicable to improve resiliency for high loads and lower container restarts.


#### Readiness probes

In Kubernetes, the kubelet uses readiness probes to know when a container is ready to start accepting traffic. A pod is considered *ready* when all of its containers are ready. When a pod is *not ready*, it's removed from service load balancers. For more information, see [Readiness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes).

The following example pod definition file shows a readiness probe configuration:

```
readinessProbe:
exec:
command:
- cat
- /tmp/healthy
initialDelaySeconds: 5
periodSeconds: 5
```


For more information, see [Configure readiness probes](/en-us/azure/container-instances/container-instances-readiness-probe).

#### Liveness probes

In Kubernetes, the kubelet uses liveness probes to know when to restart a container. If a container fails its liveness probe, the container is restarted. For more information, see [Liveness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/).

The following example pod definition file shows a liveness probe configuration:

```
livenessProbe:
exec:
command:
- cat
- /tmp/healthy
```


Another kind of liveness probe uses an HTTP GET request. The following example pod definition file shows an HTTP GET request liveness probe configuration:

```
apiVersion: v1
kind: Pod
metadata:
labels:
test: liveness
name: liveness-http
spec:
containers:
- name: liveness
image: registry.k8s.io/liveness
args:
- /server
livenessProbe:
httpGet:
path: /healthz
port: 8080
httpHeaders:
- name: Custom-Header
value: Awesome
initialDelaySeconds: 3
periodSeconds: 3
```


For more information, see [Configure liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) and [Define a liveness HTTP request](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-http-request).

#### Startup probes

In Kubernetes, the kubelet uses startup probes to know when a container application has started. When you configure a startup probe, readiness and liveness probes don't start until the startup probe succeeds, ensuring the readiness and liveness probes don't interfere with application startup. For more information, see [Startup Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes).

The following example pod definition file shows a startup probe configuration:

```
startupProbe:
httpGet:
path: /healthz
port: 8080
failureThreshold: 30
periodSeconds: 10
```


### Multi-replica applications


Best practice guidanceDeploy at least two replicas of your application to ensure high availability and resiliency in node-down scenarios.


In Kubernetes, you can use the `replicas`

field in your deployment to specify the number of pods you want to run. Running multiple instances of your application helps ensure high availability and resiliency in node-down scenarios. If you have [availability zones](#availability-zones) enabled, you can use the `replicas`

field to specify the number of pods you want to run across multiple availability zones.

The following example pod definition file shows how to use the `replicas`

field to specify the number of pods you want to run:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
```


For more information, see [Recommended active-active high availability solution overview for AKS](active-active-solution) and [Replicas in Deployment Specs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#replicas).

## Cluster and node pool level best practices

The following cluster and node pool level best practices help ensure high availability and reliability for your AKS clusters. You can implement these best practices when creating or updating your AKS clusters.

### Availability zones


Best practice guidanceUse multiple availability zones when creating an AKS cluster to ensure high availability in zone-down scenarios. Keep in mind that you can't change the availability zone configuration after creating the cluster.


[Availability zones](/en-us/azure/reliability/availability-zones-overview) are separated groups of datacenters within a region. These zones are close enough to have low-latency connections to each other, but far enough apart to reduce the likelihood that more than one zone is affected by local outages or weather. Using availability zones helps your data stay synchronized and accessible in zone-down scenarios. For more information, see [Running in multiple zones](https://kubernetes.io/docs/setup/best-practices/multiple-zones/).

### Cluster autoscaling


Best practice guidanceUse cluster autoscaling to ensure that your cluster can handle increased load and to reduce costs during low load.


To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed. For more information, see [Cluster autoscaling in AKS](cluster-autoscaler-overview).

You can use the `--enable-cluster-autoscaler`

parameter when creating an AKS cluster to enable the cluster autoscaler, as shown in the following example:

```
az aks create \
--resource-group myResourceGroup \
--name myAKSCluster \
--node-count 2 \
--vm-set-type VirtualMachineScaleSets \
--load-balancer-sku standard \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--generate-ssh-keys
```


You can also enable the cluster autoscaler on an existing node pool and configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile.

For more information, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

### Standard Load Balancer


Best practice guidanceUse the Standard Load Balancer to provide greater reliability and resources, support for multiple availability zones, HTTP probes, and functionality across multiple data centers.


In Azure, the [Standard Load Balancer](/en-us/azure/load-balancer/skus) SKU is designed to be equipped for load balancing network layer traffic when high performance and low latency are needed. The Standard Load Balancer routes traffic within and across regions and to availability zones for high resiliency. The Standard SKU is the recommended and default SKU to use when creating an AKS cluster.

Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). We recommend that you use the Standard Load Balancer for new deployments and upgrade existing deployments to the Standard Load Balancer. For more information, see [Upgrading from Basic Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance).

The following example shows a `LoadBalancer`

service manifest that uses the Standard Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-ipv4 # Service annotation for an IPv4 address
name: azure-load-balancer
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-load-balancer
```


For more information, see [Use a standard load balancer in AKS](load-balancer-standard).

Tip

You can also use an [ingress controller](app-routing) or a [service mesh](istio-deploy-ingress) to manage network traffic, with each option providing different features and capabilities.

### System node pools

#### Use dedicated system node pools


Best practice guidanceUse system node pools to ensure no other user applications run on the same nodes, which can cause resource scarcity and impact system pods.


Use dedicated system node pools to ensure no other user application runs on the same nodes, which can cause scarcity of resources and potential cluster outages because of race conditions. To use a dedicated system node pool, you can use the `CriticalAddonsOnly`

taint on the system node pool. For more information, see [Use system node pools in AKS](use-system-pools#system-and-user-node-pools).

#### Autoscaling for system node pools


Best practice guidanceConfigure the autoscaler for system node pools to set minimum and maximum scale limits for the node pool.


Use the autoscaler on node pools to configure the minimum and maximum scale limits for the node pool. The system node pool should always be able to scale to meet the demands of system pods. If the system node pool is unable to scale, the cluster runs out of resources to help manage scheduling, scaling, and load balancing, which can lead to an unresponsive cluster.

For more information, see [Use the cluster autoscaler on node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

#### At least two nodes per system node pool


Best practice guidanceEnsure that system node pools have at least two nodes to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down.


System node pools are used to run system pods, such as the kube-proxy, coredns, and the Azure CNI plugin. We recommend that you * ensure that system node pools have at least two nodes* to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down. For more information, see

[Manage system node pools in AKS](use-system-pools).

### Upgrade configurations for node pools

#### Using `maxSurge`

for node pool upgrades


Best practice guidanceConfigure the

`maxSurge`

setting for node pool upgrades to improve reliability and minimize downtime during upgrade operations.

The `maxSurge`

setting specifies the maximum number of additional nodes that can be created during an upgrade. This ensures that new nodes are provisioned and ready before old nodes are drained and removed, reducing the risk of application downtime.

For example, the following Azure CLI command sets `maxSurge`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-surge 1
```


By configuring `maxSurge`

, you can ensure that upgrades are performed faster while maintaining application availability.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).

#### Using `maxUnavailable`

for node pool upgrades


Best practice guidanceConfigure the

`maxUnavailable`

setting for node pool upgrades to ensure application availability during upgrade operations.

The `maxUnavailable`

setting specifies the maximum number of nodes that can be unavailable during an upgrade. This ensures that a portion of your node pool remains operational while nodes are being upgraded.

For example, the following Azure CLI command sets `maxUnavailable`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-unavailable 1
```


By configuring `maxUnavailable`

, you can control the impact of upgrades on your workloads, ensuring that sufficient resources remain available during the process.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).


Best practice guidanceUse Accelerated Networking to provide lower latency, reduced jitter, and decreased CPU utilization on your VMs.


Accelerated Networking enables [single root I/O virtualization (SR-IOV)](/en-us/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-) on [supported VM types](/en-us/azure/virtual-network/accelerated-networking-overview#supported-vm-instances), greatly improving networking performance.

The following diagram illustrates how two VMs communicate with and without Accelerated Networking:


For more information, see [Accelerated Networking overview](/en-us/azure/virtual-network/accelerated-networking-overview).

### Image versions


Best practice guidanceImages shouldn't use the

`latest`

tag.

#### Container image tags

Using the `latest`

tag for [container images](https://kubernetes.io/docs/concepts/containers/images/) can lead to unpredictable behavior and makes it difficult to track which version of the image is running in your cluster. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. For more information, see [Best practices for container image management in AKS](operator-best-practices-container-image-management).

#### Node image upgrades

AKS provides multiple auto-upgrade channels for node OS image upgrades. You can use these channels to control the timing of upgrades. We recommend joining these auto-upgrade channels to ensure that your nodes are running the latest security patches and updates. For more information, see [Auto-upgrade node OS images in AKS](auto-upgrade-node-os-image).

### Standard tier for production workloads


Best practice guidanceUse the Standard tier for product workloads for greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. If you need LTS, consider using the Premium tier.


The Standard tier for Azure Kubernetes Service (AKS) provides a financially backed 99.9% uptime [service-level agreement (SLA)](https://www.azure.cn/en-us/support/sla/kubernetes-service/) for your production workloads. The standard tier also provides greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

### Azure CNI for dynamic IP allocation


Best practice guidanceConfigure Azure CNI for dynamic IP allocation for better IP utilization and to prevent IP exhaustion for AKS clusters.


The dynamic IP allocation capability in Azure CNI allocates pod IPs from a subnet separate from the subnet hosting the AKS cluster and offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pod are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this solution.

For more information, see [Configure Azure CNI networking for dynamic allocation of IPs and enhanced subnet support](configure-azure-cni-dynamic-ip-allocation).

### v5 SKU VMs


Best practice guidanceUse v5 VM SKUs for improved performance during and after updates, less overall impact, and a more reliable connection for your applications.


For node pools in AKS, use v5 SKU VMs with ephemeral OS disks to provide sufficient compute resources for kube-system pods. For more information, see [Best practices for performance and scaling large workloads in AKS](best-practices-performance-scale-large).

### Do *not* use B series VMs


Best practice guidanceDon't use B series VMs for AKS clusters because they're low performance and don't work well with AKS.


B series VMs are low performance and don't work well with AKS. Instead, we recommend using [v5 SKU VMs](#v5-sku-vms).

### Premium Disks


Best practice guidanceUse Premium Disks to achieve 99.9% availability in one virtual machine (VM).


[Azure Premium Disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer a consistent submillisecond disk latency and high IOPS and throughout. Premium Disks are designed to provide low-latency, high-performance, and consistent disk performance for VMs.

The following example YAML manifest shows a [storage class definition](https://kubernetes.io/docs/concepts/storage/storage-classes/) for a premium disk:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: premium2-disk-sc
parameters:
cachingMode: None
skuName: PremiumV2_LRS
DiskIOPSReadWrite: "4000"
DiskMBpsReadWrite: "1000"
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
volumeBindingMode: Immediate
allowVolumeExpansion: true
```


For more information, see [Use Azure Premium SSD v2 disks on AKS](use-premium-v2-disks).

### Container Insights


Best practice guidanceEnable Container Insights to monitor and diagnose the performance of your containerized applications.


[Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview) is a feature of Azure Monitor that collects and analyzes container logs from AKS. You can analyze the collected data with a collection of [views](/en-us/azure/azure-monitor/containers/container-insights-analyze) and prebuilt [workbooks](/en-us/azure/azure-monitor/containers/container-insights-reports).

You can enable Container Insights monitoring on your AKS cluster using various methods. The following example shows how to enable Container Insights monitoring on an existing cluster using the Azure CLI:

```
az aks enable-addons -a monitoring --name myAKSCluster --resource-group myResourceGroup
```


For more information, see [Enable monitoring for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable).

### Azure Policy


Best practice guidanceApply and enforce security and compliance requirements for your AKS clusters using Azure Policy.


You can apply and enforce built-in security policies on your AKS clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives to your clusters.

For more information, see [Secure your AKS clusters with Azure Policy](use-azure-policy).

## Next steps

This article focused on best practices for deployment and cluster reliability for Azure Kubernetes Service (AKS) clusters. For more best practices, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption -->

# Enable KMS data encryption in Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Key Management Service (KMS) data encryption for Kubernetes secrets in Azure Kubernetes Service (AKS). KMS encryption encrypts Kubernetes secrets stored in etcd using Azure Key Vault keys.

AKS supports two key management options:

**Platform-managed keys (PMK)**: AKS automatically creates and manages the encryption keys. This option provides the simplest setup with automatic key rotation.**Customer-managed keys (CMK)**: You create and manage your own Azure Key Vault and encryption keys. This option provides full control over key lifecycle and meets compliance requirements that mandate customer-managed keys.

For more information about encryption concepts and key options, see [Data encryption at rest concepts for AKS](kms-data-encryption-concepts).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.73.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You need the
`aks-preview`

Azure CLI extension version*19.0.0b13*or later.- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
`kubectl`

CLI tool installed.

### Register the feature flag

To use KMS data encryption with platform-managed keys, register the `KMSPMKPreview`

feature flag in your subscription.

Register the feature flag using the

command.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name KMSPMKPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name KMSPMKPreview`

When the status shows

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Set up environment variables

Set up environment variables for your deployment. Replace the placeholder values with your own.

```
# Set environment variables
export SUBSCRIPTION_ID="<your-subscription-id>"
export RESOURCE_GROUP="<your-resource-group>"
export LOCATION="<your-location>"
export CLUSTER_NAME="<your-cluster-name>"
# Set subscription
az account set --subscription $SUBSCRIPTION_ID
# Create resource group if it doesn't exist
az group create --name $RESOURCE_GROUP --location $LOCATION
```


## Enable platform-managed key encryption

With platform-managed keys, AKS automatically creates and manages the Azure Key Vault and encryption keys. Key rotation is handled automatically by the platform.

### Create a new AKS cluster with platform-managed keys

Create a new AKS cluster with KMS encryption using platform-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--generate-ssh-keys
```


### Enable platform-managed keys on an existing cluster

Enable KMS encryption with platform-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a private key vault

For enhanced security, you can use a private key vault that has public network access disabled. AKS accesses the private key vault through the [trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only). This section shows how to configure customer-managed keys with a private key vault.

### Create a key vault and key with trusted services access

Note

This section illustrates creating a key vault with public network access initially, then enabling the firewall with trusted services bypass. This approach is for illustrative purposes only. In production environments, you should create and manage your key vault as private from the start. For guidance on managing private key vaults, see [Azure Key Vault network security](/en-us/azure/key-vault/general/network-security).

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`

Enable the key vault firewall with trusted services bypass.

`az keyvault update \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --default-action Deny \ --bypass AzureServices`

The

`--default-action Deny`

parameter blocks public network access, and the`--bypass AzureServices`

parameter allows trusted Azure services (including AKS) to access the key vault.

### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys (private)

Create a new AKS cluster with KMS encryption using customer-managed keys with a private key vault.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster (private)

Enable KMS encryption with customer-managed keys using a private key vault on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Private",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a public key vault

With customer-managed keys, you create and manage your own Azure Key Vault and encryption keys. This section shows how to configure customer-managed keys with a public key vault.

### Create a key vault and key

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`


### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys

Create a new AKS cluster with KMS encryption using customer-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster

Enable KMS encryption with customer-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Public",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Migrate between key management options

You can migrate between platform-managed keys and customer-managed keys.

### Migrate from platform-managed keys to customer-managed keys

To migrate from platform-managed keys to customer-managed keys, first set up the key vault, key, and managed identity as described in the customer-managed keys section, then run the update command:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Migrate from customer-managed keys to platform-managed keys

To migrate from customer-managed keys to platform-managed keys:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--disable-azure-keyvault-kms
```


## Key rotation

With KMS data encryption, key rotation is handled differently depending on your key management option:

**Platform-managed keys**: Key rotation is automatic. No action is required.**Customer-managed keys**: When you rotate the key version in Azure Key Vault, the KMS controller detects the rotation periodically (every 6 hours) and uses the new key version.

Note

Unlike the legacy KMS experience, with this new implementation you don't need to manually re-encrypt secrets after key rotation. The platform handles this automatically.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-pod-security -->

# Best practices for pod security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), the security of your pods is a key consideration. Your applications should be designed for the principle of least number of privileges required. Keeping private data secure is top of mind for customers. You don't want credentials like database connection strings, keys, or secrets and certificates exposed to the outside world where an attacker could take advantage of those secrets for malicious purposes. Don't add them to your code or embed them in your container images. This approach would create a risk for exposure and limit the ability to rotate those credentials as the container images will need to be rebuilt.

This best practices article focuses on how to secure pods in AKS. You learn how to:

- Use pod security context to limit access to processes and services or privilege escalation
- Authenticate with other Azure resources using Microsoft Entra Workload ID
- Request and retrieve credentials from a digital vault such as Azure Key Vault

You can also read the best practices for [cluster security](operator-best-practices-cluster-security) and for [container image management](operator-best-practices-container-image-management).

## Secure pod access to resources

**Best practice guidance** - To run as a different user or group and limit access to the underlying node processes and services, define pod security context settings. Assign the least number of privileges required.

For your applications to run correctly, pods should run as a defined user or group and not as *root*. The `securityContext`

for a pod or container lets you define settings such as *runAsUser* or *fsGroup* to assume the appropriate permissions. Only assign the required user or group permissions, and don't use the security context as a means to assume additional permissions. The *runAsUser*, privilege escalation, and other Linux capabilities settings are only available on Linux nodes and pods.

When you run as a non-root user, containers cannot bind to the privileged ports under 1024. In this scenario, Kubernetes Services can be used to disguise the fact that an app is running on a particular port.

A pod security context can also define additional capabilities or permissions for accessing processes and services. The following common security context definitions can be set:

**allowPrivilegeEscalation**defines if the pod can assume*root*privileges. Design your applications so this setting is always set to*false*.**Linux capabilities**let the pod access underlying node processes. Take care with assigning these capabilities. Assign the least number of privileges needed. For more information, see[Linux capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html).**SELinux labels**is a Linux kernel security module that lets you define access policies for services, processes, and filesystem access. Again, assign the least number of privileges needed. For more information, see[SELinux options in Kubernetes](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#selinuxoptions-v1-core)**hostUsers: false**the pod runs using a user-namespace, a Linux kernel feature. This significatly improves the host isolation and limits the lateral movement in case of container breakouts. These improvements are significant whether the container is running as root or not. For more information, see[user-namespaces](secure-container-access#user-namespaces).

The following example pod YAML manifest sets security context settings to define:

- Pod runs as user ID
*1000*and part of group ID*2000* - Can't escalate privileges to use
`root`

- Allows Linux capabilities to access network interfaces and the host's real-time (hardware) clock

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
fsGroup: 2000
containers:
- name: security-context-demo
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
securityContext:
runAsUser: 1000
allowPrivilegeEscalation: false
capabilities:
add: ["NET_ADMIN", "SYS_TIME"]
```


Work with your cluster operator to determine which security context settings you need. Design your applications to minimize other permissions and access the pod requires. There are other security features to limit access using AppArmor, seccomp (secure computing), and user-namespaces that can be implemented by cluster operators.

For more information, see [Secure container access to resources](operator-best-practices-cluster-security#secure-container-access-to-resources).

## Limit credential exposure

**Best practice guidance** - Don't define credentials in your application code. Use managed identities for Azure resources to let your pod request access to other resources. A digital vault, such as Azure Key Vault, should also be used to store and retrieve digital keys and credentials. Pod-managed identities are intended for use with Linux pods and container images only.

To limit the risk of credentials being exposed in your application code, avoid the use of fixed or shared credentials. Credentials or keys shouldn't be included directly in your code. If these credentials are exposed, the application needs to be updated and redeployed. A better approach is to give pods their own identity and way to authenticate themselves, or automatically retrieve credentials from a digital vault.

#### Use a Microsoft Entra Workload ID

A workload identity is an identity used by an application running on a pod that can authenticate itself against other Azure services that support it, such as Storage or SQL. It integrates with the capabilities native to Kubernetes to federate with external identity providers. In this security model, the AKS cluster acts as token issuer, Microsoft Entra ID uses OpenID Connect to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library using the [Azure SDK](https://azure.microsoft.com/downloads/) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL).

For more information about workload identities, see [Configure an AKS cluster to use Microsoft Entra Workload ID with your applications](workload-identity-overview)

#### Use Azure Key Vault with Secrets Store CSI Driver

Using the [Microsoft Entra Workload ID](workload-identity-overview) enables authentication against supporting Azure services. For your own services or applications without managed identities for Azure resources, you can still authenticate using credentials or keys. A digital vault can be used to store these secret contents.

When applications need a credential, they communicate with the digital vault, retrieve the latest secret contents, and then connect to the required service. Azure Key Vault can be this digital vault. The simplified workflow for retrieving a credential from Azure Key Vault using pod managed identities is shown in the following diagram:


With Key Vault, you store and regularly rotate secrets such as credentials, storage account keys, or certificates. You can integrate Azure Key Vault with an AKS cluster using the [Azure Key Vault provider for the Secrets Store CSI Driver](csi-secrets-store-driver). The Secrets Store CSI driver enables the AKS cluster to natively retrieve secret contents from Key Vault and securely provide them only to the requesting pod. Work with your cluster operator to deploy the Secrets Store CSI Driver onto AKS worker nodes. You can use a Microsoft Entra Workload ID to request access to Key Vault and retrieve the secret contents needed through the Secrets Store CSI Driver.

## Next steps

This article focused on how to secure your pods. To implement some of these areas, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-service-tags -->

# Use service tags for API server authorized IP ranges in Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Service tags for API server authorized IP ranges is a preview feature that allows you to use service tags to specify authorized IP ranges for the API server in Azure Kubernetes Service (AKS). This feature simplifies the management of authorized IP ranges by allowing you to use predefined service tags instead of manually specifying individual IP addresses or CIDR ranges.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The
installed.`aks-preview`

Azure CLI extension - The
registered in your Azure subscription.`EnableServiceTagAuthorizedIPPreview`

feature flag

## Limitations

- This feature isn't compatible with
[API Server VNet Integration](api-server-vnet-integration). - Only one service tag is allowed in the
`--api-server-authorized-ip-ranges`

parameter. You can't specify multiple service tags.

## Install the `aks-preview`

Azure CLI extension

Install the Azure CLI preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update the extension to make sure you have the latest version using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the service tag authorized IP feature flag

Register the

`EnableServiceTagAuthorizedIPPreview`

feature flag using thecommand. It takes a few minutes for the registration to complete.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registering" }, "type": "Microsoft.ContainerService/features" }`

Once the feature flag state changes from

`Registering`

to`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`

Verify the registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registered" }, "type": "Microsoft.ContainerService/features" }`


## Create an AKS cluster with service tag authorized IP ranges

Create a cluster with service tag authorized IP ranges using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the*myResourceGroup*resource group and authorizes the`AzureCloud`

service tag to allow all Azure services to access the API server and specify an extra IP address:`az aks create --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges AzureCloud,20.20.20.20`

Note

You should be able to curl the API server from an Azure virtual machine (VM) or Azure service that's part of the

`AzureCloud`

service tag.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/egress-udr -->

# Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize the egress for your Azure Kubernetes Service (AKS) clusters to fit specific scenarios. AKS provisions a `Standard`

SKU load balancer for egress by default. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or the scenario requires extra hops for egress.

This article walks through how to customize a cluster's egress route to support custom network scenarios. These scenarios include ones which disallow public IPs and require the cluster to sit behind a network virtual appliance (NVA).

## Prerequisites

- Azure CLI version 2.0.81 or greater. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - API version
`2020-01-01`

or greater.

## Requirements and limitations

Using outbound type is an advanced networking scenario and requires proper network configuration. The following requirements and limitations apply to using outbound type:

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and a`load-balancer-sku`

of`Standard`

. - Setting
`outboundType`

to a value of`UDR`

requires a user-defined route with valid outbound connectivity for the cluster. - Setting
`outboundType`

to a value of`UDR`

implies the ingress source IP routed to the load-balancer may**not match**the cluster's outgoing egress destination address.

## Overview of customizing egress with a user-defined routing table

AKS doesn't automatically configure egress paths if `userDefinedRouting`

is set, which means you must configure the egress.

When you don't use standard load balancer (SLB) architecture, you must establish explicit egress. You must deploy your AKS cluster into an existing virtual network with a subnet that has been previously configured. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, or proxy, so a public IP assigned to the standard load balancer or appliance can handle the Network Address Translation (NAT).

### Load balancer creation with `userDefinedRouting`


AKS clusters with an outbound type of UDR get a standard load balancer only when the first Kubernetes service of type `loadBalancer`

is deployed. The load balancer is configured with a public IP address for *inbound* requests and a backend pool for *inbound* requests. The Azure cloud provider configures inbound rules, but it **doesn't configure outbound public IP address or outbound rules**. Your UDR is the only source for egress traffic.

Note

Azure load balancers [don't incur a charge until a rule is placed](https://azure.microsoft.com/pricing/details/load-balancer/).

## Deploy a cluster with outbound type of UDR and Azure Firewall

To see an application of a cluster with outbound type using a user-defined route, see this [restrict egress traffic with Azure firewall example](limit-egress-traffic).

Important

Outbound type of UDR requires a route for 0.0.0.0/0 and a next hop destination of NVA in the route table.
The route table already has a default 0.0.0.0/0 to the Internet. Without a public IP address for Azure to use for Source Network Address Translation (SNAT), simply adding this route won't provide you outbound Internet connectivity. AKS validates that you don't create a 0.0.0.0/0 route pointing to the Internet but instead to a gateway, NVA, etc.
When using an outbound type of UDR, a load balancer public IP address for **inbound requests** isn't created unless you configure a service of type *loadbalancer*. AKS never creates a public IP address for **outbound requests** if you set an outbound type of UDR.

## Next steps

For more information on user-defined routes and Azure networking, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files -->

# Configure Azure NetApp Files for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods. A persistent volume can be used by one or many pods, and it can be statically or dynamically provisioned. This article shows you how to configure [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) to be used by pods on an Azure Kubernetes Service (AKS) cluster.

[Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) is an enterprise-class, high-performance, metered file storage service running on Azure and supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB). Kubernetes users have two options for using Azure NetApp Files volumes for Kubernetes workloads:

- Create Azure NetApp Files volumes
**statically**. In this scenario, the creation of volumes is external to AKS. Volumes are created using the Azure CLI or from the Azure portal, and are then exposed to Kubernetes by the creation of a`PersistentVolume`

. Statically created Azure NetApp Files volumes have many limitations (for example, inability to be expanded, needing to be over-provisioned, and so on). Statically created volumes aren't recommended for most use cases. - Create Azure NetApp Files volumes
**dynamically**, orchestrating through Kubernetes. This method is the**preferred**way to create multiple volumes directly through Kubernetes, and is achieved using[Trident](https://docs.netapp.com/us-en/trident/index.html). Trident is a CSI-compliant dynamic storage orchestrator that helps provision volumes natively through Kubernetes.

Note

Dual-protocol volumes can only be created **statically**. For more information on using dual-protocol volumes with Azure Kubernetes Service, see [Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol).

Using a CSI driver to directly consume Azure NetApp Files volumes from AKS workloads is the recommended configuration for most use cases. This requirement is accomplished using Trident, an open-source dynamic storage orchestrator for Kubernetes. Trident is an enterprise-grade storage orchestrator purpose-built for Kubernetes, and fully supported by NetApp. It simplifies access to storage from Kubernetes clusters by automating storage provisioning.

You can take advantage of Trident's Container Storage Interface (CSI) driver for Azure NetApp Files to abstract underlying details and create, expand, and snapshot volumes on-demand.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

The following considerations apply when you use Azure NetApp Files:

- Your AKS cluster must be
[in a region that supports Azure NetApp Files](https://azure.microsoft.com/global-infrastructure/services/?products=netapp®ions=all). - The Azure CLI version 2.0.59 or higher installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - After the initial deployment of an AKS cluster, you can choose to provision Azure NetApp Files volumes statically or dynamically.
- To use dynamic provisioning with Azure NetApp Files with Network File System (NFS), install and configure
[Trident](https://docs.netapp.com/us-en/trident/index.html)version 19.07 or higher. To use dynamic provisioning with Azure NetApp Files with Secure Message Block (SMB), install and configure Trident version 22.10 or higher. Dynamic provisioning for SMB shares is only supported on windows worker nodes. - Before you deploy Azure NetApp Files SMB volumes, you must identify the AD DS integration requirements for Azure NetApp Files to ensure that Azure NetApp Files is well connected to AD DS. For more information, see
[Understand guidelines for Active Directory Domain Services site design and planning](/en-us/azure/azure-netapp-files/understand-guidelines-active-directory-domain-service-site). Both the AKS cluster and Azure NetApp Files must have connectivity to the same AD.

## Configure Azure NetApp Files for AKS workloads

This section describes how to set up Azure NetApp Files for AKS workloads. It's applicable for all scenarios within this article.

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*poolsize*,*premium*,*myvnet*,*myANFSubnet*, and*myprefix*with appropriate values for your environment.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SIZE="poolsize" # size in TiB SERVICE_LEVEL="Premium" # valid values are Standard, Premium and Ultra VNET_NAME="myvnet" SUBNET_NAME="myANFSubnet" ADDRESS_PREFIX="myprefix"`

Register the

*Microsoft.NetApp*resource provider by running the following command:`az provider register --namespace Microsoft.NetApp --wait`

Note

This operation can take several minutes to complete.

Create a new account by using the command

. When you create an Azure NetApp account for use with AKS, you can create the account in an existing resource group or create a new one in the same region as the AKS cluster.`az netappfiles account create`

`az netappfiles account create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME`

Create a new capacity pool by using the command

. Replace the variables shown in the command with your Azure NetApp Files information. The`az netappfiles pool create`

`account_name`

should be the same as created in Step 3.`az netappfiles pool create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --size $SIZE \ --service-level $SERVICE_LEVEL`

Create a subnet to

[delegate to Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-delegate-subnet)using the command. Specify the resource group hosting the existing virtual network for your AKS cluster. Replace the variables shown in the command with your Azure NetApp Files information.`az network vnet subnet create`

Note

This subnet must be in the same virtual network as your AKS cluster.

`az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations "Microsoft.Netapp/volumes" \ --address-prefixes $ADDRESS_PREFIX`


## Statically or dynamically provision Azure NetApp Files volumes for NFS or SMB

After you [configure Azure NetApp Files for AKS workloads](#configure-azure-netapp-files-for-aks-workloads), you can statically or dynamically provision Azure NetApp Files using NFS, SMB, or dual-protocol volumes within the capacity pool. Follow instructions in:

[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs)[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb)[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cost-analysis -->

# Azure Kubernetes Service (AKS) cost analysis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to enable cost analysis on Azure Kubernetes Service (AKS) to view detailed cost data for cluster resources.

## About cost analysis

AKS clusters rely on Azure resources, such as virtual machines (VMs), virtual disks, load balancers, and public IP addresses. Multiple applications can use these resources. The resource consumption patterns often differ for each application, so their contribution toward the total cluster resource cost might also vary. Some applications might have footprints across multiple clusters, which can pose a challenge when performing cost attribution and cost management.

When you enable cost analysis on your AKS cluster, you can view detailed cost allocation scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. The add-on is built on top of [OpenCost](https://www.opencost.io/), an open-source Cloud Native Computing Foundation Incubating project for usage data collection. Usage data is reconciled with your Azure invoice data to provide a comprehensive view of your AKS cluster costs directly in the Azure portal Cost Management views.

For more information on Microsoft Cost Management, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

After enabling the cost analysis add-on and allowing time for data to be collected, you can use the information in [Understand AKS usage and costs](understand-aks-costs) to help you understand your data.

## Prerequisites

- Your cluster must use the
`Standard`

or`Premium`

tier, not the`Free`

tier. - To view cost analysis information, you must have one of the following roles on the subscription hosting the cluster:
`Owner`

,`Contributor`

,`Reader`

,`Cost Management Contributor`

, or`Cost Management Reader`

. [Managed identity](use-managed-identity)configured on your cluster.- If using the Azure CLI, you need version
`2.61.0`

or later installed. - Once you have enabled cost analysis, you can't downgrade your cluster to the
`Free`

tier without first disabling cost analysis. - Access to the Azure API including Azure Resource Manager (ARM) API. For a list of fully qualified domain names (FQDNs) required, see
[AKS Cost Analysis required FQDN](outbound-rules-control-egress#aks-cost-analysis-add-on).

## Limitations

- Kubernetes cost views are only available for the
*Enterprise Agreement*and*Microsoft Customer Agreement*Microsoft Azure offer types. For more information, see[Supported Microsoft Azure offers](/en-us/azure/cost-management-billing/costs/understand-cost-mgt-data#supported-microsoft-azure-offers). - Currently, virtual nodes aren't supported.

## Enable cost analysis on your AKS cluster

You can enable the cost analysis with the `--enable-cost-analysis`

flag during one of the following operations:

- Creating a
`Standard`

or`Premium`

tier AKS cluster. - Updating an existing
`Standard`

or`Premium`

tier AKS cluster. - Upgrading a
`Free`

cluster to`Standard`

or`Premium`

. - Upgrading a
`Standard`

cluster to`Premium`

. - Downgrading a
`Premium`

cluster to`Standard`

tier.

### Enable cost analysis on a new cluster

Enable cost analysis on a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--enable-cost-analysis`

flag. The following example creates a new AKS cluster in the `Standard`

tier with cost analysis enabled:```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="AKSCostRG$RANDOM_SUFFIX"
export CLUSTER_NAME="AKSCostCluster$RANDOM_SUFFIX"
export LOCATION="WestUS2"
az group create --resource-group $RESOURCE_GROUP --location $LOCATION
az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION --enable-managed-identity --generate-ssh-keys --tier standard --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"location": "WestUS2",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.ContainerService/managedClusters"
}
```


### Enable cost analysis on an existing cluster

Enable cost analysis on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-cost-analysis`

flag. The following example updates an existing AKS cluster in the `Standard`

tier to enable cost analysis:```
az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

An agent is deployed to the cluster when you enable the add-on. The agent consumes a small amount of CPU and Memory resources.

Warning

The AKS cost analysis add-on Memory usage is dependent on the number of containers deployed. You can roughly approximate Memory consumption using *200 MB + 0.5 MB per container*. The current Memory limit is set to *4 GB*, which supports approximately *7000 containers per cluster*. These estimates are subject to change.

Note

Enabling the cost analysis also creates a [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) named `cost-analysis-identity`

with read access to the cluster's node resource group, and assigns it to the node pools in the cluster.
This is used to collect the ARM identifiers of cluster assets for reporting.

Since there is already a managed identity for the node pool itself, any commands on the node that use managed identities will need to [specify the identity to use](/en-us/entra/identity/managed-identities-azure-resources/managed-identities-faq#what-identity-will-imds-default-to-if-i-dont-specify-the-identity-in-the-request) rather than relying on the default.

For example, `az login --identity --resource-id <resource ID of identity>`

.

## Disable cost analysis on your AKS cluster

Disable cost analysis using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--disable-cost-analysis`

flag.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

If you want to downgrade your cluster from the `Standard`

or `Premium`

tier to the `Free`

tier while cost analysis is enabled, you must first disable cost analysis.

## View the cost data

You can view cost allocation data in the Azure portal. For more information, see [View AKS costs in Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Cost definitions

In the Kubernetes namespaces and assets views, you might see any of the following charges:

**Idle charges**represent the cost of available resource capacity that isn't used by any workloads.**Service charges**represent the charges associated with the service, like Uptime SLA, Microsoft Defender for Containers, etc.**System charges**represent the cost of capacity reserved by AKS on each node to run system processes required by the cluster, including the kubelet and container runtime.[Learn more](concepts-clusters-workloads#resource-reservations).**Unallocated charges**represent the cost of resources that couldn't be allocated to namespaces.

Note

It might take *up to one day* for data to finalize. After 24 hours, any fluctuations in costs for the previous day will have stabilized.

## Troubleshooting

If you're experiencing issues, such as the `cost-agent`

pod getting `OOMKilled`

or stuck in a `Pending`

state, see [Troubleshoot AKS cost analysis add-on issues](/en-us/troubleshoot/azure/azure-kubernetes/aks-cost-analysis-add-on-issues).

## Next steps

For more information on cost in AKS, see [Understand Azure Kubernetes Service (AKS) usage and costs](understand-aks-costs).
