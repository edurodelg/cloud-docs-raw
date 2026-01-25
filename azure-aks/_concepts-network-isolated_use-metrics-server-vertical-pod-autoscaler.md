---
merged_at: 2026-01-25T12:25:33.951746
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-network-isolated.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-isolated -->

# Network isolated Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable.

## How a network isolated cluster works

The following diagram shows the network communication between dependencies for a network isolated cluster.


AKS clusters fetch artifacts required for the cluster and its features or add-ons from the Microsoft Artifact Registry (MAR). This image pull allows AKS to provide newer versions of the cluster components and to also address critical security vulnerabilities. A network isolated cluster attempts to pull those images and binaries from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint.

The following two options are supported for a private ACR associated with network isolated clusters:

**AKS-managed ACR**- AKS creates, manages, and reconciles an ACR resource in this option. There's nothing you need to do.Note

The AKS-managed ACR resource is created in your subscription. If you delete the cluster with AKS-managed ACR for bootstrap artifact source. Related resources such as the AKS-managed ACR, private link, and private endpoint are also automatically deleted. If you change outbound type on a cluster to any type other than

`none`

or`block`

with`--bootstrap-artifact-source`

retained as`Cache`

. Then the related resources are not deleted.**Bring your own (BYO) ACR**- The BYO ACR option requires creating an ACR with a private link between the ACR resource and the AKS cluster. See[Connect privately to an Azure container registry using Azure Private Link](/en-us/azure/container-registry/container-registry-private-link)to understand how to configure a private endpoint for your registry. You also need to assign permissions and manage the cache rules, private link, and private endpoint used in the cluster.Note

When you delete the AKS cluster or after you disable the feature. The BYO ACR, private link, and private endpoint aren't deleted automatically. If you add customized images and cache rules to the BYO ACR, they persist after cluster reconciliation.


To create a network isolated cluster, you need to first ensure network traffic between your API server and your node pools remains only on the private network, you can choose one of the following private cluster modes:

[Private link-based cluster](private-clusters)- The control plane or API server is in an AKS-managed Azure resource group, and your node pool is in your resource group. The server and the node pool can communicate with each other through the Azure Private Link service in the API server virtual network and a private endpoint which is exposed on the subnet of your AKS cluster.[API Server VNet Integration configured cluster](api-server-vnet-integration)- A cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the virtual network where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel.

You also need to ensure the egress path for your AKS cluster are controlled and limited, you can choose one of the following network outbound types:

[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-none)- If`none`

`none`

is set. AKS doesn't automatically configure egress paths and a default route is not required. It is supported in both bring-your-own (BYO) virtual network scenarios and managed virtual network scenarios. For bring your own virtual network scenario, you must establish explicit egress paths if needed.[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-block-preview)-If`block`

(preview)`block`

is set. AKS configures network rules to actively block all egress traffic from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted. It is supported in managed virtual network scenario. You can also achieve similar effect by blocking all egress traffic by adding[network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview)rules with`none`

in bring-your-own virtual network scenario.

Note

Outbound type of `none`

is generally available.
Outbound type `block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Limitations

`Unmanaged`

channel is not supported.- Windows node pools are not yet supported.
- kubenet networking is not supported.

Caution

If you are using [Node Public IP](use-node-public-ips) in network isolated AKS clusters, it will allow outbound traffic with outbound type `none`

.

## Using features, add-ons, and extensions requiring egress

For network isolated clusters with BYO ACR:

- If you want to use any AKS feature or add-on that requires outbound network access in network isolated clusters with outbound type
`none`

,[this document](outbound-rules-control-egress)contains the outbound network requirements for each feature. Also, this doc enumerates the features or add-ons that support private link integration for secure connection from within the cluster's virtual network. It is recommended to set up private endpoints to access these features. For example, you can set up[private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link)to use Managed Prometheus (Azure Monitor workspace) and Container insights (Log Analytics workspace) in network isolated clusters. If a private link integration is not available for any of these features. Then you can set up the cluster with a[user-defined routing table and an Azure Firewall](limit-egress-traffic)based on the network rules and application rules that required for that feature. - If you are using
[Azure Container Storage Interface (CSI) driver](azure-files-csi)for Azure Files and Blob storage, you must create a custom storage class with "networkEndpointType: privateEndpoint", see examples in[Azure Files storage classes](/en-us/azure/aks/azure-csi-files-storage-provision#dynamically-provision-a-volume)and[Azure Blob storage classes](/en-us/azure/aks/azure-csi-blob-storage-provision?tabs=mount-nfs%2Csecret#storage-class-parameters-for-dynamic-persistent-volumes). - The following AKS cluster extensions aren't supported yet on network isolated clusters:

## Frequently asked questions

### What's the difference between network isolated cluster and Azure Firewall?

A network isolated cluster doesn't require any egress traffic beyond the VNet throughout the cluster bootstrapping process. A network isolated cluster has outbound type as either `none`

or `block`

. If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic that's based on the destination. It gives you fine-grained control of egress traffic, but at the same time allows you to provide access to the FQDNs encompassing an AKS cluster’s outbound dependencies. This is something that NSGs can't do. For example, you can set outbound type of the cluster to `userDefinedRouting`

to force outbound traffic through the firewall and then configure FQDN restrictions on outbound traffic. There are many cases where you still want a firewall. Such as you have outbound traffic anyway from your application or you want to control, inspect, and secure the cluster traffic both egress and ingress.

In summary, while Azure Firewall can be used to define egress restrictions on clusters with outbound requests, network isolated clusters go further on secure-by-default posture by eliminating or blocking the outbound requests altogether.

### Do I need to set up any allowlist endpoints for the network isolated cluster to work?

The cluster creation and bootstrapping stages don't require any outbound traffic from the network isolated cluster. Images required for AKS components and addons are pulled from the private ACR connected to the cluster instead of pulling from Microsoft Artifact Registry (MAR) over public endpoints.

After setting up a network isolated cluster. If you want to enable features or add-ons that need to make outbound requests to their service endpoints, you can set up private endpoints to the services powered by Azure Private Link.

### Can I manually upgrade packages to upgrade node pool image?

Manually upgrading packages based on egress to package repositories is not recommended. Instead, you can [manually upgrade](node-image-upgrade) or [autoupgrade your node OS images](auto-upgrade-node-os-image). Only `NodeImage`

and `None`

upgrade channels are currently supported for network isolated clusters.

### What if I change the outbound type other than `none`

or `block`

, does that still make a network isolated cluster?

The only supported outbound types for a network isolated cluster are outbound type `none`

and `block`

. If you use any other outbound type, the cluster may still pull artifacts from the private ACR associated, however that may generate egress traffic.


---

<!-- DOCUMENTO FUSIONADO: use-metrics-server-vertical-pod-autoscaler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-metrics-server-vertical-pod-autoscaler -->

# Configure Metrics Server VPA in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Metrics Server](https://kubernetes-sigs.github.io/metrics-server/) is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. With Azure Kubernetes Service (AKS), vertical pod autoscaling is enabled for the Metrics Server. The Metrics Server is commonly used by other Kubernetes add-ons, like the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler).

Vertical Pod Autoscaler (VPA) enables you to adjust the resource limit when the Metrics Server is experiencing consistent CPU and memory resource constraints.

## Prerequisites

- An AKS cluster with Kubernetes version 1.24 or higher.
- The Kubernetes command-line tool
`kubectl`

installed on your computer or use Azure Cloud Shell to run`kubectl`

commands.

## Get credentials

To run the `kubectl`

commands, you need your AKS credentials merged into your profile's `.kube/config`

file. Replace `<resourceGroupName>`

and `<clusterName>`

with your cluster's values.

```
az aks get-credentials --resource-group <resourceGroupName> --name <clusterName>
```


## Metrics server throttling

If the Metrics Server throttling rate is high, and the memory usage of its two pods is unbalanced, it's an indication that the Metrics Server needs more resources than the default values.

To update the coefficient values, create a `ConfigMap`

in the overlay `kube-system`

namespace to override the values in the Metrics Server specification. Perform the following steps to update the metrics server.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy the manifest code into the file.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 1m baseMemory: 100Mi memoryPerNode: 8Mi`

In the

`ConfigMap`

example, the resource limit and request are changed to the following values where`n`

is the number of nodes:- cpu: (100+1n) millicores
- memory: (100+8n) mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:08:34.930865 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:08:34.931128 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:08:34.931200 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:08:34.931249 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:08:34.932085 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 1m, memory: 100Mi, extra_memory: 8Mi I0811 19:08:34.932177 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:1 scale:-3} d:{Dec:<nil>} s:1m Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:8388608 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


Be cautious of the `baseCPU`

, `cpuPerNode`

, `baseMemory`

, and the `memoryPerNode`

, because AKS doesn't validate the `ConfigMap`

. As a recommended practice, increase the value gradually to avoid unnecessary resource consumption. Proactively monitor resource usage when updating or creating the `ConfigMap`

. A large number of resource requests could negatively affect the node.

## Manually configure Metrics Server resource usage

The Metrics Server VPA adjusts resource usage by the number of nodes. If the cluster scales up or down often, the Metrics Server might restart frequently. In this case, you can bypass VPA and manually control its resource usage. This method to configure VPA isn't to be performed in addition to the steps described in the previous section.

If you would like to bypass VPA for Metrics Server and manually control its resource usage, perform the following steps.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy in the following manifest.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 0m baseMemory: 100Mi memoryPerNode: 0Mi`

In this

`ConfigMap`

example, the resource limit and request are changed to the following values that don't trigger autoscaling:- cpu: 100 millicores
- memory: 100 mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:19:06.235018 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:19:06.235105 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:19:06.235136 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:19:06.235171 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:19:06.235899 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 0m, memory: 100Mi, extra_memory: 0Mi I0811 19:19:06.235917 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:0 scale:-3} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:0 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


## Troubleshooting

### ConfigMap error

If you apply the following `ConfigMap`

, the Metrics Server VPA customizations aren't applied. You need add a unit for `baseCPU`

like `baseCPU: 100m`

that includes the `m`

unit.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: metrics-server-config
namespace: kube-system
labels:
kubernetes.io/cluster-service: "true"
addonmanager.kubernetes.io/mode: EnsureExists
data:
NannyConfiguration: |-
apiVersion: nannyconfig/v1alpha1
kind: NannyConfiguration
baseCPU: 100
cpuPerNode: 1m
baseMemory: 100Mi
memoryPerNode: 8Mi
```


The following example output resembles the results showing the updated throttling settings aren't applied.

```
I0811 19:25:33.992691 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server]
I0811 19:25:33.992890 1 pod_nanny.go:87] Version: 1.8.23
I0811 19:25:33.992918 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server.
I0811 19:25:33.992937 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi
I0811 19:25:33.993586 1 pod_nanny.go:217] Unable to decode Nanny Configuration from config map, using default parameters
I0811 19:25:33.993602 1 pod_nanny.go:144] cpu: 150m, extra_cpu: 0.5m, memory: 100Mi, extra_memory: 4Mi
I0811 19:25:33.993610 1 pod_nanny.go:278] Resources: [{Base:{i:{value:150 scale:-3} d:{Dec:<nil>} s:150m Format:DecimalSI} ExtraPerResource:{i:{value:5 scale:-4} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:4194304 scale:0} d:{Dec:<nil>} s:4Mi Format:BinarySI} Name:memory}]
```


### PodDisruptionBudget

For Kubernetes version 1.23 and higher clusters, Metrics Server has a `PodDisruptionBudget`

. It ensures the number of available Metrics Server pods is at least one. If you get something like this after running `kubectl get pods --namespace kube-system`

, it's possible that the customized resource usage is small. Increase the coefficient values to resolve it.

```
metrics-server-1a2b333c44-wxyz5 1/2 CrashLoopBackOff 6 (36s ago) 6m33s
metrics-server-1a2b333c44-abcd6 1/2 CrashLoopBackOff 6 (54s ago) 6m33s
metrics-server-5d69966543-hcrff 2/2 Running 0 37m
```


## Next steps

Metrics Server is a component in the core metrics pipeline. For more information, see [Metrics Server API design](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/).
