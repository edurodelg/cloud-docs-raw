---
merged_at: 2026-01-28T07:16:09.839561
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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-health-monitoring -->

# GPU health monitoring in Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how Azure Kubernetes Service (AKS) uses Node Problem Detector (NPD) to monitor the health of GPU-enabled node pools. NPD is a Kubernetes component that detects and reports node-level issues, including hardware faults, driver errors, and connectivity problems that can affect the performance and availability of GPU workloads.

## About GPU health monitoring in NPD

AKS supports GPU health monitoring through [Node Problem Detector (NPD)](node-problem-detector), enabling automatic detection and reporting of issues that affect GPU-enabled node pools on an AKS cluster. GPU health monitoring helps Kubernetes operators keep GPU nodes healthy and performant by surfacing hardware faults, communication failures, and system-level errors. NPD sets GPU-related node conditions and enable platform engineering teams to take action before issues impact application performance or availability.

These health signals are vital for ensuring optimal performance and reliability across a range of GPU workloads, including:

- Machine learning (ML) training and inference.
- AI model development.
- High-performance computing (HPC).
- Graphics rendering and data-intensive simulations.

## Limitations

AKS Node Problem Detector * does not* run GPU health checks on node pools with

`--gpu-driver none`

, where **self-managed**or custom GPU driver was installed on the nodes.

## Supported GPU health checks

NPD regularly monitors GPU-enabled node pools and sets conditions when anomalies are detected. The following GPU health checks are currently supported:

**GPUMissing**: NPD verifies that the number of GPUs detected by the`nvidia-smi`

utility matches the expected GPU count for the VM SKU assigned to the node.- A mismatch might indicate a hardware fault, driver issue, or misconfiguration. Accurate GPU enumeration is critical for ensuring scheduling accuracy and workload availability on GPU nodes.

**GPUXIDErrors**: Checks for XID (eXecution ID) errors emitted by the GPU driver in the kernel logs. XID errors are low-level GPU faults that typically occur when:- The driver misprograms the GPU.
- There's a corruption in the command stream sent to the GPU.
- A hardware failure or instability affects GPU operation.

For more information, see

[XID errors on NVIDIA GPUs](https://docs.nvidia.com/deploy/xid-errors/index.html).**NVLink Status**: For NVIDIA VM SKUs that support NVLink, this condition confirms that NVLink is active and functioning.- NVLink is a high-speed interconnect used to facilitate data transfer between multiple GPUs.
- If NVLink is inactive or degraded, multi-GPU workloads might experience reduced performance or communication bottlenecks.

For more information, see

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/).**InfiniBand Link Flapping**: NPD monitors for InfiniBand (IB) link flapping, or intermittent connectivity of the IB network device.- Link flapping shouldn't occur under normal operating conditions and might result in degraded inter-node communication for distributed workloads.
- It can also signal physical layer issues, misconfigured firmware, or driver instability.

**NVIDIA GRID Driver License Check**: For NVIDIA VM SKUs that support GRID driver, this condition verifies license status of the installed GRID driver on[supported NVIDIA VM SKUs](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series).- Invalid might indicate the installed GRID driver is not licensed.


## Frequently asked questions

### Does Node Problem Detector (NPD) automatically remediate GPU node issues?

NPD doesn't take direct action to remediate GPU-enabled node issues. NPD detects and reports problems by publishing Kubernetes node conditions and events. Any remediation (for example: draining a node, restarting workloads, or replacing faulty hardware) must be handled manually, through external automation, or alerting systems configured by the Kubernetes operator.

### On which Azure VM sizes does AKS conduct GPU health monitoring through NPD?

Currently, NPD conducts health checks on GPU nodes provisioned with the `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size on AKS. Also on [A10 SKU](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series) for GRID Driver License checks.

### Does NPD monitor the health of multi-instance GPU (MIG) node pools?

Yes, NPD health monitoring is supported on [MIG-enabled AKS node pools](gpu-multi-instance).

## Next steps

- Provision GPUs on
[Linux](use-nvidia-gpu)or[Windows](use-windows-gpu)node pools in your AKS cluster. - Learn more about the
[types of node conditions and events](node-problem-detector)set by NPD on AKS. [Monitor general GPU metrics](monitor-gpu-metrics)using a self-managed metrics exporter.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-extensions -->

# Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cluster extensions provide an Azure Resource Manager driven experience for installation and lifecycle management of services like Azure Machine Learning or Kubernetes applications on an AKS cluster. This feature enables:

- Azure Resource Manager-based deployment of extensions, including at-scale deployments across AKS clusters.
- Lifecycle management of the extension (Update, Delete) from Azure Resource Manager.

## Categories of cluster extensions

There are two categories of cluster extensions, *Core* and *Standard* that can be deployed onto AKS clusters.

### Core extensions

Core Kubernetes extensions have broader region availability, a more integrated AKS experience, and release alignment to AKS version releases. Azure Backup is a core extension.

#### AKS native experience

Core extensions can be managed using `az aks`

CLI command.

```
az aks extension create \
--name <core extension name> \
--extension-type <type> \
--cluster-name <name> \
--resource-group <group>
```


For more information about the commands, see [ az aks](/en-us/cli/azure/aks).

#### Release policy

Minor and major upgrades of core extensions occur alongside AKS minor and major version updates to avoid introducing breaking changes and provide better reliability.

### Standard extensions

For information about the other cluster extensions, see the table in [Currently available extensions](cluster-extensions#currently-available-extensions) and the [Kubernetes apps](deploy-marketplace) deployed via Azure Marketplace are of the Standard Extension type.

Standard extensions can be managed using the `az k8s-extension`

CLI command. For more information, see [Deploy and manage cluster extensions by using Azure CLI](deploy-extensions-az-cli).

```
az k8s-extension create \
--name <standard extension name> \
--extension-type <extension-type> \
--scope cluster \
--cluster-name <clusterName> \
--resource-group <resourceGroupName> \
--cluster-type managedClusters
```


## Cluster extension requirements

The cluster extensions platform is supported in all regions where AKS is deployed, except Qatar Central and US air gapped clouds. Although the platform is available in all regions, check the region availability for individual extensions.

Important

Ensure that your AKS cluster is created with a managed identity, as cluster extensions don't work with service principal-based clusters.

For new clusters created with `az aks create`

, managed identity is configured by default. For existing service principal-based clusters that need to be switched over to managed identity, it can be enabled by running `az aks update`

with the `--enable-managed-identity`

flag. For more information, see [Use managed identity](use-managed-identity).

Note

If you enabled [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) on your AKS cluster or are considering implementing it,
we recommend you first review [Workload identity overview](workload-identity-overview) to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.
The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.

## Currently available extensions

| Extension | Description |
|---|---|
|

`Dapr`

is a portable, event-driven runtime that makes it easy for any developer to build resilient, stateless, and stateful applications that run on cloud and edge.[Azure App Configuration](azure-app-configuration-quickstart)[Azure Machine Learning](/en-us/azure/machine-learning/how-to-attach-kubernetes-anywhere)[Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/conceptual-gitops-flux2)[supported versions of Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/extensions-release#flux-gitops)and[Tutorial: Deploy applications using GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2).[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)[Azure Backup for AKS](/en-us/azure/backup/azure-kubernetes-service-backup-overview)You can also [select and deploy Kubernetes applications available through Marketplace](deploy-marketplace).

Note

Cluster extensions provide a platform for different extensions to be installed and managed on an AKS cluster. If you're facing issues while using any of these extensions, open a support ticket with the respective service.

## Next steps

- Learn how to
[deploy cluster extensions by using Azure CLI](deploy-extensions-az-cli). - Read about
[cluster extensions](/en-us/azure/azure-arc/kubernetes/conceptual-extensions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices -->

# Cluster operator and developer best practices to build and manage applications on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Building and running applications successfully in Azure Kubernetes Service (AKS) requires understanding and implementation of some key concepts, including:

- Multi-tenancy and scheduler features.
- Cluster and pod security.
- Business continuity and disaster recovery.

The AKS product group, engineering teams, and field teams (including global black belts (GBBs)) contributed to, wrote, and grouped the following best practices and conceptual articles. Their purpose is to help cluster operators and developers better understand the concepts above and implement the appropriate features.

## Cluster operator best practices

If you're a cluster operator, work with application owners and developers to understand their needs. Then, you can use the following best practices to configure your AKS clusters to fit your needs.

An important practice that you should include as part of your application development and deployment process is remembering to follow commonly used deployment and testing patterns. Testing your application before deployment is an important step to ensure its quality, functionality, and compatibility with the target environment. It can help you identify and fix any errors, bugs, or issues that might affect the performance, security, or usability of the application or underlying infrastructure.

### Multi-tenancy

[Best practices for cluster isolation](operator-best-practices-cluster-isolation)- Includes multi-tenancy core components and logical isolation with namespaces.

[Best practices for basic scheduler features](operator-best-practices-scheduler)- Includes using resource quotas and pod disruption budgets.

[Best practices for advanced scheduler features](operator-best-practices-advanced-scheduler)- Includes using taints and tolerations, node selectors and affinity, and inter-pod affinity and anti-affinity.

[Best practices for authentication and authorization](operator-best-practices-identity)- Includes integration with Microsoft Entra ID, using Kubernetes role-based access control (Kubernetes RBAC), using Azure RBAC, and pod identities.


### Security

[Best practices for cluster security and upgrades](operator-best-practices-cluster-security)- Includes securing access to the API server, limiting container access, and managing upgrades and node reboots.

[Best practices for container image management and security](operator-best-practices-container-image-management)- Includes securing the image and runtimes and automated builds on base image updates.

[Best practices for pod security](developer-best-practices-pod-security)- Includes securing access to resources, limiting credential exposure, and using pod identities and digital key vaults.


### Network and storage

[Best practices for network connectivity](operator-best-practices-network)- Includes different network models, using ingress and web application firewalls (WAF), and securing node SSH access.

[Best practices for storage and backups](operator-best-practices-storage)- Includes choosing the appropriate storage type and node size, dynamically provisioning volumes, and data backups.


### Running enterprise-ready workloads

[Best practices for business continuity and disaster recovery](operator-best-practices-multi-region)- Includes using region pairs, multiple clusters with Azure Traffic Manager, and geo-replication of container images.


## Developer best practices

If you're a developer or application owner, you can simplify your development experience and define required application performance features.

[Best practices for application developers to manage resources](developer-best-practices-resource-management)- Includes defining pod resource requests and limits, configuring development tools, and checking for application issues.

[Best practices for pod security](developer-best-practices-pod-security)- Includes securing access to resources, limiting credential exposure, and using pod identities and digital key vaults.

[Best practices for deployment and cluster reliability](best-practices-app-cluster-reliability)- Includes deployment, cluster, and node pool level best practices.


## Kubernetes and AKS concepts

The following conceptual articles cover some of the fundamental features and components for clusters in AKS:

[Kubernetes core concepts](concepts-clusters-workloads)[Access and identity](concepts-identity)[Security concepts](concepts-security)[Network concepts](concepts-network)[Storage options](concepts-storage)[Scaling options](concepts-scale)

## Next steps

For guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/events -->

# Use Kubernetes events for troubleshooting in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Kubernetes events to monitor and troubleshoot issues in your Azure Kubernetes Service (AKS) clusters.

## What are Kubernetes events?

Events are one of the most prominent sources for monitoring and troubleshooting issues in Kubernetes. They capture and record information about the lifecycle of various Kubernetes objects, such as pods, nodes, services, and deployments. By monitoring events, you can gain visibility into your cluster's activities, identify issues, and troubleshoot problems effectively.

Kubernetes events don't persist throughout your cluster lifecycle, as there's no retention mechanism. Events are **only available for one hour after the event is generated**. To store events for a longer time period, enable

[Container insights](/en-us/azure/azure-monitor/containers/container-insights-enable-aks).

## Kubernetes event objects

The following table lists some key Kubernetes event objects:

| Field name | Description |
|---|---|
| type | The type is based on the severity of the event:Warning events signal potentially problematic situations, such as a pod repeatedly failing or a node running out of resources. They require attention, but might not result in immediate failure.Normal events represent routine operations, such as a pod being scheduled or a deployment scaling up. They usually indicate healthy cluster behavior. |
| reason | The reason why the event was generated. For example, FailedScheduling or CrashLoopBackoff. |
| message | A human-readable message that describes the event. |
| namespace | The namespace of the Kubernetes object that the event is associated with. |
| firstSeen | Timestamp when the event was first observed. |
| lastSeen | Timestamp of when the event was last observed. |
| reportingController | The name of the controller that reported the event. For example, `kubernetes.io/kubelet` . |
| object | The name of the Kubernetes object that the event is associated with. |

For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/event-v1/).

## View Kubernetes events

List all events in your cluster using the `kubectl get events`

command.

Assuming your cluster is already created and available (per doc prerequisites), get credentials (note the `--overwrite-existing`

flag is set to avoid kubeconfig errors):

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --overwrite-existing
```


Now list all events in your cluster:

```
kubectl get events
```


Results:

```
LAST SEEN TYPE REASON OBJECT MESSAGE
xxm Normal Scheduled pod/my-pod-xxxxx Successfully assigned default/my-pod-xxxxx to aks-nodepoolxx-xxxxxxx-vmss000000
xxm Normal Pulled pod/my-pod-xxxxx Container image "nginx" already present on machine
xxm Normal Created pod/my-pod-xxxxx Created container nginx
xxm Normal Started pod/my-pod-xxxxx Started container nginx
...
```


Look at a specific pod's events by first finding the name of the pod and then using the `kubectl describe pod`

command.

List the pods in the current namespace:

```
kubectl get pods
```


Results:

```
NAME READY STATUS RESTARTS AGE
my-pod-xxxxx 1/1 Running 0 xxm
nginx-deployment-xxxxx 1/1 Running 0 xxm
...
```


Replace `<pod-name>`

below with your actual pod name. For automation, here's an example for the first pod in the list:

```
POD_NAME=$(kubectl get pods -o jsonpath="{.items[0].metadata.name}")
kubectl describe pod $POD_NAME
```


## Best practices for troubleshooting with events

### Filtering events for relevance

You might have various namespaces and services running in your AKS cluster. Filtering events based on object type, namespace, or reason can help narrow down the results to the most relevant information.

For example, you can use the following command to filter events within the default namespace:

```
kubectl get events --namespace default
```


### Automating event notifications

To ensure timely response to critical events in your AKS cluster, set up automated notifications. Azure offers integration with monitoring and alerting services like [Azure Monitor](monitor-aks). You can configure alerts to trigger based on specific event patterns. This way, you're immediately informed about crucial issues that require attention.

### Regularly reviewing events

Make a habit of regularly reviewing events in your AKS cluster. This proactive approach can help you identify trends, catch potential problems early, and prevent escalations. By staying on top of events, you can maintain the stability and performance of your applications.

## Next steps

Now that you understand Kubernetes events, you can continue your monitoring and observability journey by [enabling Container insights](/en-us/azure/azure-monitor/containers/container-insights-enable-aks).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/validate-postgresql-ha -->

# Validate and test a PostgreSQL database deployment on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you perform various testing and validation steps on a PostgreSQL database deployed on AKS. This includes verifying the deployment, connecting to the database, and testing failover scenarios.

- If you haven't already deployed PostgreSQL, follow the steps in
[Deploy a highly available PostgreSQL database on AKS with Azure CLI](deploy-postgresql-ha)to get set up, and then you can return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Inspect the deployed PostgreSQL cluster

Validate that PostgreSQL is spread across multiple availability zones by retrieving the AKS node details using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl get nodes \
--context $AKS_PRIMARY_CLUSTER_NAME \
--namespace $PG_NAMESPACE \
--output json | jq '.items[] | {node: .metadata.name, zone: .metadata.labels."failure-domain.beta.kubernetes.io/zone"}'
```


Your output should resemble the following example output with the availability zone shown for each node:

```
{
"node": "aks-postgres-15810965-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-postgres-15810965-vmss000001",
"zone": "westus3-2"
}
{
"node": "aks-postgres-15810965-vmss000002",
"zone": "westus3-3"
}
{
"node": "aks-systempool-26112968-vmss000000",
"zone": "westus3-1"
}
{
"node": "aks-systempool-26112968-vmss000001",
"zone": "westus3-2"
}
```


## Connect to PostgreSQL and create a sample dataset

In this section, you create a table and insert some data into the app database that was created in the CNPG Cluster CRD you deployed earlier. You use this data to validate the backup and restore operations for the PostgreSQL cluster.

Create a table and insert data into the app database using the following commands:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`-- Create a small dataset CREATE TABLE datasample (id INTEGER, name VARCHAR(255)); INSERT INTO datasample (id, name) VALUES (1, 'John'); INSERT INTO datasample (id, name) VALUES (2, 'Jane'); INSERT INTO datasample (id, name) VALUES (3, 'Alice'); SELECT COUNT(*) FROM datasample;`

Type

`\q`

to exit psql when finished.Your output should resemble the following example output:

`CREATE TABLE INSERT 0 1 INSERT 0 1 INSERT 0 1 count ------- 3 (1 row)`


## Connect to PostgreSQL read-only replicas

Connect to the PostgreSQL read-only replicas and validate the sample dataset using the following commands:

`kubectl cnpg psql --replica $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

`SELECT pg_is_in_recovery();`

Example output

`pg_is_in_recovery ------------------- t (1 row)`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row)`


## Set up on-demand and scheduled PostgreSQL backups using Barman

Note

CloudNativePG is expected to deprecate native Barman Cloud support in favor of the [Barman Cloud plugin](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) in an upcoming 1.29 release. The steps in this guide continue to work today, but plan to migrate to the plugin once it stabilizes.

Validate that the PostgreSQL cluster can access the Azure storage account specified in the CNPG Cluster CRD and that

`Working WAL archiving`

reports as`OK`

using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: Not Available Working WAL archiving: OK WALs waiting to be archived: 0 Last Archived WAL: 00000001000000000000000A @ 2024-07-09T17:18:13.982859Z Last Failed WAL: -`

Deploy an on-demand backup to Azure Storage, which uses the AKS workload identity integration, using the YAML file with the

command.`kubectl apply`

`export BACKUP_ONDEMAND_NAME="on-demand-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Backup metadata: name: $BACKUP_ONDEMAND_NAME spec: method: barmanObjectStore cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the on-demand backup using the

command.`kubectl describe`

`kubectl describe backup $BACKUP_ONDEMAND_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Type Reason Age From Message ---- ------ ---- ---- ------- Normal Starting 6s cloudnative-pg-backup Starting backup for cluster pg-primary-cnpg-r8c7unrw Normal Starting 5s instance-manager Backup started Normal Completed 1s instance-manager Backup completed`

Validate that the cluster has a first point of recoverability using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Example output

`Continuous Backup status First Point of Recoverability: 2024-06-05T13:47:18Z Working WAL archiving: OK`

Configure a scheduled backup for

*every hour at 15 minutes past the hour*using the YAML file with thecommand.`kubectl apply`

`export BACKUP_SCHEDULED_NAME="scheduled-backup-1" cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: ScheduledBackup metadata: name: $BACKUP_SCHEDULED_NAME spec: # Backup once per hour schedule: "0 15 * ? * *" backupOwnerReference: self cluster: name: $PG_PRIMARY_CLUSTER_NAME EOF`

Validate the status of the scheduled backup using the

command.`kubectl describe`

`kubectl describe scheduledbackup $BACKUP_SCHEDULED_NAME \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

View the backup files stored on Azure blob storage for the primary cluster using the

command.`az storage blob list`

`az storage blob list \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --container-name backups \ --query "[*].name" \ --only-show-errors`

Your output should resemble the following example output, validating the backup was successful:

`[ "pg-primary-cnpg-r8c7unrw/base/20240605T134715/backup.info", "pg-primary-cnpg-r8c7unrw/base/20240605T134715/data.tar", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000001", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000002", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000003.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000004", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000005.00000028.backup", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000006", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000007", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000008", "pg-primary-cnpg-r8c7unrw/wals/0000000100000000/000000010000000000000009" ]`


## Restore the on-demand backup to a new PostgreSQL cluster

In this section, you restore the on-demand backup you created earlier using the CNPG operator into a new instance using the bootstrap Cluster CRD. A single instance cluster is used for simplicity. Remember that the AKS workload identity (via CNPG inheritFromAzureAD) accesses the backup files, and that the recovery cluster name is used to generate a new Kubernetes service account specific to the recovery cluster.

You also create a second federated credential to map the new recovery cluster service account to the existing UAMI that has "Storage Blob Data Contributor" access to the backup files on blob storage.

Create a second federated identity credential using the

command.`az identity federated-credential create`

`export PG_PRIMARY_CLUSTER_NAME_RECOVERED="$PG_PRIMARY_CLUSTER_NAME-recovered-db" az identity federated-credential create \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME_RECOVERED}" \ --audience api://AzureADTokenExchange`

Restore the on-demand backup using the Cluster CRD with the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME_RECOVERED spec: inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 1 affinity: nodeSelector: workload: postgres # Point to cluster backup created earlier and stored on Azure Blob Storage bootstrap: recovery: source: clusterBackup storage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem walStorage: size: 2Gi pvcTemplate: accessModes: - ReadWriteOnce resources: requests: storage: 2Gi storageClassName: managed-csi-premium volumeMode: Filesystem serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" externalClusters: - name: clusterBackup barmanObjectStore: destinationPath: https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups serverName: $PG_PRIMARY_CLUSTER_NAME azureCredentials: inheritFromAzureAD: true wal: maxParallel: 8 EOF`

Connect to the recovered instance, then validate that the dataset created on the original cluster where the full backup was taken is present using the following command:

`kubectl cnpg psql $PG_PRIMARY_CLUSTER_NAME_RECOVERED --namespace $PG_NAMESPACE`

`SELECT COUNT(*) FROM datasample;`

Example output

`count ------- 3 (1 row) Type \q to exit psql`

Delete the recovered cluster using the following command:

`kubectl cnpg destroy $PG_PRIMARY_CLUSTER_NAME_RECOVERED 1 \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE`

Delete the federated identity credential using the

command.`az identity federated-credential delete`

`az identity federated-credential delete \ --name $PG_PRIMARY_CLUSTER_NAME_RECOVERED \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --yes`


## Expose the PostgreSQL cluster using a public load balancer

In this section, you configure the necessary infrastructure to publicly expose the PostgreSQL read-write and read-only endpoints with IP source restrictions to the public IP address of your client workstation.

You also retrieve the following endpoints from the Cluster IP service:

*One*primary read-write endpoint that ends with`*-rw`

.*Zero to N*(depending on the number of replicas) read-only endpoints that end with`*-ro`

.*One*replication endpoint that ends with`*-r`

.

Get the Cluster IP service details using the

command.`kubectl get`

`kubectl get services \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE \ -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE pg-primary-cnpg-sryti1qf-r ClusterIP 10.0.193.27 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-ro ClusterIP 10.0.237.19 <none> 5432/TCP 3h57m pg-primary-cnpg-sryti1qf-rw ClusterIP 10.0.244.125 <none> 5432/TCP 3h57m`

Note

There are three services:

`namespace/cluster-name-ro`

mapped to port 5433,`namespace/cluster-name-rw`

, and`namespace/cluster-name-r`

mapped to port 5433. It’s important to avoid using the same port as the read/write node of the PostgreSQL database cluster. If you want applications to access only the read-only replica of the PostgreSQL database cluster, direct them to port 5433. The final service is typically used for data backups but can also function as a read-only node.Get the service details using the

command.`kubectl get`

`export PG_PRIMARY_CLUSTER_RW_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-rw")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RW_SERVICE export PG_PRIMARY_CLUSTER_RO_SERVICE=$(kubectl get services \ --namespace $PG_NAMESPACE \ --context $AKS_PRIMARY_CLUSTER_NAME \ -l "cnpg.io/cluster" \ --output json | jq -r '.items[] | select(.metadata.name | endswith("-ro")) | .metadata.name') echo $PG_PRIMARY_CLUSTER_RO_SERVICE`

Configure the load balancer service with the following YAML files using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-rw namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5432 targetPort: 5432 selector: cnpg.io/instanceRole: primary cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -f - apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: $AKS_PRIMARY_CLUSTER_NODERG_NAME service.beta.kubernetes.io/azure-pip-name: $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX name: cnpg-cluster-load-balancer-ro namespace: "${PG_NAMESPACE}" spec: type: LoadBalancer ports: - protocol: TCP port: 5433 targetPort: 5432 selector: cnpg.io/instanceRole: replica cnpg.io/podRole: instance loadBalancerSourceRanges: - "$MY_PUBLIC_CLIENT_IP/32" EOF`

Get the service details using the

command.`kubectl describe`

`kubectl describe service cnpg-cluster-load-balancer-rw \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE kubectl describe service cnpg-cluster-load-balancer-ro \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_NAMESPACE export AKS_PRIMARY_CLUSTER_ALB_DNSNAME="$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query "dnsSettings.fqdn" --output tsv)" echo $AKS_PRIMARY_CLUSTER_ALB_DNSNAME`


### Validate public PostgreSQL endpoints

In this section, you validate that the Azure Load Balancer is properly set up using the static IP that you created earlier and routing connections to the primary read-write and read-only replicas and use the psql CLI to connect to both.

Remember that the primary read-write endpoint maps to TCP port 5432 and the read-only replica endpoints map to port 5433 to allow the same PostgreSQL DNS name to be used for readers and writers.

Note

You need the value of the app user password for PostgreSQL basic auth that was generated earlier and stored in the `$PG_DATABASE_APPUSER_SECRET`

environment variable.

Validate the public PostgreSQL endpoints using the following

`psql`

commands:`echo "Public endpoint for PostgreSQL cluster: $AKS_PRIMARY_CLUSTER_ALB_DNSNAME" # Query the primary, pg_is_in_recovery = false psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5432 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`pg_is_in_recovery ------------------- f (1 row)`

`echo "Query a replica, pg_is_in_recovery = true" psql -h $AKS_PRIMARY_CLUSTER_ALB_DNSNAME \ -p 5433 -U app -d appdb -W -c "SELECT pg_is_in_recovery();"`

Example output

`# Example output pg_is_in_recovery ------------------- t (1 row)`

When successfully connected to the primary read-write endpoint, the PostgreSQL function returns

`f`

for*false*, indicating that the current connection is writable.When connected to a replica, the function returns

`t`

for*true*, indicating the database is in recovery and read-only.

## Simulate an unplanned failover

In this section, you trigger a sudden failure by deleting the pod running the primary, which simulates a sudden crash or loss of network connectivity to the node hosting the PostgreSQL primary.

Check the status of the running pod instances using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Delete the primary pod using the

command.`kubectl delete`

`PRIMARY_POD=$(kubectl get pod \ --namespace $PG_NAMESPACE \ --no-headers \ -o custom-columns=":metadata.name" \ -l role=primary) kubectl delete pod $PRIMARY_POD --grace-period=1 --namespace $PG_NAMESPACE`

Validate that the

`pg-primary-cnpg-sryti1qf-2`

pod instance is now the primary using the following command:`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`pg-primary-cnpg-sryti1qf-2 0/9000060 Primary OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-1 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`

Reset the

`pg-primary-cnpg-sryti1qf-1`

pod instance as the primary using the following command:`kubectl cnpg promote $PG_PRIMARY_CLUSTER_NAME 1 --namespace $PG_NAMESPACE`

Validate that the pod instances have returned to their original state before the unplanned failover test using the following command:

`kubectl cnpg status $PG_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE`

Example output

`Name Current LSN Rep role Status Node --------------------------- ----------- -------- ------- ----------- pg-primary-cnpg-sryti1qf-1 0/9000060 Primary OK aks-postgres-32388626-vmss000000 pg-primary-cnpg-sryti1qf-2 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000001 pg-primary-cnpg-sryti1qf-3 0/9000060 Standby (sync) OK aks-postgres-32388626-vmss000002`


## Clean up resources

Once you're finished reviewing your deployment, delete all the resources you created in this guide using the

command.`az group delete`

`az group delete --resource-group $RESOURCE_GROUP_NAME --no-wait --yes`


## Next steps

In this how-to guide, you learned how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the CNPG operator.
- Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to the PostgreSQL database.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform a backup and restore of the PostgreSQL database.

To learn more about how you can use AKS for your workloads, see [What is Azure Kubernetes Service (AKS)?](what-is-aks) To learn more about Azure Database for PostgreSQL, see [What is Azure Database for PostgreSQL?](/en-us/azure/postgresql/flexible-server/overview)

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-configuration -->

# Advanced NGINX ingress controller and ingress configurations with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article walks you through two ways to configure ingress controllers and ingress objects with the application routing add-on for Azure Kubernetes Service (AKS):

[Configuration of the NGINX ingress controller](#control-the-default-nginx-ingress-controller-configuration)such as creating multiple controllers, configuring private load balancers, and setting static IP addresses.[Configuration per ingress resource](#configuration-per-ingress-resource-through-annotations)through annotations.

## Prerequisites

- An AKS cluster with the
[application routing add-on](app-routing)enabled. `kubectl`

configured to connect to your AKS cluster. For more information, see[Connect to your AKS cluster](#connect-to-your-aks-cluster).

### Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Configuration properties for NGINX ingress controllers

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://github.com/Azure/aks-app-routing-operator/blob/main/config/crd/bases/approuting.kubernetes.azure.com_nginxingresscontrollers.yaml) to configure NGINX ingress controllers. You can create more ingress controllers or modify existing configurations.

The following table lists properties you can set to configure an `NginxIngressController`

:

| Field | Type | Description | Required | Default |
|---|---|---|---|---|
`controllerNamePrefix` |
string | Name for the managed NGINX Ingress Controller resources. | Yes | `nginx` |
`customHTTPErrors` |
array | Array of error codes to be sent to the default backend if there's an error. | No | |
`defaultBackendService` |
object | Service to route unmatched HTTP traffic. Contains nested properties: | No | |
`name` |
string | Service name. | Yes | |
`namespace` |
string | Service namespace. | Yes | |
`defaultSSLCertificate` |
object | Contains the default certificate for accessing the default backend service. Contains nested properties: | No | |
`forceSSLRedirect` |
boolean | Forces HTTPS redirection when a certificate is set. | No | `false` |
`keyVaultURI` |
string | URI for a Key Vault secret storing the certificate. | No | |
`secret` |
object | Holds secret information for the default SSL certificate. Contains nested properties: | No | |
`name` |
string | Secret name. | Yes | |
`namespace` |
string | Secret namespace. | Yes | |
`httpDisabled` |
boolean | Flag to disable HTTP traffic to the controller. | No | |
`ingressClassName` |
string | IngressClass name used by the controller. | Yes | `nginx.approuting.kubernetes.azure.com` |
`loadBalancerAnnotations` |
object | A map of annotations to control the behavior of the NGINX ingress controller's service by setting
|

`scaling`

`maxReplicas`

`100`

`minReplicas`

`2`

`threshold`

**scales quickly for sudden spikes,**`rapid`

**favors cost-effectiveness, and**`steady`

**is a mix.**`balanced`

`balanced`

## Control the default NGINX ingress controller configuration

When you enable the application routing add-on with NGINX, it creates an ingress controller called `default`

in the `app-routing-namespace`

configured with a public facing Azure load balancer. That ingress controller uses an ingress class name of `webapprouting.kubernetes.azure.com`

.

You can also control if the default gets a public or an internal IP, or if it gets created at all when enabling the add-on.

Possible configuration options include:

: The default NGINX ingress controller isn't created and isn't deleted if it already exists. You should manually delete the default`None`

`NginxIngressController`

custom resource if desired.: The default NGINX ingress controller is created with an internal load balancer. Any annotation changes on the`Internal`

`NginxIngressController`

custom resource to make it external are overwritten.: The default NGINX ingress controller created with an external load balancer. Any annotation changes on the`External`

`NginxIngressController`

custom resource to make it internal are overwritten.(default): The default NGINX ingress controller is created with an external load balancer. You can edit the default`AnnotationControlled`

`NginxIngressController`

custom resource to configure load balancer annotations.)

### Control the default ingress controller configuration on a new cluster

Enable application routing on a new cluster using the

command with the`az aks create`

`--enable-app-routing`

and`--app-routing-default-nginx-controller`

flags. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --enable-app-routing \ --app-routing-default-nginx-controller <DefaultIngressControllerType>`


### Update the default ingress controller configuration on an existing cluster

Update the application routing default ingress controller configuration on an existing cluster using the

command with the`az aks approuting update`

`--nginx`

flag. You need to set the`<DefaultIngressControllerType>`

to one of the configuration options described in[Control the default NGINX ingress controller configuration](#control-the-default-nginx-ingress-controller-configuration).`az aks approuting update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --nginx <DefaultIngressControllerType>`


## Create another public facing NGINX ingress controller

Copy the following YAML manifest into a new file named

`nginx-public-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-public spec: ingressClassName: nginx-public controllerNamePrefix: nginx-public`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-public-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-public created`


## Create an internal NGINX ingress controller with a private IP address

Copy the following YAML manifest into a new file named

`nginx-internal-controller.yaml`

and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`


## Create an NGINX ingress controller with a static IP address

Create an Azure resource group using the

command.`az group create`

`az group create --name $NETWORK_RESOURCE_GROUP --location $LOCATION`

Create a static public IP address using the

command.`az network public ip create`

`az network public-ip create \ --resource-group $NETWORK_RESOURCE_GROUP \ --name $PUBLIC_IP_NAME \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use`Basic`

for the`--sku`

parameter when defining a public IP. Only`Basic`

SKU IPs work with the*Basic*SKU load balancer and only`Standard`

SKU IPs work with the*Standard*SKU load balancers.Ensure the cluster identity used by the AKS cluster has delegated permissions to the public IP's resource group using the

command.`az role assignment create`

`CLIENT_ID=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.principalId -o tsv) RG_SCOPE=$(az group show --name $NETWORK_RESOURCE_GROUP --query id -o tsv) az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Copy the following YAML manifest into a new file named

`nginx-staticip-controller.yaml`

and save the file to your local computer.Note

You can either use

`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML. Adding the`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient Load Balancer creation and is highly recommended to avoid potential throttling.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-static spec: ingressClassName: nginx-static controllerNamePrefix: nginx-static loadBalancerAnnotations: service.beta.kubernetes.io/azure-pip-name: "$PUBLIC_IP_NAME" service.beta.kubernetes.io/azure-load-balancer-resource-group: "$NETWORK_RESOURCE_GROUP"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-staticip-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-static created`


## Verify the ingress controller was created

Verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`

The following example output shows the created resource. It may take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE nginx-public nginx-public nginx True`


### View the conditions of the ingress controller

View the conditions of the ingress controller to troubleshoot any issues using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller --name $INGRESS_CONTROLLER_NAME -o jsonpath='{range .items[*].status.conditions[*]}{.lastTransitionTime}{"\t"}{.status}{"\t"}{.type}{"\t"}{.message}{"\n"}{end}'`

The following example output shows the conditions of a healthy ingress controller:

`2023-11-29T19:59:24Z True IngressClassReady Ingress Class is up-to-date 2023-11-29T19:59:50Z True Available Controller Deployment has minimum availability and IngressClass is up-to-date 2023-11-29T19:59:50Z True ControllerAvailable Controller Deployment is available 2023-11-29T19:59:25Z True Progressing Controller Deployment has successfully progressed`


## Use the ingress controller in an ingress

Copy the following YAML manifest into a new file named

`ingress.yaml`

and save the file to your local computer.Note

Update

`<HostName>`

with your DNS host name. The`<IngressClassName>`

is the one you defined when creating the`NginxIngressController`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: <IngressClassName> rules: - host: <HostName> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml --namespace hello-web-app-routing`

The following example output shows the created resource:

`ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress --namespace hello-web-app-routing`

Your output should resemble the following example output:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Remove ingress controllers

Remove the NGINX ingress controller using the

command.`kubectl delete nginxingresscontroller`

`kubectl delete nginxingresscontroller --name $INGRESS_CONTROLLER_NAME`


## Configuration per ingress resource through annotations

The NGINX ingress controller supports adding [annotations to specific ingress objects](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/) to customize their behavior.

You can [annotate](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) the ingress object by adding the respective annotation in the `metadata.annotations`

field.

Note

Annotation keys and values can only be strings. Other types, such as boolean or numeric values must be quoted. For example: `"true"`

, `"false"`

, `"100"`

.

The following sections provide examples for common configurations. For a full list, see the [NGINX ingress annotations documentation](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).

### Custom max body size

For NGINX, a 413 error is returned to the client when the size in a request exceeds the maximum allowed size of the client request body. To override the default value, use the annotation:

```
nginx.ingress.kubernetes.io/proxy-body-size: 4m
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-body-size: 4m
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Custom connection timeout

You can change the timeout that the NGINX ingress controller waits to close a connection with your workload. All timeout values are unitless and in seconds. To override the default timeout, use the following annotation to set a valid 120-seconds proxy read timeout:

```
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
```


Review [custom timeouts](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-timeouts) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/proxy-read-timeout: "120"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Backend protocol

The NGINX ingress controller uses `HTTP`

to reach the services by default. To configure alternative backend protocols such as `HTTPS`

or `GRPC`

, use one of the following annotations:

```
# HTTPS annotation
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
# GRPC annotation
nginx.ingress.kubernetes.io/backend-protocol: "GRPC"
```


Review [backend protocols](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#backend-protocol) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Cross-Origin Resource Sharing (CORS)

To enable Cross-Origin Resource Sharing (CORS) in an Ingress rule, use the following annotation:

```
nginx.ingress.kubernetes.io/enable-cors: "true"
```


Review [enable CORS](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#enable-cors) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/enable-cors: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### Disable SSL redirect

The controller redirects (308) to HTTPS if TLS is enabled for an ingress by default. To disable this feature for specific ingress resources, use the following annotation:

```
nginx.ingress.kubernetes.io/ssl-redirect: "false"
```


Review [server-side HTTPS enforcement through redirect](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#server-side-https-enforcement-through-redirect) for other configuration options.

Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- backend:
service:
name: aks-helloworld
port:
number: 80
path: /
pathType: Prefix
```


### URL rewriting

In some scenarios, the exposed URL in the backend service differs from the specified path in the ingress rule. Without a rewrite any request returns 404. This configuration is useful with [path-based routing](https://kubernetes.github.io/ingress-nginx/user-guide/ingress-path-matching/) where you can serve two different web applications under the same domain. You can set path expected by the service using the following annotation:

```
nginx.ingress.kubernetes.io/rewrite-target: /$2
```


Here's an example ingress configuration using this annotation:

Note

Update `<HostName>`

with your DNS host name.
The `<IngressClassName>`

is the one you defined when creating the `NginxIngressController`

.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: aks-helloworld
namespace: hello-web-app-routing
annotations:
nginx.ingress.kubernetes.io/rewrite-target: /$2
nginx.ingress.kubernetes.io/use-regex: "true"
spec:
ingressClassName: <IngressClassName>
rules:
- host: <HostName>
http:
paths:
- path: /app-one(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-one
port:
number: 80
- path: /app-two(/|$)(.*)
pathType: Prefix
backend:
service:
name: app-two
port:
number: 80
```


### NGINX health probe path update

The default health probe path for the Azure Load Balancer associated with the NGINX ingress controller must be set to `"/healthz"`

. To ensure correct health checks, verify that the ingress controller service has the following annotation:

```
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


If you're using Helm to manage your NGINX ingress controller, you can define the Azure Load Balancer health-probe annotation in a values file and apply it during an upgrade:

```
controller:
service:
annotations:
service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path: "/healthz"
```


This configuration helps maintain service availability and avoids unexpected traffic disruption during upgrades.

## Next steps

Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration-quickstart -->

# Quickstart: Generate ConfigMap from Azure App Configuration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can externalize the configurations of your Azure Kubernetes Service (AKS) workloads and manage them in [Azure App Configuration](/en-us/azure/azure-app-configuration/overview). The [Azure App Configuration Kubernetes provider](https://mcr.microsoft.com/artifact/mar/azure-app-configuration/kubernetes-provider/about) runs as a container in your cluster. Key benefits include:

**Seamless integration**: Pulls data from Azure App Configuration and Key Vault, making them accessible as ConfigMap and Secret without code changes in your workloads.**Dynamic update**: Built-in caching and refreshing capabilities for dynamic configuration, feature flagging, and automatic secret rotation.

The Azure App Configuration Kubernetes provider is available as an AKS extension. By following this document, you can easily install the extension and connect your AKS cluster with an App Configuration store using the Service Connector in the Azure portal. For information on setting up the provider using Helm, see the [Quickstart for Azure App Configuration Kubernetes provider](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service).

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - A running workload in Azure Kubernetes Service (AKS) cluster. If you don't have one, you can
[create a demo application running in AKS](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#create-an-application-running-in-aks).

## Create a service connection to App Configuration

Create a service connection between your AKS cluster and your App Configuration store using Microsoft Entra Workload Identity.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.Select

**Settings**>**Service Connector**>**Create**.On the

**Basics**tab, configure the following settings:**Kubernetes namespace**: Specify the namespace you'd like to create ConfigMap or Secret to.**Service type**: Select**App Configuration**.**Use App Configuration Extension on Kubernetes**: Check the box to use the[Azure App Configuration AKS extension](azure-app-configuration)for this connection. Azure App Configuration AKS extension will be installed to current cluster if it's not yet.**Connection name**: Enter a connection name or use the default name.**Subscription**: Select the subscription of your App Configuration store.**App Configuration**: Select your App Configuration store. If you don't have one, click**Create new**to set one up.

Select

**Next: Authentication**. On the**Authentication**tab, keep the default selection of**Workload Identity**, select a**User assigned managed identity**you want to use. If you don't have one, click**Create new**to set one up.Select

**Next: Networking**and use the default settings.Select

**Next: Review + create**and wait for the validation to pass.Select

**Create**to create the service connection.

Note

The Service Connector simplifies the installation of the Azure App Configuration AKS extension from the Azure portal. You can also install it without Service Connector using Azure CLI, Bicep, or an ARM template. For more information, see [Install Azure App Configuration AKS extension](azure-app-configuration).

## Generate ConfigMap from App Configuration

Update the service connection to create and deploy an `AzureAppConfigurationProvider`

YAML resource in your AKS cluster. This resource generates a ConfigMap with data from your App Configuration store.

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource and select**Settings**>**Service Connector**.Select the newly created connection, select

**Yaml snippet**in the top menu.On the

**AzureAppConfigurationProvider**tab, configure the following settings:**Using configuration as**: Choose to consume the configuration as a**mounted file**or**environment variables**.**Mounted file**: If selected, specify the**file type**and**file name**.**Selector**: Set the**Key filter**and**Label filter**to load data from your App Configuration store.

A YAML is generated based on your input. Click

**Apply**to add it to your AKS cluster. It will create a ConfigMap in your AKS cluster with data from your App Configuration store.Click

**Next**. On the**Workload**tab, configure the following settings:**File mount path**: Specify the file mount path if the mounted file option was selected.**Kubernetes Workload**: Select the workload where the generated ConfigMap will be injected.- Click
**Apply**to update the workload.


## Next Steps

To learn more about installing and customizing the Azure App Configuration AKS extension, refer to the following documents:

For a complete feature rundown of the Azure App Configuration Kubernetes Provider, see

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator -->

# Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator add-on to efficiently self-host large language models on Kubernetes, reducing costs and resource complexity, enhancing customization, and maintaining full control over your data.

## About KAITO

Self-hosting large language models (LLMs) on Kubernetes is gaining momentum among organizations with inference workloads at scale, such as batch processing, chatbots, agents, and AI-driven applications. These organizations often have access to commercial-grade GPUs and are seeking alternatives to costly per-token API pricing models, which can quickly scale out of control. Many also require the ability to fine-tune or customize their models, a capability typically restricted by closed-source API providers. Additionally, companies handling sensitive or proprietary data - especially in regulated sectors such as finance, healthcare, or defense - prioritize self-hosting to maintain strict control over data and prevent exposure through third-party systems.

To address these needs and more, the [Kubernetes AI Toolchain Operator (KAITO)](https://github.com/kaito-project/kaito), a Cloud Native Computing Foundation (CNCF) Sandbox project, simplifies the process of deploying and managing open-source LLM workloads on Kubernetes. KAITO integrates with vLLM, a high-throughput inference engine designed to serve large language models efficiently. vLLM as an inference engine helps reduce memory and GPU requirements without significantly compromising accuracy.

Built on top of the open-source KAITO project, the AI toolchain operator managed add-on offers a modular, plug-and-play setup that allows teams to quickly deploy models and expose them via production-ready APIs. It includes built-in features like OpenAI-compatible APIs, prompt formatting, and streaming response support. When deployed on an AKS cluster, KAITO ensures data stays within your organization’s controlled environment, providing a secure, compliant alternative to cloud-hosted LLM APIs.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for AKS](concepts-clusters-workloads). - For
and default resource configuration, see the**all hosted model preset images**[KAITO GitHub repository](https://github.com/kaito-project/kaito/tree/main/presets). - The AI toolchain operator add-on currently supports KAITO
**version 0.6.0**, please make a note of this in considering your choice of model from the KAITO model repository.

## Limitations

`AzureLinux`

and`Windows`

OS SKU are not currently supported.- AMD GPU VM sizes are not supported
`instanceType`

in a KAITO workspace. - AI toolchain operator add-on is supported in
**public**Azure regions.

## Prerequisites

If you don't have an Azure subscription, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.If you have multiple Azure subscriptions, make sure you select the correct subscription in which the resources will be created and charged using the

[az account set](/en-us/cli/azure/account#az-account-set)command.Note

Your Azure subscription must have GPU VM quota recommended for your model deployment in the same Azure region as your AKS resources.


Azure CLI version 2.76.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The Kubernetes command-line client, kubectl, installed and configured. For more information, see

[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Export environment variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

`export AZURE_SUBSCRIPTION_ID="mySubscriptionID" export AZURE_RESOURCE_GROUP="myResourceGroup" export AZURE_LOCATION="myLocation" export CLUSTER_NAME="myClusterName"`


## Enable the AI toolchain operator add-on on an AKS cluster

The following sections describe how to create an AKS cluster with the AI toolchain operator add-on enabled and deploy a default hosted AI model.

### Create an AKS cluster with the AI toolchain operator add-on enabled

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create --name $AZURE_RESOURCE_GROUP --location $AZURE_LOCATION`

Create an AKS cluster with the AI toolchain operator add-on enabled using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--enable-ai-toolchain-operator`

and`--enable-oidc-issuer`

flags.`az aks create --location $AZURE_LOCATION \ --resource-group $AZURE_RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-ai-toolchain-operator \ --enable-oidc-issuer \ --generate-ssh-keys`

On an existing AKS cluster, you can enable the AI toolchain operator add-on using the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command.`az aks update --name $CLUSTER_NAME \ --resource-group $AZURE_RESOURCE_GROUP \ --enable-ai-toolchain-operator \ --enable-oidc-issuer`


## Connect to your cluster

Configure

`kubectl`

to connect to your cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $CLUSTER_NAME`

Verify the connection to your cluster using the

`kubectl get`

command.`kubectl get nodes`


## Deploy a default hosted AI model

KAITO offers a range of small to large language models hosted as public container images, which can be deployed in one step using a KAITO workspace. You can browse the preset LLM images available in the [KAITO model registry](https://github.com/kaito-project/kaito/tree/main/presets). In this section, we'll use the high-performant multimodal [Microsoft Phi-4-mini](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037) language model as an example:

Deploy the

[Phi-4-mini instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct)model preset for inference from the KAITO model repository using the`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml`

Track the live resource changes in your workspace using the

`kubectl get`

command.`kubectl get workspace workspace-phi-4-mini -w`

Note

As you track the KAITO workspace deployment, note that machine readiness can take up to 10 minutes, and workspace readiness up to 20 minutes depending on the size of your model.

Check your inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-4-mini -o jsonpath='{.spec.clusterIP}')`

Test the Phi-4-mini instruct inference service with a sample input of your choice using the

[OpenAI chat completions API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions -H "Content-Type: application/json" \ -d '{ "model": "phi-4-mini-instruct", "prompt": "How should I dress for the weather today?", "max_tokens": 10 }'`


## Deploy a custom or domain-specific LLM

Open-source LLMs are often trained in different contexts and domains, and the hosted model presets may not always fit the requirements of your application or data. In this case, KAITO also supports inference deployment of newer or domain-specific language models from [HuggingFace](https://huggingface.co/). Try out a custom model inference deployment with KAITO by following [this article](kaito-custom-inference-model).

## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO workspace using the

`kubectl delete workspace`

command.`kubectl delete workspace workspace-phi-4-mini`

You need to manually delete the GPU node pools provisioned by the KAITO deployment. Use the node label created by

[Phi-4-mini instruct workspace](https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml)to get the node pool name using thecommand. In this example, the node label is "kaito.sh/workspace": "workspace-phi-4-mini".`az aks nodepool list`

`az aks nodepool list --resource-group $AZURE_RESOURCE_GROUP --cluster-name $CLUSTER_NAME`

[Delete the node pool](delete-node-pool)with this name from your AKS cluster and repeat the steps in this section for each KAITO workspace that will be removed.

## Common troubleshooting scenarios

After applying the KAITO model inference workspace, your resource readiness and workspace conditions might not update to `True`

for the following reasons:

- Your Azure subscription doesn't have quota for the minimum GPU instance type specified in your KAITO workspace. You'll need to
[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal)for the GPU VM family in your Azure subscription. - The GPU instance type isn't available in your AKS region. Confirm the
[GPU instance availability in your specific region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?regions=&products=virtual-machines)and switch the Azure region if your GPU VM family isn't available.

## Next steps

Learn more about KAITO model deployment options below:

- Deploy LLMs with your application on AKS using
[KAITO in Visual Studio Code](aks-extension-kaito). [Monitor your KAITO inference workload](ai-toolchain-operator-monitoring).[Fine tune a model](ai-toolchain-operator-fine-tune)with the AI toolchain operator add-on on AKS.- Configure and test
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling). - Integrate an
[MCP server with the AI toolchain operator](ai-toolchain-operator-mcp)add-on on AKS.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-confidential-containers-default-policy -->

# Deploy an AKS cluster with Confidential Containers and an automatically generated policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure CLI to deploy an Azure Kubernetes Service (AKS) cluster and configure Confidential Containers (preview) with an automatically generated security policy. You then deploy an application as a Confidential container. To learn more, read the [overview of AKS Confidential Containers](confidential-containers-overview).

In general, getting started with AKS Confidential Containers involves the following steps.

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML manifest to mark the pod as using confidential containers
- Add a security policy to your pod YAML manifest
- Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

The Azure CLI version 2.44.1 or later. Run

`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`aks-preview`

Azure CLI extension version 0.5.169 or later.The

`confcom`

Confidential Container Azure CLI extension 0.3.3 or later.`confcom`

is required to generate a[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy).Register the

`Preview`

feature in your Azure subscription.AKS supports Confidential Containers (preview) on version 1.25.0 and higher.

A workload identity and a federated identity credential. The workload identity credential enables Kubernetes applications access to Azure resources securely with a Microsoft Entra ID based on annotated service accounts. If you aren't familiar with Microsoft Entra Workload ID, see the

[Microsoft Entra Workload ID overview](/en-us/azure/active-directory/workload-identities/workload-identities-overview)and review how[Workload Identity works with AKS](workload-identity-overview).The identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.Confidential containers on AKS provide a sidecar open source container for attestation and secure key release. The sidecar integrates with a Key Management Service (KMS), like Azure Key Vault, for releasing a key to the container group after validation is completed. Deploying an

[Azure Key Vault Managed HSM](/en-us/azure/key-vault/managed-hsm/overview)(Hardware Security Module) is optional but recommended to support container-level integrity and attestation. See[Provision and activate a Managed HSM](/en-us/azure/key-vault/managed-hsm/quick-create-cli)to deploy Managed HSM.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension:

```
az extension update --name aks-preview
```


### Install the confcom Azure CLI extension

To install the confcom extension, run the following command:

```
az extension add --name confcom
```


Run the following command to update to the latest version of the extension:

```
az extension update --name confcom
```


### Register the KataCcIsolationPreview feature flag

Register the `KataCcIsolationPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace "Microsoft.ContainerService"
```


## Deploy a new cluster

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.**--enable-workload-identity**: Enables creating a Microsoft Entra Workload ID enabling pods to use a Kubernetes identity.**--enable-oidc-issuer**: Enables OpenID Connect (OIDC) Issuer. It allows a Microsoft Entra ID or other cloud provider identity and access management platform the ability to discover the API server's public signing keys.**--workload-runtime**: Specify*KataCcIsolation*to enable the Confidential Containers feature on the node pool.

`az aks create --resource-group myResourceGroup --name myAKSCluster --kubernetes-version <1.25.0 and above> --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation --node-count 1 --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Follow the steps to
[register the KataCcIsolationPreview](#register-the-kataccisolationpreview-feature-flag)feature flag. - Verify the cluster is running Kubernetes version 1.25.0 and higher.
[Enable workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)on the cluster if it isn't already.

Use the following command to enable Confidential Containers (preview) by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataCcIsolation*to enable the feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter(s).**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs nested virtualization works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.

The following example adds a user node pool to

*myAKSCluster*with two nodes in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --resource-group myResourceGroup --name nodepool2 –-cluster-name myAKSCluster --node-count 2 --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable Confidential Containers (preview) on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Configure container

Before you configure access to the Azure Key Vault and secret, and deploy an application as a Confidential container, you need to complete the configuration of the workload identity.

To configure the workload identity, perform the following steps described in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article:

- Retrieve the OIDC Issuer URL
- Create a managed identity
- Create Kubernetes service account
- Establish federated identity credential

Important

You need to set the *environment variables* from the section **Export environmental variables** in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article to continue completing this tutorial. Remember to set the variable `SERVICE_ACCOUNT_NAMESPACE`

to `kafka`

, and execute the command `kubectl create namespace kafka`

before configuring workload identity.

## Deploy a trusted application with kata-cc and attestation container

The following steps configure end-to-end encryption for Kafka messages using encryption keys managed by [Azure Managed Hardware Security Modules](/en-us/azure/key-vault/managed-hsm/overview) (mHSM). The key is only released when the Kafka consumer runs within a Confidential Container with an Azure attestation secret provisioning container injected in to the pod.

This configuration is based on the following four components:

- Kafka Cluster: A simple Kafka cluster deployed in the Kafka namespace on the cluster.
- Kafka Producer: A Kafka producer running as a vanilla Kubernetes pod that sends encrypted user-configured messages using a public key to a Kafka topic.
- Kafka Consumer: A Kafka consumer pod running with the kata-cc runtime, equipped with a secure key release container to retrieve the private key for decrypting Kafka messages and render the messages to web UI.

For this preview release, we recommend for test and evaluation purposes to either create or use an existing Azure Key Vault Premium tier resource to support storing keys in a hardware security module (HSM). We don't recommend using your production key vault. If you don't have an Azure Key Vault, see [Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).

Grant the managed identity you created earlier, and your account, access to the key vault.

[Assign](/en-us/azure/key-vault/general/rbac-guide#assign-role)both identities the**Key Vault Crypto Officer**and**Key Vault Crypto User**Azure RBAC roles.Note

The managed identity is the value you assign to the

`USER_ASSIGNED_IDENTITY_NAME`

variable.To add role assignments, you must have

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as[Key Vault Data Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#key-vault-data-access-administrator),[User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), or[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).You must use the Key Vault Premium SKU to support HSM-protected keys.


Run the following command to set the scope:

`AKV_SCOPE=$(az keyvault show --name <AZURE_AKV_RESOURCE_NAME> --query id --output tsv)`

Run the following command to assign the

**Key Vault Crypto Officer**role.`az role assignment create --role "Key Vault Crypto Officer" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Run the following command to assign the

**Key Vault Crypto User**role.`az role assignment create --role "Key Vault Crypto User" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Install the Kafka cluster in the kafka namespace by running the following command:

`kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka`

Run the following command to apply the

`kafka`

cluster CR file.`kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka`

Prepare the RSA Encryption/Decryption key using the

[bash script](https://github.com/microsoft/confidential-container-demos/raw/main/kafka/setup-key.sh)for the workload from GitHub. Save the file as`setup-key.sh`

.Set the

`MAA_ENDPOINT`

environment variable with the FQDN of Attest URI by running the following command.`export MAA_ENDPOINT="$(az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-)"`

Check if the FQDN of Attest URI is in correct format (the MAA_ENDPOINT should not include the prefix "https://"):

`echo $MAA_ENDPOINT`

Note

To set up Microsoft Azure Attestation, see

[Quickstart: Set up Azure Attestation with Azure CLI](/en-us/azure/attestation/quickstart-azure-cli).Copy the following YAML manifest and save it as

`consumer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-golang-consumer namespace: kafka labels: azure.workload.identity/use: "true" app.kubernetes.io/name: kafka-golang-consumer spec: serviceAccountName: workload-identity-sa runtimeClassName: kata-cc-isolation containers: - image: "mcr.microsoft.com/aci/skr:2.7" imagePullPolicy: Always name: skr env: - name: SkrSideCarArgs value: ewogICAgImNlcnRjYWNoZSI6IHsKCQkiZW5kcG9pbnRfdHlwZSI6ICJMb2NhbFRISU0iLAoJCSJlbmRwb2ludCI6ICIxNjkuMjU0LjE2OS4yNTQvbWV0YWRhdGEvVEhJTS9hbWQvY2VydGlmaWNhdGlvbiIKCX0gIAp9 command: - /bin/skr volumeMounts: - mountPath: /opt/confidential-containers/share/kata-containers/reference-info-base64 name: endor-loc - image: "mcr.microsoft.com/acc/samples/kafka/consumer:1.0" imagePullPolicy: Always name: kafka-golang-consumer env: - name: SkrClientKID value: kafka-encryption-demo - name: SkrClientMAAEndpoint value: sharedeus2.eus2.test.attest.azure.net - name: SkrClientAKVEndpoint value: "myKeyVault.vault.azure.net" - name: TOPIC value: kafka-demo-topic command: - /consume ports: - containerPort: 3333 name: kafka-consumer resources: limits: memory: 1Gi cpu: 200m volumes: - name: endor-loc hostPath: path: /opt/confidential-containers/share/kata-containers/reference-info-base64 --- apiVersion: v1 kind: Service metadata: name: consumer namespace: kafka spec: type: LoadBalancer selector: app.kubernetes.io/name: kafka-golang-consumer ports: - protocol: TCP port: 80 targetPort: kafka-consumer`

Note

Update the value for the pod environment variable

`SkrClientAKVEndpoint`

to match the URL of your Azure Key Vault, excluding the protocol value`https://`

. The current value placeholder value is`myKeyVault.vault.azure.net`

. Update the value for the pod environment variable`SkrClientMAAEndpoint`

with the value of`MAA_ENDPOINT`

. You can find the value of`MAA_ENDPOINT`

by running the command`echo $MAA_ENDPOINT`

or the command`az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-`

.Generate the security policy for the Kafka consumer YAML manifest and obtain the hash of the security policy stored in the

`WORKLOAD_MEASUREMENT`

variable by running the following command:`export WORKLOAD_MEASUREMENT=$(az confcom katapolicygen -y consumer.yaml --print-policy | base64 -d | sha256sum | cut -d' ' -f1)`

To generate an RSA asymmetric key pair (public and private keys), run the

`setup-key.sh`

script using the following command. The`<Azure Key Vault URL>`

value should be`<your-unique-keyvault-name>.vault.azure.net`

`export MANAGED_IDENTITY=${USER_ASSIGNED_CLIENT_ID} bash setup-key.sh "kafka-encryption-demo" <Azure Key Vault URL>`

Note

The envionment variable

`MANAGED_IDENTITY`

is required by the bash script`setup-key.sh`

.The public key will be saved as

`kafka-encryption-demo-pub.pem`

after executing the bash script.

Important

If you receive the error

`ForbiddenByRbac`

,you might need to wait up to 24 hours as the backend services for managed identities maintain a cache per resource URI for up to 24 hours. See also:[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#symptom---role-assignment-changes-are-not-being-detected).To verify the keys have been successfully uploaded to the key vault, run the following commands:

`az account set --subscription <Subscription ID> az keyvault key list --vault-name <KeyVault Name> -o table`

Copy the following YAML manifest and save it as

`producer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-producer namespace: kafka spec: containers: - image: "mcr.microsoft.com/acc/samples/kafka/producer:1.0" name: kafka-producer command: - /produce env: - name: TOPIC value: kafka-demo-topic - name: MSG value: "Azure Confidential Computing" - name: PUBKEY value: |- -----BEGIN PUBLIC KEY----- MIIBojAN***AE= -----END PUBLIC KEY----- resources: limits: memory: 1Gi cpu: 200m`

Note

Update the value which begin with

`-----BEGIN PUBLIC KEY-----`

and ends with`-----END PUBLIC KEY-----`

strings with the content from`kafka-encryption-demo-pub.pem`

which was created in the previous step.Deploy the

`consumer`

and`producer`

YAML manifests using the files you saved earlier.`kubectl apply -f consumer.yaml`

`kubectl apply -f producer.yaml`

Get the IP address of the web service using the following command:

`kubectl get svc consumer -n kafka`

Copy and paste the external IP address of the consumer service into your browser and observe the decrypted message.

The following example resembles the output of the command:

`Welcome to Confidential Containers on AKS! Encrypted Kafka Message: Msg 1: Azure Confidential Computing`

You should also attempt to run the consumer as a regular Kubernetes pod by removing the

`skr container`

and`kata-cc runtime class`

spec. Since you aren't running the consumer with kata-cc runtime class, you no longer need the policy.Remove the entire policy and observe the messages again in the browser after redeploying the workload. Messages appear as base64-encoded ciphertext because the private encryption key can't be retrieved. The key can't be retrieved because the consumer is no longer running in a confidential environment, and the

`skr container`

is missing, preventing decryption of messages.

## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you enabled Confidential Containers (preview) on an existing cluster, you can remove the pod(s) using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete pod pod-name
```


## Next steps

- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

# Set up Layer 7(L7) policies with Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to set up L7 policies with Advanced Container Networking Services in AKS clusters. Continue only after you have reviewed the limitations and considerations listed on the [Layer 7 Policy Overview](container-network-security-l7-policy-concepts) page.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.79.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Install the `aks-preview`

Azure CLI extension

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


### Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the `AdvancedNetworkingL7PolicyPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--acns-advanced-networkpolicies L7
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-advanced-networkpolicies L7
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Set up http-server application on your AKS cluster

Apply the below YAML to your AKS cluster to set up the `http-server`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-server
labels:
app: http-server
spec:
replicas: 1
selector:
matchLabels:
app: http-server
template:
metadata:
labels:
app: http-server
spec:
containers:
- name: http-server
image: nginx:latest
ports:
- containerPort: 8080
volumeMounts:
- name: config-volume
mountPath: /etc/nginx/conf.d
volumes:
- name: config-volume
configMap:
name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
name: http-server
spec:
selector:
app: http-server
ports:
- protocol: TCP
port: 80
targetPort: 8080
---
apiVersion: v1
kind: ConfigMap
metadata:
name: nginx-config
data:
default.conf: |
server {
listen 8080;
location / {
return 200 "Hello from the server root!\n";
}
location /products {
return 200 "Listing products...\n";
}
}
```


## Set up http-client application on your AKS Cluster

Apply the below YAML to your AKS cluster to set up the `http-client`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-client
labels:
app: http-client
spec:
replicas: 1
selector:
matchLabels:
app: http-client
template:
metadata:
labels:
app: http-client
spec:
containers:
- name: http-client
image: curlimages/curl:latest
command: ["sleep", "infinity"]
```


## Test connectivity with a policy

Next, apply the following Layer 7 policy to allow only `GET`

requests from the `http-client`

application to the `/products`

endpoint on the `http-server`

:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: allow-get-products
spec:
description: "Allow only GET requests to /products from http-client to http-server"
endpointSelector:
matchLabels:
app: http-server
ingress:
- fromEndpoints:
- matchLabels:
app: http-client
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/products"
```


### Verify policy

To verify the policy's enforcement, execute these commands from the `http-client`

pod:

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v http://http-server:80/products
```


You should expect an output like `Listing products...`

when you run the above command

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v -XPOST http://http-server:80/products -d "test=data"
```


You should expect an output like `Access Denied`

when you run the above command

### Observing L7 metrics

If you have Advanced Container Network Service's container network observability enabled, you can visualize the traffic on Grafana.

To simplify the analysis of these L7 metrics, we provide preconfigured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

You should see metrics similar to the following:

## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to enable and apply L7 Policies with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/confidential-containers-overview -->

# Confidential Containers (preview) with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Confidential Containers preview is set to sunset in **March 2026**. After this date, customers with existing Confidential Container node pools should expect to see reduced functionality, and you won't be able to spin up any new nodes with the `KataCcIsolation`

runtime. Customers currently using Confidential Container node pools can continue using them as normal. If you want to move off Confidential Containers, consider the following alternatives:

[Confidential VMs on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks): Offers a similar hardware-based TEE that leverages AMD SEV-SNP security features, without the addition of per-VM isolation for workloads seen in Confidential Containers.[Application enclave support](/en-us/azure/confidential-computing/confidential-nodes-aks-overview): Provides users with Intel SGX confidential computing VM nodes that support hardware-based, process-level container isolation through the Intel SGX trusted execution environment.[Confidential Containers on Azure Container Instances](/en-us/azure/confidential-computing/confidential-containers): Allows for lift-and-shift deployments on containers backed by AMD SEV-SNP. Functionality includes performing full guest attestation, access to toolings to generate policies, and utilizing sidecar containers for secure key releases. ACI nodes can be run on AKS via[virtual nodes](/en-us/azure/container-instances/container-instances-virtual-nodes).[Azure RedHat OpenShift Confidential Containers](/en-us/azure/openshift/confidential-containers-overview): Offers a similar AMD SEV-SNP backed TEE and utilizes the Kata runtime for per-container level isolation.[Open source Confidential Containers](https://github.com/confidential-containers): Gives a similar AMD SEV-SNP backed TEE that comes with per-container isolation through Kata.

If you have additional questions, please create a [support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) or post an issue in [AKS issues](https://github.com/Azure/AKS/issues).

Confidential Containers provide a set of features and capabilities to further secure your standard container workloads to achieve higher data security, data privacy and runtime code integrity goals. Azure Kubernetes Service (AKS) includes Confidential Containers (preview) on AKS.

Confidential Containers builds on Kata Confidential Containers and hardware-based encryption to encrypt container memory. It establishes a new level of data confidentiality by preventing data in memory during computation from being in clear text, readable format. Trust is earned in the container through hardware attestation, allowing access to the encrypted data by trusted entities.

Together with [Pod Sandboxing](use-pod-sandboxing), you can run sensitive workloads isolated in Azure to protect your data and workloads. What makes a container confidential:

- Transparency: The confidential container environment where your sensitive application is shared, you can see and verify if it's safe. All components of the Trusted Computing Base (TCB) are to be open sourced.
- Auditability: You have the ability to verify and see what version of the CoCo environment package including Linux Guest OS and all the components are current. Microsoft signs to the guest OS and container runtime environment for verifications through attestation. It also releases a secure hash algorithm (SHA) of guest OS builds to build a string audibility and control story.
- Full attestation: Anything that is part of the TEE shall be fully measured by the CPU with ability to verify remotely. The hardware report from AMD SEV-SNP processor shall reflect container layers and container runtime configuration hash through the attestation claims. Application can fetch the hardware report locally including the report that reflects Guest OS image and container runtime.
- Code integrity: Runtime enforcement is always available through customer defined policies for containers and container configuration, such as immutable policies and container signing.
- Isolation from operator: Security designs that assume least privilege and highest isolation shielding from all untrusted parties including customer/tenant admins. It includes hardening existing Kubernetes control plane access (kubelet) to confidential pods.

With other security measures or data protection controls, as part of your overall architecture, these capabilities help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand the Confidential Containers feature, and how to implement and configure the following:

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML to mark the pod as being run as a confidential container
- Add a
[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to your pod YAML - Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Supported scenarios

Confidential Containers (preview) are appropriate for deployment scenarios that involve sensitive data. For example, personally identifiable information (PII) or any data with strong security needed for regulatory compliance. Some common scenarios with containers are:

- Run big data analytics using Apache Spark for fraud pattern recognition in the financial sector.
- Running self-hosted GitHub runners to securely sign code as part of Continuous Integration and Continuous Deployment (CI/CD) DevOps practices.
- Machine Learning inferencing and training of ML models using an encrypted data set from a trusted source. It only decrypts inside a confidential container environment to preserve privacy.
- Building big data clean rooms for ID matching as part of multi-party computation in industries like retail with digital advertising.
- Building confidential computing Zero Trust landing zones to meet privacy regulations for application migrations to cloud.

## Considerations

The following are considerations with this preview of Confidential Containers:

- An increase in pod startup time compared to runc pods and kernel-isolated pods.
- Version 1 container images aren't supported.
- Ephemeral containers and other troubleshooting methods like
`exec`

into a container, log outputs from containers, and`stdio`

require a policy modification and redeployment to enable ExecProcessRequest, ReadStreamRequest, WriteStreamRequest, and CloseStdinRequest. - Due to container image layer measurements being encoded in the security policy, we don't recommend using the
`latest`

tag when specifying containers. - Services, Load Balancers, and EndpointSlices only support the TCP protocol.
- The policy generator only supports pods that use IPv4 addresses.
- Pod environment variables based on ConfigMaps and Secrets can't be changed after the pod is deployed.
- Pod termination logs aren't supported. While pods write termination logs to
`/dev/termination-log`

or to a custom location if specified in the pod manifest, the host/kubelet can't read those logs. Changes from the pod to that file aren't reflected on the host. - Confidential Containers currently only supports Azure Linux.

## Resource allocation overview

It's important you understand the memory and processor resource allocation behavior in this release.

- CPU: The shim assigns one vCPU to the base OS inside the pod. If no resource
`limits`

are specified, the workloads don't have separate CPU shares assigned, the vCPU is then shared with that workload. If CPU limits are specified, CPU shares are explicitly allocated for workloads. - Memory: The Kata-CC handler uses 2 GB memory for the UVM OS and X MB additional memory where X is the resource
`limits`

if specified in the YAML manifest (resulting in a 2-GB VM when no limit is given, without implicit memory for containers). The[Kata](https://katacontainers.io/docs/)handler uses 256 MB base memory for the UVM OS and X MB additional memory when resource`limits`

are specified in the YAML manifest. If limits are unspecified, an implicit limit of 1,792 MB is added resulting in a 2 GB VM and 1,792 MB implicit memory for containers.

In this release, specifying resource requests in the pod manifests isn't supported. containerd doesn't pass the requests to the Kata Shim, and as a result, reserving resources based on the pod manifest resource requests is not implemented. Use resource `limits`

instead of resource `requests`

to allocate memory or CPU resources for workloads or containers.

With the local container filesystem backed by VM memory, writing to the container filesystem (including logging) can fill up the available memory provided to the pod. This condition can result in potential pod crashes.

## Next steps

- See the overview of
[Confidential Containers security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to learn about how workloads and their data in a pod is protected. [Deploy Confidential Containers on AKS](deploy-confidential-containers-default-policy)with an automatically generated security policy.- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:
