---
merged_at: 2026-01-28T07:16:09.859323
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-security -->

# Security concepts for applications and clusters in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container security protects the entire end-to-end pipeline from build to the application workloads running in Azure Kubernetes Service (AKS).

The Secure Supply Chain includes the build environment and registry.

Kubernetes includes security components, such as *pod security standards* and *Secrets*. Azure includes components like Active Directory, Microsoft Defender for Containers, Azure Policy, Azure Key Vault, network security groups, and orchestrated cluster upgrades. AKS combines these security components to:

- Provide a complete authentication and authorization story.
- Apply AKS Built-in Azure Policy to secure your applications.
- End-to-End insight from build through your application with Microsoft Defender for Containers.
- Keep your AKS cluster running the latest OS security updates and Kubernetes releases.
- Provide secure pod traffic and access to sensitive credentials.

This article introduces the core concepts that secure your applications in AKS.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Build Security

As the entry point for the Supply Chain, it's important to conduct static analysis of image builds before they're promoted down the pipeline. This includes vulnerability and compliance assessment. It's not about failing a build because it has a vulnerability, as that breaks development. It's about looking at the **Vendor Status** to segment based on vulnerabilities that are actionable by the development teams. Also use **Grace Periods** to allow developers time to remediate identified issues.

## Registry Security

Assessing the vulnerability state of the image in the Registry detects drift and also catches images that didn't come from your build environment. Use [Notary V2](https://github.com/notaryproject/notaryproject) to attach signatures to your images to ensure deployments are coming from a trusted location.

## Cluster security

In AKS, the Kubernetes master components are part of the managed service provided, managed, and maintained by Microsoft. Each AKS cluster has its own single-tenanted, dedicated Kubernetes master to provide the API Server, Scheduler, etc. For more information, see [Vulnerability management for Azure Kubernetes Service](concepts-vulnerability-management).

By default, the Kubernetes API server uses a public IP address and a fully qualified domain name (FQDN). You can limit access to the API server endpoint using [authorized IP ranges](api-server-authorized-ip-ranges). You can also create a fully [private cluster](private-clusters) to limit API server access to your virtual network.

You can control access to the API server using Kubernetes role-based access control (Kubernetes RBAC) and Azure RBAC. For more information, see [Microsoft Entra integration with AKS](managed-azure-ad).

## Node security

AKS nodes are Azure virtual machines (VMs) that you manage and maintain.

- Linux nodes run optimized versions of Ubuntu or Azure Linux.
- Windows Server nodes run an optimized Windows Server release using the
`containerd`

container runtime.

When an AKS cluster is created or scaled up, the nodes are automatically deployed with the latest OS security updates and configurations.

Note

AKS clusters running:

- Kubernetes version 1.19 and higher - Linux node pools use
`containerd`

as its container runtime. Windows Server 2019 and Windows Server 2022 node pools use`containerd`

as its container runtime. For more information, see[Add a Windows Server node pool with](create-node-pools).`containerd`

- Kubernetes version 1.19 and earlier - Linux node pools use Docker as its container runtime.

For more information about the security upgrade process for Linux and Windows worker nodes, see [Security patching nodes](concepts-vulnerability-management#worker-nodes).

AKS clusters running Azure Generation 2 VMs include support for [Trusted Launch](use-trusted-launch). This feature protects against advanced and persistent attack techniques by combining technologies that you can enable independently, like secure boot and a virtualized version of the trusted platform module (vTPM). Administrators can deploy AKS worker nodes with verified and signed bootloaders, OS kernels, and drivers to ensure integrity of the entire boot chain of the underlying VM.

### Container and security optimized OS options

AKS released support for two new optimized Linux OS options. [Azure Linux OS Guard (preview)](https://aka.ms/aks/azure-linux-os-guard) is Microsoft-created and optimized for Azure. OS Guard is built on top of Azure Linux with specialized configuration to support containerized workloads with security optimizations. [Flatcar Container Linux for AKS (preview)](https://aka.ms/aks/flatcar) is a CNCF-based vendor-neutral container-optimized immutable OS, best suited for running on multicloud and on-premises environments. These OS options provide increased security when compared to other Linux OS options, such as:

- Both Azure Linux OS Guard and Flatcar Container Linux for AKS have an immutable operating system that you can't modify at runtime. All OS binaries, libraries and static configuration are read-only, and the bit-for-bit integrity is often cryptographically protected. These special purpose operating systems ship as self-contained images and come without any kind of package management or other traditional means of altering the OS. User workloads run in isolated environments like containers, sandboxed from the OS.
- Both Azure Linux OS Guard and Flatcar Container Linux for AKS use SELinux for Mandatory Access Control.
- Azure Linux OS Guard enforces
[FIPS](enable-fips-nodes)and[Trusted Launch](use-trusted-launch)enablement, providing improved compliance and protection against advanced and persistent attacks by combining secure boot and virtualized version of trusted platform module (vTPM).

When deciding between which container-optimized OS options to use, AKS recommends the following:

- Use
if you're looking for a vendor neutral immutable OS with cross-cloud support.**Flatcar Container Linux for AKS (preview)** - Use
if you're looking for an enterprise-ready immutable OS, recommended by Microsoft.**Azure Linux OS Guard (preview)** - Use
[Ubuntu](https://aka.ms/aks/supported-ubuntu-versions)if you're looking for a vendor neutral, general purpose OS with cross-cloud support. - Use
[Azure Linux](https://aka.ms/aks/use-azure-linux)if you're looking for an enterprise-ready, general purpose OS, recommended by Microsoft.


### Node authorization

Node authorization is a special-purpose authorization mode that specifically authorizes kubelet API requests to protect against East-West attacks. Node authorization is enabled by default on AKS 1.24 + clusters.

### Node deployment

Nodes are deployed onto a private virtual network subnet, with no public IP addresses assigned. For troubleshooting and management purposes, SSH is enabled by default and only accessible using the internal IP address. Disabling SSH during cluster and node pool creation, or for an existing cluster or node pool, is in preview. See [Manage SSH access](manage-ssh-node-access) for more information.

### Node storage

To provide storage, the nodes use Azure Managed Disks. For most VM node sizes, Azure Managed Disks are Premium disks backed by high-performance SSDs. The data stored on managed disks is automatically encrypted at rest within the Azure platform. To improve redundancy, Azure Managed Disks are securely replicated within the Azure datacenter.

### Hostile multitenant workloads

Currently, Kubernetes environments aren't safe for hostile multitenant usage. Extra security features, like *Pod Security Policies* or Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters. For more information on ways to isolate workloads, see [Best practices for cluster isolation in AKS](operator-best-practices-cluster-isolation).

### Compute isolation

Because of compliance or regulatory requirements, certain workloads may require a high degree of isolation from other customer workloads. For these workloads, Azure provides:

[Kernel isolated containers](/en-us/azure/confidential-computing/confidential-containers)to use as the agent nodes in an AKS cluster. These containers are completely isolated to a specific hardware type and isolated from the Azure Host fabric, the host operating system, and the hypervisor. They're dedicated to a single customer. Select[one of the isolated VMs sizes](/en-us/azure/virtual-machines/isolation)as the**node size**when creating an AKS cluster or adding a node pool.[Confidential Containers](confidential-containers-overview)(preview), also based on Kata Confidential Containers, encrypts container memory and prevents data in memory during computation from being in clear text, readable format, and tampering. It helps isolate your containers from other container groups/pods, and VM node OS kernel. Confidential Containers (preview) uses hardware based memory encryption (SEV-SNP).[Pod Sandboxing](use-pod-sandboxing)(preview) provides an isolation boundary between the container application and the shared kernel and compute resources (CPU, memory, and network) of the container host.

## Network security

For connectivity and security with on-premises networks, you can deploy your AKS cluster into existing Azure virtual network subnets. These virtual networks connect back to your on-premises network using Azure Site-to-Site VPN or Express Route. Define Kubernetes ingress controllers with private, internal IP addresses to limit services access to the internal network connection.

### Azure network security groups

To filter virtual network traffic flow, Azure uses network security group rules. These rules define the source and destination IP ranges, ports, and protocols allowed or denied access to resources. Default rules are created to allow TLS traffic to the Kubernetes API server. You create services with load balancers, port mappings, or ingress routes. AKS automatically modifies the network security group for traffic flow.

If you provide your own subnet for your AKS cluster (whether using Azure CNI or Kubenet), **do not** modify the NIC-level network security group managed by AKS. Instead, create more subnet-level network security groups to modify the flow of traffic. Make sure they don't interfere with necessary traffic managing the cluster, such as load balancer access, communication with the control plane, or [egress](limit-egress-traffic).

### Kubernetes network policy

To limit network traffic between pods in your cluster, AKS offers support for [Kubernetes network policies](use-network-policies). With network policies, you can allow or deny specific network paths within the cluster based on namespaces and label selectors.

## Application Security

To protect pods running on AKS, consider [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) to detect and restrict cyber attacks against your applications running in your pods. Run continual scanning to detect drift in the vulnerability state of your application and implement a "blue/green/canary" process to patch and replace the vulnerable images.

## Secure container access to resources

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access. Built-in Linux security features such as *AppArmor* and *seccomp* are recommended as [best practices](/en-us/azure/aks/operator-best-practices-cluster-security) to [secure container access to resources][secure-container-access].

## Kubernetes Secrets

With a Kubernetes *Secret*, you inject sensitive data into pods, such as access credentials or keys.

- Create a Secret using the Kubernetes API.
- Define your pod or deployment and request a specific Secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The Secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a Secret, the Secret is deleted from the node's
*tmpfs*.- Secrets are stored within a given namespace and are only accessible from pods within the same namespace.


Using Secrets reduces the sensitive information defined in the pod or service YAML manifest. Instead, you request the Secret stored in Kubernetes API Server as part of your YAML manifest. This approach only provides the specific pod access to the Secret.

Note

The raw secret manifest files contain the secret data in base64 format. For more information, see the [official documentation](https://kubernetes.io/docs/concepts/configuration/secret/#risks). Treat these files as sensitive information, and never commit them to source control.

Kubernetes secrets are stored in *etcd*, a distributed key-value store. AKS allows [encryption at rest of secrets in etcd using customer managed keys](use-kms-etcd-encryption).

## Next steps

To get started with securing your AKS clusters, see [Upgrade an AKS cluster](upgrade-cluster).

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

For more information on core Kubernetes and AKS concepts, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/passive-cold-solution -->

# Passive-cold solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines a passive-cold solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic when the application is needed.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Passive-cold solution overview

In this approach, we have two independent AKS clusters being deployed in two Azure regions. When the application is needed, we activate the passive cluster to receive traffic. If the passive cluster goes down, we must manually activate the cold cluster to take over the flow of traffic. We can set this condition through a manual input every time or to specify a certain event.

## Scenarios and configurations

This solution is best implemented as a “use as needed” workload, which is useful for scenarios that require workloads to run at specific times of day or run on demand. Example use cases for a passive-cold approach include:

- A manufacturing company that needs to run a complex and resource-intensive simulation on a large dataset. In this case, the passive cluster is located in a cloud region that offers high-performance computing and storage services. The passive cluster is only used when the simulation is triggered by the user or by a schedule. If the cluster doesn’t work upon triggering, the cold cluster can be used as a backup and the workload can run on it instead.
- A government agency that needs to maintain a backup of its critical systems and data in case of a cyber attack or natural disaster. In this case, the passive cluster is located in a secure and isolated location that’s not accessible to the public.

## Components

The passive-cold disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. When the app is needed, the passive cluster is activated to receive network traffic.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If the passive cluster isn't functioning properly because of an issue in its specific Azure region, you can activate the cold cluster and redirect all traffic to that cluster's region. You can use this process while the passive cluster is deactivated until it starts working again. The cold cluster can take a couple minutes to come online, as it has been turned off and needs to complete the setup process. This approach isn't ideal for time-sensitive applications. In that case, we recommend considering an [active-active failover](active-active-solution#failover-process).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-portal -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and Azure Kubernetes Service (AKS) clusters. To provide this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). AKS clusters are created with *basic* networking (kubenet) by default.

This article shows you how to create a virtual network and subnets, and then deploy an AKS cluster that uses advanced networking using the Azure portal.

Note

For an overview of virtual node region availability and limitations, see [Use virtual nodes in AKS](virtual-nodes).

## Before you begin

You need the ACI service provider registered on your subscription.

Check the status of the ACI provider registration using the

command.`az provider list`

`az provider list --query "[?contains(namespace,'Microsoft.ContainerInstance')]" -o table`

The following example output shows the

*Microsoft.ContainerInstance*provider is*Registered*:`Namespace RegistrationState RegistrationPolicy --------------------------- ------------------- -------------------- Microsoft.ContainerInstance Registered RegistrationRequired`

If the provider is

*NotRegistered*, register it using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerInstance`


## Create an AKS cluster

- Navigate to the Azure portal home page.
- Select
**Create a resource**>**Containers**. - On the
**Azure Kubernetes Service (AKS)**resource, select**Create**. - On the
**Basics**page, configure the following options:*Project details*: Select an Azure subscription, then select or create an Azure resource group, such as*myResourceGroup*.*Cluster details*: Enter a**Kubernetes cluster name**, such as*myAKSCluster*. Select a region and Kubernetes version for the AKS cluster.

- Select
**Next: Node pools**and check **Enable virtual nodes*. - Select
**Review + create**. - After the validation completes, select
**Create**.

By default, this process creates a managed cluster identity, which is used for cluster communication and integration with other Azure services. For more information, see [Use managed identities](use-managed-identity). You can also use a service principal as your cluster identity.

This process configures the cluster for advanced networking and the virtual nodes to use their own Azure virtual network subnet. The subnet has delegated permissions to connect Azure resources between the AKS cluster. If you don't already have a delegated subnet, the Azure portal creates and configures an Azure virtual network and subnet with the virtual nodes.

## Connect to the cluster

The Azure Cloud Shell is a free interactive shell you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account. To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. The `kubectl`

client is pre-installed in the Azure Cloud Shell.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the cluster name`az aks get-credentials`

*myAKSCluster*in the resource group named*myResourceGroup*:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

.`kubectl get nodes`

`kubectl get nodes`

The following example output shows the single VM node created and the virtual Linux node named

*virtual-node-aci-linux*:`NAME STATUS ROLES AGE VERSION virtual-node-aci-linux Ready agent 28m v1.11.2 aks-agentpool-14693408-0 Ready agent 32m v1.11.2`


## Deploy a sample app

In the Azure Cloud Shell, create a file named

`virtual-node.yaml`

and copy in the following YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aci-helloworld spec: replicas: 1 selector: matchLabels: app: aci-helloworld template: metadata: labels: app: aci-helloworld spec: containers: - name: aci-helloworld image: mcr.microsoft.com/azuredocs/aci-helloworld ports: - containerPort: 80 nodeSelector: kubernetes.io/role: agent beta.kubernetes.io/os: linux type: virtual-kubelet tolerations: - key: virtual-kubelet.io/provider operator: Exists`

The YAML defines a

[nodeSelector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)and[toleration](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/), which allows the pod to be scheduled on the virtual node. The pod is assigned an internal IP address from the Azure virtual network subnet delegated for use with virtual nodes.Run the application using the

command.`kubectl apply`

`kubectl apply -f virtual-node.yaml`

View the pods scheduled on the node using the

command with the`kubectl get pods`

`-o wide`

argument.`kubectl get pods -o wide`

The following example output shows the

`virtual-node-helloworld`

pod scheduled on the`virtual-node-linux`

node.`NAME READY STATUS RESTARTS AGE IP NODE virtual-node-helloworld-9b55975f-bnmfl 1/1 Running 0 4m 10.241.0.4 virtual-node-aci-linux`


Note

If you use images stored in Azure Container Registry, [configure and use a Kubernetes secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/). A limitation of virtual nodes is you can't use integrated Microsoft Entra service principal authentication. If you don't use a secret, pods scheduled on virtual nodes fail to start and report the error `HTTP response status code 400 error code "InaccessibleImage"`

.

## Test the virtual node pod

To test the pod running on the virtual node, browse to the demo application with a web client. The pod is assigned an internal IP address, so you can easily test the connectivity from another pod on the AKS cluster.

Create a test pod and attach a terminal session to it using the following

`kubectl run`

command.`kubectl run -it --rm virtual-node-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

Install

`curl`

in the pod using the following`apt-get`

command.`apt-get update && apt-get install -y curl`

Access the address of your pod using the following

`curl`

command and provide your internal IP address.`curl -L http://10.241.0.4`

The following condensed example output shows the demo application.

`<html> <head> <title>Welcome to Azure Container Instances!</title> </head> [...]`

Close the terminal session to your test pod with

`exit`

, which also deletes the pod.`exit`


## Next steps

In this article, you scheduled a pod on the virtual node and assigned a private, internal IP address. If you want, you can instead create a service deployment and route traffic to your pod through a load balancer or ingress controller. For more information, see [Create a basic ingress controller in AKS](ingress-basic).

Virtual nodes are one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/what-is-aks -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/intro-kubernetes -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler -->

# Use the cluster autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demands. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed.

This article shows you how to enable and manage the cluster autoscaler in AKS, which is based on the [open-source Kubernetes version](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).

## Before you begin

This article requires Azure CLI version 2.0.76 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Use the cluster autoscaler on an AKS cluster

Important

The cluster autoscaler is a Kubernetes component. Although the AKS cluster uses a virtual machine scale set for the nodes, don't manually enable or edit settings for scale set autoscaling. Let the Kubernetes cluster autoscaler manage the required scale settings. For more information, see [Can I modify the AKS resources in the node resource group?](faq)

### Enable the cluster autoscaler on a new cluster

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create an AKS cluster using the

command and enable and configure the cluster autoscaler on the node pool for the cluster using the`az aks create`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command creates a cluster with a single node backed by a virtual machine scale set, enables the cluster autoscaler, sets a minimum of one and maximum of three nodes:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --vm-set-type VirtualMachineScaleSets \ --load-balancer-sku standard \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --generate-ssh-keys`

It takes a few minutes to create the cluster and configure the cluster autoscaler settings.


### Enable the cluster autoscaler on an existing cluster

Update an existing cluster using the

command and enable and configure the cluster autoscaler on the node pool using the`az aks update`

`--enable-cluster-autoscaler`

parameter and specifying a node`--min-count`

and`--max-count`

. The following example command updates an existing AKS cluster to enable the cluster autoscaler on the node pool for the cluster and sets a minimum of one and maximum of three nodes:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3`

It takes a few minutes to update the cluster and configure the cluster autoscaler settings.


### Disable the cluster autoscaler on a cluster

Disable the cluster autoscaler using the

command and the`az aks update`

`--disable-cluster-autoscaler`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-cluster-autoscaler`

Nodes aren't removed when the cluster autoscaler is disabled.


Note

You can manually scale your cluster after disabling the cluster autoscaler using the [ az aks scale](/en-us/cli/azure/aks#az-aks-scale) command. If you use the horizontal pod autoscaler, it continues to run with the cluster autoscaler disabled, but pods might end up unable to be scheduled if all node resources are in use.

### Re-enable the cluster autoscaler on a cluster

You can re-enable the cluster autoscaler on an existing cluster using the [ az aks update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.## Use the cluster autoscaler on node pools

### Use the cluster autoscaler on multiple node pools

You can use the cluster autoscaler with [multiple node pools](create-node-pools) and can enable the cluster autoscaler on each individual node pool and pass unique autoscaling rules to them.

Update the settings on an existing node pool using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


### Disable the cluster autoscaler on a node pool

Disable the cluster autoscaler on a node pool using the

command and the`az aks nodepool update`

`--disable-cluster-autoscaler`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --disable-cluster-autoscaler`


### Re-enable the cluster autoscaler on a node pool

You can re-enable the cluster autoscaler on a node pool using the [ az aks nodepool update](https://github.com/Azure/azure-cli-extensions/tree/master/src/aks-preview#enable-cluster-auto-scaler-for-a-node-pool) command and specifying the

`--enable-cluster-autoscaler`

, `--min-count`

, and `--max-count`

parameters.Note

If you plan on using the cluster autoscaler with node pools that span multiple zones and leverage scheduling features related to zones, such as volume topological scheduling, we recommend you have one node pool per zone and enable `--balance-similar-node-groups`

through the autoscaler profile. This ensures the autoscaler can successfully scale up and keep the sizes of the node pools balanced.

## Update the cluster autoscaler settings

As your application demands change, you might need to adjust the cluster autoscaler node count to scale efficiently.

Change the node count using the

command and update the cluster autoscaler using the`az aks update`

`--update-cluster-autoscaler`

parameter and specifying your updated node`--min-count`

and`--max-count`

.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

The cluster autoscaler enforces the minimum count in cases where the actual count drops below the minimum due to external factors, such as during a spot eviction or when changing the minimum count value from the AKS API.

## Use the cluster autoscaler profile

You can configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile. For example, a scale down event happens after nodes are under-utilized after 10 minutes. If you have workloads that run every 15 minutes, you might want to change the autoscaler profile to scale down under-utilized nodes after 15 or 20 minutes. When you enable the cluster autoscaler, a default profile is used unless you specify different settings.

Important

The cluster autoscaler profile affects **all node pools** that use the cluster autoscaler. You can't set an autoscaler profile per node pool. When you set the profile, any existing node pools with the cluster autoscaler enabled immediately start using the profile.

### Cluster autoscaler profile settings

The following table lists the available settings for the cluster autoscaler profile:

| Setting | Description | Default value |
|---|---|---|
`scan-interval` |
How often the cluster is reevaluated for scale up or down. | 10 seconds |
`scale-down-delay-after-add` |
How long after scale up that scale down evaluation resumes. | 10 minutes |
`scale-down-delay-after-delete` |
How long after node deletion that scale down evaluation resumes. | `scan-interval` |
`scale-down-delay-after-failure` |
How long after scale down failure that scale down evaluation resumes. | Three minutes |
`scale-down-unneeded-time` |
How long a node should be unneeded before it's eligible for scale down. | 10 minutes |
`scale-down-unready-time` |
How long an unready node should be unneeded before it's eligible for scale down. | 20 minutes |
`ignore-daemonsets-utilization` |
Whether DaemonSet pods will be ignored when calculating resource utilization for scale down. | `false` |
`daemonset-eviction-for-empty-nodes` |
Whether DaemonSet pods will be gracefully terminated from empty nodes. | `false` |
`daemonset-eviction-for-occupied-nodes` |
Whether DaemonSet pods will be gracefully terminated from non-empty nodes. | `true` |
`scale-down-utilization-threshold` |
The maximum value between the sum of CPU requests and sum of Memory requests of all pods running on the node divided by node's corresponding allocatable resource, below which a node can be considered for scale down. | 0.5 |
`max-graceful-termination-sec` |
Maximum number of seconds the cluster autoscaler waits for pod termination when trying to scale down a node. | 600 seconds |
`balance-similar-node-groups` |
Detects similar node pools and balances the number of nodes between them. | `false` |
`expander` |
Type of node pool
`most-pods` , `random` , `least-waste` , and `priority` . |

`random`

`skip-nodes-with-local-storage`

`true`

, cluster autoscaler doesn't delete nodes with pods with local storage, for example, EmptyDir or HostPath.`false`

`skip-nodes-with-system-pods`

`true`

, cluster autoscaler doesn't delete nodes with pods from kube-system (except for DaemonSet or mirror pods).`true`

`max-empty-bulk-delete`

`new-pod-scale-up-delay`

`max-total-unready-percentage`

`max-node-provision-time`

`ok-total-unready-count`

Note

The ignore-daemonsets-utilization, daemonset-eviction-for-empty-nodes, and daemonset-eviction-for-occupied-nodes parameters are GA from API version 2024-05-01. If you are using the CLI to update these flags, please ensure you are using version 2.63 or later.

### Set the cluster autoscaler profile on a new cluster

Create an AKS cluster using the

command and set the cluster autoscaler profile using the`az aks create`

`cluster-autoscaler-profile`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 1 \ --enable-cluster-autoscaler \ --min-count 1 \ --max-count 3 \ --cluster-autoscaler-profile scan-interval=30s \ --generate-ssh-keys`


### Set the cluster autoscaler profile on an existing cluster

Set the cluster autoscaler on an existing cluster using the

command and the`az aks update`

`cluster-autoscaler-profile`

parameter. The following example configures the scan interval setting as*30s*:`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile scan-interval=30s`


### Configure cluster autoscaler profile for aggressive scale down

Note

Scaling down aggressively is not recommended for clusters experiencing frequent scale-outs and scale-ins within short intervals, as it could potentially result in extended node provisioning times under these circumstances. Increasing `scale-down-delay-after-add`

can help in these circumstances by keeping the node around longer to handle incoming workloads.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=30s,scale-down-delay-after-add=0m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=3m,scale-down-unready-time=3m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=1000,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Configure cluster autoscaler profile for bursty workloads

```
az aks update \
--resource-group "myResourceGroup" \
--name myAKSCluster \
--cluster-autoscaler-profile scan-interval=20s,scale-down-delay-after-add=10m,scale-down-delay-after-failure=1m,scale-down-unneeded-time=5m,scale-down-unready-time=5m,max-graceful-termination-sec=30,skip-nodes-with-local-storage=false,max-empty-bulk-delete=100,max-total-unready-percentage=100,ok-total-unready-count=1000,max-node-provision-time=15m
```


### Reset cluster autoscaler profile to default values

Reset the cluster autoscaler profile using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --cluster-autoscaler-profile ""`


## Retrieve cluster autoscaler logs and status

You can retrieve logs and status updates from the cluster autoscaler to help diagnose and debug autoscaler events. AKS manages the cluster autoscaler on your behalf and runs it in the managed control plane. You can enable control plane node to see the logs and operations from the cluster autoscaler.

Set up a rule for resource logs to push cluster autoscaler logs to Log Analytics using the

[instructions here](monitor-aks#aks-control-plane-resource-logs). Make sure you check the box for`cluster-autoscaler`

when selecting options for**Logs**.Select the

**Log**section on your cluster.Enter the following example query into Log Analytics:

`AzureDiagnostics | where Category == "cluster-autoscaler"`

View cluster autoscaler scale-up not triggered events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,reason=NotTriggerScaleUp`

View cluster autoscaler warning events on CLI.

`kubectl get events --field-selector source=cluster-autoscaler,type=Warning`

The cluster autoscaler also writes out the health status to a

`configmap`

named`cluster-autoscaler-status`

. You can retrieve these logs using the following`kubectl`

command:`kubectl get configmap -n kube-system cluster-autoscaler-status -o yaml`


For more information, see the [Kubernetes/autoscaler GitHub project FAQ](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#ca-doesnt-work-but-it-used-to-work-yesterday-why).

## Cluster Autoscaler Metrics

You can enable [control plane metrics (Preview)](monitor-control-plane-metrics) to see the logs and operations from the [cluster autoscaler](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)

## Next steps

This article showed you how to automatically scale the number of AKS nodes. You can also use the horizontal pod autoscaler to automatically adjust the number of pods that run your application. For steps on using the horizontal pod autoscaler, see [Scale applications in AKS](tutorial-kubernetes-scale).

To further help improve cluster resource utilization and free up CPU and memory for other pods, see [Vertical Pod Autoscaler](vertical-pod-autoscaler).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-aksnodeclass -->

# Configure AKSNodeClass resources for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure `AKSNodeClass`

resources to define Azure-specific settings for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using Karpenter. `AKSNodeClass`

allows you to customize various aspects of the nodes that Karpenter provisions, such as the virtual machine (VM) image, operating system (OS) disk size, maximum pods per node, and kubelet configurations.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview of AKSNodeClass resources

`AKSNodeClass`

resources enable you to configure Azure-specific settings for NAP. Each [ NodePool resource](node-auto-provisioning-node-pools) must reference an

`AKSNodeClass`

using `spec.template.spec.nodeClassRef`

. You can have multiple `NodePools`

that point to the same `AKSNodeClass`

, allowing you to share common Azure configurations across different node pools.## Image family configuration

The `imageFamily`

field dictates the default VM image and bootstrapping logic for nodes provisioned through the `AKSNodeClass`

. If you don't specify an image family, the default is `Ubuntu2204`

. GPUs are supported with both image families on compatible VM sizes.

### Supported image families

: Ubuntu 22.04 Long Term Support (LTS) is the default Linux distribution for AKS nodes.`Ubuntu`

: Azure Linux is Microsoft's alternative Linux distribution for AKS workloads. For more information, see the`AzureLinux`

[Azure Linux documentation](/en-us/azure/aks/use-azure-linux)

#### Example image family configuration

The following example configures the `AKSNodeClass`

to use the `AzureLinux`

image family:

```
spec:
imageFamily: AzureLinux
```


#### FIPS compliant node image configuration

You can enable Federal Information Process Standard (FIPS) compliant node images also. For more in FIPS in AKS, visit our [FIPS documentation](enable-fips-nodes)

The `fipsMode`

field is set by default to Disabled, and can be set to the following options:

- FIPS - select FIPS-compliant node images
- Disabled - do not use FIPS-compliant node images

The following example configures the 'AKSNodeClass' to select FIPS-compliant node images by setting `fipsMode`

to `FIPS`

:

```
spec:
fipsMode: FIPS
```


## Virtual network (VNet) subnet configuration

The `vnetSubnetID`

field specifies which Azure VNet subnet should be used for provisioning node network interfaces. This field is optional. If you don't specify a subnet, NAP uses the default subnet configured during Karpenter installation. For more information, see [Subnet configurations for NAP](node-auto-provisioning-networking#subnet-configurations-for-nap).

### Example subnet configuration

The subnet ID must be in the full Azure Resource Manager (ARM) format, as shown in the following example:

```
spec:
vnetSubnetID: "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Network/virtualNetworks/{vnet-name}/subnets/{subnet-name}"
```


## OS disk size configuration

The `osDiskSizeGB`

field specifies the size of the OS disk in gigabytes. The default value is 128 GB, and the minimum value is 30 GB.

Consider larger OS disk sizes for workloads that:

- Store significant data locally.
- Require extra space for container images.
- Have high disk I/O requirements.

### Example OS disk size configuration

```
spec:
osDiskSizeGB: 256 # 256 GB OS disk
```


## Ephemeral OS disk configuration

NAP automatically uses [Ephemeral OS disks](/en-us/azure/virtual-machines/ephemeral-os-disks) when available and suitable for the requested disk size. Ephemeral OS disks provide better performance and lower cost compared to managed disks.

### Ephemeral disk selection criteria

The system automatically chooses Ephemeral disks in the following scenarios:

- The VM instance type supports Ephemeral OS disks.
- The Ephemeral disk capacity is greater than or equal to the requested
`osDiskSizeGB`

. - The VM has sufficient ephemeral storage capacity.

If these conditions aren't met, the system falls back to using managed disks.

### Ephemeral disk types and prioritization

Azure VMs can have different types of ephemeral storage. The system uses the following priority order:

**NVMe disks**(highest performance)**Cache disks**(balanced performance)**Resource disks**(basic performance)

### Example ephemeral disk configuration

You can use node pool requirements to ensure nodes have sufficient ephemeral disk capacity, as shown in the following example:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: ephemeral-disk-pool
spec:
template:
spec:
requirements:
- key: karpenter.azure.com/sku-storage-ephemeralos-maxsize
operator: Gt
values: ["128"] # Require ephemeral disk larger than 128 GB
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: my-node-class
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: my-node-class
spec:
osDiskSizeGB: 128 # This will use ephemeral disk if available and large enough
```


This configuration ensures that only VM instance types with ephemeral disks larger than 128 GB are selected, guaranteeing ephemeral disk usage for the specified OS disk size.

## Maximum pods configuration

The `maxPods`

field specifies the maximum number of pods that can be scheduled on a node. This setting affects both cluster density and network configuration.

The minimum value for `maxPods`

is 10, and the maximum value is 250.

### Default behavior for `maxPods`


The default behavior for `maxPods`

depends on the network plugin configuration. The following table summarizes the defaults:

| Network plugin configuration | Default `maxPods` per node |
|---|---|
| Azure CNI with standard networking (v1 or NodeSubnet) | 30 |
| Azure CNI with overlay networking | 250 |
| None (no network plugin) | 250 |
| Other configurations | 110 (standard Kubernetes default) |

### Example maximum pods configuration

```
spec:
maxPods: 50 # Allow up to 50 pods per node
```


## LocalDNS configuration

LocalDNS deploys a node level DNS proxy that resolves DNS queries closer to workloads, reducing query latency and improving resiliency during transient DNS disruptions. For more information, see the [LocalDNS documentation](localdns-custom). By default, LocalDNS is set to Disabled and can be configured to the following options:

`Disabled`

(default) - Disables the LocalDNS feature. DNS queries aren't resolved locally on the node.`Preferred`

- AKS manages LocalDNS enablement based on the Kubernetes version of the node pool. The configuration is always validated and included, but LocalDNS isn't enabled unless the correct Kubernetes version is used.`Required`

- LocalDNS is enforced on the node pool if all prerequisites are satisfied. If the requirements aren't met, the deployment fails.

### Example LocalDNS configuration

You can customize LocalDNS configurations such as `vnetDNSOverrides`

and `kubeDNSOverrides`

. For more details on the supported plugins, see [Customize LocalDNS](localdns-custom).

```
spec:
LocalDNS:
mode: Required
vnetDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: VnetDNS
forwardPolicy: Random
maxConcurrent: 80
protocol: ForceTCP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "100s"
- zone: "cluster.local"
cacheDuration: "40s"
forwardDestination: VnetDNS
forwardPolicy: Sequential
maxConcurrent: 70
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
kubeDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: ClusterCoreDNS
forwardPolicy: RoundRobin
maxConcurrent: 100
protocol: PreferUDP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "60s"
- zone: "cluster.local"
cacheDuration: "10s"
forwardDestination: ClusterCoreDNS
forwardPolicy: Sequential
maxConcurrent: 50
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
```


## Kubelet configuration

The `kubelet`

section allows you to configure various kubelet parameters that affect node behavior. These parameters are typical kubelet arguments, so the Azure provider simply passes them through to the kubelet on the node.

Important

**Configure kubelet settings carefully**, and test any changes in nonproduction environments first.

### CPU management

The following settings control CPU management behavior for the kubelet:

```
spec:
kubelet:
cpuManagerPolicy: "static" # or "none"
cpuCFSQuota: true
cpuCFSQuotaPeriod: "100ms"
```


`cpuManagerPolicy`

: Controls how the kubelet allocates CPU resources. Set to`"static"`

for CPU pinning in latency-sensitive workloads.`cpuCFSQuota`

: Enables CPU Completely Fair Scheduler (CFS) quota enforcement for containers that specify CPU limits.`cpuCFSQuotaPeriod`

: Sets the CPU CFS quota period.

### Image garbage collection

The following settings control image garbage collection behavior for the kubelet:

```
spec:
kubelet:
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
```


These settings control when the kubelet performs garbage collection of container images:

`imageGCHighThresholdPercent`

: Disk usage percentage that triggers image garbage collection.`imageGCLowThresholdPercent`

: Target disk usage percentage after garbage collection.

### Topology management

The following setting controls the topology manager policy for the kubelet:

```
spec:
kubelet:
topologyManagerPolicy: "best-effort" # none, restricted, best-effort, single-numa-node
```


The topology manager helps coordinate resource allocation for latency-sensitive workloads across CPU and device (like GPU) resources.

### System configuration

The following settings allow you to configure extra system parameters for the kubelet:

```
spec:
kubelet:
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
containerLogMaxSize: "50Mi"
containerLogMaxFiles: 5
podPidsLimit: 4096
```


`allowedUnsafeSysctls`

: List of permitted unsafe sysctls that pods can use.`containerLogMaxSize`

: Maximum size of container log files before rotation.`containerLogMaxFiles`

: Maximum number of container log files to retain.`podPidsLimit`

: Maximum number of processes allowed in any pod.

## Azure resource tags configuration

You can specify Azure resource tags that apply to all VM instances created using a particular `AKSNodeClass`

resource. Tags are useful for cost tracking, resource organization, and compliance requirements.

### Tag limitations

- Azure resource tags have a limit of 50 tags per resource.
- Tag names are case-insensitive but tag values are case-sensitive.
- Azure reserves some tag names that can't be used. For more information, see
[Tag guidance and limits](/en-us/azure/azure-resource-manager/management/tag-resources#tag-restrictions).

### Example tags configuration

```
spec:
tags:
Environment: "production"
Team: "platform"
Application: "web-service"
CostCenter: "engineering"
```


## Comprehensive `AKSNodeClass`

configuration example

The following example demonstrates a comprehensive `AKSNodeClass`

configuration that includes all the settings discussed in this article:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: comprehensive-example
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: comprehensive-example
spec:
# Image family configuration
# Default: Ubuntu
# Valid values: Ubuntu, AzureLinux
imageFamily: Ubuntu
# FIPS compliant mode - allows support for FIPS-compliant node images
# Default: Disabled
# Valid values: FIPS, Disabled
fipsMode: Disabled
# LocalDNS mode - allows use of LocalDNS feature
# Default: Disabled
# Valid values: Preferred, Required, Disabled
LocalDNS:
mode: Disabled
# additional details on vnetDNSOverrides and kubeDNSOverrides can be added here
# Virtual network subnet configuration (optional)
# If not specified, uses the default --vnet-subnet-id from Karpenter installation
vnetSubnetID: "/subscriptions/12345678-1234-1234-1234-123456789012/resourceGroups/my-rg/providers/Microsoft.Network/virtualNetworks/my-vnet/subnets/my-subnet"
# OS disk size configuration
# Default: 128 GB
# Minimum: 30 GB
osDiskSizeGB: 128
# Maximum pods per node configuration
# Default behavior depends on network plugin:
# - Azure CNI with standard networking: 30 pods
# - Azure CNI with overlay networking: 250 pods
# - Other configurations: 110 pods
# Range: 10-250
maxPods: 30
# Azure resource tags (optional)
# Applied to all VM instances created with this AKSNodeClass
tags:
Environment: "production"
Team: "platform-team"
Application: "web-service"
CostCenter: "engineering"
# Kubelet configuration (optional)
# All fields are optional with sensible defaults
kubelet:
# CPU management policy
# Default: "none"
# Valid values: none, static
cpuManagerPolicy: "static"
# CPU CFS quota enforcement
# Default: true
cpuCFSQuota: true
# CPU CFS quota period
# Default: "100ms"
cpuCFSQuotaPeriod: "100ms"
# Image garbage collection thresholds
# imageGCHighThresholdPercent must be greater than imageGCLowThresholdPercent
# Range: 0-100
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
# Topology manager policy
# Default: "none"
# Valid values: none, restricted, best-effort, single-numa-node
topologyManagerPolicy: "best-effort"
# Allowed unsafe sysctls (optional)
# Comma-separated list of unsafe sysctls or patterns
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
# Container log configuration
# containerLogMaxSize default: "50Mi"
containerLogMaxSize: "50Mi"
# containerLogMaxFiles default: 5, minimum: 2
containerLogMaxFiles: 5
# Pod process limits
# Default: -1 (unlimited)
podPidsLimit: 4096
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster -->

# Tutorial - Create an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. With Azure Kubernetes Service (AKS), you can quickly create a production ready Kubernetes cluster.

In this tutorial, you deploy a Kubernetes cluster in AKS. You learn how to:

- Deploy an AKS cluster that can authenticate to an Azure Container Registry (ACR).
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

## Before you begin

In previous tutorials, you created a container image and uploaded it to an ACR instance. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- If you're using Azure CLI, this tutorial requires that you're running the Azure CLI version 2.35.0 or later. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this tutorial requires that you're running Azure PowerShell version 5.9.0 or later. Check your version with
`Get-InstalledModule -Name Az`

. To install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - If you're using Azure Developer CLI, this tutorial requires that you're running the Azure Developer CLI version 1.5.1 or later. Check your version with
`azd version`

. To install or upgrade, see[Install Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd).

## Create a Kubernetes cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. If a user is assigned multiple roles, permissions are combined. Permissions can be scoped to either a single namespace or across the whole cluster.

To learn more about AKS and Kubernetes RBAC, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra identities in AKS](azure-ad-rbac).

This tutorial requires Azure CLI version 2.35.0 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed.

## Install the Kubernetes CLI

You use the Kubernetes CLI, [ kubectl](https://kubernetes.io/docs/reference/kubectl/), to connect to your Kubernetes cluster. If you use the Azure Cloud Shell,

`kubectl`

is already installed. If you're running the commands locally, you can use the Azure CLI or Azure PowerShell to install `kubectl`

.Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`


## Create an AKS cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. Permissions are combined when users are assigned multiple roles. Permissions can be scoped to either a single namespace or across the whole cluster. For more information, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra ID in AKS](azure-ad-rbac).

For information about AKS resource limits and region availability, see [Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions).

Important

This tutorial creates a three-node cluster. To ensure your cluster operates reliably, you should run at least two nodes. A minimum of three nodes is required to use Azure Container Storage. If you get an error message when trying to create the cluster, then you might need to request a quota increase for your Azure subscription or try a different Azure region. Alternatively, you can omit the node VM size parameter to use the default VM size.

To allow an AKS cluster to interact with other Azure resources, the Azure platform automatically creates a cluster identity. In this example, the cluster identity is [granted the right to pull images](cluster-container-registry-integration) from the ACR instance you created in the previous tutorial. To execute the command successfully, you must have an **Owner** or **Azure account administrator** role in your Azure subscription.

Create an AKS cluster using the

command. The following example creates a cluster named`az aks create`

*myAKSCluster*in the resource group named*myResourceGroup*. This resource group was created in the[previous tutorial](tutorial-kubernetes-prepare-acr)in the*westus2*region. We'll continue to use the environment variable,`$ACRNAME`

, that we set in the[previous tutorial](tutorial-kubernetes-prepare-acr). If you don't have this environment variable set, set it now to the same value you used previously.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --node-vm-size standard_l8s_v3 \ --generate-ssh-keys \ --attach-acr $ACRNAME`

Note

If you already generated SSH keys, you might encounter an error similar to

`linuxProfile.ssh.publicKeys.keyData is invalid`

. To proceed, retry the command without the`--generate-ssh-keys`

parameter.

To avoid needing an **Owner** or **Azure account administrator** role, you can also manually configure a service principal to pull images from ACR. For more information, see [ACR authentication with service principals](/en-us/azure/container-registry/container-registry-auth-service-principal) or [Authenticate from Kubernetes with a pull secret](/en-us/azure/container-registry/container-registry-auth-kubernetes). Alternatively, you can use a [managed identity](use-managed-identity) instead of a service principal for easier management.

## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the AKS cluster named`az aks get-credentials`

*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify connection to your cluster using the

command, which returns a list of cluster nodes.`kubectl get nodes`

`kubectl get nodes`

The following example output shows a list of the cluster nodes:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-19366578-vmss000000 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000001 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000002 Ready agent 47h v1.30.9`


## Next step

In this tutorial, you deployed a Kubernetes cluster in AKS and configured `kubectl`

to connect to the cluster. You learned how to:

- Deploy an AKS cluster that can authenticate to an ACR.
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

In the next tutorial, you learn how to deploy Azure Container Storage on your cluster and create a generic ephemeral volume. If you're using Azure Developer CLI, or if you weren't able to use a storage optimized VM type due to quota issues, proceed directly to the [Deploy containerized application](tutorial-kubernetes-deploy-application) tutorial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni -->

# Configure Azure CNI networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Container Networking Interface (CNI) networking in Azure to create and use a virtual network subnet for an Azure Kubernetes Service (AKS) cluster. For more information on network options and considerations, see [Networking concepts for applications in Azure Kubernetes Service](/en-us/azure/aks/concepts-network).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Configure networking

For information on planning IP addresses, see [IP address planning for your Azure Kubernetes Service clusters](concepts-network-ip-address-planning).

Sign in to the

[Azure portal](https://portal.azure.com/).On the Azure portal home page, select

**Create a resource**.Under

**Categories**, select**Containers**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:- Under
**Project details**:**Subscription**: Select your Azure subscription.**Resource group**: Select**Create new**, enter a resource group name (such as**test-rg**), and then select**Ok**.

- Under
**Cluster details**:**Kubernetes cluster name**: Enter a cluster name, such as**aks-cluster**.**Region**: Select**East US 2**.


- Under
Select

**Next**>**Next**to get to the**Networking**tab.For

**Container networking**, select**Azure CNI Node Subnet**.Select

**Review + create**>**Create**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-uninstall-add-on -->

# Uninstall the Open Service Mesh (OSM) add-on from your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to uninstall the OMS add-on and related resources from your AKS cluster.

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

## Disable the OSM add-on from your cluster

Disable the OSM add-on from your cluster using the

command and the`az aks disable-addon`

`--addons`

parameter.`az aks disable-addons \ --resource-group myResourceGroup \ --name myAKSCluster \ --addons open-service-mesh`


## Remove OSM resources

Uninstall the remaining resources on the cluster using the

`osm uninstall cluster-wide-resources`

command.`osm uninstall cluster-wide-resources`

Note

For version 1.1, the command is

`osm uninstall mesh --delete-cluster-wide-resources`

Important

You must remove these additional resources after you disable the OSM add-on. Leaving these resources on your cluster may cause issues if you enable the OSM add-on again in the future.


## Next steps

Learn more about [Open Service Mesh](open-service-mesh-about).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operate-cost-optimized-scale -->

# Operate cost-optimized Azure Kubernetes Service (AKS) at scale

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to operate cost optimized Azure Kubernetes Service (AKS) at scale.

## Azure Kubernetes Fleet Manager (Kubernetes Fleet)

[Azure Kubernetes Fleet Manager (Kubernetes Fleet)](/en-us/azure/kubernetes-fleet/overview) enables at-scale management of multiple AKS clusters. You can create a *Fleet resource* and use it to manage multiple clusters as a single entity, orchestrate updates across multiple clusters, and propagate Kubernetes resources across multiple clusters. When creating a new *Fleet resource*, you can create it with or without a *hub cluster*. A *hub cluster* is a managed AKS cluster that acts a hub to store and propagate Kubernetes resources.


Kubernetes Fleet can help you reduce the management overhead cost of operating multiple clusters by providing a single entry point for managing multiple clusters. For more information, see the [Azure Kubernetes Fleet Manager documentation](/en-us/azure/kubernetes-fleet/).

### Resource propagation

Kubernetes Fleet provides *resource propagation* to enable at-scale management of Kubernetes resources. You can create Kubernetes resources in the *hub cluster* and propagate them to specified *member clusters* using the `MemberCluster`

and `ClusterResourcePlacement`

custom resources.


For more information, see [Kubernetes Fleet resource placement from hub cluster to member clusters](/en-us/azure/kubernetes-fleet/concepts-resource-propagation).

### Intelligent resource placement

Kubernetes Fleet provides *intelligent resource placement*, which can make scheduling decisions based on node count, cost of compute/memory in target member clusters, and resource availability in target member clusters. This allows you to place workloads in the most cost-effective member cluster based on your workload requirements.


For more information, see [Intelligent cross-cluster Kubernetes resource placement using Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/intelligent-resource-placement).

## AKS Automatic

[AKS Automatic](intro-aks-automatic) offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of cluster setup, including node management, scaling, and security, and preconfigures settings that follow AKS well-architected recommendations.

AKS Automatic clusters are designed to help reduce management overhead costs of creating cluster templates, managing the cluster lifecycle, guardrails, and updates. Scaling is seamless and dynamic. Nodes are created based on workload requests using [node autoprovisioning (NAP)](node-autoprovision) and workloads are automatically scaled with features like Horizontal Pod Autoscaler (HPA), [Kubernetes Event Driven Autoscaling (KEDA)](keda-about), and [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler).

## Azure Advisor cost recommendations

AKS cost recommendations in Azure Advisor provide recommendations to help you achieve cost-efficiency without sacrificing reliability. Advisor analyzes your resource configurations and recommends optimization solutions. For more information, see [Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor](cost-advisors).

## Next steps

To learn more about cost optimization in Azure Kubernetes Service (AKS), see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deployment-safeguards -->

# Use Deployment Safeguards to enforce best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Deployment Safeguards to enforce best practices on an Azure Kubernetes Service (AKS) cluster.

## Overview

Note

Deployment Safeguards is turned on by default in AKS Automatic.

Throughout the development lifecycle, it is common for bugs, issues, and other problems to arise if the initial deployment of your Kubernetes resources includes misconfigurations. To ease the burden of Kubernetes development, Azure Kubernetes Service (AKS) offers Deployment Safeguards. Deployment Safeguards enforce Kubernetes best practices in your AKS cluster through Azure Policy controls.

Deployment Safeguards offer two levels of configuration:

`Warn`

: Displays warning messages in the code terminal to alert you of any noncompliant cluster configurations but still allows the request to go through.`Enforce`

: Enforces compliant configurations by denying and mutating deployments if they don't follow best practices.

After you configure Deployment Safeguards for 'Warn' or 'Enforce', Deployment Safeguards programmatically assess your Kubernetes resources at creation or update time for compliance. Deployment Safeguards also display aggregated compliance information across your workloads at a per resource level via Azure Policy's compliance dashboard in the [Azure portal](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Compliance) or in your CLI or terminal. Running a noncompliant workload indicates that your cluster is not following best practices and that workloads on your cluster are at risk of experiencing issues caused by your cluster configuration.

## Prerequisites

Note

Cluster admins don't need Azure Policy permissions to enable or disable Deployment Safeguards. However, it's required to have the Azure Policy add-on installed.

- You need to enable the Azure Policy add-on for AKS. For more information, see
[Enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks). This includes registering the`Microsoft.PolicyInsights`

resource provider in your subscription.

## Deployment Safeguards policies

The following table lists the policies that become active and the Kubernetes resources they target when you enable Deployment Safeguards. You can view the [currently available Deployment Safeguards](https://portal.azure.com/#view/Microsoft_Azure_Policy/InitiativeDetail.ReactView/id/%2Fproviders%2FMicrosoft.Authorization%2FpolicySetDefinitions%2Fc047ea8e-9c78-49b2-958b-37e56d291a44/scopes/) in the Azure portal as an Azure Policy definition or at [Azure Policy built-in definitions for Azure Kubernetes Service](/en-us/azure/aks/policy-reference#policy-definitions). The intention behind this collection is to create a common and generic list of best practices applicable to most users and use cases.

| Deployment safeguard policy | Mutation outcome if available |
|---|---|
| Cannot Edit Individual Nodes | N/A |
| Kubernetes cluster containers CPU and memory resource limits shouldn't exceed the specified limits | Sets CPU resource limits to 500m if not set and sets memory limits to 500Mi if no path is present |
| Must Have Anti Affinity Rules or topologySpreadConstraintsSet | N/A |
| No AKS Specific Labels | N/A |
| Kubernetes cluster containers should only use allowed images | N/A |
| Reserved System Pool Taints | Removes the `CriticalAddonsOnly` taint from a user node pool if not set. AKS uses the `CriticalAddonsOnly` taint to keep customer pods away from the system pool. This configuration ensures a clear separation between AKS components and customer pods and prevents eviction of customer pods that don't tolerate the `CriticalAddonsOnly` taint. |
| Ensure cluster containers have readiness or liveness probes configured | N/A |
| Kubernetes clusters should use Container Storage Interface (CSI) driver StorageClass | N/A |
| Kubernetes cluster services should use unique selectors | N/A |
| Kubernetes cluster container images should not include latest image tag | N/A |

If you want to submit an idea or request for Deployment Safeguards, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

## Pod Security Standards in Deployment Safeguards

Note

Baseline Pod Security Standards are now turned on by default in AKS Automatic. The baseline Pod Security Standards in AKS Automatic can't be turned off.

Deployment Safeguards also supports the ability to turn on [Baseline, Restricted and Privileged Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/). To ensure your workloads deploy successfully, make sure each manifest complies with the Baseline or Restricted Pod Security requirements. By default, Azure Kubernetes Service uses Privileged Pod Security Standards.

| Policy | Error Message | Fix |
|---|---|---|
| AppArmor | `AppArmor annotation values must be undefined/nil, runtime/default, or localhost/*` or `AppArmor profile type must be one of: undefined/nil, RuntimeDefault, or Localhost` |
Remove any specification of AppArmor. Kubernetes by default applies apparmor settings. "On supported hosts, the RuntimeDefault AppArmor profile is applied by default". |
| Host Namespaces | `Host network namespaces are disallowed: spec.hostNetwork is set to true'` or `'Host PID namespaces are disallowed: spec.hostPID is set to true'` or `'Host IPC namespaces are disallowed: spec.hostIPC is set to true'` |
Set those values to false, or remove specifying the fields. |
| Privileged Containers | `'Privileged [ephemeral\|init\|N/A] containers are disallowed: spec.containers[*].securityContext.privileged is set to true'` |
Set the appropriate securityContext.privileged field to false, or remove the field. |
| Capabilities | Message will start with `'Disallowed capabilities detected` |
Remove the capability shown from the container's manifest. |
| HostPath volumes | `HostPath volumes are forbidden under restricted security policy unless containers mounting them are from allowed images` |
Remove the HostPath volume and volume mount. |
| Host Ports | HostPorts are forbidden under baseline security policy | Remove the host port specification from the offending container. |
| SELinux | `SELinux type must be one of: undefined/empty, container_t, container_init_t, container_kvm_t, or container_engine_t` |
Set the container's securityContext.seLinuxOptions.type field to one of the allowed values. |
| /proc Mount Type | ProcMount must be undefined/nil or 'Default' in spec.containers[*].securityContext.procMount | Set "* `spec.containers[*].securityContext.procMount` " to 'Default' or have it be undefined. |
| Seccomp | `Seccomp profile must not be explicitly set to Unconfined. Allowed values are: undefined/nil, RuntimeDefault, or Localhost` |
Set `securityContext.seccompProfile.type` on the pod or containers to one of the allowed values. |
| Sysctls | `Disallowed sysctl detected. Only baseline Kubernetes pod security standard sysctls are permitted` |
Remove the disallowed systctls( see the
|

`Only the following volume types are allowed under restricted policy: configMap, csi, downwardAPI, emptyDir, ephemeral, persistentVolumeClaim, projected, secret`

`Privilege escalation must be set to false under restricted policy`

`* `

spec.containers[*].securityContext.allowPrivilegeEscalation`` must explicitly be set to false for each container, initContainer, and ephemeralContainer.`Containers must not run as root user in spec.containers[*].securityContext.runAsNonRoot`

`'Containers must not run as root user: spec.securityContext.runAsUser is set to 0'`

`Seccomp profile must be "RuntimeDefault" or "Localhost" under restricted policy`

`securityContext.seccompProfile.type`

on the pod or containers to one of the allowed values. This differs from the baseline in the fact that the restricted policy doesn't allow an undefined value.`All containers must drop ALL capabilities under restricted policy`

or `Only NET_BIND_SERVICE may be added to capabilities under restricted policy`

## Enable Deployment Safeguards

Note

Using the Deployment Safeguards `Enforce`

level means you're opting in to deployments being blocked and mutated. Consider how these policies might work with your AKS cluster before enabling `Enforce`

.

### Enable Deployment Safeguards on an existing cluster

Enable Deployment Safeguards on an existing cluster that has the Azure Policy add-on enabled using the `az aks safeguard create`

command with the `--level`

flag. If you want to receive noncompliance warnings, set the `--level`

to `Warn`

. If you want to deny or mutate all noncompliant deployments, set it to `Enforce`

.

```
az aks safeguards create --resource-group <resource-group-name> --name <cluster-name> --level Enforce
```


You can also enable Deployment Safeguards by using the `--cluster`

flag and specifying the cluster resource ID.

```
az aks safeguards create --cluster <ID> --level Enforce
```


If you want to update the Deployment Safeguards level of an existing cluster, run the following command with the new value for `--level`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn
```


### Excluding namespaces

You can also exclude certain namespaces from Deployment Safeguards. When you exclude a namespace, activity in that namespace is unaffected by Deployment Safeguards warnings or enforcement.

For example, to exclude the namespaces `ns1`

and `ns2`

, use a space separated list of namespaces with the `--excluded-ns`

flag, as shown in the following example:

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --excluded-ns ns1 ns2
```


### Turn on Pod Security Standards

Note

Azure Kubernetes Service (AKS) uses `Privileged`

Pod Security Standards by default. If you want to revert to the default configuration, set the `--pss-level`

flag to `Privileged`

.

To enable Pod Security Standards in Deployment Safeguards, use the `--pss-level`

flag to select one of the following levels: `Baseline`

, `Restricted`

, or `Privileged`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --pss-level <Baseline|Restricted|Privileged>
```


### Update your Deployment Safeguard version

Deployment Safeguards adhere to the [AKS addon versioning scheme](supported-kubernetes-versions). Each new version of a Deployment Safeguard will be released as a new minor version in AKS. These updates will be communicated through the [AKS GitHub release notes](https://github.com/Azure/AKS/releases) and reflected in the "Deployment Safeguards Policies" table in our documentation.

To learn more about AKS versioning and addons, refer to the following documentation: [aks-component-versions](supported-kubernetes-versions) and [aks-versioning-for-addons](integrations#add-ons).

## Verify compliance across clusters

After deploying your Kubernetes manifest, you see warnings or a potential denial message in your CLI or terminal if the cluster isn't compliant with Deployment Safeguards, as shown in the following examples:

**Warn**

```
$ kubectl apply -f deployment.yaml
Warning: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
deployment.apps/simple-web created
```


**Enforce**

With Deployment Safeguard mutations, the `Enforce`

level mutates your Kubernetes resources when applicable. However, your Kubernetes resources still need to pass all safeguards to deploy successfully. If any safeguard policies fail, your resource is denied and won't be deployed.

```
$ kubectl apply -f deployment.yaml
Error from server (Forbidden): error when creating "deployment.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
```


If your Kubernetes resources comply with the applicable mutation safeguards and meet all other safeguard requirements, they'll be successfully deployed, as shown in the following example:

```
$ kubectl apply -f deployment.yaml
deployment.apps/simple-web created
```


## Verify compliance across clusters using the Azure Policy dashboard

To verify Deployment Safeguards have been applied and to check on your cluster's compliance, navigate to the Azure portal page for your cluster and select **Policies**, then select **go to Azure Policy**.

From the list of policies and initiatives, select the initiative associated with Deployment Safeguards. You see a dashboard showing compliance state across your AKS cluster.

Note

To properly assess compliance across your AKS cluster, the Azure Policy initiative must be scoped to your cluster's resource group.

## Disable Deployment Safeguards

To disable Deployment Safeguards on your cluster, use the `delete`

command.

```
az aks safeguards delete --resource-group <resource-group-name> --name <cluster-name>
```


## FAQ

#### Can I create my own mutations?

No. If you have an idea for a safeguard, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

#### Can I pick and choose which mutations I want in Enforcement?

No. Deployment Safeguards is all or nothing. Once you turn on Warn or Enforce, all safeguards are active.

#### Why did my deployment resource get admitted even though it wasn't following best practices?

Deployment Safeguards enforce best practice standards through Azure Policy controls and has policies that validate against Kubernetes resources. To evaluate and enforce cluster components, Azure Policy extends [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/). Gatekeeper enforcement also currently operates in a [ fail-open model](https://open-policy-agent.github.io/gatekeeper/website/docs/failing-closed/#considerations). As there's no guarantee that Gatekeeper responds to our networking call, we make sure that in that case, the validation is skipped so that the deny doesn't block your deployments.

To learn more, see [workload validation in Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/workload-resources/).

## Next steps

- Learn more about
[best practices](best-practices)for operating an AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-custom -->

# Customize CoreDNS for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses [CoreDNS](https://coredns.io/) for cluster DNS management and resolution with all *1.12.x* and higher clusters. AKS is a managed service, so you can't modify the main configuration for CoreDNS (a *CoreFile*). Instead, you use a Kubernetes *ConfigMap* to override the default settings. To see the default AKS CoreDNS ConfigMaps, use the `kubectl get configmaps --namespace=kube-system coredns --output yaml`

command.

This article shows you how to use ConfigMaps for basic CoreDNS customization options in Azure Kubernetes Service (AKS).

Note

Previously, AKS used `kube-dns`

for cluster DNS management and resolution, but it's now deprecated. `kube-dns`

offered different [customization options](https://www.danielstechblog.io/using-custom-dns-server-for-domain-specific-name-resolution-with-azure-kubernetes-service/) via a Kubernetes config map. CoreDNS is **not** backwards compatible with `kube-dns`

. You must update any previous customizations to work with CoreDNS.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Verify the version of CoreDNS you're running. The configuration values might change between versions.

## Plugin support

All built-in CoreDNS plugins are supported. No add-on/third party plugins are supported.

Important

When you create configurations like the ones in this article, the names you specify in the `data`

section must end in `.server`

or `.override`

. This naming convention is defined in the default AKS CoreDNS ConfigMap, which you can view using the `kubectl get configmaps --namespace=kube-system coredns --output yaml`

command.

## Configure DNS name rewrites

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to replace`<domain to be rewritten>`

with your own fully qualified domain name (FQDN).`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | <domain to be rewritten>.com:53 { log errors rewrite stop { name regex (.*)\.<domain to be rewritten>\.com {1}.default.svc.cluster.local answer name (.*)\.default\.svc\.cluster\.local {1}.<domain to be rewritten>.com } forward . /etc/resolv.conf # You can redirect this to a specific DNS server such as 10.0.0.10, but that server must be able to resolve the rewritten domain name }`

Important

If you redirect to a DNS server, such as the CoreDNS service IP, that DNS server must be able to resolve the rewritten domain name.

Create the ConfigMap using the

command and specify the name of your YAML manifest.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Verify the customizations were applied using the

command.`kubectl get configmaps`

`kubectl get configmaps --namespace=kube-system coredns-custom -o yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Specify a forward server for your network traffic

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to replace the`forward`

name and`<domain to be rewritten>`

with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | # You can select any name here, but it must end with the .server file extension <domain to be rewritten>.com:53 { forward foo.com 1.1.1.1 }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Use custom domains

You might want to configure custom domains that can only be resolved internally. For example, you might want to resolve the custom domain *puglife.local*, which isn't a valid top-level domain. Without a custom domain ConfigMap, the AKS cluster can't resolve the address.

Create a new file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to update the custom domain and IP address with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: puglife.server: | # You can select any name here, but it must end with the .server file extension puglife.local:53 { errors cache 30 forward . 192.11.0.1 # This is my test/dev DNS server }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Configure stub domains

Create a file named

`corednsms.yaml`

and paste the following example configuration. Make sure to update the custom domains and IP addresses with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: test.server: | # You can select any name here, but it must end with the .server file extension abc.com:53 { errors cache 30 forward . 1.2.3.4 } my.cluster.local:53 { errors cache 30 forward . 2.3.4.5 }`

Create the ConfigMap using the

command and specify.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Add custom host-to-IP mappings

Create a file named

`corednsms.yaml`

and paste the following example configuration. Make sure to update the IP addresses and hostnames with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom # This is the name of the ConfigMap you can overwrite with your changes namespace: kube-system data: test.override: | # You can select any name here, but it must end with the .override file extension hosts { 10.0.0.1 example1.org 10.0.0.2 example2.org 10.0.0.3 example3.org fallthrough }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Next steps

- To troubleshoot CoreDNS issues, see
[Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)](coredns-troubleshoot). - To learn about CoreDNS autoscaling behavior, see
[Autoscaling CoreDNS in Azure Kubernetes Service (AKS)](coredns-autoscale).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/load-balancer-standard -->

# Use a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Load Balancer](/en-us/azure/load-balancer/load-balancer-overview) operates at layer 4 of the Open Systems Interconnection (OSI) model that supports both inbound and outbound scenarios. It distributes inbound flows that arrive at the load balancer's front end to the back end pool instances.

A **public** load balancer integrated with AKS serves two purposes:

- Provide outbound connections to the cluster nodes inside the AKS virtual network (VNet) by translating the private IP address to a public IP address part of its
*outbound pool*. - Provide access to applications via Kubernetes services of type
`LoadBalancer`

, enabling you to easily scale your applications and create highly available services.

This article covers integration with a public load balancer on AKS. For internal load balancer integration, see [Use an internal load balancer in AKS](internal-lb).

## Prerequisites

- Azure Load Balancer is available in two SKUs:
*Basic*and*Standard*. The*Standard*SKU is used by default when you create an AKS cluster. The*Standard*SKU gives you access to added functionality, such as a larger backend pool,[multiple node pools](create-node-pools),[Availability Zones](availability-zones), and is[secure by default](/en-us/azure/load-balancer/load-balancer-overview#securebydefault). It's the recommended load balancer SKU for AKS. For more information on the*Basic*and*Standard*SKUs, see[Azure Load Balancer SKU comparison](/en-us/azure/load-balancer/skus). - For a full list of the supported annotations for Kubernetes services with type
`LoadBalancer`

, see[LoadBalancer annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations). - This article assumes you have an AKS cluster with the
*Standard*SKU Azure Load Balancer. If you need an AKS cluster, you can create one using[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal).

Important

If you'd prefer to use your own gateway, firewall, or proxy to provide outbound connection, you can skip the creation of the load balancer outbound pool and respective frontend IP by using [ outbound type as UserDefinedRouting (UDR)](egress-outboundtype). The outbound type defines the egress method for a cluster and defaults to type

`LoadBalancer`

.## Limitations

The following limitations apply when you create and manage AKS clusters that support a load balancer with the *Standard* SKU:

AKS manages the lifecycle and operations of agent nodes. Modifying the IaaS resources associated with the agent nodes isn't supported. An example of an unsupported operation is making manual changes to the load balancer resource group.

At least one public IP or IP prefix is required for allowing egress traffic from the AKS cluster. The public IP or IP prefix is required to maintain connectivity between the control plane and agent nodes and to maintain compatibility with previous versions of AKS. You have the following options for specifying public IPs or IP prefixes with a

*Standard*SKU load balancer:- Provide your own public IPs.
- Provide your own public IP prefixes.
- Specify a number up to 100 to allow the AKS cluster to create that many
*Standard*SKU public IPs in the same resource group as the AKS cluster. This resource group is usually named with`MC_`

at the beginning. AKS assigns the public IP to the*Standard*SKU load balancer. By default, one public IP is automatically created in the same resource group as the AKS cluster if no public IP, public IP prefix, or number of IPs is specified. You also must allow public addresses and avoid creating any Azure policies that ban IP creation.

A public IP created by AKS can't be reused as a custom bring your own (BYO) public IP address. You must create and manage all custom IP addresses.

You can only define the load balancer SKU when you create an AKS cluster. You can't change the load balancer SKU after an AKS cluster has been created.

You can only use one type of load balancer SKU (

*Basic*or*Standard*) in a single cluster.*Standard*SKU load balancers only support*Standard*SKU IP addresses.[Private Link Service](/en-us/azure/private-link/private-link-service-overview)isn't supported when the load balancer backend pool type is set to`nodeIP`

.

## Create a load balancer service in AKS

After you create an AKS cluster with outbound type `LoadBalancer`

(default), your cluster is ready to use the load balancer to expose services.

Create a service manifest named

`public-svc.yaml`

, which creates a public service of type`LoadBalancer`

.`apiVersion: v1 kind: Service metadata: name: public-svc spec: type: LoadBalancer ports: - port: 80 selector: app: public-app`


## Specify the load balancer IP address

If you want to use a specific IP address with the load balancer, you have two options to specify the IP address:

**Set service annotations**(recommended): Use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.**Add the**: Add the*LoadBalancerIP*property to the load balancer YAML manifest`Service.Spec.LoadBalancerIP`

property to the load balancer YAML manifest. This field is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235), and it can't support dual-stack. Current usage remains the same and existing services are expected to work without modification.

## Deploy the load balancer service manifest

Deploy the public service manifest using

and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f public-svc.yaml`

The Azure Load Balancer is configured with a new public IP that fronts the new service. Since the Azure Load Balancer can have multiple frontend IPs, each new service that you deploy gets a new dedicated frontend IP to be uniquely accessed.

Confirm your service is created and the load balancer is configured using the

`kubectl get service`

command.`kubectl get service public-svc`

When you view the service details, the public IP address created for this service on the load balancer is shown in the

*EXTERNAL-IP*column of the output. It might take a few minutes for the IP address to change from*<pending>*to an actual public IP address. The following example output shows successful creation of the service:`NAMESPACE NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE default public-svc LoadBalancer 10.0.39.110 203.0.113.187 80:32068/TCP 52s`

Get more detailed information about your service using the

`kubectl describe service`

command.`kubectl describe service public-svc`

The following example output is a condensed version of the output after you run

`kubectl describe service`

.*LoadBalancer Ingress*shows the external IP address exposed by your service.*IP*shows the internal addresses.`Name: public-svc Namespace: default Labels: <none> Annotations: <none> Selector: app=public-app ... IP: 10.0.39.110 ... LoadBalancer Ingress: 203.0.113.187 ... TargetPort: 80/TCP NodePort: 32068/TCP ... Session Affinity: None External Traffic Policy: Cluster ...`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/load-balancer-standard -->

# Use a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Load Balancer](/en-us/azure/load-balancer/load-balancer-overview) operates at layer 4 of the Open Systems Interconnection (OSI) model that supports both inbound and outbound scenarios. It distributes inbound flows that arrive at the load balancer's front end to the back end pool instances.

A **public** load balancer integrated with AKS serves two purposes:

- Provide outbound connections to the cluster nodes inside the AKS virtual network (VNet) by translating the private IP address to a public IP address part of its
*outbound pool*. - Provide access to applications via Kubernetes services of type
`LoadBalancer`

, enabling you to easily scale your applications and create highly available services.

This article covers integration with a public load balancer on AKS. For internal load balancer integration, see [Use an internal load balancer in AKS](internal-lb).

## Prerequisites

- Azure Load Balancer is available in two SKUs:
*Basic*and*Standard*. The*Standard*SKU is used by default when you create an AKS cluster. The*Standard*SKU gives you access to added functionality, such as a larger backend pool,[multiple node pools](create-node-pools),[Availability Zones](availability-zones), and is[secure by default](/en-us/azure/load-balancer/load-balancer-overview#securebydefault). It's the recommended load balancer SKU for AKS. For more information on the*Basic*and*Standard*SKUs, see[Azure Load Balancer SKU comparison](/en-us/azure/load-balancer/skus). - For a full list of the supported annotations for Kubernetes services with type
`LoadBalancer`

, see[LoadBalancer annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations). - This article assumes you have an AKS cluster with the
*Standard*SKU Azure Load Balancer. If you need an AKS cluster, you can create one using[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal).

Important

If you'd prefer to use your own gateway, firewall, or proxy to provide outbound connection, you can skip the creation of the load balancer outbound pool and respective frontend IP by using [ outbound type as UserDefinedRouting (UDR)](egress-outboundtype). The outbound type defines the egress method for a cluster and defaults to type

`LoadBalancer`

.## Limitations

The following limitations apply when you create and manage AKS clusters that support a load balancer with the *Standard* SKU:

AKS manages the lifecycle and operations of agent nodes. Modifying the IaaS resources associated with the agent nodes isn't supported. An example of an unsupported operation is making manual changes to the load balancer resource group.

At least one public IP or IP prefix is required for allowing egress traffic from the AKS cluster. The public IP or IP prefix is required to maintain connectivity between the control plane and agent nodes and to maintain compatibility with previous versions of AKS. You have the following options for specifying public IPs or IP prefixes with a

*Standard*SKU load balancer:- Provide your own public IPs.
- Provide your own public IP prefixes.
- Specify a number up to 100 to allow the AKS cluster to create that many
*Standard*SKU public IPs in the same resource group as the AKS cluster. This resource group is usually named with`MC_`

at the beginning. AKS assigns the public IP to the*Standard*SKU load balancer. By default, one public IP is automatically created in the same resource group as the AKS cluster if no public IP, public IP prefix, or number of IPs is specified. You also must allow public addresses and avoid creating any Azure policies that ban IP creation.

A public IP created by AKS can't be reused as a custom bring your own (BYO) public IP address. You must create and manage all custom IP addresses.

You can only define the load balancer SKU when you create an AKS cluster. You can't change the load balancer SKU after an AKS cluster has been created.

You can only use one type of load balancer SKU (

*Basic*or*Standard*) in a single cluster.*Standard*SKU load balancers only support*Standard*SKU IP addresses.[Private Link Service](/en-us/azure/private-link/private-link-service-overview)isn't supported when the load balancer backend pool type is set to`nodeIP`

.

## Create a load balancer service in AKS

After you create an AKS cluster with outbound type `LoadBalancer`

(default), your cluster is ready to use the load balancer to expose services.

Create a service manifest named

`public-svc.yaml`

, which creates a public service of type`LoadBalancer`

.`apiVersion: v1 kind: Service metadata: name: public-svc spec: type: LoadBalancer ports: - port: 80 selector: app: public-app`


## Specify the load balancer IP address

If you want to use a specific IP address with the load balancer, you have two options to specify the IP address:

**Set service annotations**(recommended): Use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.**Add the**: Add the*LoadBalancerIP*property to the load balancer YAML manifest`Service.Spec.LoadBalancerIP`

property to the load balancer YAML manifest. This field is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235), and it can't support dual-stack. Current usage remains the same and existing services are expected to work without modification.

## Deploy the load balancer service manifest

Deploy the public service manifest using

and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f public-svc.yaml`

The Azure Load Balancer is configured with a new public IP that fronts the new service. Since the Azure Load Balancer can have multiple frontend IPs, each new service that you deploy gets a new dedicated frontend IP to be uniquely accessed.

Confirm your service is created and the load balancer is configured using the

`kubectl get service`

command.`kubectl get service public-svc`

When you view the service details, the public IP address created for this service on the load balancer is shown in the

*EXTERNAL-IP*column of the output. It might take a few minutes for the IP address to change from*<pending>*to an actual public IP address. The following example output shows successful creation of the service:`NAMESPACE NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE default public-svc LoadBalancer 10.0.39.110 203.0.113.187 80:32068/TCP 52s`

Get more detailed information about your service using the

`kubectl describe service`

command.`kubectl describe service public-svc`

The following example output is a condensed version of the output after you run

`kubectl describe service`

.*LoadBalancer Ingress*shows the external IP address exposed by your service.*IP*shows the internal addresses.`Name: public-svc Namespace: default Labels: <none> Annotations: <none> Selector: app=public-app ... IP: 10.0.39.110 ... LoadBalancer Ingress: 203.0.113.187 ... TargetPort: 80/TCP NodePort: 32068/TCP ... Session Affinity: None External Traffic Policy: Cluster ...`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler -->

# Vertical pod autoscaling in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of using the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS), which is based on the open source [Kubernetes](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler) version.

When configured, the VPA automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for other pods and helps ensure effective utilization of your AKS clusters. The Vertical Pod Autoscaler provides recommendations for resource usage over time. To manage sudden increases in resource usage, use the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler), which scales the number of pod replicas as needed.

## Benefits

The Vertical Pod Autoscaler offers the following benefits:

- Analyzes and adjusts processor and memory resources to
*right size*your applications. VPA isn't only responsible for scaling up, but also for scaling down based on their resource use over time. - A pod with a scaling mode set to
*auto*or*recreate*is evicted if it needs to change its resource requests. - You can set CPU and memory constraints for individual containers by specifying a resource policy.
- Ensures nodes have correct resources for pod scheduling.
- Offers configurable logging of any adjustments made to processor or memory resources made.
- Improves cluster resource utilization and frees up CPU and memory for other pods.

## Limitations and considerations

Consider the following limitations and considerations when using the Vertical Pod Autoscaler:

- VPA supports a maximum of 1,000 pods associated with
`VerticalPodAutoscaler`

objects per cluster. - VPA might recommend more resources than available in the cluster, which prevents the pod from being assigned to a node and run due to insufficient resources. You can overcome this limitation by setting the
*LimitRange*to the maximum available resources per namespace, which ensures pods don't ask for more resources than specified. You can also set maximum allowed resource recommendations per pod in a`VerticalPodAutoscaler`

object. The VPA can't completely overcome an insufficient node resource issue. The limit range is fixed, but the node resource usage is changed dynamically. - We don't recommend using VPA with the
[Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler), which scales based on the same CPU and memory usage metrics. - The VPA Recommender only stores up to
*eight days*of historical data. - VPA doesn't support JVM-based workloads due to limited visibility into actual memory usage of the workload.
- VPA doesn't support running your own implementation of VPA alongside it. Having an extra or customized recommender is supported.
- AKS Windows containers aren't supported.

## VPA overview

The VPA object consists of three components:

**Recommender**: The Recommender monitors current and past resource consumption, including metric history, Out of Memory (OOM) events, and VPA deployment specs, and uses the information it gathers to provide recommended values for container CPU and Memory requests/limits.**Updater**: The Updater monitors managed pods to ensure that their resource requests are set correctly. If not, it removes those pods so that their controllers can recreate them with the updated requests.**VPA Admission Controller**: The VPA Admission Controller sets the correct resource requests on new pods either created or recreated by their controller based on the Updater's activity.

### VPA admission controller

The VPA Admission Controller is a binary that registers itself as a *Mutating Admission Webhook*. When a new pod is created, the VPA Admission Controller gets a request from the API server and evaluates if there's a matching VPA configuration or finds a corresponding one and uses the current recommendation to set resource requests in the pod.

A standalone job, `overlay-vpa-cert-webhook-check`

, runs outside of the VPA Admission Controller. The `overlay-vpa-cert-webhook-check`

job creates and renews the certificates and registers the VPA Admission Controller as a `MutatingWebhookConfiguration`

.

### VPA object operation modes

A Vertical Pod Autoscaler resource, most commonly a *deployment*, is inserted for each controller that you want to have automatically computed resource requirements.

There are four modes in which the VPA operates:

`Auto`

: VPA assigns resource requests during pod creation and updates existing pods using the preferred update mechanism.`Auto`

, which is equivalent to`Recreate`

, is the default mode. Once restart-free, or*in-place*, updates of pod requests are available, it can be used as the preferred update mechanism by the`Auto`

mode. With the`Auto`

mode, VPA evicts a pod if it needs to change its resource requests. It might cause the pods to be restarted all at once, which can cause application inconsistencies. You can limit restarts and maintain consistency in this situation using a[PodDisruptionBudget](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/).`Recreate`

: VPA assigns resource requests during pod creation and updates existing pods by evicting them when the requested resources differ significantly from the new recommendations (respecting the PodDisruptionBudget, if defined). You should only use this mode if you need to ensure that the pods are restarted whenever the resource request changes. Otherwise, we recommend using`Auto`

mode, which takes advantage of restart-free updates once available.`Initial`

: VPA only assigns resource requests during pod creation. It doesn't update existing pods. This mode is useful for testing and understanding the VPA behavior without affecting the running pods.`Off`

: VPA doesn't automatically change the resource requirements of the pods. The recommendations are calculated and can be inspected in the VPA object.

## Deployment pattern for application development

If you're unfamiliar with VPA, we recommend the following deployment pattern during application development to identify its unique resource utilization characteristics, test VPA to verify it's functioning properly, and test alongside other Kubernetes components to optimize resource utilization of the cluster:

- Set
`UpdateMode = "Off"`

in your production cluster and run VPA in recommendation mode so you can test and gain familiarity with VPA.`UpdateMode = "Off"`

can avoid introducing a misconfiguration that can cause an outage. - Establish observability first by collecting actual resource utilization telemetry over a given period of time, which helps you understand the behavior and any signs of issues from container and pod resources influenced by the workloads running on them.
- Get familiar with the monitoring data to understand the performance characteristics. Based on this insight, set the desired requests/limits accordingly and then in the next deployment or upgrade.
- Set
`updateMode`

value to`Auto`

,`Recreate`

, or`Initial`

depending on your requirements.

## Next steps

To learn how to set up the Vertical Pod Autoscaler on your AKS cluster, see [Use the Vertical Pod Autoscaler in AKS](use-vertical-pod-autoscaler).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/active-passive-solution -->

# Active-passive disaster recovery solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines an active-passive disaster recovery solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-passive solution overview

In this disaster recovery approach, we have two independent AKS clusters being deployed in two Azure regions. However, only one of the clusters is actively serving traffic at any one time. The secondary cluster (not actively serving traffic) contains the same configuration and application data as the primary cluster but doesn’t accept any traffic unless directed by Azure Front Door traffic manager.

## Scenarios and configurations

This solution is best implemented when hosting applications reliant on resources, such as databases, that actively serve traffic in one region. In scenarios where you need to host stateless applications deployed across both regions, such as horizontal scaling, we recommend considering an [active-active solution](active-active-solution), as active-passive involves added latency.

## Components

The active-passive disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, network traffic is routed to the primary AKS cluster set in the Azure Front Door configuration.

**Configured cluster prioritization**: You set a prioritization level between 1-5 for each cluster (with 1 being the highest priority and 5 being the lowest priority). You can set multiple clusters to the same priority level and specify the weight for each cluster. If the primary cluster becomes unavailable, traffic automatically routes to the next region selected in Azure Front Door. All traffic must go through Azure Front Door for this system to work.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to the [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance in the primary region (cluster must be marked with priority 1). In the event of a region failure, the service redirects traffic to the next cluster in the priority list.

For more information, see [Priority-based traffic-routing](/en-us/azure/frontdoor/routing-methods#priority-based-traffic-routing).

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-az-cli -->

# Install the Open Service Mesh (OSM) add-on using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Open Service Mesh (OSM) add-on on an Azure Kubernetes Service (AKS) cluster. The OSM add-on installs the OSM mesh on your cluster. The OSM mesh is a service mesh that provides traffic management, policy enforcement, and telemetry collection for your applications. For more information about the OSM mesh, see [Open Service Mesh](https://openservicemesh.io/).

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI installed](/en-us/cli/azure/install-azure-cli).

## Install the OSM add-on on your cluster

If you don't have one already, create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster with the OSM add-on installed using the

command and specify`az aks create`

`open-service-mesh`

for the`--enable-addons`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-addons open-service-mesh \ --generate-ssh-keys`


Important

You can't enable the OSM add-on on an existing cluster if an OSM mesh is already on your cluster. Uninstall any existing OSM meshes on your cluster before enabling the OSM add-on.

When installing on an existing clusters, use the [ az aks enable-addons](/en-us/cli/azure/aks#az-aks-enable-addons) command. The following code shows an example:

```
az aks enable-addons \
--resource-group myResourceGroup \
--name myAKSCluster \
--addons open-service-mesh
```


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the OSM add-on is installed on your cluster

Verify the OSM add-on is installed on your cluster using the

command with and specify`az aks show`

`'addonProfiles.openServiceMesh.enabled'`

for the`--query`

parameter. In the output, under`addonProfiles`

, the`enabled`

value should show as`true`

for`openServiceMesh`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'addonProfiles.openServiceMesh.enabled'`


## Verify the OSM mesh is running on your cluster

Verify the version, status, and configuration of the OSM mesh running on your cluster using the

`kubectl get deployment`

command and display the image version of the*osm-controller*deployment.`kubectl get deployment -n kube-system osm-controller -o=jsonpath='{$.spec.template.spec.containers[:1].image}'`

The following example output shows version

*0.11.1*of the OSM mesh:`mcr.microsoft.com/oss/openservicemesh/osm-controller:v0.11.1`

Verify the status of the OSM components running on your cluster using the following

`kubectl`

commands to show the status of the`app.kubernetes.io/name=openservicemesh.io`

deployments, pods, and services.`kubectl get deployments -n kube-system --selector app.kubernetes.io/name=openservicemesh.io kubectl get pods -n kube-system --selector app.kubernetes.io/name=openservicemesh.io kubectl get services -n kube-system --selector app.kubernetes.io/name=openservicemesh.io`

Important

If any pods have a status other than

`Running`

, such as`Pending`

, your cluster might not have enough resources to run OSM. Review the sizing for your cluster, such as the number of nodes and the virtual machine's SKU, before continuing to use OSM on your cluster.Verify the configuration of your OSM mesh using the

`kubectl get meshconfig`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

The following example output shows the configuration of an OSM mesh:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

The example output shows

`enablePermissiveTrafficPolicyMode: true`

, which means OSM has permissive traffic policy mode enabled. With this mode enabled in your OSM mesh:- The
[SMI](https://smi-spec.io/)traffic policy enforcement is bypassed. - OSM automatically discovers services that are a part of the service mesh.
- OSM creates traffic policy rules on each Envoy proxy sidecar to be able to communicate with these services.

- The

## Delete your cluster

When you no longer need the cluster, you can delete it using the

command, which removes the resource group, the cluster, and all related resources.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see [Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-load-balancer-standard -->

# Configure a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize different settings for your standard public load balancer at cluster creation time or by updating the cluster. These customization options allow you to create a load balancer that meets your workload needs. With the standard load balancer, you can:

[Change the inbound pool type](#change-the-inbound-pool-type).[Set or scale the number of managed outbound IPs](#scale-the-number-of-managed-outbound-public-ips).[Provide your own custom outbound IPs or outbound IP prefix](#provide-your-own-outbound-public-ips-or-prefixes).[Customize the number of allocated outbound ports to each node on the cluster](#configure-the-allocated-outbound-ports).[Configure the timeout setting for idle connections](#configure-the-load-balancer-idle-timeout).

Important

You can only use one outbound IP option (managed IPs, bring your own IP, or IP prefix) at a given time.

## Before you begin

- Follow the steps in
[Use a public standard load balancer in Azure Kubernetes Service (AKS)](load-balancer-standard)to create and deploy a load balancer service in AKS.

## Change the inbound pool type

You can reference AKS nodes in the load balancer backend pools by their IP configuration (Azure Virtual Machine Scale Sets based membership) or their IP address only. The IP address based backend pool membership provides higher efficiencies when updating services and provisioning load balancers, especially at high node counts. When combined with [NAT Gateway](nat-gateway) or [user-defined routing egress](egress-udr) types, provisioning of new nodes and services are more performant.

Two different pool membership types are available:

`nodeIPConfiguration`

: Legacy Virtual Machine Scale Sets IP configuration based pool membership type.`nodeIP`

: IP-based membership type.

### Requirements for changing the inbound pool type

Make sure you meet the following requirements before changing the inbound pool type:

- The AKS cluster must be version 1.23 or newer.
- The AKS cluster must be using standard load balancers and Virtual Machine Scale Sets.

-
[Create a new AKS cluster with IP-based inbound pool membership](#tabpanel_1_create-cluster-ip-based) -
[Update an existing AKS cluster to use IP-based inbound pool membership](#tabpanel_1_update-cluster-ip-based)

Create an AKS cluster with IP-based inbound pool membership using the

command with the`az aks create`

`--load-balancer-backend-pool-type=nodeIP`

parameter.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-backend-pool-type=nodeIP \ --generate-ssh-keys`


## Scale the number of managed outbound public IPs

Azure Load Balancer provides outbound and inbound connectivity from a VNet. Outbound rules make it simple to configure network address translation for the public standard load balancer.

Outbound rules follow the same syntax as load balancing and inbound NAT rules: *frontend IPs + parameters + backend pool*

An outbound rule configures outbound NAT for all virtual machines (VMs) identified by the backend pool to be translated to the frontend. Parameters provide more control over the outbound NAT algorithm.

While you can use an outbound rule with a single public IP address, outbound rules are great for scaling outbound NAT because they ease the configuration burden. You can use multiple IP addresses to plan for large-scale scenarios and outbound rules to mitigate SNAT exhaustion prone patterns. Each IP address provided by a frontend provides 64k ephemeral ports for the load balancer to use as SNAT ports.

When using a *Standard* SKU load balancer with managed outbound public IPs (which are created by default), you can scale the number of managed outbound public IPs using the `--load-balancer-managed-outbound-ip-count`

parameter.

Important

We don't recommend using the Azure portal to make any outbound rule changes. When making these changes, you should go through the AKS cluster and not directly on the Load Balancer resource.

Outbound rule changes made directly on the Load Balancer resource are removed whenever the cluster is reconciled, such as when it's stopped, started, upgraded, or scaled.

Use the Azure CLI, as shown in the examples. Outbound rule changes made using `az aks`

CLI commands are permanent across cluster downtime.

For more information, see [Azure Load Balancer outbound rules](/en-us/azure/load-balancer/outbound-rules).

### Set the number of managed outbound public IPs

-
[Create a new cluster with a specific number of managed outbound public IPs](#tabpanel_2_create-cluster-managed-outbound-ips) -
[Update an existing cluster to scale the number of managed outbound public IPs](#tabpanel_2_update-cluster-managed-outbound-ips)

Create a new AKS cluster with a specific number of managed outbound public IPs using the

command with the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter. The following example sets the number of managed outbound public IPs to*two*.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 2 \ --generate-ssh-keys`


## Provide your own outbound public IPs or prefixes

When you use a *Standard* SKU load balancer, the AKS cluster automatically creates a public IP in the AKS-managed infrastructure resource group and assigns it to the load balancer outbound pool by default.

A public IP created by AKS is an AKS-managed resource, meaning AKS manages the lifecycle of that public IP and doesn't require user action directly on the public IP resource. Alternatively, you can assign your own custom public IP or public IP prefix at cluster creation time. Your custom IPs can also be updated on an existing cluster's load balancer properties.

### Requirements for using your own outbound public IPs or prefixes

Make sure you meet the following requirements before providing your own outbound public IPs or prefixes:

- You must create and own custom public IP addresses. You can't reuse managed public IP addresses created by AKS as a "bring your own custom IP" because it can cause management conflicts.
- You must ensure the AKS cluster identity has permissions to access the outbound IP, as per the
[required public IP permissions list](kubernetes-service-principal#grant-access-to-networking-resources). - Make sure you meet the
[prerequisites and constraints](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix#limitations)necessary to configure outbound IPs or outbound IP prefixes.

### Provide your own outbound public IPs

-
[Provide your own outbound public IPs when creating a new cluster](#tabpanel_3_create-cluster-custom-ips) -
[Update an existing cluster to use your own outbound public IPs](#tabpanel_3_update-cluster-custom-ips)

Create a new AKS cluster with your own outbound public IPs using the

command with the`az aks create`

`--load-balancer-outbound-ips`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-outbound-ips $PUBLIC_IP_ID1,$PUBLIC_IP_ID2 \ --generate-ssh-keys`


### Provide your own outbound public IP prefixes

-
[Provide your own outbound public IP prefixes when creating a new cluster](#tabpanel_4_create-cluster-custom-ip-prefixes) -
[Update an existing cluster to use your own outbound public IP prefixes](#tabpanel_4_update-cluster-custom-ip-prefixes)

Create a new AKS cluster with your own outbound public IP prefixes using the

command with the`az aks create`

`--load-balancer-outbound-ip-prefixes`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --load-balancer-outbound-ip-prefixes $PUBLIC_IP_PREFIX_ID1,$PUBLIC_IP_PREFIX_ID2 \ --generate-ssh-keys`


## Configure the allocated outbound ports

Important

If you have applications on your cluster that can establish a large number of connections to small set of destinations on public IP addresses, like many instances of a frontend application connecting to a database, you might have a scenario susceptible to encounter SNAT port exhaustion. SNAT port exhaustion happens when an application runs out of outbound ports to use to establish a connection to another application or host. If you have a scenario susceptible to encounter SNAT port exhaustion, we highly recommend you increase the allocated outbound ports and outbound frontend IPs on the load balancer.

For more information on SNAT, see [Use SNAT for outbound connections](/en-us/azure/load-balancer/load-balancer-outbound-connections).

By default, AKS sets *AllocatedOutboundPorts* on its load balancer to `0`

, which enables [automatic outbound port assignment based on backend pool size](/en-us/azure/load-balancer/load-balancer-outbound-connections#preallocatedports) when creating a cluster. For example, if a cluster has 50 or fewer nodes, 1024 ports are allocated to each node. This value allows for scaling to cluster maximum node counts without requiring networking reconfiguration, but can make SNAT port exhaustion more common as more nodes are added. As the number of nodes in the cluster increases, fewer ports are available per node. Increasing the node counts across the boundaries in the chart (for example, going from 50 to 51 nodes or 100 to 101) might be disruptive to connectivity as the SNAT ports allocated to existing nodes are reduced to allow for more nodes. We recommend using an explicit value for *AllocatedOutboundPorts*.

### View the current allocated outbound ports

Get the

*AllocatedOutboundPorts*value for the AKS cluster load balancer using thecommand.`az network lb outbound-rule list`

`NODE_RG=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query nodeResourceGroup -o tsv) az network lb outbound-rule list --resource-group $NODE_RG --lb-name kubernetes -o table`

The following example output shows that automatic outbound port assignment based on backend pool size is enabled for the cluster:

`AllocatedOutboundPorts EnableTcpReset IdleTimeoutInMinutes Name Protocol ProvisioningState ResourceGroup ------------------------ ---------------- ---------------------- --------------- ---------- ------------------- ------------- 0 True 30 aksOutboundRule All Succeeded MC_myResourceGroup_myAKSCluster_eastus`


### Calculate and verify outbound ports and IPs needed

Before setting a specific value or increasing an existing value for either outbound ports or outbound IP addresses, you must calculate the appropriate number of outbound ports and IP addresses. Use the following equation for this calculation rounded to the nearest integer: `64,000 ports per IP / <outbound ports per node> * <number of outbound IPs> = <maximum number of nodes in the cluster>`

.

#### Considerations for calculating outbound ports and IPs

When calculating the number of outbound ports and IPs and setting the values, keep the following information in mind:

- The number of outbound ports per node is fixed based on the value you set.
- The value for outbound ports must be a multiple of 8.
- Adding more IPs doesn't add more ports to any node, but it provides capacity for more nodes in the cluster.
- You must account for nodes that might be added as part of upgrades, including the count of nodes specified via
and`maxCount`

values.`maxSurge`


#### Examples of calculating outbound ports and IPs

The following examples show how the values you set affect the number of outbound ports and IP addresses:

- If the default values are used and the cluster has 48 nodes, each node has 1024 ports available.
- If the default values are used and the cluster scales from 48 to 52 nodes, each node is updated from 1024 ports available to 512 ports available.
- If the number of outbound ports is set to 1,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 128 nodes:
`64,000 ports per IP / 1,000 ports per node * 2 IPs = 128 nodes`

. - If the number of outbound ports is set to 1,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 448 nodes:
`64,000 ports per IP / 1,000 ports per node * 7 IPs = 448 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 32 nodes:
`64,000 ports per IP / 4,000 ports per node * 2 IPs = 32 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 112 nodes:
`64,000 ports per IP / 4,000 ports per node * 7 IPs = 112 nodes`

.

Important

After calculating the number of outbound ports and IPs, verify you have extra outbound port capacity to handle node surge during upgrades. It's critical to allocate sufficient excess ports for extra nodes needed for upgrade and other operations. AKS defaults to *one* buffer node for upgrade operations. If you're using [ maxSurge values](upgrade-aks-cluster#customize-node-surge-upgrade), multiply the outbound ports per node by your

`maxSurge`

value to determine the number of ports required. For example, if you calculate that you need 4000 ports per node with 7 IP addresses on a cluster with a maximum of 100 nodes and a max surge of 2:- 2 surge nodes * 4000 ports per node = 8000 ports needed for node surge during upgrades.
- 100 nodes * 4000 ports per node = 400,000 ports required for your cluster.
- 7 IPs * 64000 ports per IP = 448,000 ports available for your cluster.

This example shows the cluster has an excess capacity of 48,000 ports, which is sufficient to handle the 8000 ports needed for node surge during upgrades.

### Set the allocated outbound ports and outbound IPs

Once the values have been calculated and verified, you can apply those values using `load-balancer-outbound-ports`

and either `load-balancer-managed-outbound-ip-count`

, `load-balancer-outbound-ips`

, or `load-balancer-outbound-ip-prefixes`

when creating or updating a cluster.

-
[Create a new cluster with specific outbound ports and IPs](#tabpanel_5_create-cluster-outbound-ports-ips) -
[Update an existing cluster with specific outbound ports and IPs](#tabpanel_5_update-cluster-outbound-ports-ips)

Create a new AKS cluster with specific outbound ports and IPs using the

command. The following example sets the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter to*7*and the`--load-balancer-outbound-ports`

parameter to*4000*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 7 \ --load-balancer-outbound-ports 4000 \ --generate-ssh-keys`


## Configure the load balancer idle timeout

When SNAT port resources are exhausted, outbound flows fail until existing flows release SNAT ports. Load balancer reclaims SNAT ports when the flow closes, and the AKS-configured load balancer uses a 30-minute idle timeout for reclaiming SNAT ports from idle flows. You can also use transport (for example, ** TCP keepalives** or

**) to refresh an idle flow and reset this idle timeout if necessary.**

`application-layer keepalives`

If you expect to have numerous short-lived connections and no long-lived connections that might have long times of idle, like using `kubectl proxy`

or `kubectl port-forward`

, consider using a low timeout value such as *4 minutes*. When using TCP keepalives, it's sufficient to enable them on one side of the connection. For example, it's sufficient to enable them on the server side only to reset the idle timer of the flow. It's not necessary for both sides to start TCP keepalives. Similar concepts exist for application layer, including database client-server configurations. Check the server side for what options exist for application-specific keepalives.

Important

AKS enables *TCP Reset* on idle by default. We recommend you keep this configuration and leverage it for more predictable application behavior on your scenarios. For more information, see [Azure load balancer TCP reset](/en-us/azure/load-balancer/load-balancer-tcp-reset).

When setting *IdleTimeoutInMinutes* to a different value than the default of 30 minutes, consider how long your workloads need an outbound connection. Also consider that the default timeout value for a *Standard* SKU load balancer used outside of AKS is *4 minutes*. An *IdleTimeoutInMinutes* value that more accurately reflects your specific AKS workload can help decrease SNAT exhaustion caused by tying up connections no longer being used.

Warning

Altering the values for *AllocatedOutboundPorts* and *IdleTimeoutInMinutes* might significantly change the behavior of the outbound rule for your load balancer and shouldn't be done lightly. See [Troubleshoot SNAT](troubleshoot-source-network-address-translation) and review the [Load balancer outbound rules](/en-us/azure/load-balancer/load-balancer-outbound-connections#outboundrules) and [outbound connections in Azure](/en-us/azure/load-balancer/load-balancer-outbound-connections) before updating these values to fully understand the impact of your changes.

-
[Create a new cluster with a specific idle timeout](#tabpanel_6_create-cluster-idle-timeout) -
[Update an existing cluster with a specific idle timeout](#tabpanel_6_update-cluster-idle-timeout)

Create a new AKS cluster with a specific idle timeout using the

command with the`az aks create`

`--load-balancer-idle-timeout`

parameter. The following example sets the idle timeout to*4 minutes*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-idle-timeout 4 \ --generate-ssh-keys`


## Restrict inbound traffic to specific IP ranges

The following manifest uses `loadBalancerSourceRanges`

to specify a new IP range for inbound external traffic:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-vote-front
loadBalancerSourceRanges:
- MY_EXTERNAL_IP_RANGE
```


This example updates the rule to allow inbound external traffic only from the `MY_EXTERNAL_IP_RANGE`

range. If you replace `MY_EXTERNAL_IP_RANGE`

with the internal subnet IP address, traffic is restricted to only cluster internal IPs. If traffic is restricted to cluster internal IPs, clients outside your Kubernetes cluster are unable to access the load balancer.

Note

Keep the following information in mind when restricting inbound traffic:

- When you need to allow both CIDR blocks and Azure service tags, remove the
`loadBalancerSourceRanges`

property and add the`service.beta.kubernetes.io/azure-allowed-ip-ranges`

and/or`service.beta.kubernetes.io/azure-allowed-service-tags`

Load Balancer annotations. This configuration applies filtering only at the NSG layer and skips host-level kube-proxy rules. If you set the`loadBalancerSourceRanges`

property together with the`azure-allowed-service-tags`

annotation, AKS will report an error when you attempt to apply the specification. - Inbound, external traffic flows from the load balancer to the VNet for your AKS cluster. The VNet has a network security group (NSG) which allows all inbound traffic from the load balancer. This NSG uses a
[service tag](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)of type*LoadBalancer*to allow traffic from the load balancer. - Pod CIDR should be added to
`loadBalancerSourceRanges`

if there are Pods needing to access the service's Load Balancer IP for clusters with Kubernetes version 1.25 or higher.

## Maintain the client's IP on inbound connections

By default, a service of type `LoadBalancer`

[in Kubernetes](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-type-loadbalancer) and in AKS doesn't persist the client's IP address on the connection to the pod. The source IP on the packet that's delivered to the pod becomes the private IP of the node. To maintain the client's IP address, you must set `service.spec.externalTrafficPolicy`

to `local`

in the service definition. The following manifest shows an example:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
externalTrafficPolicy: Local
ports:
- port: 80
selector:
app: azure-vote-front
```


## Customizations via Kubernetes Annotations

The following annotations are supported for Kubernetes services with type `LoadBalancer`

, and they only apply to **INBOUND** flows.

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-internal` |
`true` or `false` |
Specify whether the load balancer should be internal. If not set, it defaults to public. |
`service.beta.kubernetes.io/azure-load-balancer-internal-subnet` |
Name of the subnet | Specify which subnet the internal load balancer should be bound to. If not set, it defaults to the subnet configured in cloud config file. |
`service.beta.kubernetes.io/azure-dns-label-name` |
Name of the DNS label on Public IPs | Specify the DNS label name for the public service. If it's set to an empty string, the DNS entry in the Public IP isn't used. |
`service.beta.kubernetes.io/azure-shared-securityrule` |
`true` or `false` |
Specify exposing the service through a potentially shared Azure security rule to increase service exposure, utilizing Azure
|

`service.beta.kubernetes.io/azure-load-balancer-resource-group`

`service.beta.kubernetes.io/azure-allowed-service-tags`

[service tags](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)separated by commas.`service.beta.kubernetes.io/azure-allowed-ip-ranges`

`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

`true`

or `false`

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

`service.beta.kubernetes.io/azure-load-balancer-ipv6`

### Customize allowed IP ranges (preview)

You can use the `azure-allowed-service-tags`

and `azure-allowed-ip-ranges`

annotations to combine CIDR blocks and Azure service tags on the load balancer. Add `service.beta.kubernetes.io/azure-allowed-ip-ranges`

with a comma-separated list of IP prefixes, and add `service.beta.kubernetes.io/azure-allowed-service-tags`

with one or more Azure service tags. The AKS cloud provider merges both values into a single NSG rule, so traffic is filtered centrally at the NSG giving you a single, NSG-centric control plane for both IP addresses and service tags.

You can continue to use the `loadBalancerSourceRanges`

property for cases where you want CIDR-based restrictions enforced both in the NSG and the host. You can't use this property with the `azure-allowed-service-tags`

annotation. If both are specified, AKS reports an error when you try to apply the load balancer service specification.

### Customize the load balancer health probe

The following annotations are supported to customize the load balancer health probe behavior:

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
Health probe interval | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
The minimum number of unhealthy responses of health probe | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
Request path of the health probe | |
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
true/false | {port} is service port number. When set to `true` , no load balancer or health probe rules for this port are generated. Health check service shouldn't be exposed to the public internet. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
true/false | {port} is service port number. When set to `true` , no health probe rules for this port are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
Health probe protocol | {port} is service port number. Explicit protocol for the health probe for the service port {port}, overriding port.appProtocol if set. |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
port number or port name in service manifest | {port} is service port number. Explicit port for the health probe for the service port {port}, overriding the default value. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
Health probe interval | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
The minimum number of unhealthy responses of health probe | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
Request path of the health probe | {port} is service port number. |

Note

AKS now supports shared health probes for `externalTrafficPolicy: Cluster`

Services. To learn more, see [Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)](shared-health-probes).

#### Default health probe behavior

Currently, the default protocol of the health probe varies among services with different transport protocols, app protocols, annotation, and external traffic policies.

- For local services, HTTP and /healthz would be used. The health probe will query
`NodeHealthPort`

rather than actual backend service. - For cluster TCP services, TCP would be used.
- For cluster UDP services, no health probes.

Note

For local services with PLS integration and PLS proxy protocol enabled, the default HTTP and /healthz health probe doesn't work. Thus health probe can be customized the same way as cluster services to support this scenario.

##### Health probe request path annotation

Starting in Kubernetes version 1.20, the service annotation `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

was introduced to determine the health probe behavior.

- For clusters <=1.23,
`spec.ports.appProtocol`

would only be used as probe protocol when`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is also set. - For clusters >1.24,
`spec.ports.appProtocol`

would be used as probe protocol and`/`

would be used as default probe request path (`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

could be used to change to a different request path).

Note that the request path would be ignored when using TCP or the `spec.ports.appProtocol`

is empty. The following table summarizes the default health probe behavior:

| loadbalancer sku | `externalTrafficPolicy` |
spec.ports.Protocol | spec.ports.AppProtocol | `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
LB probe protocol | LB probe request path |
|---|---|---|---|---|---|---|
| standard | local | any | any | any | http | `/healthz` |
| standard | cluster | udp | any | any | null | null |
| standard | cluster | tcp | (ignored) | tcp | null | |
| standard | cluster | tcp | tcp | (ignored) | tcp | null |
| standard | cluster | tcp | http/https | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| standard | cluster | tcp | http/https | `/custom-path` |
http/https | `/custom-path` |
| standard | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |
| basic | local | any | any | any | http | `/healthz` |
| basic | cluster | tcp | (ignored) | tcp | null | |
| basic | cluster | tcp | tcp | (ignored) | tcp | null |
| basic | cluster | tcp | http | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| basic | cluster | tcp | http | `/custom-path` |
http | `/custom-path` |
| basic | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |

##### Health probe interval and number of probes annotations

Starting in Kubernetes version 1.21, two service annotations `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

and `load-balancer-health-probe-num-of-probe`

were introduced, which customize the configuration of health probe. If `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

isn't set, a default value of *5* is applied. If `load-balancer-health-probe-num-of-probe`

isn't set, a default value of *2* is applied.

### Custom Load Balancer health probe for port

Different ports in a service can require different health probe configurations. This could be because of service design (such as a single health endpoint controlling multiple ports), or Kubernetes features like the [MixedProtocolLBService](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancers-with-mixed-protocol-types).

The following table summarizes the port-specific annotations that can be used to override the global health probe annotations for a specific port in the service:

| Port-specific annotation | Global probe annotation | Behavior |
|---|---|---|
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
N/A (no equivalent globally) | If set to `true` , no load balancer or probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
N/A (no equivalent globally) | If set to `true` , no probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
N/A (no equivalent globally) | Sets the health probe protocol for this service port (for example: Http, Https, Tcp). |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
N/A (no equivalent globally) | Sets the health probe port for this service port (for example: 15021). |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
For Http or Https, sets the health probe request path (defaults to /). |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
Number of consecutive probe failures before the port is considered unhealthy. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
The amount of time between probe attempts. |

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

To learn more about using internal load balancer for inbound traffic, see the [AKS internal load balancer documentation](internal-lb).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-credentials -->

# Update or rotate the credentials for an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS clusters created with a service principal have a one-year expiration time. As you near the expiration date, you can reset the credentials to extend the service principal for an additional period of time. You might also want to update, or rotate, the credentials as part of a defined security policy. AKS clusters [integrated with Microsoft Entra ID](azure-ad-integration-cli) as an authentication provider have two more identities: the Microsoft Entra Server App and the Microsoft Entra Client App. This article details how to update the service principal and Microsoft Entra credentials for an AKS cluster.

Note

Alternatively, you can use a managed identity for permissions instead of a service principal. Managed identities don't require updates or rotations. For more information, see [Use managed identities](use-managed-identity).

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update or create a new service principal for your AKS cluster

When you want to update the credentials for an AKS cluster, you can choose to either:

- Update the credentials for the existing service principal.
- Create a new service principal and update the cluster to use these new credentials.

Warning

If you choose to create a *new* service principal, wait around 30 minutes for the service principal permission to propagate across all regions. Updating a large AKS cluster to use these credentials can take a long time to complete.

### Check the expiration date of your service principal

To check the expiration date of your service principal, use the [ az ad app credential list](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-list) command. The following example gets the service principal ID for the

`$CLUSTER_NAME`

cluster in the `$RESOURCE_GROUP_NAME`

resource group using the [command. The service principal ID is set as a variable named](/en-us/cli/azure/aks#az-aks-show)

`az aks show`

*SP_ID*.

```
SP_ID=$(az aks show --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME \
--query servicePrincipalProfile.clientId -o tsv)
az ad app credential list --id "$SP_ID" --query "[].endDateTime" -o tsv
```


### Reset the existing service principal credentials

To update the credentials for an existing service principal, get the service principal ID of your cluster using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command. The following example gets the ID for the

`$CLUSTER_NAME`

cluster in the `$RESOURCE_GROUP_NAME`

resource group. The variable named *SP_ID*stores the service principal ID used in the next step. These commands use the Bash command language.

Warning

When you reset your cluster credentials on an AKS cluster that uses Azure Virtual Machine Scale Sets, a [node image upgrade](node-image-upgrade) is performed to update your nodes with the new credential information.

```
SP_ID=$(az aks show --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME \
--query servicePrincipalProfile.clientId -o tsv)
```


Use the variable *SP_ID* containing the service principal ID to reset the credentials using the [ az ad app credential reset](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-reset) command. The following example enables the Azure platform to generate a new secure secret for the service principal and store it as a variable named

*SP_SECRET*.

```
SP_SECRET=$(az ad app credential reset --id "$SP_ID" --query password -o tsv)
```


Next, you [update AKS cluster with service principal credentials](#update-aks-cluster-with-service-principal-credentials). This step is necessary to update the service principal on your AKS cluster.

### Create a new service principal

Note

If you updated the existing service principal credentials in the previous section, skip this section and instead [update the AKS cluster with service principal credentials](#update-aks-cluster-with-service-principal-credentials).

To create a service principal and update the AKS cluster to use the new credential, use the [ az ad sp create-for-rbac](/en-us/cli/azure/ad/sp#az-ad-sp-create-for-rbac) command.

```
az ad sp create-for-rbac --role Contributor --scopes /subscriptions/$SUBSCRIPTION_ID
```


The output is similar to the following example output. Make a note of your own `appId`

and `password`

to use in the next step.

```
{
"appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"name": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"password": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


Define variables for the service principal ID and client secret using your output from running the [ az ad sp create-for-rbac](/en-us/cli/azure/ad/sp#az-ad-sp-create-for-rbac) command. The

*SP_ID*is the

*appId*, and the

*SP_SECRET*is your

*password*.

```
SP_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
SP_SECRET=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```


Next, you [update AKS cluster with the new service principal credential](#update-aks-cluster-with-service-principal-credentials). This step is necessary to update the AKS cluster with the new service principal credential.

## Update AKS cluster with service principal credentials

Important

For large clusters, updating your AKS cluster with a new service principal can take a long time to complete. Consider reviewing and customizing the [node surge upgrade settings](upgrade-aks-cluster#customize-node-surge-upgrade) to minimize disruption during the update. For small and midsize clusters, it takes a several minutes for the new credentials to update in the cluster.

Update the AKS cluster with your new or existing credentials by running the [ az aks update-credentials](/en-us/cli/azure/aks#az-aks-update-credentials) command.

```
az aks update-credentials \
--resource-group $RESOURCE_GROUP_NAME \
--name $CLUSTER_NAME \
--reset-service-principal \
--service-principal "$SP_ID" \
--client-secret "${SP_SECRET}"
```


## Update AKS cluster with new Microsoft Entra application credentials

You can create new Microsoft Entra server and client applications by following the [Microsoft Entra integration steps](azure-ad-integration-cli#create-azure-ad-server-component), or reset your existing Microsoft Entra applications following the [same method as for service principal reset](#reset-the-existing-service-principal-credentials). After that, you need to update your cluster Microsoft Entra application credentials using the [ az aks update-credentials](/en-us/cli/azure/aks#az-aks-update-credentials) command with the

*--reset-aad*variables.

```
az aks update-credentials \
--resource-group $RESOURCE_GROUP_NAME \
--name $CLUSTER_NAME \
--reset-aad \
--aad-server-app-id $SERVER_APPLICATION_ID \
--aad-server-app-secret $SERVER_APPLICATION_SECRET \
--aad-client-app-id $CLIENT_APPLICATION_ID
```


## Next steps

In this article, you learned how to update or rotate service principal and Microsoft Entra application credentials. For more information on how to use a manage identity for workloads within an AKS cluster, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-troubleshooting -->

# Troubleshoot Dapr extension installation errors

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses some common error messages that you may receive when you install or update the [Distributed Application Runtime (Dapr)](https://dapr.io/) extension for Microsoft Azure Kubernetes Service (AKS) or Arc for Kubernetes.

[Learn more about the level of support provided for the Dapr extension.](#next-steps)

## Scenario 1: Installation fails but doesn't show an error message

If the extension generates an error message when you create or update it, you can inspect where the creation failed by running the [az k8s-extension list](/en-us/cli/azure/k8s-extension#az-k8s-extension-list) command:

```
az k8s-extension list --resource-group <my-resource-group-name> \
--cluster-name <my-cluster-name> \
--cluster-type managedClusters
```


If a wrong key is used in the configuration settings, such as `global.ha=false`

instead of `global.ha.enabled=false`

, the following JSON status is returned. The error message is captured in the `message`

property.

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "Error: {failed to install chart from path [] for release [dapr-1]: err [template: dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml:1:17: executing \"dapr/charts/dapr_sidecar_injector/templates/dapr_sidecar_injector_poddisruptionbudget.yaml\" at <.Values.global.ha.enabled>: can't evaluate field enabled in type interface {}]} occurred while doing the operation : {Installing the extension} on the config",
"time": null
}
],
```


Here's another example of a JSON error message:

```
"statuses": [
{
"code": "InstallationFailed",
"displayStatus": null,
"level": null,
"message": "The extension operation failed with the following error: unable to add the configuration with configId {extension:microsoft-dapr} due to error: {error while adding the CRD configuration: error {failed to get the immutable configMap from the elevated namespace with err: configmaps 'extension-immutable-values' not found }}. (Code: ExtensionOperationFailed)",
"time": null
}
]
```


### Solution 1: Restart the cluster, register the service provider, or delete and reinstall Dapr

To fix this issue, try the following methods:

Force delete and

[reinstall the Dapr extension](/en-us/azure/aks/dapr).

## Scenario 2: Targeted Dapr version doesn't exist

When you try to install the Dapr extension to [target a specific version](/en-us/azure/aks/dapr#targeting-a-specific-dapr-version), you receive an error message that states that the Dapr version doesn't exist:

(ExtensionOperationFailed) The extension operation failed with the following error: Failed to resolve the extension version from the given values.

Code: ExtensionOperationFailed

Message: The extension operation failed with the following error: Failed to resolve the extension version from the given values.


### Solution 2: Install again for a supported Dapr version

Try again to install the extension. Make sure that you use a [supported version of Dapr](/en-us/azure/aks/dapr#dapr-versions).

## Scenario 3: The targeted Dapr version exists but not in the specified region

Because some versions of Dapr aren't available in all regions, you might receive the following error message:

(ExtensionTypeRegistrationGetFailed) Extension type microsoft.dapr is not registered in region <regionname>.

Code: ExtensionTypeRegistrationGetFailed

Message: Extension type microsoft.dapr is not registered in region <regionname>


### Solution 3: Install in a different region

Install in a [region in which your Dapr version is supported](/en-us/azure/aks/dapr#cloudsregions).

## Scenario 4: Dapr is already installed

You try to install the Dapr extension for AKS or Arc for Kubernetes, but you receive an error message that indicates that the `dapr-system`

namespace already exists. This error message resembles the following text:

(ExtensionOperationFailed) The extension operation failed with the following error: Error: {failed to install chart from path [] for release [dapr-ext]: err [rendered manifests contain a resource that already exists. Unable to continue with install: ServiceAccount "dapr-operator" in namespace "dapr-system" exists and cannot be imported into the current release: invalid ownership metadata; annotation validation error: key "meta.helm.sh/release-name" must equal "dapr-ext": current value is "dapr"]} occurred while doing the operation : {Installing the extension} on the config


### Solution 4: Uninstall Dapr OSS first

Uninstall the Dapr OSS before you install the Dapr extension. For more information, see [Migrate from Dapr OSS to the Dapr extension for AKS](/en-us/azure/aks/dapr-migration).

## Scenario 5: The placement server pod is in a bad state

You encounter the following error:

0/4 nodes are available: 1 node(s) were unschedulable, 3 node(s) had volume node affinity conflict. preemption: 0/4 nodes are available: 4 Preemption is not helpful for scheduling.


This issue might happen when the placement server pod tries to use the persistent volume that's created in a different zone from the placement server pod itself.

### Solution 5: Install Dapr in multiple availability zones or limit the placement service to a particular availability zone

To resolve this issue, use one of the following methods:

Follow the recommended approach in

[Install Dapr in multiple availability zones while in HA mode](/en-us/azure/aks/dapr-settings#install-dapr-in-multiple-availability-zones-while-in-ha-mode).Limit the placement service to a particular availability zone by creating a custom storage class and using it for the placement service, and then run the following command:

`az k8s-extension create --cluster-type managedClusters --cluster-name <clustername> --resource-group <resourcegroup> --name <name> --extension-type Microsoft.Dapr --auto-upgrade-minor-version <minorversion> --version <version> --configuration-settings "dapr_placement.volumeclaims.storageClassName=zone-restricted"`

Here's an example of creating a custom storage class:

`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: zone-restricted provisioner: disk.csi.azure.com reclaimPolicy: Delete allowVolumeExpansion: true volumeBindingMode: WaitForFirstConsumer allowedTopologies: - matchLabelExpressions: - key: topology.kubernetes.io/zone values: - centralus-1 parameters: storageaccounttype: StandardSSD_LRS`


## Next steps

If you're still experiencing installation issues, [create a support request](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview?DMC=troubleshoot) for Microsoft to investigate and resolve.

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](/en-us/azure/aks/dapr-overview#issue-handling).

You could also start a discussion in the Dapr project Discord:

**Third-party information disclaimer**

The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-faq -->

# Frequently asked questions about Windows Server on AKS

This article provides answers to some of the most common questions about using Windows Server containers on Azure Kubernetes Service (AKS).

## Why can't I create new Windows Server 2019 node pools?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## Why can't I upgrade my Windows Server 2019 node pools to Kubernetes version 1.33?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## What kind of disks are supported for Windows?

Azure Disks and Azure Files are the supported volume types, and are accessed as New Technology File System (NTFS) volumes in the Windows Server container.

## Does Windows support generation 2 virtual machines (VMs)?

Generation 2 VMs are supported on Windows starting with Windows Server 2022. Generation 2 VMs are default in Windows Server 2025.

For more information, see [Support for generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## How do I patch my Windows nodes?

To get the latest patches for Windows nodes, you can either [upgrade the node pool](manage-node-pools#upgrade-a-single-node-pool) or [upgrade the node image](node-image-upgrade).

## Is preserving the client source IP supported?

At this time, [client source IP preservation](concepts-network-ingress#ingress-controllers) isn't supported with Windows nodes.

## Can I change the maximum number of pods per node?

Yes. For more information, see [Maximum number of pods](concepts-network-ip-address-planning#maximum-pods-per-node).

## What is the default transmission control protocol (TCP) time-out in Windows OS?

The default TCP time-out in Windows OS is four minutes. This value isn't configurable. When an application uses a longer time-out, the TCP connections between different containers in the same node close after four minutes.

## Why am I seeing an error when I try to create a new Windows agent pool?

If you created your cluster before February 2020 and didn't perform any upgrade operations, the cluster still uses an old Windows image. You might see an error that resembles the following example:

"The following list of images referenced from the deployment template isn't found: Publisher: MicrosoftWindowsServer, Offer: WindowsServer, Sku: 2019-datacenter-core-smalldisk-2004, Version: latest. Refer to [Find and use Azure Marketplace Virtual Machine images with Azure PowerShell](/en-us/azure/virtual-machines/windows/cli-ps-findimage) for instructions on finding available images."

To fix this issue, you need to perform the following steps:

- Upgrade the
[cluster control plane](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools), which updates the image offer and publisher. - Create new Windows agent pools.
- Move Windows pods from existing Windows agent pools to new Windows agent pools.
- Delete old Windows agent pools.

## Why am I seeing an error when I try to deploy Windows pods?

If you specify a value in `--max-pods`

less than the number of pods you want to create, you might see the `No available addresses`

error.

To fix this error, use the `az aks nodepool add`

command with a high enough `--max-pods`

value. For example:

```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--name $NODEPOOL_NAME \
--max-pods 3
```


For more details, see the [ --max-pods documentation](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

## Why is there an unexpected user named "sshd" on my virtual machine node?

AKS adds a user named "sshd" when installing the OpenSSH service. This user isn't malicious. We recommend that customers update their alerts to ignore this unexpected user account.

## How do I rotate the service principal for my Windows node pool?

Windows node pools don't support service principal rotation. To update the service principal, create a new Windows node pool and migrate your pods from the older pool to the new one. After your pods are migrated to the new pool, delete the older node pool.

Instead of service principals, you can use managed identities. For more information, see [Use managed identities in AKS](use-managed-identity).

## How do I change the administrator password for Windows Server nodes on my cluster?

To change the administrator password using the Azure CLI, use the `az aks update`

command with the `--admin-password`

parameter. For example:

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--admin-password <new-password>
```


To change the password using Azure PowerShell, use the `Set-AzAksCluster`

cmdlet with the `-AdminPassword`

parameter. For example:

```
Set-AzAksCluster `
-ResourceGroupName $RESOURCE_GROUP `
-Name $CLUSTER_NAME `
-AdminPassword <new-password>
```


Keep in mind that performing a cluster update causes a restart and only updates the Windows Server node pools. For information about Windows Server password requirements, see [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).

## How many node pools can I create?

AKS clusters with Windows node pools have the same resource limits as the default limits specified for the AKS service. For more information, see [Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)](quotas-skus-regions).

## Can I run ingress controllers on Windows nodes?

Yes, you can run ingress controllers that support Windows Server containers.

## Can my Windows Server containers use gMSA?

Yes. Group-managed service account (gMSA) support is generally available (GA) for Windows on AKS. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts)

## Are there any limitations on the number of services on a cluster with Windows nodes?

A cluster with Windows nodes can have approximately 500 services (sometimes less) before it encounters port exhaustion. This limitation applies to a Kubernetes Service with External Traffic Policy set to "Cluster".

When the external traffic policy on a Service is configured as a Cluster, the traffic undergoes an extra Source NAT on the node. This process also results in reservation of a port from the TCPIP dynamic port pool. This port pool is a limited resource (~16K ports by default) and many active connections to a Service can lead to dynamic port pool exhaustion resulting in connection drops.

If the Kubernetes Service is configured with External Traffic Policy set to "Local", port exhaustion problems aren't likely to occur at 500 services.

## How do I change the time zone of a running container?

To change the time zone of a running Windows Server container, connect to the running container with a PowerShell session. For example:

```
kubectl exec -it CONTAINER-NAME -- PowerShell
```


In the running container, use [Set-TimeZone](/en-us/powershell/module/microsoft.powershell.management/set-timezone) to set the time zone of the running container. For example:

```
Set-TimeZone -Id "Russian Standard Time"
```


To see the current time zone of the running container or an available list of time zones, use [Get-TimeZone](/en-us/powershell/module/microsoft.powershell.management/get-timezone).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-kubeconfig-access -->

# Use Azure role-based access control to define access to the Kubernetes configuration file in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can interact with Kubernetes clusters using the `kubectl`

tool. The Azure CLI provides an easy way to get the access credentials and *kubeconfig* configuration file to connect to your AKS clusters using `kubectl`

. You can use Azure role-based access control (Azure RBAC) to limit who can get access to the *kubeconfig* file and the permissions they have.

This article shows you how to assign Azure roles that limit who can get the configuration information for an AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal). - This article also requires that you're running Azure CLI version 2.0.65 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Available permissions for cluster roles

When you interact with an AKS cluster using the `kubectl`

tool, a configuration file, called *kubeconfig*, defines cluster connection information. This configuration file is typically stored in *~/.kube/config*. Multiple clusters can be defined in this *kubeconfig* file. You can switch between clusters using the [ kubectl config use-context](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command.

The [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command lets you get the access credentials for an AKS cluster and merges these credentials into the

*kubeconfig*file. You can use Azure RBAC to control access to these credentials. These Azure roles let you define who can retrieve the

*kubeconfig*file and what permissions they have within the cluster.

There are two Azure roles you can apply to a Microsoft Entra user or group:

**Azure Kubernetes Service Cluster Admin Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action`

API call. This API call[lists the cluster admin credentials](/en-us/rest/api/aks/managedclusters/listclusteradmincredentials). - Downloads
*kubeconfig*for the*clusterAdmin*role.

- Allows access to
**Azure Kubernetes Service Cluster User Role**- Allows access to
`Microsoft.ContainerService/managedClusters/listClusterUserCredential/action`

API call. This API call[lists the cluster user credentials](/en-us/rest/api/aks/managedclusters/listclusterusercredentials). - Downloads
*kubeconfig*for*clusterUser*role.

- Allows access to

Note

On clusters that use Microsoft Entra ID, users with the *clusterUser* role have an empty *kubeconfig* file that prompts a login. Once logged in, users have access based on their Microsoft Entra user or group settings. Users with the *clusterAdmin* role have admin access.

On clusters that don't use Microsoft Entra ID, the *clusterUser* role has same effect of *clusterAdmin* role.

## Assign role permissions to a user or group

To assign one of the available roles, you need to get the resource ID of the AKS cluster and the ID of the Microsoft Entra user account or group using the following steps:

- Get the cluster resource ID using the
command for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group. Provide your own cluster and resource group name as needed. - Use the
and`az account show`

commands to get your user ID.`az ad user show`

- Assign a role using the
command.`az role assignment create`


The following example assigns the *Azure Kubernetes Service Cluster Admin Role* to an individual user account:

```
# Get the resource ID of your AKS cluster
AKS_CLUSTER=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query id -o tsv)
# Get the account credentials for the logged in user
ACCOUNT_UPN=$(az account show --query user.name -o tsv)
ACCOUNT_ID=$(az ad user show --id $ACCOUNT_UPN --query objectId -o tsv)
# Assign the 'Cluster Admin' role to the user
az role assignment create \
--assignee $ACCOUNT_ID \
--scope $AKS_CLUSTER \
--role "Azure Kubernetes Service Cluster Admin Role"
```


If you want to assign permissions to a Microsoft Entra group, update the `--assignee`

parameter shown in the previous example with the object ID for the *group* rather than the *user*.

To get the object ID for a group, use the [ az ad group show](/en-us/cli/azure/ad/group#az-ad-group-show) command. The following command gets the object ID for the Microsoft Entra group named

*appdev*:

```
az ad group show --group appdev --query objectId -o tsv
```


Important

In some cases, such as Microsoft Entra guest users, the *user.name* in the account is different than the *userPrincipalName*.

```
$ az account show --query user.name -o tsv
user@contoso.com
$ az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv
user_contoso.com#EXT#@contoso.onmicrosoft.com
```


In this case, set the value of *ACCOUNT_UPN* to the *userPrincipalName* from the Microsoft Entra user. For example, if your account *user.name* is *user@contoso.com*, this action would look like the following example:

```
ACCOUNT_UPN=$(az ad user list --query "[?contains(otherMails,'user@contoso.com')].{UPN:userPrincipalName}" -o tsv)
```


## Get and verify the configuration information

Once the roles are assigned, use the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command to get the

*kubeconfig*definition for your AKS cluster. The following example gets the

*--admin*credentials, which works correctly if the user has been granted the

*Cluster Admin Role*:

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
```


You can then use the [ kubectl config view](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config) command to verify that the

*context*for the cluster shows that the admin configuration information has been applied.

```
$ kubectl config view
```


Your output should look similar to the following example output:

```
apiVersion: v1
clusters:
- cluster:
certificate-authority-data: DATA+OMITTED
server: https://myaksclust-myresourcegroup-19da35-4839be06.hcp.eastus.azmk8s.io:443
name: myAKSCluster
contexts:
- context:
cluster: myAKSCluster
user: clusterAdmin_myResourceGroup_myAKSCluster
name: myAKSCluster-admin
current-context: myAKSCluster-admin
kind: Config
preferences: {}
users:
- name: clusterAdmin_myResourceGroup_myAKSCluster
user:
client-certificate-data: REDACTED
client-key-data: REDACTED
token: e9f2f819a4496538b02cefff94e61d35
```


## Remove role permissions

To remove role assignments, use the [ az role assignment delete](/en-us/cli/azure/role/assignment#az-role-assignment-delete) command. Specify the account ID and cluster resource ID that you obtained in the previous steps. If you assigned the role to a group rather than a user, specify the appropriate group object ID rather than account object ID for the

`--assignee`

parameter.```
az role assignment delete --assignee $ACCOUNT_ID --scope $AKS_CLUSTER
```


## Next steps

For enhanced security on access to AKS clusters, [integrate Microsoft Entra authentication](azure-ad-integration-cli).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-monitoring-proactive -->

# Proactive monitoring best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers the best practices for proactive monitoring on Azure Kubernetes Service (AKS) and provides a comprehensive list of the key signals AKS recommends for you to monitor.

Proactively monitoring your AKS clusters is crucial for reducing downtime and saving business interruptions for your applications. This process involves identifying and monitoring key indicators of abnormal behavior in your cluster that might lead to major issues or downtime.

## Monitoring and alerting overview

Monitoring on AKS involves using metrics, logs, and events to ensure the health and performance of your cluster. Common scenarios to monitor include node performance, pod status, and overall resource utilization in your cluster. Logs provide insights into system events and cluster operations and activity. For more information about the methods and signals AKS provides for monitoring, see [Monitor Azure Kubernetes Service (AKS)](monitor-aks).

The best way to proactively monitor your cluster is to configure [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview). Alerts act as proactive measures to notify you of potential issues or anomalies before they escalate into critical problems. By defining thresholds for key metrics and logs, you receive immediate alerts when these signals exceed predefined limits, indicating potential issues like resource exhaustion or application failures. We highly recommend defining [service-level objectives (SLOs)](/en-us/azure/well-architected/reliability/metrics) for your application to measure the performance and reliability of your service. Configuring alerts on the key signals for your SLOs allows you to quickly detect any degradation of your application's quality of service that your customers receive. Overall, setting timely alerts enables you to quickly investigate and remediate problems, minimizing downtime and ensuring high availability of applications running on your AKS cluster.

## How to configure alerts on specific metric types

| Metric type | Where to find these metrics | How to configure alerts |
|---|---|---|
| AKS Platform Metric | View
|

[Create a metric alert for an Azure resource](/en-us/azure/azure-monitor/alerts/tutorial-metric-alert).[Azure Monitor and Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).[Azure Monitor managed service for Prometheus rule groups](/en-us/azure/azure-monitor/essentials/prometheus-rule-groups).[Azure activity logs for AKS](monitor-aks#azure-activity-log).[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts).**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**Virtual Machine Scale Set instance**that matches the name of your node pool you're creating alerts for.4. Navigate to the

**Alerts**blade to create your metric alert.**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**load balancer instance**to bring up the Azure portal page for load balancer.4. Navigate to the

**Alerts**page to create your load balancer metric alert.[Azure Monitor resource logs](monitor-aks#azure-monitor-resource-logs).[Create log search alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).## Critical signals for configuring alerts

To get holistic coverage of your AKS environment, you need to configure alerts on the three main components of your cluster:

**Cluster infrastructure**: Alerts targeting the underlying infrastructure of your cluster such as nodes, disks, and networking.**Application health**: Alerts for monitoring the health of your pods and applications. Some common indicators of unhealthy applications include out-of-memory kills (OOMKills) of your pods, pods in not ready state, etc.**Kubernetes control plane**: Alerts on AKS control plane to monitor the health and performance of the API server, etcd, and other components.

The following sections contain the key signals which we recommend all AKS customers monitor closely. The AKS team is working to add all critical signals to the existing [Recommended Alerts](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts) feature, which allows you to easily enable alerts for all signals with a one-click experience. The Prometheus metrics alerts are available in Public Preview today, and the remaining alerts are estimated to be available in early 2025. For now, you can manually configure alerts on the critical signals.

### Cluster infrastructure alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| Cluster is in a failed state | Azure Activity Logs | Create or update managed cluster | Status of the log is Failed, indicating that the cluster upgrade or creation action failed. |
| Node pool is in a failed state | Azure Activity Logs | Create or update agent pool | Status of the log is Failed, indicating that the node pool is in a Failed state due to a failed Create, Read, Upgrade, or Delete (CRUD) operation. |
| High Node OS Disk Bandwidth Usage | Virtual Machine Scale Set Metric | OS Disk Bandwidth Consumed Percentage | Node OS disk bandwidth utilization is above 95%. |
| High Node OS Disk IOPS Usage | Virtual Machine Scale Set Metric | OS Disk IOPS Consumed Percentage | Node OS disk IOPS utilization is above 95%. |
| High Node OS Disk Space Usage | AKS Platform Metric | Disk Used Percentage | Node OS disk space percentage utilization is above 90%. |
| High Node CPU Usage | AKS Platform Metric | CPU Usage Percentage | Node CPU Usage is greater than 90%. |
| High Node Memory Usage | AKS Platform Metric | Memory Working Set Percentage | Node Memory Usage is greater than 90%. |
| Node is in NotReady state | AKS Platform Metric | Status for various node conditions | Node is in NotReady state for >20 minutes. |
| SNAT port exhaustion | Load Balancer (LB) Metric | SNAT Connection Count | Filter for Connection State = "Failed" |

### Application health alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| High number of unhealthy pods | Azure Managed Prometheus Metric | Alert name: KubePodReadyStateLow | Available as an AKS recommended alert. To enable this alert, see
|

[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).### Kubernetes control plane alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| ETCD is Filled Up | Azure Managed Prometheus Metric | etcd_mvcc_db_total_size_in_use_in_bytes | ETCD utilization is greater than 2 GB |
| API Server Too Many Requests Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error code 429 |
| API Server Webhook and Tunnel Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error codes 500 and 503 |

## Next steps

For more information about monitoring on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-azure-cni-pod-subnet -->

# Azure Container Networking Interface (CNI) Pod Subnet

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Pod Subnet assigns IP addresses to pods from a separate subnet from your cluster Nodes. This feature is available in two modes: Dynamic IP Allocation and Static Block Allocation.

## Prerequisites

Note

When using Static Block Allocation of CIDRs, exposing an application as a Private Link Service using a Kubernetes Load Balancer Service isn't supported.

- Review the
[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article. - Review the
[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply. - AKS Engine and DIY clusters aren't supported.
- Azure CLI version
`2.37.0`

or later and the`aks-preview`

extension version`2.0.0b2`

or later. - Register the subscription-level feature flag for your subscription: 'Microsoft.ContainerService/AzureVnetScalePreview'.

## Dynamic IP allocation mode

Dynamic IP allocation helps mitigate pod IP address exhaustion issues by allocating pod IPs from a subnet that's separate from the subnet hosting the AKS cluster.

The Dynamic IP Allocation mode offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned VNet IPs, they have direct connectivity to other cluster pods and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios, such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using network security groups (NSGs) to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this mode.

### Plan IP addressing

With Dynamic IP Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster, as the nodes request 16 IPs on startup and request another batch of 16 anytime there are <8 IPs unallocated in their allotment.

IP address planning for Kubernetes services and Docker Bridge remain unchanged.

## Static block allocation mode

Static block allocation helps mitigate potential pod subnet sizing and Azure address mapping limitations by assigning CIDR blocks to nodes rather than individual IPs.

The Static Block Allocation mode offers the following benefits:

**Better IP scalability**: CIDR blocks are statically allocated to the cluster nodes and are present for the lifetime of the node, as opposed to the traditional dynamic allocation of individual IPs with traditional CNI. This enables routing based on CIDR blocks and helps scale the cluster limit up to 1 million pods from the traditional 65K pods per cluster. Your Azure Virtual Network must be large enough to accommodate the scale of your cluster.**Flexibility**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pods and resources in the VNet.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Cilium, Azure NPM, and Calico work with this solution.

### Limitations

Below are some of the limitations of using Azure CNI Static Block allocation:

- Minimum Kubernetes Version required is 1.28.
- Maximum subnet size supported is x.x.x.x/12 ~ 1 million IPs.
- Only a single mode of operation can be used per subnet. If a subnet uses Static Block allocation mode, it cannot use Dynamic IP allocation mode in a different cluster or node pool with the same subnet and vice versa.
- Only supported in new clusters or when adding node pools with a different subnet to existing clusters. Migrating or updating existing clusters or node pools is not supported.
- Across all the CIDR blocks assigned to a node in the node pool, one IP will be selected as the primary IP of the node. Thus, for network administrators selecting the
`--max-pods`

value try to use the calculation below to best serve your needs and have optimal usage of IPs in the subnet:

`max_pods = (N * 16) - 1`

where `N`

is any positive integer and `N`

> 0

### Plan IP addressing

With Static Block Allocation, nodes and pods scale independently, so you can plan their address spaces separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

CIDR blocks of /28 (16 IPs) are allocated to nodes based on your `--max-pods`

configuration for your node pool, which defines the maximum number of pods per node. 1 IP is reserved on each node from all the available IPs on that node for internal purposes.

While planning your IPs, it's important to define your `--max-pods`

configuration using the following calculation: `max_pods_per_node = (16 * N) - 1`

, where `N`

is any positive integer greater than `0`

.

Ideal values with no IP wastage would require the max pods value to conform to the above expression.

See the following example cases:

Note

The examples assume /28 CIDR blocks (16 IPs each).

| Example case | `max_pods` |
CIDR Blocks allocated per node | Total IP available for pods | IP wastage for node |
|---|---|---|---|---|
| Low wastage (acceptable) | 30 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 30 = 1 |
| Ideal case | 31 | 2 | (16 * 2) - 1 = 32 - 1 = 31 | 31 - 31 = 0 |
| High wastage (not recommended) | 32 | 3 | (16 * 3) - 1 = 48 - 1 = 47 | 47 - 32 = 15 |

IP address planning for Kubernetes services remains unchanged.

Note

Ensure your VNet has a sufficiently large and contiguous address space to support your cluster's scale.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spark-job -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/integrations -->

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
