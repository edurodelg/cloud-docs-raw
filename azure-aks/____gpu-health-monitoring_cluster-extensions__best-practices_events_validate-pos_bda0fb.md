---
merged_at: 2026-01-26T23:04:05.994046
merged_files: 2
---


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
