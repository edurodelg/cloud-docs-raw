---
merged_at: 2026-01-25T12:25:33.940434
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-network-observability-metrics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.


---

<!-- DOCUMENTO FUSIONADO: rdp.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/rdp -->

# Connect with RDP to Azure Kubernetes Service (AKS) cluster Windows Server nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you may need to access an AKS Windows Server node. This access could be for maintenance, log collection, or other troubleshooting operations. You can access the AKS Windows Server nodes using RDP. For security purposes, the AKS nodes aren't exposed to the internet.

Alternatively, if you want to SSH to your AKS Windows Server nodes, you need access to the same key-pair that was used during cluster creation. Follow the steps in [SSH into Azure Kubernetes Service (AKS) cluster nodes](ssh).

This article shows you how to create an RDP connection with an AKS node using their private IP addresses.

## Before you begin

This article assumes that you have an existing AKS cluster with a Windows Server node. If you need an AKS cluster, see the article on [creating an AKS cluster with a Windows container using the Azure CLI](learn/quick-windows-container-deploy-cli). You need the Windows administrator username and password for the Windows Server node you want to troubleshoot. You also need an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

If you need to reset the password, use `az aks update`

to change the password.

```
az aks update --resource-group myResourceGroup --name myAKSCluster --windows-admin-password $WINDOWS_ADMIN_PASSWORD
```


If you need to reset the username and password, see [Reset Remote Desktop Services or its administrator password in a Windows VM](/en-us/troubleshoot/azure/virtual-machines/reset-rdp).

You also need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Deploy a virtual machine to the same subnet as your cluster

The Windows Server nodes of your AKS cluster don't have externally accessible IP addresses. To make an RDP connection, you can deploy a virtual machine with a publicly accessible IP address to the same subnet as your Windows Server nodes.

The following example creates a virtual machine named *myVM* in the *myResourceGroup* resource group.

You need to get the subnet ID used by your Windows Server node pool and query for:

- The cluster's node resource group
- The virtual network
- The subnet's name
- The subnet ID

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
VNET_NAME=$(az network vnet list --resource-group $CLUSTER_RG --query [0].name -o tsv)
SUBNET_NAME=$(az network vnet subnet list --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --query [0].name -o tsv)
SUBNET_ID=$(az network vnet subnet show --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --name $SUBNET_NAME --query id -o tsv)
```


Now that you've the SUBNET_ID, run the following command in the same Azure Cloud Shell window to create the VM:

```
PUBLIC_IP_ADDRESS="myVMPublicIP"
az vm create \
--resource-group myResourceGroup \
--name myVM \
--image win2019datacenter \
--admin-username azureuser \
--admin-password {admin-password} \
--subnet $SUBNET_ID \
--nic-delete-option delete \
--os-disk-delete-option delete \
--nsg "" \
--public-ip-address $PUBLIC_IP_ADDRESS \
--query publicIpAddress -o tsv
```


The following example output shows the VM has been successfully created and displays the public IP address of the virtual machine.

```
13.62.204.18
```


Record the public IP address of the virtual machine. You'll use this address in a later step.

## Allow access to the virtual machine

AKS node pool subnets are protected with NSGs (Network Security Groups) by default. To get access to the virtual machine, you'll have to enabled access in the NSG.

Note

The NSGs are controlled by the AKS service. Any change you make to the NSG will be overwritten at any time by the control plane.

First, get the resource group and name of the NSG to add the rule to:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
```


Then, create the NSG rule:

```
az network nsg rule create \
--name tempRDPAccess \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--priority 100 \
--destination-port-range 3389 \
--protocol Tcp \
--description "Temporary RDP access to Windows nodes"
```


## Get the node address

To manage a Kubernetes cluster, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. If you use Azure Cloud Shell, `kubectl`

is already installed. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command:

```
az aks install-cli
```


To configure `kubectl`

to connect to your Kubernetes cluster, use the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


List the internal IP address of the Windows Server nodes using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command:

```
kubectl get nodes -o wide
```


The following example output shows the internal IP addresses of all the nodes in the cluster, including the Windows Server nodes.

```
$ kubectl get nodes -o wide
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-42485177-vmss000000 Ready agent 18h v1.12.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1040-azure docker://3.0.4
aksnpwin000000 Ready agent 13h v1.12.7 10.240.0.67 <none> Windows Server Datacenter 10.0.17763.437
```


Record the internal IP address of the Windows Server node you wish to troubleshoot. You'll use this address in a later step.

## Connect to the virtual machine and node

Connect to the public IP address of the virtual machine you created earlier using an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

After you have connected to your virtual machine, connect to the *internal IP address* of the Windows Server node you want to troubleshoot using an RDP client from within your virtual machine.

You're now connected to your Windows Server node.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

## Remove RDP access

When done, exit the RDP connection to the Windows Server node then exit the RDP session to the virtual machine. After you exit both RDP sessions, delete the virtual machine with the [az vm delete](/en-us/cli/azure/vm#az-vm-delete) command:

```
# Delete the virtual machine
az vm delete \
--resource-group myResourceGroup \
--name myVM
```


Delete the public IP associated with the virtual machine:

```
az network public-ip delete \
--resource-group myResourceGroup \
--name $PUBLIC_IP_ADDRESS
```


Delete the NSG rule:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
az network nsg rule delete \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--name tempRDPAccess
```


## Connect with Azure Bastion

Alternatively, you can use [Azure Bastion](/en-us/azure/bastion/bastion-overview) to connect to your Windows Server node.

### Deploy Azure Bastion

To deploy Azure Bastion, you'll need to find the virtual network your AKS cluster is connected to.

- In the Azure portal, go to
**Virtual networks**. Select the virtual network your AKS cluster is connected to. - Under
**Settings**, select**Bastion**, then select**Deploy Bastion**. Wait until the process is finished before going to the next step.

### Connect to your Windows Server nodes using Azure Bastion

Go to the node resource group of the AKS cluster. Run the command below in the Azure Cloud Shell to get the name of your node resource group:

```
az aks show --name myAKSCluster --resource-group myResourceGroup --query 'nodeResourceGroup' -o tsv
```


- Select
**Overview**, and select your Windows node pool virtual machine scale set. - Under
**Settings**, select**Instances**. Select a Windows server node that you'd like to connect to. - Under
**Support + troubleshooting**, select**Bastion**. - Enter the credentials you set up when the AKS cluster was created. Select
**Connect**.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

Note

If you close out of the terminal window, press **CTRL + ALT + End**, select **Task Manager**, select **More details**, select **File**, select **Run new task**, and enter **cmd.exe** to open another terminal. You can also logout and re-connect with Bastion.

### Remove Bastion access

When you're finished, exit the Bastion session and remove the Bastion resource.

- In the Azure portal, go to
**Bastion**and select the Bastion resource you created. - At the top of the page, select
**Delete**. Wait until the process is complete before proceeding to the next step. - In the Azure portal, go to
**Virtual networks**. Select the virtual network that your AKS cluster is connected to. - Under
**Settings**, select**Subnet**, and delete the**AzureBastionSubnet**subnet that was created for the Bastion resource.

## Next steps

If you need more troubleshooting data, you can [view the Kubernetes primary node logs](monitor-aks#aks-control-plane-resource-logs) or [Azure Monitor](/en-us/azure/azure-monitor/containers/container-insights-overview).
