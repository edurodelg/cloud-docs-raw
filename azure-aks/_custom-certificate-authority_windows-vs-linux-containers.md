---
merged_at: 2026-01-25T12:06:27.701914
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: custom-certificate-authority.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/custom-certificate-authority -->

# Use custom certificate authorities (CAs) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Custom Certificate Authority (CA) allows you to add up to 10 base64-encoded certificates to your node's trust store. This feature is often needed when certificate authorities (CAs) are required to be present on the node, like when connecting to a private registry.

This article shows you how to create custom CAs and apply them to your AKS clusters.

Note

The Custom CA feature adds your custom certificates to the trust store of the AKS node. Certificates added with this feature aren't available to containers running in pods. If you need the certificates inside containers, you need to add them separately by adding them to the image used by your pods or at runtime via scripting and a secret.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.72.0 or later installed and configured. To find your CLI version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - A base64 encoded certificate string or a text file with certificate.

## Limitations

- Windows node pools aren't supported.
- Installing different CAs in the same cluster isn't supported.

## Create a certificate file

Create a text file containing up to 10 blank line separated certificates. When you pass this file to your cluster, the certificates are installed in the trust stores of the AKS node.

Example text file:

`-----BEGIN CERTIFICATE----- cert1 -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- cert2 -----END CERTIFICATE-----`


**Before proceeding to the next step, make sure that there are no blank spaces in your text file to avoid errors**.

## Pass custom CAs to your AKS cluster

Pass certificates to your cluster using the

or`az aks create`

command with`az aks update`

`--custom-ca-trust-certificates`

set to the name of your certificate file.`# Create a new cluster az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --node-count 2 \ --custom-ca-trust-certificates <path-to-certificate-file> \ --generate-ssh-keys # Update an existing cluster az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --custom-ca-trust-certificates <path-to-certificate-file>`

Note

This operation triggers a model update to ensure all existing nodes have the same CAs installed for correct provisioning. AKS creates new nodes, drains existing nodes, deletes existing nodes, and replaces them with nodes that have the new set of CAs installed.


## Verify CAs are installed

Verify the CAs are installed using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> | grep securityProfile -A 4`

In the output, the

`securityProfile`

section should include your custom CA certificates. For example:`"securityProfile": { "azureKeyVaultKms": null, "customCaTrustCertificates": [ "values"`


## Resolve custom CA formatting errors

Adding certificates to a cluster can result in an error if the file with the certificates isn't formatted properly. You might see an error similar to the following example:

```
failed to decode one of SecurityProfile.CustomCATrustCertificates to PEM after base64 decoding
```


If you encounter this error, you should check that your input file has no extra new lines, white spaces, or data other than correctly formatted certificates as shown in the example file.

## Resolve custom CA X.509 Certificate Signed by Unknown Authority errors

AKS requires certificates passed to be properly formatted and base64 encoded. Make sure the CAs you passed are properly base64 encoded and that files with CAs don't have CRLF line breaks.

## Restart containerd to pick up new certificates

If containerd doesn't pick up new certificates, run the `systemctl restart containerd`

command from the node's shell. Once containerd restarts, the container runtime should pick up the new certificates.

## Related content

For more information on AKS security best practices, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).


---

<!-- DOCUMENTO FUSIONADO: windows-vs-linux-containers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

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
