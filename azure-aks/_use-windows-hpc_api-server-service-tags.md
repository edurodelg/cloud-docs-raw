---
merged_at: 2026-01-25T12:25:33.863313
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-windows-hpc.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-windows-hpc -->

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

<!-- DOCUMENTO FUSIONADO: api-server-service-tags.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-service-tags -->

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
