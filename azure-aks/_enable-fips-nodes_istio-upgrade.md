---
merged_at: 2026-01-25T12:06:27.852361
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: enable-fips-nodes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes -->

# Enable Federal Information Process Standard (FIPS) for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Federal Information Processing Standard (FIPS) 140-2 is a US government standard that defines minimum security requirements for cryptographic modules in information technology products and systems. Azure Kubernetes Service (AKS) allows you to create Linux and Windows node pools with FIPS 140-2 enabled. Deployments running on FIPS-enabled node pools can use those cryptographic modules to provide increased security and help meet security controls as part of FedRAMP compliance. For more information on FIPS 140-2, see [Federal Information Processing Standard (FIPS) 140](/en-us/azure/compliance/offerings/offering-fips-140-2).

Caution

In this article, there are references to a feature that may be using Ubuntu OS versions that are being deprecated for AKS.

- Starting on March 17, 2027, AKS will no longer support Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools.
[Upgrade your node pools](upgrade-aks-cluster)to kubernetes version 1.35+ to migrate to a supported Ubuntu version. For more information on this retirement, see[AKS GitHub Issues](https://github.com/Azure/AKS/issues)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Azure CLI version 2.32.0 or later installed and configured. To find the version, run `az --version`

. For more information about installing or upgrading the Azure CLI, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

AKS Monitoring Addon supports FIPS enabled node pools with Ubuntu, Azure Linux, and Windows starting with Agent version 3.1.17 (Linux) and Win-3.1.17 (Windows).

## Limitations

- FIPS-enabled node pools have the following limitations:
- FIPS-enabled node pools require Kubernetes version 1.19 and greater.
- To update the underlying packages or modules used for FIPS, you must use
[Node Image Upgrade](node-image-upgrade). - Container images on the FIPS nodes aren't assessed for FIPS compliance.
- Mounting of a CIFS share fails because FIPS disables some authentication modules. To work around this issue, see
[Errors when mounting a file share on a FIPS-enabled node pool](/en-us/troubleshoot/azure/azure-kubernetes/fail-to-mount-azure-file-share#fipsnodepool). - FIPS-enabled node pools with
[Arm64 VMs](use-arm64-vms)are only supported with Azure Linux 3.0+. - FIPS isn't supported with
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks).


Important

The FIPS-enabled Linux image is a different image than the default Linux image used for Linux-based node pools.

FIPS-enabled node images can have different version numbers, such as kernel version, than images that aren't FIPS-enabled. The update cycle for FIPS-enabled node pools and node images can differ from node pools and images that aren't FIPS-enabled.

## Supported OS Versions

You can create FIPS-enabled node pools on all supported OS types (Linux and Windows). However, not all OS versions support FIPS-enabled node pools. After a new OS version is released, there's typically a waiting period before it's FIPS compliant.

This table includes the supported OS versions:

| OS Type | OS SKU | FIPS Compliance |
|---|---|---|
| Linux | Ubuntu | Supported |
| Linux | Azure Linux | Supported |
| Windows | Windows Server 2019 | Supported |
| Windows | Windows Server 2022 | Supported |

When requesting FIPS enabled Ubuntu, if the default Ubuntu version doesn't support FIPS, AKS defaults to the most recent FIPS-supported version of Ubuntu. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support FIPS, AKS defaults to Ubuntu 20.04 for Linux FIPS-enabled node pools.

Note

Previously, you could use the GetOSOptions API to determine whether a given OS supported FIPS. The GetOSOptions API is now deprecated and it will no longer be included in new AKS API versions starting with 2024-05-01.

## Create a FIPS-enabled Linux node pool

Create a FIPS-enabled Linux node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image`

Note

You can also use the

`--enable-fips-image`

parameter with the[az aks create](/en-us/cli/azure/aks#az-aks-create)command when creating a cluster to enable FIPS on the default node pool. When adding node pools to a cluster created in this way, you still must use the`--enable-fips-image`

parameter when adding node pools to create a FIPS-enabled node pool.Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows the

*fipsnp*node pool is FIPS-enabled:`Name enableFips --------- ------------ fipsnp True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-fipsnp`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-fipsnp-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-fipsnp-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-fipsnp-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-fipsnp-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-fipsnp-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Create a FIPS-enabled Windows node pool

Create a FIPS-enabled Windows node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter. Unlike Linux-based node pools, Windows node pools share the same image set.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image \ --os-type Windows`

Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

Verify Windows node pools have access to the FIPS cryptographic libraries by

[creating an RDP connection to a Windows node](rdp)in a FIPS-enabled node pool and check the registry. From the**Run**application, enter`regedit`

.Look for

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FIPSAlgorithmPolicy`

in the registry.If

`Enabled`

is set to*1*, then FIPS is enabled.FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Update an existing node pool to enable or disable FIPS

Existing Linux node pools can be updated to enable or disable FIPS. If you're planning to migrate your node pools from non-FIPS to FIPS, first validate that your application is working properly in a test environment before migrating it to a production environment. Validating your application in a test environment should prevent issues caused by the FIPS kernel blocking some weak cipher or encryption algorithm, such as an MD4 algorithm that isn't FIPS compliant.

Note

When updating an existing Linux node pool to enable or disable FIPS, the node pool update moves between the fips and non-fips image. This node pool update triggers a reimage to complete the update. This can cause the node pool update to take a few minutes to complete.

### Prerequisites

Azure CLI version 2.64.0 or later. To find the version, run `az --version`

. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable FIPS on an existing node pool

Existing Linux node pools can be updated to enable FIPS. When you update an existing node pool, the node image changes from the current image to the recommended FIPS image of the same OS SKU.

Update a node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--enable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool is FIPS-enabled:`Name enableFips --------- ------------ np True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-np`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-np-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-np-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-np-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-np-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-np-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Disable FIPS on an existing node pool

Existing Linux node pools can be updated to disable FIPS. When updating an existing node pool, the node image changes from the current FIPS image to the recommended non-FIPS image of the same OS SKU. The node image change will occur after a reimage.

Update a Linux node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--disable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --disable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool isn't FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool isn't FIPS-enabled:`Name enableFips --------- ------------ np False nodepool1 False`


## Message of the Day

Pass the `--message-of-the-day`

flag with the location of the file to replace the Message of the Day on Linux nodes at cluster creation or node pool creation.

Create a cluster with message of the day using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


Add a node pool with message of the day using the [az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


## Next steps

To learn more about AKS security, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).


---

<!-- DOCUMENTO FUSIONADO: istio-upgrade.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-upgrade -->

# Upgrade Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article addresses upgrade experiences for Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To learn more about the release schedule and support for service mesh add-on revisions, read the [support policy](istio-support-policy#versioning-and-support-policy).

## Minor revision upgrade

Istio add-on allows upgrading the minor revision using [canary upgrade process](https://istio.io/latest/docs/setup/upgrade/canary/). When an upgrade is initiated, the control plane of the new (canary) revision is deployed alongside the initial (stable) revision's control plane. You can then manually roll over data plane workloads while using monitoring tools to track the health of workloads during this process. If you don't observe any issues with the health of your workloads, you can complete the upgrade so that only the new revision remains on the cluster. Else, you can roll back to the previous revision of Istio.

Available upgrades depend on whether the current Istio revision and AKS cluster version are supported:

- You can upgrade to the
**next supported revision (**or skip one and upgrade to`n+1`

), as long as both are supported and compatible with the cluster version.`n+2`

- If both your current revision (
`n`

) and the next revision (`n+1`

) are unsupported, you can only upgrade to the**nearest supported revision (**, but not beyond it.`n+2`

or higher) - If the cluster version and Istio revision are both unsupported, the cluster version must be upgraded before an Istio upgrade can be initiated.

Note

Once an AKS version or mesh revision falls outside the support window, upgrading either version becomes error-prone. While such upgrades are **allowed** to recover to a supported version, **the upgrade process and the out-of-support versions themselves are both not supported by Microsoft**. We strongly recommend keeping AKS version and mesh revision up to date to avoid running into unsupported scenarios. Refer to the [Istio add-on support calendar](istio-support-policy#service-mesh-add-on-release-calendar) for estimated release and end-of-life dates and the [upstream Istio release notes](https://istio.io/latest/news/releases/) for the new revision for notable changes.

The following example illustrates how to upgrade from revision `asm-1-23`

to `asm-1-24`

with all workloads in the `default`

namespace. The steps are the same for all minor upgrades and may be used for any number of namespaces.

Use the

[az aks mesh get-upgrades](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-upgrades)command to check which revisions are available for the cluster as upgrade targets:`az aks mesh get-upgrades --resource-group $RESOURCE_GROUP --name $CLUSTER`

If you expect to see a newer revision not returned by this command, you may need to upgrade your AKS cluster first so that it's compatible with the newest revision.

If you set up

[mesh configuration](istio-meshconfig)for the existing mesh revision on your cluster, you need to create a separate ConfigMap corresponding to the new revision in the`aks-istio-system`

namespace**before initiating the canary upgrade**in the next step. This configuration is applicable the moment the new revision's control plane is deployed on cluster. More details can be found[here](istio-meshconfig#mesh-configuration-and-upgrades).Initiate a canary upgrade from revision

`asm-1-23`

to`asm-1-24`

using[az aks mesh upgrade start](/en-us/cli/azure/aks/mesh/upgrade#az-aks-mesh-upgrade-start):`az aks mesh upgrade start --resource-group $RESOURCE_GROUP --name $CLUSTER --revision asm-1-24`

A canary upgrade means the 1.24 control plane is deployed alongside the 1.23 control plane. They continue to coexist until you either complete or roll back the upgrade.

While a canary upgrade is in progress, the higher revision is considered the

*default revision*used for validation of Istio resources.Optionally, revision tags may be used to roll over the data plane to the new revision without needing to manually relabel each namespace. Manually relabeling namespaces when moving them to a new revision can be tedious and error-prone.

[Revision tags](https://istio.io/latest/docs/setup/upgrade/canary/#stable-revision-labels)solve this problem by serving as stable identifiers that point to revisions.Rather than relabeling each namespace, a cluster operator can change the tag to point to a new revision. All namespaces labeled with that tag are updated at the same time. However, you still need to restart the workloads to make sure the correct version of

`istio-proxy`

sidecars are injected.To use revision tags during an upgrade:

Create a revision tag for the initial revision. In this example, we name it

`prod-stable`

:`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system`

Create a revision tag for the revision installed during the upgrade. In this example, we name it

`prod-canary`

:`istioctl tag set prod-canary --revision asm-1-24 --istioNamespace aks-istio-system`

Label application namespaces to map to revision tags:

`# label default namespace to map to asm-1-23 kubectl label ns default istio.io/rev=prod-stable --overwrite`

You may also label namespaces with

`istio.io/rev=prod-canary`

for the newer revision. However, the workloads in those namespaces aren't updated to a new sidecar until they're restarted.If a new application is created in a namespace after it is labeled, a sidecar will be injected corresponding to the revision tag on that namespace.


Verify control plane pods corresponding to both

`asm-1-23`

and`asm-1-24`

exist:Verify

`istiod`

pods:`kubectl get pods -n aks-istio-system`

Example output:

`NAME READY STATUS RESTARTS AGE istiod-asm-1-23-55fccf84c8-dbzlt 1/1 Running 0 58m istiod-asm-1-23-55fccf84c8-fg8zh 1/1 Running 0 58m istiod-asm-1-24-f85f46bf5-7rwg4 1/1 Running 0 51m istiod-asm-1-24-f85f46bf5-8p9qx 1/1 Running 0 51m`

If ingress is enabled, verify ingress pods:

`kubectl get pods -n aks-istio-ingress`

Example output:

`NAME READY STATUS RESTARTS AGE aks-istio-ingressgateway-external-asm-1-23-58f889f99d-qkvq2 1/1 Running 0 59m aks-istio-ingressgateway-external-asm-1-23-58f889f99d-vhtd5 1/1 Running 0 58m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-ft9c8 1/1 Running 0 51m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-wcb6s 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-4cc2l 1/1 Running 0 58m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-jjc7m 1/1 Running 0 59m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-g89s4 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-krq9w 1/1 Running 0 51m`

Observe that ingress gateway pods of both revisions are deployed side-by-side. However, the service and its IP remain immutable.


Relabel the namespace so that any new pods are mapped to the Istio sidecar associated with the new revision and its control plane:

If using revision tags, overwrite the

`prod-stable`

tag itself to change its mapping:`istioctl tag set prod-stable --revision asm-1-24 --istioNamespace aks-istio-system --overwrite`

Verify the tag-to-revision mappings:

`istioctl tag list`

Both tags should point to the newly installed revision:

`TAG REVISION NAMESPACES prod-canary asm-1-24 default prod-stable asm-1-24 ...`

In this case, you don't need to relabel each namespace individually.

If not using revision tags, data plane namespaces must be relabeled to point to the new revision:

`kubectl label namespace default istio.io/rev=asm-1-24 --overwrite`


Relabeling doesn't affect your workloads until they're restarted.

Individually roll over each of your application workloads by restarting them. For example:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Check your monitoring tools and dashboards to determine whether your workloads are all running in a healthy state after the restart. Based on the outcome, you have two options:

**Complete the canary upgrade**: If you're satisfied that the workloads are all running in a healthy state as expected, you can complete the canary upgrade. Completion of the upgrade removes the previous revision's control plane and leaves behind the new revision's control plane on the cluster. Run the following command to complete the canary upgrade:`az aks mesh upgrade complete --resource-group $RESOURCE_GROUP --name $CLUSTER`

**Rollback the canary upgrade**: In case you observe any issues with the health of your workloads, you can roll back to the previous revision of Istio:

Relabel the namespace to the previous revision: If using revision tags:

`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system --overwrite`

Or, if not using revision tags:

`kubectl label namespace default istio.io/rev=asm-1-23 --overwrite`

Roll back the workloads to use the sidecar corresponding to the previous Istio revision by restarting these workloads again:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Roll back the control plane to the previous revision:

`az aks mesh upgrade rollback --resource-group $RESOURCE_GROUP --name $CLUSTER`


The

`prod-canary`

revision tag can be removed:`istioctl tag remove prod-canary --istioNamespace aks-istio-system`

If

[mesh configuration](istio-meshconfig)was previously set up for the revisions, you can now delete the ConfigMap for the revision that was removed from the cluster during complete/rollback.

### Minor revision upgrades with ingress and egress gateways

If you're currently using [Istio ingress gateways](istio-deploy-ingress) or [egress gateways](istio-deploy-egress) and are performing a minor revision upgrade, keep in mind that Istio ingress and egress gateway pods / deployments are deployed per-revision, but the service is shared across both revisions.

We provide a single `LoadBalancer`

service across all ingress gateway pods over multiple revisions, so the external/internal IP address of the ingress gateways remains unchanged throughout the course of an upgrade. Thus, during the canary upgrade, when two revisions exist simultaneously on the cluster, the ingress gateway pods of both revisions serve incoming traffic.

Likewise, during a canary upgrade, all pods for an egress gateway across both revisions will be served by a single `ClusterIP`

service.

### Minor revision upgrades with horizontal pod autoscaling customizations

If you have customized [horizontal pod autoscaling (HPA) settings for Istiod or the ingress gateways](istio-scale#horizontal-pod-autoscaling-customization), note the following behavior for how HPA settings are applied across both revisions to maintain consistency during a canary upgrade:

- If you update the HPA spec before initiating an upgrade, the settings from the existing (stable) revision will be applied to the HPAs of the canary revision when the new control plane is installed.
- If you update the HPA spec while a canary upgrade is in progress, the HPA spec of the stable revision will take precedence and be applied to the HPA of the canary revision.
- If you update the HPA of the stable revision during an upgrade, the HPA spec of the canary revision will be updated to reflect the new settings applied to the stable revision.
- If you update the HPA of the canary revision during an upgrade, the HPA spec of the canary revision will be reverted to the HPA spec of the stable revision.


## Patch version upgrade

- Istio add-on patch version availability information is published in
[AKS release notes](https://github.com/Azure/AKS/releases). - Patches are rolled out automatically for istiod and ingress pods as part of these AKS releases, which respect the
`default`

[planned maintenance window](planned-maintenance)set up for the cluster. - User needs to initiate patches to Istio proxy in their workloads by restarting the pods for reinjection:
Check the version of the Istio proxy intended for new or restarted pods. This version is the same as the version of the istiod and Istio ingress pods after they were patched:

`kubectl get cm -n aks-istio-system -o yaml | grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`"image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless", "image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless"`

Check the Istio proxy image version for all pods in a namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.23.0, mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless`

To trigger reinjection, restart the workloads. For example:

`kubectl rollout restart deployments/productpage-v1 -n default`

To verify that they're now on the newer versions, check the Istio proxy image version again for all pods in the namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.2.0, mcr.microsoft.com/oss/istio/proxyv2:1.24.0-distroless`


Note

In case of any issues encountered during upgrades, refer to [article on troubleshooting mesh revision upgrades](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-minor-revision-upgrade)
