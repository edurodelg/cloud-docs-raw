---
merged_at: 2026-01-25T15:16:21.149376
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __how-to-configure-container-network-metrics-filtering_container-network-observa_ee505d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _how-to-configure-container-network-metrics-filtering_container-network-observab_d8572c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: how-to-configure-container-network-metrics-filtering.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-metrics-filtering -->

# Configure container network metrics filtering for Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure container network metrics filtering for Azure Kubernetes Service (AKS) with Cilium to optimize data collection, reduce storage costs, and focus on the metrics most relevant to your monitoring needs.

Configure container network metrics filtering enables dynamic management of Hubble metrics cardinality through Kubernetes Custom Resource Definitions (CRDs). This feature allows you to dynamically control the cardinality, dimensions, and targets of Hubble metrics without restarting Cilium agents or Prometheus servers.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is

**2.73.0**. To find your version, run`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).An AKS cluster with Cilium data plane and

[Advanced Container Networking Services](advanced-container-networking-services-overview)enabled.Kubernetes version 1.32 or later.

Container network metrics filtering works specifically with Cilium data planes.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`18.0.0b2`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az_extension_add) or

[command.](/en-us/cli/azure/extension#az_extension_update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingDynamicMetricsPreview feature flag

- First, register the AdvancedNetworkingDynamicMetricsPreview feature flag by using the
command:`az feature register`


```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- Verify successful registration by using the
command. It takes a few minutes for registration to complete.`az feature show`


```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- When the feature shows
**Registered**, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand.`az provider register`


```
az provider register --namespace Microsoft.ContainerService
```


### Create a new AKS cluster with Cilium

If you already have an existing cluster, you can skip this step.

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set environment variables
export RESOURCE_GROUP="cnm-testing-rg"
export CLUSTER_NAME="cnm-cilium-cluster"
export LOCATION="eastus2euap" # Use canary region for preview features
# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create AKS cluster with Cilium and ACNS enabled
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--location $LOCATION \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--enable-managed-identity \
--generate-ssh-keys \
--kubernetes-version 1.32
```


### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az_aks_get_credentials) command:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --overwrite-existing
```


## Configure custom resources for metrics filtering

Container network metrics filtering uses the `ContainerNetworkMetric`

Custom Resource Definition (CRD) to define filtering rules. Only one CRD can exist per cluster, and changes take approximately 30 seconds to reconcile. If the CRD is not applied, all metrics will be collected.

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: : container-network-metric # Cluster scoped
spec:
filters:
- metric: flow
includeFilters: # List of include filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
metric: dns
excludeFilters: # List of exclude filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`filters.metric` |
String | Name of the metric you would like to apply the filter on. This is mandatory. The supported values are `dns` , `flow` , `tcp` , `drop` |
Mandatory |
`includeFilters` or `excludeFilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. You must have at least one include or exclude filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . Because it's an optional parameter, if it isn't specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . Because it's an optional parameter, if it isn't specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the `ContainerNetworkMetric`

custom resource to enable log collection at the cluster:

```
kubectl apply -f <crd.yaml>
```


## Clean up and reset

To clean up filtering configuration:

```
# Delete the CRD
kubectl delete ContainerNetworkMetric container-network-metric
```


## Example filtering configuration

- Create a basic filtering configuration that focuses on DNS metrics:

```
# basic-dns-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns # Supported: dns, flow, tcp, drop
excludeFilters:
- from:
namespacedPod: ["kube-system/coredns"]
```


- Configure filtering for TCP metrics with include and exclude filters:

```
# tcp-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: tcp
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
excludeFilters:
- to:
namespacedPod: ["kube-system/metrics-server"]
```


- Configure filtering for network flow metrics:

```
# flow-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: flow
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
- to:
labelSelector:
matchLabels:
tier: "backend"
excludeFilters:
- from:
namespacedPod: ["default/test"]
```


- Configure filtering for dropped packet metrics:

```
# drop-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: drop
excludeFilters:
- from:
namespacedPod: ["kube-system/"]
```


- Configure filtering for multiple metric types in a single CRD:

```
# multi-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns
includeFilters:
- protocol: ["dns"]
excludeFilters:
- from:
namespacedPod: ["kube-system/*"]
- metric: tcp
includeFilters:
- protocol: ["tcp"]
- from:
labelSelector:
matchLabels:
environment: "production"
- metric: flow
excludeFilters:
- from:
namespacedPod: ["default/debug-*"]
- metric: drop
includeFilters:
- reason: ["Policy denied", "Invalid"]
```


## Best practices

Ensure you do not have conflicting include and exclude filter on the CRD.

Leverage Kubernetes label selectors for flexible filtering.

Always validate filtering configurations in development or staging

Regularly review filtered metrics to ensure important data isn't lost.

Remember that only one CRD can exist per cluster.


## Troubleshooting

### Common issues

**Issue**: CRD configuration not applied

**Solution**: Check that the feature flag is registered and only one CRD exists:

```
# Verify feature registration
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
# Check existing CRDs
kubectl get ContainerNetworkMetric
```


**Issue**: Metrics still showing after applying excludeFilters

**Solution**: Remember that preexisting metrics persist in Prometheus. You may need to wait for new metrics to be generated to see the filtering effects.

## Limitations

- This feature is specifically designed for Cilium data planes only
- Only one
`ContainerNetworkMetric`

CRD can exist per cluster - Preexisting metrics persist in Prometheus; new filtering rules apply to newly generated metrics
- Requires Kubernetes version 1.32 or later

## Related content

- To learn about container network metrics capabilities, see
[Container network metrics overview](container-network-observability-metrics). - To create an AKS cluster with Advanced Container Networking Services, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview).


---

<!-- DOCUMENTO FUSIONADO: container-network-observability-how-to.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-how-to -->

# Set up Container Network Observability for Azure Kubernetes Service (AKS) - Azure managed Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Container Network Observability for Azure Kubernetes Service (AKS) using Managed Prometheus and Grafana and BYO Prometheus and Grafana and to visualize the scraped metrics

You can use Container Network Observability to collect data about the network traffic of your AKS clusters. It enables a centralized platform for monitoring application and network health. Currently, metrics are stored in Prometheus and Grafana can be used to visualize them. Container Network Observability also offers the ability to enable Hubble. These capabilities are supported for both Cilium and non-Cilium clusters.

Container Network Observability is one of the features of Advanced Container Networking Services. For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see [What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

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

<!-- DOCUMENTO FUSIONADO: open-service-mesh-istio-migration-guidance.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-istio-migration-guidance -->

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

<!-- DOCUMENTO FUSIONADO: ___use-flyte_automated-deployments_stateful-workload-upgrades__container-network_39475b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __use-flyte_automated-deployments_stateful-workload-upgrades.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _use-flyte_automated-deployments.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-flyte.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-flyte -->

# Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Flyte on Azure Kubernetes Service (AKS). Flyte is an open-source workflow orchestrator that unifies machine learning, data engineering, and data analytics stacks to help you build robust and reliable applications. When using Flyte as a Kubernetes-native workflow automation tool, you can focus on experimentation and providing business value without increasing your scope to infrastructure and resource management. Keep in mind that Flyte isn't officially supported by Microsoft, so use it at your own discretion.

For more information, see [Introduction to Flyte](https://www.union.ai/docs/flyte/user-guide/).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Flyte use cases

Flyte can be used for a variety of use cases, including:

- Deliver models for streamlined profit and loss financial calculations.
- Process petabytes of data to efficiently conduct 3D mapping of new areas.
- Quickly rollback to previous versions and minimize impact of bugs in your pipelines.

For more information, see [Flyte tutorials](https://www.union.ai/docs/flyte/tutorials/).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free).- If you have multiple subscriptions, make sure you select the correct one using the
`az account set --subscription <subscription-id>`

command.

- If you have multiple subscriptions, make sure you select the correct one using the
- The Azure CLI installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The Helm CLI installed and updated. Check your version using the
`helm version`

command. If you need to install or upgrade, see[Install Helm](https://helm.sh/docs/intro/install/). - The
`kubectl`

CLI installed and updated. Install it locally using the`az aks install-cli`

command or using[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - A local Docker development environment. For more information, see
[Get Docker](https://docs.docker.com/get-docker/). `flytekit`

and`flytectl`

installed. For more information, see[Flyte installation](https://www.union.ai/docs/flyte/user-guide/getting-started/local-setup/).

Note

If you're using the Azure Cloud Shell, the Azure CLI, Helm, and kubectl are already installed.

### Set environment variables

Set environment variables for use throughout the article. Replace the placeholder values with your own values.

`export RESOURCE_GROUP="<resource-group-name>" export LOCATION="<location>" export CLUSTER_NAME="<cluster-name>" export DNS_NAME_PREFIX="<dns-name-prefix>"`


## Create an AKS cluster

Create an Azure resource group for the AKS cluster using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command with the`az aks create`

`--enable-azure-rbac`

,`--enable-managed-identity`

,`--enable-aad`

, and`--dns-name-prefix`

parameters.`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac --enable-managed-identity --enable-aad --dns-name-prefix $DNS_NAME_PREFIX --generate-ssh-keys`


## Connect to your AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Add the Flyte Helm repository

Add the Flyte Helm repository using the

`helm repo add`

command.`helm repo add flyteorg https://flyteorg.github.io/flyte`


## Find Flyte Helm charts

Search for Flyte Helm charts using the

`helm search repo`

command.`helm search repo flyteorg`

The following example output shows some of the available Flyte Helm charts:

`NAME CHART VERSION APP VERSION DESCRIPTION flyteorg/flyte v1.12.0 A Helm chart for Flyte Sandbox flyteorg/flyte-binary v1.12.0 1.16.0 Chart for basic single Flyte executable deployment flyteorg/flyte-core v1.12.0 A Helm chart for Flyte core flyteorg/flyte-deps v1.12.0 A Helm chart for Flyte dependencies flyteorg/flyte-sandbox 0.1.0 1.16.1 A Helm chart for the Flyte local sandbox flyteorg/flyteagent v0.1.10 A Helm chart for Flyte Agent`

Update the repository using the

`helm repo update`

command.`helm repo update`


## Deploy a Flyte chart on AKS

In this section, you deploy the flyte-binary Helm chart so you can begin building and deploying data and machine learning pipelines with Flyte on AKS. The flyte-binary chart is a basic single Flyte executable deployment.

Create a namespace for your Flyte deployment using the

`kubectl create namespace`

command.`kubectl create namespace <namespace-name>`

Install a Flyte Helm chart using the

`helm install`

command. In this example, we use the`flyte-binary`

chart.`helm install flyte-binary flyteorg/flyte-core --namespace <namespace-name>`

Verify that the Flyte deployment is running using the

`kubectl get services`

command.`kubectl get services --namespace <namespace-name> --output wide`

The following condensed example output shows the Flyte deployment:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE flyteorg-flyte-binary-grpc ClusterIP xx.x.xx.xxx <none> 81/TCP 1m flyteorg-flyte-binary-http ClusterIP xx.x.xx.xxx <none> 80/TCP 1m flyteorg-flyte-binary-webhook ClusterIP xx.x.xx.xxx <none> 80/TCP 1m`


## Next steps

In this article, you learned how to install Flyte on AKS using a Helm chart.
The Flyte project also maintains a [reference implementation for AKS](https://github.com/unionai-oss/deploy-flyte/tree/main/environments/azure/flyte-core#readme) that automatically configures all the dependencies and deploys a production grade Flyte cluster.

To start building and deploying data and machine learning pipelines, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: automated-deployments.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/automated-deployments -->

# Automated deployments for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Automated Deployments streamline the process of setting up a GitHub Action or Azure DevOps Pipeline, making it easy to create a continuous deployment pipeline for your application to Azure Kubernetes Service (AKS). Once connected, every new commit automatically triggers the pipeline, delivering updates to your application seamlessly. You can either bring your own deployment files for quick pipeline creation or generate Dockerfiles and Kubernetes manifests to containerize and deploy non-containerized applications with minimal effort.

## Prerequisites

- A GitHub account or an Azure DevOps organization.
- An AKS cluster. If you don't have one, you can create one using the steps in
[Deploy an Azure Kubernetes Service (AKS) cluster](learn/quick-kubernetes-deploy-portal). - An Azure Container Registry (ACR). If you don't have one, you can create one using the steps in
[Integrate Azure Container Registry (ACR) with an Azure Kubernetes Service (AKS) cluster](cluster-container-registry-integration). - An application to deploy.

### Connect to source code repository

Create an automated deployment workflow and authorize it to connect to the desired source code repository.

- In the Azure portal, navigate to your AKS cluster resource.
- From the service menu, under
**Settings**, select**Automated deployments**>**Create**. - Under
**Repository details**, enter a name for the workflow, then select**GitHub or ADO**for your repository location. - Select
**Authorize access**to connect to the desired repository. - Choose the
**Repository**and**Branch**, and then select**Next**.

### Choose the container image configuration

To get an application ready for Kubernetes, you need to build it into a container image and store it in a container registry. You use a Dockerfile to provide instructions on how to build the container image. If your source code repository doesn't already have a Dockerfile, Automated Deployments can generate one for you. Otherwise, you can use an existing Dockerfile.

Use Automated Deployments to generate a Dockerfile for many languages and frameworks such as Go, C#, Node.js, Python, Java, Gradle, Clojure, PHP, Ruby, Erlang, Swift, and Rust. The language support is built on what's available in [draft.sh](https://draft.sh).

- Select
**Auto-containerize (generate Dockerfile)**for the container configuration. - Select the
**location of where to save the generated Dockerfile**in the repository. - Select the
**application environment**from the list of supported languages and frameworks. - Enter the
**application port**. - Provide the
**Dockerfile build context**path. - Select an existing
**Azure Container Registry**or create a new one. This registry is used to store the built application image.

### Choose the Kubernetes manifest configuration

Note

The Generate Manifests option also supports advanced features like Service Connector integration, auto-generated Ingress resources, and more detailed, customizable Kubernetes manifest files.

An application running on Kubernetes consists of many Kubernetes primitive components. These components describe what container image to use, how many replicas to run, if there's a public IP required to expose the application, etc. For more information, see the official [Kubernetes documentation][kubernetes-documentation]. If your source code repository doesn't already have the basic Kubernetes manifests to deploy, Automated Deployments can generate them for you. Otherwise, you can use a set of existing manifests. You can also choose an existing Helm chart.

If your code repository already has a Dockerfile, you can select it to be used to build the application image.

- Select
**Use existing Kubernetes manifest deployment files**for the deployment options. - Select the
**Kubernetes manifest file or folder**from your repository. - Select
**Next**.

## (Optional) Use a managed ingress and/or Service Connector

When generating Kubernetes manifests with Automated Deployments, you can optionally enable App Routing to set up an ingress controller for your application. You can also use Service Connector to create a new connection or seamlessly integrate your app with an existing Azure service backend.

App Routing provides a fully managed NGINX-based ingress controller out of the box, complete with built-in SSL/TLS encryption using certificates stored in Azure Key Vault and DNS zone management through Azure DNS. When using Automated Deployments, the expose ingress command integrates seamlessly with App Routing, making it easy to expose your application to external traffic under a secure, custom DNS name—with minimal configuration.

- Select the
**Expose ingress**box. - Choose between an
**Existing ingress controller**or a**New ingress controller**. - Choose between using a
**SSL/TLS enabled**or**Insecure**ingress controller. - (Optional) Enter
**Certificate details**if choosing a**SSL/TLS enabled**ingress controller. - Choose between using
**Azure DNS**or a**3rd party provider**. - Enter the
**Azure DNS Zone**and**Subdomain name**.

## (Optional) Add environment variables

Define environment variables for a container in Kubernetes by specifying name-value pairs. Environment variables are important as they help enable easier management of settings, secure handling of sensitive information, and flexibility across environments.

## Review configuration and deploy

Review the configuration for the application, and Kubernetes manifests, then select **Deploy**. A pull request (PR) will be generated against the repository that you selected, so don't navigate away from deployment page.

### Review and merge pull request

When the deployment succeeds, select **View pull request** to view the details of the generated pull request on your code repository.

- Review the changes under
**Files changed**and make any desired edits. - Select
**Merge pull request**to merge the changes into your code repository.

Merging the change runs the GitHub Actions workflow that builds your application into a container image, stores it in Azure Container Registry, and deploys it to the cluster.

### Check the deployed resources

After the pipeline is completed, you can review the created Kubernetes `Service`

in the Azure portal by selecting **Services and ingresses** under the **Kubernetes resources** section of the service menu.

Selecting the **External IP** should open up a new browser page with the running application.

## Delete resources

Once you're done with your cluster, use the following steps to delete it to avoid incurring Azure charges:

- In the Azure portal, navigate to
**Automated deployments** - Select
**...**on the pipeline of your choice. - Select
**Delete**.


---

<!-- DOCUMENTO FUSIONADO: stateful-workload-upgrades.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/stateful-workload-upgrades -->

# Stateful workload upgrade patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade clusters that run databases and stateful applications without data loss by using these proven patterns.

## What this article covers

This article provides database-specific upgrade patterns for Azure Kubernetes Service (AKS) clusters with stateful workloads, such as:

- PostgreSQL Ferris wheel pattern for ~30-second downtime.
- Redis rolling replacement for zero-downtime cache upgrades.
- MongoDB step-down cascades for replica set safety.
- Emergency upgrade checklists for security responses.
- Validation and rollback procedures for data protection.

These patterns are best for use by database administrators for applications with persistent data and mission-critical stateful services.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

[Do you need an emergency upgrade?](#emergency-upgrade-checklist)[Do you need help with a PostgreSQL cluster?](#the-ferris-wheel-pattern-postgresql)[Do you need a Redis cache rolling replace?](#redis-cluster-rolling-replace)

## Choose your pattern

| Database type | Upgrade pattern | Downtime | Complexity | Best for |
|---|---|---|---|---|
| PostgreSQL |
|

[Rolling replace](#redis-cluster-rolling-replace)[Step-down cascade](#mongodb-replica-set-step-down)*(coming soon)**(coming soon)*## Emergency upgrade checklist

Do you need to upgrade now because of security issues?

Run the following commands for an immediate safety check (two minutes):

`# Verify all replicas are healthy kubectl get pods -l tier=database -o wide # Check replication lag ./scripts/check-replica-health.sh # Ensure recent backup exists kubectl get job backup-job -o jsonpath='{.status.completionTime}'`

Choose an emergency pattern (one minute):

**PostgreSQL/MySQL:**Use[Ferris wheel](#the-ferris-wheel-pattern-postgresql)(30-second downtime).**Redis/Memcached:**Use[Rolling replace](#redis-cluster-rolling-replace)(zero downtime).**MongoDB/CouchDB:**Use[Step-down cascade](#mongodb-replica-set-step-down)(10-second downtime).

Run with a safety net (15-minute to 30-minute window):

- Always test rollback procedures in advance.
- Monitor application metrics during the upgrade.
- Keep the database team on standby.


## The Ferris wheel pattern: PostgreSQL

This pattern is best for 3-node PostgreSQL clusters with primary/replica setup across availability zones.

Visual pattern:

```
Initial: [PRIMARY] [REPLICA-1] [REPLICA-2]
Step 1: [PRIMARY] [REPLICA-1] [NEW-NODE] ← Add new node
Step 2: [REPLICA-1] [NEW-NODE] [REPLICA-2] ← Promote & remove old primary
Step 3: [NEW-PRIMARY] [NEW-NODE] [REPLICA-2] ← Complete rotation
```


### Quick implementation (20 minutes)

```
# 1. Add new node to cluster
kubectl scale statefulset postgres-cluster --replicas=4
# 2. Wait for new replica to sync
kubectl wait --for=condition=ready pod postgres-cluster-3 --timeout=300s
# 3. Promote new primary and failover (30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# 4. Update service endpoint
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"app":"postgres-cluster","role":"primary","pod":"postgres-cluster-3"}}}'
# 5. Remove old primary node
kubectl delete pod postgres-cluster-0
```


**Detailed step-by-step guide**

#### Prerequisites validation

```
#!/bin/bash
# pre-upgrade-validation.sh
echo "=== PostgreSQL Cluster Health Check ==="
# Check replication status
kubectl exec postgres-primary-0 -- psql -c "SELECT * FROM pg_stat_replication;"
# Verify sync replication (must show 'sync' state)
SYNC_COUNT=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT count(*) FROM pg_stat_replication WHERE sync_state='sync';")
if [ "$SYNC_COUNT" -lt 2 ]; then
echo "ERROR: Need at least 2 synchronous replicas"
exit 1
fi
# Confirm recent backup exists
LAST_BACKUP=$(kubectl get job postgres-backup -o jsonpath='{.status.completionTime}')
echo "Last backup: $LAST_BACKUP"
# Test failover capability in staging first
echo "✅ Prerequisites validated"
```


#### Step 1: Scale up with a new node

```
# Add new node with upgraded Kubernetes version
kubectl patch statefulset postgres-cluster --patch '{
"spec": {
"replicas": 4,
"template": {
"spec": {
"nodeSelector": {
"kubernetes.io/arch": "amd64",
"aks-nodepool": "upgraded-pool"
}
}
}
}
}'
# Monitor new pod startup
kubectl get pods -l app=postgres-cluster -w
# Verify new replica joins cluster
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
```


#### Step 2: Run a controlled failover

```
#!/bin/bash
# controlled-failover.sh
echo "=== Starting Controlled Failover ==="
# Ensure minimal replication lag (< 0.1-second)
LAG=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT EXTRACT(EPOCH FROM now() - pg_last_xact_replay_timestamp());")
if (( $(echo "$LAG > 0.1" | bc -l) )); then
echo "ERROR: Replication lag too high ($LAG seconds)"
exit 1
fi
# Pause application writes (use connection pool drain)
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement max_db_connections=0"}}'
# Wait for active transactions to complete
sleep 10
# Promote new primary (this is the 30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# Update service selector to new primary
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-3"
}
}
}'
# Resume application writes
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement"}}'
echo "✅ Failover completed"
```


#### Step 3: Clean up and validate

```
# Remove old primary node
kubectl delete pod postgres-cluster-0 --force
# Scale back to 3 replicas
kubectl patch statefulset postgres-cluster --patch '{"spec":{"replicas":3}}'
# Validate cluster health
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
# Test application connectivity
kubectl run test-db-connection --image=postgres:15 --rm -it -- psql -h postgres-primary -U app_user -d app_db -c "SELECT version();"
```


### Advanced configuration

For mission-critical databases that require a <10-second downtime:

```
# Use synchronous replication with multiple standbys
# postgresql.conf
synchronous_standby_names = 'ANY 2 (standby1, standby2, standby3)'
synchronous_commit = 'remote_apply'
```


### Success validation

To validate your progress, use the following checklist:

- New primary accepts reads and writes.
- All replicas show healthy replication.
- Application reconnects automatically.
- No data loss detected.
- Backup/restore tested on new primary.

### Emergency rollback

##### For immediate issues (<2 minutes)

Redirect traffic to the previous primary:

```
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-1"
}
}
}'
```


##### For comprehensive failover recovery (5-10 minutes)

Stop writes to the current primary:

`kubectl exec postgres-primary-0 -- psql -c "SELECT pg_reload_conf();"`

Redirect service to a healthy replica:

`kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-1-0"}}}'`

Promote a replica to the new primary:

`kubectl exec postgres-replica-1-0 -- pg_ctl promote -D /var/lib/postgresql/data kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=60s`

Update connection strings:

`kubectl patch configmap postgres-config --patch '{"data":{"primary-host":"postgres-replica-1-0.postgres"}}'`

Verify that the new primary accepts writes:

`kubectl exec postgres-replica-1-0 -- psql -c "CREATE TABLE upgrade_test (id serial, timestamp timestamp default now());" kubectl exec postgres-replica-1-0 -- psql -c "INSERT INTO upgrade_test DEFAULT VALUES;"`


**Expected outcome:** Approximately 30-second downtime, zero data loss, and an upgraded node that runs the current version of Kubernetes.

#### Step 3: Upgrade Node1 (former primary)

```
#!/bin/bash
# upgrade-node1.sh
echo "=== Step 3: Upgrade Node1 (Former Primary) ==="
# Drain Node1 gracefully
kubectl drain aks-nodepool1-12345678-vmss000000 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
# Trigger node upgrade
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Monitor upgrade progress
while kubectl get node aks-nodepool1-12345678-vmss000000 -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}' | grep -q "False"; do
echo "Waiting for node upgrade to complete..."
sleep 30
done
echo "Node1 upgrade completed"
```


#### Step 4: Rejoin Node1 as a replica

```
#!/bin/bash
# rejoin-node1.sh
echo "=== Step 4: Rejoin Node1 as Replica ==="
# Wait for postgres pod to be scheduled on upgraded node
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=300s
# Reconfigure as replica pointing to new primary (Node2)
kubectl exec postgres-primary-0 -- bash -c "
echo 'standby_mode = on' >> /var/lib/postgresql/data/recovery.conf
echo 'primary_conninfo = \"host=postgres-replica-1-0.postgres port=5432\"' >> /var/lib/postgresql/data/recovery.conf
"
# Restart postgres to apply replica configuration
kubectl delete pod postgres-primary-0
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=120s
# Verify replication is working
kubectl exec postgres-replica-1-0 -- psql -c "SELECT * FROM pg_stat_replication WHERE application_name='postgres-primary-0';"
echo "Node1 successfully rejoined as replica"
```


#### Step 5: Upgrade Node3 (Replica-2)

```
#!/bin/bash
# upgrade-node3.sh
echo "=== Step 5: Upgrade Node3 (Replica-2) ==="
# Similar process for Node3
kubectl drain aks-nodepool1-12345678-vmss000002 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Wait for upgrade and pod readiness
kubectl wait --for=condition=ready pod postgres-replica-2-0 --timeout=300s
# Verify all replicas are in sync
kubectl exec postgres-replica-1-0 -- psql -c "SELECT application_name, state, sync_state FROM pg_stat_replication;"
```


#### Step 6: Final failover (Node2 → Node3)

```
#!/bin/bash
# final-failover.sh
echo "=== Step 6: Final Failover and Node2 Upgrade ==="
# Failover primary from Node2 to Node3
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-2-0"}}}'
kubectl exec postgres-replica-2-0 -- pg_ctl promote -D /var/lib/postgresql/data
# Upgrade Node2
kubectl drain aks-nodepool1-12345678-vmss000001 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Rejoin Node2 as replica
kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=300s
echo "All nodes upgraded successfully. PostgreSQL cluster operational."
```


### Validation and monitoring

```
#!/bin/bash
# post-upgrade-validation.sh
echo "=== Post-Upgrade Validation ==="
# Verify cluster topology
kubectl get pods -l app=postgres -o wide
# Check all replicas are connected
kubectl exec postgres-replica-2-0 -- psql -c "SELECT application_name, client_addr, state FROM pg_stat_replication;"
# Validate data integrity
kubectl exec postgres-replica-2-0 -- psql -c "SELECT COUNT(*) FROM upgrade_test;"
# Performance validation
kubectl exec postgres-replica-2-0 -- psql -c "EXPLAIN ANALYZE SELECT * FROM pg_stat_activity;"
echo "Upgrade validation completed successfully"
```


## Redis cluster rolling replace

In this scenario, a six-node Redis cluster (three primaries and three replicas) requires zero downtime.

### Implementation

```
#!/bin/bash
# redis-cluster-upgrade.sh
echo "=== Redis Cluster Rolling Upgrade ==="
# Get cluster topology
kubectl exec redis-0 -- redis-cli cluster nodes
# Upgrade replica nodes first (no impact to writes)
for replica in redis-1 redis-3 redis-5; do
echo "Upgrading replica: $replica"
# Remove replica from cluster temporarily
REPLICA_ID=$(kubectl exec redis-0 -- redis-cli cluster nodes | grep $replica | cut -d' ' -f1)
kubectl exec redis-0 -- redis-cli cluster forget $REPLICA_ID
# Drain and upgrade node
kubectl delete pod $replica
kubectl wait --for=condition=ready pod $replica --timeout=120s
# Rejoin cluster
kubectl exec redis-0 -- redis-cli cluster meet $(kubectl get pod $replica -o jsonpath='{.status.podIP}') 6379
echo "Replica $replica upgraded and rejoined"
done
# Upgrade master nodes with failover
for master in redis-0 redis-2 redis-4; do
echo "Upgrading master: $master"
# Trigger failover to replica
kubectl exec $master -- redis-cli cluster failover
# Wait for failover completion
sleep 10
# Upgrade the demoted master (now replica)
kubectl delete pod $master
kubectl wait --for=condition=ready pod $master --timeout=120s
echo "Master $master upgraded"
done
echo "Redis cluster upgrade completed"
```


## MongoDB replica set step-down

In this scenario, a three-member MongoDB replica set requires coordinated primary step-down.

### Implementation

```
#!/bin/bash
# MongoDB upgrade script
Echo "=== MongoDB Replica Set Upgrade ==="
# Check replica set status
kubectl exec mongo-0 --mongo --eval "rs.status()"
```


---

<!-- DOCUMENTO FUSIONADO: _container-network-observability-logs__use-azure-dedicated-hosts_aks-communicati_a157e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-network-observability-logs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.


---

<!-- DOCUMENTO FUSIONADO: _use-azure-dedicated-hosts_aks-communication-manager.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-azure-dedicated-hosts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-azure-dedicated-hosts -->

# Add Azure Dedicated Host to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Dedicated Host is a service that provides physical servers - able to host one or more virtual machines - dedicated to one Azure subscription. Dedicated hosts are the same physical servers used in our data centers, provided as a resource. You can provision dedicated hosts within a region, availability zone, and fault domain. Then, you can place VMs directly into your provisioned hosts, in whatever configuration best meets your needs.

Using Azure Dedicated Hosts for nodes with your AKS cluster has the following benefits:

- Hardware isolation at the physical server level. No other VMs will be placed on your hosts. Dedicated hosts are deployed in the same data centers and share the same network and underlying storage infrastructure as other, non-isolated hosts.
- Control over maintenance events initiated by the Azure platform. While most maintenance events have little to no impact on your virtual machines, there are some sensitive workloads where each second of pause can have an impact. With dedicated hosts, you can opt in to a maintenance window to reduce the impact to your service.

## Before you begin

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Before you start, ensure that your version of the Azure CLI is 2.39.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you integrate Azure Dedicated Host with Azure Kubernetes Service:

- Accelerated Networking
- An existing agent pool can't be converted from non-ADH to ADH or ADH to non-ADH.
- It isn't supported to update agent pool from host group A to host group B.
- Using ADH across subscriptions.

## Planning for ADH Capacity on AKS

Not all host SKUs are available in all regions, and availability zones. You can list host availability, and any offer restrictions before you start provisioning dedicated hosts.

```
az vm list-skus --location eastus --resource-type hostGroups/hosts -o table
```


Note

First, when using host group, the nodepool fault domain count is always the same as the host group fault domain count. In order to use cluster auto-scaling to work with ADH and AKS, please make sure your host group fault domain count and capacity is enough. Secondly, only change fault domain count from the default of 1 to any other number if you know what they are doing as a misconfiguration could lead to a unscalable configuration.

[Determine how many hosts you would need based on the expected VM Utilization](/en-us/azure/virtual-machines/dedicated-host-general-purpose-skus).

Evaluate [host utilization](/en-us/azure/virtual-machines/dedicated-hosts-how-to#check-the-status-of-the-host) to determine the number of allocatable VMs by size before you deploy.

```
az vm host get-instance-view --resource-group myDHResourceGroup --host-group MyHostGroup --name MyHost
```


## Add a Dedicated Host Group to an AKS cluster

A host group is a resource that represents a collection of dedicated hosts. You create a host group in a region and an availability zone, and add hosts to it. When planning for high availability, there are more options. You can use one or both of the following options with your dedicated hosts:

- Span across multiple availability zones. In this case, you're required to have a host group in each of the zones you wish to use.
- Span across multiple fault domains, which are mapped to physical racks.

In either case, you need to provide the fault domain count for your host group. If you don't want to span fault domains in your group, use a fault domain count of 1.

You can also decide to use both availability zones and fault domains.

## Create a Host Group

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

For more information about the host SKUs and pricing, see [Azure Dedicated Host pricing](https://azure.microsoft.com/pricing/details/virtual-machines/dedicated-host/).

Use az vm host create to create a host. If you set a fault domain count for your host group, you'll be asked to specify the fault domain for your host.

In this example, we'll use [az vm host group create](/en-us/cli/azure/vm/host/group#az-vm-host-group-create) to create a host group using both availability zones and fault domains.

```
az vm host group create \
--name myHostGroup \
--resource-group myDHResourceGroup \
--zone 1 \
--platform-fault-domain-count 1 \
--automatic-placement true
```


## Create a Dedicated Host

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

If you set a fault domain count for your host group, you'll need to specify the fault domain for your host.

```
az vm host create \
--host-group myHostGroup \
--name myHost \
--sku DSv3-Type1 \
--platform-fault-domain 1 \
--resource-group myDHResourceGroup
```


## Use a user-assigned Identity

Important

A user-assigned Identity with "contributor" role on the Resource Group of the Host Group is required.

First, create a Managed Identity

```
az identity create --resource-group <Resource Group> --name <Managed Identity name>
```


Assign Managed Identity

```
az role assignment create --assignee <id> --role "Contributor" --scope <Resource id>
```


## Create an AKS cluster using the Host Group

Create an AKS cluster, and add the Host Group you just configured.

```
az aks create \
--resource-group MyResourceGroup \
--name MyManagedCluster \
--location eastus \
--nodepool-name agentpool1 \
--node-count 1 \
--host-group-id <id> \
--node-vm-size Standard_D2s_v3 \
--assign-identity <id> \
--generate-ssh-keys
```


## Add a Dedicated Host Node Pool to an existing AKS cluster

Add a Host Group to an already existing AKS cluster.

```
az aks nodepool add --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup --node-count 1 --host-group-id <id> --node-vm-size Standard_D2s_v3
```


## Remove a Dedicated Host Node Pool from an AKS cluster

```
az aks nodepool delete --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup
```


## Next steps

In this article, you learned how to create an AKS cluster with a Dedicated host, and to add a dedicated host to an existing cluster. For more information about Dedicated Hosts, see [dedicated-hosts](/en-us/azure/virtual-machines/dedicated-hosts).


---

<!-- DOCUMENTO FUSIONADO: aks-communication-manager.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-communication-manager -->

# Set up the Azure Kubernetes Service communication manager

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) communication manager streamlines notifications for all your AKS maintenance tasks by using Azure Resource Notifications and Azure Resource Graph frameworks. The communication manager gives you timely alerts on event triggers and outcomes, so that you can closely monitor your upgrades.

If maintenance fails, the communication manager notifies you with the reasons for the failure. This information reduces operational hassles related to observability and follow-ups.

By following the steps in this article, you can set up notifications for all types of automatic upgrades that use maintenance windows.

## Prerequisites

Configure your cluster for either the

[automatic upgrade channel](auto-upgrade-cluster)or the[automatic upgrade channel for nodes](auto-upgrade-node-os-image).Create a

[planned maintenance window](planned-maintenance)for your configuration of automatic upgrades.

## Set up the communication manager

In the Azure portal, go to the resource.

Select

**Monitoring**>**Alerts**>**Alert Rules**, and then select**Create**.On the

**Condition**tab, for**Signal name**, select**Custom log search**.In the

**Search query**box, paste one of the following custom queries. Be sure to update the`where id contains`

path to reference your resources for subscription ID, resource group name, and cluster name.The following query is for notifications of automatic upgrades for clusters:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "K8sVersionUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

The following query is for notifications of automatic upgrades for NodeOS:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "NodeOSUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

Go to the

**Condition**tab. Configure the alert conditions with the following settings:**Measure**: Select**Table rows**.**Aggregation type**: Select**Count**.**Aggregation granularity**: Select**30 minutes**.**Threshold value**: Keep at**0**.**Split by dimensions**: For**Dimension name**, select**status**. Then select the**Include all future values**checkbox.

In the

**Split by dimensions**area, for**Dimension values**, select a value. Because you selected**status**for the dimension name, the available values are**Scheduled**,**Started**,**Completed**,**Canceled**, and**Failed**.Note

These status values appear only if your cluster previously executed automatic upgrade operations. For new clusters or for clusters that haven't undergone automatic upgrades yet, the dropdown list might appear empty or show no available dimensions. After your cluster performs its first automatic upgrade, these status values become available for selection.

Go to the

**Actions**tab. Make sure that an action group with the correct email address exists, so that you can receive the notifications:Select

**Use action groups**>**Create an action group**.For

**Notification type**, select**Email/SMS_message/Push/Voice**.Select the

**Email**checkbox, and then enter the email address in the**Email**box.

Go to the

**Details**tab. Assign a managed identity so that you can grant access to the necessary resources. In the**Identity**area, select**System assigned managed identity**.Go to the

**Review + create**tab, and then select**Create**.Now that you've created the alert rule, you can assign the appropriate roles for the managed identity:

- In the alert rule, go to
**Settings**>**Identity**>**System assigned managed identity**>**Azure role assignments**. - Select
**Add role assignment**, select the**Reader**role, and assign it to the resource group. - Select
**Add role assignment**again, select the**Reader**role, and assign it to the subscription.

Tip

If you don't see the

**Identity**option, make sure that you created your alert rule and that you have the necessary permissions.- In the alert rule, go to

After you set up the communication manager, it sends advance notices one week before maintenance starts and one day before maintenance starts. It also sends you timely alerts during the maintenance operation.

## Verify the configuration

To upgrade the cluster, wait for the automatic upgrader to start. Then verify that you promptly receive notices on the email address that you configured to receive notices.

Check the Azure Resource Graph database for the scheduled notification record. Each scheduled event notification should be listed as one record in the `ContainerServiceEventResources`

table.
