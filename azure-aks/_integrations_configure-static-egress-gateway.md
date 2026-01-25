---
merged_at: 2026-01-25T12:25:33.914525
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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
