---
merged_at: 2026-01-25T12:25:33.947683
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-pod-sandboxing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-pod-sandboxing -->

# Pod Sandboxing with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To help secure and protect your container workloads from untrusted or potentially malicious code, AKS now includes a mechanism called Pod Sandboxing. Pod Sandboxing provides an isolation boundary between the container application and the shared kernel and compute resources of the container host such as CPU, memory, and networking. Applications are spun up in isolated, lightweight pod virtual machines (VMs). Pod Sandboxing complements other security measures or data protection controls with your overall architecture to help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand this new feature, and how to implement it.

## Prerequisites

The Azure CLI version 2.80.0 or later. Run

`az --version`

to find the version of your Azure CLI, and run`az upgrade`

to upgrade. For more details, see the steps at[Install Azure CLI](/en-us/cli/azure/install-azure-cli).AKS supports Pod Sandboxing on Kubernetes version 1.27.0 and higher.

To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.

## Limitations

The following are constraints applicable to Pod Sandboxing:

Kata containers might not reach the IOPS performance limits that traditional containers can reach on Azure Files and high-performance local SSD.

[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)doesn't support assessing Kata runtime pods.[Kata](https://github.com/kata-containers/kata-containers/blob/main/docs/Limitations.md#host-network)host-network access isn't supported. It isn't possible to directly access the host networking configuration from within the VM.CPU and memory allocation with Pod Sandboxing has other considerations compared to

`runc`

. Reference the memory management sections in the[considerations page](considerations-pod-sandboxing).

## How it works

Pod Sandboxing on AKS builds on top of the open-source [Kata Containers](https://katacontainers.io/) project. Kata Containers running on the Azure Linux container host for AKS provides VM based isolation and a separate kernel for each pod. Pod Sandboxing allows users to allocate resources for each pod and doesn't share them with other Kata Containers or namespace containers running on the same host.

The solution architecture is based on the following main components:

- The
[Azure Linux container host for AKS](use-azure-linux) - Microsoft Hyper-V Hypervisor
- Open-source
[Cloud-Hypervisor](https://www.cloudhypervisor.org)Virtual Machine Monitor (VMM) - Integration with
[Kata Container](https://katacontainers.io)for the runtime

Deploying Pod Sandboxing using Kata Containers is similar to the standard `containerd`

workflow to deploy containers. Clusters with Pod Sandboxing enabled come with a specific runtime class that can be referenced in a pod manifest (`runtimeClassName: kata-vm-isolation`

).

To use this feature with a pod, the only difference is to add the **runtimeClassName**, `kata-vm-isolation`

to the pod spec. When a pod uses the `kata-vm-isolation`

runtimeClass, the hypervisor spins up a lightweight virtual machine with its own kernel, for the workload to operate in.

## Deploy new cluster

Perform the following steps to deploy an Azure Linux AKS cluster using the Azure CLI.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. With this parameter, these other parameters should satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameters.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.

The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*:`az aks create --name myAKSCluster \ --resource-group myResourceGroup \ --os-sku AzureLinux \ --workload-runtime KataVmIsolation \ --node-vm-size Standard_D4s_v3 \ --node-count 3 \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

List all Pods in all namespaces using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods --all-namespaces`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Verify the cluster is running Kubernetes version 1.27.0 and higher.

Use the following command to enable Pod Sandboxing by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.


The following example adds a node pool to

*myAKSCluster*with one node in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --cluster-name myAKSCluster --resource-group myResourceGroup --name nodepool2 --os-sku AzureLinux --workload-runtime KataVmIsolation --node-vm-size Standard_D4s_v3`

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable pod sandboxing on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`


## Deploying your applications

With Pod Sandboxing, you can deploy a mix of "normal" pods that don't utilize the Kata runtime alongside Kata pods that do utilize the runtime. The main difference between the two, when deploying, lies in the fact that a Kata pod has the line `runtimeClassName: kata-vm-isolation`

in its spec.

### Deploy an application with the Kata runtime

To deploy a pod with the Kata runtime on your AKS cluster, perform the following steps.

Create a file named

*kata-app.yaml*to describe your kata pod, and then paste the following manifest.`kind: Pod apiVersion: v1 metadata: name: isolated-pod spec: runtimeClassName: kata-vm-isolation containers: - name: kata image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11 command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]`

The value for

**runtimeClassNameSpec**is`kata-vm-isolation`

.Deploy the Kubernetes pod by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your*kata-app.yaml*file:`kubectl apply -f kata-app.yaml`

The output of the command resembles the following example:

`pod/isolated-pod created`


## (Optional) Verify Kernel Isolation configuration

If you would like to verify the difference between the kernel of a Kata and non-Kata pod, you can spin up another workload that doesn't have the Kata runtime.

```
kind: Pod
apiVersion: v1
metadata:
name: normal-pod
spec:
containers:
- name: non-kata
image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11
command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]
```


To access a container inside the AKS cluster, start a shell session by running the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command. In this example, you're accessing the container inside*kata-pod*.`kubectl exec -it isolated-pod -- /bin/sh`

Kubectl connects to your cluster, runs

`/bin/sh`

inside the first container within`isolated-pod`

, and forwards your terminal's input and output streams to the container's process. You can also start a shell session to the container hosting the non-Kata pod to see the differences.After starting a shell session to the container from

*kata-pod*, you can run commands to verify that the*kata*container is running in a pod sandbox. Notice that it has a different kernel version compared to the non-Kata container outside the sandbox.To see the kernel version run the following command:

`uname -r`

The following example resembles output from the pod sandbox kernel:

`[user]/# uname -r 6.6.96.mshv1`

Start a shell session to the container from

*normal-pod*to verify the kernel output:`kubectl exec -it normal-pod -- /bin/bash`

To see the kernel version run the following command:

`uname -r`

The following example resembles output from the VM that's running

*normal-pod*, which is a different kernel than the Kata pod running within the pod sandbox:`6.6.100.mshv1-1.azl3`


## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you deployed Pod Sandboxing on an existing cluster, you can remove the pods using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl get pods
kubectl delete pod <kata-pod-name>
```


## Next steps

- Learn more about
[Azure Dedicated hosts](use-azure-dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events. - To further explore Pod Sandboxing isolation and explore workload scenarios, try out the
[Pod Sandboxing labs](https://azure-samples.github.io/aks-labs/docs/security/pod-sandboxing-on-aks).


---

<!-- DOCUMENTO FUSIONADO: certificate-rotation.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/certificate-rotation -->

# Certificate rotation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses certificates for authentication with many of its components. You need to periodically rotate those certificates for security or policy reasons. This article shows you how certificate rotation works in your AKS cluster.

## Prerequisites

This article requires the Azure CLI version 2.0.77 or later. Check your version using the

`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Configure

`kubectl`

to connect to your AKS cluster using thecommand:`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## AKS certificates, Certificate Authorities, and Service Accounts

AKS generates and uses the following certificates, Certificate Authorities (CA), and Service Accounts (SA):

- The AKS API server creates a CA called the
*Cluster CA*, which signs certificates for one-way communication from the API server to kubelet. - Each kubelet creates a Certificate Signing Request (CSR), which the Cluster CA signs, for communication from the kubelet to the API server.
- The API aggregator uses the Cluster CA to issue certificates for communication with other APIs. The API aggregator can also have its own CA for issuing those certificates, but it currently uses the Cluster CA.
- Each agent node uses an SA token, which the Cluster CA signs.
- The
`kubectl`

client has a certificate for communicating with the AKS cluster.

Microsoft maintains all certificates mentioned in this section, except for the cluster certificate.

## Certificate expiration dates

Important

The expiration date for your certificates depends on when your AKS cluster was created:

**AKS clusters created**have certificates that expire after two years.*before*May 2019**AKS clusters created**have Cluster CA certificates that expire after 30 years.*after*May 2019

You can verify when your cluster was created using the `kubectl get nodes`

command, which shows you the `Age`

of your agent nodes.

## Check cluster certificate expiration date

Check the expiration date of the cluster certificate using the

`kubectl config view`

command.`kubectl config view --raw -o jsonpath="{.clusters[?(@.name == '')].cluster.certificate-authority-data}" | base64 -d | openssl x509 -text | grep -A2 Validity`


## Check API server certificate expiration date

Check the expiration date of the API server certificate using the following

`curl`

command:`curl https://{apiserver-fqdn} -k -v 2>&1 | grep expire`


## Check virtual machine (VM) agent node certificate expiration date

Check the expiration date of the VM agent node certificate using the

command.`az vm run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the VM agent node. -`--name <vm-name>`

: The name of the VM agent node. -`--scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`

: The script that retrieves the expiration date of the API server certificate located at`/etc/kubernetes/certs/apiserver.crt`

.`az vm run-command invoke --resource-group <node-resource-group> --name <vm-name> --command-id RunShellScript --query 'value[0].message' -otsv --scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`


## Check certificate expiration for the Azure Virtual Machine Scale Set agent node

Check the expiration date of the Azure Virtual Machine Scale Set agent node certificate using the

command.`az vmss run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the Azure Virtual Machine Scale Set agent node. -`--name <vmss-name>`

: The name of the Azure Virtual Machine Scale Set. -`--instance-id 1`

: The instance ID of the Azure Virtual Machine Scale Set agent node. -`--scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate"`

: The script that retrieves the expiration date of the kubelet client certificate located at`/var/lib/kubelet/pki/kubelet-client-current.pem`

.`az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 1 --scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate" --query "value[0].message"`


## Manually rotate your cluster certificates

Rotate all certificates, CAs, and SAs on your cluster using the

command.`az aks rotate-certs`

`az aks rotate-certs --resource-group <resource-group> --name <cluster-name>`

Important

The

command recreates all of your agent nodes, Azure Virtual Machine Scale Sets, and disks. This command can also cause up to`az aks rotate-certs`

*30 minutes of downtime*for your AKS cluster. If the command fails before completing, use the [`az aks show`

][az-aks-show] command to verify the status of the cluster is`Certificate Rotating`

. If the cluster is in a failed state, rerun thecommand to rotate your certificates again.`az aks rotate-certs`

Verify the old certificates are no longer valid using any

`kubectl`

command. The following example uses the`kubectl get nodes`

command:`kubectl get nodes`

If you didn't update the certificates used by

`kubectl`

, you see an error similar to the following example output:`Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "ca")`

Update the certificate used by

`kubectl`

using thecommand with the`az aks get-credentials`

`--overwrite-existing`

flag.`az aks get-credentials --resource-group <resource-group> --name <cluster-name> --overwrite-existing`

Verify the certificates are updated using the

command.`kubectl get`

`kubectl get nodes`


If you have any services that run on top of AKS, you might need to update their certificates as well.

## Rotate the kubelet serving certificate

When you rotate the kubelet serving certificate, AKS allows kubelet server Transport Layer Security (TLS) Bootstrapping for both bootstrapping and rotating serving certificates signed by the Cluster CA.

### Limitations for kubelet serving certificate rotation

- Supported on Kubernetes version 1.27 and above.
- Not supported when the node pool is using a node pool snapshot based on any node image older than
`202501.12.0`

. - You can't manually enable this feature. Kubelet serving certificate rotation is enabled by default on existing node pools when they perform their first upgrade to any Kubernetes version 1.27 or higher. Kubelet serving certificate rotation is enabled by default on new node pools using Kubernetes version 1.27 or higher. To see if kubelet serving certificate rotation is enabled in your region, check the
[AKS releases](https://github.com/Azure/AKS/releases).

## Verify kubelet serving certificate rotation is enabled

Each node with the feature enabled is automatically given the label `kubernetes.azure.com/kubelet-serving-ca=cluster`

.

Verify the labels are set using the

`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

command.`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

The output should show the label

`kubernetes.azure.com/kubelet-serving-ca`

with the value`cluster`

for each agent node.

## Verify kubelet TLS Bootstrapping is working

Verify the bootstrapping process is taking place using the

command.`kubectl get`

`kubectl get csr --field-selector=spec.signerName=kubernetes.io/kubelet-serving`

In the output, all serving CSRs should be in the

`Approved,Issued`

state, which indicates the CSR was approved and issued a signed certificate. Serving CSRs have a signer name of`kubernetes.io/kubelet-serving`

. For example:`NAME AGE SIGNERNAME REQUESTOR REQUESTEDDURATION CONDITION csr-1ab2c 113s kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:uoxr9r none Approved,Issued csr-defgh 111s kubernetes.io/kubelet-serving system:node:akswinp7000000 none Approved,Issued csr-ij3kl 46m kubernetes.io/kubelet-serving system:node:akswinp6000000 none Approved,Issued csr-mn4op 46m kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:ho7zyu none Approved,Issued`


## Verify kubelet is using a certificate obtained from server TLS Bootstrapping

Confirm the kubelet is using a serving certificate signed by the Cluster CA using the

command.`kubectl debug`

`kubectl debug node/<node> -ti --image=mcr.microsoft.com/azurelinux/base/core:3.0 -- ls -l /host/var/lib/kubelet/kubelet-server-current.pem`

If a

`kubelet-server-current.pem`

symlink exists, then the kubelet bootstrapped/rotated its own serving certificate, and the Cluster CA signed it.

## Disable kubelet serving certificate rotation

Disable kubelet serving certificate rotation by updating the node pool using the

command with the`az aks nodepool update`

`aks-disable-kubelet-serving-certificate-rotation=true`

tag.`az aks nodepool update --cluster-name <cluster-name> --resource-group <resource-group> --name <node-pool-name> --tags aks-disable-kubelet-serving-certificate-rotation=true`


- Reimage your nodes using a
[node image upgrade](node-image-upgrade)or by scaling the pool to*zero*instances and then back up to the desired value.

## Certificate autorotation

Keep the following considerations in mind when using certificate autorotation:

- If you have an existing cluster, you have to upgrade that cluster to enable certificate autorotation.
- Don't disable TLS Bootstrap to keep certificate autorotation enabled.
- If the cluster is in a stopped state during certificate autorotation, only the control plane certificates are rotated. In this case, you should recreate the node pool after certificate rotation to initiate the node pool certificate rotation.
- For any AKS clusters created or upgraded after March 2022, AKS automatically rotates non-CA certificates on both the control plane and agent nodes within 80% of the client certificate valid time before they expire with no downtime for the cluster.

## Verify TLS Bootstrapping is enabled on current agent node pool

Verify your cluster has TLS Bootstrapping enabled by browsing to one to the following paths:

**On a Linux node**:`/var/lib/kubelet/bootstrap-kubeconfig`

or`/host/var/lib/kubelet/bootstrap-kubeconfig`

**On a Windows node**:`C:\k\bootstrap-config`


For more information, see

[Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting](node-access).Note

The file path might change as Kubernetes versions evolve.

Once a region is configured, create a new cluster or upgrade an existing cluster to set certificate autorotation for the cluster certificate. You need to upgrade the control plane and node pool to enable this feature.
