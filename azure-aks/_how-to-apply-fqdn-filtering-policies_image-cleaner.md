---
merged_at: 2026-01-25T12:25:33.948290
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: how-to-apply-fqdn-filtering-policies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-fqdn-filtering-policies -->

# Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Advanced Container Networking Services with Container Network Security feature in AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you can't use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempt to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods might exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP, HTTPS, Kafka, and gRPC) will be blocked.
- Alpine-based container images might encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

```
rules:
dns:
- matchPattern: "*.example.com"
- matchPattern: "*.example.com.*.*"
- matchPattern: "*.example.com.*.*.*"
- matchPattern: "*.example.com.*.*.*.*"
- matchPattern: "*.example.com.*.*.*.*.*"
- toFQDNs:
- matchPattern: "*.example.com"
```


### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--network-plugin azure \
--network-dataplane cilium \
--node-count 2 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Test connectivity with a policy

This section demonstrates how to observe a policy being enforced through the Cilium Agent. A DNS request is made to an allowed FQDN and another case where it's blocked.

Create a file named `demo-policy.yaml`

and paste the following YAML manifest:

Note

The field `spec.egress.toPorts.rules.dns.matchPattern`

is **mandatory** when using to FQDNs in a policy. This section tells Cilium to inspect DNS queries and match them against specified patterns. Without this section, Cilium only allows the DNS traffic and not inspect its contents to learn which IPs are associated with the FQDNs. As a result, connections to those IPs (i.e., non-DNS traffic) are blocked because Cilium can't associate them with the allowed domain.

Make sure to check the [limitations](#limitations) section first.

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: "allow-bing-fqdn"
spec:
endpointSelector:
matchLabels:
app: demo-container
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


Specify the name of your YAML manifest and apply it by using [kubectl apply][kubectl-apply]:

```
kubectl create ns demo
kubectl apply -f demo-policy.yaml -n demo
```


### Create a demo pod

Create a `client`

pod running Bash:

```
kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.43 --labels="app=demo-container" --command -- bash
```


A shell with utilities for testing FQDN should open with the following output:

```
If you don't see a command prompt, try pressing enter.
bash-5.0#
```


In a separate window, run the following command to get the node of the running pod.

```
kubectl get po -n demo --sort-by="{spec.nodeName}" -o wide
```


The output should look similar to the following example:

```
NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES
client 1/1 Running 0 5m50s 192.168.0.139 aks-nodepool1-22058664-vmss000001 <none> <none>
```


The pod is running on a node named `aks-nodepool1-22058664-vmss000001`

. Obtain the Cilium Agent instance running on that node:

```
kubectl get po -n kube-system -o wide --field-selector spec.nodeName="aks-nodepool1-22058664-vmss000001" | grep "cilium"
```


The expected `cilium-s4x24`

should be in the output.

```
cilium-s4x24 1/1 Running 0 47m 10.224.0.4 aks-nodepool1-22058664-vmss000001 <none> <none>
```


### Inspect a Cilium Agent

Use the `cilium`

CLI to monitor traffic being blocked.

```
kubectl exec -it -n kube-system cilium-s4x24 -- sh
```


```
Defaulted container "cilium-agent" out of: cilium-agent, install-cni-binaries (init), mount-cgroup (init), apply-sysctl-overwrites (init), mount-bpf-fs (init), clean-cilium-state (init), block-wireserver (init)
#
```


Inside this shell, run `cilium monitor -t drop`

:

```
Listening for events on 2 CPUs with 64x4096 of shared memory
Press Ctrl-C to quit
time="2024-10-08T17:48:27Z" level=info msg="Initializing dissection cache..." subsys=monitor
```


### Verify policy

From the first shell, create a request to the allowed FQDN, `*.bing.com`

, as specified by the policy. This request should succeed and allowed by the agent.

```
./agnhost connect www.bing.com:80
```


Then create another request to an FQDN expected to be blocked:

```
./agnhost connect www.example.com:80
```


Cilium Agent blocked the request with the output:

```
xx drop (Policy denied) flow 0xfddd76f6 to endpoint 0, ifindex 29, file bpf_lxc.c:1274, , identity 48447->world: 192.168.0.149:45830 -> 93.184.215.14:80 tcp SYN
```


### Supported by CiliumClusterwideNetworkPolicy(CCNP)

`CiliumClusterwideNetworkPolicy`

supports FQDN filtering.

Note

[Namespace specific information](https://docs.cilium.io/en/latest/security/policy/kubernetes/#namespace-specific-information) such as `io.kubernetes.pod.namespace`

is only supported in cluster-wide policies.

```
apiVersion: cilium.io/v2
kind: CiliumClusterwideNetworkPolicy
metadata:
name: allow-bing-fqdn
spec:
endpointSelector: {} # Applies to all pods in the cluster
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable security features with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).


---

<!-- DOCUMENTO FUSIONADO: image-cleaner.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/image-cleaner -->

# Use Image Cleaner to clean up vulnerable stale images on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

It's common to use pipelines to build and deploy images on Azure Kubernetes Service (AKS) clusters. While great for image creation, this process often doesn't account for the stale images left behind and can lead to image bloat on cluster nodes. These images might contain vulnerabilities, which might create security issues. To remove security risks in your clusters, you can clean these unreferenced images. Manually cleaning images can be time intensive. Image Cleaner performs automatic image identification and removal, which mitigates the risk of stale images and reduces the time required to clean them up.

Note

Image Cleaner is a feature based on [Eraser](https://eraser-dev.github.io/eraser).
On an AKS cluster, the feature name and property name is `Image Cleaner`

, while the relevant Image Cleaner pods' names contain `Eraser`

.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.49.0 or later. Run
`az --version`

to find your version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

Image Cleaner doesn't yet support Windows node pools or AKS virtual nodes.

## How Image Cleaner works

After you enable Image Cleaner, there will be a controller manager pod named `eraser-controller-manager`

deployed to your cluster.


With Image Cleaner, you can choose between manual and automatic mode and the following configuration options:

## Configuration options

| Name | Description | Required |
|---|---|---|
`--enable-image-cleaner` |
Enable the Image Cleaner feature for an AKS cluster | Yes, unless disable is specified |
`--disable-image-cleaner` |
Disable the Image Cleaner feature for an AKS cluster | Yes, unless enable is specified |
`--image-cleaner-interval-hours` |
This parameter determines the interval time (in hours) Image Cleaner uses to run. The default value for Azure CLI is one week, the minimum value is 24 hours and the maximum is three months. | Not required for Azure CLI, required for ARM template or other clients |

### Automatic mode

Once `eraser-controller-manager`

is deployed, the following steps will be taken automatically:

- It immediately starts the cleanup process and creates
`eraser-aks-xxxxx`

worker pods for each node. - There are three containers in each worker pod:
- A
**collector**, which collects unused images. - A
**trivy-scanner**, which leverages[trivy](https://github.com/aquasecurity/trivy)to scan image vulnerabilities. - A
**remover**, which removes unused images with vulnerabilities.

- A
- After the cleanup process completes, the worker pod is deleted and the next scheduled cleanup happens according to the
`--image-cleaner-interval-hours`

you define.

### Manual mode

You can manually trigger the cleanup by defining a CRD object,`ImageList`

. This triggers the `eraser-contoller-manager`

to create `eraser-aks-xxxxx`

worker pods for each node and complete the manual removal process.

Note

After disabling Image Cleaner, the old configuration still exists. This means if you enable the feature again without explicitly passing configuration, the existing value is used instead of the default.

## Enable Image Cleaner on your AKS cluster

### Enable Image Cleaner on a new cluster

Enable Image Cleaner on a new AKS cluster using the

command with the`az aks create`

`--enable-image-cleaner`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --generate-ssh-keys`


### Enable Image Cleaner on an existing cluster

Enable Image Cleaner on an existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner`


### Update the Image Cleaner interval on a new or existing cluster

Update the Image Cleaner interval on a new or existing AKS cluster using the

`--image-cleaner-interval-hours`

parameter.`# Create a new cluster with specifying the interval az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48 \ --generate-ssh-keys # Update the interval on an existing cluster az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48`


## Manually remove images using Image Cleaner

Important

The `name`

must be set to `imagelist`

.

Manually remove an image using the following

`kubectl apply`

command. This example removes the`docker.io/library/alpine:3.7.3`

image if it's unused.`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


The manual cleanup is a one-time operation and is only triggered when a new `imagelist`

is created or changes are made to the existing `imagelist`

. After the image is deleted, the `imagelist`

won't be deleted automatically.

If you need to trigger another manual cleanup, you have to create a new `imagelist`

or make changes to an existing one. If you want to remove the same image again, you need to create a new `imagelist`

.

### Delete an existing ImageList and create a new one

Delete the old

`imagelist`

using the`kubectl delete`

command.`kubectl delete ImageList imagelist`

Create a new

`imagelist`

with the same image name. The following example uses the same image as the[previous example](#manually-remove-images-using-image-cleaner).`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


### Modify an existing ImageList

Modify the existing

`imagelist`

using the`kubectl edit`

command.`kubectl edit ImageList imagelist # Add a new image to the list apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: docker.io/library/python:alpine3.18`


When using manual mode, the `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion.

## Image exclusion list

Images specified in the exclusion list aren't removed from the cluster. Image Cleaner supports system and user-defined exclusion lists. It's not supported to edit the system exclusion list.

### Check the system exclusion list

Check the system exclusion list using the following

`kubectl get`

command.`kubectl get -n kube-system configmap eraser-system-exclusion -o yaml`


### Create a user-defined exclusion list

Create a sample JSON file to contain excluded images.

`cat > sample.json <<EOF {"excluded": ["excluded-image-name"]} EOF`

Create a

`configmap`

using the sample JSON file using the following`kubectl create`

and`kubectl label`

command.`kubectl create configmap excluded --from-file=sample.json --namespace=kube-system kubectl label configmap excluded eraser.sh/exclude.list=true -n kube-system`


## Disable Image Cleaner

Disable Image Cleaner on your cluster using the

command with the`az aks update`

`--disable-image-cleaner`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --disable-image-cleaner`


## FAQ

### How can I check which version Image Cleaner is using?

```
kubectl describe configmap -n kube-system eraser-manager-config | grep tag -C 3
```


### Does Image Cleaner support other vulnerability scanners besides trivy-scanner?

No.

### Can I specify vulnerability levels for images to clean?

No. The default settings for vulnerability levels include:

`LOW`

,`MEDIUM`

,`HIGH`

, and`CRITICAL`


You can't customize the default settings.

### How to review images were cleaned up by Image Cleaner?

Image logs are stored in the `eraser-aks-xxxxx`

worker pod. When `eraser-aks-xxxxx`

is alive, you can run the following commands to view deletion logs:

```
kubectl logs -n kube-system <worker-pod-name> -c collector
kubectl logs -n kube-system <worker-pod-name> -c trivy-scanner
kubectl logs -n kube-system <worker-pod-name> -c remover
```


The `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion. You can follow these steps to enable the [Azure Monitor add-on](monitor-aks) and use the Container Insights pod log table. After that, historical logs will be stored and you can review them even `eraser-aks-xxxxx`

is deleted.

Ensure Azure Monitoring is enabled on your cluster. For detailed steps, see

[Enable Container Insights on AKS clusters](/en-us/azure/azure-monitor/containers/container-insights-enable-aks#existing-aks-cluster).Logs for the containers running in

`kube-system`

namespace are not collected by default. Remove the`kube-system`

namespace from`exclude_namespaces`

in the configmap and apply the config map to enable collection of these logs. See[Configure Container insights data collection](/en-us/azure/azure-monitor/containers/container-insights-data-collection-configure#configure-data-collection-using-configmap)for details.Get the Log Analytics resource ID using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myManagedCluster`

After a few minutes, the command returns JSON-formatted information about the solution, including the workspace resource ID:

`"addonProfiles": { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/<WorkspaceSubscription>/resourceGroups/<DefaultWorkspaceRG>/providers/Microsoft.OperationalInsights/workspaces/<defaultWorkspaceName>" }, "enabled": true } }`

In the Azure portal, search for the workspace resource ID, then select

**Logs**.Copy one of the following queries and paste into the query window.

Use the following query if your cluster is using the

[ContainerLogV2 schema](/en-us/azure/azure-monitor/containers/container-insights-logs-schema). If you're still using`ContainerLog`

, you should upgrade to ContainerlogV2.`ContainerLogV2 | where PodName startswith "eraser-aks-" and PodNamespace == "kube-system" | project TimeGenerated, PodName, LogMessage, LogSource`

If you want continue to use

`ContainerLog`

, use the following query instead:`let startTimestamp = ago(1h); KubePodInventory | where TimeGenerated > startTimestamp | project ContainerID, PodName=Name, Namespace | where PodName startswith "eraser-aks-" and Namespace == "kube-system" | distinct ContainerID, PodName | join ( ContainerLog | where TimeGenerated > startTimestamp ) on ContainerID // at this point before the next pipe, columns from both tables are available to be "projected". Due to both // tables having a "Name" column, we assign an alias as PodName to one column which we actually want | project TimeGenerated, PodName, LogEntry, LogEntrySource | summarize by TimeGenerated, LogEntry | order by TimeGenerated desc`


Select

**Run**. Any deleted image logs appear in the**Results**area.
