---
merged_at: 2026-01-25T12:25:33.923464
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: csi-secrets-store-configuration-options.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-configuration-options -->

# Azure Key Vault provider for Secrets Store CSI Driver for AKS configuration and troubleshooting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver enables secure and automated management of secrets in Azure Kubernetes Service (AKS). This article provides guidance on configuring the provider, troubleshooting common issues, and optimizing secret handling in your AKS environment.

## Prerequisites

Follow the steps in the following articles before proceeding with this guide. Once you complete these steps, you can apply extra configurations or perform troubleshooting on your AKS cluster.

[Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver in AKS](csi-secrets-store-identity-access)

## Configuration options

### Manage auto rotation

Once you enable auto rotation for Azure Key Vault Secrets Provider, it updates the pod mount and the Kubernetes secret defined in the `secretObjects`

field of `SecretProviderClass`

. It does so by polling for changes periodically, based on the rotation poll interval you defined. The default rotation poll interval is *two minutes*. When a secret is updated in the external secrets store after the initial pod deployment, both the Kubernetes Secret and the pod mount are periodically refreshed. The update frequency and method depend on how your application accesses the secret data.

**Mount the Kubernetes Secret as a volume**: Use the auto rotation and sync K8s secrets features of Secrets Store CSI Driver. The application needs to watch for changes from the mounted Kubernetes Secret volume. When the CSI Driver updates the Kubernetes Secret, the corresponding volume contents automatically update as well.**Application reads the data from the container filesystem**: Use the rotation feature of Secrets Store CSI Driver. The application needs to watch for the file change from the volume mounted by the CSI driver.**Use the Kubernetes Secret for an environment variable**: Restart the pod to get the latest secret as an environment variable. Use a tool such as[Reloader](https://github.com/stakater/Reloader)to watch for changes on the synced Kubernetes Secret and perform rolling upgrades on pods.

To enable auto rotation of secrets on a new AKS cluster using the

command and enable the`az aks create`

`enable-secret-rotation`

add-on, run the following command:`az aks create \ --name myAKSCluster2 \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --enable-secret-rotation \ --generate-ssh-keys`

To update an existing AKS cluster to enable auto rotation of secrets using the

command and the`az aks addon update`

`enable-secret-rotation`

parameter, run the following command:`az aks addon update --resource-group myResourceGroup --name myAKSCluster2 --addon azure-keyvault-secrets-provider --enable-secret-rotation`


### Sync mounted content with a Kubernetes secret

Note

The YAML examples in this section are incomplete. You need to modify them to support your chosen method of access to your key vault identity. For details, see [Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-identity-access).

You might want to create a Kubernetes secret to mirror your mounted secrets content. Your secrets sync after you start a pod to mount them. When you delete the pods that consume the secrets, your Kubernetes secret is also deleted.

Sync mounted content with a Kubernetes secret using the `secretObjects`

field when creating a `SecretProviderClass`

to define the desired state of the Kubernetes secret, as shown in the
following example YAML. Make sure the `objectName`

in the `secretObjects`

field matches the file name of the mounted content. If you use `objectAlias`

instead, it should match the object alias.

```
apiVersion: secrets-store.csi.x-k8s.io/v1
kind: SecretProviderClass
metadata:
name: azure-sync
spec:
provider: azure
secretObjects: # [OPTIONAL] SecretObjects defines the desired state of synced Kubernetes secret objects
- data:
- key: username # data field to populate
objectName: foo1 # name of the mounted content to sync; this could be the object name or the object alias
secretName: foosecret # name of the Kubernetes secret object
type: Opaque # type of Kubernetes secret object (for example, Opaque, kubernetes.io/tls)
```


### Set an environment variable to reference Kubernetes secrets

Note

The example YAML demonstrates how to access a secret using either environment variables or `volume/volumeMount`

. Typically, an application uses one method or the other. However, to make a secret available through environment variables, at least one pod must mount the secret.

Reference your newly created Kubernetes secret by setting an environment variable in your pod, as shown in the following example YAML.

```
kind: Pod
apiVersion: v1
metadata:
name: busybox-secrets-store-inline
spec:
containers:
- name: busybox
image: registry.k8s.io/e2e-test-images/busybox:1.29-1
command:
- "/bin/sleep"
- "10000"
volumeMounts:
- name: secrets-store01-inline
mountPath: "/mnt/secrets-store"
readOnly: true
env:
- name: SECRET_USERNAME
valueFrom:
secretKeyRef:
name: foosecret
key: username
volumes:
- name: secrets-store01-inline
csi:
driver: secrets-store.csi.k8s.io
readOnly: true
volumeAttributes:
secretProviderClass: "azure-sync"
```


### Migrate from open-source to AKS-managed Secrets Store CSI Driver

Uninstall the open-source Secrets Store CSI Driver using the following

`helm delete`

command:`helm delete <release name>`

Tip

If you installed the driver and provider using deployment YAMLs, you can delete the components using the following

`kubectl delete`

command:`# Delete AKV provider pods from Linux nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer.yaml # Delete AKV provider pods from Windows nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer-windows.yaml`

Upgrade your existing AKS cluster with the feature using the

command:`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


## Access metrics

You can monitor the health and performance of the Azure Key Vault provider for Secrets Store CSI Driver by collecting metrics it exposes. These metrics provide insights into request durations, error rates, and the overall operation of the provider and driver components, helping you troubleshoot issues and optimize your AKS cluster's secret management.

Metrics are served via Prometheus from port 8898, but this port isn't exposed outside the pod by default. Access the metrics over localhost using the `kubectl port-forward`

command:

```
kubectl port-forward -n kube-system ds/aks-secrets-store-provider-azure 8898:8898 & curl localhost:8898/metrics
```


These metrics help you monitor the performance and reliability of the Azure Key Vault provider including request latency and error tracking for both Key Vault and gRPC operations.

| Metric | Description | Tags |
|---|---|---|
| keyvault_request | The distribution of how long it took to get from the key vault. | `os_type=<runtime os>` , `provider=azure` , `object_name=<keyvault object name>` , `object_type=<keyvault object type>` , `error=<error if failed>` |
| grpc_request | The distribution of how long it took for the gRPC requests. | `os_type=<runtime os>` , `provider=azure` , `grpc_method=<rpc full method>` , `grpc_code=<grpc status code>` , `grpc_message=<grpc status message>` |

## Troubleshooting

For troubleshooting steps, see [Troubleshoot Azure Key Vault Provider for Secrets Store CSI Driver](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-key-vault-csi-secrets-store-csi-driver).

## Next steps

To learn more about the Azure Key Vault provider for Secrets Store CSI Driver, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: container-network-security-wireguard-encryption-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-security-wireguard-encryption-concepts -->

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
