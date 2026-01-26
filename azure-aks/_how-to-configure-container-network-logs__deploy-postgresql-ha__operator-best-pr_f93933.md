---
merged_at: 2026-01-26T23:04:05.989226
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-logs -->

# Set up container network logs with Advanced Container Networking Services (preview)

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

In this article, you complete the steps to configure and use the container network logs feature in Advanced Container Networking Services for Azure Kubernetes Service (AKS). These logs offer persistent network flow monitoring tailored to enhance visibility in containerized environments.

By capturing container network logs, you can effectively track network traffic, detect anomalies, optimize performance, and ensure compliance with established policies. Follow the detailed instructions provided to set up and integrate container network logs for your system. For more information about the container network logs feature, see [Overview of container network logs](container-network-observability-logs).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is 2.75.0. To find your version, run

`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Container network logs in stored logs mode work only for Cilium data planes.

Container network logs in on-demand mode work for both Cilium and non-Cilium data planes.

If your existing cluster is version 1.33 or earlier, upgrade the cluster to the latest available Kubernetes version.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`19.0.07`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingFlowLogsPreview feature flag

First, register the AdvancedNetworkingFlowLogsPreview feature flag by using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command:

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


Verify successful registration by using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


When the feature shows **Registered**, refresh the registration of the `Microsoft.ContainerService`

resource provider by using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

## Limitations

- Layer 7 flow data is captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - Domain Name System (DNS) flows and related metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform isn't supported at this time.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the log table plan is set to Basic logs, the prebuilt Grafana dashboards don't function as expected.
- The Auxiliary logs table plan isn't supported.

## Configure stored logs mode for container network logs

### Deployment methods

You can onboard to container network logs using different deployment methods:

This section provides two paths for setting up container network logs based on your current situation:

: Complete setup for new AKS clusters[New clusters](#new-clusters): Enable container network logs on existing AKS clusters[Existing clusters](#existing-clusters)

## New clusters

This section guides you through setting up container network logs on a new AKS cluster from start to finish.

### Create a new AKS cluster with Advanced Container Networking Services

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
export LOCATION="<location>"
# Create the resource group if it doesn't already exist
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location $LOCATION \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 or later \
--enable-acns
```


### Configure custom resources for log filtering

To configure container network logs in stored logs mode, you must define specific custom resources to set filters for log collection. When at least one custom resource is defined, logs are collected and stored on the host node at `/var/log/acns/hubble/events.log`

.

To configure logging, you must define and apply the `ContainerNetworkLog`

type of custom resource. You set filters like namespace, pod, service, port, protocol, and verdict. Multiple custom resources can exist in a cluster simultaneously. If no custom resource is defined with nonempty filters, no logs are saved in the designated location.

The following sample definition demonstrates how to configure the `ContainerNetworkLog`

type of custom resource.

### ContainerNetworkLog CRD template

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkLog
metadata:
name: sample-containernetworklog # Cluster scoped
spec:
includefilters: # List of filters
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
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`includefilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. Include filters can't be empty and must have at least one filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . This parameter is optional. If not specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . This parameter is optional. If not specified, logs with all verdicts are included. |
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

Apply the

`ContainerNetworkLog`

custom resource to enable log collection at the cluster:`kubectl apply -f <crd.yaml>`

Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

Logs stored locally on host nodes are temporary because the host or node itself isn't a persistent storage solution. Logs on host nodes are also rotated when their size reaches 50 MB. For longer-term storage and analysis, we recommend that you configure the Azure Monitor Agent on the cluster to collect and retain logs in the Log Analytics workspace.

Alternatively, you can integrate a partner logging service like an OpenTelemetry collector for more log management options.

### Configure Azure Monitor for managed storage (recommended)

For persistent storage and advanced analytics, configure the Azure Monitor Agent to collect and store logs in a Log Analytics workspace:

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
# Enable azure monitor with high log scale mode
### To use the default Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME
### To use an existing Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>
# Update the AKS cluster with the enable-container-network-logs flag
az aks update --enable-acns \
--enable-container-network-logs \
-g $RESOURCE_GROUP \
-n $CLUSTER_NAME
```


Note

When enabled, container network flow logs are written to `/var/log/acns/hubble/events.log`

when the `ContainerNetworkLog`

custom resource is applied. If Log Analytics integration is enabled later, the Azure Monitor Agent begins collecting logs at that point. Logs older than two minutes aren't ingested. Only new entries that are appended after monitoring begins are collected in a Log Analytics workspace.

## Existing clusters

Note

If your cluster already has Advanced Container Networking Services (ACNS) enabled, you can start collecting flow logs on the host node by simply applying a ContainerNetworkLog CRD. However, if you want to enable flow logs with Log Analytics workspace integration for persistent storage and advanced analytics, follow the steps in the [Configure integration with log analytics on existing cluster](#configure-integration-with-log-analytics-on-existing-cluster) section.

```
# Set environment variables for your existing cluster. Make sure you replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
```


### Configure integration with log analytics on existing cluster

To enable container network logs on an existing cluster:

Check whether monitoring add-ons are already enabled on that cluster:

`az aks addon list -g $RESOURCE_GROUP -n $CLUSTER_NAME`

If monitoring add-ons are enabled, disable monitoring add-ons:

`az aks disable-addons -a monitoring -g $RESOURCE_GROUP -n $CLUSTER_NAME`

Complete this step because monitoring add-ons might already be enabled, but not for high scale. For more information, see

[High-scale mode](/en-us/azure/azure-monitor/containers/container-insights-high-scale).Set Azure Monitor to

`enable-high-log-scale-mode`

:`### Use default Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME ### Use existing Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>`

Update the AKS cluster with the

`enable-container-network-logs`

flag:`az aks update --enable-acns \ --enable-container-network-logs \ -g $RESOURCE_GROUP \ -n $CLUSTER_NAME`

Create the CRD as per the

[ContainerNetworkLog template](#containernetworklog-crd-template)mentioned above and apply it to start log collection in log analytics workspace.Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

**Viewing L7 flows and DNS errors**

To capture Layer 7 (L7) flow data and DNS errors/flows in your container network logs, you must apply Cilium network policies with FQDN filtering and L7 policy support enabled. Without these policies, L7 and DNS-related flow information won't be captured.

Example of a Cilium network policy with FQDN filtering and L7 support:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: l7-dns-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: myapp
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: UDP
rules:
dns:
- matchPattern: "*.example.com"
- toFQDNs:
- matchPattern: "*.example.com"
toPorts:
- ports:
- port: "443"
protocol: TCP
rules:
http:
- method: "GET"
path: "/1"
```


Apply the policy using:

```
kubectl apply -f l7-dns-policy.yaml
```


For more information, see [Configure a Layer 7 policy](how-to-apply-l7-policies) and [Configure an FQDN policy](how-to-apply-fqdn-filtering-policies)

## Common post-setup steps to verify configuration

The following steps apply to both new and existing cluster setups.

### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Validate the setup

Validate that the retina network flow log capability is enabled:

```
az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME
```


Expected output:

```
"networkProfile":{
"advancedNetworking": {
"enabled": true,
"observability":{
"enabled": true
}
}
}
----------------------------
"osmagent":{
"config":{
"enableContainerNetworkLogs": "True"
}
}
```


Check which custom resource definitions are installed for flow logs:

```
kubectl get containernetworklog
```


This command lists all the `ContainerNetworkLog`

custom resources created in the cluster.

Validate that the `ContainerNetworkLog`

custom resource is applied:

```
k describe containernetworklog <cr-name>
```


Expect to see a `Spec`

node that contains `Include filters`

and a `Status`

node. The value for `Status`

> `State`

should be `CONFIGURED`

(not `FAILED`

).

```
Spec:
Includefilters:
From:
Namespaced Pod:
namespace/pod-
Name: sample-filter
Protocol:
tcp
To:
Namespaced Pod:
namespace/pod-
Verdict:
dropped
Status:
State: CONFIGURED
Timestamp: 2025-05-01T11:24:48Z
```


Users can apply multiple `ContainerNetworkLog`

custom resources in the cluster. Each custom resource has its own status.

### Querying Container Network Flow Logs in Log Analytics dashboard

When Container Network Flow Logs are enabled with a Log Analytics workspace, you have access to historical logs that allow you to analyze network traffic patterns over time. You can query these logs using the `ContainerNetworkLog`

table to perform detailed forensic analysis and troubleshooting.

Customers can use Kusto Query Language (KQL) to analyze network data in Log Analytics. This historical data is invaluable for understanding network behavior patterns, identifying security incidents, troubleshooting connectivity issues, and performing root cause analysis over extended periods. The ability to correlate network events across time helps detect intermittent issues and understand traffic flows that may not be apparent in real-time monitoring.

To see sample queries that can be applied for troubleshooting connectivity issues, refer to the [progressive diagnosis using flow logs](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#progressive-diagnosis-using-flow-logs) in the AKS Labs documentation.

### Azure Managed Grafana

You can access prebuilt Grafana dashboards through the Azure portal. Navigate to either the Azure Monitor resource or your Azure Kubernetes Service (AKS) cluster to view and interact with these dashboards. But before that:

Make sure that the Azure logs pods are running:

`kubectl get pods -o wide -n kube-system | grep ama-logs`

Your output should look similar to the following example:

`ama-logs-9bxc6 3/3 Running 1 (39m ago) 44m ama-logs-fd568 3/3 Running 1 (40m ago) 44m ama-logs-rs-65bdd98f75-hqnd2 2/2 Running 1 (43m ago) 22h`

Ensure that your Managed Grafana workspace can access and search all monitoring data in the relevant subscription. This step is required to access prebuilt dashboards for network flow logs.

**Use case 1**: If you're a subscription Owner or a User Access Administrator, when a Managed Grafana workspace is created, it comes with the Monitoring Reader role granted on all Azure Monitor data and Log Analytics resources in the subscription. The new Managed Grafana workspace can access and search all monitoring data in the subscription. It can view the Azure Monitor metrics and logs from all resources and view any logs stored in Log Analytics workspaces in the subscription.**Use case 2**: If you're not a subscription Owner or User Access Administrator, or if your Log Analytics and Managed Grafana workspaces are in different subscriptions, Grafana can't access Log Analytics and the subscription. The Grafana workspace must have the Monitoring Reader role in the relevant subscription to access prebuilt Grafana dashboards. In this scenario, complete these steps to provide access:In your Managed Grafana workspace, go to

**Settings**>**Identity**.Select

**Azure role assignments**>**Add role assignments**.For

**Scope**, enter**Subscription**. Select your subscription. Set**Role**to**Monitoring Reader**, and then select**Save**.Verify the data source for the Managed Grafana instance. To verify the subscription for the data source for the Grafana dashboards, check the

**Data source**tab in the Managed Grafana instance:


#### Visualization in Grafana dashboards

Azure Monitor dashboards with Grafana enable you to use Grafana's query, transformation, and visualization capabilities on metrics and logs collected in Azure Monitor. You can use this option as an alternative to visualize container network flow logs.

- Navigate to the left pane of the Kubernetes cluster in the Azure portal.
- Select
**Dashboards with Grafana (Preview)**. - Browse the list of available dashboards in the Azure Monitor or Azure Managed Prometheus listings.
- Select a dashboard, for example
**Azure | Insights | Containers | Networking | Flow Logs**.

You can visualize container network flow logs for analysis by using two prebuilt Grafana dashboards. You can access the dashboards either through Azure Managed Grafana or in the Azure portal.

To simplify log analysis, we provide two preconfigured Azure Managed Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard provides visualizations in which AKS workloads communicate with each other, including network requests, responses, drops, and errors. Currently, you must use[ID 23155](https://grafana.com/grafana/dashboards/23155-azure-insights-containers-networking-flow-logs//)to import these dashboards.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard provides visualizations in which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors. Use[ID 23156](https://grafana.com/grafana/dashboards/23156-azure-insights-containers-networking-flow-logs-external-traffic//).

For more information about how to use this dashboard, see the [overview of container network logs](container-network-observability-logs).

## Configure on-demand logs mode

On-demand logs mode for network flows works with both Cilium and non-Cilium data planes.

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. The features include:

**Container Network Observability:**Provides insights into your network traffic. To learn more, visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters that have the Cilium data plane support the Container Network Observability and Container Network Security features in Kubernetes version 1.29 and later.

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
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
--kubernetes-version 1.33 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-acns`

flag updates an existing AKS cluster with all Advanced Container Networking Services features. The features include [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and

[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Only clusters that have the Cilium data plane support the Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


Next, get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Install the Hubble CLI

Install the Hubble CLI to access the data it collects. Run the following commands:

```
# Set environment variables
export HUBBLE_VERSION=v1.16.3
export HUBBLE_ARCH=amd64
#Install the Hubble CLI
if [ "$(uname -m)" = "aarch64" ]; then HUBBLE_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
sha256sum --check hubble-linux-${HUBBLE_ARCH}.tar.gz.sha256sum
sudo tar xzvfC hubble-linux-${HUBBLE_ARCH}.tar.gz /usr/local/bin
rm hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
```


### Visualize the Hubble flows

Make sure that the Hubble pods are running:

`kubectl get pods -o wide -n kube-system -l k8s-app=hubble-relay`

Your output should look similar to the following example:

`hubble-relay-7ddd887cdb-h6khj 1/1 Running 0 23h`

Port-forward the Hubble Relay server:

`kubectl port-forward -n kube-system svc/hubble-relay --address 127.0.0.1 4245:443`

Mutual TLS (mTLS) ensures the security of the Hubble Relay server. To enable the Hubble client to retrieve flows, you must get the appropriate certificates and configure the client with them. Apply the certificates by using the following commands:

`#!/usr/bin/env bash set -euo pipefail set -x # Directory where certificates will be stored CERT_DIR="$(pwd)/.certs" mkdir -p "$CERT_DIR" declare -A CERT_FILES=( ["tls.crt"]="tls-client-cert-file" ["tls.key"]="tls-client-key-file" ["ca.crt"]="tls-ca-cert-files" ) for FILE in "${!CERT_FILES[@]}"; do KEY="${CERT_FILES[$FILE]}" JSONPATH="{.data['${FILE//./\\.}']}" # Retrieve the secret and decode it kubectl get secret hubble-relay-client-certs -n kube-system \ -o jsonpath="${JSONPATH}" | \ base64 -d > "$CERT_DIR/$FILE" # Set the appropriate hubble CLI config hubble config set "$KEY" "$CERT_DIR/$FILE" done hubble config set tls true hubble config set tls-server-name instance.hubble-relay.cilium.io`

Confirm that the secrets were generated:

`kubectl get secrets -n kube-system | grep hubble-`

Your output should look similar to the following example:

`kube-system hubble-relay-client-certs kubernetes.io/tls 3 9d kube-system hubble-relay-server-certs kubernetes.io/tls 3 9d kube-system hubble-server-certs kubernetes.io/tls 3 9d`

Verify that the Hubble Relay pod is running:

`hubble observe --pod hubble-relay-7ddd887cdb-h6khj`


### Visualize by using the Hubble UI

To use the Hubble UI, save the following script in the

`hubble-ui.yaml`

file:`apiVersion: v1 kind: ServiceAccount metadata: name: hubble-ui namespace: kube-system --- kind: ClusterRole apiVersion: rbac.authorization.k8s.io/v1 metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina rules: - apiGroups: - networking.k8s.io resources: - networkpolicies verbs: - get - list - watch - apiGroups: - "" resources: - componentstatuses - endpoints - namespaces - nodes - pods - services verbs: - get - list - watch - apiGroups: - apiextensions.k8s.io resources: - customresourcedefinitions verbs: - get - list - watch - apiGroups: - cilium.io resources: - "*" verbs: - get - list - watch --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRoleBinding metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina roleRef: apiGroup: rbac.authorization.k8s.io kind: ClusterRole name: hubble-ui subjects: - kind: ServiceAccount name: hubble-ui namespace: kube-system --- apiVersion: v1 kind: ConfigMap metadata: name: hubble-ui-nginx namespace: kube-system data: nginx.conf: | server { listen 8081; server_name localhost; root /app; index index.html; client_max_body_size 1G; location / { proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; # CORS add_header Access-Control-Allow-Methods "GET, POST, PUT, HEAD, DELETE, OPTIONS"; add_header Access-Control-Allow-Origin *; add_header Access-Control-Max-Age 1728000; add_header Access-Control-Expose-Headers content-length,grpc-status,grpc-message; add_header Access-Control-Allow-Headers range,keep-alive,user-agent,cache-control,content-type,content-transfer-encoding,x-accept-content-transfer-encoding,x-accept-response-streaming,x-user-agent,x-grpc-web,grpc-timeout; if ($request_method = OPTIONS) { return 204; } # /CORS location /api { proxy_http_version 1.1; proxy_pass_request_headers on; proxy_hide_header Access-Control-Allow-Origin; proxy_pass http://127.0.0.1:8090; } location / { try_files $uri $uri/ /index.html /index.html; } # Liveness probe location /healthz { access_log off; add_header Content-Type text/plain; return 200 'ok'; } } } --- kind: Deployment apiVersion: apps/v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: replicas: 1 selector: matchLabels: k8s-app: hubble-ui template: metadata: labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: serviceAccountName: hubble-ui automountServiceAccountToken: true containers: - name: frontend image: mcr.microsoft.com/oss/cilium/hubble-ui:v0.12.2 imagePullPolicy: Always ports: - name: http containerPort: 8081 livenessProbe: httpGet: path: /healthz port: 8081 readinessProbe: httpGet: path: / port: 8081 resources: {} volumeMounts: - name: hubble-ui-nginx-conf mountPath: /etc/nginx/conf.d/default.conf subPath: nginx.conf - name: tmp-dir mountPath: /tmp terminationMessagePolicy: FallbackToLogsOnError securityContext: {} - name: backend image: mcr.microsoft.com/oss/cilium/hubble-ui-backend:v0.12.2 imagePullPolicy: Always env: - name: EVENTS_SERVER_PORT value: "8090" - name: FLOWS_API_ADDR value: "hubble-relay:443" - name: TLS_TO_RELAY_ENABLED value: "true" - name: TLS_RELAY_SERVER_NAME value: ui.hubble-relay.cilium.io - name: TLS_RELAY_CA_CERT_FILES value: /var/lib/hubble-ui/certs/hubble-relay-ca.crt - name: TLS_RELAY_CLIENT_CERT_FILE value: /var/lib/hubble-ui/certs/client.crt - name: TLS_RELAY_CLIENT_KEY_FILE value: /var/lib/hubble-ui/certs/client.key livenessProbe: httpGet: path: /healthz port: 8090 readinessProbe: httpGet: path: /healthz port: 8090 ports: - name: grpc containerPort: 8090 resources: {} volumeMounts: - name: hubble-ui-client-certs mountPath: /var/lib/hubble-ui/certs readOnly: true terminationMessagePolicy: FallbackToLogsOnError securityContext: {} nodeSelector: kubernetes.io/os: linux volumes: - configMap: defaultMode: 420 name: hubble-ui-nginx name: hubble-ui-nginx-conf - emptyDir: {} name: tmp-dir - name: hubble-ui-client-certs projected: defaultMode: 0400 sources: - secret: name: hubble-relay-client-certs items: - key: tls.crt path: client.crt - key: tls.key path: client.key - key: ca.crt path: hubble-relay-ca.crt --- kind: Service apiVersion: v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: type: ClusterIP selector: k8s-app: hubble-ui ports: - name: http port: 80 targetPort: 8081`

Apply the

`hubble-ui.yaml`

manifest to your cluster:`kubectl apply -f hubble-ui.yaml`

Set up port forwarding for the Hubble UI:

`kubectl -n kube-system port-forward svc/hubble-ui 12000:80`

In your web browser, enter

`http://localhost:12000/`

to access the Hubble UI.

### Basic troubleshooting

Advanced Container Networking Services is a prerequisite to turn on the Azure Monitor Agent log collection feature.

Trying to enable the container network flow logs capability on a cluster without enabling Advanced Container Networking Services, for example:

`az aks update -g test-rg -n test-cluster --enable-container-network-logs`

Results in an error message:

`Flow logs requires '--enable-acns', advanced networking to be enabled, and the monitoring addon to be enabled.`

If the cluster Kubernetes version is earlier than version 1.33.0, trying to run

`--enable-container-network-logs`

results in an error message:`The specified orchestrator version %s is not valid. Advanced Networking Flow Logs is only supported on Kubernetes version 1.33.0 or later.`

where

`%s`

is your Kubernetes version.If you try to run

`--enable-container-network-logs`

on a subscription where the Azure Feature Exposure Control (AFEC) flag isn't enabled, an error message appears:`Feature Microsoft.ContainerService/AdvancedNetworkingFlowLogsPreview is not enabled. Please see https://aka.ms/aks/previews for how to enable features.`

If you try to apply a

`ContainerNetworkLog`

custom resource on a cluster where Advanced Container Networking Services isn't enabled, an error message appears:`error: resource mapping not found for <....>": no matches for kind "ContainerNetworkLog" in version "acn.azure.com/v1alpha1"`

Ensure that you install custom resources first.


### Disable container network logs: Stored logs mode on existing cluster

If all custom resources are deleted, flow log collection stops because no filters are defined for collection.

To disable container network log collection by the Azure Monitor Agent, run:

```
az aks update -n $CLUSTER_NAME -g $RESOURCE_GROUP --disable-container-network-logs
```


## Clean up resources

If you don't plan to use this example application, delete the resources you created in this article by using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-postgresql-ha -->

# Deploy a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you deploy a highly available PostgreSQL database on AKS.

- If you still need to create the required infrastructure for this deployment, follow the steps in
[Create infrastructure for deploying a highly available PostgreSQL database on AKS](create-postgresql-ha)to get set up, and then return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Create secret for bootstrap app user

- Generate a secret to validate the PostgreSQL deployment by interactive login for a bootstrap app user using the
command.`kubectl create secret`


Important

Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a high degree of trust in the application and carries risks that are not present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

```
PG_DATABASE_APPUSER_SECRET=$(echo -n | openssl rand -base64 16)
kubectl create secret generic db-user-pass \
--from-literal=username=app \
--from-literal=password="${PG_DATABASE_APPUSER_SECRET}" \
--namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME
```


Validate that the secret was successfully created using the

command.`kubectl get`

`kubectl get secret db-user-pass --namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


## Set environment variables for the PostgreSQL cluster

Deploy a ConfigMap to configure the CNPG operator using the following

command. These values replace the legacy`kubectl apply`

`ENABLE_AZURE_PVC_UPDATES`

toggle, which is no longer required, and help stagger upgrades and speed up replica reconnections. Before rolling this configuration into production, validate that any existing`DRAIN_TAINTS`

settings you rely on remain compatible with your Azure environment.`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -f - apiVersion: v1 kind: ConfigMap metadata: name: cnpg-controller-manager-config data: CLUSTERS_ROLLOUT_DELAY: '120' STANDBY_TCP_USER_TIMEOUT: '10' EOF`


## Install the Prometheus PodMonitors

Prometheus scrapes CNPG using the recording rules stored in the CNPG GitHub samples repo. Because the operator-managed PodMonitor is being deprecated, create and manage the PodMonitor resource yourself so you can tailor it to your monitoring stack.

Add the Prometheus Community Helm repo using the

command.`helm repo add`

`helm repo add prometheus-community \ https://prometheus-community.github.io/helm-charts`

Upgrade the Prometheus Community Helm repo and install it on the primary cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install \ --namespace $PG_NAMESPACE \ -f https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/main/docs/src/samples/monitoring/kube-stack-config.yaml \ prometheus-community \ prometheus-community/kube-prometheus-stack \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME`

Create a PodMonitor for the cluster. The CNPG team is deprecating the operator-managed PodMonitor, so you now manage it directly:

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f - apiVersion: monitoring.coreos.com/v1 kind: PodMonitor metadata: name: $PG_PRIMARY_CLUSTER_NAME namespace: ${PG_NAMESPACE} labels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} spec: selector: matchLabels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} podMetricsEndpoints: - port: metrics EOF`


## Create a federated credential

In this section, you create a federated identity credential for PostgreSQL backup to allow CNPG to use AKS workload identity to authenticate to the storage account destination for backups. The CNPG operator creates a Kubernetes service account with the same name as the cluster named used in the CNPG Cluster deployment manifest.

Get the OIDC issuer URL of the cluster using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_OIDC_ISSUER="$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

Create a federated identity credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name $AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME}" \ --audience api://AzureADTokenExchange`


## Deploy a highly available PostgreSQL cluster

In this section, you deploy a highly available PostgreSQL cluster using the [CNPG Cluster custom resource definition (CRD)](https://cloudnative-pg.io/documentation/1.23/cloudnative-pg.v1/#postgresql-cnpg-io-v1-ClusterSpec).

### Cluster CRD parameters

The following table outlines the key properties set in the YAML deployment manifest for the Cluster CRD:

| Property | Definition |
|---|---|
`imageName` |
Points to the CloudNativePG operand container image. Use `ghcr.io/cloudnative-pg/postgresql:18-system-trixie` with the in-core backup integration shown in this guide, or switch to `18-standard-trixie` when you adopt the Barman Cloud plugin. |
`inheritedMetadata` |
Specific to the CNPG operator. The CNPG operator applies the metadata to every object related to the cluster. |
`annotations` |
Includes the DNS label required when exposing the cluster endpoints and enables
`alpha.cnpg.io/failoverQuorum` |

`labels: azure.workload.identity/use: "true"`

`topologySpreadConstraints`

`"workload=postgres"`

.`resources`

*Guaranteed*. In a production environment, these values are key for maximizing usage of the underlying node VM and vary based on the Azure VM SKU used.`probes`

`startDelay`

configuration. Streaming startup and readiness probes help ensure replicas are healthy before serving traffic.`smartShutdownTimeout`

`bootstrap`

`storage`

`postgresql.synchronous`

`minSyncReplicas`

/`maxSyncReplicas`

and lets you specify synchronous replication behavior using the newer schema.`postgresql.parameters`

`postgresql.conf`

, `pg_hba.conf`

, and `pg_ident.conf`

. The sample emphasizes observability and WAL retention defaults that suit the AKS workload identity scenario but should be tuned per workload.`serviceAccountTemplate`

`barmanObjectStore`

To further isolate PostgreSQL workloads, you can add a taint (for example, `node-role.kubernetes.io/postgres=:NoSchedule`

) to your data plane nodes and replace the sample `nodeSelector`

/`tolerations`

with the values recommended by CloudNativePG. If you take this approach, label the nodes accordingly and confirm the AKS autoscaler policies align with your topology.

### PostgreSQL performance parameters

PostgreSQL performance heavily depends on your cluster's underlying resources and workload. The following table provides baseline guidance for a three-node cluster running on Standard D4s v3 nodes (16-GiB memory). Treat these values as a starting point and adjust them once you understand your workload profile:

| Property | Recommended value | Definition |
|---|---|---|
`wal_compression` |
lz4 | Compresses full-page writes written in WAL file with specified method |
`max_wal_size` |
6 GB | Sets the WAL size that triggers a checkpoint |
`checkpoint_timeout` |
15 min | Sets the maximum time between automatic WAL checkpoints |
`checkpoint_completion_target` |
0.9 | Balances checkpoint work across the checkpoint window |
`checkpoint_flush_after` |
2 MB | Number of pages after which previously performed writes are flushed to disk |
`wal_writer_flush_after` |
2 MB | Amount of WAL written out by WAL writer that triggers a flush |
`min_wal_size` |
2 GB | Sets the minimum size to shrink the WAL to |
`max_slot_wal_keep_size` |
10 GB | Upper bound for WAL left to service replication slots |
`shared_buffers` |
4 GB | Sets the number of shared memory buffers used by the server (25% of node memory in this example) |
`effective_cache_size` |
12 GB | Sets the planner's assumption about the total size of the data caches |
`work_mem` |
1/256th of node memory | Sets the maximum memory to be used for query workspaces |
`maintenance_work_mem` |
6.25% of node memory | Sets the maximum memory to be used for maintenance operations |
`autovacuum_vacuum_cost_limit` |
2400 | Vacuum cost amount available before napping, for autovacuum |
`random_page_cost` |
1.1 | Sets the planner's estimate of the cost of a nonsequentially fetched disk page |
`effective_io_concurrency` |
64 | Sets how many simultaneous requests the disk subsystem can handle efficiently |
`maintenance_io_concurrency` |
64 | A variant of "effective_io_concurrency" that is used for maintenance work |

### Deploying PostgreSQL

Deploy the PostgreSQL cluster with the Cluster CRD using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME annotations: alpha.cnpg.io/failoverQuorum: "true" spec: imageName: ghcr.io/cloudnative-pg/postgresql:18-system-trixie inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 3 smartShutdownTimeout: 30 probes: startup: type: streaming maximumLag: 32Mi periodSeconds: 5 timeoutSeconds: 3 failureThreshold: 120 readiness: type: streaming maximumLag: 0 periodSeconds: 10 failureThreshold: 6 topologySpreadConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule labelSelector: matchLabels: cnpg.io/cluster: $PG_PRIMARY_CLUSTER_NAME affinity: nodeSelector: workload: postgres resources: requests: memory: '8Gi' cpu: 2 limits: memory: '8Gi' cpu: 2 bootstrap: initdb: database: appdb owner: app secret: name: db-user-pass dataChecksums: true storage: storageClass: $POSTGRES_STORAGE_CLASS size: 64Gi postgresql: synchronous: method: any number: 1 parameters: wal_compression: lz4 max_wal_size: 6GB max_slot_wal_keep_size: 10GB checkpoint_timeout: 15min checkpoint_completion_target: '0.9' checkpoint_flush_after: 2MB wal_writer_flush_after: 2MB min_wal_size: 2GB shared_buffers: 4GB effective_cache_size: 12GB work_mem: 62MB maintenance_work_mem: 1GB autovacuum_vacuum_cost_limit: "2400" random_page_cost: "1.1" effective_io_concurrency: "64" maintenance_io_concurrency: "64" log_checkpoints: 'on' log_lock_waits: 'on' log_min_duration_statement: '1000' log_statement: 'ddl' log_temp_files: '1024' log_autovacuum_min_duration: '1s' pg_stat_statements.max: '10000' pg_stat_statements.track: 'all' hot_standby_feedback: 'on' pg_hba: - host all all all scram-sha-256 serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" backup: barmanObjectStore: destinationPath: "https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups" azureCredentials: inheritFromAzureAD: true retentionPolicy: '7d' EOF`


Note

The sample manifest uses the `ghcr.io/cloudnative-pg/postgresql:18-system-trixie`

image because it works with the in-core Barman Cloud integration shown later. When you're ready to switch to the Barman Cloud plugin, update `spec.imageName`

to `ghcr.io/cloudnative-pg/postgresql:18-standard-trixie`

and follow the [plugin configuration guidance](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) before redeploying the cluster.

Important

The example `pg_hba`

entry allows non-TLS access. If you keep this configuration, document the security implications for your team and prefer encrypted connections wherever possible.

Validate that the primary PostgreSQL cluster was successfully created using the

command. The CNPG Cluster CRD specified three instances, which can be validated by viewing running pods once each instance is brought up and joined for replication. Be patient as it can take some time for all three instances to come online and join the cluster.`kubectl get`

`kubectl get pods --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME READY STATUS RESTARTS AGE pg-primary-cnpg-r8c7unrw-1 1/1 Running 0 4m25s pg-primary-cnpg-r8c7unrw-2 1/1 Running 0 3m33s pg-primary-cnpg-r8c7unrw-3 1/1 Running 0 2m49s`


Important

If you use local NVMe with Azure Container Storage and a pod remains in the init state with a multi-attach error, the pod is still searching for the volume on a lost node. After the pod starts running, it enters a `CrashLoopBackOff`

state because CNPG creates a new replica on a new node without data and can't find the `pgdata`

directory. To resolve this issue, destroy the affected instance and bring up a new one. Run the following command:

```
kubectl cnpg destroy [cnpg-cluster-name] [instance-number]
```


## Validate the Prometheus PodMonitor is running

The manually created PodMonitor ties the kube-prometheus-stack scrape configuration to the CNPG pods you deployed earlier.

Validate the PodMonitor is running using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.monitoring.coreos.com \
$PG_PRIMARY_CLUSTER_NAME \
--output yaml
```


Example output

```
kind: PodMonitor
metadata:
labels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
name: pg-primary-cnpg-r8c7unrw
namespace: cnpg-database
spec:
podMetricsEndpoints:
- port: metrics
selector:
matchLabels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
```


If you're using Azure Monitor for Managed Prometheus, you need to add another pod monitor using the custom group name. Managed Prometheus doesn't pick up the custom resource definitions (CRDs) from the Prometheus community. Aside from the group name, the CRDs are the same. That design lets pod monitors for Managed Prometheus run alongside pod monitors that use the community CRD. If you're not using Managed Prometheus, you can skip this section. Create a new pod monitor:

```
cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f -
apiVersion: azmonitoring.coreos.com/v1
kind: PodMonitor
metadata:
name: cnpg-cluster-metrics-managed-prometheus
namespace: ${PG_NAMESPACE}
labels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
spec:
selector:
matchLabels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
podMetricsEndpoints:
- port: metrics
EOF
```


Verify that the pod monitor is created (note the difference in the group name).

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.azmonitoring.coreos.com \
-l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME \
-o yaml
```


### Option A - Azure Monitor workspace

After you deploy the Postgres cluster and the pod monitor, you can view the metrics using the Azure portal in an Azure Monitor workspace.

### Option B - Managed Grafana

Alternatively, after you deploy the Postgres cluster and pod monitors, you can create a metrics dashboard on the Managed Grafana instance created by the deployment script to visualize the metrics exported to the Azure Monitor workspace. You can access the Managed Grafana via the Azure portal. Navigate to the Managed Grafana instance created by the deployment script and select the Endpoint link as shown here:

Selecting the Endpoint link opens a new browser window where you can create dashboards on the Managed Grafana instance. Following the instructions to [configure an Azure Monitor data source](/en-us/azure/azure-monitor/visualize/grafana-plugin#configure-an-azure-monitor-data-source-plug-in), you can then add visualizations to create a dashboard of metrics from the Postgres cluster. After setting up the data source connection, from the main menu, select the Data sources option. You should see a set of data source options for the data source connection as shown here:

On the Managed Prometheus option, select the option to build a dashboard to open the dashboard editor. After the editor window opens, select the Add visualization option then select the Managed Prometheus option to browse the metrics from the Postgres cluster. After you select the metric you want to visualize, select the Run queries button to fetch the data for the visualization as shown here:

Select the Save icon to add the panel to your dashboard. You can add other panels by selecting the Add button in the dashboard editor and repeating this process to visualize other metrics. Adding the metrics visualizations, you should have something that looks like this:

Select the Save icon to save your dashboard.

## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-security -->

# Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), workload and data security is a key consideration. When you run multi-tenant clusters using logical isolation, you especially need to secure resource and workload access. Minimize the risk of attack by applying the latest Kubernetes and node OS security updates.

This article focuses on how to secure your AKS cluster. You learn how to:

- Use Microsoft Entra ID and Kubernetes role-based access control (Kubernetes RBAC) to secure API server access.
- Secure container access to node resources.
- Upgrade an AKS cluster to the latest Kubernetes version.
- Keep nodes up to date and automatically apply security patches.

You can also read the best practices for [container image management](operator-best-practices-container-image-management) and for [pod security](developer-best-practices-pod-security).

## Enable threat protection


Best practice guidanceYou can enable

[Defender for Containers]to help secure your containers. Defender for Containers can assess cluster configurations and provide security recommendations, run vulnerability scans, and provide real-time protection and alerting for Kubernetes nodes and clusters.

## Secure access to the API server and cluster nodes


Best practice guidanceOne of the most important ways to secure your cluster is to secure access to the Kubernetes API server. To control access to the API server, integrate Kubernetes RBAC with Microsoft Entra ID. With these controls,you secure AKS the same way that you secure access to your Azure subscriptions.


The Kubernetes API server provides a single connection point for requests to perform actions within a cluster. To secure and audit access to the API server, limit access and provide the lowest possible permission levels. while this approach isn't unique to Kubernetes, it's especially important when you've logically isolated your AKS cluster for multi-tenant use.

Microsoft Entra ID provides an enterprise-ready identity management solution that integrates with AKS clusters. Since Kubernetes doesn't provide an identity management solution, you may be hard-pressed to granularly restrict access to the API server. With Microsoft Entra integrated clusters in AKS, you use your existing user and group accounts to authenticate users to the API server.

Using Kubernetes RBAC and Microsoft Entra ID-integration, you can secure the API server and provide the minimum permissions required to a scoped resource set, like a single namespace. You can grant different Microsoft Entra users or groups different Kubernetes roles. With granular permissions, you can restrict access to the API server and provide a clear audit trail of actions performed.

The recommended best practice is to use *groups* to provide access to files and folders instead of individual identities. For example, use a Microsoft Entra ID *group* membership to bind users to Kubernetes roles rather than individual *users*. As a user's group membership changes, their access permissions on the AKS cluster change accordingly.

Meanwhile, let's say you bind the individual user directly to a role and their job function changes. While the Microsoft Entra group memberships update, their permissions on the AKS cluster would not. In this scenario, the user ends up with more permissions than they require.

For more information about Microsoft Entra integration, Kubernetes RBAC, and Azure RBAC, see [Best practices for authentication and authorization in AKS](concepts-identity).

## Restrict access to Instance Metadata API


Best practice guidanceAdd a network policy in all user namespaces to block pod egress to the metadata endpoint.


Note

To implement Network Policy, include the attribute `--network-policy azure`

when creating the AKS cluster. Use the following command to create the cluster:
`az aks create -g myResourceGroup -n myManagedCluster --network-plugin azure --network-policy azure --generate-ssh-keys`


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-instance-metadata
spec:
podSelector:
matchLabels: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.10.0.0/0#example
except:
- 169.254.169.254/32
```


## Secure container access to resources


Best practice guidanceLimit access to actions that containers can perform. Provide the least number of permissions, and avoid the use of root access or privileged escalation.


In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

Using user-namespaces, you improve the host isolation and limit the lateral movement in case of container breakouts. These improvements are significant whether the pod is running as root or not.

For even more granular control of container actions, you can also use built-in Linux security features such as *AppArmor* and *seccomp*.

For more information, see [Secure container access to resources](secure-container-access).

## Regularly update to the latest version of Kubernetes


Best practice guidanceTo stay current on new features and bug fixes, regularly upgrade the Kubernetes version in your AKS cluster.


Kubernetes releases new features at a quicker pace than more traditional infrastructure platforms. Kubernetes updates include:

- New features
- Bug or security fixes

New features typically move through *alpha* and *beta* status before they become *stable*. Once stable, are generally available and recommended for production use. Kubernetes new feature release cycle allows you to update Kubernetes without regularly encountering breaking changes or adjusting your deployments and templates.

AKS supports three minor versions of Kubernetes. Once a new minor patch version is introduced, the oldest minor version and patch releases supported are retired. Minor Kubernetes updates happen on a periodic basis. To stay within support, ensure you have a governance process to check for necessary upgrades. For more information, see [Supported Kubernetes versions AKS](supported-kubernetes-versions).

To check the versions that are available for your cluster, use the [az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command as shown in the following example:

```
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```


You can then upgrade your AKS cluster using the [az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The upgrade process safely:

- Cordons and drains one node at a time.
- Schedules pods on remaining nodes.
- Deploys a new node running the latest OS and Kubernetes versions.

Important

Test new minor versions in a dev test environment and validate that your workload remains healthy with the new Kubernetes version.

Kubernetes may deprecate APIs (like in version 1.16) that your workloads rely on. When bringing new versions into production, consider using [multiple node pools on separate versions](create-node-pools) and upgrade individual pools one at a time to progressively roll the update across a cluster. If running multiple clusters, upgrade one cluster at a time to progressively monitor for impact or changes.

```
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version KUBERNETES_VERSION
```


For more information about upgrades in AKS, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions) and [Upgrade an AKS cluster](upgrade-cluster).

## Process Linux node updates

Each evening, Linux nodes in AKS get security patches through their distro update channel. This behavior is automatically configured as the nodes are deployed in an AKS cluster. To minimize disruption and potential impact to running workloads, nodes are not automatically rebooted if a security patch or kernel update requires it. For more information about how to handle node reboots, see [Apply security and kernel updates to nodes in AKS](node-updates-kured).

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node will receive all the security and kernel updates available during the automatic check every night but will remain unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

## Process Windows Server node updates

For Windows Server nodes, regularly perform a node image upgrade operation to safely cordon and drain pods and deploy updated nodes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

# Windows container considerations with Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create deployments that use Windows Server containers on Azure Kubernetes Service (AKS), there are a few differences relative to Linux deployments you should keep in mind. For a detailed comparison of the differences between Windows and Linux in upstream Kubernetes, see [Windows containers in Kubernetes](https://kubernetes.io/docs/concepts/windows/intro/).

Some of the major differences include:

**Identity**: Windows Server uses a larger binary security identifier (SID) that's stored in the Windows Security Access Manager (SAM) database. This database isn't shared between the host and containers or between containers.**File permissions**: Windows Server uses an access control list based on SIDs rather than a bitmask of permissions and UID+GID.**File paths**: The convention on Windows Server is to use \ instead of /. In pod specs that mount volumes, specify the path correctly for Windows Server containers. For example, rather than a mount point of*/mnt/volume*in a Linux container, specify a drive letter and location such as*/K/Volume*to mount as the*K:*drive.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

This article covers important considerations to keep in mind when using Windows containers instead of Linux containers in Kubernetes. For an in-depth comparison of Windows and Linux containers, see [Comparison with Linux](https://kubernetes.io/docs/concepts/windows/intro/#compatibility-linux-similarities).

## Considerations

| Feature | Windows considerations |
|---|---|
|

*must*be Linux.• The maximum number of nodes per cluster is 5000.

• The Windows Server node pool name has a limit of six characters.

[Privileged containers](use-windows-hpc#limitations)**HostProcess Containers (HPC) containers**.[HPC containers](use-windows-hpc#limitations)[Create a Windows HostProcess pod](https://kubernetes.io/docs/tasks/configure-pod-container/create-hostprocess-pod/).[Azure Network Policy Manager (Azure)](use-network-policies#overview-of-network-policy)• Named ports

• SCTP protocol

• Negative match labels or namespace selectors (all labels except "debug=true")

• "except" CIDR blocks (a CIDR with exceptions)

• Windows Server 2019

[Node upgrade](manage-node-pools#upgrade-a-single-node-pool)[node image upgrade](node-image-upgrade). These upgrades deploy new nodes with the latest Window Server 2019 and Windows Server 2022 base node image and security patches.[AKS Image Cleaner](image-cleaner#limitations)[BYOCNI](use-byo-cni)[Open Service Mesh](open-service-mesh-about)[GPU](use-windows-gpu)[Multi-instance GPU](gpu-multi-instance)[Generation 2 VMs](generation-2-vms)[Custom node config](custom-node-configuration)•

[kubelet](custom-node-configuration#kubelet-configuration): Supported.• OS config: Not supported.

## Next steps

For more information on Windows containers, see the [Windows Server containers FAQ](windows-faq).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay-pod-expand -->

# Expand pod CIDR space in Azure CNI Overlay Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can expand your pod Classless Inter-Domain Routing (CIDR) space on Azure CNI Overlay clusters in Azure Kubernetes Service with Linux nodes only. The operation uses the [ az aks update](/en-us/cli/azure/aks#az_aks_update) command and allows expansions without the need to re-create your AKS cluster.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Requirements and parameters

| Requirement or parameter | Supported versions or values | Description |
|---|---|---|
| Feature flag | `EnableAzureCNIOverlayPodCIDRExpansion` |
This feature flag must be registered in your subscription to enable pod CIDR expansion in Azure CNI Overlay AKS clusters. |
| Azure CLI version | 2.48.0 or later | The Azure CLI version must be 2.48.0 or later to support the pod CIDR expansion feature. |
| Kubernetes version | 1.33 | Pod CIDR expansion is supported only on AKS clusters running Kubernetes version 1.33. |
| Node operating system | Linux | Pod CIDR expansion is supported only on Azure CNI Overlay AKS clusters with Linux nodes. |
| Networking mode | Azure CNI Overlay | Pod CIDR expansion is supported only on AKS clusters that use Azure CNI Overlay networking. |
| Example original pod CIDR | `10.244.0.0/18` |
This is an example of a starting pod CIDR block. |
| Example expanded pod CIDR | `10.244.0.0/16` |
This is an example of a target expanded pod CIDR block. |

## Limitations

- Windows nodes and hybrid node scenarios aren't supported.
- Shrinking or changing the pod CIDR isn't supported.
- Adding a discontinuous pod CIDR isn't supported. The new pod CIDR must be a larger superset that contains the complete original range.
- IPv6 pod CIDR expansion isn't supported.
- Changing multiple pod CIDR blocks via
`--pod-cidrs`

isn't supported. - If an
[Azure availability zone](availability-zones)is down during the expansion operation, new nodes might appear as`unready`

. You can expect these nodes to reconcile after the availability zone is up.

## Prerequisites

- You need an Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Ensure that you meet the requirements listed in the
[Requirements and parameters](#requirements-and-parameters)section.

## Register the `EnableAzureCNIOverlayPodCIDRExpansion`

feature flag

Register the

`EnableAzureCNIOverlayPodCIDRExpansion`

feature flag by using thecommand:`az feature register`

`az feature register --namespace Microsoft.ContainerService --name EnableAzureCNIOverlayPodCIDRExpansion`

Verify successful registration by using the

command. It takes a few minutes for the registration to finish.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableAzureCNIOverlayPodCIDRExpansion"`

After the feature shows

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Update an Azure CNI Overlay AKS cluster to expand the pod CIDR space

Starting from a pod CIDR block of

`10.244.0.0/18`

, you can expand the pod CIDR space by using thecommand. For example:`az aks update`

`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --pod-cidr 10.244.0.0/16`

Note

Although the update operation might successfully finish and show the new pod CIDR in the network profile, be sure to validate the new cluster state through

`NodeNetworkConfig`

(`nnc`

).Verify the state of the upgrade operation by checking

`NodeNetworkConfig`

(`nnc`

) via the`kubectl get nnc`

command. In the output, all node pools should match your new pod CIDR block (for example,`10.244.0.0/16`

).`kubectl get nnc -A -o jsonpath='{range .items[*]}{.metadata.name}{" "}{.status.networkContainers[0].subnetAddressSpace}{"\n"}{end}'`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:
