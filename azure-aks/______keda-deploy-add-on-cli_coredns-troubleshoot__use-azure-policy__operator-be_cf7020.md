---
merged_at: 2026-02-04T00:17:48.876884
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-cli -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using the Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to install the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using the Azure CLI.

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

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

## Install the KEDA add-on with Azure CLI

To install the KEDA add-on, use `--enable-keda`

when creating or updating a cluster.

## Enable the KEDA add-on on your AKS cluster

Note

While KEDA provides various customization options, the KEDA add-on currently provides basic common configuration.

If you require custom configurations, you can manually edit the KEDA YAML files to customize the installation. **Azure doesn't offer support for custom configurations**.

### Create a new AKS cluster with KEDA add-on enabled

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster using the

command and enable the KEDA add-on using the`az aks create`

`--enable-keda`

flag.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda \ --generate-ssh-keys`


### Enable the KEDA add-on on an existing AKS cluster

Update an existing cluster using the

command and enable the KEDA add-on using the`az aks update`

`--enable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the KEDA add-on is installed on your cluster

Verify the KEDA add-on is installed on your cluster using the

command and set the`az aks show`

`--query`

parameter to`workloadAutoScalerProfile.keda.enabled`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query "workloadAutoScalerProfile.keda.enabled"`

The following example output shows the KEDA add-on is installed on the cluster:

`true`


## Verify KEDA is running on your cluster

Verify the KEDA add-on is running on your cluster using the

`kubectl get pods`

command.`kubectl get pods -n kube-system`

The following example output shows the KEDA operator, admissions hook, and metrics API server are installed on the cluster:

`keda-admission-webhooks-**********-2n9zl 1/1 Running 0 3d18h keda-admission-webhooks-**********-69dkg 1/1 Running 0 3d18h keda-operator-*********-4hb5n 1/1 Running 0 3d18h keda-operator-*********-pckpx 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-gqg4s 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-trfcb 1/1 Running 0 3d18h`


## Verify the KEDA version on your cluster

To verify the version of your KEDA, use `kubectl get crd/scaledobjects.keda.sh -o yaml `

. For example:

```
kubectl get crd/scaledobjects.keda.sh -o yaml
```


The following example output shows the configuration of KEDA in the `app.kubernetes.io/version`

label:

```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
annotations:
controller-gen.kubebuilder.io/version: v0.9.0
meta.helm.sh/release-name: aks-managed-keda
meta.helm.sh/release-namespace: kube-system
creationTimestamp: "2023-08-09T15:58:56Z"
generation: 1
labels:
app.kubernetes.io/component: operator
app.kubernetes.io/managed-by: Helm
app.kubernetes.io/name: keda-operator
app.kubernetes.io/part-of: keda-operator
app.kubernetes.io/version: 2.10.1
helm.toolkit.fluxcd.io/name: keda-adapter-helmrelease
helm.toolkit.fluxcd.io/namespace: 64d3b6fd3365790001260647
name: scaledobjects.keda.sh
resourceVersion: "1421"
uid: 29109c8c-638a-4bf5-ac1b-c28ad9aa11fa
spec:
conversion:
strategy: None
group: keda.sh
names:
kind: ScaledObject
listKind: ScaledObjectList
plural: scaledobjects
shortNames:
- so
singular: scaledobject
scope: Namespaced
# Redacted due to length
```


## Disable the KEDA add-on on your AKS cluster

Disable the KEDA add-on on your cluster using the

command with the`az aks update`

`--disable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-keda`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster using the Azure CLI.

With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-troubleshoot -->

# Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides troubleshooting guidance for various CoreDNS issues on Azure Kubernetes Service (AKS).

## Debug DNS resolution issues

For general CoreDNS troubleshooting steps, such as checking the endpoints or resolution, see [Debugging DNS resolution](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/).

## Troubleshoot CoreDNS pod traffic imbalance

You might see one or two CoreDNS pods showing significantly higher CPU usage and handling more DNS queries than others, even with multiple CoreDNS pods running in your AKS cluster. This is a [known issue](https://github.com/kubernetes/kubernetes/issues/76517#issuecomment-490731578) in Kubernetes and can lead to one of the CoreDNS pods being overloaded and crashing.

This uneven distribution of DNS queries is primarily caused by User Datagram Protocol (UDP) load balancing limitations in Kubernetes. The platform uses a five-tuple hash (source IP, source port, destination IP, destination port, protocol) to distribute UDP traffic, so if an application reuses the same source port for DNS queries, all queries from that client are routed to the same CoreDNS pod. This distribution method can result in a single pod handling a disproportionate amount of traffic. Additionally, some applications use connection pooling and reuse DNS connections. This behavior can further concentrate DNS queries on a single CoreDNS pod, increasing the imbalance and the risk of overloading and potential crashes.

The following sections help you troubleshoot and mitigate this issue.

### Enable DNS query logging

Enable DNS query logging to capture required DNS query logs from CoreDNS pods.

Add the following configuration to your

`coredns-custom`

ConfigMap:`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: log.override: | # You can select any name here, but it must end with the .override file extension log`

Apply the ConfigMap changes using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`

View the CoreDNS debug logging using the

`kubectl logs`

command.`kubectl logs --namespace kube-system -l k8s-app=kube-dns`


### Check your CoreDNS pod traffic distribution

Get the names of all CoreDNS pods in your cluster using the

command.`kubectl get pods`

`kubectl get pods --namespace kube-system -l k8s-app=kube-dns`

Review the logs for each CoreDNS pod to analyze DNS query patterns using the

command. Repeat this command for all CoreDNS pods, replacing`kubectl logs`

`<coredns-pod-x>`

with the actual pod names.`kubectl logs --namespace kube-system <coredns-pod-x>`

In the outputs, look for repeated client IP addresses and ports that appear only in the logs of a single CoreDNS pod. This indicates that DNS queries from certain clients aren't being distributed evenly.

Example log output:

`[INFO] 10.244.0.247:5556 - 42621 "A IN myservice.default.svc.cluster.local. udp 28" NOERROR qr,aa,rd 106 0.000141s`

In this example log entry:

`10.244.0.247`

is the client IP address making the DNS query.`5556`

is the client source port.`42621`

is the query ID.

**If you see the same client IP and port repeatedly in only one pod's logs, this confirms a traffic imbalance**.

### Mitigate CoreDNS pod traffic imbalance

If you notice an imbalance, your application could be reusing UDP source ports or pooling their connections. Based on the root cause, you can take the following mitigation actions:

**Caused by UDP source port reuse**: UDP source port reuse occurs when a client application sends multiple DNS queries from the same UDP source port. If this is the issue, update your applications or DNS clients to randomize source ports for each DNS query, which helps distribute requests more evenly across pods.**Caused by connection pooling**: Connection pools are mechanisms applications use to reuse existing network connections instead of creating a new connection for each request. While this improves efficiency, it can result in all DNS queries from an application being sent over the same connection, and thus routed to the same CoreDNS pod. To mitigate this, adjust your application's DNS connection handling by reducing connection Time to Live (TTL) or randomizing connection creation, ensuring queries aren't concentrated on a single CoreDNS pod.

These changes can help achieve a more balanced DNS query distribution and reduce the risk of overloading individual pods.

## Troubleshoot invalid search domain completions for internal.cloudapp.net and reddog.microsoft.com

Azure DNS configures a default search domain of `<VNET_ID>.<REGION>.internal.cloudapp.net`

in virtual networks (VNets) using Azure DNS and a nonfunctional stub `reddog.microsoft.com`

in VNets using custom DNS servers. For more information, see the [Name resolution for resources documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

Kubernetes configures pod DNS settings with `ndots: 5`

to properly support cluster service hostname resolution. These two configurations combine to result in invalid search domain completion queries that never succeed being sent to upstream name servers while the system processes through the domain search list. These invalid queries cause name resolution delays and can place extra load on upstream DNS servers.

As of the *v20241025* AKS release, AKS configures CoreDNS to respond with `NXDOMAIN`

in the following cases in order to prevent these invalid search domain completion queries from being forwarded to upstream DNS:

- Any query for the root domain or a subdomain of
`reddog.microsoft.com`

. - Any query for a subdomain of
`internal.cloudapp.net`

that has seven or more labels in the domain name.- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends
`aks12345.myvnetid.myregion.internal.cloudapp.net`

(*six*labels) to Azure DNS, but rejects`mcr.microsoft.com.myvnetid.myregion.internal.cloudapp.net`

(*eight*labels).

- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends

This block is implemented in the default server block in the CoreFile for the cluster. If needed, you can disable this rejection configuration by creating custom server blocks for the appropriate domain with a forward plugin enabled:

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to update the IP addresses and hostnames with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom # This is the name of the ConfigMap you can overwrite with your changes namespace: kube-system data: override-block.server: | internal.cloudapp.net:53 { errors cache 30 forward . /etc/resolv.conf } reddog.microsoft.com:53 { errors cache 30 forward . /etc/resolv.conf }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Troubleshoot CoreDNS autoscaling issues

To troubleshoot CoreDNS autoscaling issues, see [Autoscaling CoreDNS in Azure Kubernetes Service (AKS)](coredns-autoscale).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-policy -->

# Secure your Azure Kubernetes Service (AKS) clusters with Azure Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can apply and enforce built-in security policies on your Azure Kubernetes Service (AKS) clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives (sometimes called policysets) to your cluster. See [Azure Policy built-in definitions for AKS](policy-reference) for a complete list of AKS policy and initiative definitions.

This article shows you how to apply policy definitions to your cluster and verify those assignments are being enforced.

## Prerequisites

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the
[Azure Policy add-on for AKS installed on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).

## Assign a built-in policy definition or initiative

You can apply a policy definition or initiative in the Azure portal using the following steps:

- Navigate to the Azure Policy service in Azure portal called
**Policy**. - In the left pane of the Azure Policy page, select
**Definitions**. - Under
**Categories**, select`Kubernetes`

. - Choose the policy definition or initiative you want to apply. For this example, select the
**Kubernetes cluster pod security baseline standards for Linux-based workloads**initiative. - Select
**Assign**. - Set the
**Scope**to the resource group of the AKS cluster with the Azure Policy add-on enabled. - Select the
**Parameters**page and update the**Effect**from`audit`

to`deny`

to block new deployments violating the baseline initiative. You can also add extra namespaces to exclude from evaluation. For this example, keep the default values. - Select
**Review + create**>**Create**to submit the policy assignment.

## Create and assign a custom policy definition

Custom policies allow you to define rules for using Azure. For example, you can enforce the following types of rules:

- Security practices
- Cost management
- Organization-specific rules (like naming or locations)

Before creating a custom policy, check the [list of common patterns and samples](/en-us/azure/governance/policy/samples/) to see if your case is already covered.

Custom policy definitions are written in JSON. To learn more about creating a custom policy, see [Azure Policy definition structure](/en-us/azure/governance/policy/concepts/definition-structure) and [Create a custom policy definition](/en-us/azure/governance/policy/tutorials/create-custom-policy-definition).

Note

Azure Policy now utilizes a new property known as *templateInfo* that allows you to define the source type for the constraint template. When you define *templateInfo* in policy definitions, you don’t have to define *constraintTemplate* or *constraint* properties. You still need to define *apiGroups* and *kinds*. For more information on this, see [Understanding Azure Policy effects](/en-us/azure/governance/policy/concepts/effects#audit-properties).

Once you create your custom policy definition, see [Assign a policy definition](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition) for a step-by-step walkthrough of assigning the policy to your Kubernetes cluster.

## Validate an Azure Policy is running

Confirm the policy assignments are applied to your cluster using the following

`kubectl get`

command.`kubectl get constrainttemplates`

Note

Policy assignments can take

[up to 20 minutes to sync](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition)into each cluster.Your output should be similar to the following example output:

`NAME AGE k8sazureallowedcapabilities 23m k8sazureallowedusersgroups 23m k8sazureblockhostnamespace 23m k8sazurecontainerallowedimages 23m k8sazurecontainerallowedports 23m k8sazurecontainerlimits 23m k8sazurecontainernoprivilege 23m k8sazurecontainernoprivilegeescalation 23m k8sazureenforceapparmor 23m k8sazurehostfilesystem 23m k8sazurehostnetworkingports 23m k8sazurereadonlyrootfilesystem 23m k8sazureserviceallowedports 23m`


### Validate rejection of a privileged pod

Let's first test what happens when you schedule a pod with the security context of `privileged: true`

. This security context escalates the pod's privileges. The initiative disallows privileged pods, so the request is denied, which results in the deployment being rejected.

Create a file named

`nginx-privileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-privileged spec: containers: - name: nginx-privileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine securityContext: privileged: true`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-privileged.yaml`

As expected, the pod fails to be scheduled, as shown in the following example output:

`Error from server ([denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}): error when creating "privileged.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}`

The pod doesn't reach the scheduling stage, so there are no resources to delete before you move on.


### Test creation of an unprivileged pod

In the previous example, the container image automatically tried to use root to bind NGINX to port 80. The policy initiative denies this request, so the pod fails to start. Now, let's try running that same NGINX pod without privileged access.

Create a file named

`nginx-unprivileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-unprivileged spec: containers: - name: nginx-unprivileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-unprivileged.yaml`

Check the status of the pod using the

command.`kubectl get pods`

`kubectl get pods`

Your output should be similar to the following example output, which shows the pod is successfully scheduled and has a status of

*Running*:`NAME READY STATUS RESTARTS AGE nginx-unprivileged 1/1 Running 0 18s`

This example shows the baseline initiative affecting only the deployments that violate policies in the collection. Allowed deployments continue to function.

Delete the NGINX unprivileged pod using the

command and specify the name of your YAML manifest.`kubectl delete`

`kubectl delete -f nginx-unprivileged.yaml`


## Disable a policy or initiative

You can remove the baseline initiative in the Azure portal using the following steps:

- Navigate to the
**Policy**pane on the Azure portal. - Select
**Assignments**. - Select the
**...**button next to the**Kubernetes cluster pod security baseline standards for Linux-based workload**initiative. - Select
**Delete assignment**.

## Next steps

For more information about how Azure Policy works, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-container-image-management -->

# Best practices for container image management and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container and container image security is a major priority when developing and running applications in Azure Kubernetes Service (AKS). Containers with outdated base images or unpatched application runtimes introduce security risks and possible attack vectors. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. The earlier you catch the vulnerability or outdated base image, the more secure your application is.

In this article, *"containers"* refers to both the container images stored in a container registry and running containers.

This article focuses on how to secure your containers in AKS. You learn how to:

- Scan for and remediate image vulnerabilities.
- Automatically trigger and redeploy container images when a base image is updated.

- You can read the best practices for
[cluster security](operator-best-practices-cluster-security)and[pod security](developer-best-practices-pod-security). - You can use
[Container security in Defender for Cloud](/en-us/azure/security-center/container-security)to help scan your containers for vulnerabilities.[Azure Container Registry integration](/en-us/azure/security-center/defender-for-container-registries-introduction)with Defender for Cloud helps protect your images and registry from vulnerabilities.

## Secure the images and runtime


Best practice guidance

- Scan your container images for vulnerabilities.
- Only deploy validated images.
- Regularly update the base images and application runtime.
- Redeploy workloads in the AKS cluster.

When adopting container-based workloads, you want to verify the security of images and runtime used to build your own applications. To help avoid introducing security vulnerabilities into your deployments, you can use the following best practices:

- Include in your deployment workflow a process to scan container images using tools, such as
[Twistlock](https://www.twistlock.com/)or[Aqua](https://www.aquasec.com/). - Only allow verified images to be deployed.

For example, you can use a continuous integration and continuous deployment (CI/CD) pipeline to automate the image scans, verification, and deployments. Azure Container Registry includes these vulnerabilities scanning capabilities.

## Automatically build new images on base image update


Best practice guidanceAs you use base images for application images, use automation to build new images when the base image is updated. Since updated base images typically include security fixes, update any downstream application container images.


Each time a base image is updated, you should also update any downstream container images. Integrate this build process into validation and deployment pipelines such as [Azure Pipelines](/en-us/azure/devops/pipelines/) or Jenkins. These pipelines ensure your applications continue to run on the updated based images. Once your application container images are validated, you can then update AKS deployments to run the latest secure images.

Azure Container Registry Tasks can also automatically update container images when the base image is updated. With this feature, you build a few base images and keep them updated with bug and security fixes.

For more information about base image updates, see [Automate image builds on base image update with Azure Container Registry Tasks](/en-us/azure/container-registry/container-registry-tutorial-base-image-update).

## Next steps

This article focused on how to secure your containers. To implement some of these areas, see the following article:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/scale-cluster -->

# Manually scale the node count in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If the resource needs of your applications change, your cluster performance may be impacted due to low capacity on CPU, memory, PID space, or disk sizes. To address these changes, you can manually scale your AKS cluster to run a different number of nodes. When you scale in, nodes are carefully [cordoned and drained](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) to minimize disruption to running applications. When you scale out, AKS waits until nodes are marked **Ready** by the Kubernetes cluster before pods are scheduled on them.

This article describes how to manually increase or decrease the number of nodes in an AKS cluster.

## Before you begin

Review the

[AKS service quotas and limits](quotas-skus-regions#service-quotas-and-limits)to verify your cluster can scale to your desired number of nodes.The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-11 characters.
- For Windows node pools, the length must be between 1-6 characters.


## Scale the cluster nodes

Important

Removing nodes from a node pool using the kubectl command isn't supported. Doing so can create scaling issues with your AKS cluster.

Get the

*name*of your node pool using thecommand. The following example gets the node pool name for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks show --resource-group myResourceGroup --name myAKSCluster --query agentPoolProfiles`

The following example output shows that the

*name*is*nodepool1*:`[ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2" } ]`

Scale the cluster nodes using the

command. The following example scales a cluster named`az aks scale`

*myAKSCluster*to a single node. Provide your own`--nodepool-name`

from the previous command, such as*nodepool1*:`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 1 --nodepool-name <your node pool name>`

The following example output shows the cluster successfully scaled to one node, as shown in the

*agentPoolProfiles*section:`{ "aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2", "vnetSubnetId": null } ], [...] }`


## Scale `User`

node pools to 0

Unlike `System`

node pools that always require running nodes, `User`

node pools allow you to scale to 0. To learn more on the differences between system and user node pools, see [System and user node pools](use-system-pools).

Important

You can't scale a user node pool with the cluster autoscaler enabled to 0 nodes. To scale a user node pool to 0 nodes, you must disable the cluster autoscaler first. For more information, see [Disable the cluster autoscaler on a node pool](cluster-autoscaler#disable-the-cluster-autoscaler-on-a-node-pool).

To scale a user pool to 0, you can use the

[az aks nodepool scale](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-scale)in alternative to the above`az aks scale`

command, and set`0`

as your node count.`az aks nodepool scale --name <your node pool name> --cluster-name myAKSCluster --resource-group myResourceGroup --node-count 0`

You can also autoscale

`User`

node pools to zero nodes, by setting the`--min-count`

parameter of the[Cluster Autoscaler](cluster-autoscaler)to`0`

.

## Next steps

In this article, you manually scaled an AKS cluster to increase or decrease the number of nodes. You can also use the [cluster autoscaler](cluster-autoscaler) to automatically scale your cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-aks-scheduler -->

# Configure advanced scheduler profiles on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy example scheduler profiles in Azure Kubernetes Service (AKS) to configure advanced scheduling behavior using in-tree scheduling plugins. This guide also explains how to verify the successful application of custom scheduler profiles targeting specific node pools or the entire AKS cluster.

## Limitations

- AKS currently doesn't manage the deployment of third-party schedulers or out-of-tree scheduling plugins.
- AKS doesn't support in-tree scheduling plugins targeting the
`aks-system`

scheduler. This restriction is in place to help prevent unexpected changes to AKS add-ons enabled on your cluster. Additionally, you can't define a`profile`

called`aks-system`

.

## Prerequisites

- The Azure CLI version
`2.76.0`

or later. Run`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version
`1.33`

or later running on your AKS cluster. - The
version`aks-preview`

Azure CLI extension`18.0.0b27`

or later. [Register the](#register-the-user-defined-scheduler-configuration-preview-feature-flag)in your Azure subscription.`UserDefinedSchedulerConfigurationPreview`

feature flag- Review the
[supported advanced scheduling concepts](concepts-scheduler-configuration)and in-tree scheduling plugins on AKS.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the User Defined Scheduler Configuration Preview feature flag

Register the

`UserDefinedSchedulerConfigurationPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "UserDefinedSchedulerConfigurationPreview"`

It takes a few minutes for the status to show

*Registered*.When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable scheduler profile configuration on an AKS cluster

You can enable schedule profile configuration on a new or existing AKS cluster.

Create an AKS cluster with scheduler profile configuration enabled using the

command with the`az aks create`

`--enable-upstream-kubescheduler-user-configuration`

flag.`# Set environment variables export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<aks-cluster-name> # Create an AKS cluster with schedule profile configuration enabled az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-upstream-kubescheduler-user-configuration \ --generate-ssh-keys`

Once the creation process completes, connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify installation of the scheduler controller

After enabling the feature on your AKS cluster, verify the custom resource definition (CRD) of the scheduler controller was successfully installed using the

`kubectl get`

command.`kubectl get crd schedulerconfigurations.aks.azure.com`

Note

This command won't succeed if the feature wasn't successfully enabled in the

[previous section](#enable-scheduler-profile-configuration-on-an-aks-cluster).

## Configure node bin-packing

Node bin-packing is a scheduling strategy that maximizes resource utilization by increasing pod density on nodes, within the set configuration. This strategy helps improve cluster efficiency by minimizing wasted resources and lowering the operational cost of maintaining idle or underutilized nodes.

In this example, the configured scheduler prioritizes scheduling pods on nodes with high CPU usage. Explicitly, this configuration avoids underutilizing nodes that still have free resources and helps to make better use of the resources already allocated to nodes. The CRD must be named `upstream`

.

Create a file named

`bin-pack-cpu-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: node-binpacking-cpu-scheduler pluginConfig: - name: NodeResourcesFit args: scoringStrategy: type: MostAllocated resources: - name: cpu weight: 1`

`NodeResourcesFit`

ensures that the scheduler checks if a node has enough resources to run the pod.`scoringStrategy: MostAllocated`

tells the scheduler to prefer nodes with high CPU resource usage. This helps achieve**better resource utilization**by placing new pods on nodes that are already "highly used".`Resources`

specifies that`CPU`

is the primary resource being considered for scoring, and with a weight of`1`

, CPU usage is prioritized with a relatively equal level of importance in the scheduling decision.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f bin-pack-cpu-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: node-binpacking-cpu-scheduler ... ...`


## Configure pod topology spread

Pod topology spread is a scheduling strategy that seeks to distribute pods evenly across failure domains (such as availability zones or regions) to ensure high availability and fault tolerance in the event of zone or node failures. This strategy helps prevent the risk of all replicas of a pod being placed in the same failure domain. For more configuration guidance, see the [Kubernetes Pod Topology Spread Constraints documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/). The CRD must be named `upstream`

.

Create a file named

`pod-topology-spreader-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: pod-distribution-scheduler pluginConfig: - name: PodTopologySpread args: apiVersion: kubescheduler.config.k8s.io/v1 kind: PodTopologySpreadArgs defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: ScheduleAnyway`

`PodTopologySpread`

plugin instructs the scheduler to try and distribute pods as evenly as possible across availability zones.`whenUnsatisfiable: ScheduleAnyway`

specifies schedule to schedule pods despite the inability to meet the topology constraints. This avoids pod scheduling failures when exact distribution isn't feasible.`List`

type applies the default constraints as a list of rules. The scheduler uses the rules in the order they're defined, and they apply to all pods that don’t specify custom topology spread constraints.`maxSkew: 1`

means the number of pods can differ by at most*1*between any two availability zones.`topologyKey: topology.kubernetes.io/zone`

indicates that the scheduler should spread pods across availability zones.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f pod-topology-spreader-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: pod-distribution-scheduler ... ...`


## Assign a scheduler profile to an entire AKS cluster

In your scheduler profile configuration, update the

`schedulerName`

field as follows:`... ... - schedulerName: default_scheduler ... ...`

Reapply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`

Now, this configuration will become the

**default**scheduling operation for your entire AKS cluster.

## Configure multiple scheduler profiles

You can customize the upstream scheduler with multiple profiles and customize each profile with multiple plugins while using the same configuration file. As a reminder, the CRD must be named `upstream`

and user-configured fields include `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, and `profiles`

.

In the following example, we create two scheduling profiles called **scheduler-one** and **scheduler-two**. The fields `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, apply globally to all profiles defined.

**global parameters**

`percentageOfNodesToScore`

specifies the percentage of cluster nodes the scheduler evaluates during scoring to balance scheduling accuracy and speed. So**percentageOfNodesToScore: 40**means the scheduler will sample 40% of nodes instead of the entire cluster.`podInitialBackoffSeconds`

defines the initial delay before retrying a failed scheduling attempt to prevent rapid, repeated retries. So**podInitialBackoffSeconds: 1**means the scheduler waits 1 second before the first retry.`podMaxBackoffSeconds`

sets the maximum delay the scheduler will wait between exponential backoff retries for unschedulable pods. So**podMaxBackoffSeconds: 8**means the retry delay will never exceed 8 seconds even as backoff increases.

**scheduler-one** prioritizes placing pods across zones and nodes for balanced distribution with the following settings:

- Enforces strict zonal distribution and
*preferred*node distribution using`PodTopologySpread`

. - Honors hard pod affinity rules and considers the soft affinity rules with
`InterPodAffinity`

. *Prefers*nodes in specific zones to reduce cross-zone networking using`NodeAffinity`

.

**scheduler-two** prioritizes placing pods on nodes with available storage, CPU, and memory resources for timely resource-efficient resource usage with the following settings:

- Ensures pods are placed on nodes where PVCs can bind to PVs using
`VolumeBinding`

. - Validates that nodes and volumes satisfy zonal requirements using
`VolumeZone`

to avoid cross-zone storage access. - Prioritizes nodes based on CPU, memory, and ephemeral storage utilization, with
`NodeResourcesFit`

. - Favors nodes that already have the required container images using
`ImageLocality`

.

Note

You might need to adjust zones and other parameters based on your workload type.

Create a file named

`aks-scheduler-customization.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration percentageOfNodesToScore: 40 podInitialBackoffSeconds: 1 podMaxBackoffSeconds: 8 profiles: - schedulerName: scheduler-one plugins: multiPoint: enabled: - name: PodTopologySpread - name: InterPodAffinity - name: NodeAffinity pluginConfig: # PodTopologySpread with strict zonal distribution - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 2 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: ScheduleAnyway - name: InterPodAffinity args: hardPodAffinityWeight: 1 ignorePreferredTermsOfExistingPods: false - name: NodeAffinity args: addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2, westus3-3] - schedulerName: scheduler-two plugins: multiPoint: enabled: - name: VolumeBinding - name: VolumeZone - name: NodeAffinity - name: NodeResourcesFit - name: PodTopologySpread - name: ImageLocality pluginConfig: - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: DoNotSchedule - name: VolumeBinding args: apiVersion: kubescheduler.config.k8s.io/v1 kind: VolumeBindingArgs bindTimeoutSeconds: 300 - name: NodeAffinity args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeAffinityArgs addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2] - name: NodeResourcesFit args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeResourcesFitArgs scoringStrategy: type: MostAllocated resources: - name: cpu weight: 3 - name: memory weight: 1 - name: ephemeral-storage weight: 2`

Apply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`


## Disable an AKS scheduler profile configuration

To disable the AKS scheduler profile configuration and revert to AKS scheduler default configuration on the cluster, first delete the

`schedulerconfiguration`

resource using the`kubectl delete`

command.`kubectl delete schedulerconfiguration upstream || true`

Note

Ensure that the previous step is complete and confirm that the

`schedulerconfiguration`

resource was deleted before proceeding to disable this feature.Disable the feature using the

command with the`az aks update`

`--disable-upstream-kubescheduler-user-configuration`

flag.`az aks update --subscription="${SUBSCRIPTION_ID}" \ --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --disable-upstream-kubescheduler-user-configuration`

Verify the feature is disabled using the

command.`az aks show`

`az aks show --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --query='properties.schedulerProfile'`

Your output should indicate that the feature is no longer enabled on your AKS cluster.


## Frequently asked questions (FAQ)

### What happens if I apply misconfigured scheduler profile to my AKS cluster?

Once you apply a scheduler profile, AKS checks if it contains a valid configuration of plugins and arguments. If the configuration targets a disallowed scheduler or sets the in-tree scheduling plugins improperly, AKS rejects the configuration and reverts to the last known "accepted" scheduler configuration. This check aims to limit impact on new and existing AKS clusters due to scheduler misconfiguration.

### How can I monitor and validate that the scheduler honored my configuration?

There are *three* recommended methods for observing the results of your applied scheduler profile:

- View the AKS
`kube-scheduler`

control plane logs to ensure that the scheduler received the configuration from the CRD. - Run the
`kubectl get schedulerconfiguration`

command. The output displays the status of the`configuration: pending`

during the rollout and`Succeeded`

or`Failed`

after the configuration is accepted or rejected by the scheduler. - Run the
`kubectl describe schedulerconfiguration`

command. The output displays a more detailed state of the scheduler, including any error during the reconciliation, and the current scheduler configuration in effect.

## Next steps

To learn more about the AKS scheduler and best practices, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-storage-drivers -->

# Container Storage Interface (CSI) drivers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Kubernetes. By adopting and using CSI, Azure Kubernetes Service (AKS) can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes without having to touch the core Kubernetes code and wait for its release cycles.

The CSI storage driver support on AKS allows you to natively use:

can be used to create a Kubernetes**Azure Disks***DataDisk*resource. Disks can use Azure Premium Storage, backed by high-performance SSDs, or Azure Standard Storage, backed by regular HDDs or Standard SSDs. For most production and development workloads, use Premium Storage. Azure Disks are mounted as*ReadWriteOnce*and are only available to one node in AKS. For storage volumes that can be accessed by multiple nodes simultaneously, use Azure Files.can be used to mount an SMB 3.0/3.1 share backed by an Azure storage account to pods. With Azure Files, you can share data across multiple nodes and pods. Azure Files can use Azure Standard storage backed by regular HDDs or Azure Premium storage backed by high-performance SSDs.**Azure Files**can be used to mount Blob storage (or object storage) as a file system into a container or pod. Using Blob storage enables your cluster to support applications that work with large unstructured datasets like log file data, images or documents, HPC, and others. Additionally, if you ingest data into**Azure Blob storage**[Azure Data Lake storage](/en-us/azure/storage/blobs/data-lake-storage-introduction), you can directly mount and use it in AKS without configuring another interim filesystem.

Tip

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Prerequisites

- You need the Azure CLI version 2.42 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If the open-source CSI storage driver is installed on your cluster, uninstall it before enabling the Azure storage CSI driver.
- To enforce the Azure Policy for AKS
[policy definition](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes)**Kubernetes clusters should use Container Storage Interface(CSI) driver StorageClass**, the Azure Policy add-on needs to be enabled on new and existing clusters. For an existing cluster, review the[Learn Azure Policy for Kubernetes](/en-us/azure/governance/policy/concepts/policy-for-kubernetes)to enable it.

## Disk encryption supported scenarios

CSI storage drivers support the following scenarios:

[Encrypted managed disks with customer-managed keys](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys)using Azure Key Vaults stored in a different Microsoft Entra tenant.- Encrypt your Azure Storage disks hosting AKS OS and application data with
[customer-managed keys](azure-disk-customer-managed-keys).

## Enable CSI storage drivers on an existing cluster

To enable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--enable-disk-driver`

allows you to enable the[Azure Disks CSI driver](azure-disk-csi).`--enable-file-driver`

allows you to enable the[Azure Files CSI driver](azure-files-csi).`--enable-blob-driver`

allows you to enable the[Azure Blob storage CSI driver](azure-blob-csi).`--enable-snapshot-controller`

allows you to enable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks update --name myAKSCluster --resource-group myResourceGroup --enable-disk-driver --enable-file-driver --enable-blob-driver --enable-snapshot-controller
```


It might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results when enabling the Blob storage CSI driver:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
```


## Disable CSI storage drivers on a new or existing cluster

To disable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--disable-disk-driver`

allows you to disable the[Azure Disks CSI driver](azure-disk-csi).`--disable-file-driver`

allows you to disable the[Azure Files CSI driver](azure-files-csi).`--disable-blob-driver`

allows you to disable the[Azure Blob storage CSI driver](azure-blob-csi).`--disable-snapshot-controller`

allows you to disable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks create \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller \
--generate-ssh-keys
```


To disable CSI storage drivers on an existing cluster, use one of the parameters listed earlier depending on the storage system:

```
az aks update \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller
```


Note

We recommend deleting the corresponding PersistentVolumeClaim object instead of the PersistentVolume object when deleting a CSI volume. The external provisioner in the CSI driver will react to the deletion of the PersistentVolumeClaim and based on its reclamation policy, it issues the DeleteVolume call against the CSI volume driver commands to delete the volume. The PersistentVolume object is then deleted.

## Migrate custom in-tree storage classes to CSI

Starting with Kubernetes version 1.26, in-tree persistent volume types *kubernetes.io/azure-disk* and *kubernetes.io/azure-file* are deprecated and will no longer be supported. *In-tree drivers* refers to the storage drivers that are part of the core Kubernetes code opposed to the CSI drivers, which are plug-ins.

Removing these drivers following their deprecation isn't planned, however you should migrate to the corresponding CSI drivers *disk.csi.azure.com* and *file.csi.azure.com*. To review the migration options for your storage classes and upgrade your cluster to use Azure Disks and Azure Files CSI drivers, see [Migrate from in-tree to CSI drivers](csi-migrate-in-tree-volumes).

If you've created in-tree driver storage classes, those storage classes continue to work since CSI migration is turned on after upgrading your cluster to 1.21.x. If you want to use CSI features you'll need to perform the migration.

## Next steps

- To use the CSI driver for Azure Disks, see
[Use Azure Disks with CSI drivers](azure-disk-csi). - To use the CSI driver for Azure Files, see
[Use Azure Files with CSI drivers](azure-files-csi). - To use the CSI driver for Azure Blob storage, see
[Use Azure Blob storage with CSI drivers](azure-blob-csi) - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information on CSI migration, see
[Kubernetes in-tree to CSI Volume Migration](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-csi-migration-beta).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/resize-node-pool -->

# Resize node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might want to change the size of your virtual machines (VMs) to accommodate an increasing number of deployments or to run a larger workload. Resizing AKS instances directly isn't supported when using [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview) in AKS, as outlined in the [support policies for AKS](support-policies#user-customization-of-agent-nodes):

AKS agent nodes appear in the Azure portal as regular Azure IaaS resources. But these virtual machines are deployed into a custom Azure resource group (usually prefixed with MC_*). You can't make direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't done via the AKS API won't persist through an upgrade, scale, update, or reboot.


In this article, you learn the recommended method to resize a node pool by creating a new node pool with the desired SKU size, cordoning and draining the existing nodes, and then removing the existing node pool.

Important

This method is specific to [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview)-based AKS clusters. When using Virtual Machines-based node pools, you can easily update the VM sizes in an existing node pool using a single Azure CLI command and have multiple VM sizes in the same node pool. For more information, see the [Virtual Machines node pools documentation](virtual-machines-node-pools).

## Create a new node pool with the desired SKU

Note

Every AKS cluster must contain at least one system node pool with at least one node. In this example, we use a `--mode`

of `System`

to add a system node pool to replace the system node pool we want to resize. You can [update the mode of a node pool](use-system-pools#update-existing-cluster-system-and-user-node-pools) at any time. You can also add a user node pool by setting `--mode`

to `User`

.

When resizing, make sure you consider all workload requirements, such as availability zones, and configure your VMSS node pool accordingly. You might need to modify the following command to best fit your needs. For a full list of the configuration options, see the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) reference page.

Create a new node pool using the

command. In this example, we create a new node pool,`az aks nodepool add`

`mynodepool`

, with three nodes and the`Standard_DS3_v2`

VM SKU to replace an existing node pool,`nodepool1`

, that has the`Standard_DS2_v2`

VM SKU.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 3 \ --node-vm-size Standard_DS3_v2 \ --mode System \ --no-wait`

It takes a few minutes for the new node pool to be created.

Get the status of the new node pool using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing both the new node pool

`mynodepool`

and the existing node pool`nodepool1`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 23m v1.21.9 aks-nodepool1-12345678-vmss000000 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 10d v1.21.9`


## Cordon the existing nodes

Cordoning marks specified nodes as unschedulable and prevents any more pods from being added to the nodes.

Get the names of the nodes you want to cordon using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing the nodes in the existing node pool

`nodepool1`

that you want to cordon:`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 7d21h v1.21.9`

Cordon the existing nodes using the

`kubectl cordon`

command, specifying the desired nodes in a space-separated list. For example:`kubectl cordon aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002`

Your output should resemble the following example output, showing that the nodes are cordoned:

`node/aks-nodepool1-12345678-vmss000000 cordoned node/aks-nodepool1-12345678-vmss000001 cordoned node/aks-nodepool1-12345678-vmss000002 cordoned`


## Drain the existing nodes

Important

To successfully drain nodes and evict running pods, ensure that any PodDisruptionBudgets (PDBs) allow for at least one pod replica to be moved at a time. Otherwise, the drain/evict operation fails. To check this, you can run `kubectl get pdb -A`

and verify `ALLOWED DISRUPTIONS`

is at least `1`

or higher.

When you drain nodes, the pods running on them are evicted and recreated on the other schedulable nodes.

Drain the existing nodes using the

`kubectl drain`

command with the`--ignore-daemonsets`

and`--delete-emptydir-data`

flags, specifying the desired nodes in a space-separated list. For example:Important

Using

`--delete-emptydir-data`

is required to evict the AKS-created`coredns`

and`metrics-server`

pods. If you don't use this flag, you get an error. For more information, see the[documentation on emptydir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir).`kubectl drain aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002 --ignore-daemonsets --delete-emptydir-data`

After the drain operation finishes, all pods (excluding the pods controlled by daemon sets) should be running on the new node pool. You can verify this using the

`kubectl get pods`

command.`kubectl get pods -o wide -A`


### Troubleshoot pod eviction issues

You might encounter the following error when draining nodes:


`Error when evicting pods/[podname] -n [namespace] (will retry after 5s): Cannot evict pod as it would violate the pod's disruption budget.`


By default, your cluster has AKS-managed pod disruption budgets (such as `coredns-pdb`

or `konnectivity-agent`

) with a `MinAvailable`

of `1`

. For example, if there are two `coredns`

pods running, only one can be disrupted at a time. While one of them is getting recreated and is unavailable, the other `coredns`

pod can't be evicted due to the pod disruption budget. This issue resolves itself after the initial `coredns`

pod is scheduled and running, allowing the second pod to be properly evicted and recreated.

Tip

Consider draining nodes one by one for a smoother eviction experience and to avoid throttling. For more information, see:

## Remove the existing node pool

Important

When you delete a node pool, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the node pool you plan to delete, perform a cordon and drain on all nodes in the node pool before deleting.

Delete the original node pool using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1`

Verify that your AKS cluster has only the new node pool with the applications and pods properly running using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing only the new node pool

`mynodepool`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 63m v1.21.9`


## Next steps

After resizing a node pool by cordoning and draining, learn more about [using multiple node pools](create-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-annual-channel -->

# Use Windows Server Annual Channel for Containers on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS supports [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) in public preview. Each channel version is released annually and is supported for *two years*. This channel is beneficial if you require increased innovation cycles and portability.

Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Supported Annual Channel releases

AKS releases support for new releases of Windows Server Annual Channel for Containers in alignment with Kubernetes versions. For the latest updates, see the [AKS release notes](https://github.com/Azure/AKS/releases). The following table provides an *estimated* release schedule for upcoming Annual Channel releases:

| K8s version | Annual Channel (host) version | Container image supported | End of support date |
|---|---|---|---|
| 1.28 | 23H2 (preview only) | Windows Server 2022 | End of 1.33 support |
| 1.34 | 24H2 | Windows Server 2022 & Windows Server 2025 | End of 1.35 support |

## Windows Server Annual Channel vs. Long Term Servicing Channel Releases (LTSC)

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025, Windows Server 2022, and Windows Server 2019. These come from a different release channel than Windows Server Annual Channel for Containers. To view our current recommendations, see the [Windows best practices documentation](windows-best-practices).

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

The following table compares Windows Server Annual Channel and Long Term Servicing Channel releases:

| Channel | Support | Upgrades |
|---|---|---|
| Long Term Servicing Channel (LTSC) | LTSC channels are released every three years and are supported for five years. This channel is recommended for customers using Long Term Support. | To upgrade from one release to the next, you need to migrate your node pools to a new OS SKU option and rebuild your container images with the new OS version. |
| Windows Server Annual Channel for Containers | Annual Channel releases occur annually and are supported for two years. | To upgrade to the latest release, you can upgrade the Kubernetes version of your node pool. |

## Before you begin

- You need the Azure CLI version 2.56.0 or later installed and configured to set
`os-sku`

to`WindowsAnnual`

with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- Windows Server Annual Channel doesn't support Azure Network Policy Manager.

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `AKSWindowsAnnualPreview`

feature flag

Register the

`AKSWindowsAnnualPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Use Windows Server Annual Channel for Containers on AKS

To use Windows Server Annual Channel on AKS, specify the following parameters:

`os-type`

set to`Windows`

`os-sku`

set to`WindowsAnnual`


Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To check which release you'll get based on the Kubernetes version of your node pool, see the [supported Annual Channel releases](#supported-annual-channel-releases).

### Create a new Windows Server Annual Channel node pool

Create a Windows Server Annual Channel node pool using the

command. The following example creates a Windows Server Annual Channel node pool with the 23H2 release:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --os-sku WindowsAnnual \ --kubernetes-version 1.29 --name $NODE_POOL_NAME \ --node-count 1`

Note

If you don't specify the Kubernetes version during node pool creation, AKS uses the same Kubernetes version as your cluster.


### Verify Windows Server Annual Channel node pool creation

Verify Windows Server Annual Channel node pool creation by checking the OS SKU of your node pool using

`kubectl describe node`

command.`kubectl describe node $NODE_POOL_NAME`

If you successfully created a Windows Server Annual Channel node pool, you should see the following output:

`Name: npwin Roles: agent Labels: agentpool=npwin ... kubernetes.azure.com/os=windows ... kubernetes.azure.com/node-image-version=AKSWindows-23H2-gen2 ... kubernetes.azure.com/os-sku=WindowsAnnual`


### Upgrade an existing node pool to Windows Server Annual Channel

You can upgrade an existing node pool from an LTSC release to Windows Server Annual Channel by following the guidance in [Upgrade the OS version for your Azure Kubernetes Service (AKS) Windows workloads](upgrade-windows-os).

To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

## Next steps

To learn more about Windows Containers on AKS, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/artifact-streaming -->

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

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **July 15, 2025**, Azure Kubernetes Service (AKS) no longer supports [Teleport (preview)](https://github.com/Azure/acr/blob/main/docs/teleport/aks-getting-started.md) on AKS. After this date, AKS node pools with Teleport enabled might experience breakage and node provisioning failures. Azure Container Registry removed the Teleport API, meaning that any nodes with Teleport enabled will pull images from Azure Container Registry like any other AKS node without Teleport. Migrate to [Artifact Streaming (preview)](/en-us/azure/aks/artifact-streaming) or update your node pools to set `--aks-custom-headers EnableACRTeleport=false`

. For more information on this retirement, see the [Retirement GitHub issue](https://aka.ms/aks/teleport-retirement). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ray-overview -->

# Deploy a Ray cluster on Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy a Ray cluster on Azure Kubernetes Service (AKS) using the KubeRay operator. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What is Ray?

[Ray](https://docs.ray.io/en/latest/index.html#) is an open-source project developed at UC Berkeley's RISE Lab that provides a unified framework for scaling AI and Python applications. It consists of a core distributed runtime and a set of AI libraries designed to accelerate machine learning workloads.

Ray simplifies the process of running compute-intensive Python tasks at scale, allowing you to seamlessly scale your applications. The framework supports various machine learning tasks, including distributed training, hyperparameter tuning, reinforcement learning, and production model serving.

For more information, see the [Ray GitHub repository](https://github.com/ray-project/ray).

## What is KubeRay?

[KubeRay](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started.html) is an open-source Kubernetes operator for deploying and managing Ray clusters on Kubernetes. KubeRay automates the deployment, scaling, and monitoring of Ray clusters. It provides a declarative way to define Ray clusters using Kubernetes custom resources, making it easy to manage Ray clusters alongside other Kubernetes resources.

For more information, see the [KubeRay GitHub repository](https://github.com/ray-project/kuberay).

## Ray deployment process

The deployment process consists of the following steps:

- Use Terraform to create a local plan file to define the desired state for infrastructure required AKS infrastructure that consists of an Azure resource group, a dedicated system node pool, and a workload node pool for Ray with three nodes.
- Deploy a local Terraform plan to Azure.
- Retrieve outputs from the Terraform deployment and obtain Kubernetes credentials to the newly deployed AKS cluster.
- Install the Helm Ray repository and deploy KubeRay to the AKS cluster using Helm.
- Download and execute a
[Ray Job](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/index.html)YAML manifest from the Ray GitHub samples repo to perform an image classification with a[MNIST](https://github.com/cvdfoundation/mnist)dataset using[Convolutional Neural Networks (CNNs)](https://techcommunity.microsoft.com/discussions/machinelearning/what-is-convolutional-neural-network-%E2%80%94-cnn-deep-learning/4184725). - Output the logs from the Ray Job to gain insight into the machine learning process performed by Ray.

## Next step

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-migration -->

# Migrate from Dapr OSS to the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to migrate from Dapr OSS to the Dapr extension for AKS.

You can configure the Dapr extension to use and manage the Kubernetes resources created by Dapr OSS by either:

[Checking for an existing Dapr installation using the Azure CLI](#check-for-an-existing-dapr-installation)(*default method*), or[Configuring the existing Dapr installation using](#configure-the-existing-dapr-installation-using---configuration-settings).`--configuration-settings`


For more information, see [an overview of the Dapr extension for AKS](dapr-overview).

## Check for an existing Dapr installation

When you [install the Dapr extension](dapr), the extension checks for an existing Dapr installation on your cluster. If Dapr exists, the extension uses and manages the Kubernetes resources created by Dapr OSS.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Enter the Helm release name and namespace (from

`helm list -A`

) when prompted with the following questions:`Enter the Helm release name for Dapr, or press Enter to use the default name [dapr]: Enter the namespace where Dapr is installed, or press Enter to use the default namespace [dapr-system]:`


## Configure the existing Dapr installation using `--configuration-settings`


When you [create the Dapr extension](dapr), you can configure the extension to use and manage the Kubernetes resources created by Dapr OSS using the `--configuration-settings`

flag.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Create the Dapr extension using the

and use the`az k8s-extension create`

`--configuration-settings`

flags to set the Dapr release name and namespace.`az k8s-extension create --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --configuration-settings "existingDaprReleaseName=dapr" \ --configuration-settings "existingDaprReleaseNamespace=dapr-system"`


## Update HA mode or placement service settings

When installing the Dapr extension on top of an existing Dapr installation, you receive the following message:

```
The extension will be installed on your existing Dapr installation. Note, if you have updated the default values for global.ha.* or dapr_placement.* in your existing Dapr installation, you must provide them in the configuration settings. Failing to do so will result in an error, since Helm upgrade will try to modify the StatefulSet. See <link> for more information.
```


Kubernetes only allows patching for limited fields in StatefulSets. If any of the HA mode or placement service settings are configured, the upgrade fails. To update the HA mode or placement service settings, you must delete the stateful set and then update the HA mode.

Delete the stateful set using the

`kubectl delete`

command.`kubectl delete statefulset.apps/dapr-placement-server -n dapr-system`

Update the HA mode using the

command.`az k8s-extension update`

`az k8s-extension update --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --auto-upgrade-minor-version true \ --configuration-settings "global.ha.enabled=true" \`


For more information, see the [Dapr production guidelines](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production/#enabling-high-availability-in-an-existing-dapr-deployment).

## Next steps

Learn more about [Dapr](dapr-overview) and [how to use it](dapr).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/supported-kubernetes-versions -->

# Supported Kubernetes versions in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community [releases minor versions](https://kubernetes.io/releases/) roughly every four months.

Minor version releases include new features and improvements. Patch releases are more frequent (sometimes weekly) and are intended for critical bug fixes within a minor version. Patch releases include fixes for security vulnerabilities or major bugs.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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

**allowPrivilegeEscalation**defines if the pod can assume*root*privileges. Design your applications so this setting is always set to*false*.**Linux capabilities**let the pod access underlying node processes. Take care with assigning these capabilities. Assign the least number of privileges needed. For more information, see[Linux capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html).**SELinux labels**is a Linux kernel security module that lets you define access policies for services, processes, and filesystem access. Again, assign the least number of privileges needed. For more information, see[SELinux options in Kubernetes](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#selinuxoptions-v1-core)**hostUsers: false**the pod runs using a user-namespace, a Linux kernel feature. This significantly improves the host isolation and limits the lateral movement in case of container breakouts. These improvements are significant whether the container is running as root or not. For more information, see[user-namespaces](secure-container-access#overview-of-user-namespaces).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-ad-pod-identity -->

# Use Microsoft Entra pod-managed identities in AKS (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Entra pod-managed identities use Azure Kubernetes Service (AKS) primitives to associate [managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview) and identities in Microsoft Entra ID with pods. Administrators create identities and bindings as Kubernetes primitives that allow pods to access Azure resources that rely on Microsoft Entra ID as an identity provider.

Microsoft Entra pod-managed identities in AKS have the following limitations:

- Each cluster supports up to 200 pod-managed identities.
- Each cluster supports up to 200 pod-managed identity exceptions.
- Pod-managed identities are supported only on Linux node pools.
- This feature is supported only on clusters backed by Virtual Machine Scale Sets.

Important

We recommend you review [Microsoft Entra Workload ID](workload-identity-overview). This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities to federate with any external identity providers on behalf of the application.

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated on October 24, 2022, and the project archived in September 2023. For more information, see the [deprecation notice](https://github.com/Azure/aad-pod-identity#-announcement). The AKS Pod Identity Managed add-on is patched and supported through September 2025 to allow time for customers to move over to [Microsoft Entra Workload ID](workload-identity-overview).

## Operation mode options

Microsoft Entra pod-managed identity supports two modes of operation:

**Standard Mode**: In this mode, the following two components are deployed to the AKS cluster:[Managed Identity Controller (MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): An MIC is a Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/), and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying Virtual Machine Scale Set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the Virtual Machine Scale Set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): NMI is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. NMI intercepts token requests and redirects them to itself. It then checks if the pod is authorized to access the requested identity and, if so, retrieves the token from the Microsoft Entra tenant on behalf of the application.

**Managed Mode**: This mode offers only NMI. When installed via the AKS cluster add-on, Azure manages creation of Kubernetes primitives (AzureIdentity and AzureIdentityBinding) and identity assignment in response to CLI commands by the user. Otherwise, if installed via Helm chart, the identity needs to be manually assigned and managed per the user. For more information, see[Pod identity in managed mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/).

When you install the Microsoft Entra pod-managed identity via Helm chart or YAML manifest as shown in the [Installation Guide](https://azure.github.io/aad-pod-identity/docs/getting-started/installation/), you can choose between the `standard`

and `managed`

mode. If you instead decide to install the
Microsoft Entra pod-managed identity using the AKS cluster add-on as shown in this article, the setup uses the `managed`

mode.

## Prerequisites

Your Microsoft Entra pod-managed identities in AKS must meet the following requirements:

The Azure CLI version 2.20.0 or later is installed.

Your AKS cluster is at version 1.26 or later.

You must have the appropriate permissions such as the

**Owner**or**Contributor**role.

## Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension released:

```
az extension update --name aks-preview
```


## Register the EnablePodIdentityPreview feature flag

Register the `EnablePodIdentityPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


Tip

To disable the AKS Managed add-on, run the following command:

```
az feature unregister --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


It takes a few minutes for the status to show as *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace Microsoft.ContainerService
```


## Manage an AKS cluster with pod-managed identities

You can manage your AKS cluster with either the Azure Container Networking Interface (CNI) or Kubenet network plugin when enabling Microsoft Entra pod-managed identities.

Create an AKS cluster with Azure CNI and pod-managed identity enabled with the default recommended configuration. The following commands use

[az group create](/en-us/cli/azure/group#az-group-create)to create a resource group named*myResourceGroup*and thecommand to create an AKS cluster named`az aks create`

*myAKSCluster*in the*myResourceGroup*resource group.`az group create --name myResourceGroup --location eastus az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-pod-identity \ --network-plugin azure \ --generate-ssh-keys`

Use

to sign in to your AKS cluster. This command also downloads and configures the`az aks get-credentials`

`kubectl`

client certificate on your development computer.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


When you enable pod-managed identity on your AKS cluster, the system adds an `AzurePodIdentityException`

named *aks-addon-exception* to the *kube-system* namespace. An `AzurePodIdentityException`

lets pods with certain labels access the Azure Instance Metadata Service (IMDS) endpoint without interception by the NMI server. The *aks-addon-exception* allows AKS first-party addons, such as Microsoft Entra pod-managed identity, to operate without requiring you to manually configure an `AzurePodIdentityException`

. Optionally, you can add, remove, and update an `AzurePodIdentityException`

using:

`az aks pod-identity exception add`

`az aks pod-identity exception delete`

`az aks pod-identity exception update`

Or

`kubectl`


## Update an existing AKS cluster with Azure CNI

To update an existing AKS cluster with Azure CNI to include pod-managed identity, run the following command:

```
az aks update --resource-group $MY_RESOURCE_GROUP --name $MY_CLUSTER --enable-pod-identity
```


## Create a managed identity

You must have the relevant permissions (for example, **Owner**) on your subscription to create the identity.

To create an identity to be used by the demo pod with [az identity create](/en-us/cli/azure/identity#az-identity-create), set the *IDENTITY_CLIENT_ID* and *IDENTITY_RESOURCE_ID* variables, run the following command:

```
az group create --name myIdentityResourceGroup --location eastus
export IDENTITY_RESOURCE_GROUP="myIdentityResourceGroup"
export IDENTITY_NAME="application-identity"
az identity create --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME}
export IDENTITY_CLIENT_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query clientId -o tsv)"
export IDENTITY_RESOURCE_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query id -o tsv)"
```


## Assign permissions for the managed identity

The managed identity assigned to the pod must be granted appropriate permissions based on the operations the pod performs. Ensure that you assign only the minimum required roles to follow security best practices.

To run the demo, the *IDENTITY_CLIENT_ID* managed identity must have **Virtual Machine Contributor** permissions in the resource group that contains the Virtual Machine Scale Set of your AKS cluster.

```
# Obtain the name of the resource group containing the Virtual Machine Scale set of your AKS cluster, commonly called the node resource group
NODE_GROUP=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
# Obtain the id of the node resource group
NODES_RESOURCE_ID=$(az group show --name $NODE_GROUP -o tsv --query "id")
# Create a role assignment granting your managed identity permissions on the node resource group
az role assignment create --role "Virtual Machine Contributor" --assignee "$IDENTITY_CLIENT_ID" --scope $NODES_RESOURCE_ID
```


## Create a pod-managed identity

To create a pod-managed identity for the cluster using `az aks pod-identity add`

, run the following command:

```
export POD_IDENTITY_NAME="my-pod-identity"
export POD_IDENTITY_NAMESPACE="my-app"
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME} --identity-resource-id ${IDENTITY_RESOURCE_ID}
```


Note

The "POD_IDENTITY_NAME" has to be a valid Domain Name System [(DNS) subdomain name](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-subdomain-names) as defined in [RFC 1123](https://tools.ietf.org/html/rfc1123).

When you assign the pod-managed identity by using `pod-identity add`

, the Azure CLI attempts to grant the Managed Identity Operator role over the pod-managed identity (*IDENTITY_RESOURCE_ID*) to the cluster identity.

Azure creates an AzureIdentity resource in your cluster representing the identity in Azure, and an AzureIdentityBinding resource that connects the AzureIdentity to a selector. You can view these resources by running the following command:

```
kubectl get azureidentity -n $POD_IDENTITY_NAMESPACE
kubectl get azureidentitybinding -n $POD_IDENTITY_NAMESPACE
```


## Run a sample application

For a pod to use Microsoft Entra pod-managed identity, the pod needs an *aadpodidbinding* label with a value that matches a selector from a *AzureIdentityBinding*. By default, the selector matches the name of the pod-managed identity, but it can also be set using the `--binding-selector`

option when calling `az aks pod-identity add`

.

To run a sample application using Microsoft Entra pod-managed identity, create a `demo.yaml`

file with the following contents. Replace *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* with the values from the previous steps. Replace *SUBSCRIPTION_ID* with your subscription ID.

Note

In the previous steps, you created the *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* variables. You can use a command such as `echo`

to display the value you set for variables, for example `echo $POD_IDENTITY_NAME`

.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: $POD_IDENTITY_NAME
spec:
containers:
- name: demo
image: mcr.microsoft.com/oss/azure/aad-pod-identity/demo:v1.6.3
args:
- --subscriptionid=$SUBSCRIPTION_ID
- --clientid=$IDENTITY_CLIENT_ID
- --resourcegroup=$IDENTITY_RESOURCE_GROUP
env:
- name: MY_POD_NAME
valueFrom:
fieldRef:
fieldPath: metadata.name
- name: MY_POD_NAMESPACE
valueFrom:
fieldRef:
fieldPath: metadata.namespace
- name: MY_POD_IP
valueFrom:
fieldRef:
fieldPath: status.podIP
nodeSelector:
kubernetes.io/os: linux
```


Notice the pod definition has an `aadpodidbinding`

label with a value that matches the name of the pod-managed identity you ran `az aks pod-identity add`

in the previous step.

Deploy the

`demo.yaml`

to the same namespace as your pod-managed identity using`kubectl apply`

:`kubectl apply -f demo.yaml --namespace $POD_IDENTITY_NAMESPACE`

Verify the sample application successfully runs using

`kubectl logs`

:`kubectl logs demo --follow --namespace $POD_IDENTITY_NAMESPACE`

Verify that the logs show a token is successfully acquired and that the HTTP

*GET*request operation is successful.`... successfully doARMOperations vm count 0 successfully acquired a token using the MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) successfully acquired a token, userAssignedID MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) clientID(xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) successfully made GET on instance metadata ...`


## Run an application with multiple identities

To enable an application to use multiple identities, set the `--binding-selector`

to the same selector when creating pod identities:

```
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_1} --identity-resource-id ${IDENTITY_RESOURCE_ID_1} --binding-selector myMultiIdentitySelector
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_2} --identity-resource-id ${IDENTITY_RESOURCE_ID_2} --binding-selector myMultiIdentitySelector
```


Then set the `aadpodidbinding`

field in your pod YAML to the binding selector you specified.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: myMultiIdentitySelector
...
```


## Disable pod-managed identity on an existing cluster

To disable pod-managed identity on an existing cluster, remove the pod-managed identities from the cluster by running the following command:

`az aks pod-identity delete --name ${POD_IDENTITY_NAME} --namespace ${POD_IDENTITY_NAMESPACE} --resource-group myResourceGroup --cluster-name myAKSCluster`

Then disable the feature on the cluster by running the following command:

`az aks update --resource-group myResourceGroup --name myAKSCluster --disable-pod-identity`


## Clean up resources

To remove a Microsoft Entra pod-managed identity from your cluster, remove the sample application and the pod-managed identity from the cluster.

```
kubectl delete pod demo --namespace $POD_IDENTITY_NAMESPACE
```


Then remove the identity and the role assignment of cluster identity.

```
az aks pod-identity delete \
--name ${POD_IDENTITY_NAME} \
--namespace ${POD_IDENTITY_NAMESPACE} \
--resource-group myResourceGroup \
--cluster-name myAKSCluster
az identity delete \
--resource-group ${IDENTITY_RESOURCE_GROUP} \
--name ${IDENTITY_NAME}
az role assignment delete \
--role "Managed Identity Operator" \
--assignee "$IDENTITY_CLIENT_ID" \
--scope "$IDENTITY_RESOURCE_ID"
```


## Next steps

For more information on managed identities, see [Managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview).

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

Starting on **September 30, 2025**, Azure Kubernetes Service (AKS) no longer supports Basic Load Balancer. To avoid any potential service disruptions, we recommend using Standard Load Balancer for new deployments and [upgrading any existing deployments to the Standard Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance). For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5020) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-premium-v2-disks -->

# Use Azure Premium SSD v2 disks on Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer IO-intense enterprise workloads, a consistent submillisecond disk latency, and high IOPS and throughput. The performance (capacity, throughput, and IOPS) of Premium SSD v2 disks can be independently configured at any time, making it easier for more scenarios to be cost efficient while meeting performance needs.

This article describes how to configure a new or existing AKS cluster to use Azure Premium SSD v2 disks.

## Before you begin

Before creating or upgrading an AKS cluster that is able to use Azure Premium SSD v2 disks, you need to create an AKS cluster in the same region and availability zone that supports Premium Storage and attach the disks following the steps below.

For an existing AKS cluster, you can enable Premium SSD v2 disks by adding a new node pool to your cluster, and then attach the disks following the steps below.

Important

Azure Premium SSD v2 disks require node pools deployed in regions that support these disks. For a list of supported regions, see [Premium SSD v2 disk supported regions](/en-us/azure/virtual-machines/disks-types#regional-availability).

### Limitations

- Azure Premium SSD v2 disks have certain limitations that you need to be aware of. For a complete list, see
[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).

## Use Premium SSD v2 disks dynamically with a storage class

To use Premium SSD v2 disks in a deployment or stateful set, you can use a [storage class for dynamic provisioning](azure-disk-csi).

### Create the storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. For more information on Kubernetes storage classes, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

In this example, you create a storage class that references Premium SSD v2 disks. Create a file named `azure-pv2-disk-sc.yaml`

, and copy in the following manifest.

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


Create the storage class with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-sc.yaml* file:

```
kubectl apply -f azure-pv2-disk-sc.yaml
```


The output from the command resembles the following example:

```
storageclass.storage.k8s.io/premium2-disk-sc created
```


## Create a persistent volume claim

A persistent volume claim (PVC) is used to automatically provision storage based on a storage class. In this case, a PVC can use the previously created storage class to create an ultra disk.

Create a file named `azure-pv2-disk-pvc.yaml`

, and copy in the following manifest. The claim requests a disk named `premium2-disk`

that is *1000 GB* in size with *ReadWriteOnce* access. The *premium2-disk-sc* storage class is specified as the storage class.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: premium2-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: premium2-disk-sc
resources:
requests:
storage: 1000Gi
```


Create the persistent volume claim with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-pvc.yaml* file:

```
kubectl apply -f azure-pv2-disk-pvc.yaml
```


The output from the command resembles the following example:

```
persistentvolumeclaim/premium2-disk created
```


## Use the persistent volume

Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk. The following manifest creates a basic NGINX pod that uses the persistent volume claim named *premium2-disk* to mount the Azure disk at the path `/mnt/azure`

.

Create a file named `nginx-premium2.yaml`

, and copy in the following manifest.

```
kind: Pod
apiVersion: v1
metadata:
name: nginx-premium2
spec:
containers:
- name: nginx-premium2
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: premium2-disk
```


Create the pod with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command, as shown in the following example:

```
kubectl apply -f nginx-premium2.yaml
```


The output from the command resembles the following example:

```
pod/nginx-premium2 created
```


You now have a running pod with your Azure disk mounted in the `/mnt/azure`

directory. This configuration can be seen when inspecting your pod via `kubectl describe pod nginx-premium2`

, as shown in the following condensed example:

```
kubectl describe pod nginx-premium2
[...]
Volumes:
volume:
Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
ClaimName: premium2-disk
ReadOnly: false
kube-api-access-sh59b:
Type: Projected (a volume that contains injected data from multiple sources)
TokenExpirationSeconds: 3607
ConfigMapName: kube-root-ca.crt
ConfigMapOptional: <nil>
DownwardAPI: true
QoS Class: Burstable
Node-Selectors: <none>
Tolerations: node.kubernetes.io/memory-pressure:NoSchedule op=Exists
node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal Scheduled 7m58s default-scheduler Successfully assigned default/nginx-premium2 to aks-agentpool-12254644-vmss000006
Normal SuccessfulAttachVolume 7m46s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-ff39fb64-1189-4c52-9a24-e065b855b886"
Normal Pulling 7m39s kubelet Pulling image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine"
Normal Pulled 7m38s kubelet Successfully pulled image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" in 1.192915667s
Normal Created 7m38s kubelet Created container nginx-premium2
Normal Started 7m38s kubelet Started container nginx-premium2
[...]
```


## Set IOPS and throughput limits

Input/Output Operations Per Second (IOPS) and throughput limits for Azure Premium v2 SSD disk is currently not supported through AKS. To adjust performance, you can use the Azure CLI command [az disk update](/en-us/cli/azure/disk#az-disk-update) and including the `--disk-iops-read-write`

and `--disk-mbps-read-write`

parameters.

The following example updates the disk IOPS read/write to **5000** and Mbps to **200**. For `--resource-group`

, the value must be the second resource group automatically created to store the AKS worker nodes with the naming convention *MC_resourcegroupname_clustername_location*. For more information, see [Why are two resource groups created with AKS?](faq).

The value for the `--name`

parameter is the name of the volume created using the StorageClass, and it starts with `pvc-`

. To identify the disk name, you can run `kubectl get pvc`

or navigate to the secondary resource group in the portal to find it. See [manage resources from the Azure portal](/en-us/azure/azure-resource-manager/management/manage-resources-portal#open-resources) to learn more.

```
az disk update --subscription subscriptionName --resource-group myResourceGroup --name diskName --disk-iops-read-write=5000 --disk-mbps-read-write=200
```


## Next steps

- For more about Premium SSD v2 disks, see
[Using Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-deploy-premium-v2). - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-nfs -->

# Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using NFS (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), or [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning NFS volumes statically or dynamically.
- For information about provisioning SMB volumes statically or dynamically, see
[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use NFS volumes

This section describes how to create an NFS volume on Azure NetApp Files and expose the volume statically to Kubernetes. It also describes how to use the volume with a containerized application.

### Create an NFS volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*,*vnetid*, and*anfSubnetID*with an appropriate value from your account and environment. The*filepath*must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are Standard, Premium, and Ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command. For more information, see`az netappfiles volume create`

[Create an NFS volume for Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-create-volumes).`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types NFSv3`


### Create the persistent volume

List the details of your volume using

command. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myfilepath2", ... "mountTargets": [ { ... "ipAddress": "10.0.0.4", ... } ], ... }`

Create a file named

`pv-nfs.yaml`

and copy in the following YAML. Make sure the server matches the output IP address from Step 1, and the path matches the output from`creationToken`

above. The capacity must also match the volume size from the step above.`apiVersion: v1 kind: PersistentVolume metadata: name: pv-nfs spec: capacity: storage: 100Gi accessModes: - ReadWriteMany mountOptions: - vers=3 nfs: server: 10.0.0.4 path: /myfilepath2`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-nfs.yaml`

Verify the status of the persistent volume is

*Available*by using thecommand:`kubectl describe`

`kubectl describe pv pv-nfs`


### Create a persistent volume claim

Create a file named

`pvc-nfs.yaml`

and copy in the following YAML. This manifest creates a PVC named`pvc-nfs`

for 100Gi storage and`ReadWriteMany`

access mode, matching the PV you created.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: pvc-nfs spec: accessModes: - ReadWriteMany storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-nfs.yaml`

Verify the

*Status*of the persistent volume claim is*Bound*by using thecommand:`kubectl describe`

`kubectl describe pvc pvc-nfs`


### Mount with a pod

Create a file named

`nginx-nfs.yaml`

and copy in the following YAML. This manifest defines a`nginx`

pod that uses the persistent volume claim.`kind: Pod apiVersion: v1 metadata: name: nginx-nfs spec: containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine name: nginx-nfs command: - "/bin/sh" - "-c" - while true; do echo $(date) >> /mnt/azure/outfile; sleep 1; done volumeMounts: - name: disk01 mountPath: /mnt/azure volumes: - name: disk01 persistentVolumeClaim: claimName: pvc-nfs`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f nginx-nfs.yaml`

Verify the pod is

*Running*by using thecommand:`kubectl describe`

`kubectl describe pod nginx-nfs`

Verify your volume has been mounted on the pod by using

to connect to the pod, and then use`kubectl exec`

`df -h`

to check if the volume is mounted.`kubectl exec -it nginx-nfs -- sh`

`/ # df -h Filesystem Size Used Avail Use% Mounted on ... 10.0.0.4:/myfilepath2 100T 384K 100T 1% /mnt/azure ...`


## Dynamically configure for applications that use NFS volumes

Trident may be used to dynamically provision NFS or SMB files on Azure NetApp Files. Dynamically provisioned SMB volumes are only supported with windows worker nodes.

This section describes how to use Trident to dynamically create an NFS volume on Azure NetApp Files and automatically mount it to a containerized application.

### Install Trident

To dynamically provision NFS volumes, you need to install Trident. Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

To install Trident using Helm for a cluster with only Linux worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 13:55:36 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: false Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 2m59s trident-operator.netapp.io Installing Trident Normal Installed 2m31s trident-operator.netapp.io Trident installed`


### Create a backend

To instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes, a backend is created. This step requires details about the account that was created in a previous step.

Create a file named

`backend-secret.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf.yaml`

and copy in the following YAML. Change the`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. Use the`subscriptionID`

for the Azure subscription where Azure NetApp Files is enabled. Obtain the`tenantID`

,`clientID`

, and`clientSecret`

from an[application registration](/en-us/azure/active-directory/develop/howto-create-service-principal-portal)in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The location must be an Azure location that contains at least one delegated subnet created in a previous step. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret`

For more information about backends, see

[Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).Apply the secret and backend using the

command. First apply the secret:`kubectl apply`

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Apply the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Confirm the backend was created by using the

command:`kubectl get`

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-kfrdh backend-tbc-anf 8da4e926-9dd4-4a40-8d6a-375aab28c566`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass.yaml`

and copy in the following YAML:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azure-netapp-files provisioner: csi.trident.netapp.io parameters: backendType: "azure-netapp-files" fsType: "nfs"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass.yaml`

The output of the command resembles the following example:

`storageclass/azure-netapp-files created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE azure-netapp-files csi.trident.netapp.io Delete Immediate false`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files volume and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc.yaml`

and copy in the following YAML. In this example, a 1-TiB volume is needed with ReadWriteMany access.`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc spec: accessModes: - ReadWriteMany resources: requests: storage: 1Ti storageClassName: azure-netapp-files`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`kubectl get pvc -n trident NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc Bound pvc-bffa315d-3f44-4770-86eb-c922f567a075 1Ti RWO azure-netapp-files 62s`


### Use the persistent volume

After the PVC is created, Trident creates the persistent volume. A pod can be spun up to mount and access the Azure NetApp Files volume.

The following manifest can be used to define an NGINX pod that mounts the Azure NetApp Files volume created in the previous step. In this example, the volume is mounted at `/mnt/data`

.

Create a file named

`anf-nginx-pod.yaml`

and copy in the following YAML:`kind: Pod apiVersion: v1 metadata: name: nginx-pod spec: containers: - name: nginx image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/data" name: volume volumes: - name: volume persistentVolumeClaim: claimName: anf-pvc`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f anf-nginx-pod.yaml`

The output of the command resembles the following example:

`pod/nginx-pod created`

Kubernetes has created a pod with the volume mounted and accessible within the

`nginx`

container at`/mnt/data`

. You can confirm by checking the event logs for the pod usingcommand:`kubectl describe`

`kubectl describe pod nginx-pod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: anf-pvc ReadOnly: false default-token-k7952: Type: Secret (a volume populated by a Secret) SecretName: default-token-k7952 Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 15s default-scheduler Successfully assigned trident/nginx-pod to brameshb-non-root-test Normal SuccessfulAttachVolume 15s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-bffa315d-3f44-4770-86eb-c922f567a075" Normal Pulled 12s kubelet Container image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" already present on machine Normal Created 11s kubelet Created container nginx Normal Started 10s kubelet Started container nginx`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-vertical-pod-autoscaler -->

# Use the Vertical Pod Autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the Vertical Pod Autoscaler (VPA) on your Azure Kubernetes Service (AKS) cluster. The VPA automatically adjusts the CPU and memory requests for your pods to match the usage patterns of your workloads. This feature helps to optimize the performance of your applications and reduce the cost of running your workloads in AKS.

For more information, see the [Vertical Pod Autoscaler overview](vertical-pod-autoscaler).

## Before you begin

If you have an existing AKS cluster, make sure it's running Kubernetes version 1.24 or higher.

You need the Azure CLI version 2.52.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If enabling VPA on an existing cluster, make sure

`kubectl`

is installed and configured to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --name <cluster-name> --resource-group <resource-group-name>`


## Deploy the Vertical Pod Autoscaler on a new cluster

Create a new AKS cluster with the VPA enabled using the

command with the`az aks create`

`--enable-vpa`

flag.`az aks create --name <cluster-name> --resource-group <resource-group-name> --enable-vpa --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Update an existing cluster to use the Vertical Pod Autoscaler

Update an existing cluster to use the VPA using the

command with the`az aks update`

`--enable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --enable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Disable the Vertical Pod Autoscaler on an existing cluster

Disable the VPA on an existing cluster using the

command with the`az aks update`

`--disable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --disable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Test Vertical Pod Autoscaler installation

In the following example, we create a deployment with two pods, each running a single container that requests 100 millicore and tries to utilize slightly above 500 millicores. We also create a VPA config pointing at the deployment. The VPA observes the behavior of the pods, and after about five minutes, updates the pods to request 500 millicores.

Create a file named

`hamster.yaml`

and copy in the following manifest of the Vertical Pod Autoscaler example from the[kubernetes/autoscaler](https://github.com/kubernetes/autoscaler/blob/master/vertical-pod-autoscaler/examples/hamster.yaml)GitHub repository:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: hamster image: registry.k8s.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

Deploy the

`hamster.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f hamster.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods -l app=hamster`

Your output should look similar to the following example output:

`hamster-78f9dcdd4c-hf7gk 1/1 Running 0 24s hamster-78f9dcdd4c-j9mc7 1/1 Running 0 24s`

View the CPU and Memory reservations on one of the pods using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`hamster: Container ID: containerd:// Image: k8s.gcr.io/ubuntu-slim:0.1 Image ID: sha256: Port: <none> Host Port: <none> Command: /bin/sh Args: -c while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done State: Running Started: Wed, 28 Sep 2022 15:06:14 -0400 Ready: True Restart Count: 0 Requests: cpu: 100m memory: 50Mi Environment: <none>`

The pod has 100 millicpu and 50 Mibibytes of Memory reserved in this example. For this sample application, the pod needs less than 100 millicpu to run, so there's no CPU capacity available. The pods also reserves less memory than needed. The Vertical Pod Autoscaler

*vpa-recommender*deployment analyzes the pods hosting the hamster application to see if the CPU and Memory requirements are appropriate. If adjustments are needed, the vpa-updater relaunches the pods with updated values.Monitor the pods using the

command.`kubectl get`

`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, you can view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

In the previous output, you can see that the CPU reservation increased to 587 millicpu, which is over five times the original value. The Memory increased to 262,144 Kilobytes, which is around 250 Mibibytes, or five times the original value. This pod was under-resourced, and the Vertical Pod Autoscaler corrected the estimate with a much more appropriate value.

View updated recommendations from VPA using the

command to describe the hamster-vpa resource information.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`


## Set Vertical Pod Autoscaler requests

The `VerticalPodAutoscaler`

object automatically sets resource requests on pods with an `updateMode`

of `Auto`

. You can set a different value depending on your requirements and testing. In this example, we create and test a deployment manifest with two pods, each running a container that requests 100 milliCPU and 50 MiB of Memory, and sets the `updateMode`

to `Recreate`

.

Create a file named

`azure-autodeploy.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: vpa-auto-deployment spec: replicas: 2 selector: matchLabels: app: vpa-auto-deployment template: metadata: labels: app: vpa-auto-deployment spec: containers: - name: mycontainer image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: ["-c", "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"]`

Create the pod using the

command.`kubectl create`

`kubectl create -f azure-autodeploy.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-kchc5 1/1 Running 0 52s vpa-auto-deployment-54465fb978-nhtmj 1/1 Running 0 52s`

Create a file named

`azure-vpa-auto.yaml`

and copy in the following manifest:`apiVersion: autoscaling.k8s.io/v1 kind: VerticalPodAutoscaler metadata: name: vpa-auto spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: vpa-auto-deployment updatePolicy: updateMode: "Recreate"`

The

`targetRef.name`

value specifies that any pod controlled by a deployment named`vpa-auto-deployment`

belongs to`VerticalPodAutoscaler`

. The`updateMode`

value of`Recreate`

means that the Vertical Pod Autoscaler controller can delete a pod, adjust the CPU and Memory requests, and then create a new pod.Apply the manifest to the cluster using the

command.`kubectl apply`

`kubectl create -f azure-vpa-auto.yaml`

Wait a few minutes and then view the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-qbhc4 1/1 Running 0 2m49s vpa-auto-deployment-54465fb978-vbj68 1/1 Running 0 109s`

Get detailed information about one of your running pods using the

command. Make sure you replace`kubectl get`

`<pod-name>`

with the name of one of your pods from your previous output.`kubectl get pod <pod-name> --output yaml`

Your output should look similar to the following example output, which shows that VPA controller increased the Memory request to 262144k and the CPU request to 25 milliCPU:

`apiVersion: v1 kind: Pod metadata: annotations: vpaObservedContainers: mycontainer vpaUpdates: 'Pod resources updated by vpa-auto: container 0: cpu request, memory request' creationTimestamp: "2022-09-29T16:44:37Z" generateName: vpa-auto-deployment-54465fb978- labels: app: vpa-auto-deployment spec: containers: - args: - -c - while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done command: - /bin/sh image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine imagePullPolicy: IfNotPresent name: mycontainer resources: requests: cpu: 25m memory: 262144k`

Get detailed information about the Vertical Pod Autoscaler and its recommendations for CPU and Memory using the

command.`kubectl get`

`kubectl get vpa vpa-auto --output yaml`

Your output should look similar to the following example output:

`recommendation: containerRecommendations: - containerName: mycontainer lowerBound: cpu: 25m memory: 262144k target: cpu: 25m memory: 262144k uncappedTarget: cpu: 25m memory: 262144k upperBound: cpu: 230m memory: 262144k`

In this example, the results in the

`target`

attribute specify that it doesn't need to change the CPU or the Memory target for the container to run optimally. However, results can vary depending on the application and its resource utilization.The Vertical Pod Autoscaler uses the

`lowerBound`

and`upperBound`

attributes to decide whether to delete a pod and replace it with a new pod. If a pod has requests less than the lower bound or greater than the upper bound, the Vertical Pod Autoscaler deletes the pod and replaces it with a pod that meets the target attribute.

## Extra Recommender for Vertical Pod Autoscaler

The Recommender provides recommendations for resource usage based on real-time resource consumption. AKS deploys a Recommender when a cluster enables VPA. You can deploy a customized Recommender or an extra Recommender with the same image as the default one. The benefit of having a customized Recommender is that you can customize your recommendation logic. With an extra Recommender, you can partition VPAs to use different Recommenders.

In the following example, we create an extra Recommender, apply to an existing AKS cluster, and configure the VPA object to use the extra Recommender.

Create a file named

`extra_recommender.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: extra-recommender namespace: kube-system spec: replicas: 1 selector: matchLabels: app: extra-recommender template: metadata: labels: app: extra-recommender spec: serviceAccountName: vpa-recommender securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: recommender image: registry.k8s.io/autoscaling/vpa-recommender:0.13.0 imagePullPolicy: Always args: - --recommender-name=extra-recommender resources: limits: cpu: 200m memory: 1000Mi requests: cpu: 50m memory: 500Mi ports: - name: prometheus containerPort: 8942`

Deploy the

`extra-recomender.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f extra-recommender.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Create a file named

`hamster-extra-recommender.yaml`

and copy in the following manifest:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: recommenders: - name: 'extra-recommender' targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster updatePolicy: updateMode: "Auto" resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 # nobody containers: - name: hamster image: k8s.gcr.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

If

`memory`

isn't specified in`controlledResources`

, the Recommender doesn't respond to OOM events. In this example, we only set CPU in`controlledValues`

.`controlledValues`

allows you to choose whether to update the container's resource requests using the`RequestsOnly`

option, or by both resource requests and limits using the`RequestsAndLimits`

option. The default value is`RequestsAndLimits`

. If you use the`RequestsAndLimits`

option, requests are computed based on actual usage, and limits are calculated based on the current pod's request and limit ratio.For example, if you start with a pod that requests 2 CPUs and limits to 4 CPUs, VPA always sets the limit to be twice as much as requests. The same principle applies to Memory. When you use the

`RequestsAndLimits`

mode, it can serve as a blueprint for your initial application resource requests and limits.You can simplify the VPA object using

`Auto`

mode and computing recommendations for both CPU and Memory.Deploy the

`hamster-extra-recomender.yaml`

example using thecommand.`kubectl apply`

`kubectl apply -f hamster-extra-recommender.yaml`

Monitor your pods using the

`[kubectl get`

][kubectl-get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of your pod IDs.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

View updated recommendations from VPA using the

command.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none> Spec: recommenders: Name: customized-recommender`


## Troubleshoot the Vertical Pod Autoscaler

If you encounter issues with the Vertical Pod Autoscaler, you can troubleshoot the system components and custom resource definition to identify the problem.

Verify that all system components are running using the following command:

`kubectl get pods|grep vpa`

Your output should list

*three pods*: recommender, updater, and admission-controller, all with a status of`Running`

.For each of the pods returned in your previous output, verify that the system components are logging any errors using the following command:

`kubectl logs [pod name] | grep -e '^E[0-9]\{4\}'`

Verify that the custom resource definition was created using the following command:

`kubectl get customresourcedefinition | grep verticalpodautoscalers`


## Next steps

To learn more about the VPA object, see the [Vertical Pod Autoscaler API reference](vertical-pod-autoscaler-api-reference).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-cost -->

# Best practices for cost optimization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cost optimization is about maximizing the value of resources while minimizing unnecessary expenses within your cloud environment. This process involves identifying cost effective configuration options and implementing best practices to improve operational efficiency. An AKS environment can be optimized to minimize cost while taking into account performance and reliability requirements.

In this article, you learn about:

- Holistic monitoring and FinOps practices.
- Strategic infrastructure selection.
- Dynamic rightsizing and autoscaling.
- Leveraging Azure discounts for substantial savings.

## Embrace FinOps to build a cost saving culture

[Financial operations (FinOps)](https://www.finops.org/introduction/what-is-finops/) is a discipline that combines financial accountability with cloud management and optimization. It focuses on driving alignment between finance, operations, and engineering teams to understand and control cloud costs. The FinOps foundation has several notable projects, such as the [ FinOps Framework](https://finops.org/framework) and the

[.](https://focus.finops.org/)

**FOCUS Specification**For more information, see [What is FinOps?](/en-us/azure/cost-management-billing/finops/)

## Prepare the application environment

### Evaluate SKU family

It's important to evaluate the resource requirements of your application before deployment. Small development workloads have different infrastructure needs than large production ready workloads. While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, consider the following virtual machine (VM) types:

| SKU family | Description | Use case |
|---|---|---|
Azure Spot Virtual Machines |

[Spot node pools](spot-node-pool)and deployed to a single fault domain with no high availability or service-level agreement (SLA) guarantees. Spot VMs allow you to take advantage of unutilized Azure capacity with significant discounts (up to 90%, as compared to pay-as-you-go prices). If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.**Arm-based processors (Arm64)**[Arm64 node pool support in AKS](use-arm64-vms), you can create Arm64 Ubuntu agent nodes and even mix Intel and ARM architecture nodes within a cluster. These ARM VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.**GPU optimized SKUs**[GPU-enabled Linux node pools on AKS](gpu-cluster)are best for compute-intensive workloads like graphics rendering, large model training, and inferencing.Note

The cost of compute varies across regions. When picking a less expensive region to run workloads, be conscious of the potential impact of latency as well as data transfer costs. To learn more about VM SKUs and their characteristics, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

### Review storage options

For more information on storage options and related cost considerations, see the following articles:

[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage)[Storage options for applications in Azure Kubernetes Service (AKS)](concepts-storage)

### Use cluster preset configurations

It can be difficult to pick the right VM SKU, regions, number of nodes, and other configuration options. [Cluster preset configurations](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal) in the Azure portal offloads this initial challenge by providing recommended configurations for different application environments that are cost-conscious and performant. The **Dev/Test** preset is best for developing new workloads or testing existing workloads. The **Production Economy** preset is best for serving production traffic in a cost-conscious way if your workloads can tolerate interruptions. Noncritical features are off by default, and the preset values can be modified at any time.

### Consider multitenancy

AKS offer flexibility in how you run multitenant clusters and isolate resources. For friendly multitenancy, you can share clusters and infrastructure across teams and business units through [ logical isolation](operator-best-practices-cluster-isolation#logically-isolated-clusters). Kubernetes

[Namespaces](concepts-clusters-workloads#namespaces)form the logical isolation boundary for workloads and resources. Sharing infrastructure reduces cluster management overhead while also improving resource utilization and pod density within the cluster. To learn more about multitenancy on AKS and to determine if it's right for your organizational needs, see

[AKS considerations for multitenancy](/en-us/azure/architecture/guide/multitenant/service/aks)and

[Design clusters for multitenancy](operator-best-practices-cluster-isolation#design-clusters-for-multi-tenancy).

Warning

Kubernetes environments aren't entirely safe for hostile multitenancy. If any tenant on the shared infrastructure can't be trusted, more planning is needed to prevent tenants from impacting the security of other services.

Consider [ physical isolation](operator-best-practices-cluster-isolation#physically-isolated-clusters) boundaries. In this model, teams or workloads are assigned to their own cluster. Added management and financial overhead will be a tradeoff.

## Build cloud native applications

### Make your container as lean as possible

A lean container refers to optimizing the size and resource footprint of the containerized application. Check that your base image is minimal and only contains the necessary dependencies. Remove any unnecessary libraries and packages. A smaller container image accelerates deployment times and increases the efficiency of scaling operations. [Artifact Streaming on AKS](artifact-streaming) allows you to stream container images from Azure Container Registry (ACR). It pulls only the necessary layer for initial pod startup, reducing the pull time for larger images from minutes to seconds.

### Enforce resource quotas

[Resource quotas](operator-best-practices-scheduler#enforce-resource-quotas) provide a way to reserve and limit resources across a development team or project. Quotas are defined on a namespace and can set on compute resources, storage resources, and object counts. When you define resource quotas, it prevents individual namespaces from consuming more resources than allocated. Resource quotas are useful for multitenant clusters where teams are sharing infrastructure.

### Use cluster start/stop

When left unattended, small development/test clusters can accrue unnecessary costs. You can turn off clusters that don't need to run at all times using the [cluster start and stop](start-stop-cluster?tabs=azure-cli) feature. This feature shuts down all system and user node pools so you don't pay for extra compute. The state of your cluster and objects is maintained when you start the cluster again.

### Use capacity reservations

Capacity reservations allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. Reserved capacity is available for immediate use until the reservation is deleted. [Associating an existing capacity reservation group to a node pool](manage-node-pools#associate-capacity-reservation-groups-to-node-pools) guarantees allocated capacity for your node pool and helps you avoid potential on-demand pricing spikes during periods of high compute demand.

## Monitor your environment and spend

### Increase visibility with Microsoft Cost Management

[Microsoft Cost Management](/en-us/azure/cost-management-billing/cost-management-billing-overview) offers a broad set of capabilities to help with cloud budgeting, forecasting, and visibility for costs both inside and outside of the cluster. Proper visibility is essential for deciphering spending trends, identifying optimization opportunities, and increasing accountability among application developers and platform teams. Enable the [AKS Cost Analysis add-on](cost-analysis) for granular cluster cost breakdown by Kubernetes constructs along with Azure Compute, Network, and Storage categories.

### Azure Monitor

If you're ingesting metric data via Container insights, we recommend migrating to managed Prometheus, which offers a significant cost reduction. You can [disable Container insights metrics using the data collection rule (DCR)](/en-us/azure/azure-monitor/containers/container-insights-data-collection-dcr?tabs=portal) and deploy the [managed Prometheus add-on](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana), which supports configuration via Azure Resource Manager, Azure CLI, Azure portal, and Terraform.

For more information, see [Azure Monitor best practices](/en-us/azure/azure-monitor/best-practices-containers#cost-optimization) and [managing costs for Container insights](/en-us/azure/azure-monitor/containers/container-insights-cost).

### Log Analytics

For control plane logs, consider disabling the categories you don't need and/or using the Basic Logs API when applicable to reduce Log Analytics costs. For more information, see [Azure Kubernetes Service (AKS) control plane/resource logs](monitor-aks#aks-control-plane-resource-logs). For data plane logs, or *application logs*, consider adjusting the [cost optimization settings](monitor-aks#aks-data-plane-container-insights-logs).

You can also use [Transformations in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations) to filter or modify control plane and data plane logs before they are sent to a Log Analytics workspace. For more information on how to create a transformation see [Create a transformation in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations-create?tabs=portal).

### Azure Advisor cost recommendations

AKS cost recommendations in Azure Advisor provide recommendations to help you achieve cost-efficiency without sacrificing reliability. Advisor analyzes your resource configurations and recommends optimization solutions. For more information, see [Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor](cost-advisors).

## Optimize workloads through autoscaling

### Establish a baseline

Before configuring your autoscaling settings, you can use [Azure Load Testing](/en-us/azure/load-testing/overview-what-is-azure-load-testing) to establish a baseline for your application. Load testing helps you understand how your application behaves under different traffic conditions and identify performance bottlenecks. Once you have a baseline, you can configure autoscaling settings to ensure your application can handle the expected load.

### Enable application autoscaling

#### Vertical pod autoscaling

Requests and limits that are higher than actual usage can result in overprovisioned workloads and wasted resources. In contrast, requests and limits that are too low can result in throttling and workload issues due to lack of memory. The [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) allows you to fine-tune CPU and memory resources required by your pods. VPA provides recommended values for CPU and memory requests and limits based on historical container usage, which you can set manually or update automatically. * Best for applications with fluctuating resource demands*. VPA’s recommendation-only

*off mode*allows teams to review resource suggestions without enforcing them automatically. This mode can be enabled during testing, and VPA recommendations can be used to set the CPU and memory request and limits for production environments.

#### Horizontal pod autoscaling

The [Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler) dynamically scales the number of pod replicas based on observed metrics, such as CPU or memory utilization. During periods of high demand, HPA scales out, adding more pod replicas to distribute the workload. During periods of low demand, HPA scales in, reducing the number of replicas to conserve resources. * Best for applications with predictable resource demands*.

Warning

You shouldn't use the VPA with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

#### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA) add-on](keda-about) provides extra flexibility to scale based on various event-driven metrics that align with your application behavior. For example, for a web application, KEDA can monitor incoming HTTP request traffic and adjust the number of pod replicas to ensure the application remains responsive. For processing jobs, KEDA can scale the application based on message queue length. Managed support is provided for all [Azure Scalers](https://keda.sh/docs/2.13/scalers/). KEDA also allows you to scale down to 0 replicas, especially helpful for sporadic event-driven workloads, periodic machine learning (ML) or GPU workloads, and dev/test or low traffic environments.

### Enable infrastructure autoscaling

#### Cluster autoscaling

To keep up with application demand, the [Cluster Autoscaler](cluster-autoscaler-overview) watches for pods that can't be scheduled due to resource constraints and scales the number of nodes in the node pool accordingly. When nodes don't have running pods, the Cluster Autoscaler scales down the number of nodes. The Cluster Autoscaler profile settings apply to all autoscaler-enabled node pools in a cluster. For more information, see [Cluster Autoscaler best practices and considerations](cluster-autoscaler-overview#best-practices-and-considerations).

#### Node autoprovisioning

Complicated workloads might require several node pools with different VM size configurations to accommodate CPU and memory requirements. Accurately selecting and managing several node pool configurations adds complexity and operational overhead. [Node Autoprovision (NAP)](node-autoprovision?tabs=azure-cli) simplifies the SKU selection process and decides the optimal VM configuration based on pending pod resource requirements to run workloads in the most efficient and cost effective manner.

Note

For more information on scaling best practices, see [Performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale) and [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

## Save with Azure discounts

### Azure Reservations

If your workload is predictable and exists for an extended period of time, consider purchasing an [Azure Reservation](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) to further reduce your resource costs. Azure Reservations operate on a one-year or three-year term, offering up to 72% discount as compared to pay-as-you-go prices for compute. Reservations automatically apply to matching resources. * Best for workloads that are committed to running in the same SKUs and regions over an extended period of time*.

### Azure Savings Plan

If you have consistent spend, but your use of disparate resources across SKUs and regions makes Azure Reservations infeasible, consider purchasing an [Azure Savings Plan](/en-us/azure/cost-management-billing/savings-plan/savings-plan-compute-overview). Like Azure Reservations, Azure Savings Plans operate on a one-year or three-year term and automatically apply to any resources within benefit scope. You commit to spend a fixed hourly amount on compute resources irrespective of SKU or region. * Best for workloads that utilize different resources and/or different data center regions*.

### Azure Hybrid Benefit

[Azure Hybrid Benefit for Azure Kubernetes Service (AKS)](azure-hybrid-benefit) allows you to maximize your on-premises licenses at no extra cost. Use any qualifying on-premises licenses that also have an active Software Assurance (SA) or a qualifying subscription to get Windows VMs on Azure at a reduced cost.

## Next steps

Cost optimization is an ongoing and iterative effort. Learn more by reviewing the following recommendations and architecture guidance:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/postgresql-ha-overview -->

# Overview of deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this guide, you deploy a highly available PostgreSQL cluster that spans multiple Azure availability zones on AKS with Azure CLI.

This article walks through the prerequisites for setting up a PostgreSQL cluster on [Azure Kubernetes Service (AKS)](what-is-aks) and provides an overview of the full deployment process and architecture.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Prerequisites

- This guide assumes a basic understanding of
[core Kubernetes concepts](concepts-clusters-workloads)and[PostgreSQL](https://www.postgresql.org/). - You need the
**Owner**or**User Access Administrator**and the**Contributor**[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)on a subscription in your Azure account.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


You also need the following resources installed:

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.56 or later.[jq](https://jqlang.github.io/jq/), version 1.5 or later.[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)version 1.21.0 or later.[Helm](https://helm.sh/docs/intro/install/)version 3.0.0 or later.[openssl](https://www.openssl.org/)version 3.3.0 or later.[Visual Studio Code](https://code.visualstudio.com/Download)or equivalent.[Krew](https://krew.sigs.k8s.io/)version 0.4.4 or later.[kubectl CloudNativePG (CNPG) Plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew).


## Deployment process

In this guide, you learn how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the
[CNPG operator](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). - Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to a PostgreSQL database.
- Perform PostgreSQL and AKS cluster upgrades.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform backup and restore of a PostgreSQL database.

## Deployment architecture

This diagram illustrates a PostgreSQL cluster setup with one primary replica and two read replicas managed by the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator. The architecture provides a highly available PostgreSQL running on an AKS cluster that can withstand a zone outage by failing over across replicas.

Backups are stored on [Azure Blob Storage](/en-us/azure/storage/blobs/), providing another way to restore the database in the event of an issue with streaming replication from the primary replica.

You might choose to host PostgreSQL on AKS when you need full control over database configuration, extensions, and deployment architecture. It’s ideal for integrating tightly with Kubernetes-native tooling, optimizing costs at scale, and fine-tuning performance through custom resource allocation, caching strategies, and storage configurations tailored to your workload.

Note

For applications that require data separation at the database level, you can add more databases with postInitSQL commands and similar. It's currently not possible to add more databases in a declarative way with the CNPG operator. [Learn more](https://github.com/cloudnative-pg/cloudnative-pg) about the CNPG operator.

### Storage considerations

The type of storage you use can have large effects on PostgreSQL performance. Later in this guide, you select the option best suited for your goals and performance needs.

| Storage type | Compatible driver | Description |
|---|---|---|
|

**Maximum data resiliency**. Azure Premium SSD delivers high-performance storage and seamlessly works with Azure Premium zone-redundant storage (ZRS). Premium SSD is provisioned based on specific sizes, which each offer certain IOPS and throughput levels.[Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2)**Best price-performance**. Azure Premium SSD v2 offers higher performance than Azure Premium SSDs while also generally being less costly. Unlike Premium SSDs, Premium SSD v2 doesn't have dedicated sizes. You can set a Premium SSD v2 to any supported size you prefer, and make granular adjustments to the performance without downtime. Azure Premium SSD v2 disks have certain limitations that you should be aware of. For a complete list, see[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).[Local NVMe or temp SSD (Ephemeral Disks)](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk#what-is-ephemeral-disk)**Maximum performance**. Ephemeral Disks are local NVMe and temporary SSD storage available on select VM families. They offer the highest possible IOPS, throughput, and submillisecond latency for your AKS cluster. You can also take advantage of Ephemeral Disks' high performance using[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), a managed Kubernetes storage solution that dynamically provisions persistent volumes for stateful workloads like PostgreSQL. However, because these disks reside on the local VMs hosting the cluster, data isn't persisted to an Azure storage service. As a result, any data stored on these disks will be lost if the cluster is stopped or deallocated. To address this limitation, later sections in this guide show you how to set up periodic backups of your PostgreSQL data to[Azure Blob Storage](/en-us/azure/storage/blobs/).## Next steps

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr -->

# Tutorial - Create an Azure Container Registry (ACR) and build images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Container Registry (ACR) is a private registry for container images. A private container registry allows you to securely build and deploy your applications and custom code.

In this tutorial, you deploy an ACR instance and push a container image to it. You learn how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

## Before you begin

In the [previous tutorial](tutorial-kubernetes-prepare-app), you used Docker to create a container image for a simple Azure Store Front application. If you haven't created the Azure Store Front app image, return to [Tutorial 1 - Prepare an application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an Azure Container Registry

Before creating an ACR instance, you need a resource group. An Azure resource group is a logical container into which you deploy and manage Azure resources.

Important

This tutorial uses *myResourceGroup* as a placeholder for the resource group name. If you want to use a different name, replace *myResourceGroup* with your own resource group name.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location westus2`

Create an ACR instance using the

command and provide your own unique registry name. The registry name must be unique within Azure and contain 5-50 lowercase alphanumeric characters. This tutorial series uses an environment variable,`az acr create`

`$ACRNAME`

, as a placeholder for the container registry name. You can set this environment variable to your unique ACR name to use in future commands. The*Basic*SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.`az acr create --resource-group myResourceGroup --name $ACRNAME --sku Basic`


## Build and push container images to registry

Build and push the images to your ACR using the Azure CLI

command.`az acr build`

Note

For this step, there isn't an equivalent Azure PowerShell cmdlet that performs this task.

In the following example, we don't build the

`product-service`

image. This image can take a long time to build, and there's a container image already available in the GitHub Container Registry (GHCR). You can use thecommand to import the image from the GHCR to your ACR instance. We also don't build the`az acr import`

`rabbitmq`

image. This image is available from the Docker Hub public repository and doesn't need to be built or pushed to your ACR instance.`az acr import --name $ACRNAME --source ghcr.io/azure-samples/aks-store-demo/product-service:latest --image aks-store-demo/product-service:latest az acr build --registry $ACRNAME --image aks-store-demo/order-service:latest ./src/order-service/ az acr build --registry $ACRNAME --image aks-store-demo/store-front:latest ./src/store-front/`


## List images in registry

View the images in your ACR instance using the

command.`az acr repository list`

`az acr repository list --name $ACRNAME --output table`

The following example output lists the available images in your registry:

`Result ---------------- aks-store-demo/product-service aks-store-demo/order-service aks-store-demo/store-front`


## Next steps

In this tutorial, you created an ACR and pushed images to it to use in an AKS cluster. You learned how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

In the next tutorial, you learn how to deploy a Kubernetes cluster in Azure.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-metrics-managed-prometheus -->

# Collect metrics for Istio service mesh add-on workloads for Azure Kubernetes Service in Azure Managed Prometheus

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide explains how to set up and use Azure Managed Prometheus to collect metrics from Istio service mesh add-on workloads on your Azure Kubernetes cluster.

## Prerequisites

Complete steps to enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)

## Enable Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus collects data from Azure Kubernetes cluster.
To enable Azure Monitor managed service for Prometheus, you must create an [Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage?tabs=cli#create-an-azure-monitor-workspace) to store the metrics:

```
export AZURE_MONITOR_WORKSPACE=<azure-monitor-workspace-name>
export AZURE_MONITOR_WORKSPACE_ID=$(az monitor account create \
--name $AZURE_MONITOR_WORKSPACE \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--query id -o tsv)
```


### Enable Prometheus addon

To collect Prometheus metrics from your Kubernetes cluster, [enable Prometheus addon](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable?tabs=cli#enable-with-cli):

```
az aks update --enable-azure-monitor-metrics --name $CLUSTER --resource-group $RESOURCE_GROUP --azure-monitor-workspace-resource-id $AZURE_MONITOR_WORKSPACE_ID
```


### Customize scraping of Prometheus metrics in Azure Monitor managed service

Create a scrape config in a file named `prometheus-config`

, similar to the sample provided below. This configuration enables pod annotation-based scraping, which allows Prometheus to automatically discover and scrape metrics from pods with specific annotations.

Important

The scrape config below is just an example. We **highly** recommend customizing it based on your needs. If not adjusted, it could lead to unexpected costs from frequent metric collection and increased data storage.

```
global:
scrape_interval: 30s
scrape_configs:
- job_name: workload
scheme: http
kubernetes_sd_configs:
- role: endpoints
relabel_configs:
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
action: keep
regex: true
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
action: replace
target_label: __metrics_path__
regex: (.+)
- source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
action: replace
regex: ([^:]+)(?::\d+)?;(\d+)
replacement: $1:$2
target_label: __address__
```


To [enable pod annotation-based scraping](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration), create configmap `ama-metrics-prometheus-config`

that references `prometheus-config`

file in `kube-system`

namespace.

```
kubectl create configmap ama-metrics-prometheus-config --from-file=prometheus-config -n kube-system
```


### Verify Metric Collection

Configure access permissions: navigate to your Azure Monitor workspace in Azure portal and create role assignment for yourself to grant 'Monitoring Data Reader' role on the workspace resource.

Generate sample traffic: send a few requests to the product page created earlier, for example:

`curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"`

View/Query metrics in Azure portal: navigate to Prometheus explorer under your Azure Monitor workspace and

[query metrics](/en-us/azure/azure-monitor/essentials/prometheus-workbooks). The example below shows results for query`istio_requests_total`

.

## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-cluster -->

# Use GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Linux node pools to run compute-intensive Kubernetes workloads.

This article helps you provision nodes with schedulable GPUs on new and existing AKS clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported GPU-enabled VMs

To view the available GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). If a GPU VM size is not in our list of supported VM sizes, AKS does not install the necessary GPU software components or provide support. AKS allows the use of unsupported GPU VM sizes after [skipping the automatic GPU driver installation](#skip-gpu-driver-installation).

Check available and supported VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm) command.

```
az vm list-skus --location <your-location> --output table
```


For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- If you're using an Azure Linux GPU-enabled node pool, automatic security patches aren't applied. Refer to your current AKS API version for the default behavior of node OS upgrade channel.
[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)isn't supported with NVIDIA GPU on AKS.[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)isn't supported with NVIDIA GPU on AKS.

Note

For AKS API version 2023-06-01 or later, the default channel for node OS upgrade is *NodeImage*. For previous versions, the default channel is *None*. To learn more, see [auto-upgrade](auto-upgrade-node-image).

- Updating an existing node pool to add GPU VM size is not supported on AKS.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the

*myAKSCluster*in the

*myResourceGroup*resource group:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


## Options for using NVIDIA GPUs

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), GPU driver installation, and more.

Note

By default, Microsoft automatically maintains the version of the NVIDIA drivers as part of the node image deployment, and AKS * supports and manages* it. While the NVIDIA drivers are installed by default on GPU capable nodes, you need to install the device plugin.

### NVIDIA device plugin installation

NVIDIA device plugin installation is required when using GPUs on AKS. In some cases, the installation is handled automatically, such as when using the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html). Alternatively, you can manually install the NVIDIA device plugin.

#### Manually install the NVIDIA device plugin

You can deploy a DaemonSet for the NVIDIA device plugin, which runs a pod on each node to provide the required drivers for the GPUs. This is the recommended approach when using GPU-enabled node pools for Azure Linux.

To use the default OS SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--node-vm-size Standard_NC6s_v3 \
--node-taints sku=gpu:NoSchedule \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3
```


This command adds a node pool named *gpunp* to *myAKSCluster* in *myResourceGroup* and uses parameters to configure the following node pool settings:

`--node-vm-size`

: Sets the VM size for the node in the node pool to*Standard_NC6s_v3*.`--node-taints`

: Specifies a*sku=gpu:NoSchedule*taint on the node pool.`--enable-cluster-autoscaler`

: Enables the cluster autoscaler.`--min-count`

: Configures the cluster autoscaler to maintain a minimum of one node in the node pool.`--max-count`

: Configures the cluster autoscaler to maintain a maximum of three nodes in the node pool.

Note

Taints and VM sizes can only be set for node pools during node pool creation, but you can update autoscaler settings at any time.

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*nvidia-device-plugin-ds.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin/blob/4b3d6b0a6613a3672f71ea4719fd8633eaafb4f3/deployments/static/nvidia-device-plugin.yml):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: labels: name: nvidia-device-plugin-ds spec: tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" # Mark this pod as a critical add-on; when enabled, the critical add-on # scheduler reserves resources for critical add-on pods so that they can # be rescheduled after a failure. # See https://kubernetes.io/docs/tasks/administer-cluster/guaranteed-scheduling-critical-addon-pods/ priorityClassName: "system-node-critical" containers: - image: nvcr.io/nvidia/k8s-device-plugin:v0.18.0 name: nvidia-device-plugin-ctr env: - name: FAIL_ON_INIT_ERROR value: "false" securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable)and[run a GPU workload](#run-a-gpu-enabled-workload).

### Skip GPU driver installation

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can skip the default GPU driver installation. Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and set`az aks nodepool add`

`--gpu-driver`

field to`none`

to skip default GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --gpu-driver none \ --node-vm-size Standard_NC6s_v3 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

Setting the

`--gpu-driver`

API field to`none`

during node pool creation skips the automatic GPU driver installation. Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.If you get the error

`unrecognized arguments: --gpu-driver none`

then[update the Azure CLI version](/en-us/cli/azure/update-azure-cli). For more information, see[Before you begin](#before-you-begin).You can optionally install the NVIDIA GPU Operator following

[these steps](nvidia-gpu-operator).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`nvidia.com/gpu: 1`

. Your output should look similar to the following condensed example output:`Name: aks-gpunp-28993262-0 Roles: agent Labels: accelerator=nvidia [...] Capacity: [...] nvidia.com/gpu: 1 [...]`


## Run a GPU-enabled workload

To see the GPU in action, you can schedule a GPU-enabled workload with the appropriate resource request. In this example, we'll run a [Tensorflow](https://www.tensorflow.org/) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).

Create a file named

*samples-tf-mnist-demo.yaml*and paste the following YAML manifest, which includes a resource limit of`nvidia.com/gpu: 1`

:Note

If you receive a version mismatch error when calling into drivers, such as "CUDA driver version is insufficient for CUDA runtime version", review the

[NVIDIA driver matrix compatibility chart](https://docs.nvidia.com/deploy/cuda-compatibility/index.html).`apiVersion: batch/v1 kind: Job metadata: labels: app: samples-tf-mnist-demo name: samples-tf-mnist-demo spec: template: metadata: labels: app: samples-tf-mnist-demo spec: containers: - name: samples-tf-mnist-demo image: mcr.microsoft.com/azuredocs/samples-tf-mnist-demo:gpu args: ["--max_steps", "500"] imagePullPolicy: IfNotPresent resources: limits: nvidia.com/gpu: 1 restartPolicy: OnFailure tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule"`

Run the job using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f samples-tf-mnist-demo.yaml`


## View the status of the GPU-enabled workload

Monitor the progress of the job using the

command with the`kubectl get jobs`

`--watch`

flag. It may take a few minutes to first pull the image and process the dataset.`kubectl get jobs samples-tf-mnist-demo --watch`

When the

*COMPLETIONS*column shows*1/1*, the job has successfully finished, as shown in the following example output:`NAME COMPLETIONS DURATION AGE samples-tf-mnist-demo 0/1 3m29s 3m29s samples-tf-mnist-demo 1/1 3m10s 3m36s`

Exit the

`kubectl --watch`

process with*Ctrl-C*.Get the name of the pod using the

command.`kubectl get pods`

`kubectl get pods --selector app=samples-tf-mnist-demo`

View the output of the GPU-enabled workload using the

command.`kubectl logs`

`kubectl logs samples-tf-mnist-demo-smnr6`

The following condensed example output of the pod logs confirms that the appropriate GPU device,

`Tesla K80`

, has been discovered:`2019-05-16 16:08:31.258328: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA 2019-05-16 16:08:31.396846: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties: name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235 pciBusID: 2fd7:00:00.0 totalMemory: 11.17GiB freeMemory: 11.10GiB 2019-05-16 16:08:31.396886: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: Tesla K80, pci bus id: 2fd7:00:00.0, compute capability: 3.7) 2019-05-16 16:08:36.076962: I tensorflow/stream_executor/dso_loader.cc:139] successfully opened CUDA library libcupti.so.8.0 locally Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes. Extracting /tmp/tensorflow/input_data/train-images-idx3-ubyte.gz Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes. Extracting /tmp/tensorflow/input_data/train-labels-idx1-ubyte.gz Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes. Extracting /tmp/tensorflow/input_data/t10k-images-idx3-ubyte.gz Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes. Extracting /tmp/tensorflow/input_data/t10k-labels-idx1-ubyte.gz Accuracy at step 0: 0.1081 Accuracy at step 10: 0.7457 Accuracy at step 20: 0.8233 Accuracy at step 30: 0.8644 Accuracy at step 40: 0.8848 Accuracy at step 50: 0.8889 Accuracy at step 60: 0.8898 Accuracy at step 70: 0.8979 Accuracy at step 80: 0.9087 Accuracy at step 90: 0.9099 Adding run metadata for 99 Accuracy at step 100: 0.9125 Accuracy at step 110: 0.9184 Accuracy at step 120: 0.922 Accuracy at step 130: 0.9161 Accuracy at step 140: 0.9219 Accuracy at step 150: 0.9151 Accuracy at step 160: 0.9199 Accuracy at step 170: 0.9305 Accuracy at step 180: 0.9251 Accuracy at step 190: 0.9258 Adding run metadata for 199 [...] Adding run metadata for 499`


## Upgrading a node pool

Whether you want to [update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) or [upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) your node pools, you might notice that there is no `--gpu-driver`

parameter for either operation. You might run into an error like `unrecognized arguments: --gpu-driver none`

if you attempt to pass the parameter. There is no need to call on the parameter, as the value is not affected by any such operations.

When you first create your node pool, whatever parameter you declare for `--gpu-driver`

will not be impacted by upgrade/update operations. If you don't want any drivers to be installed, and selected `--gpu-driver None`

when creating your node pool, drivers will not be installed in any subsequent updates/upgrades.

## Clean up resources

Remove the associated Kubernetes objects you created in this article using the [ kubectl delete job](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete jobs samples-tf-mnist-demo
```


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-nvidia-gpu -->

# Use GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Linux node pools to run compute-intensive Kubernetes workloads.

This article helps you provision nodes with schedulable GPUs on new and existing AKS clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported GPU-enabled VMs

To view the available GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). If a GPU VM size is not in our list of supported VM sizes, AKS does not install the necessary GPU software components or provide support. AKS allows the use of unsupported GPU VM sizes after [skipping the automatic GPU driver installation](#skip-gpu-driver-installation).

Check available and supported VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm) command.

```
az vm list-skus --location <your-location> --output table
```


For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- If you're using an Azure Linux GPU-enabled node pool, automatic security patches aren't applied. Refer to your current AKS API version for the default behavior of node OS upgrade channel.
[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)isn't supported with NVIDIA GPU on AKS.[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)isn't supported with NVIDIA GPU on AKS.

Note

For AKS API version 2023-06-01 or later, the default channel for node OS upgrade is *NodeImage*. For previous versions, the default channel is *None*. To learn more, see [auto-upgrade](auto-upgrade-node-image).

- Updating an existing node pool to add GPU VM size is not supported on AKS.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the

*myAKSCluster*in the

*myResourceGroup*resource group:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


## Options for using NVIDIA GPUs

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), GPU driver installation, and more.

Note

By default, Microsoft automatically maintains the version of the NVIDIA drivers as part of the node image deployment, and AKS * supports and manages* it. While the NVIDIA drivers are installed by default on GPU capable nodes, you need to install the device plugin.

### NVIDIA device plugin installation

NVIDIA device plugin installation is required when using GPUs on AKS. In some cases, the installation is handled automatically, such as when using the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html). Alternatively, you can manually install the NVIDIA device plugin.

#### Manually install the NVIDIA device plugin

You can deploy a DaemonSet for the NVIDIA device plugin, which runs a pod on each node to provide the required drivers for the GPUs. This is the recommended approach when using GPU-enabled node pools for Azure Linux.

To use the default OS SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--node-vm-size Standard_NC6s_v3 \
--node-taints sku=gpu:NoSchedule \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3
```


This command adds a node pool named *gpunp* to *myAKSCluster* in *myResourceGroup* and uses parameters to configure the following node pool settings:

`--node-vm-size`

: Sets the VM size for the node in the node pool to*Standard_NC6s_v3*.`--node-taints`

: Specifies a*sku=gpu:NoSchedule*taint on the node pool.`--enable-cluster-autoscaler`

: Enables the cluster autoscaler.`--min-count`

: Configures the cluster autoscaler to maintain a minimum of one node in the node pool.`--max-count`

: Configures the cluster autoscaler to maintain a maximum of three nodes in the node pool.

Note

Taints and VM sizes can only be set for node pools during node pool creation, but you can update autoscaler settings at any time.

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*nvidia-device-plugin-ds.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin/blob/4b3d6b0a6613a3672f71ea4719fd8633eaafb4f3/deployments/static/nvidia-device-plugin.yml):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: labels: name: nvidia-device-plugin-ds spec: tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" # Mark this pod as a critical add-on; when enabled, the critical add-on # scheduler reserves resources for critical add-on pods so that they can # be rescheduled after a failure. # See https://kubernetes.io/docs/tasks/administer-cluster/guaranteed-scheduling-critical-addon-pods/ priorityClassName: "system-node-critical" containers: - image: nvcr.io/nvidia/k8s-device-plugin:v0.18.0 name: nvidia-device-plugin-ctr env: - name: FAIL_ON_INIT_ERROR value: "false" securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable)and[run a GPU workload](#run-a-gpu-enabled-workload).

### Skip GPU driver installation

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can skip the default GPU driver installation. Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and set`az aks nodepool add`

`--gpu-driver`

field to`none`

to skip default GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --gpu-driver none \ --node-vm-size Standard_NC6s_v3 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

Setting the

`--gpu-driver`

API field to`none`

during node pool creation skips the automatic GPU driver installation. Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.If you get the error

`unrecognized arguments: --gpu-driver none`

then[update the Azure CLI version](/en-us/cli/azure/update-azure-cli). For more information, see[Before you begin](#before-you-begin).You can optionally install the NVIDIA GPU Operator following

[these steps](nvidia-gpu-operator).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`nvidia.com/gpu: 1`

. Your output should look similar to the following condensed example output:`Name: aks-gpunp-28993262-0 Roles: agent Labels: accelerator=nvidia [...] Capacity: [...] nvidia.com/gpu: 1 [...]`


## Run a GPU-enabled workload

To see the GPU in action, you can schedule a GPU-enabled workload with the appropriate resource request. In this example, we'll run a [Tensorflow](https://www.tensorflow.org/) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).

Create a file named

*samples-tf-mnist-demo.yaml*and paste the following YAML manifest, which includes a resource limit of`nvidia.com/gpu: 1`

:Note

If you receive a version mismatch error when calling into drivers, such as "CUDA driver version is insufficient for CUDA runtime version", review the

[NVIDIA driver matrix compatibility chart](https://docs.nvidia.com/deploy/cuda-compatibility/index.html).`apiVersion: batch/v1 kind: Job metadata: labels: app: samples-tf-mnist-demo name: samples-tf-mnist-demo spec: template: metadata: labels: app: samples-tf-mnist-demo spec: containers: - name: samples-tf-mnist-demo image: mcr.microsoft.com/azuredocs/samples-tf-mnist-demo:gpu args: ["--max_steps", "500"] imagePullPolicy: IfNotPresent resources: limits: nvidia.com/gpu: 1 restartPolicy: OnFailure tolerations: - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule"`

Run the job using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f samples-tf-mnist-demo.yaml`


## View the status of the GPU-enabled workload

Monitor the progress of the job using the

command with the`kubectl get jobs`

`--watch`

flag. It may take a few minutes to first pull the image and process the dataset.`kubectl get jobs samples-tf-mnist-demo --watch`

When the

*COMPLETIONS*column shows*1/1*, the job has successfully finished, as shown in the following example output:`NAME COMPLETIONS DURATION AGE samples-tf-mnist-demo 0/1 3m29s 3m29s samples-tf-mnist-demo 1/1 3m10s 3m36s`

Exit the

`kubectl --watch`

process with*Ctrl-C*.Get the name of the pod using the

command.`kubectl get pods`

`kubectl get pods --selector app=samples-tf-mnist-demo`

View the output of the GPU-enabled workload using the

command.`kubectl logs`

`kubectl logs samples-tf-mnist-demo-smnr6`

The following condensed example output of the pod logs confirms that the appropriate GPU device,

`Tesla K80`

, has been discovered:`2019-05-16 16:08:31.258328: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA 2019-05-16 16:08:31.396846: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties: name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235 pciBusID: 2fd7:00:00.0 totalMemory: 11.17GiB freeMemory: 11.10GiB 2019-05-16 16:08:31.396886: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: Tesla K80, pci bus id: 2fd7:00:00.0, compute capability: 3.7) 2019-05-16 16:08:36.076962: I tensorflow/stream_executor/dso_loader.cc:139] successfully opened CUDA library libcupti.so.8.0 locally Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes. Extracting /tmp/tensorflow/input_data/train-images-idx3-ubyte.gz Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes. Extracting /tmp/tensorflow/input_data/train-labels-idx1-ubyte.gz Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes. Extracting /tmp/tensorflow/input_data/t10k-images-idx3-ubyte.gz Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes. Extracting /tmp/tensorflow/input_data/t10k-labels-idx1-ubyte.gz Accuracy at step 0: 0.1081 Accuracy at step 10: 0.7457 Accuracy at step 20: 0.8233 Accuracy at step 30: 0.8644 Accuracy at step 40: 0.8848 Accuracy at step 50: 0.8889 Accuracy at step 60: 0.8898 Accuracy at step 70: 0.8979 Accuracy at step 80: 0.9087 Accuracy at step 90: 0.9099 Adding run metadata for 99 Accuracy at step 100: 0.9125 Accuracy at step 110: 0.9184 Accuracy at step 120: 0.922 Accuracy at step 130: 0.9161 Accuracy at step 140: 0.9219 Accuracy at step 150: 0.9151 Accuracy at step 160: 0.9199 Accuracy at step 170: 0.9305 Accuracy at step 180: 0.9251 Accuracy at step 190: 0.9258 Adding run metadata for 199 [...] Adding run metadata for 499`


## Upgrading a node pool

Whether you want to [update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) or [upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) your node pools, you might notice that there is no `--gpu-driver`

parameter for either operation. You might run into an error like `unrecognized arguments: --gpu-driver none`

if you attempt to pass the parameter. There is no need to call on the parameter, as the value is not affected by any such operations.

When you first create your node pool, whatever parameter you declare for `--gpu-driver`

will not be impacted by upgrade/update operations. If you don't want any drivers to be installed, and selected `--gpu-driver None`

when creating your node pool, drivers will not be installed in any subsequent updates/upgrades.

## Clean up resources

Remove the associated Kubernetes objects you created in this article using the [ kubectl delete job](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete jobs samples-tf-mnist-demo
```


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-wireguard-encryption-concepts -->

# In transit encryption with WireGuard (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As organizations increasingly rely on Azure Kubernetes Service (AKS) to run containerized workloads, ensuring the security of network traffic between applications and services becomes essential especially in regulated or security-sensitive environments. In-transit encryption with WireGuard protects data as it moves between pods and nodes, mitigating risks of interception or tampering. WireGuard is known for its simplicity, and robust cryptography, offers a powerful solution for securing communication within AKS clusters.

WireGuard encryption for AKS is part of the [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) feature set, and its implementation is based on [Cilium](https://docs.cilium.io/en/stable/security/network/encryption-wireguard/).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## WireGuard encryption scope

WireGuard in-transit encryption in AKS is designed to secure specific traffic flows within your Kubernetes cluster. This section outlines which traffic types are encrypted and which aren't currently supported via Advanced Container Networking Services(ACNS).

Supported/Encrypted traffic flows:

- Inter-node pod traffic: Traffic leaving a pod from one node destined to a pod on another node.

Unsupported/Unencrypted traffic flows

- Same-node pod traffic: Traffic between pods on the same node
- Node-network traffic: traffic generated by the node itself destined to another node

## Architecture overview

WireGuard encryption relies on [Azure CNI powered by cilium](azure-cni-powered-by-cilium) to secure inter-node communications within a distributed system. The architecture uses a dedicated WireGuard agent that orchestrates key management, interface configuration, and dynamic peer updates. This section attempts to provide a detailed explanation

### WireGuard agent

Upon startup, the Cilium agent evaluates its configuration to determine if encryption is enabled. When WireGuard is selected as the encryption mode, the agent initializes a dedicated WireGuard subsystem. The wireguard agent is responsible for configuring and initializing components required for enforcing WireGuard encryption.

### Key generation

A fundamental requirement to secure communication is the generation of cryptographic key pairs. Each node in the Kubernetes cluster will automatically generate a unique WireGuard key pair during the initialization phase and distributes its public key via the “network.cilium.io/wg-pub-key” annotation in the Kubernetes CiliumNode custom resource object. The key pairs are stored in memory and rotated every 120 seconds. The private key serves as the node’s confidential identity. The public key is shared with the peer nodes in the cluster to decrypt and encrypt traffic from and to Cilium-managed endpoints running on that node. These keys are managed entirely by Azure, not by the customer, ensuring secure and automated handling without requiring manual intervention. This mechanism ensures that only nodes with validated credentials can participate in the encrypted network.

### Interface creation

Once the key generation process concludes, the WireGuard agent configures a dedicated network interface (cilium_wg0). This process involves interface creation and configuration with the previously generated private key.

## Comparison with virtual network encryption

Azure offers multiple options for securing in-transit traffic in AKS, including [virtual network level encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview) and WireGuard-based encryption. While both approaches enhance the confidentiality and integrity of network traffic, they differ in scope, flexibility, and deployment requirements. This section helps you understand when to use each solution.

**Use virtual network encryption when**

**You require full network-layer encryption for all traffic within the virtual network:**Virtual network encryption ensures that all traffic regardless of workload or orchestration layer is automatically encrypted as it traverses the Azure Virtual Network.**You need minimal performance overhead:**Virtual network encryption uses hardware acceleration in supported VM SKUs, offloading encryption from the OS to the underlying hardware. This design delivers high throughput with low CPU usage.**All your virtual machines support virtual network encryption:**Virtual network encryption depends on VM SKUs that support the necessary hardware acceleration. If your infrastructure consists entirely of supported SKUs, virtual network encryption can be seamlessly enabled.**Your AKS Network configurations supports virtual network encryption:**Virtual network encryption has some limitations when it comes to aks pod networking. For more information, see[Virtual network encryption supported scenarios](/en-us/azure/virtual-network/virtual-network-encryption-overview#supported-scenarios)

**Use WireGuard encryption When**

**You want to make sure that your application traffic is encrypted across all node**virtual network encryption does not encrypt traffic between nodes on the same physical host.**You want to unify encryption across multi-cloud or hybrid environments:**WireGuard offers a cloud-agnostic solution, enabling consistent encryption across clusters running in different cloud providers or on-premises.**You don’t need or want to encrypt all traffic within the virtual network:**WireGuard enables a more targeted encryption strategy ideal for securing sensitive workloads without incurring the overhead of encrypting all traffic.**Some of your VM SKUs don’t support virtual network encryption:**WireGuard is implemented in software and works regardless of VM hardware support, making it a practical option for heterogeneous environments.

## Considerations & limitations

• WireGuard isn't [FIPS](https://csrc.nist.gov/pubs/fips/140-2/upd2/final) compliant.
• WireGuard encryption doesn't apply to pods uses host networking (spec.hostNetwork: true) because these pods use the host identity instead of having individual identities.

Important

WireGuard encryption operates at the software level, which can introduce latency and impact throughput performance. The extent of this impact depends on various factors, including VM size (node SKU), network configuration, and application traffic patterns. Our benchmarking indicates that throughput is limited to 1.5 Gbps with an MTU of 1500; however, results may vary depending on workload characteristics and cluster configuration. Using a SKU that supports MTU 3900 resulted in approximately 2.5x higher throughput. While WireGuard encryption can be used alongside network policies, doing so may lead to further performance degradation, with reduced throughput and increased latency. For applications sensitive to latency or throughput, we strongly recommend evaluating WireGuard in a non-production environment first. As always, results may vary based on workload characteristics and cluster configuration.

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[WireGuard encryption](how-to-apply-wireguard)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-resource-reservations -->

# Node resource reservations in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about node resource reservations in Azure Kubernetes Service (AKS).

## Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS.

AKS reserves two types of resources, **CPU** and **memory**, on each node to maintain node performance and functionality. As a node grows larger in resources, the resource reservations also grow due to a higher need for management of user-deployed pods. Keep in mind that you can't change resource reservations on a node.

### CPU reservations

Reserved CPU is dependent on node type and cluster configuration, which might result in less allocatable CPU due to running extra features. The following table shows CPU reservations in millicores:

| CPU cores on host | 1 core | 2 cores | 4 cores | 8 cores | 16 cores | 32 cores | 64 cores |
|---|---|---|---|---|---|---|---|
| Kube-reserved CPU (millicores) | 60 | 100 | 140 | 180 | 260 | 420 | 740 |

### Memory reservations

In AKS, reserved memory consists of the sum of two values:

**AKS 1.29 and later**

has the`kubelet`

daemon*memory.available < 100 Mi*eviction rule by default. This rule ensures that a node has at least 100 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and frees up memory on the host machine.**A rate of memory reservations**set according to the lesser value of:*20 MB * Max Pods supported on the Node + 50 MB*or*25% of the total system memory resources*.**Examples**:- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves
*20 MB * 30 Max Pods + 50 MB = 650 MB*for kube-reserved.`Allocatable space = 8 GB - 0.65 GB (kube-reserved) - 0.1 GB (eviction threshold) = 7.25 GB or 90.625% allocatable.`

- If the VM provides 4 GB of memory and the node supports up to 70 pods, AKS reserves
*25% * 4 GB = 1000 MB*for kube-reserved, as this is less than*20 MB * 70 Max Pods + 50 MB = 1450 MB*.

For more information, see

[Configure maximum pods per node in an AKS cluster](concepts-network-ip-address-planning#maximum-pods-per-node).- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves

**AKS versions prior to 1.29**

has the`kubelet`

daemon*memory.available < 750 Mi*eviction rule by default. This rule ensures that a node has at least 750 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and free up memory on the host machine.**A regressive rate of memory reservations**for the kubelet daemon to properly function (*kube-reserved*).- 25% of the first 4 GB of memory
- 20% of the next 4 GB of memory (up to 8 GB)
- 10% of the next 8 GB of memory (up to 16 GB)
- 6% of the next 112 GB of memory (up to 128 GB)
- 2% of any memory more than 128 GB


Note

AKS reserves an extra 2 GB for system processes in Windows nodes that isn't part of the calculated memory.

Memory and CPU allocation rules are designed to:

- Keep agent nodes healthy, including some hosting system pods critical to cluster health.
- Cause the node to report less allocatable memory and CPU than it would report if it weren't part of a Kubernetes cluster.

For example, if a node offers 7 GB, it reports 34% of memory not allocatable including the 750 Mi hard eviction threshold.

`0.75 + (0.25*4) + (0.20*3) = 0.75 GB + 1 GB + 0.6 GB = 2.35 GB / 7 GB = 33.57% reserved`


In addition to reservations for Kubernetes itself, the underlying node OS also reserves an amount of CPU and memory resources to maintain OS functions.

For associated best practices, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-diagnostics -->

# Azure Kubernetes Service Diagnose and Solve Problems overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Troubleshooting Azure Kubernetes Service (AKS) cluster issues plays an important role in maintaining your cluster, especially if your cluster is running mission-critical workloads. AKS Diagnose and Solve Problems is an intelligent, self-diagnostic experience that:

- Helps you identify and resolve problems in your cluster.
- Requires no extra configuration or billing cost.

## Open AKS Diagnose and Solve Problems

You can access AKS Diagnose and Solve Problems using the following steps:

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.From the service menu, select

**Diagnose and solve problems**.Select a troubleshooting category tile that best describes the issue of your cluster by referring the keywords in each tile description on the homepage or typing a keyword that best describes your issue in the search bar.


## View a diagnostic report

After selecting a category, you can view various diagnostic reports that provide detailed information about the issue. The *Overview* option from the navigation menu runs all the diagnostics in that particular category and displays any issues that are found with the cluster. Select **View details** under each tile to view a detailed description of the issue, including:

- An issue summary
- Error details
- Recommended actions
- Links to helpful docs
- Related-metrics
- Logging data

### Example scenario: Diagnose connectivity issues

I observed that my application is getting disconnected or experiencing intermittent connection issues. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Connectivity Issues** tile to investigate the potential causes.

I received a diagnostic alert indicating that the disconnection might be related to my *Cluster DNS*. To gather more information, I select **View details**.

Based on the diagnostic result, it appears that the issue might be related to known DNS issues or the VNet configuration. I can use the documentation links provided to address the issue and resolve the problem.

If the recommended documentation based on the diagnostic results doesn't resolve the issue, I can return to the previous step in Diagnostics and refer to additional documentation.

## Use AKS Diagnose and Solve Problems for best practices

Deploying applications on AKS requires adherence to best practices to guarantee optimal performance, availability, and security. The AKS Diagnose and Solve Problems **Best Practices** tile provides an array of best practices that can assist in managing various aspects, such as VM resource provisioning, cluster upgrades, scaling operations, subnet configuration, and other essential aspects of a cluster's configuration.

Leveraging the AKS Diagnose and Solve Problems can be vital in ensuring that your cluster adheres to best practices and that any potential issues are identified and resolved in a timely and effective manner. By incorporating AKS Diagnose and Solve Problems into your operational practices, you can be confident in the reliability and security of your application in production.

### Example scenario: View best practices

I'm curious about the best practices I can follow to prevent potential problems. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Best Practices** tile.

From here, I can view the best practices that are recommended for my cluster and select **View details** to see the results.

## Next steps

- Collect logs to help you further troubleshoot your cluster issues using
[AKS Periscope](https://aka.ms/aksperiscope). - Read the
[triage practices section](/en-us/azure/architecture/operator-guides/aks/aks-triage-practices)of the AKS day-2 operations guide. - Post your questions or feedback at
[UserVoice](https://feedback.azure.com/d365community/forum/aabe212a-f724-ec11-b6e6-000d3a4f0da0). Make sure to add "[Diag]" in the title.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-action -->

# Build, test, and deploy containers to Azure Kubernetes Service (AKS) using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[GitHub Actions](https://docs.github.com/en/actions) gives you the flexibility to build an automated software development lifecycle workflow. You can use multiple Kubernetes actions to deploy to containers from Azure Container Registry (ACR) to Azure Kubernetes Service (AKS) with GitHub Actions.

## Prerequisites

- An Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - A GitHub account. If you don't have one,
[sign up for free](https://github.com/join).- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
[Use GitHub Actions to connect to Azure](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux).

- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
- An existing AKS cluster with an attached ACR. If you don't have one, see
[Authenticate with ACR from AKS](cluster-container-registry-integration).

## GitHub Actions for AKS

With GiHub Actions, you can automate your software development workflows from within GitHub. For more information, see [GitHub Actions for Azure](/en-us/azure/developer/github/github-actions).

The following table lists the available actions for AKS:

| Name | Description | More details |
|---|---|---|
`azure/aks-set-context` |
Set the target AKS cluster context for other actions to use or run any kubectl commands. |
|

`azure/k8s-set-context`

[azure/k8s-set-context](https://github.com/Azure/k8s-set-context)`azure/k8s-bake`

[azure/k8s-bake](https://github.com/Azure/k8s-bake)`azure/k8s-create-secret`

[azure/k8s-create-secret](https://github.com/Azure/k8s-create-secret)`azure/k8s-deploy`

[azure/k8s-deploy](https://github.com/Azure/k8s-deploy)`azure/k8s-lint`

[azure/k8s-lint](https://github.com/Azure/k8s-lint)`azure/setup-helm`

[azure/setup-helm](https://github.com/Azure/setup-helm)`azure/setup-kubectl`

[azure/setup-kubectl](https://github.com/Azure/setup-kubectl)`azure/k8s-artifact-substitute`

[azure/k8s-artifact-substitute](https://github.com/Azure/k8s-artifact-substitute)`azure/aks-create-action`

[azure/aks-create-action](https://github.com/Azure/aks-create-action)`azure/aks-github-runner`

[azure/aks-github-runner](https://github.com/Azure/aks-github-runner)`azure/acr-build`

[azure/acr-build](https://github.com/Azure/acr-build)## Use GitHub Actions with AKS

As an example, you can use GitHub Actions to deploy an application to your AKS cluster every time a change is pushed to your GitHub repository. This example uses the [Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis) application.

Note

This example uses a service principal for authentication with your ACR and AKS cluster. Alternatively, you can configure Open ID Connect (OIDC) and update the `azure/login`

action to use OIDC. For more information, see [Set up Azure Login with OpenID Connect authentication](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux#use-the-azure-login-action-with-openid-connect).

### Fork and update the repository

Navigate to the

[Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis)repository and select**Fork**.Update the

`azure-vote-all-in-one-redis.yaml`

to use your ACR for the`azure-vote-front`

image. Replace`<registryName>`

with the name of your registry.`... containers: - name: azure-vote-front image: <registryName>.azurecr.io/azuredocs/azure-vote-front:v1 ...`

Commit the updated

`azure-vote-all-in-one-redis.yaml`

to your repository.

### Create secrets

Create a service principal to access your resource group with the

`Contributor`

role using thecommand. Replace`az ad sp create-for-rbac`

`<SUBSCRIPTION_ID>`

with the subscription ID of your Azure account and`<RESOURCE_GROUP>`

with the name of the resource group containing your ACR.`az ad sp create-for-rbac \ --name "ghActionAzureVote" \ --scope /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP> \ --role Contributor \ --json-auth`

Your output should look similar to the following example output:

`{ "clientId": <clientId>, "clientSecret": <clientSecret>, "subscriptionId": <subscriptionId>, "tenantId": <tenantId>, ... }`

Navigate to your GitHub repository settings and select

**Security**>**Secrets and variables**>**Actions**.For each secret, select

**New Repository Secret**and enter the name and value of the secret.Secret name Secret value AZURE_CREDENTIALS The entire JSON output from the `az ad sp create-for-rbac`

command.service_principal The value of `<clientId>`

.service_principal_password The value of `<clientSecret>`

.subscription The value of `<subscriptionId>`

.tenant The value of `<tenantId>`

.registry The name of your registry. repository azuredocs resource_group The name of your resource group. cluster_name The name of your cluster.

For more information about creating secrets, see [Encrypted Secrets](https://docs.github.com/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

### Create actions file

In your repository, create a

`.github/workflows/main.yml`

and paste in the following contents:`name: build_deploy_aks on: push: paths: - "azure-vote/**" jobs: build: runs-on: ubuntu-latest steps: - name: Checkout source code uses: actions/checkout@v3 - name: ACR build id: build-push-acr uses: azure/acr-build@v1 with: service_principal: ${{ secrets.service_principal }} service_principal_password: ${{ secrets.service_principal_password }} tenant: ${{ secrets.tenant }} registry: ${{ secrets.registry }} repository: ${{ secrets.repository }} image: azure-vote-front folder: azure-vote branch: master tag: ${{ github.sha }} - name: Azure login id: login uses: azure/login@v1.4.3 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Set AKS context id: set-context uses: azure/aks-set-context@v3 with: resource-group: '${{ secrets.resource_group }}' cluster-name: '${{ secrets.cluster_name }}' - name: Setup kubectl id: install-kubectl uses: azure/setup-kubectl@v3 - name: Deploy to AKS id: deploy-aks uses: Azure/k8s-deploy@v4 with: namespace: 'default' manifests: | azure-vote-all-in-one-redis.yaml images: '${{ secrets.registry }}.azurecr.io/${{ secrets.repository }}/azure-vote-front:${{ github.sha }}' pull-images: false`

The

`on`

section contains the event that triggers the action. In the example file, the action triggers when a change is pushed to the`azure-vote`

directory.The

`steps`

section contains each distinct action:*Checkout source code*uses the[GitHub Actions Checkout Action](https://github.com/actions/checkout)to clone the repository.*ACR build*uses the[Azure Container Registry Build Action](https://github.com/Azure/acr-build)to build the image and upload it to your registry.*Azure login*uses the[Azure Login Action](https://github.com/Azure/login)to sign in to your Azure account.*Set AKS context*uses the[Azure AKS Set Context Action](https://github.com/Azure/aks-set-context)to set the context for your AKS cluster.*Setup kubectl*uses the[Azure AKS Setup Kubectl Action](https://github.com/Azure/setup-kubectl)to install kubectl on your runner.*Deploy to AKS*uses the[Azure Kubernetes Deploy Action](https://github.com/Azure/k8s-deploy)to deploy the application to your Kubernetes cluster.

Commit the

`.github/workflows/main.yml`

file to your repository.To confirm the action is working, update the

`azure-vote/azure-vote/config_file.cfg`

with the following contents:`# UI Configurations TITLE = 'Azure Voting App' VOTE1VALUE = 'Fish' VOTE2VALUE = 'Dogs' SHOWHOST = 'false'`

Commit the updated

`azure-vote/azure-vote/config_file.cfg`

to your repository.In your repository, select

**Actions**and confirm a workflow is running. Then, confirm the workflow has a green checkmark and the updated application is deployed to your cluster.

## Next steps

Review the following starter workflows for AKS. For more information, see [Using starter workflows](https://docs.github.com/actions/using-workflows/using-starter-workflows#using-starter-workflows).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-vs-code -->

# Use the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) extension for Visual Studio Code allows you to easily view and manage your AKS clusters from your development environment.

## Features

The Azure Kubernetes Service (AKS) extension for Visual Studio Code provides a rich set of features to help you manage your AKS clusters, including:

**Merge into Kubeconfig**: Merge your AKS cluster into your`kubeconfig`

file to manage your cluster from the command line.**Save Kubeconfig**: Save your AKS cluster configuration to a file.**AKS Diagnostics**: View diagnostics information based on your cluster's backend telemetry for identity, security, networking, node health, and create, upgrade, delete, and scale issues.**AKS Periscope**: Extract detailed diagnostic information and export it to an Azure storage account for further analysis.**Install Azure Service Operator (ASO)**: Deploy the latest version of ASO and provision Azure resources within Kubernetes.**Start or stop a cluster**: Start or stop your AKS cluster to save costs when you're not using it.

For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Installation

- Open Visual Studio Code.
- In the
**Extensions**view, search for**Azure Kubernetes Service**. - Select the
**Azure Kubernetes Service**extension and then select**Install**.

For more information, see [Install the AKS extension for Visual Studio Code](https://code.visualstudio.com/docs/azure/aksextensions#_install-the-azure-kubernetes-services-extension).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations with AKS](integrations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/troubleshooting -->

# Azure Kubernetes Service (AKS) troubleshooting documentation

Welcome to Azure Kubernetes Service troubleshooting. These articles explain how to determine, diagnose, and fix issues that you might encounter when you use Azure Kubernetes Service (AKS). In the navigation pane on the left, browse through the article list or use the search box to find issues and solutions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks -->

# Azure Kubernetes Service (AKS)

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.

This browser is no longer supported.

Upgrade to Microsoft Edge to take advantage of the latest features, security updates, and technical support.

AKS allows you to quickly deploy a production ready Kubernetes cluster in Azure. Learn how to use AKS with these quickstarts, tutorials, and samples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-latency -->

# Latency comparison across versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This document elaborates on the [data plane latency performance](istio-scale#data-plane-performance) across Istio add-on versions and Kubernetes version. The results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency difference. The comparison measures the difference between traffic routed through the sidecar and traffic sent directly to the pod.

- Traffic going through the sidecar: client --> client-sidecar --> server-sidecar --> server
- Traffic directly going to the pod: client --> server

## Test specifications

- Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled

| P99 Latency Difference | P90 Latency Difference |
|---|---|
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/troubleshoot-source-network-address-translation -->

# Troubleshoot SNAT port exhaustion for a Standard Load Balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you know that you're starting many outbound TCP or UDP connections to the same destination IP address and port, and you observe failing outbound connections or support notifies you that you're exhausting SNAT ports, you have several general mitigation options. Review these options and decide what's best for your scenario. It's possible that one or more can help manage your scenario. For detailed information, review the [outbound connections troubleshooting guide](/en-us/azure/load-balancer/troubleshoot-outbound-connection).

The root cause of SNAT exhaustion is frequently an anti-pattern for how outbound connectivity is established, managed, or configurable timers changed from their default values.

This article helps you troubleshoot SNAT port exhaustion issues when using a Standard Load Balancer in Azure Kubernetes Service (AKS).

## Steps to troubleshoot SNAT port exhaustion

Use the following steps to troubleshoot SNAT port exhaustion:

- Check if your connections remain idle for a long time and rely on the default idle timeout for releasing that port. If so, the default timeout of 30 minutes might need to be reduced for your scenario.
- Investigate how your application creates outbound connectivity (for example: code review or packet capture).
- Determine if this activity is expected behavior or whether the application is misbehaving. Use
[metrics](/en-us/azure/load-balancer/load-balancer-standard-diagnostics)and[logs](/en-us/azure/load-balancer/monitor-load-balancer)in Azure Monitor to substantiate your findings. For example, use the "Failed" category for SNAT connections metric. - Evaluate if appropriate
[design patterns](#snat-port-exhaustion-design-patterns)are followed. - Evaluate if SNAT port exhaustion should be mitigated with
[more outbound IP addresses and allocated outbound ports](configure-load-balancer-standard#configure-the-allocated-outbound-ports).

## SNAT port exhaustion design patterns

Take advantage of connection reuse and connection pooling whenever possible. These patterns help you avoid resource exhaustion problems and result in predictable behavior.

- Atomic requests (one request per connection) generally aren't a good design choice. Such anti-patterns limit scale, reduce performance, and decrease reliability. Instead, reuse HTTP/S connections to reduce the numbers of connections and associated SNAT ports. The application scale increases and performance improves because of reduced handshakes, overhead, and cryptographic operation cost when using TLS.
- If you're using out of cluster/custom DNS, or custom upstream servers on coreDNS, keep in mind that DNS can introduce many individual flows at volume when the client isn't caching the DNS resolvers result. Make sure to customize coreDNS first instead of using custom DNS servers and to define a good caching value.
- UDP flows (for example, DNS lookups) allocate SNAT ports during the idle timeout. The longer the idle timeout, the higher the pressure on SNAT ports. Use short idle timeout (for example, 4 minutes).
- Use connection pools to shape your connection volume.
- Never silently abandon a TCP flow and rely on TCP timers to clean up flow. If you don't let TCP explicitly close the connection, state remains allocated at intermediate systems and endpoints, and it makes SNAT ports unavailable for other connections. This pattern can trigger application failures and SNAT exhaustion.
- Don't change OS-level TCP close related timer values without expert knowledge of impact. While the TCP stack recovers, your application performance can be negatively affected when the endpoints of a connection have mismatched expectations. Wishing to change timers is usually a sign of an underlying design problem. Review following recommendations.

## Next steps

To learn more about AKS Standard Load Balancer configuration options, see [Configure your public standard load balancer in AKS](configure-load-balancer-standard).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-enable-ebpf-host-routing -->

# Enable eBPF Host Routing with Advanced Container Networking Services (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

eBPF Host Routing with Advanced Container Networking Services is currently in PREVIEW.

See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to enable eBPF Host Routing with Advanced Container Networking Services (ACNS) on Azure Kubernetes Service (AKS) clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).eBPF Host Routing is only supported with Azure CNI powered by Cilium. See

[Configure Azure CNI Powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium)for more information on managed Cilium clusters.Review the

[Limitations](container-network-performance-ebpf-host-routing#limitations)section for node requirements and compatibility with existing iptable rules.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingPerformancePreview`

feature flag

Register the `AdvancedNetworkingPerformancePreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services and eBPF Host Routing

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).**Container Network Performance:**Improves latency and throughput for pod network traffic. To learn more visit[Container Network Performance](advanced-container-networking-services-overview#container-network-performance)

Note

Clusters with the Cilium data plane support Container Network Performance with eBPF Host Routing starting with Kubernetes version 1.33.

Warning

The only compatible OS versions are Ubuntu 24.04 or Azure Linux 3.0.

Create an Azure resource group for the cluster using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
export LOCATION="<location>"
az group create --location $LOCATION --name <resourcegroup-name>
```


Create a new AKS cluster with eBPF Host Routing by enabling ACNS through `--enable-acns`

and setting the acceleration mode with `--acns-datapath-acceleration-mode BpfVeth`

.

```
# Set environment variables for the AKS cluster name and resource group. Make sure to replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<resourcegroup-name>"
export LOCATION="<location>"
export OS_SKU="<os-sku>" # Use AzureLinux or Ubuntu2404
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--kubernetes-version 1.33 \
--os-sku $OS_SKU \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth \
--generate-ssh-keys
```


### Enable eBPF Host Routing with Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with `--acns-datapath-acceleration-mode BpfVeth`

to enable Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability),

[Container Network Security](advanced-container-networking-services-overview#container-network-security), and

[Container Network Performance](advanced-container-networking-services-overview#container-network-performance).

Note

Enabling eBPF Host Routing on an existing cluster may disrupt existing connections.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth
```


## Disabling eBPF Host Routing on an existing cluster

eBPF Host Routing can be disabled independently without affecting other ACNS features. To disable it, set the flag `--acns-datapath-acceleration-mode=None`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode None
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-multi-instance -->

# Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain NVIDIA GPUs can be divided in up to seven independent instances. Each instance has its own Stream Multiprocessor (SM), which is responsible for executing instructions in parallel, and GPU memory. For more information on GPU partitioning, see [NVIDIA MIG](https://www.nvidia.com/en-us/technologies/multi-instance-gpu/).

This article walks you through how to create a multi-instance GPU node pool using a MIG-compatible VM size in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites and limitations

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The Kubernetes command-line client,
[kubectl](https://kubernetes.io/docs/reference/kubectl/), installed and configured. If you use Azure Cloud Shell,`kubectl`

is already installed. If you want to install it locally, you can use thecommand.`az aks install-cli`

- Helm v3 installed and configured. For more information, see
[Installing Helm](https://helm.sh/docs/intro/install/). - Multi-instance GPU is currently supported on the
`Standard_NC40ads_H100_v5`

,`Standard_ND96isr_H100_v5`

, and A100 GPU VM sizes on AKS.

## GPU instance profiles

GPU instance profiles define how GPUs are partitioned. The following table shows the available GPU instance profile for the `Standard_ND96asr_v4`

:

| Profile name | Fraction of SM | Fraction of memory | Number of instances created |
|---|---|---|---|
| MIG 1g.5gb | 1/7 | 1/8 | 7 |
| MIG 2g.10gb | 2/7 | 2/8 | 3 |
| MIG 3g.20gb | 3/7 | 4/8 | 2 |
| MIG 4g.20gb | 4/7 | 4/8 | 1 |
| MIG 7g.40gb | 7/7 | 8/8 | 1 |

As an example, the GPU instance profile of `MIG 1g.5gb`

indicates that each GPU instance has 1g SM (streaming multiprocessors) and 5gb memory. In this case, the GPU is partitioned into seven instances.

The available GPU instance profiles available for this VM size include `MIG1g`

, `MIG2g`

, `MIG3g`

, `MIG4g`

, and `MIG7g`

.

Important

You can't change the applied GPU instance profile after node pool creation.

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location southcentralus`

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --generate-ssh-keys`

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Create a multi-instance GPU node pool

You can use either the Azure CLI or an HTTP request to the ARM API to create the node pool.

Create a multi-instance GPU node pool using the

command and specify the GPU instance profile. The example below creates a node pool with the`az aks nodepool add`

`Standard_ND96asr_v4`

MIG-compatible GPU VM size.`az aks nodepool add \ --name aksMigNode \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --node-vm-size Standard_ND96asr_v4 \ --node-count 1 \ --gpu-instance-profile MIG1g`


## Determine multi-instance GPU (MIG) strategy

Before you install the NVIDIA plugins, you need to specify which multi-instance GPU (MIG) strategy to use for GPU partitioning: *Single strategy* or *Mixed strategy*. The two strategies don't affect how you execute CPU workloads, but how GPU resources are displayed.

**Single strategy**: The single strategy treats every GPU instance as a GPU. If you use this strategy, the GPU resources are displayed as`nvidia.com/gpu: 1`

.**Mixed strategy**: The mixed strategy exposes the GPU instances and the GPU instance profile. If you use this strategy, the GPU resource are displayed as`nvidia.com/mig1g.5gb: 1`

.

## Install the NVIDIA device plugin and GPU feature discovery (GFD) components

Set your MIG strategy as an environment variable. You can use either single or mixed strategy.

`# Single strategy export MIG_STRATEGY=single # Mixed strategy export MIG_STRATEGY=mixed`

Add the NVIDIA device plugin helm repository using the

`helm repo add`

and`helm repo update`

commands.`helm repo add nvdp https://nvidia.github.io/k8s-device-plugin helm repo update`

Install the NVIDIA device plugin using the

`helm install`

command.`helm install nvdp nvdp/nvidia-device-plugin \ --version=0.17.0 \ --set migStrategy=${MIG_STRATEGY} \ --set gfd.enabled=true \ --namespace nvidia-device-plugin \ --create-namespace`


Note

Helm installation of the NVIDIA device plugin consolidates the Kubernetes device plugin and GFD repositories. Separate helm installation of the GFD software component is not recommended when using AKS-managed multi-instance GPU.

## Confirm multi-instance GPU capability

Verify the

`kubectl`

connection to your cluster using the`kubectl get`

command to return a list of cluster nodes.`kubectl get nodes -o wide`

Confirm the node has multi-instance GPU capability using the

`kubectl describe node`

command. The following example command describes the node named*aksMigNode*, which uses MIG1g as the GPU instance profile.`kubectl describe node aksMigNode`

Your output should resemble the following example output:

`# Single strategy output Allocatable: nvidia.com/gpu: 56 # Mixed strategy output Allocatable: nvidia.com/mig-1g.5gb: 56`


## Schedule work

The following examples are based on CUDA base image **version 12.1.1** for Ubuntu **22.04**, tagged as `12.1.1-base-ubuntu22.04`

.

### Single strategy

Create a file named

`single-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-single spec: containers: - name: nvidia-single image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 1000"] resources: limits: "nvidia.com/gpu": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f single-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-single -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c) MIG 1g.5gb Device 1: (UUID: MIG-3d4db13e-c42d-5555-98f4-8b50389791bc) MIG 1g.5gb Device 2: (UUID: MIG-de819d17-9382-56a2-b9ca-aec36c88014f) MIG 1g.5gb Device 3: (UUID: MIG-50ab4b32-92db-5567-bf6d-fac646fe29f2) MIG 1g.5gb Device 4: (UUID: MIG-7b6b1b6e-5101-58a4-b5f5-21563789e62e) MIG 1g.5gb Device 5: (UUID: MIG-14549027-dd49-5cc0-bca4-55e67011bd85) MIG 1g.5gb Device 6: (UUID: MIG-37e055e8-8890-567f-a646-ebf9fde3ce7a)`


### Mixed strategy

Create a file named

`mixed-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-mixed spec: containers: - name: nvidia-mixed image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 100"] resources: limits: "nvidia.com/mig-1g.5gb": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mixed-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-mixed -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c)`


Important

The `latest`

tag for CUDA images has been deprecated on Docker Hub. Please refer to [NVIDIA's repository](https://hub.docker.com/r/nvidia/cuda/tags) for the latest images and corresponding tags.

## Troubleshooting

If you don't see multi-instance GPU capability after creating the node pool, confirm the API version isn't older than *2021-08-01*.

## Next steps

To learn more about GPUs on Azure Kubernetes Service, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/active-active-solution -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-problem-detector -->

# Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Node Problem Detector (NPD)](https://github.com/kubernetes/node-problem-detector) is an open source Kubernetes component that detects node-related problems and reports on them. It runs as a systemd serviced on each node in the cluster and collects various metrics and system information, such as CPU usage, disk usage, and network connectivity. When it detects a problem, it generates *events and/or node conditions*. Azure Kubernetes Service (AKS) uses NPD to monitor and manage nodes in a Kubernetes cluster running on the Azure cloud platform. The AKS Linux extension enables NPD by default.

Note

Upgrades to NPD are independent of the node image and Kubernetes version upgrade processes. If a node pool is unhealthy (that is, in a failed state), new NPD versions aren't installed.

## Node conditions

Node conditions indicate a permanent problem that makes the node unavailable. AKS uses the following node conditions from NPD to expose permanent problems on the node. NPD also emits corresponding Kubernetes events.

| Problem Daemon type | NodeCondition | Reason | Compute type |
|---|---|---|---|
| CustomPluginMonitor | FilesystemCorruptionProblem | FilesystemCorruptionDetected | General purpose |
| CustomPluginMonitor | KubeletProblem | KubeletIsDown | General purpose |
| CustomPluginMonitor | ContainerRuntimeProblem | ContainerRuntimeIsDown | General purpose |
| CustomPluginMonitor | VMEventScheduled | VMEventScheduled | General purpose |
| CustomPluginMonitor | FrequentUnregisterNetDevice | UnregisterNetDevice | General purpose |
| CustomPluginMonitor | FrequentKubeletRestart | FrequentKubeletRestart | General purpose |
| CustomPluginMonitor | FrequentContainerdRestart | FrequentContainerdRestart | General purpose |
| CustomPluginMonitor | FrequentDockerRestart | FrequentDockerRestart | General purpose |
| CustomPluginMonitor | GPUMissing | Observed GPU count does not match expected GPU count | GPU only |
| CustomPluginMonitor | NVLinkStatusInactive | NVLinkStatusInactive | GPU only |
| CustomPluginMonitor | XIDErrors | XID errors present in kernel log | GPU only |
| CustomPluginMonitor | IBLinkFlapping | Intermittent InfiniBand device connectivity | GPU only |
| SystemLogMonitor | KernelDeadlock | DockerHung | General purpose |
| SystemLogMonitor | ReadonlyFilesystem | FilesystemIsReadOnly | General purpose |

Note

The `GPU only`

node conditions currently apply to AKS node pools with `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size, and are supported on standard GPU and [MIG-enabled GPU node pools](gpu-multi-instance).

## Events

NPD emits events with relevant information to help you diagnose underlying issues.

| Problem Daemon type | Reason | Frequency | Description | Action |
|---|---|---|---|---|
| CustomPluginMonitor | EgressBlocked | 30 min | This event checks for connectivity to external
|

[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more information[https://aka.ms/aks/scheduledevents](https://aka.ms/aks/scheduledevents)for more informationIn certain instances, AKS automatically cordons and drains the node to minimize disruption to workloads. For more information about the events and actions, see [Node autodrain](/en-us/azure/aks/node-auto-repair#node-auto-drain).

### EgressBlocked

The list of endpoints checked by the EgressBlocked are listed below

Note

The actual endpoints will depend on the type of the cluster and the location where it's hosted (Public cloud vs Airgapped clouds). Review the documentation for outbound access [here](/en-us/azure/aks/outbound-rules-control-egress). The documentation is for public clouds

| Type | Example | Note |
|---|---|---|
| MCR |
|

`https://login.microsoftonline.com`

[https://packages.aks.azure.com/acs-mirror/healthz](https://packages.aks.azure.com/acs-mirror/healthz)## Check the node conditions and events

Check the node conditions and events using the

`kubectl describe node`

command.`kubectl describe node my-aks-node`

Your output should look similar to the following example condensed output:

`... ... Conditions: Type Status LastHeartbeatTime LastTransitionTime Reason Message ---- ------ ----------------- ------------------ ------ ------- VMEventScheduled False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoVMEventScheduled VM has no scheduled event FrequentContainerdRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentContainerdRestart containerd is functioning properly FrequentDockerRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentDockerRestart docker is functioning properly FilesystemCorruptionProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 FilesystemIsOK Filesystem is healthy FrequentUnregisterNetDevice False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentUnregisterNetDevice node is functioning properly ContainerRuntimeProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:40 +0000 ContainerRuntimeIsUp container runtime service is up KernelDeadlock False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 KernelHasNoDeadlock kernel has no deadlock FrequentKubeletRestart False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 NoFrequentKubeletRestart kubelet is functioning properly KubeletProblem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 KubeletIsUp kubelet service is up ReadonlyFilesystem False Thu, 01 Jun 2023 19:14:25 +0000 Thu, 01 Jun 2023 03:57:41 +0000 FilesystemIsNotReadOnly Filesystem is not read-only NetworkUnavailable False Thu, 01 Jun 2023 03:58:39 +0000 Thu, 01 Jun 2023 03:58:39 +0000 RouteCreated RouteController created a route MemoryPressure True Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 19:16:50 +0000 KubeletHasInsufficientMemory kubelet has insufficient memory available DiskPressure False Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:22 +0000 KubeletHasNoDiskPressure kubelet has no disk pressure PIDPressure False Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:22 +0000 KubeletHasSufficientPID kubelet has sufficient PID available Ready True Thu, 01 Jun 2023 19:16:50 +0000 Thu, 01 Jun 2023 03:57:23 +0000 KubeletReady kubelet is posting ready status. AppArmor enabled ... ... ... Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal NodeHasSufficientMemory 94s (x176 over 15h) kubelet Node aks-agentpool-40622340-vmss000009 status is now: NodeHasSufficientMemory`


These events are also available in [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview) through [KubeEvents](/en-us/azure/azure-monitor/reference/tables/kubeevents).

## Metrics

NPD also exposes Prometheus metrics based on the node problems, which you can use for monitoring and alerting. These metrics are exposed on port 20257 of the Node IP and Prometheus can scrape them.

The following example YAML shows a scrape config you can use with the [Azure Managed Prometheus add on as a DaemonSet](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-configuration#advanced-setup-configure-custom-prometheus-scrape-jobs-for-the-daemonset):

```
kind: ConfigMap
apiVersion: v1
metadata:
name: ama-metrics-prometheus-config-node
namespace: kube-system
data:
prometheus-config: |-
global:
scrape_interval: 1m
scrape_configs:
- job_name: node-problem-detector
scrape_interval: 1m
scheme: http
metrics_path: /metrics
relabel_configs:
- source_labels: [__metrics_path__]
regex: (.*)
target_label: metrics_path
- source_labels: [__address__]
replacement: '$NODE_NAME'
target_label: instance
static_configs:
- targets: ['$NODE_IP:20257']
```


The following example shows the scraped metrics:

```
problem_gauge{reason="UnregisterNetDevice",type="FrequentUnregisterNetDevice"} 0
problem_gauge{reason="VMEventScheduled",type="VMEventScheduled"} 0
```


## Next steps

For more information on NPD, see [kubernetes/node-problem-detector](https://github.com/kubernetes/node-problem-detector).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network -->

# Networking concepts for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In a container-based, microservices approach to application development, application components work together to process their tasks. Kubernetes provides various resources enabling this cooperation:

- You can connect to and expose applications internally or externally.
- You can build highly available applications by load balancing your applications.
- You can restrict the flow of network traffic into or between pods and nodes to improve security.
- You can configure Ingress traffic for SSL/TLS termination or routing of multiple components for your more complex applications.

This article introduces the core concepts that provide networking to your applications in AKS:

## Kubernetes networking basics

Kubernetes employs a virtual networking layer to manage access within and between your applications or their components:

**Kubernetes nodes and virtual network**: Kubernetes nodes are connected to a virtual network. This setup enables pods (basic units of deployment in Kubernetes) to have both inbound and outbound connectivity.**Kube-proxy component**: kube-proxy runs on each node and is responsible for providing the necessary network features.

Regarding specific Kubernetes functionalities:

**Load balancer**: You can use a load balancer to distribute network traffic evenly across various resources.**Ingress controllers**: These facilitate Layer 7 routing, which is essential for directing application traffic.**Egress traffic control**: Kubernetes allows you to manage and control outbound traffic from cluster nodes.**Network policies**: These policies enable security measures and filtering for network traffic in pods.

In the context of the Azure platform:

- Azure streamlines virtual networking for AKS (Azure Kubernetes Service) clusters.
- Creating a Kubernetes load balancer on Azure simultaneously sets up the corresponding Azure load balancer resource.
- As you open network ports to pods, Azure automatically configures the necessary network security group rules.
- Azure can also manage external DNS configurations for HTTP application routing as new Ingress routes are established.

## Azure virtual networks

In AKS, you can deploy a cluster that uses one of the following network models:

**Overlay network model**: Overlay networking is the most common networking model used in Kubernetes. Pods are given an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This model enables simpler, improved scalability when compared to the flat network model.**Flat network model**: A flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Any traffic leaving your clusters isn't SNAT'd, and the pod IP address is directly exposed to the destination. This model can be useful for scenarios like exposing pod IP addresses to external services.

For more information on networking models in AKS, see [CNI Networking in AKS](concepts-network-cni-overview).

## Control outbound (egress) traffic

AKS clusters are deployed on a virtual network and have outbound dependencies on services outside of that virtual network, which are almost entirely defined with fully qualified domain names (FQDNs). AKS provides several outbound configuration options which allow you to customize the way in which these external resources are accessed.

Important

Starting on **March 31, 2026**, Azure Kubernetes Service (AKS) no longer supports default outbound access for virtual machines (VMs). New AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

). This setting **doesn't impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It might affect **unsupported scenarios**, such as deploying other resources into the same subnet. Clusters using **BYO VNets are unaffected** by this change. In supported configurations, no action is required. For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

### Outbound configuration options

For more information on the supported AKS cluster outbound configuration types, see [Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)](egress-outboundtype).

By default, AKS clusters have unrestricted outbound (egress) Internet access, which allows the nodes and services you run to access external resources as needed. If desired, you can restrict outbound traffic.

For more information on how to restrict outbound traffic from your cluster see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

## Network security groups

A network security group filters traffic for VMs like the AKS nodes. As you create Services, such as a *LoadBalancer*, the Azure platform automatically configures any necessary network security group rules.

You don't need to manually configure network security group rules to filter traffic for pods in an AKS cluster. You can define any required ports and forwarding as part of your Kubernetes Service manifests and let the Azure platform create or update the appropriate rules.

You can also use network policies to automatically apply traffic filter rules to pods.

For more information, see [How network security groups filter network traffic](/en-us/azure/virtual-network/network-security-group-how-it-works).

### Custom virtual network requirements

When using a custom virtual network with AKS clusters, if you have added Network Security Group (NSG) rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communication between the Azure Load Balancer and the API Server Subnet CIDR. |
| Node CIDR | Node CIDR | All Protocols | All Ports | Required to enable communication between Nodes. |
| Node CIDR | Pod CIDR | All Protocols | All Ports | Required for Service traffic routing. |
| Pod CIDR | Pod CIDR | All Protocols | All Ports | Required for Pod to Pod and Pod to Service traffic, including DNS. |

These requirements apply to both AKS Standard and AKS Automatic clusters when using custom virtual networks.

## Network policies

By default, all pods in an AKS cluster can send and receive traffic without limitations. For improved security, define rules that control the flow of traffic, like:

- Back-end applications are only exposed to required frontend services.
- Database components are only accessible to the application tiers that connect to them.

Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You can allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. While network security groups are better for AKS nodes, network policies are a more suited, cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

For more information, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Next steps

To get started with AKS networking, create and configure an AKS cluster with your own IP address ranges using [Azure CNI Overlay](azure-cni-overlay) or [Azure CNI](configure-azure-cni).

For associated best practices, see [Best practices for network connectivity and security in AKS](operator-best-practices-network).

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/access-private-cluster -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/intro-aks-automatic -->

# What is Azure Kubernetes Service (AKS) Automatic?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

Azure Kubernetes Service (AKS) Automatic offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of your cluster setup, including node management, scaling, security, and preconfigured settings that follow AKS well-architected recommendations. Automatic clusters dynamically allocate compute resources based on your specific workload requirements and are tuned for running production applications.

**Production ready by default**: Clusters are preconfigured for optimal production use, suitable for most applications. They offer fully managed node pools that automatically allocate and scale resources based on your workload needs. Pods are bin packed efficiently, to maximize resource utilization.**Built-in best practices and safeguards**: AKS Automatic clusters have a hardened default configuration, with many cluster, application, and networking security settings enabled by default. AKS automatically patches your nodes and cluster components while adhering to any planned maintenance schedules.**Code to Kubernetes in minutes**: Go from a container image to a deployed application that adheres to best practices patterns within minutes, with access to the comprehensive capabilities of the Kubernetes API and its rich ecosystem.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## AKS Automatic and Standard feature comparison

The following table provides a comparison of options that are available, preconfigured, and default in both AKS Automatic and AKS Standard. For more information on whether specific features are available in Automatic, you can check the documentation for that feature.

**Preconfigured** features are always enabled and you can't disable or change their settings. **Default** features are configured for you but can be changed. **Optional** features are available for you to configure and aren't enabled by default.

When enabling optional features, you can follow the linked feature documentation. When you reach a step for cluster creation, follow steps to create an [AKS Automatic cluster](learn/quick-kubernetes-automatic-deploy) instead of creating an AKS Standard cluster.

### Application deployment, monitoring, and observability

Application deployment can be streamlined using [automated deployments](automated-deployments) from source control, which creates Kubernetes manifest and generates CI/CD workflows. Additionally, the cluster is configured with monitoring tools such as Managed Prometheus for metrics, Managed Grafana for visualization, and Container Insights for log collection.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Application deployment | Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
| Monitoring, logging, and visualization | Default: *
*
*
*
Optional: *
|
Default:
Optional: *
*
*
*
|

### Node management, scaling, and cluster operations

Node management is automatically handled without the need for manual node pool creation. Scaling is seamless, with nodes created based on workload requests. Additionally, features for workload scaling like Horizontal Pod Autoscaler (HPA), [Kubernetes Event Driven Autoscaling (KEDA)](keda-about), and [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) are enabled. Clusters are configured for automatic node repair, automatic cluster upgrades, and detection of deprecated Kubernetes standard API usage. You can also set a planned maintenance schedule for upgrades if needed.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Node management | Preconfigured: AKS Automatic manages the node pools using
|
Default: You create and manage system and user node pools Optional: AKS Standard manages user node pools using
|
| Scaling | Preconfigured: AKS Automatic creates nodes based on workload requests using
|
Default: Manual scaling of node pools. Optional: *
*
*
*
|
| Cluster tier and Service Level Agreement (SLA) | Preconfigured: Standard tier cluster with up to 5,000 nodes, a
|
Default: Free tier cluster with 10 nodes but can support up to 1,000 nodes. Optional: * Standard tier cluster with up to 5,000 nodes and a
* Premium tier cluster with up to 5,000 nodes,
|
| Node operating system | Preconfigured:
|
Default: Ubuntu Optional: *
*
|
| Node resource group | Preconfigured: Fully managed node resource group to prevent accidental or intentional changes to cluster resources. |
Default: Unrestricted Optional:
|
| Node auto-repair | Preconfigured: Continuously monitors the health state of worker nodes and performs
|
Preconfigured: Continuously monitors the health state of worker nodes and performs
|
| Cluster upgrades | Preconfigured: Clusters are
|
Default: Manual upgrade. Optional: Automatic upgrade using a selectable
|
| Kubernetes API breaking change detection | Preconfigured: Cluster upgrades are stopped on detection of
|
Preconfigured: Cluster upgrades are stopped on detection of
|
| Planned maintenance windows | Default: Set
|
Optional: Set
|

### Security and policies

Cluster authentication and authorization use [Azure Role-based Access Control (RBAC) for Kubernetes authorization](manage-azure-rbac) and applications can use features like [workload identity with Microsoft Entra Workload ID](workload-identity-overview) and [OpenID Connect (OIDC) cluster issuer](use-oidc-issuer) to have secure communication with Azure services. [Deployment safeguards](deployment-safeguards) enforce Kubernetes best practices through Azure Policy controls and the built-in [image cleaner](image-cleaner) removes unused images with vulnerabilities, enhancing image security.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Cluster authentication and authorization | Preconfigured:
|
Default: Local accounts. Optional: *
*
|
| Cluster security | Preconfigured:
|
Optional:
|
| Application security | Preconfigured: *
*
Optional:*
|
Optional: *
*
Optional:*
|
| Image security | Preconfigured:
|
Optional:
|
| Policy enforcement | Preconfigured:
Optional:*
|
Optional:
Optional:*
|
| Managed namespaces | Optional: Use
|
Optional: Use
|

### Networking

AKS Automatic clusters use [managed Virtual Network powered by Azure CNI Overlay with Cilium](azure-cni-powered-by-cilium) for high-performance networking and robust security. Ingress is handled by [managed NGINX using the application routing add-on](app-routing), integrating seamlessly with Azure DNS and Azure Key Vault. Egress uses a [managed NAT gateway](nat-gateway#create-an-aks-cluster-with-a-managed-nat-gateway) for scalable outbound connections. Additionally, you have the flexibility to enable [Istio-based service mesh add-on for AKS](istio-about) or bring your own service mesh.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Virtual network | Default:
Optional: *
*
|
Default:
Optional: *
*
*
*
|
| Ingress | Preconfigured:
Optional: *
* Bring your own ingress or gateway. |
Optional: *
*
* Bring your own ingress or gateway. |
| Egress | Preconfigured:
Optional (with custom virtual network): *
*
*
|
Default:
Optional: *
*
*
|
| Service mesh | Optional: *
* Bring your own service mesh. |
Optional: *
* Bring your own service mesh. |

## Next steps

To learn more about AKS Automatic, follow the quickstart to create a cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-scale -->

# Istio service mesh add-on performance and scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Istio-based service mesh add-on is logically split into a control plane (`istiod`

) and a data plane. The data plane is composed of Envoy sidecar proxies inside workload pods. Istiod manages and configures these Envoy proxies. This article presents the performance of both the control and data plane for revision asm-1-19, including resource consumption, sidecar capacity, and latency overhead. Additionally, it provides suggestions for addressing potential strain on resources during periods of heavy load. This article also covers how to customize scaling for the control plane and gateways.

## Control plane performance

[Istiod’s CPU and memory requirements](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#control-plane-performance) correlate with the rate of deployment and configuration changes and the number of proxies connected. The scenarios tested were:

- Pod churn: examines the impact of pod churning on
`istiod`

. To reduce variables, only one service is used for all sidecars. - Multiple services: examines the impact of multiple services on the maximum sidecars Istiod can manage (sidecar capacity), where each service has
`N`

sidecars, totaling the overall maximum.

#### Test specifications

- One
`istiod`

instance with default settings - Horizontal pod autoscaling disabled
- Tested with two network plugins: Azure Container Networking Interface (CNI) Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v3 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Istio revision: asm-1-19

### Pod churn

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars Istiod can manage when there's sidecar churning. The churn percent is defined as the percent of sidecars churned down/up during the test. For example, 50% churn for 10,000 sidecars would mean that 5,000 sidecars were churned down, then 5,000 sidecars were churned up. The churn percents tested were determined from the typical churn percentage during deployment rollouts (`maxUnavailable`

). The churn rate was calculated by determining the total number of sidecars churned (up and down) over the actual time taken to complete the churning process.

#### Sidecar capacity and Istiod CPU and memory

**Azure CNI overlay**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 25000 | 32.1 | 15 |
| 25 | 31.2 | 15000 | 22.2 | 15 |
| 50 | 31.2 | 15000 | 25.4 | 15 |

**Azure CNI overlay with Cilium**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 30000 | 41.2 | 15 |
| 25 | 41.7 | 25000 | 36.1 | 16 |
| 50 | 37.9 | 25000 | 42.7 | 16 |

### Multiple services

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars `istiod`

can manage with 1,000 services. The results can be compared to the 0% churn test (one service) in the pod churn scenario. Each service had `N`

sidecars contributing to the overall maximum sidecar count. The API Server resource usage was observed to determine if there was any significant stress from the add-on.

**Sidecar capacity**

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
| 20000 | 20000 |

**CPU and memory**

| Resource | Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|---|
| API Server Memory (GB) | 38.9 | 9.7 |
| API Server CPU | 6.1 | 4.7 |
| Istiod Memory (GB) | 40.4 | 42.6 |
| Istiod CPU | 15 | 16 |

## Data plane performance

Various factors impact [sidecar performance](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#data-plane-performance) such as request size, number of proxy worker threads, and number of client connections. Additionally, any request flowing through the mesh traverses the client-side proxy and then the server-side proxy. Therefore, latency and resource consumption are measured to determine the data plane performance.

[ Fortio](https://fortio.org/) was used to create the load. The test was conducted with the

[Istio benchmark repository](https://github.com/istio/tools/tree/master/perf/benchmark#istio-performance-benchmarking)that was modified for use with the add-on.

#### Test specifications

- Tested with two network plugins: Azure CNI Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled- 26 data points collected

#### CPU and memory

The memory and CPU usage for both the client and server proxy for 16 client connections and 1,000 QPS across all network plugin scenarios is roughly 0.4 vCPU and 72 MB.

#### Latency

The sidecar Envoy proxy collects raw telemetry data after responding to a client, which doesn't directly affect the request's total processing time. However, this process delays the start of handling the next request, contributing to queue wait times and influencing average and tail latencies. Depending on the traffic pattern, the actual tail latency varies.

The following results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency.

- Sidecar traffic path: client --> client-sidecar --> server-sidecar --> server
- Baseline traffic path: client --> server

A comparison of data plane latency performance across Istio add-on and AKS versions can be found [here](istio-latency).

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
|

## Scaling

### Horizontal pod autoscaling customization

[Horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) is enabled for the `istiod`

and ingress/egress gateway deployments. The default configurations for `istiod`

and the gateways are:

- Min Replicas: 2
- Max Replicas: 5
- CPU Utilization: 80%

Note

To prevent conflicts with the `PodDisruptionBudget`

, the add-on does not allow setting the `minReplicas`

below the initial default of `2`

.

The following are the `istiod`

and ingress gateway HPA resources:

```
NAMESPACE NAME REFERENCE
aks-istio-ingress aks-istio-ingressgateway-external-asm-1-19 Deployment/aks-istio-ingressgateway-external-asm-1-19
aks-istio-ingress aks-istio-ingressgateway-internal-asm-1-19 Deployment/aks-istio-ingressgateway-internal-asm-1-19
aks-istio-system istiod-asm-1-19 Deployment/istiod-asm-1-19
```


The HPA configuration can be modified through patches and direct edits. Example:

```
kubectl patch hpa aks-istio-ingressgateway-external-asm-1-19 -n aks-istio-ingress --type merge --patch '{"spec": {"minReplicas": 3, "maxReplicas": 6}}'
```


Note

See the [Istio add-on upgrade documentation](istio-upgrade#minor-revision-upgrades-with-horizontal-pod-autoscaling-customizations) for details on how HPA settings are applied across both revisions during a canary upgrade.

## Service entry

Istio's ServiceEntry custom resource definition enables adding other services into the Istio’s internal service registry. A [ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/) allows services already in the mesh to route or access the services specified. However, the configuration of multiple ServiceEntries with the `resolution`

field set to DNS can cause a [heavy load on Domain Name System (DNS) servers](https://preliminary.istio.io/latest/docs/ops/configuration/traffic-management/dns/#proxy-dns-resolution). The following suggestions can help reduce the load:

- Switch to
`resolution: NONE`

to avoid proxy DNS lookups entirely. Suitable for most use cases. However, when using an[Istio add-on egress gateway](istio-deploy-egress), the ServiceEntry resolution must be set to`DNS`

. - Increase TTL (Time To Live) if you control the domains being resolved.
- Limit the ServiceEntry scope with
`exportTo`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-cluster -->

# Upgrade options and recommendations for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article gives you a technical foundation for Azure Kubernetes Service (AKS) cluster upgrades by covering upgrade options and common scenarios. For in-depth guidance tailored to your needs, use the scenario-based navigation paths at the end of this article.

## What this article covers

This technical reference provides comprehensive AKS upgrade fundamentals on:

- Manual versus automated upgrade options and when to use each.
- Common upgrade scenarios with specific recommendations.
- Optimization techniques for performance and minimal disruption.
- Troubleshooting guidance for capacity, drain failures, and timing issues.
- Validation processes and pre-upgrade checks.

This hub is best for helping you to understand upgrade mechanics, troubleshoot issues, optimize upgrade settings, and learn about technical implementation.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

If you're new to AKS upgrades, start with the [upgrade scenarios hub](upgrade-scenarios-hub) for guided, scenario-based assistance.

## Quick navigation

| Your situation | Recommended path |
|---|---|
| Production cluster needs an upgrade |
|

[Stateful workload patterns](stateful-workload-upgrades)[Basic AKS cluster upgrade](upgrade-aks-cluster)[Upgrade scenarios hub](upgrade-scenarios-hub)[Node pool upgrades](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools)[Single node pool upgrade](node-image-upgrade#upgrade-a-specific-node-pool)## Upgrade options

### Perform manual upgrades

Manual upgrades let you control when your cluster upgrades to a new Kubernetes version. These upgrades are useful for testing or targeting a specific version:

[Upgrade an AKS cluster](upgrade-aks-cluster)[Upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-orchestration)[Upgrade the node image](node-image-upgrade)[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade)[Process node OS updates](node-updates-kured)

### Configure automatic upgrades

Automatic upgrades keep your cluster on a supported version and up to date. Use these upgrades when you want to automate your settings:

[Automatically upgrade an AKS cluster](auto-upgrade-cluster)[Automatically upgrade multiple AKS clusters via Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/update-automation)[Use planned maintenance to schedule and control upgrades](planned-maintenance)[Stop AKS cluster upgrades automatically on API breaking changes (preview)](stop-cluster-upgrade-api-breaking-changes)[Automatically upgrade AKS cluster node operating system images](auto-upgrade-node-image)[Apply security updates to AKS nodes automatically by using GitHub actions](node-upgrade-github-actions)

### Special considerations for node pools that span multiple availability zones

AKS uses best-effort zone balancing in node groups. During an upgrade surge, the zones for surge nodes in virtual machine scale sets are unknown ahead of time, which can temporarily cause an unbalanced zone configuration. AKS deletes surge nodes after the upgrade and restores the original zone balance.

To keep zones balanced, set surge to a multiple of three nodes. Persistent volume claims that use Azure locally redundant storage disks are zone bound and might cause downtime if surge nodes are in a different zone. Use a [pod disruption budget (PDB)](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) to maintain high availability during drains.

### Optimize upgrades to improve performance and minimize disruptions

Combine [planned maintenance window](planned-maintenance), [max surge](upgrade-aks-cluster#customize-node-surge-upgrade), [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), [node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value), and [node soak time](upgrade-aks-cluster#set-node-soak-time-value) to increase the likelihood of successful, low-disruption upgrades:

[Planned maintenance window](planned-maintenance): Schedule auto-upgrade during low-traffic periods. We recommend at least four hours.[Max surge](upgrade-aks-node-pools-rolling#set-max-surge-value): Higher values speed upgrades but might disrupt workloads. We recommend 33% for production.[Max unavailable](upgrade-aks-node-pools-rolling#customize-unavailable-nodes): Use when capacity is limited.[Pod disruption budget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/): Set to limit pods down during upgrades. Validate for your service.[Node drain timeout](upgrade-aks-cluster#set-node-drain-timeout-value): Configure pod eviction wait duration. The default is 30 minutes.[Node soak time](upgrade-aks-cluster#set-node-soak-time-value): Stagger upgrades to minimize downtime. The default is 0 minutes.

| Upgrade settings | How extra nodes are used | Expected behavior |
|---|---|---|
`maxSurge=5` , `maxUnavailable=0` |
5 surge nodes | Five nodes are surged for upgrade. |
`maxSurge=5` , `maxUnavailable=0` |
0-4 surge nodes | Upgrade fails because of insufficient surge nodes. |
`maxSurge=0` , `maxUnavailable=5` |
N/A | Five existing nodes are drained for upgrade. |

Note

Before you upgrade, check for API breaking changes and review the [AKS release notes](https://github.com/Azure/AKS/releases) to avoid disruptions.

## Validations used in the upgrade process

AKS performs pre-upgrade validations to ensure cluster health:

**API breaking changes:**Detects deprecated APIs.**Kubernetes upgrade version:**Ensures a valid upgrade path.**PDB configuration:**Checks for misconfigured PDBs (for example,`maxUnavailable=0`

).**Quota:**Confirms enough quota for surge nodes.**Subnet:**Verifies sufficient IP addresses.**Certificates/service principals:**Detects expired credentials.

These checks help to minimize upgrade failures and provide early visibility into issues.

## Common upgrade scenarios and recommendations

### Scenario 1: Capacity constraints

If your cluster is limited by product tier or regional capacity, upgrades might fail when surge nodes can't be provisioned. This situation is common with specialized product tiers (like GPU nodes) or in regions with limited resources. Errors such as `SKUNotAvailable`

, `AllocationFailed`

, or `OverconstrainedAllocationRequest`

might occur if `maxSurge`

is set too high for available capacity.

#### Recommendations to prevent or resolve

- Use
`maxUnavailable`

to upgrade by using existing nodes instead of surging new ones. For more information, see[Customize unavailable nodes during upgrade](upgrade-aks-cluster#customize-unavailable-nodes-during-upgrade). - Lower
`maxSurge`

to reduce extra capacity needs. For more information, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade). - For security-only updates, use security patch reimages that don't require surge nodes. For more information, see
[Apply security and kernel updates to Linux nodes in Azure Kubernetes Service](node-updates-kured).

### Scenario 2: Node drain failures and PDBs

Upgrades require draining nodes (evicting pods). Drains can fail when pods are slow to terminate or strict [Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/) block pod evictions.

Example error:

```
Code: UpgradeFailed
Message: Drain node ... failed when evicting pod ... Cannot evict pod as it would violate the pod's disruption budget.
```


#### Option 1: Force upgrade (bypass PDB)

Warning

Force upgrade bypasses Pod Disruption Budget (PDB) constraints and may cause service disruption by draining all pods simultaneously. Before using this option, first try to fix PDB misconfigurations (review the PDB minAvailable/maxUnavailable settings, ensure adequate pod replicas, verify PDBs aren't blocking all evictions).

Use force upgrade only when PDBs prevent critical upgrades and cannot be resolved. This will override PDB protections and potentially cause complete service unavailability during the upgrade.

**Requirements:** Azure CLI 2.79.0+ or AKS API version 2025-09-01+

```
az aks upgrade \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--kubernetes-version $KUBERNETES_VERSION \
--enable-force-upgrade \
--upgrade-override-until 2023-10-01T13:00:00Z
```


Note

- The
`upgrade-override-until`

parameter defines when validation bypass ends (must be a future date/time) - If not specified, the window defaults to 3 days from current time
- The 'Z' indicates UTC/GMT time zone

Warning

When force upgrade is enabled, it takes precedence over all other drain configurations. The undrainable node behavior settings (Option 2) will not be applied when force upgrade is active.

#### Option 2: Handle undrainable nodes (honor PDB)

Use this conservative approach to honor PDBs while preventing upgrade failures.

**Configure undrainable node behavior:**

```
az aks nodepool update \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name> \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 30
```


**Behavior options:**

**Schedule (default):**Deletes blocked node and surges replacement**Cordon (recommended):**Cordons node and labels it as`kubernetes.azure.com/upgrade-status=Quarantined`


**Max blocked nodes (preview):**

- Specifies how many nodes that fail to drain are tolerated
- Requires
`undrainable-node-behavior`

to be set - Defaults to
`maxSurge`

value (typically 10%) if not specified

##### Prerequisites for max blocked nodes

The Azure CLI

`aks-preview`

extension version 18.0.0b9 or later is required to use the max blocked nodes feature.`# Install or update the aks-preview extension az extension add --name aks-preview az extension update --name aks-preview`


##### Example configuration with max blocked nodes

```
az aks nodepool update \
--cluster-name jizenMC1 \
--name nodepool1 \
--resource-group jizenTestMaxBlockedNodesRG \
--max-surge 1 \
--undrainable-node-behavior Cordon \
--max-blocked-nodes 2 \
--drain-timeout 5
```


#### Recommendations to prevent drain failures

- Set
`maxUnavailable`

in PDBs to allow at least one pod eviction - Increase pod replicas to meet disruption budget requirements
- Extend drain timeout if workloads need more time. (The default is
*30 minutes*.) - Test PDBs in staging, monitor upgrade events, and use blue-green deployments for critical workloads. For more information, see
[Blue-green deployment of AKS clusters](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks).

##### Verify undrainable nodes

The blocked nodes are unscheduled for pods and marked with the label

`"kubernetes.azure.com/upgrade-status: Quarantined"`

.Verify the label on any blocked nodes when there's a drain node failure on upgrade:

`kubectl get nodes --show-labels=true`


##### Resolve undrainable nodes

Remove the responsible PDB:

`kubectl delete pdb <pdb-name>`

Remove the

`kubernetes.azure.com/upgrade-status: Quarantined`

label:`kubectl label nodes <node-name> <label-name>`

Optionally, delete the blocked node:

`az aks nodepool delete-machines --cluster-name <cluster-name> --machine-names <machine-name> --name <node-pool-name> --resource-group <resource-group-name>`

After you finish this step, you can reconcile the cluster status by performing any update operation without the optional fields as outlined in

[az aks](/en-us/cli/azure/aks#az-aks-update). Alternatively, you can scale the node pool to the same number of nodes as the count of upgraded nodes. This action ensures that the node pool gets to its intended original size. AKS prioritizes the removal of the blocked nodes. This command also restores the cluster provisioning status to`Succeeded`

. In the following example,`2`

is the total number of upgraded nodes.`# Update the cluster to restore the provisioning status az aks update --resource-group <resource-group-name> --name <cluster-name> # Scale the node pool to restore the original size az aks nodepool scale --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --node-count 2`


### Scenario 3: Slow upgrades

Conservative settings or node-level issues can delay upgrades, which affects your ability to stay current with patches and improvements.

Common causes of slow upgrades include:

- Low
`maxSurge`

or`maxUnavailable`

values (limits parallelism). - High soak times (long waits between node upgrades).
- Drain failures (see
[Node drain failures](#scenario-2-node-drain-failures-and-pdbs)).

#### Recommendations to prevent or resolve

- Use
`maxSurge=33%`

,`maxUnavailable=1`

for production. - Use
`maxSurge=50%`

,`maxUnavailable=2`

for dev/test. - Use OS Security Patch for fast, targeted patching (avoids full node reimaging).
- Enable
`undrainableNodeBehavior`

to avoid upgrade blockers.

### Scenario 4: IP exhaustion

Surge nodes require more IPs. If the subnet is near capacity, node provisioning can fail (for example, `Error: SubnetIsFull`

). This scenario is common with Azure Container Networking Interface, high `maxPods`

, or large node counts.

#### Recommendations to prevent or resolve

Ensure that your subnet has enough IPs for all nodes, surge nodes, and pods. The formula is

`Total IPs = (Number of nodes + maxSurge) * (1 + maxPods)`

.Reclaim unused IPs or expand the subnet (for example, from /24 to /22).

Lower

`maxSurge`

if subnet expansion isn't possible:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --max-surge 10%`

Monitor IP usage with Azure Monitor or custom alerts.

Reduce

`maxPods`

per node, clean up orphaned load balancer IPs, and plan subnet sizing for high-scale clusters.

## Frequently asked questions

### Can I use open-source tools for validation?

Yes. Many open-source tools integrate well with AKS upgrade processes:

[kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble): Scans for deprecated APIs before upgrades.[Trivy](https://aquasecurity.github.io/trivy/): Security scanning for container images and Kubernetes configurations.[Sonobuoy](https://sonobuoy.io/): Kubernetes conformance testing and cluster validation.[kube-bench](https://github.com/aquasecurity/kube-bench): Security benchmark checks against Center for Internet Security standards.[Polaris](https://github.com/FairwindsOps/polaris): Validation of Kubernetes best practices.[kubectl-neat](https://github.com/itaysk/kubectl-neat): Clean up Kubernetes manifests for validation.

### How do I validate API compatibility before upgrading?

Run deprecation checks by using tools like kubent:

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Check for deprecated APIs in your cluster
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


### What makes AKS upgrades different from other Kubernetes platforms?

AKS provides several unique advantages:

- Native Azure integration with Azure Traffic Manager, Azure Load Balancer, and networking.
- Azure Kubernetes Fleet Manager for coordinated multicluster upgrades.
- Automatic node image patching without manual node management.
- Built-in validation for quota, networking, and credentials.
- Azure support for upgrade-related issues.

## Choose your upgrade path

This article provided you with a technical foundation. Now select your scenario-based path.

### Ready to execute?

| If you have... | Then go to... |
|---|---|
| Production environment |
|

[Stateful workload patterns](stateful-workload-upgrades): Safe upgrade patterns for data persistence[Upgrade scenarios hub](upgrade-scenarios-hub): Decision tree for complex setups[Upgrade an AKS cluster](upgrade-aks-cluster): Step-by-step cluster upgrade### Still deciding?

Use the [upgrade scenarios hub](upgrade-scenarios-hub) for a guided decision tree that considers your:

- Downtime tolerance
- Environment complexity
- Risk profile
- Timeline constraints

## Next tasks

- Review
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices)for best practices and planning tips before you start any upgrade. - Always check for
[API breaking changes](https://aka.ms/aks/breakingchanges)and validate your workload's compatibility with the target Kubernetes version. - Test upgrade settings (such as
`maxSurge`

,`maxUnavailable`

, and PDBs) in a staging environment to minimize production risk. - Monitor upgrade events and cluster health throughout the process.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-apiserver-vnet-integration-cluster -->

# Connect to an API Server VNet Integration cluster by using Azure Private Link

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

API Server VNet Integration lets you place the control‑plane IP inside your own VNet. The pattern described here extends that capability to more VNets by chaining Private Link. It's useful for hub‑and‑spoke topologies, dedicated build networks, or jump‑host VNets that must administer production clusters without opening the API server to the public internet.

This article applies **only to clusters that are created with API Server VNet Integration** and shows you how to:

- Deploy a
**private**AKS cluster with API Server VNet Integration. - Expose the API server through a
**Private Link Service (PLS)**inside the cluster virtual network. - Create a
**Private Endpoint (PE)**in a different virtual network. - Configure
**private DNS**so Kubernetes tools resolve the cluster’s private FQDN inside the remote network.

For private clusters that **do not** use API Server VNet Integration, see [Create a private AKS cluster](private-clusters).

## Region availability

API Server VNet Integration is currently available in a subset of Azure regions and is subject to regional capacity limits. Before you begin, confirm that your target region is supported. For more information, see [API Server VNet Integration](api-server-vnet-integration).

## Prerequisites

| Requirement | Minimum |
|---|---|
| Azure CLI | 2.73.0 |
| Permissions | Contributor + Network Contributor on both subscriptions |

If you use custom DNS servers, add Azure’s virtual IP **168.63.129.16** as an upstream forwarder.

## Set environment variables

Set the following environment variables for use throughout this article. Feel free to replace the placeholder values with your own.

```
LOCATION="westus3"
# Resource groups
AKS_RG="aks-demo-rg"
REMOTE_RG="client-demo-rg"
# AKS cluster
AKS_CLUSTER="aks-private"
AKS_SUBNET="aks-subnet"
# Private Link Service
PLS_NAME="apiserver-pls"
PLS_SUBNET="pls-subnet"
PLS_PREFIX="10.225.0.0/24"
# Remote VNet
REMOTE_VNET="client-vnet"
REMOTE_SUBNET="client-subnet"
REMOTE_VNET_PREFIX="192.168.0.0/16"
REMOTE_SUBNET_PREFIX="192.168.1.0/24"
PE_NAME="aks-pe"
PE_CONN_NAME="aks-pe-conn"
# DNS
DNS_ZONE="private.${LOCATION}.azmk8s.io"
DNS_LINK="dns-link"
```


## Create resource groups

```
# Create resource groups for the AKS cluster
az group create --name $AKS_RG --location $LOCATION
# Create a resource group for the remote VNet
az group create --name $REMOTE_RG --location $LOCATION
```


## Deploy a private cluster with API Server VNet Integration

Important

API Server VNet Integration requires its own subnet. If you don't supply one, AKS automatically creates it in the node resource group.

```
az aks create \
--name $AKS_CLUSTER \
--resource-group $AKS_RG \
--location $LOCATION \
--enable-private-cluster \
--enable-apiserver-vnet-integration
```


After the cluster finishes provisioning, capture the autogenerated node resource group, cluster VNet name, and private FQDN label:

```
AKS_NODE_RG=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query nodeResourceGroup -o tsv)
AKS_VNET=$(az network vnet list --resource-group $AKS_NODE_RG --query '[0].name' -o tsv)
DNS_RECORD=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query privateFqdn -o tsv | cut -d'.' -f1,2)
FRONTEND_IP_CONFIG_ID=$(az network lb show \
--name kube-apiserver \
--resource-group $AKS_NODE_RG \
--query "frontendIPConfigurations[0].id" \
-o tsv)
```


## Create a Private Link Service (PLS) in the AKS cluster VNet

Add a dedicated subnet for the PLS and disable network policies, which aren't supported on Private Link subnets.

Create the PLS and point it to the kube‑apiserver internal load balancer that AKS created for the control plane.

```
# Subnet for the PLS
az network vnet subnet create \
--name $PLS_SUBNET \
--vnet-name $AKS_VNET \
--resource-group $AKS_NODE_RG \
--address-prefixes $PLS_PREFIX \
--disable-private-link-service-network-policies
# PLS pointing to the API‑server ILB
az network private-link-service create \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--vnet-name $AKS_VNET \
--subnet $PLS_SUBNET \
--lb-frontend-ip-configs $FRONTEND_IP_CONFIG_ID \
--location $LOCATION
```


## Create a PrivateEndpoint (PE) in the remote VNet

```
# Remote VNet and subnet
az network vnet create \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--location $LOCATION \
--address-prefixes $REMOTE_VNET_PREFIX
az network vnet subnet create \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--address-prefixes $REMOTE_SUBNET_PREFIX
# Private Endpoint
PLS_ID=$(az network private-link-service show \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--query id -o tsv)
az network private-endpoint create \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--private-connection-resource-id $PLS_ID \
--connection-name $PE_CONN_NAME \
--location $LOCATION
```


When the Private Endpoint finishes provisioning, note its network interface (NIC) ID so you can retrieve the allocated private IP address.

```
PE_NIC_ID=$(az network private-endpoint show \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--query 'networkInterfaces[0].id' \
--output tsv)
# Capture the IP from the NIC
PE_IP=$(az network nic show \
--ids $PE_NIC_ID \
--query 'ipConfigurations[0].privateIPAddress' \
--output tsv)
```


## Configure private DNS

```
# Create or reuse the regional DNS zone
az network private-dns zone create \
--name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a create \
--name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a add-record \
--record-set-name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--ipv4-address $PE_IP
# Link zone to the remote VNet
REMOTE_VNET_ID=$(az network vnet show \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--query id -o tsv)
az network private-dns link vnet create \
--name $DNS_LINK \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--virtual-network $REMOTE_VNET_ID \
--registration-enabled false
```


## Test the connection

If you try to test the connection locally, you might get an error because the DNS zone isn't linked to your local network.

```
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
kubectl get nodes
```


### Deploy a test VM in the remote VNet

To confirm the Private Endpoint path, deploy a test VM in the remote VNet and use it to connect to the AKS cluster.

```
# Create Network Security Group that allows inbound SSH (TCP 22)
az network nsg create \
--name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--location $LOCATION
az network nsg rule create \
--nsg-name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--name allow-ssh \
--priority 100 \
--access Allow \
--protocol Tcp \
--direction Inbound \
--source-address-prefixes '*' \
--destination-port-ranges 22
# Associate the NSG with the remote subnet
az network vnet subnet update \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--network-security-group "${REMOTE_VNET}-nsg"
# Create a small Ubuntu VM in that subnet (with a public IP for quick SSH)
az vm create \
--resource-group $REMOTE_RG \
--name test-vm \
--image Ubuntu2204 \
--size Standard_B2s \
--admin-username azureuser \
--generate-ssh-keys \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--public-ip-sku Standard
# Capture the public IP address
VM_PUBLIC_IP=$(az vm show -d -g $REMOTE_RG -n test-vm --query publicIps -o tsv)
```


### Connect to the VM and test the connection

```
ssh -i ~/.ssh/id_rsa azureuser@$VM_PUBLIC_IP
# Inside the VM
# Install Azure CLI
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
# Install kubectl
sudo az aks install-cli
# re-export the aks variables
export AKS_RG="aks-demo-rg"
export AKS_CLUSTER="aks-private"
# login to Azure. Follow the instructions to authenticate
az login
# Get the AKS credentials
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
# Test the connection
kubectl get nodes
# You should see the AKS nodes
# Exit the VM
exit
```


## Clean up resources

To avoid ongoing Azure charges, delete the resource groups using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $AKS_RG --yes --no-wait
az group delete --name $REMOTE_RG --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver -->

# Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store CSI Driver allows for the integration of an Azure Key Vault as a secret store with an Azure Kubernetes Service (AKS) cluster via a [CSI volume](https://kubernetes-csi.github.io/docs/).

## Features

- Mounts secrets, keys, and certificates to a pod using a CSI volume.
- Supports CSI inline volumes.
- Supports mounting multiple secrets store objects as a single volume.
- Supports pod portability with the
`SecretProviderClass`

CRD. - Supports Windows containers.
- Syncs with Kubernetes secrets.
- Supports autorotation of mounted contents and synced Kubernetes secrets.

## Limitations

- A container using a
`ConfigMap`

or`Secret`

as a`subPath`

volume mount does not receive automated updates when the secret is rotated. This is a Kubernetes limitation. To have the changes take effect, the application needs to reload the changed file by either watching for changes in the file system or by restarting the pod. For more information, see[Secrets Store CSI Driver known limitations](https://secrets-store-csi-driver.sigs.k8s.io/known-limitations.html#secrets-not-rotated-when-using-subpath-volume-mount). - The add-on creates a managed identity named
`azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Check that your version of the Azure CLI is 2.30.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

### Network

- If using network isolated clusters, it's recommended to
[set up private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service). - If the cluster has outbound type
`userDefinedRouting`

and uses a firewall device that can control outbound traffic based on domain names, such as Azure Firewall, ensure the[required outbound network rules and FQDNs are allowed](outbound-rules-control-egress#azure-key-vault-provider-for-secrets-store-csi-driver). - If you're restricting Ingress to the cluster, make sure ports
**9808**and**8095**are open.

### Roles

- The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Certificate User`

to access`key`

or`certificate`

[object types](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types). - The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Secrets User`

to access`secret`

[object type](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types).

## Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus2`

Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command with the`az aks create`

`--enable-addons azure-keyvault-secrets-provider`

parameter. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault. The following example creates an AKS cluster with the Azure Key Vault provider for Secrets Store CSI Driver enabled.Note

If you want to use Microsoft Entra Workload ID, you must also use the

`--enable-oidc-issuer`

and`--enable-workload-identity`

parameters, such as in the following example:`az aks create --name myAKSCluster --resource-group myResourceGroup --enable-addons azure-keyvault-secrets-provider --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --generate-ssh-keys`

The previous command creates a user-assigned managed identity,

`azureKeyvaultSecretsProvider`

, to access Azure resources. The following example uses this identity to connect to the key vault that stores the secrets, but you can also use other[identity access methods](csi-secrets-store-identity-access). Take note of the identity's`clientId`

in the output.`..., "addonProfiles": { "azureKeyvaultSecretsProvider": { ..., "identity": { "clientId": "<client-id>", ... } }`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command and enable the`az aks enable-addons`

`azure-keyvault-secrets-provider`

add-on. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault.`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Verify the Azure Key Vault provider for Secrets Store CSI Driver installation

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name myAKSCluster --resource-group myResourceGroup`

Verify the installation is finished using the

`kubectl get pods`

command, which lists all pods with the`secrets-store-csi-driver`

and`secrets-store-provider-azure`

labels in the kube-system namespace.`kubectl get pods -n kube-system -l 'app in (secrets-store-csi-driver,secrets-store-provider-azure)'`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE aks-secrets-store-csi-driver-4vpkj 3/3 Running 2 4m25s aks-secrets-store-csi-driver-ctjq6 3/3 Running 2 4m21s aks-secrets-store-csi-driver-tlvlq 3/3 Running 2 4m24s aks-secrets-store-provider-azure-5p4nb 1/1 Running 0 4m21s aks-secrets-store-provider-azure-6pqmv 1/1 Running 0 4m24s aks-secrets-store-provider-azure-f5qlm 1/1 Running 0 4m25s`

Verify that each node in your cluster's node pool has a Secrets Store CSI Driver pod and a Secrets Store Provider Azure pod running.


## Create or use an existing Azure Key Vault

Create or update a key vault with Azure role-based access control (Azure RBAC) enabled using the

command or the`az keyvault create`

command with the`az keyvault update`

`--enable-rbac-authorization`

flag. The name of the key vault must be globally unique. For more details on key vault permission models and Azure RBAC, see[Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)`## Create a new Azure key vault az keyvault create --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization ## Update an existing Azure key vault az keyvault update --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization`

Your key vault can store keys, secrets, and certificates. In this example, use the

command to set a plain-text secret called`az keyvault secret set`

`ExampleSecret`

.`az keyvault secret set --vault-name <keyvault-name> --name ExampleSecret --value MyAKSExampleSecret`

Take note of the following properties for future use:

- The name of the secret object in the key vault
- The object type (secret, key, or certificate)
- The name of your key vault resource
- The Azure tenant ID of the subscription


## Next steps

In this article, you learned how to use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster. You now need to provide an identity to access the Azure Key Vault. To learn how, continue to the next article.
