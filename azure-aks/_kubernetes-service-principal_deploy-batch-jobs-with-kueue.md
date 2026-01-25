---
merged_at: 2026-01-25T12:25:33.958941
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kubernetes-service-principal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-service-principal -->

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


---

<!-- DOCUMENTO FUSIONADO: deploy-batch-jobs-with-kueue.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-batch-jobs-with-kueue -->

# Schedule and deploy batch jobs with Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to schedule and deploy sample batch jobs on Azure Kubernetes Service (AKS) using Kueue. Also, this guide covers installing Kueue, configuring ResourceFlavors and ClusterQueues for fine-grained resource management, and submitting jobs via LocalQueues. You also learn how to use Kueue to queue up a sample batch job and track the results across Pending, Running, and Finished states.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

To learn more about Kueue and common uses cases for batch workload administrators and users, see [Kueue overview on AKS](kueue-overview).

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.[The latest version of Kueue installed in a dedicated namespace on your cluster](kueue-overview#prerequisites).

## Define a ResourceFlavor object

In Kueue, a ResourceFlavors enables fine-grained resource management by associating workloads with specific nodes, taints, tolerations, or availability zones. For nodes, `ResourceFlavors`

can define the characteristics like pricing, availability, brands, models, and architecture (that is, x86 versus ARM CPUs). A `ClusterQueue`

uses these flavors to manage quotas and admission policies for workloads.

This configuration defines a `ResourceFlavor`

without any labels or taints, known as an empty `ResourceFlavor`

. This configuration is perfect when quotas for different flavors don't need to be managed.

Create and save a

`ResourceFlavor`

in a file named`resourceflavor-sample.yaml`

with the following manifest:`cat << EOF > resourceflavor-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ResourceFlavor metadata: name: on-demand EOF`

apply

`kubectl apply -f resourceflavor-sample.yaml`

verify

`kubectl get resourceflavors`

Example output

`NAME AGE on-demand 5m32s`


## Create a ClusterQueue

A ClusterQueue is a cluster-scoped resource that governs a pool of resources, defining usage limits and Fair Sharing rules. Where applicable, Fair Sharing rules allow another ClusterQueue in the **same** cohort to unused quota for pending jobs. Each ClusterQueue specifies which flavors it supports and how much quota is available for each.

This sample `ClusterQueue`

defines:

: Indicates that`namespaceSelector: {}`

`sample-jobs`

accepts workloads from any namespace that references this`ClusterQueue`

via a`LocalQueue`

(you can restrict usage (for example, to only team A's namespace) with a label selector).: Defines the standard CPU and memory resource types managed by this`coveredResources: ["cpu", "memory"]`

in`resourceGroups`

`ClusterQueue`

.: Only workloads scheduled on`flavor`

of`on-demand`

nodes with`4`

CPUs,`8Gi`

memory`on-demand`

nodes consume this quota. If the cluster uses up this quota, it doesn't admit any other workloads using this flavor (unless you allow borrowing from the`cohort`

).

Create and save a Kueue

`ClusterQueue`

in a file named`clusterqueue-sample.yaml`

with the following manifest:`cat <<EOF > clusterqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ClusterQueue metadata: name: sample-jobs spec: cohort: general namespaceSelector: {} # Accept workloads from any namespace resourceGroups: - coveredResources: ["cpu", "memory"] flavors: - name: on-demand resources: - name: "cpu" nominalQuota: 4 - name: "memory" nominalQuota: 8Gi EOF`

Apply the

`ClusterQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f clusterqueue-sample.yaml`

Verify the ClusterQueue` manifest was applied

`kubectl get clusterqueues`

Example output

`NAME COHORT PENDING WORKLOADS sample-jobs general 0`


Note

The `ClusterQueue`

isn't ready for use until a `ResourceFlavor`

object is configured. If you create a `ClusterQueue`

without any existing `ResourceFlavor`

, workloads referencing it are marked as `Inadmissible`

.

## Create a LocalQueue

A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs. A `LocalQueue`

is assigned to one `ClusterQueue`

from which resources are allocated to run its workloads.

This sample `LocalQueue`

configures the following settings:

- Enables users in the
`batch-jobs`

namespace to submit batch workloads to Kueue. - Route the batch workloads to the
`sample-jobs`

`ClusterQueue`

, which manages the actual compute resource quotas and scheduling policies.

Create a namespace named

*batch-jobs*using the`kubectl create`

command.`kubectl create ns batch-jobs`

Create and save a

`LocalQueue`

in a file named`localqueue-sample.yaml`

with the following YAML manifest:`cat <<EOF > localqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: LocalQueue metadata: name: sample-queue namespace: batch-jobs spec: clusterQueue: sample-jobs EOF`

Apply the

`LocalQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f localqueue-sample.yaml`

Verify the

`LocalQueue`

manifest was applied`kubectl get localqueues --all-namespaces`

Exampmle output

`NAMESPACE NAME CLUSTERQUEUE PENDING WORKLOADS ADMITTED WORKLOADS batch-jobs sample-queue sample-jobs 0 0`


## Create 2 batch jobs

This configuration defines two Kubernetes batch jobs submitted to the batch-jobs namespace and assigned to the sample-queue managed by Kueue. Both jobs are single-instance (parallelism: 1, completions: 1) and are configured with `Never`

restart policy. The fields `parallelism`

and `completions`

control how many pods are run and how the job is considered complete. So `parallelism`

and `completions`

of 1 means that one pod can run at once, and the job is marked as complete once one pod finishes successfully, per batch job.

- Job test-batch-1: Requests one CPU and 500Mi memory
- Job test-batch-2: Requests two CPUs and 1Gi memory

Create two sample batch jobs to deploy in the

*batch-jobs*namespace using the following YAML manifest named`batch-workloads.yaml`

:`cat <<EOF > batch-workloads.yaml apiVersion: batch/v1 kind: Job metadata: name: test-batch-1 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Running test-batch-1; sleep 60"] resources: requests: cpu: "1" memory: "500Mi" limits: cpu: "1" memory: "500Mi" restartPolicy: Never --- apiVersion: batch/v1 kind: Job metadata: name: test-batch-2 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Waiting in queue for CPUs...; sleep 30"] resources: requests: cpu: "2" memory: "1Gi" limits: cpu: "2" memory: "1Gi" restartPolicy: Never EOF`

Apply the manifest for the batch jobs using the

`kubectl apply`

command.`kubectl apply -f batch-workloads.yaml`


## Verify Batch Jobs are Submitted to `LocalQueue`


View the status of the batched workloads using the

`kubectl get`

command.`kubectl get workloads --namespace batch-jobs`

Example output

`NAME ADMITTED AGE test-batch-1 True 10s test-batch-2 False 5s`

Run the following command for

`test-batch-2`

while it is in a`Pending`

state`kubectl get workloads test-batch-2 -o yaml`

Expected output

`... ... Status: Conditions: Type: Admitted Status: False Reason: QuotaUnavailable Message: Insufficient quota in ClusterQueue sample-jobs (flavor on-demand): requested 2 CPUs, available 1 ... ...`

After

`test-batch-1`

completes,`test-batch-2`

will be admitted and run.Now, the output should look like the following example output:

`Status: Conditions: Type: Admitted Status: True Last Transition Time: 1234-56-78T00:00:00Z Admission: ClusterQueue: sample-jobs PodSetAssignments: Name: main Flavors: cpu: on-demand memory: on-demand ResourceUsage: cpu: 2 memory: 1Gi`

View the final status of the

`batch-jobs`

namespace using the`kubectl get`

command.`kubectl get job,deploy,rs,pod,workload --namespace batch-jobs`

Example output

`NAME STATUS COMPLETIONS DURATION AGE job.batch/test-batch-1 Complete 1/1 97s 3m15s job.batch/test-batch-2 Complete 1/1 35s 3m15s NAME READY STATUS RESTARTS AGE pod/test-batch-1-hb8zl 0/1 Completed 0 3m15s pod/test-batch-2-dx9hk 0/1 Completed 0 3m15s NAME QUEUE RESERVED IN ADMITTED FINISHED AGE workload.kueue.x-k8s.io/job-test-batch-1-6fb85 sample-queue sample-jobs True True 3m15s workload.kueue.x-k8s.io/job-test-batch-2-84f49 sample-queue sample-jobs True True 3m15s`


## FAQ

### Question 1: How can I confirm that the Kueue controller is available and running as expected?

Confirm the Kueue controller manager pod is running using the

`kubectl get`

command.`kubectl get pods --namespace kueue-system`

The Kueue controller manager pod should be in a

`Running`

state with`1/1`

containers ready, as shown in the following example output:`NAME READY STATUS RESTARTS AGE kueue-controller-manager-xxxxxxx 1/1 Running 0 2m`

If the

`Status`

shows`CrashLoopBackOff`

or`Pending`

, check the deployment logs using the`kubectl logs`

command.`kubectl logs --namespace kueue-system deployment/kueue-controller-manager`


### Question 2: One or more of the Kueue custom resources (CRDs) are missing when I install via Helm. How can I ensure all of the CRDs are installed?

After installing Kueue with the

[Kueue overview on AKS](kueue-overview)guidance, confirm that all of the CRDs are installed using the`kubectl get`

command.`kubectl get crds | grep kueue`

These CRDs should be listed, as shown in the following example output:

`admissionchecks.kueue.x-k8s.io clusterqueues.kueue.x-k8s.io cohorts.kueue.x-k8s.io localqueues.kueue.x-k8s.io multikueueclusters.kueue.x-k8s.io multikueueconfigs.kueue.x-k8s.io provisioningrequestconfigs.kueue.x-k8s.io resourceflavors.kueue.x-k8s.io topologies.kueue.x-k8s.io workloadpriorityclasses.kueue.x-k8s.io workloads.kueue.x-k8s.io`

If one or more of the CRDs are missing, you might see errors in controller logs, failed job queuing,

`CrashLoopBackOff`

for the controller, or inability to admit or schedule workloads. In this case, you can manually reinstall the Kueue CRDs using the`kubectl apply`

command.`kubectl apply -f https://github.com/kubernetes-sigs/kueue/releases/latest/download/kueue-crds.yaml`

Note

Note that if you manually install the CRDs, you need to manually delete them once you're finished using the

`kubectl delete`

command.

### Question 3: What's the difference between a LocalQueue and a ClusterQueue

A ClusterQueue is a cluster-scoped resource that defines and governs a pool of compute resources like CPU, memory, pods, and accelerators across the entire Kubernetes cluster. A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs within the defined Kubernetes cluster. This separation allows for fine-grained control over resource allocation and multi-tenant scheduling without exposing cluster-wide quotas directly to users.

How they work together:

- A user submits a job to a LocalQueue in their namespace.
- Kueue routes the job to the referenced ClusterQueue.
- The ClusterQueue checks resource availability and quota limits.
- If admitted, the job is unsuspended and scheduled.

## Next steps

In this article, you:

- Installed Kueue on your Azure Kubernetes Service (AKS) cluster using Helm and verified CRDs, controller health, and namespace setup.
- Configured
`ClusterQueue`

and`LocalQueue`

for general-purpose workloads with resource quotas and flavors (such as on-demand). - Submitted two batch jobs to demonstrate queuing: one admitted immediately, the second held due to quota limits, then admitted when resources became available.
- Monitored workload status and controller logs to confirm scheduling behavior and queuing logic.

To learn more about Kueue, visit the following resources:

[Multi-cluster scheduling and resource placement with Kueue and KubeFleet on AKS](https://blog.aks.azure.com/2025/04/02/Scaling-Kubernetes-for-AI-and-Data-intensive-Workloads).[Kueue developer tools](https://kueue.sigs.k8s.io/docs/tasks/dev/)official documentation.
