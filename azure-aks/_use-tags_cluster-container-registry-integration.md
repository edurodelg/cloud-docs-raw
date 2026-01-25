---
merged_at: 2026-01-25T12:25:33.928867
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-tags.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-tags -->

# Use Azure tags in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Azure Kubernetes Service (AKS), you can set Azure tags on an AKS cluster and its related resources using Azure Resource Manager and the Azure CLI. You can also use Kubernetes manifests to set Azure tags for certain resources. Azure tags are a useful tracking resource for certain business processes, such as *chargeback*.

This article explains how to set Azure tags for AKS clusters and related resources.

## Before you begin

Review the following information before you begin:

- Tags set on an AKS cluster apply to all resources related to the cluster, but not the node pools. This operation overwrites the values of existing keys.
- Tags set on a node pool apply only to resources related to that node pool. This operation overwrites the values of existing keys. Resources outside that node pool, including resources for the rest of the cluster and other node pools, are unaffected.
- Public IPs, files, and disks can have tags set by Kubernetes through a Kubernetes manifest. Tags set in this way maintain the Kubernetes values, even if you update them later using a different method. When you remove public IPs, files, or disks through Kubernetes, any tags set by Kubernetes are removed. The tags on those resources that Kubernetes doesn't track remain unaffected.

### Prerequisites

- The Azure CLI version 2.0.59 or later. To find your version, run
`az --version`

. If you need to install it or update your version, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version 1.20 or later.

### Limitations

- Azure tags have keys that are case-insensitive for operations, such as when you're retrieving a tag by searching the key. In this case, a tag with the specified key is updated or retrieved regardless of casing. Tag values are case-sensitive.
- In AKS, if multiple tags are set with identical keys but different casing, the tags are used in alphabetical order. For example,
`{"Key1": "val1", "kEy1": "val2", "key1": "val3"}`

results in`Key1`

and`val1`

being set. - For shared resources, tags can't determine the split in resource usage on their own.

## Azure tags and AKS clusters

When you create or update an AKS cluster with the `--tags`

parameter, the following are assigned the Azure tags that you specified:

- The AKS cluster itself and its related resources:
- Route table
- Public IP
- Load balancer
- Network security group
- Virtual network
- AKS-managed kubelet msi
- AKS-managed add-on msi
- Private DNS zone associated with the
*private cluster* - Private endpoint associated with the
*private cluster*

- The node resource group

Note

Azure Private DNS only supports 15 tags. For more information, see the [tag resources](/en-us/azure/azure-resource-manager/management/tag-resources).

## Create or update tags on an AKS cluster

### Create a new AKS cluster

Important

If you're using existing resources when you create a new cluster, such as an IP address or route table, the `az aks create`

command overwrites the set of tags. If you delete the cluster later, any tags set by the cluster are removed.

Create a cluster and assign Azure tags using the

command with the`az aks create`

`--tags`

parameter.Note

To set tags on the initial node pool, the virtual machine scale set, and each virtual machine scale set instance associated with the initial node pool, you can also set the

`--nodepool-tags`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags dept=IT costcenter=9999 \ --generate-ssh-keys`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "dept": "IT", "costcenter": "9999" } }`


### Update an existing AKS cluster

Important

Setting tags on a cluster using the `az aks update`

command overwrites the set of tags. For example, if your cluster has the tags *dept=IT* and *costcenter=9999*, and you use `az aks update`

with the tags *team=alpha* and *costcenter=1234*, the new list of tags would be *team=alpha* and *costcenter=1234*.

Update the tags on an existing cluster using the

command with the`az aks update`

`--tags`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags team=alpha costcenter=1234`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "team": "alpha", "costcenter": "1234" } }`


## Add tags to node pools

You can apply an Azure tag to a new or existing node pool in your AKS cluster. Tags applied to a node pool are applied to each node within the node pool and are persisted through upgrades. Tags are also applied to new nodes that are added to a node pool during scale-out operations. Adding a tag can help with tasks such as policy tracking or cost estimation.

When you create or update a node pool with the `--tags`

parameter, the tags you specify are assigned to the following resources:

- The node pool.
- The virtual machine scale set and each virtual machine scale set instance associated with the node pool.

### Create a new node pool

Create a node pool with an Azure tag using the

command with the`az aks nodepool add`

`--tags`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --node-count 1 \ --tags abtest=a costcenter=5555 \ --no-wait`

Verify that the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "abtest": "a", "costcenter": "5555" } } ]`


### Update an existing node pool

Important

Setting tags on a node pool using the `az aks nodepool update`

command overwrites the set of tags. For example, if your node pool has the tags *abtest=a* and *costcenter=5555*, and you use `az aks nodepool update`

with the tags *appversion=0.0.2* and *costcenter=4444*, the new list of tags would be *appversion=0.0.2* and *costcenter=4444*.

Update a node pool with an Azure tag using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --tags appversion=0.0.2 costcenter=4444 \ --no-wait`

Verify the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "appversion": "0.0.2", "costcenter": "4444" } } ]`


## Add tags using Kubernetes

Important

Setting tags on files, disks, and public IPs using Kubernetes updates the set of tags. For example, if your disk has the tags *dept=IT* and *costcenter=5555*, and you use Kubernetes to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=3333*.

Any updates you make to tags through Kubernetes retain the value set through Kubernetes. For example, if your disk has tags *dept=IT* and *costcenter=5555* set by Kubernetes, and you use the portal to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=5555*. If you then remove the disk through Kubernetes, the disk would have the tag *team=beta*.

You can apply Azure tags to public IPs, disks, and files using a Kubernetes manifest.

For public IPs, use

*service.beta.kubernetes.io/azure-pip-tags*under*annotations*. For example:`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-pip-tags: costcenter=3333,team=beta spec: ...`

For files and disks, use

*tags*under*parameters*. For example:`--- apiVersion: storage.k8s.io/v1 ... parameters: ... tags: costcenter=3333,team=beta ...`


## Next steps

Learn more about [using labels in an AKS cluster](use-labels).


---

<!-- DOCUMENTO FUSIONADO: cluster-container-registry-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cluster-container-registry-integration -->

# Authenticate with Azure Container Registry (ACR) from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When using [Azure Container Registry (ACR)](/en-us/azure/container-registry/container-registry-intro) with Azure Kubernetes Service (AKS), you need to establish an authentication mechanism. You can configure the required permissions between ACR and AKS using the Azure CLI, Azure PowerShell, or Azure portal. This article provides examples to configure authentication between these Azure services using the Azure CLI or Azure PowerShell.

The AKS to ACR integration assigns the [ AcrPull role](/en-us/azure/role-based-access-control/built-in-roles#acrpull) to the

[Microsoft Entra ID](/en-us/azure/active-directory/managed-identities-azure-resources/overview)associated with the agent pool in your AKS cluster. For more information on AKS managed identities, see

**managed identity**[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Important

There's a latency issue with Microsoft Entra groups when attaching ACR. If the **AcrPull** role is granted to a Microsoft Entra group and the kubelet identity is added to the group to complete the RBAC configuration, there may be a delay before the RBAC group takes effect. If you're running automation that requires the RBAC configuration to be complete, we recommend you use [Bring your own kubelet identity](use-managed-identity#create-a-kubelet-managed-identity) as a workaround. You can pre-create a user-assigned identity, add it to the Microsoft Entra group, then use the identity as the kubelet identity to create an AKS cluster. This ensures the identity is added to the Microsoft Entra group before a token is generated by kubelet, which avoids the latency issue.

Note

This article covers automatic authentication between AKS and ACR. If you need to pull an image from a private external registry, use an [image pull secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/).

Caution

The AKS-ACR integration through `az aks --attach-acr`

is not supported for ABAC-enabled ACR registries where the role assignment permissions mode is set to "RBAC Registry + ABAC Repository Permissions." ABAC-enabled ACR registries require the [ Container Registry Repository Reader role](/en-us/azure/role-based-access-control/built-in-roles#container-registry-repository-reader) instead of the

`AcrPull`

role for granting image pull permissions. For ABAC-enabled ACR registries, you should not use `az aks --attach-acr`

but instead manually assign the `Container Registry Repository Reader`

role assignment using either the Azure Portal, `az role assignment`

CLI, or Azure Resource Manager. Please visit [https://aka.ms/acr/auth/abac](https://aka.ms/acr/auth/abac)for more information on ABAC-enabled ACR registries.

## Before you begin

- You need the
,**Owner**, or**Azure account administrator**role on your Azure subscription.**Azure co-administrator**- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
[Use an Azure managed identity to authenticate to an ACR](/en-us/azure/container-registry/container-registry-authentication-managed-identity).

- To avoid needing one of these roles, you can instead use an existing managed identity to authenticate ACR from AKS. For more information, see
- If you're using Azure CLI, this article requires that you're running Azure CLI version 2.7.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Examples and syntax to use Terraform for configuring ACR can be found in the
[Terraform reference](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_registry).

## Create a new ACR

If you don't already have an ACR, create one using the

command. The following example sets the`az acr create`

`MYACR`

variable to the name of the ACR,*mycontainerregistry*, and uses the variable to create the registry. Your ACR name must be globally unique and use only lowercase letters.`MYACR=mycontainerregistry az acr create --name $MYACR --resource-group myContainerRegistryResourceGroup --sku basic`


## Create a new AKS cluster and integrate with an existing ACR

Create a new AKS cluster and integrate with an existing ACR using the

command with the`az aks create`

. This command allows you to authorize an existing ACR in your subscription and configures the appropriate`--attach-acr`

parameter**AcrPull**role for the managed identity.`MYACR=mycontainerregistry az aks create --name myAKSCluster --resource-group myResourceGroup --generate-ssh-keys --attach-acr $MYACR`

This command may take several minutes to complete.

Note

If you're using an ACR located in a different subscription from your AKS cluster or would prefer to use the ACR

*resource ID*instead of the ACR name, you can do so using the following syntax:`az aks create -n myAKSCluster -g myResourceGroup --generate-ssh-keys --attach-acr /subscriptions/<subscription-id>/resourceGroups/myContainerRegistryResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry`


## Configure ACR integration for an existing AKS cluster

### Attach an ACR to an existing AKS cluster

Integrate an existing ACR with an existing AKS cluster using the

command with the`az aks update`

and a valid value for`--attach-acr`

parameter**acr-name**or**acr-resource-id**.`# Attach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-name> # Attach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --attach-acr <acr-resource-id>`

Note

The

`az aks update --attach-acr`

command uses the permissions of the user running the command to create the ACR role assignment. This role is assigned to the[kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)managed identity. For more information on AKS managed identities, see[Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

### Detach an ACR from an AKS cluster

Remove the integration between an ACR and an AKS cluster using the

command with the`az aks update`

and a valid value for`--detach-acr`

parameter**acr-name**or**acr-resource-id**.`# Detach using acr-name az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-name> # Detach using acr-resource-id az aks update --name myAKSCluster --resource-group myResourceGroup --detach-acr <acr-resource-id>`


## Working with ACR & AKS

### Import an image into your ACR

Import an image from Docker Hub into your ACR using the

command.`az acr import`

`az acr import --name <acr-name> --source docker.io/library/nginx:latest --image nginx:v1`


### Deploy the sample image from ACR to AKS

Ensure you have the proper AKS credentials using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a file called

**acr-nginx.yaml**using the following sample YAML and replace**acr-name**with the name of your ACR.`apiVersion: apps/v1 kind: Deployment metadata: name: nginx0-deployment labels: app: nginx0-deployment spec: replicas: 2 selector: matchLabels: app: nginx0 template: metadata: labels: app: nginx0 spec: containers: - name: nginx image: <acr-name>.azurecr.io/nginx:v1 ports: - containerPort: 80`

Run the deployment in your AKS cluster using the

`kubectl apply`

command.`kubectl apply -f acr-nginx.yaml`

Monitor the deployment using the

`kubectl get pods`

command.`kubectl get pods`

The output should show two running pods, as shown in the following example output:

`NAME READY STATUS RESTARTS AGE nginx0-deployment-669dfc4d4b-x74kr 1/1 Running 0 20s nginx0-deployment-669dfc4d4b-xdpd6 1/1 Running 0 20s`


### Troubleshooting

- Validate the registry is accessible from the AKS cluster using the
command.`az aks check-acr`

- Learn more about
[ACR monitoring](/en-us/azure/container-registry/monitor-service). - Learn more about
[ACR health](/en-us/azure/container-registry/container-registry-check-health).
