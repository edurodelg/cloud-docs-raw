---
merged_at: 2026-01-25T12:25:33.926281
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: active-active-solution.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/active-active-solution -->

# Recommended active-active high availability solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. In the event of a disaster that causes the region to become unavailable, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

While there are multiple patterns that can provide recoverability for an AKS solution, this guide outlines the recommended active-active high availability solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with both clusters actively serving traffic.

Note

The following use case can be considered standard practice within AKS. It has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-active high availability solution overview

This solution relies on two identical AKS clusters configured to actively serve traffic. You place a global traffic manager, such as [Azure Front Door](/en-us/azure/frontdoor/front-door-overview), in front of the two clusters to distribute traffic across them. You must consistently configure the clusters to host an instance of all applications required for the solution to function.

Availability zones are another way to ensure high availability and fault tolerance for your AKS cluster within the same region. Availability zones allow you to distribute your cluster nodes across multiple isolated locations within an Azure region. This way, if one zone goes down due to a power outage, hardware failure, or network issue, your cluster can continue to run and serve your applications. Availability zones also improve the performance and scalability of your cluster by reducing the latency and contention among nodes. To set up availability zones for your AKS cluster, you need to specify the zone numbers when creating or updating your node pools. For more information, see [What are Azure availability zones?](/en-us/azure/reliability/availability-zones-overview)

Note

Many regions support availability zones. Consider using regions with availability zones to provide more resiliency and availability for your workloads. For more information, see [Recover from a region-wide service disruption](/en-us/azure/architecture/resiliency/recovery-loss-azure-region).

## Scenarios and configurations

This solution is best implemented when hosting stateless applications and/or with other technologies also deployed across both regions, such as horizontal scaling. In scenarios where the hosted application is reliant on resources, such as databases, that are actively in only one region, we recommend instead implementing an [active-passive solution](active-passive-solution) for potential cost savings, as active-passive has more downtime than active-active.

## Components

The active-active high availability solution uses many Azure services. This section covers only the components unique to this multi-cluster architecture. For more information on the remaining components, see the [AKS baseline architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=%2Fazure%2Faks%2Ftoc.json&bc=%2Fazure%2Faks%2Fbreadcrumb%2Ftoc.json).

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, your Azure Front Door configuration routes network traffic between all regions. If one region becomes unavailable, traffic routes to a region with the fastest load time for the user.

**Hub-spoke network per region**: A regional hub-spoke network pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall policies across all regions.

**Regional key store**: You provision [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store sensitive values and keys specific to the AKS instance and to support services found in that region.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to a regional [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance, which sits in front of each AKS cluster. Azure Front Door allows for *layer seven* global routing.

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


---

<!-- DOCUMENTO FUSIONADO: access-private-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/access-private-cluster -->

# Access a private Azure Kubernetes Service (AKS) cluster using the command invoke or Run command feature

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you access a private Azure Kubernetes Service (AKS) cluster, you need to connect to the cluster from the cluster virtual network (VNet), a peered network, or a configured private endpoint. These approaches require extra configuration, such as setting up a VPN or Express Route.

With the Azure CLI, you can use `command invoke`

to access private clusters without the need to configure a VPN or Express Route. `command invoke`

allows you to remotely invoke commands, like `kubectl`

and `helm`

, on your private cluster through the Azure API without directly connecting to the cluster. The RBAC actions `Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

control the permissions for using `command invoke`

.

With the Azure portal, you can use the `Run command`

feature to run commands on your private cluster. The `Run command`

feature uses the same `command invoke`

functionality to run commands on your cluster. The pod created by `Run command`

provides `kubectl`

and `helm`

for operating your cluster. `jq`

, `xargs`

, `grep`

, and `awk`

are available for Bash support.

Tip

You can use Azure Copilot to run `kubectl`

commands in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#run-cluster-commands).

## Prerequisites

**System and permission requirements**

| Requirement type | Specification | How to verify |
|---|---|---|
Azure CLI version |
2.24.0 or later | Use the
`az --version` |

**Private AKS cluster**[Create a private AKS cluster](private-clusters).**RBAC actions**`Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

[Azure CLI command.](/en-us/cli/azure/role/assignment#az-role-assignment-list)`az role assignment list`

**Run command pod resource specifications**

| Resource type | Value | Impact |
|---|---|---|
CPU requests |
200m | Minimum CPU reserved for command pod |
Memory requests |
500Mi | Minimum memory reserved for command pod |
CPU limits |
500m | Maximum CPU available to command pod |
Memory limits |
1Gi | Maximum memory available to command pod |
Azure Resource Manager (ARM) API timeout |
60 seconds | Maximum time for pod scheduling |
Output size limit |
512kB | Maximum command output size |

## Limitations and considerations

**Design scope**

**Not for programmatic access**: Use Bastion, VPN, or ExpressRoute for automated API calls.**Pod scheduling dependency**: Requires sufficient cluster resources (see the[resource specifications](#prerequisites)).**Output limitations**:*exitCode*and*text*only, no API-level details.**Network constraints apply**: Subject to cluster networking and security restrictions.

**Potential failure points**

- Pod scheduling failure if nodes are resource-constrained.
- ARM API timeout (60 seconds) if pod can't be scheduled quickly.
- Output truncation if response exceeds 512kB limit.

## Use `command invoke`

on a private AKS cluster with the Azure CLI

Set environment variables for your resource group and cluster name to use in subsequent commands.

`export AKS_RESOURCE_GROUP="<resource-group-name>" export AKS_CLUSTER_NAME="<cluster-name>"`

These environment variables allow you to run AKS commands without having to rewrite their names.


### Use `command invoke`

to run a single command

Run a single command on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the command to run. The following example gets the pods in the`kube-system`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl get pods -n kube-system"`


### Use `command invoke`

to run multiple commands

Run multiple commands on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the commands to run. The following example adds the Bitnami Helm chart repository, updates the repository, and installs the`nginx`

chart.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "helm repo add bitnami https://charts.bitnami.com/bitnami && helm repo update && helm install my-release bitnami/nginx"`


### Use `command invoke`

to run commands with an attached file

If you want to run a command with an attached file, the file must exist and be accessible in your current working directory. In the following example, we create a minimal deployment file for demonstration.

Create a Kubernetes manifest file named

`deployment.yaml`

. The following example deployment file deploys an`nginx`

pod.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF`

Apply the deployment file to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

file to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -n default" \ --file deployment.yaml`


### Use `command invoke`

to run commands with all files in the current directory

Note

Use only small, necessary files to avoid exceeding system size limits.

In the following example, we create two minimal deployment files for demonstration.

Create two Kubernetes manifest files named

`deployment.yaml`

and`configmap.yaml`

. The following example deployment files deploy an`nginx`

pod and create a ConfigMap with a welcome message.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF cat <<EOF > configmap.yaml apiVersion: v1 kind: ConfigMap metadata: name: nginx-config data: welcome-message: "Hello from configmap" EOF`

Apply the deployment files to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

and`configmap.yaml`

files to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -f configmap.yaml -n default" \ --file deployment.yaml \ --file configmap.yaml`


## Use `Run command`

on a private AKS cluster in the Azure portal

You can use the following `kubectl`

commands with the `Run command`

feature:

`kubectl get nodes`

`kubectl get deployments`

`kubectl get pods`

`kubectl describe nodes`

`kubectl describe pod <pod-name>`

`kubectl describe deployment <deployment-name>`

`kubectl apply -f <file-name>`


### Use `Run command`

to run a single command

- In the Azure portal, navigate to your private cluster.
- From the service menu, under
**Kubernetes resources**, select**Run command**. - Enter the command you want to run and select
**Run**.

### Use `Run command`

to run commands with attached files

In the Azure portal, navigate to your private cluster.

From the service menu, under

**Kubernetes resources**, select**Run command**.Select

**Attach files**>**Browse for files**.Select the file or files you want to attach, and then select

**Attach**.Enter the command you want to run and select

**Run**.

## Disable `Run command`


You can disable the `Run command`

feature by setting [ .properties.apiServerAccessProfile.disableRunCommand to true](/en-us/rest/api/aks/managed-clusters/create-or-update).


## Troubleshoot `command invoke`

issues

For information on the most common issues with `az aks command invoke`

and how to fix them, see [Resolve az aks command invoke failures](/en-us/troubleshoot/azure/azure-kubernetes/resolve-az-aks-command-invoke-failures).

## Related content

In this article, you learned how to access a private cluster and run commands on that cluster. For more information on AKS clusters, see the following articles:
