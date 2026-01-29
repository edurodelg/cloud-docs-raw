---
merged_at: 2026-01-29T15:23:36.553011
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-ssh-node-access -->

# Manage SSH for secure access to Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to configure SSH access (preview) on your AKS clusters or node pools, during initial deployment or at a later time.

AKS supports the following configuration options to manage SSH access on cluster nodes:

**Disabled SSH**: Completely disable SSH access to cluster nodes for enhanced security**Entra ID based SSH**: Use Microsoft Entra ID credentials for SSH authentication. Benefits of using Entra ID based SSH:**Centralized identity management**: Use your existing Entra ID identities to access cluster nodes**No SSH key management**: Eliminates the need to generate, distribute, and rotate SSH keys**Enhanced security**: Leverage Entra ID security features like Conditional Access and MFA**Audit and compliance**: Centralized logging of access events through Entra ID logs**Just-in-time access**: Combine with Azure RBAC for granular access control

**Local User SSH**: Traditional SSH key-based authentication for node access

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires version 2.61.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.

You need

`aks-preview`

version 9.0.0b1 or later.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
Register the

`DisableSSHPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "DisableSSHPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "DisableSSHPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires version 2.73.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.

You need

`aks-preview`

version 19.0.0b7 or later for Entra ID SSH.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
Appropriate Azure RBAC permissions to access nodes:

**Required action**:`Microsoft.Compute/virtualMachineScaleSets/*/read`

- to read Virtual Machine Scale Sets information**Required data action**:`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/login/action`

- to authenticate and log in to VMs as regular user.`Microsoft.Compute/virtualMachines/loginAsAdmin/action`

- to login with root user privileges.

**Built-in role**:or**Virtual Machine Administrator Login**(for non-admin access)**Virtual Machine User Login**


Register the

`EntraIdSSHPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EntraIdSSHPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EntraIdSSHPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.61.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You need
`aks-preview`

version 9.0.0b1 or later to update SSH access method on nodepools.- If you don't already have the
`aks-preview`

extension, install it using thecommand:`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand:`az extension update`

`az extension update --name aks-preview`


- If you don't already have the

### Set environment variables

Set the following environment variables for your resource group, cluster name, and location:

```
export RESOURCE_GROUP="<your-resource-group-name>"
export CLUSTER_NAME="<your-cluster-name>"
export LOCATION="<your-azure-region>"
```


## Limitations

- Entra ID SSH to nodes is not yet available for Windows node pool.
- Entra ID SSH to nodes is not supported for AKS automatic because of
[node resource group lockdown](node-resource-group-lockdown)preventing role assignments.

## Configure SSH access

To improve security and support your corporate security requirements or strategy, AKS supports disabling SSH both on the cluster and at the node pool level. Disable SSH introduces a simplified approach compared to configuring [network security group rules](concepts-security#azure-network-security-groups) on the AKS subnet/node network interface card (NIC). Disable SSH only supports Virtual Machine Scale Sets node pools.

When you disable SSH at cluster creation time, it takes effect after the cluster is created. However, when you disable SSH on an existing cluster or node pool, AKS doesn't automatically disable SSH. At any time, you can choose to perform a nodepool upgrade operation. The disable/enable SSH operation takes effect after the node image update is complete.

Note

When you disable SSH at the cluster level, it applies to all existing node pools. Any node pools created after this operation will have SSH enabled by default, and you'll need to run these commands again in order to disable it.

Note

[kubectl debug node](node-access) continues to work after you disable SSH because it doesn't depend on the SSH service.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Disable SSH on a new cluster deployment

By default, the SSH service on AKS cluster nodes is open to all users and pods running on the cluster. You can prevent direct SSH access from any network to cluster nodes to help limit the attack vector if a container in a pod becomes compromised.

Use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command to create a new cluster, and include the

`--ssh-access disabled`

argument to disable SSH (preview) on all the node pools during cluster creation.Important

After you disable the SSH service, you can't SSH into the cluster to perform administrative tasks or to troubleshoot.

Note

On a newly created cluster, disable SSH will only configure the first system node pool. All other node pools need to be configured at the node pool level.

```
az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


### Disable SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command to add a node pool, and include the

`--ssh-access disabled`

argument to disable SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster indicating *mynodepool* was successfully created. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


### Disable SSH for an existing node pool

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access disabled`

argument to disable SSH (preview) on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access disabled
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster indicating *mynodepool* was successfully updated. The following example resembles the output and the results related to disabling SSH:

```
"securityProfile": {
"sshAccess": "Disabled"
},
```


For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


Important

To disable SSH on an existing cluster, you need to disable SSH for each node pool on this cluster.

### Re-enable SSH access

To re-enable SSH access on a node pool, update the node pool with either `--ssh-access localuser`

(for traditional SSH key-based access) or `--ssh-access entraid`

(for Entra ID based access). See the respective sections for detailed instructions.

You can configure your AKS cluster to use Microsoft Entra ID (formerly Azure AD) for SSH authentication to cluster nodes. This eliminates the need to manage SSH keys and allows you to use your Entra ID credentials to access nodes securely.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Enable Entra ID based SSH on a new cluster

Use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH authentication during cluster creation.```
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


### Enable Entra ID based SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information indicating *mynodepool* was successfully created with Entra ID based SSH. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


### Enable Entra ID based SSH for an existing node pool

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access entraid`

argument to enable Entra ID based SSH on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access entraid
```


After a few minutes, the command completes and returns JSON-formatted information indicating *mynodepool* was successfully updated with Entra ID based SSH. The following example resembles the output:

```
"securityProfile": {
"sshAccess": "EntraID"
},
```


For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


Important

To enable Entra ID based SSH on an existing cluster, you need to enable it for each node pool individually.

Local user SSH access uses traditional SSH key-based authentication. This is the default SSH access method for AKS clusters.

### Create a resource group

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $RESOURCE_GROUP --location $LOCATION
```


### Create an AKS cluster with SSH keys

Use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command to deploy an AKS cluster with an SSH public key. You can either specify the key or a key file using the `--ssh-key-value`

argument, or use `--ssh-access localuser`

to explicitly set local user SSH access.

| SSH parameter | Description | Default value |
|---|---|---|
`--generate-ssh-key` |
If you don't have your own SSH keys, specify `--generate-ssh-key` . The Azure CLI automatically generates a set of SSH keys and saves them in the default directory `~/.ssh/` . |
|
`--ssh-key-value` |
Public key path or key contents to install on node VMs for SSH access. For example, `ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm` . |
`~/.ssh/id_rsa.pub` |
`--ssh-access localuser` |
Explicitly enable local user SSH access with key-based authentication. | |
`--no-ssh-key` |
If you don't require SSH keys, specify this argument. However, AKS automatically generates a set of SSH keys because the Azure Virtual Machine resource dependency doesn't support an empty SSH keys file. As a result, the keys aren't returned and can't be used to SSH into the node VMs. The private key is discarded and not saved. |

Note

If no parameters are specified, the Azure CLI defaults to referencing the SSH keys stored in the `~/.ssh/id_rsa.pub`

file. If the keys aren't found, the command returns the message `An RSA key file or key value must be supplied to SSH Key Value`

.

**Examples:**

To create a cluster and use the default generated SSH keys:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --generate-ssh-key`

To specify an SSH public key file:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value ~/.ssh/id_rsa.pub`

To explicitly enable local user SSH access:

`az aks create --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-access localuser --generate-ssh-key`


### Enable local user SSH for a new node pool

Use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command with the

`--ssh-access localuser`

argument to enable local user SSH during node pool creation.```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access localuser
```


### Enable local user SSH for an existing node pool

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command with the

`--ssh-access localuser`

argument to enable local user SSH on an existing node pool.```
az aks nodepool update \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--ssh-access localuser
```


Important

For the change to take effect, you need to reimage the node pool by using the [ az aks nodepool upgrade](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade) command.

```
az aks nodepool upgrade \
--cluster-name $CLUSTER_NAME \
--name mynodepool \
--resource-group $RESOURCE_GROUP \
--node-image-only
```


### Update SSH public key on an existing AKS cluster

Use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command to update the SSH public key (preview) on your cluster. This operation updates the key on all node pools. You can either specify a key or a key file using the

`--ssh-key-value`

argument.Note

Updating the SSH keys is supported on Azure virtual machine scale sets with AKS clusters.

**Examples:**

To specify a new SSH public key value:

`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value 'ssh-rsa AAAAB3Nza-xxx'`

To specify an SSH public key file:

`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --ssh-key-value ~/.ssh/id_rsa.pub`


Important

After you update the SSH key, AKS doesn't automatically update your node pool. At any time, you can choose to perform a [nodepool upgrade operation](node-image-upgrade). The update SSH keys operation takes effect after a node image update is complete. For clusters with [Node Auto-provisioning](node-autoprovision) enabled, a node image update can be performed by applying a new label to the Kubernetes NodePool custom resource.

## Verify SSH service status

After disabling SSH, you can verify that the SSH service is inactive on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is disabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n○ ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; disabled; vendor preset: enabled)\n Active: inactive (dead) since Wed 2024-01-03 15:36:53 UTC; 25min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: inactive (dead)`

, which confirms SSH is disabled on the node.

After enabling Entra ID based SSH, you can verify that the SSH service is active and configured for Entra ID authentication on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is enabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n● ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)\n Active: active (running) since Wed 2024-01-03 15:40:20 UTC; 19min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: active (running)`

, which confirms SSH is enabled on the node.

After configuring local user SSH, you can verify that the SSH service is active on your cluster nodes.

Use the Virtual Machine Scale Set [ az vmss run-command invoke](/en-us/cli/azure/vmss/run-command#az-vmss-run-command-invoke) command to check SSH service status.

```
az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 0 --scripts "systemctl status ssh"
```


The following sample output shows the expected result when SSH is enabled:

```
{
"value": [
{
"code": "ProvisioningState/succeeded",
"displayStatus": "Provisioning succeeded",
"level": "Info",
"message": "Enable succeeded: \n[stdout]\n● ssh.service - OpenBSD Secure Shell server\n Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)\n Active: active (running) since Wed 2024-01-03 15:40:20 UTC; 19min ago\n..."
}
]
}
```


Search for the word **Active** and verify that its value is `Active: active (running)`

, which confirms SSH is enabled on the node.

## Next steps

To help troubleshoot any issues with SSH connectivity to your clusters nodes, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes master node logs](monitor-aks-reference#resource-logs).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app -->

# Tutorial - Prepare an application for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this tutorial, you prepare a multi-container application to use in Kubernetes. You use existing development tools like Docker Compose to locally build and test the application. You learn how to:

- Clone a sample application source from GitHub.
- Create a container image from the sample application source.
- Test the multi-container application in a local Docker environment.

Once completed, the following application runs in your local development environment:

In later tutorials, you upload the container image to an Azure Container Registry (ACR), and then deploy it into an AKS cluster.

## Before you begin

This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and `docker`

commands. For a primer on container basics, see [Get started with Docker](https://docs.docker.com/get-started/).

To complete this tutorial, you need a local Docker development environment running Linux containers. Docker provides packages that configure Docker on a [Mac](https://docs.docker.com/desktop/install/mac-install/), [Windows](https://docs.docker.com/desktop/install/windows-install/), or [Linux](https://docs.docker.com/desktop/install/linux-install/) system.

Note

Azure Cloud Shell doesn't include the Docker components required to complete every step in these tutorials. Therefore, we recommend using a full Docker development environment.

## Get application code

The [sample application](https://github.com/Azure-Samples/aks-store-demo) used in this tutorial is a basic store front app including the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Use

[git](https://git-scm.com/downloads)to clone the sample application to your development environment.`git clone https://github.com/Azure-Samples/aks-store-demo.git`

Change into the cloned directory.

`cd aks-store-demo`


## Review Docker Compose file

The sample application you create in this tutorial uses the [ docker-compose-quickstart YAML file](https://github.com/Azure-Samples/aks-store-demo/blob/main/docker-compose-quickstart.yml) from the

[repository](https://github.com/Azure-Samples/aks-store-demo/tree/main)you cloned.

```
services:
rabbitmq:
image: rabbitmq:3.13.2-management-alpine
container_name: 'rabbitmq'
restart: always
environment:
- "RABBITMQ_DEFAULT_USER=username"
- "RABBITMQ_DEFAULT_PASS=password"
ports:
- 15672:15672
- 5672:5672
healthcheck:
test: ["CMD", "rabbitmqctl", "status"]
interval: 30s
timeout: 10s
retries: 5
volumes:
- ./rabbitmq_enabled_plugins:/etc/rabbitmq/enabled_plugins
networks:
- backend_services
order-service:
build: src/order-service
container_name: 'order-service'
restart: always
ports:
- 3000:3000
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://order-service:3000/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- ORDER_QUEUE_HOSTNAME=rabbitmq
- ORDER_QUEUE_PORT=5672
- ORDER_QUEUE_USERNAME=username
- ORDER_QUEUE_PASSWORD=password
- ORDER_QUEUE_NAME=orders
- ORDER_QUEUE_RECONNECT_LIMIT=3
networks:
- backend_services
depends_on:
rabbitmq:
condition: service_healthy
product-service:
build: src/product-service
container_name: 'product-service'
restart: always
ports:
- 3002:3002
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://product-service:3002/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- AI_SERVICE_URL=http://ai-service:5001/
networks:
- backend_services
store-front:
build: src/store-front
container_name: 'store-front'
restart: always
ports:
- 8080:8080
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://store-front:80/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3002/
- VUE_APP_ORDER_SERVICE_URL=http://order-service:3000/
networks:
- backend_services
depends_on:
- product-service
- order-service
networks:
backend_services:
driver: bridge
```


## Create container images and run application

You can use [Docker Compose](https://docs.docker.com/compose/) to automate building container images and the deployment of multi-container applications.

### Docker

Create the container image, download the RabbitMQ image, and start the application using the

`docker compose`

command:`docker compose -f docker-compose-quickstart.yml up -d`

View the created images using the

command.`docker images`

`docker images`

The following condensed example output shows the created images:

`REPOSITORY TAG IMAGE ID aks-store-demo-product-service latest 72f5cd7e6b84 aks-store-demo-order-service latest 54ad5de546f9 aks-store-demo-store-front latest 1125f85632ae ...`

View the running containers using the

command.`docker ps`

`docker ps`

The following condensed example output shows four running containers:

`CONTAINER ID IMAGE f27fe74cfd0a aks-store-demo-product-service df1eaa137885 aks-store-demo-order-service b3ce9e496e96 aks-store-demo-store-front 31df28627ffa rabbitmq:3.13.2-management-alpine`


## Test application locally

To see your running application, navigate to `http://localhost:8080`

in a local web browser. The sample application loads, as shown in the following example:

, you can view products, add them to your cart, and then place an order.

## Clean up resources

Since you validated the application's functionality, you can stop and remove the running containers. * Do not delete the container images* - you use them in the next tutorial.

Stop and remove the container instances and resources using the

command.`docker-compose down`

`docker compose down`


## Next steps

In this tutorial, you created a sample application, created container images for the application, and then tested the application. You learned how to:

- Clone a sample application source from GitHub.
- Create a container image from the sample application source.
- Test the multi-container application in a local Docker environment.

In the next tutorial, you learn how to store container images in an ACR.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-autoscale -->

# Autoscaling CoreDNS in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure and customize CoreDNS autoscaling in Azure Kubernetes Service (AKS) clusters.

## Configure CoreDNS horizontal pod scaling

Due to the elastic nature of AKS, it's common to experience sudden spikes in DNS traffic within your clusters. These spikes can lead to an increase in memory consumption by CoreDNS pods. In some cases, this increased memory consumption can cause `Out of memory`

issues.

To preempt this issue, AKS clusters autoscale CoreDNS pods to reduce memory usage per pod. The default settings for this autoscaling logic are stored in the `coredns-autoscaler`

ConfigMap. However, you might observe that the default autoscaling of CoreDNS pods isn't always aggressive enough to prevent `Out of memory`

issues for your CoreDNS pods. In this case, you can directly modify the `coredns-autoscaler`

ConfigMap. Keep in mind that simply increasing the number of CoreDNS pods without addressing the root cause of the `Out of memory`

issue might only provide a temporary fix. If there's not enough memory available across the nodes where the CoreDNS pods are running, increasing the number of CoreDNS pods won't help. You might need to investigate further and implement appropriate solutions such as optimizing resource usage, adjusting resource requests and limits, or adding more memory to the nodes.

CoreDNS uses the [horizontal cluster proportional autoscaler](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler) for pod autoscaling. You can edit the `coredns-autoscaler`

to configure the scaling logic for the number of CoreDNS pods. The `coredns-autoscaler`

ConfigMap currently supports two different ConfigMap key values: `linear`

and `ladder`

, which correspond to two supported control modes.

- The
`linear`

controller yields a number of replicas in [min,max] range equivalent to`max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

. - The
`ladder`

controller calculates the number of replicas by consulting two different step functions, one for core scaling and another for node scaling, yielding the max of the two replica values.

For more information on the control modes and ConfigMap format, see the [upstream documentation](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler#control-patterns-and-configmap-formats).

Important

We recommend a minimum of *two* CoreDNS pod replicas per cluster.

### View the current `coredns-autoscaler`

ConfigMap

Get the current

`coredns-autoscaler`

ConfigMap using thecommand.`kubectl get configmaps`

`kubectl get configmap coredns-autoscaler --namespace kube-system --output yaml`

Your output should resemble the following example output:

`apiVersion: v1 data: ladder: '{"coresToReplicas":[[1,2],[512,3],[1024,4],[2048,5]],"nodesToReplicas":[[1,2],[8,3],[16,4],[32,5]]}' kind: ConfigMap metadata: name: coredns-autoscaler namespace: kube-system resourceVersion: "..." creationTimestamp: "..."`


Note

The configuration provided serves as a potential starting point, but you should customize the values based on your specific cluster requirements and DNS traffic patterns. One way to determine the appropriate number of replicas for your environment is to use the linear scaling formula: `replicas = max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

to determine replica counts based on core / node count in the cluster.

## CoreDNS vertical pod autoscaling behavior

CoreDNS uses the original provided resource requests/limits when enabling the [add-on autoscaling feature](optimized-addon-scaling) to prevent service unavailability during the CoreDNS pod restart process.

The following table outlines the default requests/limits and request-to-limit ratios for the AKS CoreDNS add-on:

| Resource | Requests/limits | Request-to-limit ratio |
|---|---|---|
| CPU | `100 m / 3 cores` |
Approximately 1:30 |
| Memory | `70 Mi / 500 Mi` |
Approximately 1:7 |

If the recommended CPU requests are *500 m*, VPA adjusts the CPU limits to *15* to maintain this ratio. Similarly, if the recommended memory requests are *700 Mi*, VPA adjusts the memory limit to *5000 Mi*.

VPA sets CoreDNS CPU and memory limits to large values based on the VPA recommended CPU/Memory request and AKS defined request-to-limit ratio. These adjustments are beneficial for handling multiple requests during peak service times. The drawback is that CoreDNS might consume all the CPU and memory available resource on the node when the peak service time.

It's difficult to set a single ideal CPU and memory requests/limits value to meet the requirements of both large cluster and small cluster at the same time. By enabling optimized add-on scaling, you have the flexibility to customize the CoreDNS CPU and memory requests/limits or use VPA to autoscale CoreDNS to meet specific cluster requirements. Keep the following scenarios in mind when deciding whether to customize the resource configuration or use VPA:

- You're considering whether VPA is suitable for your CoreDNS service and want to only view the VPA recommendations. You can disable VPA for CoreDNS by enabling the override VPA update mode to
*Off*if you don't want VPA to automatically update the pods.[Customize the resource configuration in Deployment](customize-resource-configuration)to set the CPU/Memory requests/limits to the value you prefer. - You're considering using VPA but want to restrict the ratio of request-to-limit so VPA won't bump the CPU and Memory limit to large values at one time. You can customize resources in the Deployment and update the CPU and Memory requests/limits value to keep the ratio of request-to-limit to
*1:2*or*1:3*. - If a VPA container policy sets maxAllowed CPU and Memory, the recommended resource requests won't exceed those limits. Customizing the resource configuration allows you to increase or decrease the maxAllowed values and control the recommendations of VPA.

For more information, see [Enable add-on autoscaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Next steps

To learn how to troubleshoot CoreDNS issues, see [Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)](coredns-troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-about -->

# Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

Kubernetes Event-driven Autoscaling (KEDA) is a single-purpose and lightweight component that strives to make application autoscaling simple and is a Cloud Native Computing Federation (CNCF) Graduate project.

It applies event-driven autoscaling to scale your application to meet demand in a sustainable and cost-efficient manner with scale-to-zero.

The KEDA add-on makes it even easier by deploying a managed KEDA installation, providing you with [a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) that you can scale your applications with on your Azure Kubernetes Services (AKS) cluster.

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.32.

For more information on how to securely scale your applications with workload identity, read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Architecture

[KEDA](https://keda.sh/) provides two main components:

**KEDA operator**allows end-users to scale workloads in or out from 0 to N instances with support for Kubernetes Deployments, Jobs,`StatefulSets`

, or any custom resource that defines`/scale`

subresource.**Metrics server**exposes external metrics to Horizontal Pod Autoscaler (HPA) in Kubernetes for autoscaling purposes such as messages in a Kafka topic, or number of events in an Azure event hub. Due to upstream limitations, KEDA must be the only installed external metric adapter.


Learn more about how KEDA works in the [official KEDA documentation](https://keda.sh/docs/latest/concepts/).

## Installation

KEDA can be added to your Azure Kubernetes Service (AKS) cluster by enabling the KEDA add-on using an [ARM template](keda-deploy-add-on-arm) or [Azure CLI](keda-deploy-add-on-cli).

The KEDA add-on provides a fully supported installation of KEDA that is integrated with AKS.

## Capabilities and features

KEDA provides the following capabilities and features:

- Build sustainable and cost-efficient applications with scale-to-zero
- Scale application workloads to meet demand using
[a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) - Autoscale applications with
`ScaledObjects`

, such as Deployments,`StatefulSets`

, or any custom resource that defines`/scale`

subresource - Autoscale job-like workloads with
`ScaledJobs`

- Use production-grade security by decoupling autoscaling authentication from workloads
- Bring-your-own external scaler to use tailor-made autoscaling decisions
- Integrate with
[Microsoft Entra Workload ID](workload-identity-overview)for authentication

Note

If you plan to use workload identity, [enable the workload identity add-on](workload-identity-deploy-cluster) before enabling the KEDA add-on.

## Add-on limitations

The KEDA AKS add-on has the following limitations:

- KEDA's
[HTTP add-on (preview)](https://github.com/kedacore/http-add-on)to scale HTTP workloads isn't installed with the extension, but can be deployed separately. - KEDA's
[external scaler for Azure Cosmos DB](https://github.com/kedacore/external-scaler-azure-cosmos-db)to scale based on Azure Cosmos DB change feed isn't installed with the extension, but can be deployed separately. - Only one external metric server is allowed in the Kubernetes cluster. Because of that the KEDA add-on should be the only external metrics server inside the cluster.
- Multiple KEDA installations aren't supported

- It's not recommended to combine KEDA's
`ScaledObject`

with a Horizontal Pod Autoscaler (HPA) to scale the same workload. They compete with each other because KEDA uses Horizontal Pod Autoscaler (HPA) in the background and results in odd scaling behavior.- If an HPA is created first, then a KEDA
`ScaledObject`

is created and the KEDA`ScaledObject`

would fail to be created. - If a KEDA
`ScaledObject`

is created first and then an HPA is created, the HPA creation isn't blocked.

- If an HPA is created first, then a KEDA

For general KEDA questions, we recommend [visiting the FAQ overview](https://keda.sh/docs/2.14/reference/faq/).

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

## Supported Kubernetes and KEDA versions

Your cluster Kubernetes version determines which KEDA version is installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/faq -->

# AKS frequently asked questions

This article provides answers to some of the most common questions about Azure Kubernetes Service (AKS).

## Support

### Does AKS offer a service-level agreement?

AKS provides service-level agreement (SLA) guarantees in the [Standard pricing tier with the Uptime SLA feature](free-standard-pricing-tiers).

### What is platform support, and what does it include?

Platform support is a reduced support plan for unsupported n-3 version clusters. Platform support includes only Azure infrastructure support.

For more information, see the [platform support policy](supported-kubernetes-versions).

### Does AKS automatically upgrade my unsupported clusters?

Yes, AKS initiates auto-upgrades for unsupported clusters. When a cluster in an n-3 version (where *n* is the latest supported AKS minor version that's generally available) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support policy.

For more information, see [Supported Kubernetes versions](supported-kubernetes-versions), [Planned maintenance windows](planned-maintenance), and [Automatic upgrades](auto-upgrade-cluster).

### Can I apply Azure reservation discounts to my AKS agent nodes?

AKS agent nodes are billed as standard Azure virtual machines (VMs). If you purchased [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) for the VM size that you're using in AKS, those discounts are automatically applied.

## Operations

### Can I run Windows Server containers on AKS?

Yes, AKS supports Windows Server containers. For more information, see the [Windows Server on AKS FAQ](windows-faq).

### What Linux operating systems (OS) are supported on AKS?

AKS supports four main Linux operating systems, including Ubuntu Linux, [Azure Linux](use-azure-linux), [Azure Linux OS Guard](use-azure-linux-os-guard), and [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks). When specifying `--os-type Linux`

during node pool creation or cluster creation, the default OS is Ubuntu Linux.

### What operating systems (OS) versions are supported on AKS?

When using `--os-sku Ubuntu`

, AKS defaults to Ubuntu 22.04 in Kubernetes versions 1.25-1.34. AKS defaults to Ubuntu 24.04 in Kubernetes versions 1.35+.
When using `--os-sku AzureLinux`

, AKS defaults to Azure Linux 3.0 in Kubernetes versions 1.32+.
In some scenarios, like FIPS-enabled node pools, the default OS version might differ. See [node images](node-images) for more information.

### Can I move or migrate my cluster between Azure tenants?

No. Moving your AKS cluster between tenants is currently unsupported.

### Can I move or migrate my cluster between subscriptions?

No. Moving your AKS cluster between subscriptions is currently unsupported.

### Can I move my AKS cluster or AKS infrastructure resources to other resource groups or rename them?

No. Moving or renaming your AKS cluster and its associated resources isn't supported.

### Can I restore my cluster after I delete it?

No. You can't restore your cluster after you delete it. When you delete your cluster, the node resource group and all its resources are also deleted.

If you want to keep any of your resources, move them to another resource group before you delete your cluster. If you want to protect against accidental deletes, you can lock the AKS managed resource group that's hosting your cluster resources by using [Node resource group lockdown](node-resource-group-lockdown).

### Can I scale my AKS cluster to zero?

You can completely [stop a running AKS cluster](start-stop-cluster) or [scale or autoscale all or specific User node pools](scale-cluster#scale-user-node-pools-to-0) to zero.

You can't directly scale [system node pools](use-system-pools) to zero.

### Can I use the virtual machine scale set APIs to scale manually?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS APIs (`az aks scale`

).

### Can I use virtual machine scale sets to manually scale to zero nodes?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS API to scale nonsystem node pools to zero or [stop your cluster](start-stop-cluster) instead.

### Can I stop or deallocate all my VMs?

No. This configuration isn't supported. [Stop your cluster](start-stop-cluster) instead.

### Why are two resource groups created with AKS?

AKS builds upon many Azure infrastructure resources, including virtual machine scale sets, virtual networks, and managed disks. These integrations enable you to apply many of the core capabilities of the Azure platform within the managed Kubernetes environment provided by AKS. For example, you can use most Azure VM types directly with AKS, and you can use Azure Reservations to receive discounts on those resources automatically.

To enable this architecture, each AKS deployment spans two resource groups:

- You create the first resource group. This group contains only the Kubernetes service resource. The AKS resource provider automatically creates the second resource group during deployment. An example of the second resource group is
*MC_myResourceGroup_myAKSCluster_eastus*. For information on how to specify the name of this second resource group, see the next section. - The second resource group, known as the
*node resource group*, contains all of the infrastructure resources associated with the cluster. These resources include the Kubernetes node VMs, virtual networking, and storage. By default, the node resource group has a name like*MC_myResourceGroup_myAKSCluster_eastus*. AKS automatically deletes the node resource group whenever you delete the cluster. Use this resource group only for resources that share the cluster's lifecycle.

Note

Modifying any resource under the node resource group in the AKS cluster is an unsupported action and will cause cluster operation failures. You can prevent changes from being made to the node resource group. [Block users from modifying resources](node-resource-group-lockdown) that the AKS cluster manages.

### Can I provide my own name for the AKS node resource group?

By default, AKS names the node resource group *MC_resourcegroupname_clustername_location*, but you can provide your own name.

To specify your own resource group name, install the [aks-preview](/en-us/cli/azure/aks) Azure CLI extension version *0.3.2* or later. When you create an AKS cluster by using the `az aks create`

command, use the `--node-resource-group`

parameter and specify a name for the resource group. If you use an [Azure Resource Manager template](/en-us/azure/templates/microsoft.containerservice/2022-09-01/managedclusters) to deploy an AKS cluster, you can define the resource group name by using the `nodeResourceGroup`

property.

- The Azure resource provider automatically creates the secondary resource group.
- You can specify a custom resource group name only when you create the cluster.

As you work with the node resource group, you can't:

- Specify an existing resource group for the node resource group.
- Specify a different subscription for the node resource group.
- Change the node resource group name after you create the cluster.
- Specify names for the managed resources within the node resource group.
- Modify or delete Azure-created tags of managed resources within the node resource group.

### Can I modify tags and other properties of the AKS resources in the node resource group?

You might get unexpected scaling and upgrading errors if you modify or delete Azure-created tags and other resource properties in the node resource group. AKS allows you to create and modify custom tags created by end users, and you can add those tags when you [create a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool). You might want to create or modify custom tags, for example, to assign a business unit or cost center. Another option is to apply policies and modify tags through the AKS resource itself—specifically via the cluster and node pools..

Azure-created tags are created for their respective Azure services, and you should always allow them. For AKS, there are the `aks-managed`

and `k8s-azure`

tags. Modifying any *Azure-created tags* on resources under the node resource group in the AKS cluster is an unsupported action, which breaks the service-level objective (SLO).

Note

In the past, the tag name `Owner`

was reserved for AKS to manage the public IP that's assigned on the front-end IP of the load balancer. Now, services use the `aks-managed`

prefix. For legacy resources, don't use Azure policies to apply the `Owner`

tag name. Otherwise, all resources on your AKS cluster deployment and update operations will break. This restriction doesn't apply to newly created resources.

### Why do I see aks-managed prefixed Helm releases on my cluster, and why does their revision count keep increasing?

AKS uses Helm to deliver components to your cluster. You can safely ignore `aks-managed`

prefixed Helm releases. Continuously increasing revisions on these Helm releases are expected and safe.

## Quotas, limits, and region availability

### Which Azure regions currently provide AKS?

For a complete list of available regions, see [AKS regions and availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

### Can I spread an AKS cluster across regions?

No. AKS clusters are regional resources and can't span regions. For guidance on how to create an architecture that includes multiple regions, see [best practices for business continuity and disaster recovery](operator-best-practices-multi-region#plan-for-multiregion-deployment).

### Can I spread an AKS cluster across availability zones?

Yes, you can deploy an AKS cluster across one or more [availability zones](availability-zones) in [regions that support them](/en-us/azure/reliability/availability-zones-region-support).

### Can I have different VM sizes in a single cluster?

Yes, you can use different VM sizes in your AKS cluster by creating [multiple node pools](create-node-pools).

### What's the size limit on a container image in AKS?

AKS doesn't set a limit on the container image size. But the larger the image, the higher the memory demand. A larger size could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is excessively large, as in the terabyte (TB) range, the kubelet might not be able to pull it from your container registry to a node because of the lack of disk space.

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. You should perform an upgrade on the cluster and the Windows Server node pools in your AKS cluster. Follow a regular schedule based on the Windows Update release cycle and your own validation process. This upgrade process creates nodes that run the latest Windows Server image and patches, and then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

### Are AKS images required to run as root?

The following images have functional requirements to run as root, and exceptions must be filed for any policies:

*mcr.microsoft.com/oss/kubernetes/coredns**mcr.microsoft.com/azuremonitor/containerinsights/ciprod**mcr.microsoft.com/oss/calico/node**mcr.microsoft.com/oss/kubernetes-csi/azuredisk-csi*

## Security, access, and identity

### Can I limit who has access to the Kubernetes API server?

Yes, there are two options for limiting access to the API server:

- Use
[API server authorized IP ranges](api-server-authorized-ip-ranges)if you want to maintain a public endpoint for the API server but restrict access to a set of trusted IP ranges. - Use a
[private cluster](private-clusters)if you want to limit the API server to be accessible*only*from within your virtual network.

### Are security updates applied to AKS agent nodes?

AKS patches CVEs that have a *vendor fix* every week. CVEs without a fix are waiting on a vendor fix before they can be remediated. The AKS images are automatically updated within 30 days. We recommend that you apply an updated node image on a regular cadence to ensure that the latest patched images and OS patches are all applied and current. You can do this task:

- Manually, through the Azure portal or the Azure CLI.
- By upgrading your AKS cluster. The cluster upgrades
[cordon and drain nodes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)automatically. Then it brings a new node online with the latest Ubuntu image and a new patch version or a minor Kubernetes version. For more information, see[Upgrade an AKS cluster](upgrade-cluster). - By using a
[node image upgrade](node-image-upgrade).

### Are there security threats that target AKS that I should be aware of?

Microsoft provides guidance for other actions that you can take to secure your workloads through services like [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks). For information on a security threat related to AKS and Kubernetes, see [New large-scale campaign targets Kubeflow](https://techcommunity.microsoft.com/t5/azure-security-center/new-large-scale-campaign-targets-kubeflow/ba-p/2425750) (June 8, 2021).

### Does AKS store any customer data outside the cluster's region?

No. All data is stored in the cluster's region.

### How can I avoid permission ownership setting slow issues when the volume has numerous files?

Traditionally, if your pod is running as a nonroot user (which it should), you must specify an `fsGroup`

parameter inside the pod's security context so that the volume is readable and writable by the pod. For more information on this requirement, see [Configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

A side effect of setting `fsGroup`

is that each time a volume is mounted, Kubernetes must use the `chown()`

and `chmod()`

commands recursively for all the files and directories inside the volume (with a few exceptions). This scenario happens even if group ownership of the volume already matches the requested `fsGroup`

parameter. This configuration might be expensive for larger volumes with lots of small files, which can cause pod startup to take a long time. This scenario was a known problem before v1.20. The workaround is to set the pod to run as root:

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
runAsUser: 0
fsGroup: 0
```


The issue was resolved with Kubernetes version 1.20. For more information, see [Kubernetes 1.20: Granular control of volume permission changes](https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/).

## Networking

### How does the managed control plane communicate with my nodes?

AKS uses a secure tunnel communication to allow the `api-server`

and individual node kubelets to communicate, even on separate virtual networks. The tunnel is secured through mutual Transport Layer Security encryption. The current main tunnel that AKS uses is [Konnectivity, previously known as apiserver-network-proxy](https://kubernetes.io/docs/tasks/extend-kubernetes/setup-konnectivity/). Verify that all network rules follow the [Azure required network rules and fully qualified domain names (FQDNs)](limit-egress-traffic).

### Can my pods use the API server FQDN instead of the cluster IP?

Yes, you can add the annotation `kubernetes.azure.com/set-kube-service-host-fqdn`

to pods to set the `KUBERNETES_SERVICE_HOST`

variable to the domain name of the API server instead of the in-cluster service IP. This modification is useful in cases where your cluster egress is done via a layer 7 firewall. An example is when you use Azure Firewall with application rules.

### Can I configure NSGs with AKS?

AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. AKS modifies only the network interface NSG settings. If you're using Container Network Interface (CNI), you also must ensure that the security rules in the NSGs allow traffic between the node and pod classless interdomain routing (CIDR) ranges. If you're using kubenet, you must also ensure that the security rules in the NSGs allow traffic between the node and pod CIDR. For more information, see [Network security groups](concepts-network#network-security-groups).

### How does time synchronization work in AKS?

AKS nodes run the chrony service, which pulls time from the local host. Containers that run on pods get the time from the AKS nodes. Applications that open inside a container use time from the container of the pod.

## Add-ons, extensions, and integrations

### Can I use custom VM extensions?

No. AKS is a managed service. Manipulation of the infrastructure as a service (IaaS) resources isn't supported. To install custom components, use the Kubernetes APIs and mechanisms. For example, use DaemonSets to install any required components.

### What Kubernetes admission controllers does AKS support? Can admission controllers be added or removed?

AKS supports the following [admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/):

`NamespaceLifecycle`

`LimitRanger`

`ServiceAccount`

`DefaultIngressClass`

`DefaultStorageClass`

`DefaultTolerationSeconds`

`MutatingAdmissionWebhook`

`ValidatingAdmissionWebhook`

`ResourceQuota`

`PodNodeSelector`

`PodTolerationRestriction`

`ExtendedResourceToleration`


Currently, you can't modify the list of admission controllers in AKS.

### Can I use admission controller webhooks on AKS?

Yes, you can use admission controller webhooks on AKS. We recommend that you exclude internal AKS namespaces, which are marked with the `control-plane`

label. For example:

```
namespaceSelector:
matchExpressions:
- key: control-plane
operator: DoesNotExist
```


AKS firewalls the API server egress so that your admission controller webhooks need to be accessible from within the cluster.

### Can admission controller webhooks affect kube-system and internal AKS namespaces?

To protect the stability of the system and prevent custom admission controllers from affecting internal services in the `kube-system`

namespace, AKS has an admissions enforcer, which automatically excludes `kube-system`

and AKS internal namespaces. This service ensures that the custom admission controllers don't affect the services that run in `kube-system`

.

If you have a critical use case for deploying something on `kube-system`

(not recommended) in support of your custom admission webhook, you can add the following label or annotation so that the admissions enforcer ignores it:

- Label:
`"admissions.enforcer/disabled": "true"`

- Annotation:
`"admissions.enforcer/disabled": true`


### Is Azure Key Vault integrated with AKS?

[Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-driver) provides native integration of Azure Key Vault into AKS.

### Can I use FIPS cryptographic libraries with deployments on AKS?

Nodes that are enabled with Federal Information Processing Standards (FIPS) are now supported on Linux-based node pools. For more information, see [Add a FIPS-enabled node pool](enable-fips-nodes).

### How are AKS add-ons updated?

Any patch, including a security patch, is automatically applied to the AKS cluster. Anything bigger than a patch, like major or minor version changes (which can have breaking changes to your deployed objects), are updated when you update your cluster if a new release is available. For information on when a new release is available, see [AKS release notes](https://github.com/Azure/AKS/releases).

### What is the purpose of the AKS Linux extension that I see installed on my Linux virtual machine scale sets instances?

The AKS Linux extension is an Azure VM extension that installs and configures monitoring tools on Kubernetes worker nodes. The extension is installed on all new and existing Linux nodes. It configures the following monitoring tools:

[Node-exporter](https://github.com/prometheus/node_exporter): Collects hardware telemetry from the VM and makes it available by using a metrics endpoint. Then, a monitoring tool, such as Prometheus, can scrap these metrics.[Node-problem-detector](https://github.com/kubernetes/node-problem-detector): Aims to make various node problems visible to upstream layers in the cluster management stack. It's a systemd unit that runs on each node, detects node problems, and reports them to the cluster's API server by using`Events`

and`NodeConditions`

.[ig](https://go.microsoft.com/fwlink/p/?linkid=2260320): Is an eBPF-powered open-source framework for debugging and observing Linux and Kubernetes systems. It provides a set of tools (or gadgets) that gather relevant information that users can use to identify the cause of performance issues, crashes, or other anomalies. Notably, its independence from Kubernetes enables users to employ it also for debugging control plane issues.

These tools help provide observability around many node health-related problems, such as:

**Infrastructure daemon issues:**NTP service down**Hardware issues:**Bad CPU, memory, or disk**Kernel issues:**Kernel deadlock, corrupted file system**Container runtime issues:**Unresponsive runtime daemon

The extension *doesn't require extra outbound access* to any URLs, IP addresses, or ports beyond the [documented AKS egress requirements](limit-egress-traffic). It doesn't require any special permissions granted in Azure. It uses `kubeconfig`

to connect to the API server to send the monitoring data that's collected.

## Troubleshoot cluster issues

### Why is it taking so long to delete my cluster?

Most clusters are deleted upon user request. In some cases, especially cases where you bring your own resource group or perform cross-resource group tasks, deletion can take more time or even fail. If you have an issue with deletions, double-check that you don't have locks on the resource group. Also make sure that any resources outside the resource group are disassociated from the resource group.

### Why is it taking so long to create or update my cluster?

If you have issues with creating and updating clusters, make sure that you don't have any assigned policies or service constraints that might block your AKS cluster from managing resources like VMs, load balancers, or tags.

### If I have pods or deployments in NodeLost or Unknown states, can I still upgrade my cluster?

You can, but we don't recommend it. Perform updates when the state of the cluster is known and healthy.

### If I have a cluster with one or more nodes in an Unhealthy state, or if it's shut down, can I perform an upgrade?

No. Delete or remove any nodes that are in a failed state or otherwise from the cluster before you upgrade.

### I tried to delete my cluster, but I see the error "[Errno 11001] getaddrinfo failed."

Most commonly, this error arises if you have one or more NSGs in use that are still associated with the cluster. Remove them and attempt to delete the cluster again.

### I ran an upgrade, but now my pods are in crash loops and readiness probes fail.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

### My cluster was working, but suddenly I can't provision load balancers or mount persistent volume claims.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

## Retirements and deprecations

### Which Linux OS versions are deprecated on AKS?

Starting on March 17, 2027, Azure Kubernetes Service (AKS) no longer supports or provides security updates Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

### Which Windows OS versions are deprecated on AKS?

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).
Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-policy-best-practices -->

# Best practices for network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes, by default, operates as a flat network where all pods can communicate freely with each other. This unrestricted connectivity can be convenient for developers but poses significant security risks as applications scale. Imagine an organization deploying multiple microservices, each handling sensitive data, customer transactions, or backend operations. Without any restrictions, any compromised pod could potentially access unauthorized data or disrupt services.

To address these security concerns, [Network Policies in Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/) allow administrators to control and restrict traffic between workloads. They provide a declarative way to enforce traffic rules, ensuring secure and controlled network behavior within a cluster.

## What is Kubernetes Network Policy?

A Network Policy in Kubernetes is a set of rules that control how pods communicate with each other and with external services. It provides fine-grained control over network traffic, allowing administrators to enforce security and segmentation at the namespace level. By implementing Network Policies, you gain:

**Stronger security posture**: Prevent unauthorized lateral movement within the cluster.**Compliance and governance**: Enforce regulatory requirements by controlling communication pathways.**Reduced blast radius**: Limit the impact of a compromised workload by restricting its network access.

Initially, Network Policies were designed to operate at Layer 3 (IP) and Layer 4 (TCP/UDP) of the OSI model, enabling basic control over pod-to-pod and external communications. However, advanced network policy engines like Cilium have extended Network Policies to Layer 7 (Application Layer), allowing deeper control over application traffic for modern cloud-native applications.

Network Policies are defined at the namespace level, meaning each policy applies to workloads within a specific namespace. The main components of a Network Policy include:

**Pod selector**: Defines which pods the policy applies to based on labels.**Ingress rules**: Specify the allowed incoming connections.**Egress rules**: Specify the allowed outgoing connections.**Policy types**: Define whether the policy applies to ingress (incoming), egress (outgoing), or both.

## Foundations of building effective network policies

Building effective network policies in Kubernetes isn't just about writing YAML configurations—it requires a deep understanding of your application architecture, traffic patterns, and security requirements. Without a clear picture of how workloads communicate, enforcing security policies can lead to unintended disruptions or gaps in protection. The following sections cover how to systematically approach network policy design.

### Understanding your workload connectivity

Before implementing network policies, you need visibility into how workloads communicate with each other and external services. This step ensures that policies don’t inadvertently block critical traffic while effectively limiting unnecessary exposure.

**Leverage Visibility Tools:**in addition to the network requirements provided by application team you can use tools like[Cilium Hubble](https://github.com/cilium/hubble), and[Retina](https://retina.sh/)help you analyze pod-to-pod traffic, identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database. Identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database.**The importance of labels in network policies:**Traditionally, network security policies have relied on static IP addresses to define traffic rules. This approach is problematic in Kubernetes because pods are ephemeral—created and destroyed frequently, often with dynamically assigned IP addresses. Maintaining security rules based on constantly changing IPs would require continuous updates, making policy management inefficient and error-prone.

Labels solve this challenge by providing a stable way to group workloads. Instead of relying on fixed IPs, Kubernetes Network Policies use labels to define security rules that remain consistent even as pods restart or shift across nodes. For example, a policy can allow communication between pods labeled `app: frontend`

and `app: backend`

, ensuring traffic flows as intended regardless of pod IP changes. This label-based approach is critical for achieving scalable, intent-driven network security in cloud-native environments.

A well-defined labeling strategy simplifies policy management, reduces misconfigurations, and enhances security enforcement across clusters.

**Define Micro-segmentation:**Organizing workloads into security zones (e.g., frontend, backend, database) helps enforce the principle of least privilege. For instance, microservices handling customer transactions should be isolated from general-purpose applications.

### Layered security approach for Kubernetes

Relying solely on basic Kubernetes Network Policies might not be sufficient for all security needs. A layered approach ensures comprehensive protection across different levels of network communication.

**(L3/L4) policies**: The foundation of network security, controlling traffic based on pod labels and namespaces at the IP, port, and protocol level.**FQDN-based policies**: Restrict egress traffic to specific external domains, ensuring workloads can only reach approved external services (for example: only allowing access to*microsoft.com*for API calls).**Layer 7 policies**: Introduces fine-grained control over traffic by filtering requests based on HTTP methods, headers, and paths. This is useful for securing APIs and enforcing application-layer security policies.

### Management of Network Policies

Who should manage network policies? This often depends on an organization’s structure and security requirements. A well-balanced approach allows both security teams and application developers to collaborate effectively.

**Centralized security administration**: Security or networking teams should define baseline policies to enforce global security requirements, such as default deny-all rules or compliance-driven restrictions.**Developer autonomy with guardrails**: Application teams should be able to define service-specific network policies within their namespaces, enabling security while maintaining agility.**Policy lifecycle management**: Regularly reviewing and updating policies ensures that security remains aligned with evolving application architectures. Observability tools can help detect policy misconfigurations and missing rules.

#### Example: Securing a multi-tier web application with Network Policies

**Step 1: Understanding workload connectivity**

- Visibility tools: Use Cilium Hubble to observe how pods communicate.


Mapping connectivity:

Source Destination Protocol Port Frontend Backend TCP 8080 Backend Database TCP 5432 Backend External Payment Gateway TCP 443

**Step 2: Applying labels for policy enforcement**

By labeling workloads correctly, policies can remain stable even if pod IPs change.

`app: frontend`

for UI pods.`app: backend`

for API pods.`app: database`

for DB pods.

**Step 3: Implementing application-level Network Policies**

In this example, we use two layers of network policies: an L3/L4 basic policy to control traffic between microservices and a fully qualified domain name (FQDN) policy to control egress traffic with external payment gateway.

| Allow frontend to communicate with backend | Allow backend to access the database | Allow backend to reach external payment API |
|---|---|---|
Policy 1: Frontend egress`to:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 8080` Policy 2: Backend ingress`from:` ` - podSelector:` ` matchLabels:` ` app: frontend` ` ports:` ` - protocol: TCP` ` port: 8080` |
Policy 1: Backend egress`to:` ` - podSelector:` ` matchLabels:` ` app: database` ` ports:` ` - protocol: TCP` ` port: 5432` Policy 2: Database ingress`from:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 5432` |
Policy 1: Backend`spec:` ` endpointSelector:` ` matchLabels:` ` app: backend` ` egress:` ` - toFQDNs:` ` - matchName: payments.example.com` ` ports:` ` - protocol: TCP` ` port: 443` |

**Step 4: Managing and maintaining policies**

Security and platform teams enforce baseline deny rules.

Baseline policy Platform policy Security - Default deny all traffic - Allow DNS

- Allow Logs- Block traffic

to known

malicious IPs

and domainsEnsuring that the application's network policies comply with platform and security requirements while avoiding any policy violations.

**Baseline****Platform policy****Security policy****Allow frontend to communicate with backend****Allow backend to access the database****Allow backend to reach external payment API**- Default deny all traffic - Allow DNS

- Allow Logs- Block traffic to known malicious IPs and domains **Policy 1: Frontend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 8080


**Policy 2: Backend ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: frontend

ports:

-**protocol:**TCP

port: 8080**Policy 1: Backend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: database

ports:

-**protocol:**TCP

port: 5432


**Policy 2: Database ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 5432**Policy 1: Backend**

**spec:**

**endpointSelector:**

**matchLabels:**

app: backend

**egress:**

-**toFQDNs:**

-**matchName:**payments.example.com

**ports:**

-**protocol:**TCP

port: 443This structured approach ensures security without disrupting application functionality.


## Azure Powered by Cilium

[Azure Container Network Interface (CNI) powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium) leverages eBPF (extended Berkeley Packet Filter) to provide high-performance networking, observability, and security for Kubernetes workloads. Unlike traditional CNIs that rely on iptables-based packet filtering, Azure CNI powered by Cilium uses eBPF to operate at the kernel level, enabling efficient and scalable network policy enforcement. On Azure Kubernetes Service (AKS), Cilium is the only supported network policy engine, reflecting Azure’s investment in performance, scalability, and security.
Azure Kubernetes Service integrates Cilium as a managed component, simplifying network security enforcement. Administrators can define Cilium Network Policies directly within their AKS clusters without requiring external controllers.

Cilium extends the usage of labels with Identities. Large clusters with many pods might experience scale issues where constantly updating IP filters occurs with a high pod churn rate. Under the hood, Identities map to labels and allow connections to initiate as soon as the identity resolves rather than needing to update rules on nodes.

With Azure CNI powered by Cilium you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

Use the following command to create a cluster with Azure CNI powered by cilium

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


### Anatomy of the Cilium Network Policy

With Azure CNI powered by Cilium, you can configure network policies natively in Kubernetes using two available formats:

**The standard**, which supports L3 and L4 policies at ingress or egress of the Pod.`NetworkPolicy`

resource**The extended**, which is available as a CustomResourceDefinition that supports specification of policies at Layers 3-7 for both ingress and egress.`CiliumNetworkPolicy`

format

With these CRDs, we can define security policies, and Kubernetes automatically distributes these policies to all the nodes in the cluster.

A Network Policy consists of several key components:

**Pod selector**: Specifies which pods the policy applies to using labels.**Policy types**: Determines whether the policy applies to ingress (incoming traffic), egress (outgoing traffic), or both.**Ingress rules**: Defines allowed sources (pods, namespaces, or IP ranges) and ports.**Egress rules**: Defines allowed destinations and ports.`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: frontend-egress namespace: default spec: podSelector: matchLabels: app: frontend policyTypes: - Egress egress: - to: - podSelector: matchLabels: app: backend ports: - protocol: TCP port: 8080`


## Advanced Network Policy

Azure Kubernetes services offers the [Advanced Container Networking Service (ACNS)](/en-us/azure/aks/advanced-container-networking-services-overview?tabs=cilium) a suite of services designed to enhance the networking capabilities of AKS clusters.

A key feature of ACNS is Container Network Security, which offers advanced security functionalities to safeguard containerized workloads. One notable aspect is the ability to implement advanced network policies, including Fully Qualified Domain Name (FQDN) filtering and Layer 7 (L7) policies, allowing for more granular control over both egress traffic and application-layer communication.

### Secure Egress traffic with FQDN Filtering

Traditionally, network policies in Kubernetes are based on IP addresses. However, in dynamic environments where pod IPs frequently change, managing such policies becomes cumbersome. [FQDN filtering](/en-us/azure/aks/container-network-security-concepts#overview-of-fqdn-filtering) simplifies this by allowing policies to be defined using domain names instead of IP addresses. This approach provides a more intuitive and user-friendly method of controlling network traffic, allowing organizations to enforce security policies with greater precision and flexibility.

Implementing FQDN filtering in AKS clusters requires enabling ACNS and configuring the necessary policies to define allowed or blocked domains, thereby enhancing the security posture of your containerized applications.

To enable Advanced Container Networking Services (ACNS) in Azure Kubernetes Service (AKS), use the flag --enable-acns

#### Example: Enable Advanced Container Networking Services on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Build a network policy that allows traffic to “bing.com”

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


### Protection and security for APIs with L7 policies

As modern applications increasingly rely on APIs for communication, securing these interactions at the network layer alone is no longer sufficient. Standard network policies operate at Layer 3 (IP) and Layer 4 (TCP/UDP), controlling which pods can communicate, but they lack visibility into the actual API requests being made.

Layer 7 (L7) policies provide the following benefits and features:

**Granular API security**: Enforce policies based on HTTP, gRPC, or Kafka request data, rather than just IP addresses and ports.**Reduced attack surface**: Prevent unauthorized access and mitigate API-based attacks by filtering traffic at the application layer.**Compliance and auditing**: Ensure adherence to security standards by logging and controlling specific API interactions.**Simplified policy management**: Avoid the operational burden of additional sidecar proxies by leveraging built-in Cilium-powered L7 controls.

L7 policies AKS are enabled through ACNS and are available to customers using Azure CNI powered by Cilium. These policies support HTTP, gRPC, and Kafka protocols.

To enforce L7 policies, customers define `CiliumNetworkPolicy`

resources, specifying rules for application-layer traffic control.

#### Example: Enable ACNS on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Allow only GET requests to /api from the frontend pod to the backend service on port 8080

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


## Strategies for network policies

Securing Kubernetes workloads requires a thoughtful approach to defining and enforcing network policies. A well-designed strategy ensures that applications communicate only as intended, reducing the risk of unauthorized access, lateral movement, and potential breaches. The following sections cover key strategies for implementing effective Kubernetes Network Policies.

### Adopt a Zero-Trust model

By default, Kubernetes allows unrestricted communication between all pods in a cluster. A Zero-Trust approach dictates that no traffic should be trusted by default, and only explicitly allowed communication paths should be permitted. Implementing a default deny-all network policy ensures that only necessary traffic flows between workloads.

Example of a deny-all policy:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny
namespace: default
spec:
podSelector: {}
policyTypes:
- Ingress
- Egress
```


### Namespace and multi-tenancy segmentation

In multi-tenant environments, namespaces help isolate workloads. Different teams typically manage their applications within dedicated namespaces, ensuring logical isolation between workloads. This separation is critical when multiple applications run alongside each other. Applying network policies at the namespace scope is often the first step in securing workloads, as it prevents unrestricted lateral movement between applications managed by different teams.

For example, restrict all ingress traffic to a namespace, allowing only traffic from the same namespace:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-cross-namespace
namespace: team-a
spec:
podSelector: {}
policyTypes:
- Ingress
ingress:
- from:
- namespaceSelector:
matchLabels:
name: team-a
```


### Microsegmentation for workload isolation

While namespace-based segmentation is an essential first step in securing multi-tenant Kubernetes clusters, application-level microsegmentation provides fine-grained control over how workloads interact within a namespace. Namespace isolation alone does not prevent unintended or unauthorized communication between different applications within the same namespace. This is where pod-level segmentation becomes critical.

For instance, if a frontend service should only talk to a backend service within the same namespace, a policy using pod labels can enforce this restriction:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: frontend-to-backend
namespace: team-a
spec:
podSelector:
matchLabels:
app: frontend
policyTypes:
- Egress
egress:
- to:
- podSelector:
matchLabels:
app: backend
ports:
- protocol: TCP
port: 8080
```


This prevents frontend pods from making unintended connections to other services, reducing the risk of unauthorized access or lateral movement inside the namespace.

By combining namespace-wide isolation with fine-grained application-level policies, teams can implement a multi-layered security model that prevents unauthorized traffic while allowing necessary communication for application functionality.

### Layered security approach

Network security should be implemented in layers, combining multiple levels of enforcement:

**L3/L4 policies**: Restrict traffic at the IP and port level (for example: allow TCP traffic on port 443).**FQDN-based filtering**: Restrict external communication based on domain names rather than IP addresses.**L7 policies**: Control communication based on application-layer attributes (for example: allow only HTTP GET requests to specific API paths).

For example, a Cilium L7 policy can restrict frontend services to only issue GET requests to the backend API:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


This prevents the frontend from making POST or DELETE requests, limiting the attack surface.

### Integrating RBAC with Network Policy management

Role-based access control (RBAC) plays a crucial role in ensuring that only authorized users or teams can create, modify, or delete network policies. Without proper access controls, a misconfigured policy could either expose workloads to unauthorized access or unintentionally block critical application traffic.

By leveraging Kubernetes RBAC in conjunction with network policies, organizations can enforce separation of duties between platform administrators, security teams, and application developers. A typical approach is:

- Platform or security teams define baseline security policies that enforce compliance and restrict external access.
- Application teams are granted limited permissions to create or update network policies only for their respective namespaces.

For example, the following RBAC policy allows developers to create and modify network policies but only within their assigned namespace:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
name: network-policy-editor
namespace: team-a
rules:
- apiGroups: ["networking.k8s.io"]
resources: ["networkpolicies"]
verbs: ["get", "list", "create", "update", "delete"]
```


This role can then be bound to a specific team using a RoleBinding:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
name: team-a-network-policy-binding
namespace: team-a
subjects:
- kind: User
name: developer@example.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: network-policy-editor
apiGroup: rbac.authorization.k8s.io
```


By restricting network policy modifications to designated teams and namespaces, organizations can prevent accidental misconfigurations or unauthorized changes while still allowing flexibility for developers to implement application-specific security policies.

This approach reinforces the principle of least privilege while ensuring that network segmentation strategies remain consistent, secure, and aligned with organizational policies.

## Legacy and third-party solutions

### Azure Network Policy Manager (NPM)

Azure Network Policy Manager (NPM) is a legacy solution for enforcing Kubernetes network policies on AKS. As we continue to evolve our networking stack, we intend to deprecate NPM soon.

We strongly recommend all customers transition to Cilium Network Policy, which provides better performance, scalability, and enhanced security through eBPF-based enforcement. Cilium is the future of network policy in AKS and offers a more flexible and feature-rich alternative to NPM.

### NetworkPolicy support for Windows nodes

AKS doesn't natively support Kubernetes NetworkPolicy for Windows nodes out of the box. To enable network policies for Windows workloads, you can use Calico for Windows nodes, which is integrated into AKS to simplify deployment. You can enable it using the `--network-policy calico`

flag when creating a cluster.

Microsoft doesn't maintain the Calico images used in this integration. Our support is limited to ensuring Calico is properly integrated with AKS and functions as expected within the platform. Any issues related to Calico upstream bugs, feature requests, or troubleshooting beyond AKS integration should be directed to the Calico open-source community or Tigera, the maintainers of Calico.

### Calico open source – Third-party solution

Calico open source is a widely used third-party solution for enforcing Kubernetes network policies. It supports both Linux and Windows nodes and provides advanced networking and security capabilities, including network policy enforcement, workload identity, and encryption.

While Calico is integrated with AKS for Windows network policies (`--network-policy calico`

), it remains an open-source project maintained by Tigera. Microsoft doesn't maintain Calico images and provides limited support focused on ensuring proper integration with AKS. For advanced troubleshooting, feature requests, or issues beyond AKS integration, we recommend reaching out to the Calico open-source community or Tigera.

For Linux nodes, we strongly recommend using Cilium for network policy enforcement. For Windows nodes, we recommend using Calico.

## Conclusion

Network policies are a fundamental part of Kubernetes security, enabling organizations to control traffic flow, enforce workload isolation, and reduce the attack surface. As cloud-native environments evolve, relying solely on basic Layer 3/4 policies is no longer sufficient. Advanced solutions, such as Layer 7 filtering and FQDN-based policies, provide the granular security and flexibility needed to protect modern applications.

By following best practices including zero-trust model, microsegmentation, and adopting scalable solutions like Azure managed Cilium teams can enhance security while maintaining operational efficiency. As Kubernetes networking continues to evolve, adopting modern, observability-driven approaches will be key to securing workloads effectively.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-vnet-integration -->

# Create an Azure Kubernetes Service cluster with API Server VNet Integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the VNet where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel. The API server is available behind an internal load balancer VIP in the delegated subnet, which the nodes are configured to utilize. By using API Server VNet Integration, you can ensure network traffic between your API server and your node pools remains on the private network only.

## API server connectivity

The control plane or API server is in an AKS-managed Azure subscription. Your cluster or node pool is in your Azure subscription. The server and the virtual machines that make up the cluster nodes can communicate with each other through the API server VIP and pod IPs that are projected into the delegated subnet.

API Server VNet Integration is supported for public or private clusters. You can add or remove public access after cluster provisioning. Unlike non-VNet integrated clusters, the agent nodes always communicate directly with the private IP address of the API server internal load balancer (ILB) IP without using DNS. All node to API server traffic is kept on private networking, and no tunnel is required for API server to node connectivity. Out-of-cluster clients needing to communicate with the API server can do so normally if public network access is enabled. If public network access is disabled, you should follow the same private DNS setup methodology as standard [private clusters](private-clusters).

## Prerequisites

- You must have Azure CLI version 2.73.0 or later installed. You can check your version using the
`az --version`

command.

## Limitations

- API Server VNet Integration does not support
[Virtual Network Encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview). Clusters deployed on**v3 or earlier AKS node SKUs**(which do not support VNet Encryption) are allowed but traffic will not be encrypted. Clusters deployed on**v4 or later AKS node SKUs**(which support VNet Encryption) are blocked because encrypted VNets are incompatible with API Server VNet Integration. See[AKS supported VM SKUs](quotas-skus-regions#supported-vm-sizes)for details.

## Availability

- API Server VNet Integration is available in all GA public cloud regions except eastus2 and qatarcentral. We are continually working on enabling this feature in these regions and will update this page when these regions become available.

## Create an AKS cluster with API Server VNet Integration using managed VNet

You can configure your AKS clusters with API Server VNet Integration in managed VNet or bring-your-own VNet mode. You can create them as public clusters (with API server access available via a public IP) or private clusters (where the API server is only accessible via private VNet connectivity). You can also toggle between a public and private state without redeploying your cluster.

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --location westus2 --name <resource-group>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


## Create a private AKS cluster with API Server VNet Integration using bring-your-own VNet

When using bring-your-own VNet, you must create and delegate an API server subnet to `Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same virtual network. The minimum supported API server subnet size is a */28*.

The cluster identity needs permissions to both the API server subnet and the node subnet. Lack of permissions at the API server subnet can cause a provisioning failure.

Warning

An AKS cluster reserves at least 9 IPs in the subnet address space. Running out of IP addresses may prevent API server scaling and cause an API server outage.

### Create a resource group

- Create a resource group using the
command.`az group create`


```
az group create --location <location> --name <resource-group>
```


### Create a virtual network

Create a virtual network using the

command.`az network vnet create`

`az network vnet create --name <vnet-name> \ --resource-group <resource-group> \ --location <location> \ --address-prefixes 172.19.0.0/16`

Create an API server subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <apiserver-subnet-name> \ --delegations Microsoft.ContainerService/managedClusters \ --address-prefixes 172.19.0.0/28`

Create a cluster subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <cluster-subnet-name> \ --address-prefixes 172.19.1.0/24`


### Create a managed identity and give it permissions on the virtual network

Create a managed identity using the

command.`az identity create`

`az identity create --resource-group <resource-group> --name <managed-identity-name> --location <location>`

Assign the Network Contributor role to the API server subnet using the

command.`az role assignment create`

`az role assignment create --scope <apiserver-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`

Assign the Network Contributor role to the cluster subnet using the

command.`az role assignment create`

`az role assignment create --scope <cluster-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


## Convert an existing AKS cluster to API Server VNet Integration

Warning

**API Server VNet Integration is a one-way, capacity-sensitive feature.**

**Manual restart required.**

After enabling API Server VNet Integration using`az aks update --enable-apiserver-vnet-integration`

, due to control plane resource transition, you must immediately restart the cluster for the change to take effect. This restart is not automated. Delaying the restart increases the risk of capacity becoming unavailable, which can prevent the API server from starting. The cluster restart also ensures that all nodes reliably reconnect to the new API server endpoint.**Capacity is validated, but not reserved.**

AKS validates regional capacity when you enable the feature on an existing cluster, but this validation does not reserve capacity. If the restart is delayed and capacity becomes unavailable in the meantime, the cluster may fail to start after a stop or restart. Clusters that enabled this feature before general availability (GA), or that have not yet restarted since enablement, will not undergo capacity validation.**Feature cannot be disabled.**

Once enabled, the feature is permanent. You cannot disable API Server VNet Integration.

This upgrade performs a node-image version upgrade on all node pools and restarts all workloads while they undergo a rolling image upgrade.

Warning

Converting a cluster to API Server VNet Integration results in a change of the API Server IP address, though the hostname remains the same. If the IP address of the API server has been configured in any firewalls or network security group rules, those rules may need to be updated.

Update your cluster to API Server VNet Integration using the

command with the`az aks update`

`--enable-apiserver-vnet-integration`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-apiserver-vnet-integration \ --apiserver-subnet-id <apiserver-subnet-resource-id>`


## Enable or disable private cluster mode on an existing cluster with API Server VNet Integration

AKS clusters configured with API Server VNet Integration can have public network access/private cluster mode enabled or disabled without redeploying the cluster. The API server hostname doesn't change, but public DNS entries are modified or removed if necessary.

Note

`--disable-private-cluster`

is currently in preview. For more information, see [Reference and support levels](/en-us/cli/azure/reference-types-and-status).

### Enable private cluster mode

Enable private cluster mode using the

command with the`az aks update`

`--enable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-private-cluster`


### Disable private cluster mode

Disable private cluster mode using the

command with the`az aks update`

`--disable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --disable-private-cluster`


## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## Expose the API server through Private Link

You can expose the API server endpoint of a private cluster with API Server VNet Integration using Azure Private Link. The following steps show how to create a Private Link Service (PLS) in the cluster VNet and connect to it from another VNet or subscription using a Private Endpoint.

### Create an API Server VNet Integration Private cluster

Create a private AKS cluster with API Server VNet Integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --enable-private-cluster \ --enable-apiserver-vnet-integration`


For more guidance on how to set up Private Link with API Server VNet Integration, see [Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).

## NSG security rules

All traffic within the VNet is allowed by default. But if you have added NSG rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communications between the Azure Load Balancer and the API Server Subnet CIDR. |

## Next steps

- For associated best practices, see
[Best practices for network connectivity and security in AKS](operator-best-practices-network). - For guidance on how to set up private link with API Server VNet Integration, see
[Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-extensions-az-cli -->

# Deploy and manage cluster extensions by using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can create extension instances in an AKS cluster, setting required and optional parameters including options related to updates and configurations. You can also view, list, update, and delete extension instances.

Before you begin, read about [cluster extensions](cluster-extensions).

Note

The examples provided in this article are not complete, and are only meant to showcase functionality. For a comprehensive list of commands and their parameters, see the [az k8s-extension CLI reference](/en-us/cli/azure/k8s-extension).

## Prerequisites

An Azure subscription. If you don't have an Azure subscription, you can create a

[free account](https://azure.microsoft.com/free).The

`Microsoft.ContainerService`

and`Microsoft.KubernetesConfiguration`

resource providers must be registered on your subscription. To register these providers, run the following command:`az provider register --namespace Microsoft.ContainerService --wait az provider register --namespace Microsoft.KubernetesConfiguration --wait`

An AKS cluster. This cluster must have been created with a managed identity, as cluster extensions won't work with service principal-based clusters. For new clusters created with

`az aks create`

, managed identity is configured by default. For existing service principal-based clusters, switch to manage identity by running`az aks update`

with the`--enable-managed-identity`

flag. For more information, see[Use managed identity](use-managed-identity).[Azure CLI](/en-us/cli/azure/install-azure-cli)version >= 2.16.0 installed. We recommend using the latest version.The latest version of the

`k8s-extension`

Azure CLI extensions. Install the extension by running the following command:`az extension add --name k8s-extension`

If the extension is already installed, make sure you're running the latest version by using the following command:

`az extension update --name k8s-extension`


## Create extension instance

Create a new extension instance with `k8s-extension create`

, passing in values for the mandatory parameters. This example command creates an Azure Machine Learning extension instance on your AKS cluster:

```
az k8s-extension create --name azureml --extension-type Microsoft.AzureML.Kubernetes --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters --configuration-settings enableInference=True allowInsecureConnections=True inferenceRouterServiceType=LoadBalancer
```


This example command creates a sample Kubernetes application (published on Marketplace) on your AKS cluster:

```
az k8s-extension create --name voteapp --extension-type Contoso.AzureVoteKubernetesAppTest --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters --plan-name testPlanID --plan-product testOfferID --plan-publisher testPublisherID --configuration-settings title=VoteAnimal value1=Cats value2=Dogs
```


Note

The Cluster Extensions service is unable to retain sensitive information for more than 48 hours. If the cluster extension agents don't have network connectivity for more than 48 hours and can't determine whether to create an extension on the cluster, then the extension transitions to `Failed`

state. Once in `Failed`

state, you'll need to run `k8s-extension create`

again to create a fresh extension instance.

### Required parameters

| Parameter name | Description |
|---|---|
`--name` |
Name of the extension instance |
`--extension-type` |
The type of extension you want to install on the cluster. For example: `Microsoft.AzureML.Kubernetes` |
`--cluster-name` |
Name of the AKS cluster on which the extension instance has to be created |
`--resource-group` |
The resource group containing the AKS cluster |
`--cluster-type` |
The cluster type on which the extension instance has to be created. Specify `managedClusters` as it maps to AKS clusters |

### Optional parameters

| Parameter name | Description |
|---|---|
`--auto-upgrade-minor-version` |
Boolean property that specifies if the extension minor version will be upgraded automatically or not. Default: `true` . If this parameter is set to true, you can't set `version` parameter, as the version will be dynamically updated. If set to `false` , extension won't be auto-upgraded even for patch versions. |
`--version` |
Version of the extension to be installed (specific version to pin the extension instance to). Must not be supplied if auto-upgrade-minor-version is set to `true` . |
`--configuration-settings` |
Settings that can be passed into the extension to control its functionality. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-settings-file` can't be used in the same command. |
`--configuration-settings-file` |
Path to the JSON file having key value pairs to be used for passing in configuration settings to the extension. If this parameter is used in the command, then `--configuration-settings` can't be used in the same command. |
`--configuration-protected-settings` |
These settings are not retrievable using `GET` API calls or `az k8s-extension show` commands, and are thus used to pass in sensitive settings. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-protected-settings-file` can't be used in the same command. |
`--configuration-protected-settings-file` |
Path to the JSON file having key value pairs to be used for passing in sensitive settings to the extension. If this parameter is used in the command, then `--configuration-protected-settings` can't be used in the same command. |
`--scope` |
Scope of installation for the extension - `cluster` or `namespace` |
`--release-namespace` |
This parameter indicates the namespace within which the release is to be created. This parameter is only relevant if `scope` parameter is set to `cluster` . |
`--release-train` |
Extension authors can publish versions in different release trains such as `Stable` , `Preview` , etc. If this parameter isn't set explicitly, `Stable` is used as default. This parameter can't be used when `--auto-upgrade-minor-version` parameter is set to `false` . |
`--target-namespace` |
This parameter indicates the namespace within which the release will be created. Permission of the system account created for this extension instance will be restricted to this namespace. This parameter is only relevant if the `scope` parameter is set to `namespace` . |
`--plan-name` |
Plan ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |
`--plan-product` |
Product ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. An example of this is the name of the ISV offering used. |
`--plan-publisher` |
Publisher ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |

## Show details of an extension instance

To view details of a currently installed extension instance, use `k8s-extension show`

, passing in values for the mandatory parameters.

```
az k8s-extension show --name azureml --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


## List all extensions installed on the cluster

To list all extensions installed on a cluster, use `k8s-extension list`

, passing in values for the mandatory parameters.

```
az k8s-extension list --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


## Update extension instance

Note

Refer to documentation for the specific extension type to understand the specific settings in `--configuration-settings`

and `--configuration-protected-settings`

that are able to be updated. For `--configuration-protected-settings`

, all settings are expected to be provided, even if only one setting is being updated. If any of these settings are omitted, those settings will be considered obsolete and deleted.

To update an existing extension instance, use `k8s-extension update`

, passing in values for the mandatory parameters. The following command updates the auto-upgrade setting for an Azure Machine Learning extension instance:

```
az k8s-extension update --name azureml --extension-type Microsoft.AzureML.Kubernetes --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


### Required parameters for update

| Parameter name | Description |
|---|---|
`--name` |
Name of the extension instance |
`--extension-type` |
The type of extension you want to install on the cluster. For example: Microsoft.AzureML.Kubernetes |
`--cluster-name` |
Name of the AKS cluster on which the extension instance has to be created |
`--resource-group` |
The resource group containing the AKS cluster |
`--cluster-type` |
The cluster type on which the extension instance has to be created. Specify `managedClusters` as it maps to AKS clusters |

If updating a Kubernetes application procured through Marketplace, the following parameters are also required:

| Parameter name | Description |
|---|---|
`--plan-name` |
Plan ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |
`--plan-product` |
Product ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. An example of this is the name of the ISV offering used. |
`--plan-publisher` |
Publisher ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |

### Optional parameters for update

| Parameter name | Description |
|---|---|
`--auto-upgrade-minor-version` |
Boolean property that specifies if the extension minor version will be upgraded automatically or not. Default: `true` . If this parameter is set to true, you cannot set `version` parameter, as the version will be dynamically updated. If set to `false` , extension won't be auto-upgraded even for patch versions. |
`--version` |
Version of the extension to be installed (specific version to pin the extension instance to). Must not be supplied if auto-upgrade-minor-version is set to `true` . |
`--configuration-settings` |
Settings that can be passed into the extension to control its functionality. Only the settings that require an update need to be provided. The provided settings would be replaced with the provided values. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-settings-file` can't be used in the same command. |
`--configuration-settings-file` |
Path to the JSON file having key value pairs to be used for passing in configuration settings to the extension. If this parameter is used in the command, then `--configuration-settings` can't be used in the same command. |
`--configuration-protected-settings` |
These settings are not retrievable using `GET` API calls or `az k8s-extension show` commands, and are thus used to pass in sensitive settings. When you update a setting, all settings are expected to be specified. If some settings are omitted, those settings would be considered obsolete and deleted. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-protected-settings-file` can't be used in the same command. |
`--configuration-protected-settings-file` |
Path to the JSON file having key value pairs to be used for passing in sensitive settings to the extension. If this parameter is used in the command, then `--configuration-protected-settings` can't be used in the same command. |
`--scope` |
Scope of installation for the extension - `cluster` or `namespace` |
`--release-train` |
Extension authors can publish versions in different release trains such as `Stable` , `Preview` , etc. If this parameter isn't set explicitly, `Stable` is used as default. This parameter can't be used when `autoUpgradeMinorVersion` parameter is set to `false` . |

## Delete extension instance

To delete an extension instance on a cluster, use `k8s-extension-delete`

, passing in values for the mandatory parameters.

```
az k8s-extension delete --name azureml --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


Note

The Azure resource representing this extension gets deleted immediately. The Helm release on the cluster associated with this extension is only deleted when the agents running on the Kubernetes cluster have network connectivity and can reach out to Azure services again to fetch the desired state.

## Next steps

- View the list of
[currently available cluster extensions](cluster-extensions#currently-available-extensions). - Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/nat-gateway -->

# Create a managed or user-assigned NAT gateway for your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

While you can route egress traffic through an Azure Load Balancer, there are limitations on the number of outbound flows of traffic you can have. Azure NAT Gateway allows up to 64,512 outbound UDP and TCP traffic flows per IP address with a maximum of 16 IP addresses.

This article shows you how to create an Azure Kubernetes Service (AKS) cluster with a managed NAT gateway and a user-assigned NAT gateway for egress traffic. It also shows you how to disable OutboundNAT on Windows.

## Before you begin

- Make sure you're using the latest version of
[Azure CLI](/en-us/cli/azure/install-azure-cli). - Make sure you're using Kubernetes version 1.20.x or above.
- Managed NAT gateway is incompatible with custom virtual networks.

Important

In non-private clusters, API server cluster traffic is routed and processed through the clusters outbound type. To prevent API server traffic from being processed as public traffic, consider using a [private cluster](private-clusters), or check out the [API Server VNet Integration](api-server-vnet-integration) feature.

## Create an AKS cluster with a managed NAT gateway

- Create an AKS cluster with a new managed NAT gateway using the
command with the`az aks create`

`--outbound-type managedNATGateway`

,`--nat-gateway-managed-outbound-ip-count`

, and`--nat-gateway-idle-timeout`

parameters. If you want the NAT gateway to operate out of a specific availability zone, specify the zone using`--zones`

. - If no zone is specified when creating a managed NAT gateway, then NAT gateway is deployed to "no zone" by default. When NAT gateway is placed in
**no zone**, Azure places the resource in a zone for you. For more information on non-zonal deployment model, see[non-zonal NAT gateway](/en-us/azure/nat-gateway/nat-availability-zones#non-zonal). - A managed NAT gateway resource can't be used across multiple availability zones.

The following commands first create the required resource group, then the AKS cluster with a managed NAT gateway.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export MY_RG="myResourceGroup$RANDOM_SUFFIX"
export MY_AKS="myNatCluster$RANDOM_SUFFIX"
az group create --name $MY_RG --location "eastus2"
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


```
az aks create \
--resource-group $MY_RG \
--name $MY_AKS \
--node-count 3 \
--outbound-type managedNATGateway \
--nat-gateway-managed-outbound-ip-count 2 \
--nat-gateway-idle-timeout 4 \
--generate-ssh-keys
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


- Update the outbound IP address or idle timeout using the
command with the`az aks update`

`--nat-gateway-managed-outbound-ip-count`

or`--nat-gateway-idle-timeout`

parameter.

The following example updates the NAT gateway managed outbound IP count for the AKS cluster to 5.

```
az aks update \
--resource-group $MY_RG \
--name $MY_AKS \
--nat-gateway-managed-outbound-ip-count 5
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


## Create an AKS cluster with a user-assigned NAT gateway

This configuration requires bring-your-own networking (via [Kubenet](configure-kubenet) or [Azure CNI](configure-azure-cni)) and that the NAT gateway is preconfigured on the subnet. The following commands create the required resources for this scenario.

Create a resource group using the

command.`az group create`

`export RANDOM_SUFFIX=$(openssl rand -hex 3) export MY_RG="myResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RG --location southcentralus`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx", "location": "southcentralus", "managedBy": null, "name": "myResourceGroupxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`

Create a managed identity for network permissions and store the ID to

`$IDENTITY_ID`

for later use.`export IDENTITY_NAME="myNatClusterId$RANDOM_SUFFIX" export IDENTITY_ID=$(az identity create \ --resource-group $MY_RG \ --name $IDENTITY_NAME \ --location southcentralus \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myNatClusterIdxxx`

Create a public IP for the NAT gateway using the

command.`az network public-ip create`

`export PIP_NAME="myNatGatewayPip$RANDOM_SUFFIX" az network public-ip create \ --resource-group $MY_RG \ --name $PIP_NAME \ --location southcentralus \ --sku standard`

Results:

`{ "publicIp": { "ddosSettings": null, "dnsSettings": null, "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx", "ipAddress": null, "ipTags": [], "location": "southcentralus", "name": "myNatGatewayPipxxx", ... "provisioningState": "Succeeded", ... "sku": { "name": "Standard", "tier": "Regional" }, "type": "Microsoft.Network/publicIPAddresses", ... } }`

Create the NAT gateway using the

command.`az network nat gateway create`

`export NATGATEWAY_NAME="myNatGateway$RANDOM_SUFFIX" az network nat gateway create \ --resource-group $MY_RG \ --name $NATGATEWAY_NAME \ --location southcentralus \ --public-ip-addresses $PIP_NAME`

Results:

`{ "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/natGateways/myNatGatewayxxx", "location": "southcentralus", "name": "myNatGatewayxxx", "provisioningState": "Succeeded", "publicIpAddresses": [ { "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx" } ], ... "type": "Microsoft.Network/natGateways" }`

Important

A single NAT gateway resource can't be used across multiple availability zones. To ensure zone-resiliency, it is recommended to deploy a NAT gateway resource to each availability zone and assign to subnets containing AKS clusters in each zone. For more information on this deployment model, see

[NAT gateway for each zone](/en-us/azure/nat-gateway/nat-availability-zones#zonal-nat-gateway-resource-for-each-zone-in-a-region-to-create-zone-resiliency). If no zone is configured for NAT gateway, the default zone placement is "no zone", in which Azure places NAT gateway into a zone for you.Create a virtual network using the

command.`az network vnet create`

`export VNET_NAME="myVnet$RANDOM_SUFFIX" az network vnet create \ --resource-group $MY_RG \ --name $VNET_NAME \ --location southcentralus \ --address-prefixes 172.16.0.0/20`

Results:

`{ "newVNet": { "addressSpace": { "addressPrefixes": [ "172.16.0.0/20" ] }, ... "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx", "location": "southcentralus", "name": "myVnetxxx", "provisioningState": "Succeeded", ... "type": "Microsoft.Network/virtualNetworks", ... } }`

Create a subnet in the virtual network using the NAT gateway and store the ID to

`$SUBNET_ID`

for later use.`export SUBNET_NAME="myNatCluster$RANDOM_SUFFIX" export SUBNET_ID=$(az network vnet subnet create \ --resource-group $MY_RG \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --address-prefixes 172.16.0.0/22 \ --nat-gateway $NATGATEWAY_NAME \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx/subnets/myNatClusterxxx`

Create an AKS cluster using the subnet with the NAT gateway and the managed identity using the

command.`az aks create`

`export AKS_NAME="myNatCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RG \ --name $AKS_NAME \ --location southcentralus \ --network-plugin azure \ --vnet-subnet-id $SUBNET_ID \ --outbound-type userAssignedNATGateway \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys`

Results:

`{ "aadProfile": null, "agentPoolProfiles": [ { ... "name": "nodepool1", ... "provisioningState": "Succeeded", ... } ], "dnsPrefix": "myNatClusterxxx-dns-xxx", "fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx", "name": "myNatClusterxxx", ... "resourceGroup": "myResourceGroupxxx", ... "provisioningState": "Succeeded", ... "type": "Microsoft.ContainerService/ManagedClusters" }`


## Disable OutboundNAT for Windows

Windows OutboundNAT can cause certain connection and communication issues with your AKS pods. An example issue is node port reuse. In this example, Windows OutboundNAT uses ports to translate your pod IP to your Windows node host IP, which can cause an unstable connection to the external service due to a port exhaustion issue.

Windows enables OutboundNAT by default. You can now manually disable OutboundNAT when creating new Windows agent pools.

### Prerequisites

- Existing AKS cluster with v1.26 or above. If you're using Kubernetes version 1.25 or older, you need to
[update your deployment configuration](tutorial-kubernetes-upgrade-cluster).

### Limitations

- You can't set cluster outbound type to LoadBalancer. You can set it to NAT Gateway or UDR:
[NAT Gateway](nat-gateway): NAT Gateway can automatically handle NAT connection and is more powerful than Standard Load Balancer. You might incur extra charges with this option.[UDR (UserDefinedRouting)](limit-egress-traffic): You must keep port limitations in mind when configuring routing rules.- If you need to switch from a load balancer to NAT Gateway, you can either add a NAT gateway into the VNet or run
to update the outbound type.`az aks upgrade`


Note

UserDefinedRouting has the following limitations:

- SNAT by Load Balancer (must use the default OutboundNAT) has "64 ports on the host IP".
- SNAT by Azure Firewall (disable OutboundNAT) has 2496 ports per public IP.
- SNAT by NAT Gateway (disable OutboundNAT) has 64512 ports per public IP.
- If the Azure Firewall port range isn't enough for your application, you need to use NAT Gateway.
- Azure Firewall doesn't SNAT with Network rules when the destination IP address is in a private IP address range per
[IANA RFC 1918 or shared address space per IANA RFC 6598](/en-us/azure/firewall/snat-private-range).

### Manually disable OutboundNAT for Windows

Manually disable OutboundNAT for Windows when creating new Windows agent pools using the

command with the`az aks nodepool add`

`--disable-windows-outbound-nat`

flag.Note

You can use an existing AKS cluster, but you might need to update the outbound type and add a node pool to enable

`--disable-windows-outbound-nat`

.The following command adds a Windows node pool to an existing AKS cluster, disabling OutboundNAT.

`export WIN_NODEPOOL_NAME="win$(head -c 1 /dev/urandom | xxd -p)" az aks nodepool add \ --resource-group $MY_RG \ --cluster-name $MY_AKS \ --name $WIN_NODEPOOL_NAME \ --node-count 3 \ --os-type Windows \ --disable-windows-outbound-nat`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx/agentPools/mynpxxx", "name": "mynpxxx", "osType": "Windows", "provisioningState": "Succeeded", "resourceGroup": "myResourceGroupxxx", "type": "Microsoft.ContainerService/managedClusters/agentPools" }`


## Next steps

For more information on Azure NAT Gateway, see [Azure NAT Gateway](/en-us/azure/virtual-network/nat-gateway/nat-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-legacy-cni -->

# AKS Legacy Container Networking Interfaces (CNI)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

In Azure Kubernetes Service (AKS), while [Azure CNI Overlay](concepts-network-azure-cni-overlay) and [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) are recommended for most scenarios, legacy networking models such as Azure CNI Node Subnet and kubenet are still available and supported. These legacy models offer different approaches to pod IP address management and networking, each with its own set of capabilities and considerations. This article provides an overview of these legacy networking options, detailing their prerequisites, deployment parameters, and key characteristics to help you understand their roles and how they can be used effectively within your AKS clusters.

## Prerequisites

The following prerequisites are required for Azure CNI Node Subnet:

The virtual network for the AKS cluster must allow outbound internet connectivity.

AKS clusters can't use

`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range.The cluster identity used by the AKS cluster must have at least

[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within the virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`

`Microsoft.Authorization/roleAssignments/write`


The subnet assigned to the AKS node pool can't be a

[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview).

- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, make sure the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Network security groups](concepts-network#network-security-groups).

## Azure CNI Node Subnet

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.

With Azure CNI Node Subnet, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with Azure CNI.

### Deployment parameters

When you create an AKS cluster, the following parameters are configurable for Azure CNI networking:

**Virtual network**: The virtual network into which you want to deploy the Kubernetes cluster. You can create a new virtual network or use an existing one. If you want to use an existing virtual network, make sure it's in the same location and Azure subscription as your Kubernetes cluster. For information about the limits and quotas for an Azure virtual network, see [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-resource-manager-virtual-networking-limits).

**Subnet**: The subnet within the virtual network where you want to deploy the cluster. You can add new subnets into the virtual network during the cluster creation process. For hybrid connectivity, the address range shouldn't overlap with any other virtual networks in your environment.

**Azure Network Plugin**: When Azure network plugin is used, the internal LoadBalancer service with "externalTrafficPolicy=Local" can't be accessed from VMs with an IP in clusterCIDR that doesn't belong to AKS cluster.

**Kubernetes service address range**: This parameter is the set of virtual IPs that Kubernetes assigns to internal [services](concepts-network-services) in your cluster. This range can't be updated after you create your cluster. You can use any private address range that satisfies the following requirements:

- Must not be within the virtual network IP address range of your cluster.
- Must not overlap with any other virtual networks with which the cluster virtual network peers.
- Must not overlap with any on-premises IPs.
- Must not be within the ranges
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

.

While it's possible to specify a service address range within the same virtual network as your cluster, we don't recommend it. Overlapping IP ranges can result in unpredictable behavior. For more information, see the [FAQ](#azure-cni-pod-subnet-frequently-asked-questions). For more information on Kubernetes services, see [Services](concepts-network-services) in the Kubernetes documentation.

**Kubernetes DNS service IP address**: The IP address for the cluster's DNS service. This address must be within the *Kubernetes service address range*. Don't use the first IP address in your address range. The first address in your subnet range is used for the *kubernetes.default.svc.cluster.local* address.

**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*8*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

## Virtual network peering and ExpressRoute connections

You can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction) with *Azure CNI* to provide on-premises connectivity. Make sure you plan your IP addresses carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside of this address range, such as *172.16.0.0/16*.

For more information, see [Compare network models and their support scopes](concepts-network-cni-overview).

## Azure CNI Pod Subnet frequently asked questions

**Can I deploy VMs in my cluster subnet?**Yes for Azure CNI Node Subnet, the VMs can be deployed in the same subnet as the AKS cluster.

**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. But for

[Azure CNI dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I configure per-pod network policies?**Yes, Kubernetes network policy is available in AKS. To get started, see

[Secure traffic between pods by using network policies in AKS](use-network-policies).**Is the maximum number of pods deployable to a node configurable?**With

[Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.**Can I deploy VMs in my cluster subnet?**Yes. But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), the VMs cannot be deployed in pod's subnet.**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod.

But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk. Yes, when you deploy a cluster with the Azure CLI or a Resource Manager template. See

[Maximum pods per node](concepts-network-ip-address-planning#maximum-pods-per-node).**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-application-az-cli -->

# Deploy an Azure Kubernetes application programmatically by using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To deploy a Kubernetes application programmatically through Azure CLI, you select the Kubernetes application and settings, accept legal terms and conditions, and finally deploy the application through CLI commands.

## Select Kubernetes application

First, you need to select the Kubernetes application that you want to deploy in the Azure portal. You'll also need to copy some of the details for later use.

In the Azure portal, go to the

[Marketplace page](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/home/fromContext/AKS).Select your Kubernetes application.

Select the required plan.

Select the

**Create**button.Fill out all the application (extension) details.

In the

**Review + Create**tab, select**Download a template for automation**. If all the validations are passed, you'll see the ARM template in the editor.Examine the ARM template:

In the variables section, copy the

`plan-name,`

`plan-publisher,`

`plan-offerID,`

and`clusterExtensionTypeName`

values for later use.`"variables": { "plan-name": "DONOTMODIFY", "plan-publisher": "DONOTMODIFY", "plan-offerID": "DONOTMODIFY", "releaseTrain": "DONOTMODIFY", "clusterExtensionTypeName": "DONOTMODIFY" },`

In the resource

`Microsoft.KubernetesConfiguration/extensions`

section, copy the`configurationSettings`

section for later use.

`{ "type": "Microsoft.KubernetesConfiguration/extensions", "apiVersion": "2022-11-01", "name": "[parameters('extensionResourceName')]", "properties": { "extensionType": "[variables('clusterExtensionTypeName')]", "autoUpgradeMinorVersion": true, "releaseTrain": "[variables('releaseTrain')]", "configurationSettings": { "title": "[parameters('app-title')]", "value1": "[parameters('app-value1')]", "value2": "[parameters('app-value2')]" },`

Note

If there are no configuration settings in the ARM template, refer to the application-related documentation in Azure Marketplace or on the partner's website.


## Accept terms and agreements

Before you can deploy a Kubernetes application, you need to accept its terms and agreements. To do so, run the following command, using the values you copied for `plan-publisher`

, `plan-offerID`

, and `plan-name`

.

```
az vm image terms accept --offer <plan-offerID> --plan <plan-name> --publisher <plan-publisher>
```


Note

Although this command is for VMs, it also works for containers. For more information, see the [ az cm image terms reference](/en-us/cli/azure/vm/image/terms).

## Deploy the application

To deploy the application (extension) through Azure CLI, follow the steps outlined in [Deploy and manage cluster extensions by using Azure CLI](deploy-extensions-az-cli).

## Next steps

- Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace). - Learn about
[cluster extensions](cluster-extensions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/scale-node-pools -->

# Scale node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your application workload demands change, you might need to scale the number of nodes in a node pool in Azure Kubernetes Service (AKS). In this article, you learn how to manually and automatically scale node pools in AKS.

## Prerequisites for AKS node pool scaling

- An existing AKS cluster with at least one node pool. If you need to create one, see
[Create an AKS cluster with node pools](create-node-pools). - You need the Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Scale a node pool manually

Scale the number of nodes in a node pool using the [

`az aks nodepool scale`

][az-aks-nodepool-scale] command. The`--node-count`

flag specifies the desired number of nodes in the node pool. In this example, the node pool is scaled to five nodes.`az aks nodepool scale \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --node-count 5 \ --no-wait`

Check the status of your node pools using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Scaling*state with a new count of five nodes:`[ { ... "count": 5, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Scaling", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes for the scale operation to complete. After the scale operation is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Scale a node pool automatically with the cluster autoscaler

You can use the [cluster autoscaler](cluster-autoscaler-overview) with multiple node pools, and you can enable it on individual node pools and pass unique autoscaling rules to them.

Enable the cluster autoscaler on an existing node pool using the [

`az aks nodepool update`

][az-aks-nodepool-update] command with the`--update-cluster-autoscaler`

flag. The`--min-count`

and`--max-count`

flags specify the minimum and maximum number of nodes in the node pool. In this example, the cluster autoscaler is enabled with a minimum count of one node and a maximum count of five nodes:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

If you want to disable the cluster autoscaler on a node pool, use the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `--disable-cluster-autoscaler`

flag instead of `--update-cluster-autoscaler`

.

## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-fqdn-filtering-concepts -->

# Overview of FQDN filtering

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Containerized environments present unique security challenges. Traditional network security methods, often reliant on IP-based filtering, can become cumbersome and less effective as IP addresses frequently change. Additionally, understanding network traffic patterns and identifying potential threats can be complex.

FQDN filtering offers an efficient and user-friendly approach for managing network policies. By defining these policies based on domain names rather than IP addresses, organizations can significantly simplify the process of policy management. This approach eliminates the need for frequent updates that are typically required when IP addresses change, as a result reducing the administrative burden and minimizing the risk of configuration errors.

In a Kubernetes cluster, pod IP addresses can change often, which makes it challenging to secure the pods with security policies using IP addresses. FQDN filtering allows you to create pod level policies using domain names rather than IP addresses, which eliminates the need to update policies when an IP address changes.

Note

Azure CNI Powered by Cilium and Kubernetes version 1.29 or greater is required in order to use Container Network security features of Advanced Container Networking Services.

## Components of FQDN filtering

**Cilium Agent**: The Cilium Agent is a critical networking component that runs as a DaemonSet within Azure CNI clusters powered by Cilium. It handles networking, load balancing, and network policies for pods in the cluster. For pods with enforced FQDN policies, the Cilium Agent redirects packets to the ACNS Security Agent for DNS resolution and updates the network policy using the FQDN-IP mappings obtained from the ACNS Security Agent.

**ACNS Security Agent**: ACNS Security Agent runs as DaemonSet in Azure CNI powered by Cilium cluster with Advanced Container Networking services enabled. It handles DNS resolution for pods and on successful DNS resolution, it updates Cilium Agent with FQDN to IP mappings.

## How FQDN filtering works

When FQDN Filtering is enabled, DNS requests are first evaluated to determine if they should be allowed after which pods can only access specified domain names based on the network policy. The Cilium Agent marks DNS request packets originating from the pods, redirecting them to the ACNS Security Agent. This redirection occurs only for pods that are enforcing FQDN policies.

The ACNS Security Agent then decides whether to forward a DNS request to the DNS server based on the policy criteria. If permitted, the request is sent to the DNS server, and upon receiving the response, the ACNS Security Agent updates the Cilium Agent with FQDN mappings. This allows the Cilium Agent to update the network policy within the policy engine. The following image illustrates the high-level flow of FQDN Filtering.

## Key benefits

**Scalable security policy management**: Cluster and security admins don't have to update security policies each time an IP address changes making operations more efficient.

**Enhanced security compliance**: FQDN filtering supports a Zero Trust security model. Network traffic is restricted to trusted domains only mitigating risks from unauthorized access.

**Resilient Policy enforcement**: The ACNS Security Agent that is implemented with FQDN filtering ensures that DNS resolution continues seamlessly even if the Cilium agent goes down and policies continue to remain enforced. This implementation critically ensures that security and stability are maintained in dynamic and distributed environments.

## Considerations:

Container Network Security features require Azure CNI Powered by Cilium and Kubernetes version 1.29 and above.

Supported by

`CiliumClusterwideNetworkPolicy`

(CCNP): FQDN filtering can be applied cluster wide via`CiliumClusterwideNetworkPolicy`

.

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you cannot use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempts to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods may exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP(s), Kafka and gRPC) will be blocked.
- Alpine-based container images may encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

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


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[fqdn filtering policies](how-to-apply-fqdn-filtering-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler-overview -->

# Cluster autoscaling in Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in Azure Kubernetes Service (AKS), you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects unscheduled pods, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes that don't have any scheduled pods and scales down the number of nodes as needed.

This article helps you understand how the cluster autoscaler works in AKS. It also provides guidance, best practices, and considerations when configuring the cluster autoscaler for your AKS workloads. If you want to enable, disable, or update the cluster autoscaler for your AKS workloads, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

## About the cluster autoscaler

Clusters often need a way to scale automatically to adjust to changing application demands, such as between workdays and evenings or weekends. AKS clusters can scale in the following ways:

- The
**cluster autoscaler**periodically checks for pods that can't be scheduled on nodes because of resource constraints. The cluster then automatically increases the number of nodes. Manual scaling is disabled when you use the cluster autoscaler. For more information, see[How does scale up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work). - The
uses the Metrics Server in a Kubernetes cluster to monitor the resource demand of pods. If an application needs more resources, the number of pods is automatically increased to meet the demand.[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler) - The
automatically sets resource requests and limits on containers per workload based on past usage to ensure pods are scheduled onto nodes that have the required CPU and memory resources.[Vertical Pod Autoscaler](vertical-pod-autoscaler)


It's a common practice to enable cluster autoscaler for nodes and either the Vertical Pod Autoscaler or Horizontal Pod Autoscaler for pods. When you enable the cluster autoscaler, it applies the specified scaling rules when the node pool size is lower than the minimum node count, up to the maximum node count. The cluster autoscaler waits to take effect until a new node is needed in the node pool or until a node might be safely deleted from the current node pool. For more information, see [How does scale down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work)

## Best practices and considerations

- When implementing
**availability zones with the cluster autoscaler**, we recommend using a single node pool for each zone. You can set the`--balance-similar-node-groups`

parameter to`True`

to maintain a balanced distribution of nodes across zones for your workloads during scale up operations. When this approach isn't implemented, scale down operations can disrupt the balance of nodes across zones.

Note

The Cluster Autoscaler is not zone-aware, and zone allocation is handled by the underlying Virtual Machine Scale Sets. The above best practice becomes even more relevant when using zone-based [pod topology spread constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) on a single multi-zonal node pool, as restrictive constraints may leave pods in a pending state, especially in capacity-constrained regions or during zone-down scenarios.

For

**clusters with more than 400 nodes**, we recommend using Azure CNI or Azure CNI Overlay.To

**effectively run workloads concurrently on both Spot and On-demand node pools**, consider using. This approach allows you to scale out nodepools based on assigned priority. The following configuration illustrates this setup.*priority expanders*`apiVersion: v1 kind: ConfigMap metadata: name: cluster-autoscaler-priority-expander namespace: kube-system data: priorities: |- 10: - .*spotpool1.* - .*spotpool2.* 50: - .*ondemandpool1.*`

Exercise caution when

**assigning CPU/Memory requests on pods**. The cluster autoscaler scales up based on pending pods rather than CPU/Memory pressure on nodes.For

**clusters concurrently hosting both long-running workloads, like web apps, and short/bursty job workloads**, we recommend separating them into distinct node pools with[Affinity Rules](operator-best-practices-advanced-scheduler#node-affinity)/[expanders](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-are-expanders).Use

[PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)to help prevent unnecessary node drain or scale down operations. Specifying the annotation[cluster-autoscaler.kubernetes.io/safe-to-evict: "false"](https://kubernetes.io/docs/reference/labels-annotations-taints/#cluster-autoscaler-kubernetes-io-safe-to-evict)on the Pod spec will also prevent the pods from being evicted. Use this annotation with caution, as it may cause the Cluster Autoscaler encounter issues when draining a node with a running Pod that includes this annotation.In an autoscaler-enabled node pool, scale down nodes by removing workloads, instead of manually reducing the min/ max count of the node pool. This can be problematic if the node pool is already at maximum capacity or if there are active workloads running on the nodes, potentially causing unexpected behavior by the cluster autoscaler.

Nodes don't scale up if pods have a PriorityClass value below -10. Priority -10 is reserved for

[overprovisioning pods](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). For more information, see[Using the cluster autoscaler with Pod Priority and Preemption](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption).**Don't combine other node autoscaling mechanisms**, such as Virtual Machine Scale Set autoscalers, with the cluster autoscaler.The cluster autoscaler

**might be unable to scale down if pods can't move, such as in the following situations**:- A directly created pod not backed by a controller object, such as a Deployment or ReplicaSet.
- A pod disruption budget (PDB) that's too restrictive and doesn't allow the number of pods to fall below a certain threshold.
- A pod uses node selectors or anti-affinity that can't be honored if scheduled on a different node.
For more information, see
[What types of pods can prevent the cluster autoscaler from removing a node?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-types-of-pods-can-prevent-ca-from-removing-a-node).


Important

**Don't make changes to individual nodes within the autoscaled node pools**. All nodes in the same node group should have uniform capacity, labels, taints and system pods running on them.

- The cluster autoscaler isn't responsible for enforcing a "maximum node count" in a cluster node pool irrespective of pod scheduling considerations. If any non-cluster autoscaler actor sets the node pool count to a number beyond the cluster autoscaler's configured maximum, the cluster autoscaler doesn't automatically remove nodes. The cluster autoscaler scale down behaviors remain scoped to removing underutilized nodes. The sole purpose of the cluster autoscaler's max node count configuration is to enforce an upper limit for scale up operations. It doesn't have any effect on scale down considerations.

## Cluster autoscaler profile

The [cluster autoscaler profile](cluster-autoscaler#cluster-autoscaler-profile-settings) is a set of parameters that control the behavior of the cluster autoscaler. You can configure the cluster autoscaler profile when you create a cluster or update an existing cluster.

### Optimizing the cluster autoscaler profile

You should fine-tune the cluster autoscaler profile settings according to your specific workload scenarios while also considering tradeoffs between performance and cost. This section provides examples that demonstrate those tradeoffs.

It's important to note that the cluster autoscaler profile settings are cluster-wide and applied to all autoscale-enabled node pools. Any scaling actions that take place in one node pool can affect the autoscaling behavior of other node pools, which can lead to unexpected results. Make sure you apply consistent and synchronized profile configurations across all relevant node pools to ensure you get your desired results.

#### Example 1: Optimizing for performance

For clusters that handle substantial and bursty workloads with a primary focus on performance, we recommend increasing the `scan-interval`

and decreasing the `scale-down-utilization-threshold`

. These settings help batch multiple scaling operations into a single call, optimizing scaling time and the utilization of compute read/write quotas. It also helps mitigate the risk of swift scale down operations on underutilized nodes, enhancing the pod scheduling efficiency. Also increase `ok-total-unready-count`

and `max-total-unready-percentage`

.

For clusters with daemonset pods, we recommend setting `ignore-daemonsets-utilization`

to `true`

, which effectively ignores node utilization by daemonset pods and minimizes unnecessary scale down operations. See [profile for bursty workloads](cluster-autoscaler#configure-cluster-autoscaler-profile-for-bursty-workloads)

#### Example 2: Optimizing for cost

If you want a [cost-optimized profile](cluster-autoscaler#configure-cluster-autoscaler-profile-for-aggressive-scale-down), we recommend setting the following parameter configurations:

- Reduce
`scale-down-unneeded-time`

, which is the amount of time a node should be unneeded before it's eligible for scale down. - Reduce
`scale-down-delay-after-add`

, which is the amount of time to wait after a node is added before considering it for scale down. - Increase
`scale-down-utilization-threshold`

, which is the utilization threshold for removing nodes. - Increase
`max-empty-bulk-delete`

, which is the maximum number of nodes that can be deleted in a single call. - Set
`skip-nodes-with-local-storage`

to false. - Increase
`ok-total-unready-count`

and`max-total-unready-percentage`

.

## Common issues and mitigation recommendations

View scaling failures and scale-up not triggered events via [CLI or Portal](cluster-autoscaler#retrieve-cluster-autoscaler-logs-and-status).

### Not triggering scale up operations

| Common causes | Mitigation recommendations |
|---|---|
| PersistentVolume node affinity conflicts, which can arise when using the cluster autoscaler with multiple availability zones or when a pod's or persistent volume's zone differs from the node's zone. | Use one node pool per availability zone and enabling `--balance-similar-node-groups` . You can also set the
`volumeBindingMode` field to `WaitForFirstConsumer` |
| Taints and Tolerations/Node affinity conflicts | Assess the taints assigned to your nodes and review the tolerations defined in your pods. If necessary, make adjustments to the
|

[Restrictive Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)### Scale up operation failures

| Common causes | Mitigation recommendations |
|---|---|
| IP address exhaustion in the subnet | Add another subnet in the same virtual network and add another node pool into the new subnet. |
| Core quota exhaustion | Approved core quota has been exhausted.
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).### Scale down operation failures

| Common causes | Mitigation recommendations |
|---|---|
| Pod preventing node drain/Unable to evict pod | • View
• For pods using local storage, such as hostPath and emptyDir, set the cluster autoscaler profile flag `skip-nodes-with-local-storage` to `false` . • In the pod specification, set the `cluster-autoscaler.kubernetes.io/safe-to-evict` annotation to `true` . • Check your
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).[fully managed AKS resource group](cluster-configuration#fully-managed-resource-group-preview)(see[AKS support policies](support-policies)). Remove or reset any[resource locks](/en-us/azure/azure-resource-manager/management/lock-resources)you previously applied to the resource group.### Other issues

| Common causes | Mitigation recommendations |
|---|---|
| PriorityConfigMapNotMatchedGroup | Make sure that you add all the node groups requiring autoscaling to the
|

### Node pool in backoff

Node pool in backoff was introduced in version 0.6.2 and causes the cluster autoscaler to back off from scaling a node pool after a failure.

Depending on how long the scaling operations have been experiencing failures, it may take up to 30 minutes before making another attempt. You can reset the node pool's backoff state by disabling and then re-enabling autoscaling.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration -->

# Install Azure App Configuration AKS extension

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure App Configuration](/en-us/azure/azure-app-configuration/overview) provides a service to centrally manage application settings and feature flags. [Azure App Configuration Kubernetes Provider](https://mcr.microsoft.com/en-us/product/azure-app-configuration/kubernetes-provider/about) is a Kubernetes operator that gets key-values, Key Vault references and feature flags from Azure App Configuration and builds them into Kubernetes ConfigMaps and Secrets. Azure App Configuration extension for Azure Kubernetes Service (AKS) allows you to install and manage Azure App Configuration Kubernetes Provider on your AKS cluster via Azure Resource Manager (ARM).

## Prerequisites

- An Azure subscription.
[Create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - Permission with the
[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)role.

### Set up the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you haven't previously used cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?namespace=='Microsoft.KubernetesConfiguration']" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


## Install the extension on your AKS cluster

Create the Azure App Configuration extension, which installs Azure App Configuration Kubernetes Provider on your AKS.

For example, install the latest version of Azure App Configuration Kubernetes Provider via the Azure App Configuration extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration
```


Important

The Azure App Configuration AKS extension is installed into the `azappconfig-system`

namespace by default. If you have Azure Policy assignments that validate or mutate pod specifications (for example, the built-in policy "Kubernetes clusters should disable automounting API credentials" which enforces `automountServiceAccountToken: false`

), exclude the `azappconfig-system`

namespace from those policies by adding it to the policy's namespace exclusion list so the extension can function correctly. Not excluding it may cause the extension pods to fail validation or appear non-compliant.

### Configure automatic updates

If you create Azure App Configuration extension without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Azure App Configuration extension to automatically update its minor version on new releases.

You can disable auto update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

### Targeting a specific version

The same command-line argument is used for installing a specific version of Azure App Configuration Kubernetes Provider or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Azure App Configuration Kubernetes Provider you wish to install. If the `version`

parameter is omitted, the extension installs the latest version.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version false
--version 2.1.0
```


## Extension versions

The Azure App Configuration extension supports the following version of Azure App Configuration Kubernetes Provider:

`2.1.0`

`2.0.0`


## Troubleshoot extension installation errors

If the extension fails to create or update, try suggestions and solutions in the [Azure App Configuration extension troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-app-configuration-extension-installation-errors).

## Troubleshoot Azure App Configuration Kubernetes Provider

Troubleshoot Azure App Configuration Kubernetes Provider errors via the [troubleshooting guide](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#troubleshooting).

## Delete the extension

If you need to delete the extension and remove Azure App Configuration Kubernetes Provider from your AKS cluster, you can use the following command:

```
az k8s-extension delete --resource-group myResourceGroup --cluster-name myAKSCluster --cluster-type managedClusters --name appconfigurationkubernetesprovider
```


## Next Steps

- Learn more about
[extra settings and preferences you can set on the Azure App Configuration extension](azure-app-configuration-settings). - Once you successfully install Azure App Configuration extension in your AKS cluster, try
[quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service)to learn how to use it. - See all the supported features of
[Azure App Configuration Kubernetes Provider](/en-us/azure/azure-app-configuration/reference-kubernetes-provider).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-cluster -->

# Upgrade the Azure Kubernetes Service (AKS) cluster control plane

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters consist of two main components: the **control plane managed by Azure** and the **node pools where your workloads run**. This article focuses on upgrading the control plane independently, which allows you to adopt new Kubernetes versions for API server features while separately managing node pool upgrades.

## Before you begin

- If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires Azure PowerShell version 5.9.0 or later. Use the
`Get-InstalledModule -Name Az`

cmdlet to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Performing upgrade operations requires the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role. For more on Azure RBAC roles, see the[Azure resource provider operations](/en-us/azure/role-based-access-control/built-in-roles#containers). - Starting with Kubernetes version 1.30 and 1.27 LTS versions, beta APIs are disabled by default when you upgrade to them.

Warning

Ensure you have sufficient compute quota before upgrading. If quota is low, the upgrade might fail. For more information, see [increase quotas](/en-us/azure/azure-portal/supportability/regional-quota-requests).

## Overview of AKS upgrade types

The following table outlines three types of AKS upgrades, highlighting their scope and use cases:

| Upgrade type | Scope | Use case |
|---|---|---|
|

[Full cluster](#upgrade-the-full-aks-cluster)[Node pool only](upgrade-aks-node-pools-rolling)Tip

Upgrading the control plane first allows you to validate Kubernetes API compatibility before affecting running workloads. For node pool upgrade strategies, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

## Kubernetes version upgrade rules

When you upgrade a supported AKS cluster, you can't skip Kubernetes minor versions. You must perform all upgrades sequentially by minor version number. For example, upgrades between *1.28.x* -> *1.29.x* or *1.29.x* -> *1.30.x* are allowed. *1.28.x* -> *1.30.x* isn't allowed.

The control plane can be up to two minor versions ahead of node pools. For example, if your control plane is at *1.30.x*, your node pools can be at *1.28.x*, *1.29.x*, or *1.30.x*.

## Check for available AKS upgrades

Tip

To stay up to date with the latest AKS releases and updates, see the [AKS release tracker](release-tracker).

Check for available Kubernetes releases for your AKS cluster using the [ az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command.

```
az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name> --output table
```


The following example output shows the current version as *1.28.9* and lists the available versions under `upgrades`

:

```
Name ResourceGroup MasterVersion Upgrades
------- --------------- --------------- --------------
default <resource-group-name> 1.28.9 1.29.2, 1.29.4
```


## Upgrade the AKS control plane only

Upgrade the control plane using the

command with the`az aks upgrade`

`--control-plane-only`

flag. The following example upgrades the control plane to Kubernetes version*1.29.4*:`az aks upgrade \ --resource-group <resource-group-name> \ --name <cluster-name> \ --kubernetes-version 1.29.4 \ --control-plane-only`

Confirm the control plane upgrade was successful using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> --output table`

The following example output shows the control plane now runs

*1.29.4*:`Name Location ResourceGroup KubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------- ------------------------------------------------ <cluster-name> eastus <resource-group-name> 1.29.4 Succeeded <cluster-name>-dns-123abcd4.hcp.eastus.azmk8s.io`

Verify the node pool versions remain unchanged using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name> --query "[].{Name:name,Version:orchestratorVersion}" --output table`

In the output, the node pools should still show the previous Kubernetes version.


## Upgrade the full AKS cluster

Note

During a full cluster upgrade, AKS upgrades the control plane first, then upgrades each node pool sequentially. For more control over node pool upgrades, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

Upgrade the full cluster (control plane and all node pools) using the [ az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The following example upgrades the cluster to Kubernetes version

*1.29.4*:

```
az aks upgrade \
--resource-group <resource-group-name> \
--name <cluster-name> \
--kubernetes-version 1.29.4
```


## Frequently asked questions (FAQs)

### Why were my node pools upgraded when I only upgraded the control plane?

AKS might trigger a rolling node pool upgrade alongside a control plane upgrade to keep the cluster compliant and healthy. This upgrade typically occurs when a previous node upgrade failed or left nodes on mixed versions.

### Can I upgrade node pools before the control plane?

No. The control plane version must always be equal to or greater than any node pool version. You must upgrade the control plane first.

### How long does a control plane upgrade take?

Control plane upgrades typically complete within 5-15 minutes, depending on cluster configuration and Azure region load. Node pool upgrades take longer as they involve draining and reimaging nodes.

## Resolve control plane upgrade issues

### No upgrades available

If `az aks get-upgrades`

shows no available upgrades, your cluster might be:

- Already on the latest supported version.
- On an unsupported version that requires migration.

For unsupported versions, create a new cluster with a supported version and migrate your workloads.

### Upgrade failed due to deprecated APIs

Before upgrading, check for deprecated APIs using tools like [kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble):

```
kubent
```


Update your manifests to use supported API versions before upgrading.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-service-principal -->

# Use a service principal with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters require either a [Microsoft Entra service principal](/en-us/entra/identity-platform/app-objects-and-service-principals) or a [managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview) to dynamically create and manage other Azure resources. This article describes how to create a Microsoft Entra service principal and use it with your AKS cluster.

Note

For optimal security and ease of use, we recommend using managed identities instead of service principals to authorize access from an AKS cluster to other resources in Azure. A managed identity is a special type of service principal that you can use to get Microsoft Entra credentials without the need to manage and secure credentials. For more information, see [Use a managed identity in AKS](use-managed-identity).

## Prerequisites

- You need Azure CLI version 2.0.59 or higher. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- If using Azure PowerShell, you need Azure PowerShell version 5.0.0 or higher. Find your version using the
`Get-InstalledModule -Name Az`

cmdlet. If you need to install or upgrade, see[Install the Azure Az PowerShell module](/en-us/powershell/azure/install-az-ps).

- You need permissions to register an application with your Microsoft Entra tenant and to assign the application to a role in your subscription. If you don't have the necessary permissions, you need to ask your Microsoft Entra ID or subscription administrator to assign the necessary permissions or create the service principal for you.

## Considerations when using a service principal

Keep the following considerations in mind when using a Microsoft Entra service principal with AKS:

- The service principal for Kubernetes is a part of the cluster configuration, but don't use this identity to deploy the cluster. Instead,
[create a service principal](#create-a-service-principal)first, then use that service principal to create the AKS cluster. - Every service principal is associated with a Microsoft Entra application. You can associate the service principal for a Kubernetes cluster with any valid Microsoft Entra application name (for example:
`https://www.contoso.org/example`

). The URL for the application doesn't have to be a real endpoint. - When you specify the service principal
**client ID**, use the value of the application ID (`appId`

for Azure CLI or`ApplicationId`

for Azure PowerShell). - On the agent node virtual machines (VMs) in the AKS cluster, the service principal credentials are stored in the
`/etc/kubernetes/azure.json`

file. - When you delete an AKS cluster that you created using the
command or the`az aks create`

cmdlet, the service principal created isn't automatically deleted. See the`New-AzAksCluster`

[steps to delete a service principal](#delete-a-service-principal). - If you're using a service principal from a different Microsoft Entra tenant, there are other considerations around the permissions available when you deploy the cluster. You might not have the appropriate permissions to read and write directory information. For more information, see
[What are the default user permissions in Microsoft Entra ID?](/en-us/azure/active-directory/fundamentals/users-default-permissions)

## Create a service principal

Create a service principal using the

command.`az ad sp create-for-rbac`

`# Set environment variable SERVICE_PRINCIPAL_NAME=<your-service-principal-name> # Create the service principal az ad sp create-for-rbac --name $SERVICE_PRINCIPAL_NAME`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "myAKSClusterServicePrincipal", "name": "http://myAKSClusterServicePrincipal", "password": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the values for

`appId`

and`password`

from the output to use when creating the AKS cluster.

Create a service principal using the

command.`New-AzADServicePrincipal`

`# Set environment variable $SpName = <your-service-principal-name> # Create the service principal New-AzADServicePrincipal -DisplayName $SpName -OutVariable sp`

Your output should be similar to the following example output:

`Secret : System.Security.SecureString ServicePrincipalNames : {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, http://myAKSClusterServicePrincipal} ApplicationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ObjectType : ServicePrincipal DisplayName : myAKSClusterServicePrincipal Id : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Type :`

The values are stored in a variable that you use when creating the AKS cluster.

Decrypt the value stored in the

**Secret**secure string using the following command.`$BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sp.Secret) [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)`


## Create an AKS cluster with an existing service principal

Create an AKS cluster with an existing service principal using the

command with the`az aks create`

`--service-principal`

and`--client-secret`

parameters set to specify the`appId`

and`password`

values.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> APP_ID=<app-id> CLIENT_SECRET=<password-value> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --service-principal $APP_ID \ --client-secret $CLIENT_SECRET \ --generate-ssh-keys`


Convert the service principal

`ApplicationId`

and`Secret`

to a**PSCredential**object using the following command.`$Cred = New-Object -TypeName System.Management.Automation.PSCredential ($sp.ApplicationId, $sp.Secret)`

Create an AKS cluster with an existing service principal using the

cmdlet and specify the`New-AzAksCluster`

`ServicePrincipalIdAndSecret`

parameter with the**PSCredential**object as its value.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> # Create the AKS cluster New-AzAksCluster -ResourceGroupName $ResourceGroupName -Name $ClusterName -ServicePrincipalIdAndSecret $Cred`


Note

If you're using an existing service principal with customized secret, make sure the secret isn't longer than 190 bytes.

## Delegate access to other Azure resources

You can use the service principal for the AKS cluster to access other resources. For example, if you want to deploy your AKS cluster into an existing Azure virtual network (VNet) subnet, connect to ACR, or access keys or secrets in a key vault from your cluster, then you need to delegate access to those resources to the service principal. To delegate access, assign an Azure role-based access control (Azure RBAC) role to the service principal.

When you assign roles, you specify the scope for the role assignment, such as a resource group or VNet resource. The role assignment determines what permissions the service principal has on the resource and at what scope.

Important

Permissions granted to a service principal associated with a cluster can take up 60 minutes to propagate.

## Create a role assignment

Note

The scope for a resource needs to be a full resource ID, such as `/subscriptions/\<guid\>/resourceGroups/myResourceGroup`

or `/subscriptions/\<guid\>/resourceGroups/myResourceGroupVnet/providers/Microsoft.Network/virtualNetworks/myVnet`

.

Create a role assignment using the

command. Specify the value of the service principal app ID for the`az role assignment create`

`--assignee`

parameter and the scope for the role assignment for the`--scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`az role assignment create \ --assignee <app-id> \ --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" \ --role "Key Vault Secrets User"`


Create a role assignment using the

cmdlet. Specify the value of the service principal app ID for the`New-AzRoleAssignment`

`-ApplicationId`

parameter and the scope for the role assignment for the`-Scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`New-AzRoleAssignment -ApplicationId <app-id> ` -Scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" ` -RoleDefinitionName "Key Vault Secrets User"`


## Grant access to Azure Container Registry

If you use Azure Container Registry (ACR) as your container image store, you need to grant permissions to the service principal for your AKS cluster to read and pull images. We recommend following the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration) to integrate with a registry and assign the appropriate role for the service principal.

## Grant access to networking resources

If you're using advanced networking with a VNet and subnet or public IP addresses in different resource group, you can assign the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) built-in role on the subnet within the VNet. Alternatively, you can create a [custom role](/en-us/azure/role-based-access-control/custom-roles) with permissions to access the network resources in that resource group. For more information, see [AKS service permissions](concepts-identity#aks-service-permissions).

## Grant access to storage disks

If you need to access existing disk resources in another resource group, assign one of the following sets of role permissions:

- Create a
[custom role](/en-us/azure/role-based-access-control/custom-roles)and define the*Microsoft.Compute/disks/read*and*Microsoft.Compute/disks/write*role permissions. - Assign the
[Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor)built-in role on the resource group.

## Grant access to Azure Container Instances

If you use virtual kubelet to integrate with AKS and run Azure Container Instances (ACI) in resource group separate from the AKS cluster, you need to assign *Contributor* permissions to the AKS cluster service principal for the ACI resource group.

## Delete a service principal

Query for the service principal client ID (

`servicePrincipalProfile.clientId`

) and delete the service principal using thecommand with the`az ad sp delete`

`--id`

parameter. The [`az aks show`

][az-aks-show] command retrieves the client ID for the specified AKS cluster.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Delete the service principal az ad sp delete --id $(az aks show \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --query servicePrincipalProfile.clientId \ --output tsv)`


Query for the service principal client ID (

`ServicePrincipalProfile.ClientId`

) and delete the service principal using thecmdlet with the`Remove-AzADServicePrincipal`

`-ApplicationId`

parameter. The [`Get-AzAksCluster`

][get-azakscluster] cmdlet retrieves the client ID for the specified AKS cluster.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> $ClientId = (Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster ).ServicePrincipalProfile.ClientId # Delete the service principal Remove-AzADServicePrincipal -ApplicationId $ClientId`


## Resolve service principal credential issues

Azure CLI caches the service principal credentials for AKS clusters.

Azure PowerShell caches the service principal credentials for AKS clusters.

If these credentials expire, you might encounter errors during AKS cluster deployment. If there's an issue with the cached credentials, you might receive an error message similar to the following error message:

```
Operation failed with status: 'Bad Request'.
Details: The credentials in ServicePrincipalProfile were invalid. Please see https://aka.ms/aks-sp-help for more details.
Details: adal: Refresh request failed. Status Code = '401'.
```


You can check the expiration date of your service principal credentials using the [ az ad app credential list](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-list) command with the

`"[].endDateTime"`

query. The output shows you the `endDateTime`

of your credentials.```
az ad app credential list \
--id <app-id> \
--query "[].endDateTime" \
--output tsv
```


- Check the expiration date of your service principal credentials using the
cmdlet. The output shows you the`Get-AzADAppCredential`

`EndDate`

of your credentials.

```
Get-AzADAppCredential -ApplicationId <app-id>
```


**The default expiration time for the service principal credentials is one year**. If your credentials are older than one year, you can [reset the existing credentials](update-credentials#reset-the-existing-service-principal-credentials) or [create a new service principal](update-credentials#create-a-new-service-principal).
