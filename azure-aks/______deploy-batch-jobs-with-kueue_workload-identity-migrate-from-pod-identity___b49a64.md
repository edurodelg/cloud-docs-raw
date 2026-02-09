---
merged_at: 2026-02-09T09:22:46.218998
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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-batch-jobs-with-kueue -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-migrate-from-pod-identity -->

# Migrate Azure Kubernetes Service (AKS) pods from pod-managed identity to Microsoft Entra Workload ID

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrate AKS pods from pod-managed identities to [Microsoft Entra Workload ID](workload-identity-overview) (workload identity) using one of three approaches based on your current [Azure Identity SDK](/en-us/entra/identity-platform/reference-v2-libraries) version: latest SDK parallel deployment, migration sidecar proxy (Linux only), or SDK rewrite.

## Prerequisites

- Azure CLI version 2.47.0 or later. Run the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Set environment variables

The following table lists the environment variables used in the commands throughout this article. Make sure to replace the placeholder values with your own values.

| Environment variable | Description | Example value |
|---|---|---|
`SUBSCRIPTION_ID` |
The ID of the Azure subscription where the AKS cluster and managed identity are created. | `00000000-0000-0000-0000-000000000000` |
`RESOURCE_GROUP` |
The name of the resource group where the AKS cluster and managed identity are created. | `myResourceGroup` |
`LOCATION` |
The Azure region where the AKS cluster and managed identity are created. | `eastus` |
`CLUSTER_NAME` |
The name of the AKS cluster. | `myAKSCluster` |
`MANAGED_IDENTITY_NAME` |
The name of the user-assigned managed identity. | `myManagedIdentity` |
`SERVICE_ACCOUNT_NAME` |
The name of the Kubernetes service account to create or associate with the managed identity. | `workload-identity-sa` |
`SERVICE_ACCOUNT_NAMESPACE` |
The namespace of the Kubernetes service account. | `default` |
`FEDERATED_IDENTITY_NAME` |
The name of the federated identity credential to create. | `myFederatedIdentity` |

## Choose a migration path

Select the appropriate migration approach based on your current Azure Identity SDK version:

**Latest Azure Identity SDK**: If your application already uses the latest version of Azure Identity SDK, you can migrate by deploying Microsoft Entra Workload ID in parallel with existing pod-managed identity.**Older SDK with migration sidecar**- If your application uses an older SDK version and runs on Linux containers, you can use a temporary migration sidecar to proxy Instance Metadata Service (IMDS) transactions while planning your SDK upgrade.**Older SDK rewrite approach**: If your application uses an older SDK version, you can update your application code to use the latest Azure Identity SDK, then migrate to workload identity.

## Prepare for migration

For all migration paths, you need to have the federated trust set up before you update your application to use Microsoft Entra Workload ID. The following are the minimum steps required:

[Create a managed identity](#create-a-managed-identity)credential.- Associate the user-assigned managed identity with the Kubernetes service account already used for the pod-managed identity or
[create a new Kubernetes service account](#create-kubernetes-service-account)and then associate it with the managed identity. [Establish a federated trust relationship](#establish-federated-identity-credential-trust)between the managed identity and Microsoft Entra ID using the[OpenID Connect (OIDC)](/en-us/azure/active-directory/develop/v2-protocols-oidc)issuer URL and the service account.

## Migrate from latest version of Azure Identity SDK

**This migration path applies when** your application already uses the latest version of the Azure Identity SDK and you want to migrate with minimal code changes.

**Migration approach**: Deploy Microsoft Entra Workload ID in parallel with pod-managed identity, verify functionality, then remove pod-managed identity.

**Steps**:

- Deploy Microsoft Entra Workload ID in parallel with existing pod-managed identity.
- Restart your application deployment to begin using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify the application can authenticate successfully using workload identity.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations from your application.- Remove the pod-managed identity add-on from your cluster.

## Use a migration sidecar (Linux containers only)

**This migration path applies when** your application uses an older version of the Azure Identity SDK, runs on Linux containers, and you need a temporary solution while planning SDK updates.

**Migration approach**: Deploy a migration sidecar that proxies IMDS transactions to OIDC, allowing your existing application code to work without immediate changes.

**Important limitations**:

**Linux containers only**. Windows containers aren't supported.**Temporary solution**that's not intended for long-term production use.**Planning required**to schedule SDK updates for long-term support.

**Steps**:

[Deploy the workload with migration sidecar](#deploy-the-workload-with-migration-sidecar)to proxy IMDS transactions.- Verify authentication transactions complete successfully.
- Schedule application SDK updates to supported Azure Identity versions.
- Once SDKs are updated, remove the proxy sidecar and redeploy applications.

## Rewrite application for latest Azure Identity SDK

**This migration path applies when** your application uses an older version of the Azure Identity SDK and you want to update to the latest supported SDK before migrating.

**Migration approach**: Update your application code to use the latest Azure Identity SDK, then migrate to Microsoft Entra Workload ID with the updated code.

**Technical outcomes**:

- Uses current Azure Identity SDK versions (no deprecation timeline).
- Supports both Linux and Windows containers (unlike sidecar approach).
- Eliminates proxy components and IMDS translation overhead.

**Steps**:

- Update your application code to use the latest
[Azure Identity SDK](workload-identity-overview#prerequisites). - Test the updated application with pod-managed identity.
- Restart your application deployment to begin authenticating using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify authentication transactions complete successfully.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations and add-on.

## Set an active Azure subscription

Set a specific Azure subscription as the current active subscription using the

command.`az account set`

`az account set --subscription $SUBSCRIPTION_ID`


## Create a managed identity

Create a managed identity using the

command.`az identity create`

`az identity create --name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --location $LOCATION --subscription $SUBSCRIPTION_ID`


## Get managed identity client ID

Get the client ID of the managed identity and save it to an environmental variable using the

command.`az identity show`

`export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $MANAGED_IDENTITY_NAME --query 'clientId' -otsv)"`


## Grant managed identity access to Azure resources

- Grant the managed identity the permissions needed to access the required Azure resources. Follow the steps in
[Assign a managed identity access to a resource](/en-us/azure/role-based-access-control/role-assignments-portal-managed-identity)to assign the appropriate role to the managed identity.

## Get OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the

command.`az aks show`

`export AKS_OIDC_ISSUER="$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "oidcIssuerProfile.issuerUrl" -o tsv)"`

The variable should contain an issuer URL similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/`

By default, the issuer uses the base URL

`https://{region}.oic.prod-aks.azure.com/{uuid}`

, where the value for`{region}`

matches the location the AKS cluster is deployed in. The value`{uuid}`

represents the OIDC key.

## Get AKS cluster credentials

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`


## Create Kubernetes service account

Create a Kubernetes service account and annotate it with the managed identity client ID using the

`kubectl apply`

command. Make sure to replace the placeholder values with your own values.`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

The following output resembles successful creation of the identity:

`Serviceaccount/workload-identity-sa created`


## Establish federated identity credential trust

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME} --audience api://AzureADTokenExchange`

The federated identity credential takes a few minutes to propagate after being added. If a token request is made immediately after adding the federated identity credential, the token request might fail because the Azure AD directory cache contains outdated information.


## Deploy the workload with migration sidecar

If your application uses user-assigned managed identity and still relies on IMDS to get an access token you can use the migration sidecar to start migrating to Microsoft Entra Workload ID. In long-term applications, you should modify the code to use the latest Azure Identity SDKs that support client assertion.

To update or deploy the workload, add the following [pod annotations](workload-identity-overview#pod-annotations) to your pod specification (only if you want to use the migration sidecar):

| Pod annotation | Description | Value |
|---|---|---|
`azure.workload.identity/inject-proxy-sidecar` |
Indicates whether to inject the proxy sidecar into the pod. | `true` or `false` |
`azure.workload.identity/proxy-sidecar-port` |
Desired port for the proxy sidecar. | Default value: `8000` |

When you create a pod with these annotations, the Microsoft Entra Workload ID mutating webhook automatically injects the `init-container`

and proxy sidecar to the pod spec. The following YAML shows an example of what the mutating webhook adds to the pod deployment:

```
apiVersion: v1
kind: Pod
metadata:
name: httpbin-pod
labels:
app: httpbin
azure.workload.identity/use: "true"
annotations:
azure.workload.identity/inject-proxy-sidecar: "true"
spec:
serviceAccountName: workload-identity-sa
initContainers:
- name: init-networking
image: mcr.microsoft.com/oss/azure/workload-identity/proxy-init:v1.1.0
securityContext:
capabilities:
add:
- NET_ADMIN
drop:
- ALL
privileged: true
runAsUser: 0
env:
- name: PROXY_PORT
value: "8000"
containers:
- name: nginx
image: nginx:alpine
ports:
- containerPort: 80
- name: proxy
image: mcr.microsoft.com/oss/azure/workload-identity/proxy:v1.1.0
ports:
- containerPort: 8000
```


## Verify the workload with migration sidecar

Verify the pod is in a running state using the

command. Replace`kubectl describe pod`

`<pod-name>`

with the name of your pod.`kubectl describe pods <pod-name>`

Verify the pod is passing IMDS transactions using the

command. Replace`kubectl logs`

`<pod-name>`

with the name of your pod.`kubectl logs <pod-name>`

The following example log output resembles successful communication through the proxy sidecar. Verify the logs show a token is successfully acquired and the

`GET`

operation is successful.`I0926 00:29:29.968723 1 proxy.go:97] proxy "msg"="starting the proxy server" "port"=8080 "userAgent"="azure-workload-identity/proxy/v0.13.0-12-gc8527f3 (linux/amd64) c8527f3/2022-09-26-00:19" I0926 00:29:29.972496 1 proxy.go:173] proxy "msg"="received readyz request" "method"="GET" "uri"="/readyz" I0926 00:29:30.936769 1 proxy.go:107] proxy "msg"="received token request" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>" I0926 00:29:31.101998 1 proxy.go:129] proxy "msg"="successfully acquired token" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>"`


## Remove pod-managed identity

After you complete your testing and the application can successfully get a token using the proxy sidecar, you can remove the identity and pod-managed identity mapping from your AKS cluster

Remove the pod-managed identity binding from your pod using the

command. Replace`az aks pod-identity delete`

`<pod-identity-name>`

and`<pod-identity-namespace>`

with the name and namespace of your pod identity.`az aks pod-identity delete --name <pod-identity-name> --namespace <pod-identity-namespace> --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME`


## Related content

For more information about Microsoft Entra Workload ID, see the [Overview](workload-identity-overview) article.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-taints -->

# Use node taints in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use node taints in an Azure Kubernetes Service (AKS) cluster.

## Overview

The AKS scheduling mechanism is responsible for placing pods onto nodes and is based upon the upstream Kubernetes scheduler, [kube-scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/). You can constrain a pod to run on particular nodes by attaching the pods to a set of nodes using [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) or by instructing the node to repel a set of pods using [node taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/), which interact with the AKS scheduler.

Node taints work by marking a node so that the scheduler avoids placing certain pods on the marked nodes. You can place [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) on a pod to allow the scheduler to schedule that pod on a node with a matching taint. Taints and tolerations work together to help you control how the scheduler places pods onto nodes. For more information, see [example use cases of taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations).

Taints are key-value pairs with an [effect](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). There are three values for the effect field when using node taints: `NoExecute`

, `NoSchedule`

, and `PreferNoSchedule`

.

`NoExecute`

: Pods already running on the node are immediately evicted if they don't have a matching toleration. If a pod has a matching toleration, it might be evicted if`tolerationSeconds`

are specified.`NoSchedule`

: Only pods with a matching toleration are placed on this node. Existing pods aren't evicted.`PreferNoSchedule`

: The scheduler avoids placing any pods that don't have a matching toleration.

### Node taint options

There are two types of node taints that can be applied to your AKS nodes: **node taints** and **node initialization taints**.

**Node taints**are meant to remain permanently on the node for scheduling pods with node affinity. Node taints can only be added, updated, or removed completely using the AKS API.**Node initialization taints**are placed on the node at boot time and are meant to be used temporarily, such as in scenarios where you might need extra time to set up your nodes. You can remove node initialization taint using the Kubernetes API and they aren't guaranteed during the node lifecycle. They will appear on new replicas of the node when it is scaled up or on all replicas when a node is upgraded. If you want to remove the initialization taints completely, you can remove them using the AKS API after untainting the nodes using the Kubernetes API. Once you remove the initialization taints from the cluster spec using the AKS API, newly created nodes don't come up with those initialization taints. If the initialization taint is still present on existing nodes, you can permanently remove it by performing a node image upgrade operation.

Note

Node taints and labels applied using the AKS node pool API aren't modifiable from the Kubernetes API and vice versa. Modifications to system taints aren't allowed.

This doesn't apply to node initialization taints.

## Use node taints

### Prerequisites

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### Create a node pool with a node taint

Create a node pool with a taint using the

command and use the`az aks nodepool add`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 1 \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


### Update a node pool to add a node taint

Update a node pool to add a node taint using the

command and use the`az aks nodepool update`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool update \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


## Use node initialization taints (preview)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Prerequisites and limitations

- You need the Azure CLI version
`3.0.0b3`

or later installed and configured. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can only apply initialization taints via cluster create or upgrade when using the AKS API. If using ARM template that will result in a Managed Cluster level operation, you can specify node initialization taints during node pool creation and update. Agentpool level operations are blocked when
`NodeInitializationTaints`

are present in the request body. - You can't apply initialization taints to Windows node pools using the Azure CLI.

### Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `NodeInitializationTaintsPreview`

feature flag

Register the

`NodeInitializationTaintsPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a cluster with a node initialization taint

Create a cluster with a node initialization taint using the

command and the`az aks create`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

The node initialization taints you specify apply to all of the node pools in the cluster. To apply the initialization taint to a specific node, you can use an ARM template instead of the CLI.

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-count 1 \ --node-init-taints "sku=gpu:NoSchedule" \ --generate-ssh-keys`


### Update a cluster to add a node initialization taint

Update a cluster to add a node initialization taint using the

command and the`az aks update`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

When updating a cluster with a node initialization taint, the taints apply to all node pools in the cluster. If your nodes are using VMSS, you can view updates to node initialization taints on the node after the node's VMSS model is updated (for example, after a node image version upgrade operation). Initialization taints will not appear on your nodes until an operation that triggers a VMSS model update occurs.

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints "sku=gpu:NoSchedule"`


## Check the status of the node pool

After applying the node taint or initialization taint, check the status of the node pool using the

command.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`

If you applied node initialization taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeInitializationTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeInitializationTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`


## Check that the taint is set on the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool has the specified`Taints`

:`[ ... Name: <node-pool-name> ... Taints: sku=gpu:NoSchedule ... ], ... ... ]`


Important

If your nodes are using VMSS, node initialization taints will not be visible on actual nodes in your cluster until an operation that triggers VMSS model update occurs (for example, Kubernetes version upgrade or node image version upgrade).

## Remove node taints

### Remove a specific node taint

Remove node taints using the

command. The following example command removes the`az aks nodepool update`

`"sku=gpu:NoSchedule"`

node taint from the node pool.`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --node-taints ""`


### Remove all node taints

Remove all node taints from a node pool using the

command. The following example command removes all node taints from the node pool.`az aks nodepool update`

`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --name $NODE_POOL_NAME \ --node-taints ""`


## Remove node initialization taints

You have the following options to remove node initialization taints from the node:

**Remove node initialization taints temporarily**using the Kubernetes API. If you remove them this way, the taints reappear after node scaling or upgrade occurs. New nodes still have the node initialization taint after scaling. Node initialization taints appear on all nodes after upgrading.**Remove node initialization taints permanently**by untainting the node using the Kubernetes API, and then removing the taint using the AKS API. Once the initialization taints are removed from cluster spec using AKS API, newly created nodes after reimage operations no longer have initialization taints.

When you remove all initialization taint occurrences from node pool replicas, the existing initialization taint might reappear after an upgrade with any new initialization taints.

### Remove node initialization taints temporarily

Remove node initialization taints temporarily using the

`kubectl taint nodes`

command.This command removes the taint from only the specified node. If you want to remove the taint from every node in the node pool, you need to run the command for every node that you want the taint removed from.

`kubectl taint nodes $NODE_POOL_NAME sku=gpu:NoSchedule-`

Once removed, node initialization taints reappear after node scaling or upgrading occurs.


### Remove node initialization taints permanently

Follow steps in

[Remove node initialization taints temporarily](#remove-node-initialization-taints-temporarily)to remove the node initialization taint using the Kubernetes API.Remove the taint from the node using the AKS API using the

command. This command removes the node initialization taint from every node in the cluster.`az aks update`

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints ""`


## Check that the taint has been removed from the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you removed a node taint, the following example output shows that the

`<node-pool-name>`

node pool doesn't have the removed taint under`Taints`

:`[ ... Name: <node-pool-name> ... Taints: ... ], ... ... ]`


## Next steps

- Learn more about example use cases for
[taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations). - Learn more about
[best practices for advanced AKS scheduler features](operator-best-practices-advanced-scheduler). - Learn more about Kubernetes labels in the
[Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-images -->

# Node images in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the node images available for Azure Kubernetes Service (AKS) nodes.

Important

Starting on **March 17, 2027**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Older node images can contain unpatched security vulnerabilities and might not work properly with recently released features. Using older images might lead to issues with scaling, node readiness, and security. Depending on the age of the image version, it could also place the cluster outside of the support scope until you perform a node image upgrade. **We recommend that you keep node images current and enable automatic upgrades**.

## Node image releases

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to access the latest AKS features, component updates, and security fixes. You can find detailed summaries of each node image version in the [AKS VHD notes](https://github.com/Azure/AKS/tree/master/vhd-notes).

Linux node images are released weekly, and Windows node images are released monthly. New node images are included in the [AKS release notes](https://github.com/Azure/AKS/releases).


Best practice guidanceConfigure

[automatic node image upgrades]and schedule them using[planned maintenance]. This will ensure that your node images are always up to date without requiring manual upgrades.

When new node images are released, it can take up to two weeks for the updates to be rolled out across all regions. The [AKS Release Tracker](release-tracker) shows the current latest node image version, three previously available node image versions for each region, and the node image update order by region. Once the node image is available in your region, you can perform a [manual node image upgrade](node-image-upgrade) or configure [automatic node image upgrades](auto-upgrade-node-os-image) and schedule them using [planned maintenance](planned-maintenance).

## Default node images

AKS sets a default operating system (OS) and node image during cluster and node pool creation. OS Type can be used to filter between Linux or Windows.

| OS Type | Default OS | Default node image |
|---|---|---|
| Not Specified | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Linux | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Windows | Windows Server | Windows Server Long Term Servicing Channel (LTSC) with containerd and gen 1 |

Note

You can't specify the Windows OS Type during cluster creation since the system node pool in every cluster must be Linux.

### Factors that influence the default node image

The following factors influence the default image AKS chooses for your node pool:

**OS SKU**: If`--os-sku`

is specified, then your default OS changes. For example, if you specify Azure Linux as the OS SKU, then your node image is Azure Linux with containerd.**Virtual machine (VM) size**:**Hypervisor generation**: Each VM size supports Generation 1,[Generation 2](generation-2-vm), or both.- If Generation 2 is supported, AKS defaults to using the Generation 2 node image in all OS versions except for Windows Server 2019 and Windows Server 2022.
- If only Generation 1 is supported, AKS defaults to using the Generation 1 node image. Generation 1 isn't supported for Azure Linux OS Guard (preview) or Flatcar Container Linux for AKS (preview).

**Feature enablement**: There are some features embedded into the node image. If you choose to use any of these features, your default node image changes.[Federal Information Processing Standards (FIPS)](enable-fips-nodes)changes the default node image for all Linux node pools.[Pod Sandboxing](use-pod-sandboxing)changes the default node image for Azure Linux node pools.[Trusted Launch](use-trusted-launch)changes the default node image for all Linux node pools.


Note

Certain features can't be combined in a single node pool. Follow links to the feature documentation to review the limitations.

## Available Linux node images

### Ubuntu node images

The Ubuntu node images are fully validated by AKS and supported by Microsoft, Canonical, and the Ubuntu community. AKS won't retire an Ubuntu version before the end of Canonical's support lifecycle.

| Node image | Use case | Limitations |
|---|---|---|
Ubuntu with containerd and Gen 1 |
This is the standard node image for Ubuntu node pools using a VM size that only supports Generation 1. | N/A |
Ubuntu with containerd and Gen 2 |
This is the standard node image for Ubuntu node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Ubuntu with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Ubuntu with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Ubuntu with containerd and CVM**[Confidential VM](use-cvm)size. These images support Generation 2 only.**Ubuntu with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.### Azure Linux node images

The Azure Linux node images are fully validated by AKS and built from source, using a native AKS image.

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with containerd and Gen 1 |
This is the standard node image for Azure Linux node pools using a VM size that only supports Generation 1. | N/A |
Azure Linux with containerd and Gen 2 |
This is the standard node image for Azure Linux node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, node image is selected. | N/A |
Azure Linux with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Azure Linux with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd, FIPS, and Arm64**[Federal Information Processing Standards (FIPS)](enable-fips-nodes)and use a VM size that supports[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.**Azure Linux with containerd and Pod Sandboxing**[Pod Sandboxing](use-pod-sandboxing). These images support Generation 2 only.### Azure Linux with OS Guard for AKS (preview) node images

The Azure Linux with OS Guard for AKS node images are fully validated by AKS and built from source, using a native AKS image. Versioning for Azure Linux with OS Guard node images follow the AKS date-based format (for example: 202509.23.0). You can check the node images in the release notes and by running the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For more information, see [Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with OS Guard with containerd, Gen 2, FIPS, and Trusted Launch |
This is the standard node image for Azure Linux with OS Guard for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Azure Linux with OS Guard. | N/A |

### Flatcar Container Linux for AKS (preview) node images

The Flatcar Container Linux for AKS node images are fully validated by AKS and supported by Microsoft and the Flatcar community. Versioning for Flatcar Container Linux node images follow the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. You can check the Flatcar version number (for example: Flatcar 4344.0.0) in the release notes and by running the `kubectl get nodes`

command. For more information, see [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).

| Node image | Use case | Limitations |
|---|---|---|
Flatcar Container Linux with containerd and Gen 2 |
This is the standard node image for Flatcar Container Linux for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Flatcar OS. | N/A |
Flatcar Container Linux with containerd and Arm64 |
This is a variant of the default node image for customers that use a VM size that supports
|

## Available Windows Server node images

The Windows Server node images are fully validated by AKS and supported by Microsoft.

### Windows Server Long Term Servicing Channel (LTSC) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2019 or Windows Server 2022. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2025. | N/A |

### Windows Server Annual Channel for Containers (preview) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that only supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. | N/A |

## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-support-policy -->

# Support policy for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines the support policy for the Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

## Versioning and support policy

### Service mesh add-on release calendar

The Istio-based service mesh add-on release calendar indicates each revision's AKS compatibility and estimated release and deprecation dates.

New minor revisions and patches are rolled out as part of AKS releases. Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To see real-time updates of regional release status and AKS release notes containing updates about Istio revision support, visit the [AKS release status webpage](https://releases.aks.azure.com/).

| Service mesh revision | Upstream release | AKS release | End of life | Compatible AKS versions | Compatible AKS LTS versions |
|---|---|---|---|---|---|
| asm-1-17 | Feb 2023 | Apr 2023 | Jan 2024 | 1.23, 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-18 | Jun 2023 | Nov 2023 | Feb 2024 | 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-19 | Sept 2023 | Jan 2024 | Jun 2024 | 1.25, 1.26, 1.27, 1.28 | |
| asm-1-20 | Nov 2023 | Feb 2024 | Sept 2024 | 1.25, 1.26, 1.27, 1.28, 1.29 | |
| asm-1-21 | Mar 2024 | Apr 2024 | Oct 2024 | 1.26, 1.27, 1.28, 1.29, 1.30 | |
| asm-1-22 | May 2024 | Jul 2024 | March 2025 | 1.27, 1.28, 1.29, 1.30 | |
| asm-1-23 | Aug 2024 | Sept 2024 | June 2025 | 1.27, 1.28, 1.29, 1.30, 1.31, 1.32 | |
| asm-1-24 | Nov 2024 | Feb 2025 | Sept 2025 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 | |
| asm-1-25 | Mar 2025 | May 2025 | Jan 2026 | 1.29, 1.30, 1.31, 1.32, 1.33 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 |
| asm-1-26 | May 2025 | July 2025 | ~Feb 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 |
| asm-1-27 | Aug 2025 | Sept 2025 | ~May 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |
| asm-1-28 | Nov 2025 | Jan 2026 | ~Aug 2026 (expected) | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |

If using an AKS [long term-support (LTS) cluster](long-term-support), a newer revision may be declared as compatible when a previous compatible Istio revision reaches end of life before the AKS LTS version's end of life. For more details, read Istio's [AKS compatibility policy](#aks-compatibility).

### Supported revisions

**Minor revision**:- At any given time, at least two revisions of the Istio-based service mesh add-on are supported.
- An older revision
`n-2`

will continue to be supported until six weeks after the newest revision`n`

starts rolling out to all regions. For example, if`asm-1-22`

just started rolling out to all regions,`asm-1-20`

will be deprecated after six weeks. - Deprecation means no new mesh installations can be done with this revision. While clusters already having this revision continue to work, for support issues and security patches, it's recommended to
[upgrade to a newer supported mesh revision](istio-upgrade#minor-revision-upgrade).

**Patch version**:- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then
[upgrade istio-proxy sidecars by restarting their workloads](istio-upgrade#patch-version-upgrade). - AKS reserves the right to deprecate patches if a critical Common Vulnerability and Exposure (CVE) or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to
[AKS release notes](https://github.com/Azure/AKS/releases)and visit the[AKS release status webpage](https://releases.aks.azure.com/).

- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then

### Default revision

If a revision isn't explicitly provided by user during installation, the `n-1`

revision is installed by default. For example, if `asm-1-22`

is the latest revision, the default is `asm-1-21`

.

### AKS compatibility

Each revision of the add-on is compatible with a set of AKS minor versions established by the [upstream Istio support and release calendar](https://istio.io/latest/docs/releases/supported-releases/#support-status-of-istio-releases).

**AKS LTS clusters may be compatible with additional revisions beyond upstream Istio's support table.** For Istio revisions `asm-1-25`

+ and AKS LTS versions 1.28+, every supported AKS LTS version will have *at least one* compatible Istio revision.

To check the compatible AKS versions for an Istio revision, use the command [ az aks mesh get-revisions](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-revisions):

```
az aks mesh get-revisions --location <location> -o table
```


This command has been updated to include separate `CompatibleWith`

outputs for `KubernetesOfficial`

(standard tier) and `AKSLongTermSupport`

, replacing the earlier response that only included `kubernetes`

(standard tier).

If using the Azure portal to enable the Istio add-on for an existing cluster, the available Istio revisions will be filtered based on the cluster's tier.

Each Istio add-on revision follows upstream lifecycle for end of life and patch availability. This means:

Every Istio revision will not be compatible with every AKS LTS version, but every AKS LTS version will be compatible with at least one Istio add-on revision.

If an Istio revision reaches end of life before the AKS LTS version it is compatible with, a newer revision will be declared compatible with that LTS version. The add-on will need to be upgraded to stay in support.

For example, if

`asm-1-26`

is compatible with AKS LTS 1.28, and`asm-1-26`

reaches end of life,`asm-1-27`

may become compatible with 1.28 LTS instead.

## Allowed, supported, and blocked customizations

The Istio-based service mesh add-on for AKS designates features and [configuration options](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values) as `allowed`

, `supported`

, or `blocked`

.

**Blocked**: Disallowed features and configuration options are blocked via add-on managed admission webhooks. The API server immediately publishes the error message to the user that the feature is disallowed.**Supported**: Supported features receive support from Azure support.**Allowed**: Allowed features are open and available to Istio add-on users but aren't covered by Azure support.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-resource-management -->

# Best practices for application developers to manage resources in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), there are a few key areas to consider. The way you manage your application deployments can negatively impact the end-user experience of services you provide.

This article focuses on running your clusters and workloads from an application developer perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

This article covers the following topics:

- Pod resource requests and limits.
- Ways to develop, debug, and deploy applications with Bridge to Kubernetes and Visual Studio Code.

## Define pod resource requests and limits


Best practice guidanceSet pod requests and limits on all pods in your YAML manifests. If the AKS cluster uses

resource quotasand you don't define these values, your deployment may be rejected.

Use pod requests and limits to manage compute resources within an AKS cluster. Pod requests and limits inform the Kubernetes scheduler of the compute resources to assign to a pod.

### Pod CPU/Memory requests

*Pod requests* define a set amount of CPU and memory the pod needs regularly.

In your pod specifications, it's important you define these requests and limits based on the above information. If you don't include these values, the Kubernetes scheduler can't consider the resources your applications require to help with scheduling decisions.

Monitor the performance of your application to adjust pod requests. If you underestimate pod requests, your application may receive degraded performance due to over-scheduling a node. If requests are overestimated, your application may have increased scheduling difficulty.

### Pod CPU/Memory limits

*Pod limits* set the maximum amount of CPU and memory a pod can use. *Memory limits* define which pods should be removed when nodes are unstable due to insufficient resources. Without proper limits set, pods are removed until resource pressure is lifted. While a pod may exceed the *CPU limit* periodically, the pod isn't removed for exceeding the CPU limit.

Pod limits define when a pod loses control of resource consumption. When it exceeds the limit, the pod is marked for removal. This behavior maintains node health and minimizes impact to pods sharing the node. If you don't set a pod limit, it defaults to the highest available value on a given node.

Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. Your application may try to consume too many resources on the node for other pods to successfully run.

Monitor the performance of your application at different times during the day or week. Determine peak demand times and align the pod limits to the resources required to meet maximum needs.

Important

In your pod specifications, define these requests and limits based on the above information. Failing to include these values prevents the Kubernetes scheduler from accounting for resources your applications require to help with scheduling decisions.

If the scheduler places a pod on a node with insufficient resources, application performance is degraded. Cluster administrators **must set resource quotas** on a namespace that requires you to set resource requests and limits. For more information, see

[resource quotas on AKS clusters](operator-best-practices-scheduler#enforce-resource-quotas).

When you define a CPU request or limit, the value is measured in CPU units.

*1.0*CPU equates to one underlying virtual CPU core on the node.- The same measurement is used for GPUs.

- You can define fractions measured in millicores. For example,
*100 m*is*0.1*of an underlying vCPU core.

In the following basic example for a single NGINX pod, the pod requests *100 m* of CPU time and *128Mi* of memory. The resource limits for the pod are set to *250 m* CPU and *256Mi* memory.

```
kind: Pod
apiVersion: v1
metadata:
name: mypod
spec:
containers:
- name: mypod
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
```


For more information about resource measurements and assignments, see [Managing compute resources for containers](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/).

## Develop and debug applications against an AKS cluster


Best practice guidanceDevelopment teams should deploy and debug against an AKS cluster using Bridge to Kubernetes.


With Bridge to Kubernetes, you can develop, debug, and test applications directly against an AKS cluster. Developers within a team collaborate to build and test throughout the application lifecycle. You can continue to use existing tools such as Visual Studio or Visual Studio Code with the Bridge to Kubernetes extension.

Using integrated development and test process with Bridge to Kubernetes reduces the need for local test environments like [minikube](https://kubernetes.io/docs/setup/minikube/). Instead, you develop and test against an AKS cluster, even in secured and isolated clusters.

Note

Bridge to Kubernetes is intended for use with applications running on Linux pods and nodes.

## Use the Visual Studio Code (VS Code) extension for Kubernetes


Best practice guidanceInstall and use the VS Code extension for Kubernetes when you write YAML manifests. You can also use the extension for integrated deployment solution, which may help application owners that infrequently interact with the AKS cluster.


The [Visual Studio Code extension for Kubernetes](https://github.com/Azure/vscode-kubernetes-tools) helps you develop and deploy applications to AKS. The extension provides the following features:

Intellisense for Kubernetes resources, Helm charts, and templates.

The ability to browse, deploy, and edit capabilities for Kubernetes resources from within VS Code.

Intellisense checks for resource requests or limits being set in the pod specifications:


## Next steps

This article focused on how to run your cluster and workloads from a cluster operator perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

To implement some of these best practices, see [Develop with Bridge to Kubernetes](/en-us/visualstudio/containers/overview-bridge-to-kubernetes).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-ai-quickstart -->

# Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy an application that uses Azure OpenAI or OpenAI on AKS. With OpenAI, you can easily adapt different AI models, such as content generation, summarization, semantic search, and natural language to code generation, for your specific tasks. You start by deploying an AKS cluster in your Azure subscription. Then, you deploy your OpenAI service and the sample application.

The sample cloud native application is representative of real-world implementations. The multi-container application is comprised of applications written in multiple languages and frameworks, including:

- Golang with Gin
- Rust with Actix-Web
- JavaScript with Vue.js and Fastify
- Python with FastAPI

These applications provide front ends for customers and store admins, REST APIs for sending data to RabbitMQ message queue and MongoDB database, and console apps to simulate traffic.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

To access the GitHub codebase for the sample application, see [AKS Store Demo](https://github.com/Azure-Samples/aks-store-demo).

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - For this demo, you can either use Azure OpenAI service or OpenAI service.
- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the
[Request access to Azure OpenAI Service form](https://aka.ms/oai/access). - If you plan on using OpenAI, sign up on the
[OpenAI website](https://openai.com/).

- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which you deploy and manage Azure resources. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

The following example output shows successful creation of the resource group:

`{ "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup", "location": "eastus", "managedBy": null, "name": "myResourceGroup", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

The following example creates a cluster named *myAKSCluster* in *myResourceGroup*.

Create an AKS cluster using the

command.`az aks create`

`az aks create --resource-group myResourceGroup --name myAKSCluster --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Connect to the cluster

To manage a Kubernetes cluster, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`

Note

If your Linux-based system requires elevated permissions, you can use the

`sudo az aks install-cli`

command.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

This command executes the following operations:

- Downloads credentials and configures the Kubernetes CLI to use them.
- Uses
`~/.kube/config`

, the default location for the[Kubernetes configuration file](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/). Specify a different location for your Kubernetes configuration file using*--file*argument.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31469198-vmss000000 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000001 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000002 Ready agent 3h29m v1.25.6`


Note

For private clusters, the nodes might be unreachable if you try to connect to them through the public IP address. In order to fix this, you need to create an endpoint within the same VNET as the cluster to connect from. Follow the instructions to [Create a private AKS cluster](private-clusters) and then connect to it.

## Deploy the application

The [AKS Store application](https://github.com/Azure-Samples/aks-store-demo) manifest includes the following Kubernetes deployments and services:

**Product service**: Shows product information.**Order service**: Places orders.**Makeline service**: Processes orders from the queue and completes the orders.**Store front**: Web application for customers to view products and place orders.**Store admin**: Web application for store employees to view orders in the queue and manage product information.**Virtual customer**: Simulates order creation on a scheduled basis.**Virtual worker**: Simulates order completion on a scheduled basis.**Mongo DB**: NoSQL instance for persisted data.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Review the

[YAML manifest](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-all-in-one.yaml)for the application.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-all-in-one.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/mongodb created service/mongodb created deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/makeline-service created service/makeline-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created deployment.apps/store-admin created service/store-admin created deployment.apps/virtual-customer created deployment.apps/virtual-worker created`


## Deploy OpenAI

You can either use Azure OpenAI or OpenAI and run your application on AKS.

- In the Azure portal, create an Azure OpenAI instance.
- Navigate to the Azure OpenAI instance you created.
- From the
**Overview**blade, navigate to the[Azure AI Foundry portal](https://oai.azure.com/portal/). - Create a new
**Chat**deployment using the**gpt-4o-mini**base model.

For more information on how to create a deployment in Azure OpenAI, see [Get started generating text using Azure OpenAI Service](/en-us/azure/ai-services/openai/quickstart).

## Deploy the AI service

Now that the application is deployed, you can deploy the Python-based microservice that uses OpenAI to automatically generate descriptions for new products being added to the store's catalog.

Create a file named

`ai-service.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "" - name: AZURE_OPENAI_ENDPOINT value: "" - name: OPENAI_API_KEY value: "" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: ai-service spec: type: ClusterIP ports: - name: http port: 5001 targetPort: 5001 selector: app: ai-service`

Set the environment variable

`USE_AZURE_OPENAI`

to`"True"`

.Get your Azure OpenAI deployment name from

[Azure AI Foundry](https://oai.azure.com/portal/)and fill in the`AZURE_OPENAI_DEPLOYMENT_NAME`

value.Get your Azure OpenAI endpoint and Azure OpenAI API key from the Azure portal by selecting

**Keys and Endpoint**in the left blade of the resource. Update the`AZURE_OPENAI_ENDPOINT`

and`OPENAI_API_KEY`

in the YAML accordingly.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f ai-service.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/ai-service created service/ai-service created`


Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use [Managed Identity](/en-us/azure/ai-services/openai/how-to/managed-identity#authorize-access-to-managed-identities) to authenticate to Azure OpenAI service instead or store your secrets in [Azure Key Vault](csi-secrets-store-driver).

## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods`

Make sure all the pods are

*Running*before continuing to the next step.`NAME READY STATUS RESTARTS AGE makeline-service-7db94dc7d4-8g28l 1/1 Running 0 99s mongodb-78f6d95f8-nptbz 1/1 Running 0 99s order-service-55cbd784bb-6bmfb 1/1 Running 0 99s product-service-6bf4d65f74-7cbvk 1/1 Running 0 99s rabbitmq-9855984f9-94nlm 1/1 Running 0 99s store-admin-7f7d768c48-9hn8l 1/1 Running 0 99s store-front-6786c64d97-xq5s9 1/1 Running 0 99s virtual-customer-79498f8667-xzsb7 1/1 Running 0 99s virtual-worker-6d77fff4b5-7g7rj 1/1 Running 0 99s`

Get the IP of the store admin web application and store front web application using the

`kubectl get service`

command.`kubectl get service store-admin`

The application exposes the Store Admin site to the internet via a public load balancer provisioned by the Kubernetes service. This process can take a few minutes to complete.

**EXTERNAL IP**initially shows*pending*until the service comes up and shows the IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-admin LoadBalancer 10.0.142.228 40.64.86.161 80:32494/TCP 50m`

Repeat the same step for the service named `store-front``.

Open a web browser and browse to the external IP address of your service. In the example shown here, open

*40.64.86.161*to see Store Admin in the browser. Repeat the same step for Store Front.In store admin, select the products tab, then select

**Add Products**.When the `ai-service`` is running successfully, you should see the Ask OpenAI button next to the description field. Fill in the name, price, and keywords, then generate a product description by selecting

**Ask OpenAI**>**Save product**.You can now see the new product you created on Store Admin used by sellers. In the picture, you can see Dog Smart Collar is added.

You can also see the new product you created on Store Front used by buyers. In the picture, you can see Dog Smart Collar is added. Remember to get the IP address of store front using the

command.`kubectl get service`


## Next steps

Now that you added OpenAI functionality to an AKS application, you can [Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)](open-ai-secure-access-quickstart).

To learn more about generative AI use cases, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-settings -->

# Configure the Dapr extension for your Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After [completing the prerequisites for installing the Dapr extension](dapr), you can configure the [Dapr](https://dapr.io/) extension to work best for you and your project using various configuration options, like:

- Rotating expiring certificates
- Provisioning Dapr with high availability (HA) enabled
- Limiting which of your nodes use the Dapr extension
- Setting automatic custom resource definition (CRD) updates
- Configuring the Dapr release namespace

The extension enables you to set Dapr configuration options by using the `--configuration-settings`

parameter in the Azure CLI or `configurationSettings`

property in a Bicep template.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Update configuration settings

Important

Some configuration options cannot be modified post-creation. Adjustments to these options require deletion and recreation of the extension, applicable to the following settings:

`global.ha.*`

`dapr_placement.*`


HA is enabled by default. Disabling it requires deletion and recreation of the extension.

To update your Dapr configuration settings, recreate the extension with the desired state. For example, let's say you previously created and installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


To update the `dapr_operator.replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=3"
```


## Manage mTLS certificates

The Dapr extension supports in-transit encryption of communication between Dapr instances using the Dapr Sentry service control plane, which is a central Certificate Authority (CA). With the Sentry service, you can encrypt communication using self-signed or user-supplied x.509 certificates. [Learn more about setting up mTLS certificates in the open-source Dapr documentation.](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates)

You can [bring in your own certificates](https://docs.dapr.io/operations/security/mtls/#bringing-your-own-certificates), or let [Dapr automatically create and persist self-signed root and issuer certificates](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates).

Important

If you don't explicitly configure certificates, [Dapr defaults to generating self-signed certificates](#manage-dapr-generated-self-signed-certificates), which are generally valid for 1 year. **Currently, using self-signed certificates generated by Dapr is not recommended.** Best practice is to generate custom certificates and update them manually.

### Manage Dapr-generated self-signed certificates

If you haven't provided any custom certificates, Dapr automatically creates and persists self-signed certificates, valid for 1 year. The Dapr extension installs the `dapr-trust-bundle`

secret, which contains certificate information under the default `dapr-system`

namespace.

#### Check expiry of current Dapr-generated self-signed certificates

You can check when the Dapr root certificate of your Kubernetes cluster expires by using [the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/).

```
dapr mtls expiry
```


**Expected output:**

```
Root certificate expires in 8759 hours. Expiry date: 2025-12-06 18:14:20 +0000 UTC
```


You can also find the expiration date for your current certificate in the Kubernetes `dapr-trust-bundle`

secret data.

```
kubectl get secret dapr-trust-bundle -n dapr-system -o jsonpath='{.data.issuer\.crt}' | base64 -d | openssl x509 -noout -dates
```


**Expected output:**

```
notBefore=Dec 6 17:59:20 2024 GMT
notAfter=Dec 6 18:14:20 2025 GMT
```


#### Generate a new Dapr-generated self-signed certificate

**Via the Dapr CLI (recommended)**

Refer to Dapr's[Root and issuer certificate upgrade using CLI](https://docs.dapr.io/operations/security/mtls/#root-and-issuer-certificate-upgrade-using-cli-recommended)guide.**Via**Refer to Dapr's`kubectl`

commands[Updating root or issuer certs using Kubectl](https://docs.dapr.io/operations/security/mtls/#updating-root-or-issuer-certs-using-kubectl)guide.

### Manage your own user-supplied x.509 certificates

You can also bring your own custom certificates.

**Generate custom certificates**

Create your own custom certificate; for example,[an Azure Key Vault certificate](/en-us/azure/key-vault/certificates/certificate-scenarios).**Update your custom certficate manually**

Follow[the instructions provided in the Dapr open source documentation to update your custom certificates manually](https://docs.dapr.io/operations/security/mtls/#custom-certificates-bring-your-own)using.`kubectl`


## Provision Dapr with high availability (HA) enabled

Provision Dapr with high availability (HA) enabled by setting the `global.ha.enabled`

parameter to `true`

.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

If no configuration-settings are passed, the Dapr configuration defaults to:

```
ha:
enabled: true
replicaCount: 3
disruption:
minimumAvailable: ""
maximumUnavailable: "25%"
prometheus:
enabled: true
port: 9090
mtls:
enabled: true
workloadCertTTL: 24h
allowedClockSkew: 15m
```


For a list of available options, see [Dapr configuration](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md#configuration).

## Limit the extension to certain nodes

In some configurations, you may only want to run Dapr on certain nodes. You can limit the extension by passing a `nodeSelector`

in the extension configuration. If the desired `nodeSelector`

contains `.`

, you must escape them from the shell and the extension. For example, the following configuration installs Dapr only to nodes with `topology.kubernetes.io/zone: "us-east-1c"`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.nodeSelector.kubernetes\.io/zone=us-east-1c"
```


For managing OS and architecture, use the [supported versions](https://github.com/dapr/dapr/blob/b8ae13bf3f0a84c25051fcdacbfd8ac8e32695df/docker/docker.mk#L50) of the `global.daprControlPlaneOs`

and `global.daprControlPlaneArch`

configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.daprControlPlaneOs=linux" \
--configuration-settings "global.daprControlPlaneArch=amd64"
```


## Install Dapr in multiple availability zones while in HA mode

By default, the placement service uses a storage class of type `standard_LRS`

. It's recommended to create a **zone redundant storage class** while installing Dapr in HA mode across multiple availability zones. For example, to create a `zrs`

type storage class, add the `storageaccounttype`

parameter:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: custom-zone-redundant-storage
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
storageaccounttype: Premium_ZRS
```


When installing Dapr, use the storage class you used in the YAML file:

```
az k8s-extension create --cluster-type managedClusters
--cluster-name XXX
--resource-group XXX
--name XXX
--extension-type Microsoft.Dapr
--auto-upgrade-minor-version XXX
--version XXX
--configuration-settings "dapr_placement.volumeclaims.storageClassName=custom-zone-redundant-storage"
```


## Configure the Dapr release namespace

You can configure the release namespace.

The Dapr extension gets installed in the `dapr-system`

namespace by default. To override it, use `--release-namespace`

. To redefine the namespace, include the cluster `--scope`

.

```
az k8s-extension create \
--cluster-type managedClusters \
--cluster-name dapr-aks \
--resource-group dapr-rg \
--name my-dapr-ext \
--extension-type microsoft.dapr \
--release-train stable \
--auto-upgrade false \
--version 1.9.2 \
--scope cluster \
--release-namespace dapr-custom
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Dapr configuration settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr
```


## Set Dapr monitoring log levels

You can configure settings for the Dapr monitoring component with your AKS cluster extension. For exmaple, to update `dapr_monitoring`

log levels to "warn" (only notified when receiving a warning or error), set the following `configuration-settings`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_monitoring.logLevel=warn"
```


## Set the outbound proxy for Dapr extension for Azure Arc on-premises

If you want to use an outbound proxy with the Dapr extension for AKS, you can do so by:

- Setting the proxy environment variables using the
:`dapr.io/env`

annotations`HTTP_PROXY`

`HTTPS_PROXY`

`NO_PROXY`


[Installing the proxy certificate in the sidecar](https://docs.dapr.io/operations/configuration/install-certificates/).

## Updating your Dapr installation version

If you are on a specific Dapr version and you don't have `--auto-upgrade-minor-version`

available, you can use the following command to upgrade or downgrade Dapr:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--version 1.12.0 # Version to upgrade or downgrade to
```


The preceding command updates the Dapr control plane *only.* To update the Dapr sidecars, restart your application deployments:

```
kubectl rollout restart deploy/<DEPLOYMENT-NAME>
```


## Using Azure Linux-based images

From Dapr version 1.8.0, you can use Azure Linux images with the Dapr extension. To use them, set the `global.tag`

flag:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--set global.tag=1.10.0-mariner
```


[Learn more about using Mariner-based images with Dapr](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-deploy/#using-mariner-based-images).[Learn more about deploying Azure Linux on AKS](cluster-configuration#azure-linux-container-host-for-aks).

## Disable automatic CRD updates

From Dapr version 1.9.2, CRDs are automatically upgraded when the extension upgrades. To disable this setting, you can set `hooks.applyCrds`

to `false`

.

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--configuration-settings "hooks.applyCrds=false"
```


Note

CRDs are only applied in case of upgrades and are skipped during downgrades.

## Meet network requirements

The Dapr extension requires the following outbound URLs on `https://:443`

to function on AKS and Arc for Kubernetes:

`https://mcr.microsoft.com/daprio`

URL for pulling Dapr artifacts.- The
[outbound URLs required for AKS or Arc for Kubernetes](/en-us/azure/azure-arc/kubernetes/network-requirements).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-flyte -->

# Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Flyte on Azure Kubernetes Service (AKS). Flyte is an open-source workflow orchestrator that unifies machine learning, data engineering, and data analytics stacks to help you build robust and reliable applications. When using Flyte as a Kubernetes-native workflow automation tool, you can focus on experimentation and providing business value without increasing your scope to infrastructure and resource management. Keep in mind that Flyte isn't officially supported by Microsoft, so use it at your own discretion.

For more information, see [Introduction to Flyte](https://www.union.ai/docs/flyte/user-guide/).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Flyte use cases

Flyte can be used for a variety of use cases, including:

- Deliver models for streamlined profit and loss financial calculations.
- Process petabytes of data to efficiently conduct 3D mapping of new areas.
- Quickly rollback to previous versions and minimize impact of bugs in your pipelines.

For more information, see [Flyte tutorials](https://www.union.ai/docs/flyte/tutorials/).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free).- If you have multiple subscriptions, make sure you select the correct one using the
`az account set --subscription <subscription-id>`

command.

- If you have multiple subscriptions, make sure you select the correct one using the
- The Azure CLI installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The Helm CLI installed and updated. Check your version using the
`helm version`

command. If you need to install or upgrade, see[Install Helm](https://helm.sh/docs/intro/install/). - The
`kubectl`

CLI installed and updated. Install it locally using the`az aks install-cli`

command or using[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - A local Docker development environment. For more information, see
[Get Docker](https://docs.docker.com/get-docker/). `flytekit`

and`flytectl`

installed. For more information, see[Flyte installation](https://www.union.ai/docs/flyte/user-guide/getting-started/local-setup/).

Note

If you're using the Azure Cloud Shell, the Azure CLI, Helm, and kubectl are already installed.

### Set environment variables

Set environment variables for use throughout the article. Replace the placeholder values with your own values.

`export RESOURCE_GROUP="<resource-group-name>" export LOCATION="<location>" export CLUSTER_NAME="<cluster-name>" export DNS_NAME_PREFIX="<dns-name-prefix>"`


## Create an AKS cluster

Create an Azure resource group for the AKS cluster using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command with the`az aks create`

`--enable-azure-rbac`

,`--enable-managed-identity`

,`--enable-aad`

, and`--dns-name-prefix`

parameters.`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac --enable-managed-identity --enable-aad --dns-name-prefix $DNS_NAME_PREFIX --generate-ssh-keys`


## Connect to your AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Add the Flyte Helm repository

Add the Flyte Helm repository using the

`helm repo add`

command.`helm repo add flyteorg https://flyteorg.github.io/flyte`


## Find Flyte Helm charts

Search for Flyte Helm charts using the

`helm search repo`

command.`helm search repo flyteorg`

The following example output shows some of the available Flyte Helm charts:

`NAME CHART VERSION APP VERSION DESCRIPTION flyteorg/flyte v1.12.0 A Helm chart for Flyte Sandbox flyteorg/flyte-binary v1.12.0 1.16.0 Chart for basic single Flyte executable deployment flyteorg/flyte-core v1.12.0 A Helm chart for Flyte core flyteorg/flyte-deps v1.12.0 A Helm chart for Flyte dependencies flyteorg/flyte-sandbox 0.1.0 1.16.1 A Helm chart for the Flyte local sandbox flyteorg/flyteagent v0.1.10 A Helm chart for Flyte Agent`

Update the repository using the

`helm repo update`

command.`helm repo update`


## Deploy a Flyte chart on AKS

In this section, you deploy the flyte-binary Helm chart so you can begin building and deploying data and machine learning pipelines with Flyte on AKS. The flyte-binary chart is a basic single Flyte executable deployment.

Create a namespace for your Flyte deployment using the

`kubectl create namespace`

command.`kubectl create namespace <namespace-name>`

Install a Flyte Helm chart using the

`helm install`

command. In this example, we use the`flyte-binary`

chart.`helm install flyte-binary flyteorg/flyte-core --namespace <namespace-name>`

Verify that the Flyte deployment is running using the

`kubectl get services`

command.`kubectl get services --namespace <namespace-name> --output wide`

The following condensed example output shows the Flyte deployment:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE flyteorg-flyte-binary-grpc ClusterIP xx.x.xx.xxx <none> 81/TCP 1m flyteorg-flyte-binary-http ClusterIP xx.x.xx.xxx <none> 80/TCP 1m flyteorg-flyte-binary-webhook ClusterIP xx.x.xx.xxx <none> 80/TCP 1m`


## Next steps

In this article, you learned how to install Flyte on AKS using a Helm chart.
The Flyte project also maintains a [reference implementation for AKS](https://github.com/unionai-oss/deploy-flyte/tree/main/environments/azure/flyte-core#readme) that automatically configures all the dependencies and deploys a production grade Flyte cluster.

To start building and deploying data and machine learning pipelines, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automated-deployments -->

# Automated deployments for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Automated Deployments streamline the process of setting up a GitHub Action or Azure DevOps Pipeline, making it easy to create a continuous deployment pipeline for your application to Azure Kubernetes Service (AKS). Once connected, every new commit automatically triggers the pipeline, delivering updates to your application seamlessly. You can either bring your own deployment files for quick pipeline creation or generate Dockerfiles and Kubernetes manifests to containerize and deploy non-containerized applications with minimal effort.

## Prerequisites

- A GitHub account or an Azure DevOps organization.
- An AKS cluster. If you don't have one, you can create one using the steps in
[Deploy an Azure Kubernetes Service (AKS) cluster](learn/quick-kubernetes-deploy-portal). - An Azure Container Registry (ACR). If you don't have one, you can create one using the steps in
[Integrate Azure Container Registry (ACR) with an Azure Kubernetes Service (AKS) cluster](cluster-container-registry-integration). - An application to deploy.

### Connect to source code repository

Create an automated deployment workflow and authorize it to connect to the desired source code repository.

- In the Azure portal, navigate to your AKS cluster resource.
- From the service menu, under
**Settings**, select**Automated deployments**>**Create**. - Under
**Repository details**, enter a name for the workflow, then select**GitHub or ADO**for your repository location. - Select
**Authorize access**to connect to the desired repository. - Choose the
**Repository**and**Branch**, and then select**Next**.

### Choose the container image configuration

To get an application ready for Kubernetes, you need to build it into a container image and store it in a container registry. You use a Dockerfile to provide instructions on how to build the container image. If your source code repository doesn't already have a Dockerfile, Automated Deployments can generate one for you. Otherwise, you can use an existing Dockerfile.

Use Automated Deployments to generate a Dockerfile for many languages and frameworks such as Go, C#, Node.js, Python, Java, Gradle, Clojure, PHP, Ruby, Erlang, Swift, and Rust. The language support is built on what's available in [draft.sh](https://draft.sh).

- Select
**Auto-containerize (generate Dockerfile)**for the container configuration. - Select the
**location of where to save the generated Dockerfile**in the repository. - Select the
**application environment**from the list of supported languages and frameworks. - Enter the
**application port**. - Provide the
**Dockerfile build context**path. - Select an existing
**Azure Container Registry**or create a new one. This registry is used to store the built application image.

### Choose the Kubernetes manifest configuration

Note

The Generate Manifests option also supports advanced features like Service Connector integration, auto-generated Ingress resources, and more detailed, customizable Kubernetes manifest files.

An application running on Kubernetes consists of many Kubernetes primitive components. These components describe what container image to use, how many replicas to run, if there's a public IP required to expose the application, etc. For more information, see the official [Kubernetes documentation][kubernetes-documentation]. If your source code repository doesn't already have the basic Kubernetes manifests to deploy, Automated Deployments can generate them for you. Otherwise, you can use a set of existing manifests. You can also choose an existing Helm chart.

If your code repository already has a Dockerfile, you can select it to be used to build the application image.

- Select
**Use existing Kubernetes manifest deployment files**for the deployment options. - Select the
**Kubernetes manifest file or folder**from your repository. - Select
**Next**.

## (Optional) Use a managed ingress and/or Service Connector

When generating Kubernetes manifests with Automated Deployments, you can optionally enable App Routing to set up an ingress controller for your application. You can also use Service Connector to create a new connection or seamlessly integrate your app with an existing Azure service backend.

App Routing provides a fully managed NGINX-based ingress controller out of the box, complete with built-in SSL/TLS encryption using certificates stored in Azure Key Vault and DNS zone management through Azure DNS. When using Automated Deployments, the expose ingress command integrates seamlessly with App Routing, making it easy to expose your application to external traffic under a secure, custom DNS name—with minimal configuration.

- Select the
**Expose ingress**box. - Choose between an
**Existing ingress controller**or a**New ingress controller**. - Choose between using a
**SSL/TLS enabled**or**Insecure**ingress controller. - (Optional) Enter
**Certificate details**if choosing a**SSL/TLS enabled**ingress controller. - Choose between using
**Azure DNS**or a**3rd party provider**. - Enter the
**Azure DNS Zone**and**Subdomain name**.

## (Optional) Add environment variables

Define environment variables for a container in Kubernetes by specifying name-value pairs. Environment variables are important as they help enable easier management of settings, secure handling of sensitive information, and flexibility across environments.

## Review configuration and deploy

Review the configuration for the application, and Kubernetes manifests, then select **Deploy**. A pull request (PR) will be generated against the repository that you selected, so don't navigate away from deployment page.

### Review and merge pull request

When the deployment succeeds, select **View pull request** to view the details of the generated pull request on your code repository.

- Review the changes under
**Files changed**and make any desired edits. - Select
**Merge pull request**to merge the changes into your code repository.

Merging the change runs the GitHub Actions workflow that builds your application into a container image, stores it in Azure Container Registry, and deploys it to the cluster.

### Check the deployed resources

After the pipeline is completed, you can review the created Kubernetes `Service`

in the Azure portal by selecting **Services and ingresses** under the **Kubernetes resources** section of the service menu.

Selecting the **External IP** should open up a new browser page with the running application.

## Delete resources

Once you're done with your cluster, use the following steps to delete it to avoid incurring Azure charges:

- In the Azure portal, navigate to
**Automated deployments** - Select
**...**on the pipeline of your choice. - Select
**Delete**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/monitor-aks -->

# Monitor Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS monitoring requires multiple levels of observability across platform metrics, Prometheus metrics, activity logs, resource logs, and container insights. AKS provides built-in monitoring capabilities and integrates with Azure Monitor, Container insights, managed service for Prometheus, and Azure Managed Grafana for comprehensive cluster health and performance monitoring.

Tip

You can use Azure Copilot to configure monitoring on your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#configure-monitoring-on-clusters).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

## AKS monitoring data: metrics, logs, integrations

AKS generates the same kinds of monitoring data as other Azure resources as described in [Monitor data from Azure resources](/en-us/azure/azure-monitor/essentials/monitor-azure-resource#monitoring-data-from-azure-resources). For detailed information on the metrics and logs created by AKS, see the [AKS monitoring data reference](monitor-aks-reference).

[Other Azure services and features](#integrations) collect other data and enable other analysis options as shown in the following diagram and table.

| Source | Description |
|---|---|
| Platform metrics |
|

[enable metric scraping](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana)for your cluster, the[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor collects[Prometheus metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)and stores them in an[Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-overview). Analyze these metrics using[prebuilt dashboards](/en-us/azure/azure-monitor/visualize/grafana-plugin#use-out-of-the-box-dashboards)in[Azure Managed Grafana](/en-us/azure/managed-grafana/overview)and with[Prometheus alerts](/en-us/azure/azure-monitor/alerts/prometheus-alerts).[activity log](monitor-aks-reference)automatically collects some data for AKS clusters at no cost. These log files track information like when a cluster is created or changes are made to a cluster configuration. To analyze activity log data with your other log data,[send activity log data to a Log Analytics workspace](/en-us/azure/azure-monitor/essentials/activity-log#send-to-log-analytics-workspace).[Create a diagnostic setting](#aks-control-plane-resource-logs)to[send the logs to a Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview). In the workspace, you can analyze the logs using queries and set up alerts based on log information.[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview)and in[Azure Monitor metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics). Analyze data like`stdout`

and `stderr`

streams using views and workbooks in Container insights or [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview)and the[metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics).[Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview), a feature of Azure Monitor, collects logs, metrics, and distributed traces. The telemetry is stored in a[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview)for analysis in the Azure portal. To enable Application Insights with code changes, see[Enable Azure Monitor OpenTelemetry](/en-us/azure/azure-monitor/app/opentelemetry-overview). To enable Application Insights without code changes, see[AKS autoinstrumentation](/en-us/azure/azure-monitor/app/kubernetes-codeless). For more information on instrumentation, learn about[data collection basics](/en-us/azure/azure-monitor/app/opentelemetry-overview).## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about resource types in AKS, see the [AKS monitoring data reference](monitor-aks-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of metrics you can collect for AKS, see the [AKS monitoring data reference](monitor-aks-reference#metrics).

Metrics play an important role in monitoring clusters, identifying issues, and optimizing performance in AKS clusters. Platform metrics are captured using the out-of-the-box metrics server installed in the `kube-system`

namespace, which periodically scrapes metrics from all AKS nodes served by kubelet. You should also enable managed service for Prometheus metrics to collect container metrics and Kubernetes object metrics, including object deployment state.

You can view the [list of default managed service for Prometheus metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default).

For more information, see [Collect managed service for Prometheus metrics from an AKS cluster](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana).

## Non-Azure Monitor based metrics

This service provides other metrics that aren't included in the Azure Monitor metrics database.

You can use the following Azure services and Azure Monitor features to monitor your AKS clusters. You enable these features when you create an AKS cluster.

In the Azure portal, use the **Integrations** tab, or use the Azure CLI, Terraform, or Azure Policy. In some cases, you can onboard your cluster to a monitoring service or feature after you create the cluster. Each service or feature might incur cost, so see the pricing information for each component before you enable it.

| Service or feature | Description |
|---|---|
|

[Azure Monitor Agent](/en-us/azure/azure-monitor/agents/agents-overview)to collect`stdout`

and `stderr`

logs and Kubernetes events from each node in your cluster. The feature supports a [variety of monitoring scenarios for AKS clusters](/en-us/azure/azure-monitor/containers/container-insights-overview). You can enable monitoring for an AKS cluster when it's created using the[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure Policy](/en-us/azure/azure-monitor/containers/container-insights-enable-aks-policy), the Azure portal, or Terraform. If you don't enable Container insights when you create your cluster, see[Enable Container insights for AKS cluster](/en-us/azure/azure-monitor/containers/container-insights-enable-aks)for other options to enable it.Container insights stores most of its data in a

[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview). You typically use the same Log Analytics workspace as the[resource logs](monitor-aks-reference#resource-logs)for your cluster. For guidance on how many workspaces you should use and where to locate them, see[Design a Log Analytics workspace architecture](/en-us/azure/azure-monitor/logs/workspace-design).[Managed service for Prometheus in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)[Prometheus](https://prometheus.io/)is a cloud-native metrics solution from the Cloud Native Computing Foundation. It's the most common tool to use to collect and analyze metric data from Kubernetes clusters. The managed service for Prometheus in Azure Monitor is a fully managed Prometheus-compatible monitoring solution. If you don't enable the managed service for Prometheus when you create your cluster, see[Collect Prometheus metrics from an AKS cluster](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana)for other options to enable it.The managed service for Prometheus in Azure Monitor stores its data in an

[Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-overview)that is[linked to a Grafana workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage#link-a-grafana-workspace). You can use Azure Managed Grafana to analyze the data.[Azure Managed Grafana](/en-us/azure/managed-grafana/overview)[Grafana](https://grafana.com/). Grafana is an open-source data visualization platform commonly used to present Prometheus data. Multiple predefined Grafana dashboards are available for monitoring Kubernetes and full-stack troubleshooting. If you don't enable Azure Managed Grafana when you create your cluster, see[Link a Grafana workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage#link-a-grafana-workspace). You can link it to your Azure Monitor workspace so that it can access Prometheus metrics from your cluster.### AKS control plane metrics monitoring (preview)


Prerequisites and scope: This preview feature is available for AKS clusters running Kubernetes 1.27 or later and requires the managed service for Prometheus to be enabled on your cluster. The feature currently supports Linux and Windows node pools but is not compatible with Virtual Machine Availability Sets (VMAS).

AKS also exposes metrics from critical control plane components like the API server, etcd, and the scheduler through the managed service for Prometheus in Azure Monitor. Currently, this feature is in preview. For more information, see [Monitor AKS control plane metrics](control-plane-metrics-monitor). A subset of control plane metrics for the API server and etcd are available free through [Azure Monitor platform metrics](monitor-aks-reference#metrics). These metrics are collected by default. You can use the metrics to create alerts.

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

For the available resource log categories, their associated Log Analytics tables, and log schemas for AKS, see the [AKS monitoring data reference](monitor-aks-reference#resource-logs).

### AKS control plane resource logs


Prerequisites: Requires a Log Analytics workspace in the same subscription as your AKS cluster. Resource logs incur ingestion and retention costs in the destination workspace. For cost optimization, use resource-specific mode and configure Basic logs tier for audit tables.

Control plane logs for AKS clusters are implemented as [resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) in Azure Monitor. Resource logs aren't collected and stored until you create a diagnostic setting to route them to at least one location. You typically send resource logs to a Log Analytics workspace, where most data for Container insights is stored.

To learn how to create a diagnostic setting using the Azure portal, the Azure CLI, or Azure PowerShell, see [Create diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings). When you create a diagnostic setting, you specify which categories of logs to collect. The categories for AKS are listed in the [AKS monitoring data reference](monitor-aks-reference#resource-logs).

Warning

You can incur substantial cost when you collect resource logs for AKS, particularly for *kube-audit* logs. Consider the following recommendations to reduce the amount of data collected:

- Disable
`kube-audit`

logging when not required. - Enable collection from
`kube-audit-admin`

, which excludes the`get`

and`list`

audit events. - Enable resource-specific logs as described in this article, and configure the
**AKSAudit**table as[Basic logs](/en-us/azure/azure-monitor/logs/logs-table-plans).

For more monitoring recommendations, see [Monitor AKS clusters using Azure services and cloud-native tools](/en-us/azure/azure-monitor/containers/monitor-kubernetes). For strategies to reduce your monitoring costs, see [Cost optimization and Azure Monitor](/en-us/azure/azure-monitor/best-practices-cost).

AKS supports either [Azure diagnostics mode](/en-us/azure/azure-monitor/essentials/resource-logs#azure-diagnostics-mode) or [resource-specific mode](/en-us/azure/azure-monitor/essentials/resource-logs#resource-specific) for resource logs. Azure diagnostics mode sends all data to the [AzureDiagnostics table](/en-us/azure/azure-monitor/reference/tables/azurediagnostics). Resource-specific mode specifies the tables in the Log Analytics workspace where the data is sent. It also sends data to [ AKSAudit](/en-us/azure/azure-monitor/reference/tables/aksaudit),

[, and](/en-us/azure/azure-monitor/reference/tables/aksauditadmin)

`AKSAuditAdmin`

[as shown in the table in](/en-us/azure/azure-monitor/reference/tables/akscontrolplane)

`AKSControlPlane`

[Resource logs](monitor-aks-reference#resource-logs).

We recommend that you use resource-specific mode for AKS for the following reasons:

- Data is easier to query because it's in individual tables that are dedicated to AKS.
- Resource-specific mode supports configuration as
[Basic logs](/en-us/azure/azure-monitor/logs/logs-table-plans)for significant cost savings.

For more information on the difference between collection modes, including how to change an existing setting, see [Select the collection mode](/en-us/azure/azure-monitor/essentials/resource-logs#select-the-collection-mode).

Note

You can configure diagnostic settings using the Azure CLI. This approach isn't guaranteed to be successful because it doesn't check for the cluster's provisioning state. After you change diagnostic settings, check to be sure that the cluster reflects the setting changes.

```
az monitor diagnostic-settings create --name AKS-Diagnostics --resource /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myresourcegroup/providers/Microsoft.ContainerService/managedClusters/my-cluster --logs '[{"category": "kube-audit","enabled": true}, {"category": "kube-audit-admin", "enabled": true}, {"category": "kube-apiserver", "enabled": true}, {"category": "kube-controller-manager", "enabled": true}, {"category": "kube-scheduler", "enabled": true}, {"category": "cluster-autoscaler", "enabled": true}, {"category": "cloud-controller-manager", "enabled": true}, {"category": "guard", "enabled": true}, {"category": "csi-azuredisk-controller", "enabled": true}, {"category": "csi-azurefile-controller", "enabled": true}, {"category": "csi-snapshot-controller", "enabled": true}]' --workspace /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/microsoft.operationalinsights/workspaces/myworkspace --export-to-resource-specific true
```


#### AKS resource log queries and examples


Query scope requirements: When you selectLogson an AKS cluster menu, Log Analytics opens with the query scope set to the current cluster. Log queries include data only from that resource. To run queries that include data from other clusters or Azure services, selectLogsfrom theAzure Monitormenu.

If the [diagnostic settings for your cluster](monitor-aks-reference#resource-logs) use Azure diagnostics mode, the resource logs for AKS are stored in the [AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics) table. Identify logs via the **Category** column. For a description of each category, see [AKS reference resource logs](monitor-aks-reference).

| Description | Mode | Log query |
|---|---|---|
| Count logs for each category | Azure diagnostics mode | `AzureDiagnostics` | `where ResourceType == "MANAGEDCLUSTERS"` | `summarize count() by Category` |
| All API server logs | Azure diagnostics mode | `AzureDiagnostics` | `where Category == "kube-apiserver"` |
| All kube-audit logs in a time range | Azure diagnostics mode | `let starttime = datetime("2023-02-23");` `let endtime = datetime("2023-02-24");` `AzureDiagnostics` | `where TimeGenerated between(starttime..endtime)` | `where Category == "kube-audit"` | `extend event = parse_json(log_s)` | `extend HttpMethod = tostring(event.verb)` | `extend User = tostring(event.user.username)` | `extend Apiserver = pod_s` | `extend SourceIP = tostring(event.sourceIPs[0])` | `project TimeGenerated, Category, HttpMethod, User, Apiserver, SourceIP, OperationName, event` |
| All audit logs | Resource-specific mode | `AKSAudit` |
All audit logs excluding the `get` and `list` audit events |
Resource-specific mode | `AKSAuditAdmin` |
| All API server logs | Resource-specific mode | `AKSControlPlane` | `where Category == "kube-apiserver"` |

To access a set of prebuilt queries in the Log Analytics workspace, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries#queries-interface), and select the **Kubernetes Services** resource type. For a list of common queries for Container insights, see [Container insights queries](/en-us/azure/azure-monitor/containers/container-insights-log-query).

#### AKS audit policy

AKS uses a Kubernetes [audit policy](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/) to control what events are logged and what data they contain. The policy defines rules that determine the audit level for different types of API requests based on users, resources, namespaces, and verbs. The following audit levels are used:

**None**: Events matching this rule aren't logged.**Metadata**: Log request metadata (requesting user, timestamp, resource, verb) but not request or response body.**Request**: Log event metadata and request body but not response body.**RequestResponse**: Log event metadata, request and response bodies.

The following table summarizes the key audit policy rules applied in AKS:

| Audit level | Description | Example events |
|---|---|---|
None |
High-volume, low-risk read operations | `aksService` user `get` /`list` operations, `kube-proxy` watch on endpoints/services, kubelet `get` on nodes/node status, health check URLs (`/healthz*` , `/version` , `/swagger*` ) |
Metadata |
System events, events resources (except creates/updates in `default` /`kube-system` ), secrets, configmaps, service accounts, token reviews |
Token reviews, secret/configmap access, large CRDs like `installations.operator.tigera.io` |
Request |
Node and pod status updates from kubelets/nodes, delete collection operations, CRD updates for volume snapshots, read operations (`get` /`list` /`watch` ) on core API groups, VPA changes |
Kubelet status updates, namespace deletions, VPA checkpoint updates |
RequestResponse |
CoreDNS custom configmap updates, Fleet API operations, Karpenter resource changes, all other write operations on core API groups | CoreDNS configuration changes, Fleet member cluster operations, Karpenter node pool changes |

The complete audit policy used in AKS is available for review in the following collapsible section.

## View the complete AKS audit policy

```
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
# audit level 'None' for high volume and low risk events
- level: None
users: ["aksService"]
verbs: ["get", "list"]
# audit level 'None' for low-risk requests
- level: None
users: ["system:kube-proxy"]
verbs: ["watch"]
resources:
- group: ""
resources: ["endpoints", "services", "services/status"]
# audit level 'None' for low-risk requests
- level: None
users: ["kubelet"] # legacy kubelet identity
verbs: ["get"]
resources:
- group: ""
resources: ["nodes", "nodes/status"]
# audit level 'None' for low-risk requests
- level: None
userGroups: ["system:nodes"]
verbs: ["get"]
resources:
- group: ""
resources: ["nodes", "nodes/status"]
# audit level 'None' for low-risk requests
- level: None
users:
- aksService # the default user/cert used by aks in master node
- system:serviceaccount:kube-system:endpoint-controller
verbs: ["get", "update"]
namespaces: ["kube-system"]
resources:
- group: ""
resources: ["endpoints"]
# audit level 'None' for low-risk requests
- level: None
users: ["system:apiserver"]
verbs: ["get"]
resources:
- group: ""
resources: ["namespaces", "namespaces/status", "namespaces/finalize"]
# audit level 'None' for low-risk requests
- level: None
users:
- aksService # the default user/cert used by aks in master node
verbs: ["get", "list"]
resources:
- group: "metrics.k8s.io"
# Don't log these read-only URLs.
- level: None
nonResourceURLs:
- /healthz*
- /version
- /swagger*
# monitor metadata for system events which are being logged by eventlogger component
- level: Metadata
verbs: ["create", "update", "patch"]
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
namespaces: ["default", "kube-system"]
# Monitoring of actions to detect security/performance relevant activities.
- level: Metadata
verbs: ["delete", "list"]
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
# Don't log other events requests.
- level: None
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
# node and pod status calls from nodes are high-volume and can be large, don't log responses for expected updates from nodes
- level: Request
users: ["client", "kubelet", "system:node-problem-detector", "system:serviceaccount:kube-system:node-problem-detector", "system:serviceaccount:kube-system:aci-connector-linux"]
verbs: ["update","patch"]
resources:
- group: ""
resources: ["nodes/status", "pods/status"]
omitStages:
- "RequestReceived"
# node and pod status calls from nodes are high-volume and can be large, don't log responses for expected updates from nodes
- level: Request
userGroups: ["system:nodes"]
verbs: ["update","patch"]
resources:
- group: ""
resources: ["nodes/status", "pods/status"]
omitStages:
- "RequestReceived"
# deletecollection calls can be large, don't log responses for expected namespace deletions
- level: Request
users: ["system:serviceaccount:kube-system:namespace-controller"]
verbs: ["deletecollection"]
omitStages:
- "RequestReceived"
# ignore response object that has big size
- level: Request
verbs: ["update","patch"]
resources:
- group: "apiextensions.k8s.io"
resources: ["customresourcedefinitions"]
resourceNames: ["volumesnapshotcontents.snapshot.storage.k8s.io", "volumesnapshots.snapshot.storage.k8s.io"]
omitStages:
- "RequestReceived"
# ignore request and response objects for large CRDs that will be filtered down anyway
- level: Metadata
resources:
- group: "apiextensions.k8s.io"
resources: ["customresourcedefinitions"]
resourceNames: ["installations.operator.tigera.io"]
omitStages:
- "RequestReceived"
# overriding the default behavior of coredns might have security threats for Kubernetes DNS in security perspective, set the level as RequestResponse
- level: RequestResponse
verbs: ["update","patch"]
resources:
- group: ""
resources: ["configmaps"]
resourceNames: ["coredns-custom"]
namespaces: ["kube-system"]
omitStages:
- "RequestReceived"
# Secrets, ConfigMaps, ServiceAccounts, TokenRequest and TokenReviews can contain sensitive & binary data,
# so only log at the Metadata level.
- level: Metadata
resources:
- group: ""
resources: ["secrets", "configmaps", "serviceaccounts", "serviceaccounts/token"]
- group: authentication.k8s.io
resources: ["tokenreviews"]
omitStages:
- "RequestReceived"
# Capture state of vertical pod autoscalers
- level: Request
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "autoscaling.k8s.io"
resources: ["verticalpodautoscalers", "verticalpodautoscalercheckpoints"]
omitStages:
- "RequestReceived"
# Capture create and delete of internal fleet resources
- level: RequestResponse
verbs: ["create", "delete"]
resources:
- group: "cluster.kubernetes-fleet.io"
resources: ["memberclusters", "internalmemberclusters"]
- group: "placement.kubernetes-fleet.io"
resources: ["works"]
- group: "networking.fleet.azure.com"
resources: ["internalserviceexports", "internalserviceimports"]
omitStages:
- "RequestReceived"
# Capture CUD of user facing Fleet API
- level: RequestResponse
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "placement.kubernetes-fleet.io"
resources: ["clusterstagedupdateruns", "clusterresourceplacements", "clusterresourceplacementevictions", "clusterresourceplacementdisruptionbudgets", "clusterstagedupdatestrategies", "clusterapprovalrequests", "clusterresourceoverrides", "resourceoverrides"]
- group: "networking.fleet.azure.com"
resources: ["serviceexports", "multiclusterservices", "trafficmanagerprofiles", "trafficmanagerbackends"]
omitStages:
- "RequestReceived"
# Capture CUD of user facing Karpenter resources
- level: RequestResponse
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "karpenter.azure.com"
resources: ["aksnodeclasses", "aksnodeclasses/status"]
- group: "karpenter.sh"
resources: ["nodepools", "nodepools/status", "nodeclaims", "nodeclaims/status"]
omitStages:
- "RequestReceived"
# Get responses can be large; don't log response
- level: Request
verbs: ["get", "list", "watch"]
resources:
- group: ""
- group: "admissionregistration.k8s.io"
- group: "apiextensions.k8s.io"
- group: "apiregistration.k8s.io"
- group: "apps"
- group: "authentication.k8s.io"
- group: "authorization.k8s.io"
- group: "autoscaling"
- group: "batch"
- group: "certificates.k8s.io"
- group: "extensions"
- group: "metrics.k8s.io"
- group: "networking.k8s.io"
- group: "policy"
- group: "rbac.authorization.k8s.io"
- group: "scheduling.k8s.io"
- group: "settings.k8s.io"
- group: "storage.k8s.io"
omitStages:
- "RequestReceived"
# Default level for known APIs
- level: RequestResponse
resources:
- group: ""
- group: "admissionregistration.k8s.io"
- group: "apiextensions.k8s.io"
- group: "apiregistration.k8s.io"
- group: "apps"
- group: "authentication.k8s.io"
- group: "authorization.k8s.io"
- group: "autoscaling"
- group: "batch"
- group: "certificates.k8s.io"
- group: "extensions"
- group: "metrics.k8s.io"
- group: "networking.k8s.io"
- group: "policy"
- group: "rbac.authorization.k8s.io"
- group: "scheduling.k8s.io"
- group: "settings.k8s.io"
- group: "storage.k8s.io"
omitStages:
- "RequestReceived"
# Default level for all other requests.
- level: Metadata
omitStages:
- "RequestReceived"
```


Note

The audit policy is managed by AKS and can't be customized. The policy is designed to balance security observability with performance and cost optimization by reducing log volume for high-frequency, low-risk operations.

### AKS data plane Container insights logs


Prerequisites and configuration requirements: Container insights requires a Log Analytics workspace for log storage and supports both managed identity and legacy authentication methods. For new clusters, managed identity authentication is recommended. Data collection can be customized using Azure Monitor Data Collection Rules (DCRs) to control costs and reduce ingestion volume.

Container insights collects various types of telemetry data from containers and AKS clusters to help you monitor, troubleshoot, and gain insights into your containerized applications running in your AKS clusters. For a list of tables and their detailed descriptions used by Container insights, see the [Azure Monitor table reference](/en-us/azure/azure-monitor/logs/manage-logs-tables). All the tables are available for [log queries](/en-us/azure/azure-monitor/logs/log-query-overview).

Use [cost optimization settings](/en-us/azure/azure-monitor/containers/container-insights-cost-config) to customize and control the metrics data collected through the Container insights agent. This feature supports the data collection settings for individual table selection, data collection intervals, and namespaces to exclude the data collection through [Azure Monitor Data Collection Rules (DCRs)](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview). These settings control the volume of ingestion and reduce the monitoring costs of Container insights. You can customize Container insights collected data in the Azure portal using the following options. Selecting any options other than **All (Default)** makes the Container insights experience unavailable.

| Grouping | Tables | Notes |
|---|---|---|
| All (Default) | All standard Container insights tables | Required to enable the default Container insights visualizations. |
| Performance | Perf, InsightsMetrics | N/A |
| Logs and events | ContainerLog or ContainerLogV2, KubeEvents, KubePodInventory | Recommended if you enabled managed service for Prometheus metrics. |
| Workloads, Deployments, and HPAs | InsightsMetrics, KubePodInventory, KubeEvents, ContainerInventory, ContainerNodeInventory, KubeNodeInventory, KubeServices | N/A |
| Persistent Volumes | InsightsMetrics, KubePVInventory | N/A |

The **Logs and events** grouping captures the logs from the **ContainerLog** or **ContainerLogV2**, **KubeEvents**, and **KubePodInventory** tables, but not the metrics. The recommended path to collect metrics is to enable the [managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview) from your AKS cluster and use [Azure Managed Grafana](/en-us/azure/managed-grafana/overview) for data visualization. For more information, see [Manage an Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage).

#### ContainerLogV2 schema


Compatibility and configuration requirements: ContainerLogV2 schema is recommended for new Container insights deployments using managed identity authentication via Azure Resource Manager (ARM) templates, Bicep, Terraform, Azure Policy, or the Azure portal. The schema is compatible with Basic logs tier for cost savings and doesn't affect analytics or alerts functionality. For more information about how to enable ContainerLogV2 through either the cluster's DCR or configmap, see[Enable the ContainerLogV2 schema].

Container insights in Azure Monitor provides a recommended schema for container logs, *ContainerLogV2*. The format includes the following fields for common queries to view data related to AKS and Azure Arc-enabled Kubernetes clusters:

**ContainerName****PodName****PodNamespace**

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## View AKS container logs, events, and pod metrics in real time


Prerequisites and setup requirements: Live data feature requires Container insights to be enabled on your cluster and uses direct Kubernetes API access. For private clusters, access requires a computer in the same private network as the cluster. Authentication follows the Kubernetes RBAC model and requires appropriate cluster permissions.

You can view AKS container logs, events, and pod metrics using the *live data* feature in Container insights and troubleshoot issues in real time with direct access to `kubectl logs -c`

, `kubectl get`

events, and `kubectl top pods`

.

Note

AKS uses [Kubernetes cluster-level logging architectures](https://kubernetes.io/docs/concepts/cluster-administration/logging/#cluster-level-logging-architectures). The container logs are located at `/var/log/containers`

on the node. To access a node, see [Connect to AKS cluster nodes](node-access).

To learn how to set up this feature, see [Configure live data in Container insights](/en-us/azure/azure-monitor/containers/container-insights-livedata-setup). The feature directly accesses the Kubernetes API. For more information about the authentication model, see the [Kubernetes API](https://kubernetes.io/docs/concepts/overview/kubernetes-api/).

### View AKS resource live logs


Private cluster network requirements: To access logs from a private cluster, you must use a computer that's in the same private network as the cluster.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Kubernetes resources**, select**Workloads**.For

**Deployment**,**Pod**,**Replica Set**,**Stateful Set**,**Job**, or**Cron Job**, select a value, and then select**Live Logs**.Select a resource log to view.

The following example shows the logs for a pod resource:


### View container live logs using Container insights


Authentication and data streaming: After successful authentication, if data can be retrieved, it begins streaming to theLive Logstab. Log data appears in a continuous stream. Alternative log access is available throughView Logs in Log Analyticsfor historical analysis.

You can view real-time log data as the container engine generates it on the **Cluster**, **Nodes**, **Controllers**, or **Containers** tab.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.On the

**Cluster**,**Nodes**,**Controllers**, or**Containers**tab, select a value.On the

**Overview**pane for the resource, select**Live Logs**.The following image shows the logs for a container resource:


### View container live events using Container insights


Event streaming and access: Real-time event data streams as the container engine generates it. Events include pod creation, deletion, scaling operations, and error conditions. Historical event data is accessible viaView Events in Log Analytics.

You can view real-time event data as the container engine generates it on the **Cluster**, **Nodes**, **Controllers**, or **Containers** tab.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.Select the

**Cluster**,**Nodes**,**Controllers**, or**Containers**tab, and then select an object.On the resource

**Overview**pane, select**Live Events**.After successful authentication, if data can be retrieved, it begins streaming to the

**Live Events**tab. The following image shows the events for a container resource:

### View pod live metrics using Container insights


Metrics scope and availability: Live metrics are available for pod resources on theNodesorControllerstabs. Metrics include CPU usage, memory consumption, network I/O, and filesystem statistics. Historical metrics are accessible throughView Events in Log Analytics.

You can view real-time metrics data as the container engine generates it on the **Nodes** or **Controllers** tab by selecting a pod resource.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.Select the

**Nodes**or**Controllers**tab, and then select a pod object.On the resource

**Overview**pane, select**Live Metrics**.After successful authentication, if data can be retrieved, it begins streaming to the

**Live Metrics**tab. The following image shows the metrics for a pod resource:## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see

[Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Monitor AKS clusters in the Azure portal

The **Monitoring** tab on the **Overview** pane for your AKS cluster resource offers a quick way to start viewing monitoring data in the Azure portal. This tab includes graphs with common metrics for the cluster separated by node pool. You can select any of these graphs to further analyze the data in the [metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).

The **Monitoring** tab also includes links to the [Azure managed service for Prometheus](#integrations) and [Container insights](#integrations) for the cluster. You can enable these tools on the **Monitoring** tab. You might also see a banner at the top of the pane that recommends other features to improve monitoring for your cluster.

Tip

To access monitoring features for all AKS clusters in your subscription, on the Azure portal home page, select **Azure Monitor**.

## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

### Recommended alert rules

For some Azure services, you can [enable recommended out-of-the-box alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

The system compiles a list of recommended alert rules based on:

- The resource provider's knowledge of important signals and thresholds for monitoring the resource.
- Data that tells what customers commonly alert on for this resource.

Note

Recommended alert rules are available for:

- Virtual machines
- Azure Kubernetes Service (AKS) resources
- Log Analytics workspaces

### Configure Prometheus metrics-based alerts


Download and configuration requirements: Alert rules are available as downloadable ARM templates or Bicep files. Before configuring alerts, ensure the managed service for Prometheus is enabled on your cluster and an Azure Monitor workspace is properly linked to your AKS cluster.

When you [enable collection of the managed service for Prometheus metrics](#integrations) for your cluster, you can download a collection of [recommended managed service for Prometheus alert rules](/en-us/azure/azure-monitor/containers/container-insights-metric-alerts#enable-prometheus-alert-rules).

The download includes the following rules:

| Level | Alerts |
|---|---|
| Cluster level | `KubeCPUQuotaOvercommit` `KubeMemoryQuotaOvercommit` `KubeContainerOOMKilledCount` `KubeClientErrors` `KubePersistentVolumeFillingUp` `KubePersistentVolumeInodesFillingUp` `KubePersistentVolumeErrors` `KubeContainerWaiting` `KubeDaemonSetNotScheduled` `KubeDaemonSetMisScheduled` `KubeQuotaAlmostFull` |
| Node level | `KubeNodeUnreachable` `KubeNodeReadinessFlapping` |
| Pod level | `KubePVUsageHigh` `KubeDeploymentReplicasMismatch` `KubeStatefulSetReplicasMismatch` `KubeHpaReplicasMismatch` `KubeHpaMaxedOut` `KubePodCrashLooping` `KubeJobStale` `KubePodContainerRestart` `KubePodReadyStateLow` `KubePodFailedState` `KubePodNotReadyByController` `KubeStatefulSetGenerationMismatch` `KubeJobFailed` `KubeContainerAverageCPUHigh` `KubeContainerAverageMemoryHigh` `KubeletPodStartUpLatencyHigh` |

For more information, see [Create log alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts) and [Query logs from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query).

[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-unified-log) can measure two types of information to help you monitor diverse scenarios:

[Result count](/en-us/azure/azure-monitor/alerts/alerts-unified-log#result-count): Counts the number of rows returned by the query. Use this information to work with events like Windows event logs, syslog events, and application exceptions.[Calculation of a value](/en-us/azure/azure-monitor/alerts/alerts-unified-log#calculation-of-a-value): Makes a calculation based on a numeric column. Use this information to include diverse resources. An example is CPU percentage.

Most log queries compare a `DateTime`

value to the present time using the `now`

operator and going back one hour. To learn how to build log-based alerts, see [Create log alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).

### AKS alert rules

The following table lists some suggested alert rules for AKS. These alerts are only examples. You can set alerts for any metric, log entry, or activity log entry listed in the [AKS monitoring data reference](monitor-aks-reference).

| Condition | Description |
|---|---|
CPU Usage Percentage > 95 |
Alerts when the average CPU usage across all nodes exceeds the threshold. |
Memory Working Set Percentage > 100 |
Alerts when the average working set across all nodes exceeds the threshold. |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

## AKS node network metrics monitoring


Version and enablement requirements: In Kubernetes version 1.29 and later, node network metrics are enabled by default for all clusters that have Azure Monitor enabled. For earlier Kubernetes versions, you must manually enable network monitoring through cluster configuration. This feature requires Azure Monitor or Container insights to be configured on your cluster.

Node network metrics are crucial for maintaining a healthy and performant Kubernetes cluster. By collecting and analyzing data about network traffic, you can gain valuable insights about your cluster's operation and identify potential issues before they lead to outages or performance loss.

The following node network metrics are enabled by default and are aggregated per node. All metrics include the labels cluster and instance (node name). You can easily view these metrics using the Managed Grafana dashboard under **Azure Managed Prometheus** > **Kubernetes** > **Networking** > **Clusters**.

### AKS node network metrics by data plane type

All metrics include these labels:

`cluster`

`instance`

(node name)


OS support and limitations: For Cilium data plane scenarios, the Container Network Observability feature provides metrics only for Linux node pools. Currently, Windows isn't supported for Container Network Observability metrics. Ensure your cluster has Linux node pools for full Cilium metrics availability.

For Cilium data plane scenarios, the Container Network Observability feature provides metrics only for Linux. Currently, Windows isn't supported for Container Network Observability metrics.

Cilium exposes several metrics that Container Network Observability uses:

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
`cilium_forward_count_total` |
Total forwarded packet count | `direction` |
Supported ✅ | Unsupported ❌ |
`cilium_forward_bytes_total` |
Total forwarded byte count | `direction` |
Supported ✅ | Unsupported ❌ |
`cilium_drop_count_total` |
Total dropped packet count | `direction` , `reason` |
Supported ✅ | Unsupported ❌ |
`cilium_drop_bytes_total` |
Total dropped byte count | `direction` , `reason` |
Supported ✅ | Unsupported ❌ |

### Disable AKS node network metrics collection

You can disable network metrics collection on specific nodes by adding the label `networking.azure.com/node-network-metrics=disabled`

to those nodes.

Note

Retina has an `operator: "Exists"`

`effect: NoSchedule`

toleration, so it bypasses `NoSchedule`

taints. Therefore, labels are used instead of taints to control scheduling.

If the cluster is `autoprovisioning/autoscaling`

nodes, you need to manually enable the flag on each node.

Important

This feature isn't applicable if Advanced Container Networking Services (ACNS) is enabled on your cluster.

To disable metrics collection on a node:

```
kubectl label node <node-name> networking.azure.com/node-network-metrics=disabled
```


For detailed pod-level and DNS metrics, see [Advanced Container Networking Services](advanced-container-networking-services-overview).

## Related content

- For a reference of the metrics, logs, and other important values created for AKS, see the
[AKS monitoring data reference](monitor-aks-reference). - For general details on monitoring Azure resources, see
[Monitor Azure resources using Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource). - For detailed monitoring of the complete Kubernetes stack, see
[Monitor Kubernetes clusters using Azure services and cloud native tools](/en-us/azure/azure-monitor/containers/monitor-kubernetes). - For collecting metrics data from Kubernetes clusters, see
[Managed service for Prometheus in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview). - For collecting logs in Kubernetes clusters, see
[Azure Monitor features for Kubernetes monitoring](/en-us/azure/azure-monitor/containers/container-insights-overview). - For data visualization, see
[Azure Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview)and[Monitor your Azure services in Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/monitor-control-plane-metrics -->

# Monitor Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS monitoring requires multiple levels of observability across platform metrics, Prometheus metrics, activity logs, resource logs, and container insights. AKS provides built-in monitoring capabilities and integrates with Azure Monitor, Container insights, managed service for Prometheus, and Azure Managed Grafana for comprehensive cluster health and performance monitoring.

Tip

You can use Azure Copilot to configure monitoring on your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#configure-monitoring-on-clusters).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

## AKS monitoring data: metrics, logs, integrations

AKS generates the same kinds of monitoring data as other Azure resources as described in [Monitor data from Azure resources](/en-us/azure/azure-monitor/essentials/monitor-azure-resource#monitoring-data-from-azure-resources). For detailed information on the metrics and logs created by AKS, see the [AKS monitoring data reference](monitor-aks-reference).

[Other Azure services and features](#integrations) collect other data and enable other analysis options as shown in the following diagram and table.

| Source | Description |
|---|---|
| Platform metrics |
|

[enable metric scraping](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana)for your cluster, the[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor collects[Prometheus metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)and stores them in an[Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-overview). Analyze these metrics using[prebuilt dashboards](/en-us/azure/azure-monitor/visualize/grafana-plugin#use-out-of-the-box-dashboards)in[Azure Managed Grafana](/en-us/azure/managed-grafana/overview)and with[Prometheus alerts](/en-us/azure/azure-monitor/alerts/prometheus-alerts).[activity log](monitor-aks-reference)automatically collects some data for AKS clusters at no cost. These log files track information like when a cluster is created or changes are made to a cluster configuration. To analyze activity log data with your other log data,[send activity log data to a Log Analytics workspace](/en-us/azure/azure-monitor/essentials/activity-log#send-to-log-analytics-workspace).[Create a diagnostic setting](#aks-control-plane-resource-logs)to[send the logs to a Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview). In the workspace, you can analyze the logs using queries and set up alerts based on log information.[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview)and in[Azure Monitor metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics). Analyze data like`stdout`

and `stderr`

streams using views and workbooks in Container insights or [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview)and the[metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics).[Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview), a feature of Azure Monitor, collects logs, metrics, and distributed traces. The telemetry is stored in a[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview)for analysis in the Azure portal. To enable Application Insights with code changes, see[Enable Azure Monitor OpenTelemetry](/en-us/azure/azure-monitor/app/opentelemetry-overview). To enable Application Insights without code changes, see[AKS autoinstrumentation](/en-us/azure/azure-monitor/app/kubernetes-codeless). For more information on instrumentation, learn about[data collection basics](/en-us/azure/azure-monitor/app/opentelemetry-overview).## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about resource types in AKS, see the [AKS monitoring data reference](monitor-aks-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of metrics you can collect for AKS, see the [AKS monitoring data reference](monitor-aks-reference#metrics).

Metrics play an important role in monitoring clusters, identifying issues, and optimizing performance in AKS clusters. Platform metrics are captured using the out-of-the-box metrics server installed in the `kube-system`

namespace, which periodically scrapes metrics from all AKS nodes served by kubelet. You should also enable managed service for Prometheus metrics to collect container metrics and Kubernetes object metrics, including object deployment state.

You can view the [list of default managed service for Prometheus metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default).

For more information, see [Collect managed service for Prometheus metrics from an AKS cluster](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana).

## Non-Azure Monitor based metrics

This service provides other metrics that aren't included in the Azure Monitor metrics database.

You can use the following Azure services and Azure Monitor features to monitor your AKS clusters. You enable these features when you create an AKS cluster.

In the Azure portal, use the **Integrations** tab, or use the Azure CLI, Terraform, or Azure Policy. In some cases, you can onboard your cluster to a monitoring service or feature after you create the cluster. Each service or feature might incur cost, so see the pricing information for each component before you enable it.

| Service or feature | Description |
|---|---|
|

[Azure Monitor Agent](/en-us/azure/azure-monitor/agents/agents-overview)to collect`stdout`

and `stderr`

logs and Kubernetes events from each node in your cluster. The feature supports a [variety of monitoring scenarios for AKS clusters](/en-us/azure/azure-monitor/containers/container-insights-overview). You can enable monitoring for an AKS cluster when it's created using the[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure Policy](/en-us/azure/azure-monitor/containers/container-insights-enable-aks-policy), the Azure portal, or Terraform. If you don't enable Container insights when you create your cluster, see[Enable Container insights for AKS cluster](/en-us/azure/azure-monitor/containers/container-insights-enable-aks)for other options to enable it.Container insights stores most of its data in a

[Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-workspace-overview). You typically use the same Log Analytics workspace as the[resource logs](monitor-aks-reference#resource-logs)for your cluster. For guidance on how many workspaces you should use and where to locate them, see[Design a Log Analytics workspace architecture](/en-us/azure/azure-monitor/logs/workspace-design).[Managed service for Prometheus in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)[Prometheus](https://prometheus.io/)is a cloud-native metrics solution from the Cloud Native Computing Foundation. It's the most common tool to use to collect and analyze metric data from Kubernetes clusters. The managed service for Prometheus in Azure Monitor is a fully managed Prometheus-compatible monitoring solution. If you don't enable the managed service for Prometheus when you create your cluster, see[Collect Prometheus metrics from an AKS cluster](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana)for other options to enable it.The managed service for Prometheus in Azure Monitor stores its data in an

[Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-overview)that is[linked to a Grafana workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage#link-a-grafana-workspace). You can use Azure Managed Grafana to analyze the data.[Azure Managed Grafana](/en-us/azure/managed-grafana/overview)[Grafana](https://grafana.com/). Grafana is an open-source data visualization platform commonly used to present Prometheus data. Multiple predefined Grafana dashboards are available for monitoring Kubernetes and full-stack troubleshooting. If you don't enable Azure Managed Grafana when you create your cluster, see[Link a Grafana workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage#link-a-grafana-workspace). You can link it to your Azure Monitor workspace so that it can access Prometheus metrics from your cluster.### AKS control plane metrics monitoring (preview)


Prerequisites and scope: This preview feature is available for AKS clusters running Kubernetes 1.27 or later and requires the managed service for Prometheus to be enabled on your cluster. The feature currently supports Linux and Windows node pools but is not compatible with Virtual Machine Availability Sets (VMAS).

AKS also exposes metrics from critical control plane components like the API server, etcd, and the scheduler through the managed service for Prometheus in Azure Monitor. Currently, this feature is in preview. For more information, see [Monitor AKS control plane metrics](control-plane-metrics-monitor). A subset of control plane metrics for the API server and etcd are available free through [Azure Monitor platform metrics](monitor-aks-reference#metrics). These metrics are collected by default. You can use the metrics to create alerts.

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

For the available resource log categories, their associated Log Analytics tables, and log schemas for AKS, see the [AKS monitoring data reference](monitor-aks-reference#resource-logs).

### AKS control plane resource logs


Prerequisites: Requires a Log Analytics workspace in the same subscription as your AKS cluster. Resource logs incur ingestion and retention costs in the destination workspace. For cost optimization, use resource-specific mode and configure Basic logs tier for audit tables.

Control plane logs for AKS clusters are implemented as [resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) in Azure Monitor. Resource logs aren't collected and stored until you create a diagnostic setting to route them to at least one location. You typically send resource logs to a Log Analytics workspace, where most data for Container insights is stored.

To learn how to create a diagnostic setting using the Azure portal, the Azure CLI, or Azure PowerShell, see [Create diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings). When you create a diagnostic setting, you specify which categories of logs to collect. The categories for AKS are listed in the [AKS monitoring data reference](monitor-aks-reference#resource-logs).

Warning

You can incur substantial cost when you collect resource logs for AKS, particularly for *kube-audit* logs. Consider the following recommendations to reduce the amount of data collected:

- Disable
`kube-audit`

logging when not required. - Enable collection from
`kube-audit-admin`

, which excludes the`get`

and`list`

audit events. - Enable resource-specific logs as described in this article, and configure the
**AKSAudit**table as[Basic logs](/en-us/azure/azure-monitor/logs/logs-table-plans).

For more monitoring recommendations, see [Monitor AKS clusters using Azure services and cloud-native tools](/en-us/azure/azure-monitor/containers/monitor-kubernetes). For strategies to reduce your monitoring costs, see [Cost optimization and Azure Monitor](/en-us/azure/azure-monitor/best-practices-cost).

AKS supports either [Azure diagnostics mode](/en-us/azure/azure-monitor/essentials/resource-logs#azure-diagnostics-mode) or [resource-specific mode](/en-us/azure/azure-monitor/essentials/resource-logs#resource-specific) for resource logs. Azure diagnostics mode sends all data to the [AzureDiagnostics table](/en-us/azure/azure-monitor/reference/tables/azurediagnostics). Resource-specific mode specifies the tables in the Log Analytics workspace where the data is sent. It also sends data to [ AKSAudit](/en-us/azure/azure-monitor/reference/tables/aksaudit),

[, and](/en-us/azure/azure-monitor/reference/tables/aksauditadmin)

`AKSAuditAdmin`

[as shown in the table in](/en-us/azure/azure-monitor/reference/tables/akscontrolplane)

`AKSControlPlane`

[Resource logs](monitor-aks-reference#resource-logs).

We recommend that you use resource-specific mode for AKS for the following reasons:

- Data is easier to query because it's in individual tables that are dedicated to AKS.
- Resource-specific mode supports configuration as
[Basic logs](/en-us/azure/azure-monitor/logs/logs-table-plans)for significant cost savings.

For more information on the difference between collection modes, including how to change an existing setting, see [Select the collection mode](/en-us/azure/azure-monitor/essentials/resource-logs#select-the-collection-mode).

Note

You can configure diagnostic settings using the Azure CLI. This approach isn't guaranteed to be successful because it doesn't check for the cluster's provisioning state. After you change diagnostic settings, check to be sure that the cluster reflects the setting changes.

```
az monitor diagnostic-settings create --name AKS-Diagnostics --resource /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myresourcegroup/providers/Microsoft.ContainerService/managedClusters/my-cluster --logs '[{"category": "kube-audit","enabled": true}, {"category": "kube-audit-admin", "enabled": true}, {"category": "kube-apiserver", "enabled": true}, {"category": "kube-controller-manager", "enabled": true}, {"category": "kube-scheduler", "enabled": true}, {"category": "cluster-autoscaler", "enabled": true}, {"category": "cloud-controller-manager", "enabled": true}, {"category": "guard", "enabled": true}, {"category": "csi-azuredisk-controller", "enabled": true}, {"category": "csi-azurefile-controller", "enabled": true}, {"category": "csi-snapshot-controller", "enabled": true}]' --workspace /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/microsoft.operationalinsights/workspaces/myworkspace --export-to-resource-specific true
```


#### AKS resource log queries and examples


Query scope requirements: When you selectLogson an AKS cluster menu, Log Analytics opens with the query scope set to the current cluster. Log queries include data only from that resource. To run queries that include data from other clusters or Azure services, selectLogsfrom theAzure Monitormenu.

If the [diagnostic settings for your cluster](monitor-aks-reference#resource-logs) use Azure diagnostics mode, the resource logs for AKS are stored in the [AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics) table. Identify logs via the **Category** column. For a description of each category, see [AKS reference resource logs](monitor-aks-reference).

| Description | Mode | Log query |
|---|---|---|
| Count logs for each category | Azure diagnostics mode | `AzureDiagnostics` | `where ResourceType == "MANAGEDCLUSTERS"` | `summarize count() by Category` |
| All API server logs | Azure diagnostics mode | `AzureDiagnostics` | `where Category == "kube-apiserver"` |
| All kube-audit logs in a time range | Azure diagnostics mode | `let starttime = datetime("2023-02-23");` `let endtime = datetime("2023-02-24");` `AzureDiagnostics` | `where TimeGenerated between(starttime..endtime)` | `where Category == "kube-audit"` | `extend event = parse_json(log_s)` | `extend HttpMethod = tostring(event.verb)` | `extend User = tostring(event.user.username)` | `extend Apiserver = pod_s` | `extend SourceIP = tostring(event.sourceIPs[0])` | `project TimeGenerated, Category, HttpMethod, User, Apiserver, SourceIP, OperationName, event` |
| All audit logs | Resource-specific mode | `AKSAudit` |
All audit logs excluding the `get` and `list` audit events |
Resource-specific mode | `AKSAuditAdmin` |
| All API server logs | Resource-specific mode | `AKSControlPlane` | `where Category == "kube-apiserver"` |

To access a set of prebuilt queries in the Log Analytics workspace, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries#queries-interface), and select the **Kubernetes Services** resource type. For a list of common queries for Container insights, see [Container insights queries](/en-us/azure/azure-monitor/containers/container-insights-log-query).

#### AKS audit policy

AKS uses a Kubernetes [audit policy](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/) to control what events are logged and what data they contain. The policy defines rules that determine the audit level for different types of API requests based on users, resources, namespaces, and verbs. The following audit levels are used:

**None**: Events matching this rule aren't logged.**Metadata**: Log request metadata (requesting user, timestamp, resource, verb) but not request or response body.**Request**: Log event metadata and request body but not response body.**RequestResponse**: Log event metadata, request and response bodies.

The following table summarizes the key audit policy rules applied in AKS:

| Audit level | Description | Example events |
|---|---|---|
None |
High-volume, low-risk read operations | `aksService` user `get` /`list` operations, `kube-proxy` watch on endpoints/services, kubelet `get` on nodes/node status, health check URLs (`/healthz*` , `/version` , `/swagger*` ) |
Metadata |
System events, events resources (except creates/updates in `default` /`kube-system` ), secrets, configmaps, service accounts, token reviews |
Token reviews, secret/configmap access, large CRDs like `installations.operator.tigera.io` |
Request |
Node and pod status updates from kubelets/nodes, delete collection operations, CRD updates for volume snapshots, read operations (`get` /`list` /`watch` ) on core API groups, VPA changes |
Kubelet status updates, namespace deletions, VPA checkpoint updates |
RequestResponse |
CoreDNS custom configmap updates, Fleet API operations, Karpenter resource changes, all other write operations on core API groups | CoreDNS configuration changes, Fleet member cluster operations, Karpenter node pool changes |

The complete audit policy used in AKS is available for review in the following collapsible section.

## View the complete AKS audit policy

```
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
# audit level 'None' for high volume and low risk events
- level: None
users: ["aksService"]
verbs: ["get", "list"]
# audit level 'None' for low-risk requests
- level: None
users: ["system:kube-proxy"]
verbs: ["watch"]
resources:
- group: ""
resources: ["endpoints", "services", "services/status"]
# audit level 'None' for low-risk requests
- level: None
users: ["kubelet"] # legacy kubelet identity
verbs: ["get"]
resources:
- group: ""
resources: ["nodes", "nodes/status"]
# audit level 'None' for low-risk requests
- level: None
userGroups: ["system:nodes"]
verbs: ["get"]
resources:
- group: ""
resources: ["nodes", "nodes/status"]
# audit level 'None' for low-risk requests
- level: None
users:
- aksService # the default user/cert used by aks in master node
- system:serviceaccount:kube-system:endpoint-controller
verbs: ["get", "update"]
namespaces: ["kube-system"]
resources:
- group: ""
resources: ["endpoints"]
# audit level 'None' for low-risk requests
- level: None
users: ["system:apiserver"]
verbs: ["get"]
resources:
- group: ""
resources: ["namespaces", "namespaces/status", "namespaces/finalize"]
# audit level 'None' for low-risk requests
- level: None
users:
- aksService # the default user/cert used by aks in master node
verbs: ["get", "list"]
resources:
- group: "metrics.k8s.io"
# Don't log these read-only URLs.
- level: None
nonResourceURLs:
- /healthz*
- /version
- /swagger*
# monitor metadata for system events which are being logged by eventlogger component
- level: Metadata
verbs: ["create", "update", "patch"]
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
namespaces: ["default", "kube-system"]
# Monitoring of actions to detect security/performance relevant activities.
- level: Metadata
verbs: ["delete", "list"]
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
# Don't log other events requests.
- level: None
resources:
- group: ""
resources: ["events"]
- group: "events.k8s.io"
resources: ["events"]
# node and pod status calls from nodes are high-volume and can be large, don't log responses for expected updates from nodes
- level: Request
users: ["client", "kubelet", "system:node-problem-detector", "system:serviceaccount:kube-system:node-problem-detector", "system:serviceaccount:kube-system:aci-connector-linux"]
verbs: ["update","patch"]
resources:
- group: ""
resources: ["nodes/status", "pods/status"]
omitStages:
- "RequestReceived"
# node and pod status calls from nodes are high-volume and can be large, don't log responses for expected updates from nodes
- level: Request
userGroups: ["system:nodes"]
verbs: ["update","patch"]
resources:
- group: ""
resources: ["nodes/status", "pods/status"]
omitStages:
- "RequestReceived"
# deletecollection calls can be large, don't log responses for expected namespace deletions
- level: Request
users: ["system:serviceaccount:kube-system:namespace-controller"]
verbs: ["deletecollection"]
omitStages:
- "RequestReceived"
# ignore response object that has big size
- level: Request
verbs: ["update","patch"]
resources:
- group: "apiextensions.k8s.io"
resources: ["customresourcedefinitions"]
resourceNames: ["volumesnapshotcontents.snapshot.storage.k8s.io", "volumesnapshots.snapshot.storage.k8s.io"]
omitStages:
- "RequestReceived"
# ignore request and response objects for large CRDs that will be filtered down anyway
- level: Metadata
resources:
- group: "apiextensions.k8s.io"
resources: ["customresourcedefinitions"]
resourceNames: ["installations.operator.tigera.io"]
omitStages:
- "RequestReceived"
# overriding the default behavior of coredns might have security threats for Kubernetes DNS in security perspective, set the level as RequestResponse
- level: RequestResponse
verbs: ["update","patch"]
resources:
- group: ""
resources: ["configmaps"]
resourceNames: ["coredns-custom"]
namespaces: ["kube-system"]
omitStages:
- "RequestReceived"
# Secrets, ConfigMaps, ServiceAccounts, TokenRequest and TokenReviews can contain sensitive & binary data,
# so only log at the Metadata level.
- level: Metadata
resources:
- group: ""
resources: ["secrets", "configmaps", "serviceaccounts", "serviceaccounts/token"]
- group: authentication.k8s.io
resources: ["tokenreviews"]
omitStages:
- "RequestReceived"
# Capture state of vertical pod autoscalers
- level: Request
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "autoscaling.k8s.io"
resources: ["verticalpodautoscalers", "verticalpodautoscalercheckpoints"]
omitStages:
- "RequestReceived"
# Capture create and delete of internal fleet resources
- level: RequestResponse
verbs: ["create", "delete"]
resources:
- group: "cluster.kubernetes-fleet.io"
resources: ["memberclusters", "internalmemberclusters"]
- group: "placement.kubernetes-fleet.io"
resources: ["works"]
- group: "networking.fleet.azure.com"
resources: ["internalserviceexports", "internalserviceimports"]
omitStages:
- "RequestReceived"
# Capture CUD of user facing Fleet API
- level: RequestResponse
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "placement.kubernetes-fleet.io"
resources: ["clusterstagedupdateruns", "clusterresourceplacements", "clusterresourceplacementevictions", "clusterresourceplacementdisruptionbudgets", "clusterstagedupdatestrategies", "clusterapprovalrequests", "clusterresourceoverrides", "resourceoverrides"]
- group: "networking.fleet.azure.com"
resources: ["serviceexports", "multiclusterservices", "trafficmanagerprofiles", "trafficmanagerbackends"]
omitStages:
- "RequestReceived"
# Capture CUD of user facing Karpenter resources
- level: RequestResponse
verbs: ["create", "update", "patch", "delete"]
resources:
- group: "karpenter.azure.com"
resources: ["aksnodeclasses", "aksnodeclasses/status"]
- group: "karpenter.sh"
resources: ["nodepools", "nodepools/status", "nodeclaims", "nodeclaims/status"]
omitStages:
- "RequestReceived"
# Get responses can be large; don't log response
- level: Request
verbs: ["get", "list", "watch"]
resources:
- group: ""
- group: "admissionregistration.k8s.io"
- group: "apiextensions.k8s.io"
- group: "apiregistration.k8s.io"
- group: "apps"
- group: "authentication.k8s.io"
- group: "authorization.k8s.io"
- group: "autoscaling"
- group: "batch"
- group: "certificates.k8s.io"
- group: "extensions"
- group: "metrics.k8s.io"
- group: "networking.k8s.io"
- group: "policy"
- group: "rbac.authorization.k8s.io"
- group: "scheduling.k8s.io"
- group: "settings.k8s.io"
- group: "storage.k8s.io"
omitStages:
- "RequestReceived"
# Default level for known APIs
- level: RequestResponse
resources:
- group: ""
- group: "admissionregistration.k8s.io"
- group: "apiextensions.k8s.io"
- group: "apiregistration.k8s.io"
- group: "apps"
- group: "authentication.k8s.io"
- group: "authorization.k8s.io"
- group: "autoscaling"
- group: "batch"
- group: "certificates.k8s.io"
- group: "extensions"
- group: "metrics.k8s.io"
- group: "networking.k8s.io"
- group: "policy"
- group: "rbac.authorization.k8s.io"
- group: "scheduling.k8s.io"
- group: "settings.k8s.io"
- group: "storage.k8s.io"
omitStages:
- "RequestReceived"
# Default level for all other requests.
- level: Metadata
omitStages:
- "RequestReceived"
```


Note

The audit policy is managed by AKS and can't be customized. The policy is designed to balance security observability with performance and cost optimization by reducing log volume for high-frequency, low-risk operations.

### AKS data plane Container insights logs


Prerequisites and configuration requirements: Container insights requires a Log Analytics workspace for log storage and supports both managed identity and legacy authentication methods. For new clusters, managed identity authentication is recommended. Data collection can be customized using Azure Monitor Data Collection Rules (DCRs) to control costs and reduce ingestion volume.

Container insights collects various types of telemetry data from containers and AKS clusters to help you monitor, troubleshoot, and gain insights into your containerized applications running in your AKS clusters. For a list of tables and their detailed descriptions used by Container insights, see the [Azure Monitor table reference](/en-us/azure/azure-monitor/logs/manage-logs-tables). All the tables are available for [log queries](/en-us/azure/azure-monitor/logs/log-query-overview).

Use [cost optimization settings](/en-us/azure/azure-monitor/containers/container-insights-cost-config) to customize and control the metrics data collected through the Container insights agent. This feature supports the data collection settings for individual table selection, data collection intervals, and namespaces to exclude the data collection through [Azure Monitor Data Collection Rules (DCRs)](/en-us/azure/azure-monitor/essentials/data-collection-rule-overview). These settings control the volume of ingestion and reduce the monitoring costs of Container insights. You can customize Container insights collected data in the Azure portal using the following options. Selecting any options other than **All (Default)** makes the Container insights experience unavailable.

| Grouping | Tables | Notes |
|---|---|---|
| All (Default) | All standard Container insights tables | Required to enable the default Container insights visualizations. |
| Performance | Perf, InsightsMetrics | N/A |
| Logs and events | ContainerLog or ContainerLogV2, KubeEvents, KubePodInventory | Recommended if you enabled managed service for Prometheus metrics. |
| Workloads, Deployments, and HPAs | InsightsMetrics, KubePodInventory, KubeEvents, ContainerInventory, ContainerNodeInventory, KubeNodeInventory, KubeServices | N/A |
| Persistent Volumes | InsightsMetrics, KubePVInventory | N/A |

The **Logs and events** grouping captures the logs from the **ContainerLog** or **ContainerLogV2**, **KubeEvents**, and **KubePodInventory** tables, but not the metrics. The recommended path to collect metrics is to enable the [managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview) from your AKS cluster and use [Azure Managed Grafana](/en-us/azure/managed-grafana/overview) for data visualization. For more information, see [Manage an Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage).

#### ContainerLogV2 schema


Compatibility and configuration requirements: ContainerLogV2 schema is recommended for new Container insights deployments using managed identity authentication via Azure Resource Manager (ARM) templates, Bicep, Terraform, Azure Policy, or the Azure portal. The schema is compatible with Basic logs tier for cost savings and doesn't affect analytics or alerts functionality. For more information about how to enable ContainerLogV2 through either the cluster's DCR or configmap, see[Enable the ContainerLogV2 schema].

Container insights in Azure Monitor provides a recommended schema for container logs, *ContainerLogV2*. The format includes the following fields for common queries to view data related to AKS and Azure Arc-enabled Kubernetes clusters:

**ContainerName****PodName****PodNamespace**

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## View AKS container logs, events, and pod metrics in real time


Prerequisites and setup requirements: Live data feature requires Container insights to be enabled on your cluster and uses direct Kubernetes API access. For private clusters, access requires a computer in the same private network as the cluster. Authentication follows the Kubernetes RBAC model and requires appropriate cluster permissions.

You can view AKS container logs, events, and pod metrics using the *live data* feature in Container insights and troubleshoot issues in real time with direct access to `kubectl logs -c`

, `kubectl get`

events, and `kubectl top pods`

.

Note

AKS uses [Kubernetes cluster-level logging architectures](https://kubernetes.io/docs/concepts/cluster-administration/logging/#cluster-level-logging-architectures). The container logs are located at `/var/log/containers`

on the node. To access a node, see [Connect to AKS cluster nodes](node-access).

To learn how to set up this feature, see [Configure live data in Container insights](/en-us/azure/azure-monitor/containers/container-insights-livedata-setup). The feature directly accesses the Kubernetes API. For more information about the authentication model, see the [Kubernetes API](https://kubernetes.io/docs/concepts/overview/kubernetes-api/).

### View AKS resource live logs


Private cluster network requirements: To access logs from a private cluster, you must use a computer that's in the same private network as the cluster.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Kubernetes resources**, select**Workloads**.For

**Deployment**,**Pod**,**Replica Set**,**Stateful Set**,**Job**, or**Cron Job**, select a value, and then select**Live Logs**.Select a resource log to view.

The following example shows the logs for a pod resource:


### View container live logs using Container insights


Authentication and data streaming: After successful authentication, if data can be retrieved, it begins streaming to theLive Logstab. Log data appears in a continuous stream. Alternative log access is available throughView Logs in Log Analyticsfor historical analysis.

You can view real-time log data as the container engine generates it on the **Cluster**, **Nodes**, **Controllers**, or **Containers** tab.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.On the

**Cluster**,**Nodes**,**Controllers**, or**Containers**tab, select a value.On the

**Overview**pane for the resource, select**Live Logs**.The following image shows the logs for a container resource:


### View container live events using Container insights


Event streaming and access: Real-time event data streams as the container engine generates it. Events include pod creation, deletion, scaling operations, and error conditions. Historical event data is accessible viaView Events in Log Analytics.

You can view real-time event data as the container engine generates it on the **Cluster**, **Nodes**, **Controllers**, or **Containers** tab.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.Select the

**Cluster**,**Nodes**,**Controllers**, or**Containers**tab, and then select an object.On the resource

**Overview**pane, select**Live Events**.After successful authentication, if data can be retrieved, it begins streaming to the

**Live Events**tab. The following image shows the events for a container resource:

### View pod live metrics using Container insights


Metrics scope and availability: Live metrics are available for pod resources on theNodesorControllerstabs. Metrics include CPU usage, memory consumption, network I/O, and filesystem statistics. Historical metrics are accessible throughView Events in Log Analytics.

You can view real-time metrics data as the container engine generates it on the **Nodes** or **Controllers** tab by selecting a pod resource.

In the

[Azure portal](https://portal.azure.com/), go to your AKS cluster.Under

**Monitoring**, select**Insights**.Select the

**Nodes**or**Controllers**tab, and then select a pod object.On the resource

**Overview**pane, select**Live Metrics**.After successful authentication, if data can be retrieved, it begins streaming to the

**Live Metrics**tab. The following image shows the metrics for a pod resource:## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see

[Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Monitor AKS clusters in the Azure portal

The **Monitoring** tab on the **Overview** pane for your AKS cluster resource offers a quick way to start viewing monitoring data in the Azure portal. This tab includes graphs with common metrics for the cluster separated by node pool. You can select any of these graphs to further analyze the data in the [metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).

The **Monitoring** tab also includes links to the [Azure managed service for Prometheus](#integrations) and [Container insights](#integrations) for the cluster. You can enable these tools on the **Monitoring** tab. You might also see a banner at the top of the pane that recommends other features to improve monitoring for your cluster.

Tip

To access monitoring features for all AKS clusters in your subscription, on the Azure portal home page, select **Azure Monitor**.

## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

### Recommended alert rules

For some Azure services, you can [enable recommended out-of-the-box alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

The system compiles a list of recommended alert rules based on:

- The resource provider's knowledge of important signals and thresholds for monitoring the resource.
- Data that tells what customers commonly alert on for this resource.

Note

Recommended alert rules are available for:

- Virtual machines
- Azure Kubernetes Service (AKS) resources
- Log Analytics workspaces

### Configure Prometheus metrics-based alerts


Download and configuration requirements: Alert rules are available as downloadable ARM templates or Bicep files. Before configuring alerts, ensure the managed service for Prometheus is enabled on your cluster and an Azure Monitor workspace is properly linked to your AKS cluster.

When you [enable collection of the managed service for Prometheus metrics](#integrations) for your cluster, you can download a collection of [recommended managed service for Prometheus alert rules](/en-us/azure/azure-monitor/containers/container-insights-metric-alerts#enable-prometheus-alert-rules).

The download includes the following rules:

| Level | Alerts |
|---|---|
| Cluster level | `KubeCPUQuotaOvercommit` `KubeMemoryQuotaOvercommit` `KubeContainerOOMKilledCount` `KubeClientErrors` `KubePersistentVolumeFillingUp` `KubePersistentVolumeInodesFillingUp` `KubePersistentVolumeErrors` `KubeContainerWaiting` `KubeDaemonSetNotScheduled` `KubeDaemonSetMisScheduled` `KubeQuotaAlmostFull` |
| Node level | `KubeNodeUnreachable` `KubeNodeReadinessFlapping` |
| Pod level | `KubePVUsageHigh` `KubeDeploymentReplicasMismatch` `KubeStatefulSetReplicasMismatch` `KubeHpaReplicasMismatch` `KubeHpaMaxedOut` `KubePodCrashLooping` `KubeJobStale` `KubePodContainerRestart` `KubePodReadyStateLow` `KubePodFailedState` `KubePodNotReadyByController` `KubeStatefulSetGenerationMismatch` `KubeJobFailed` `KubeContainerAverageCPUHigh` `KubeContainerAverageMemoryHigh` `KubeletPodStartUpLatencyHigh` |

For more information, see [Create log alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts) and [Query logs from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query).

[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-unified-log) can measure two types of information to help you monitor diverse scenarios:

[Result count](/en-us/azure/azure-monitor/alerts/alerts-unified-log#result-count): Counts the number of rows returned by the query. Use this information to work with events like Windows event logs, syslog events, and application exceptions.[Calculation of a value](/en-us/azure/azure-monitor/alerts/alerts-unified-log#calculation-of-a-value): Makes a calculation based on a numeric column. Use this information to include diverse resources. An example is CPU percentage.

Most log queries compare a `DateTime`

value to the present time using the `now`

operator and going back one hour. To learn how to build log-based alerts, see [Create log alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).

### AKS alert rules

The following table lists some suggested alert rules for AKS. These alerts are only examples. You can set alerts for any metric, log entry, or activity log entry listed in the [AKS monitoring data reference](monitor-aks-reference).

| Condition | Description |
|---|---|
CPU Usage Percentage > 95 |
Alerts when the average CPU usage across all nodes exceeds the threshold. |
Memory Working Set Percentage > 100 |
Alerts when the average working set across all nodes exceeds the threshold. |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

## AKS node network metrics monitoring


Version and enablement requirements: In Kubernetes version 1.29 and later, node network metrics are enabled by default for all clusters that have Azure Monitor enabled. For earlier Kubernetes versions, you must manually enable network monitoring through cluster configuration. This feature requires Azure Monitor or Container insights to be configured on your cluster.

Node network metrics are crucial for maintaining a healthy and performant Kubernetes cluster. By collecting and analyzing data about network traffic, you can gain valuable insights about your cluster's operation and identify potential issues before they lead to outages or performance loss.

The following node network metrics are enabled by default and are aggregated per node. All metrics include the labels cluster and instance (node name). You can easily view these metrics using the Managed Grafana dashboard under **Azure Managed Prometheus** > **Kubernetes** > **Networking** > **Clusters**.

### AKS node network metrics by data plane type

All metrics include these labels:

`cluster`

`instance`

(node name)


OS support and limitations: For Cilium data plane scenarios, the Container Network Observability feature provides metrics only for Linux node pools. Currently, Windows isn't supported for Container Network Observability metrics. Ensure your cluster has Linux node pools for full Cilium metrics availability.

For Cilium data plane scenarios, the Container Network Observability feature provides metrics only for Linux. Currently, Windows isn't supported for Container Network Observability metrics.

Cilium exposes several metrics that Container Network Observability uses:

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
`cilium_forward_count_total` |
Total forwarded packet count | `direction` |
Supported ✅ | Unsupported ❌ |
`cilium_forward_bytes_total` |
Total forwarded byte count | `direction` |
Supported ✅ | Unsupported ❌ |
`cilium_drop_count_total` |
Total dropped packet count | `direction` , `reason` |
Supported ✅ | Unsupported ❌ |
`cilium_drop_bytes_total` |
Total dropped byte count | `direction` , `reason` |
Supported ✅ | Unsupported ❌ |

### Disable AKS node network metrics collection

You can disable network metrics collection on specific nodes by adding the label `networking.azure.com/node-network-metrics=disabled`

to those nodes.

Note

Retina has an `operator: "Exists"`

`effect: NoSchedule`

toleration, so it bypasses `NoSchedule`

taints. Therefore, labels are used instead of taints to control scheduling.

If the cluster is `autoprovisioning/autoscaling`

nodes, you need to manually enable the flag on each node.

Important

This feature isn't applicable if Advanced Container Networking Services (ACNS) is enabled on your cluster.

To disable metrics collection on a node:

```
kubectl label node <node-name> networking.azure.com/node-network-metrics=disabled
```


For detailed pod-level and DNS metrics, see [Advanced Container Networking Services](advanced-container-networking-services-overview).

## Related content

- For a reference of the metrics, logs, and other important values created for AKS, see the
[AKS monitoring data reference](monitor-aks-reference). - For general details on monitoring Azure resources, see
[Monitor Azure resources using Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource). - For detailed monitoring of the complete Kubernetes stack, see
[Monitor Kubernetes clusters using Azure services and cloud native tools](/en-us/azure/azure-monitor/containers/monitor-kubernetes). - For collecting metrics data from Kubernetes clusters, see
[Managed service for Prometheus in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview). - For collecting logs in Kubernetes clusters, see
[Azure Monitor features for Kubernetes monitoring](/en-us/azure/azure-monitor/containers/container-insights-overview). - For data visualization, see
[Azure Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview)and[Monitor your Azure services in Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-upgrade -->

# Upgrade Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article addresses upgrade experiences for Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To learn more about the release schedule and support for service mesh add-on revisions, read the [support policy](istio-support-policy#versioning-and-support-policy).

## Minor revision upgrade

Istio add-on allows upgrading the minor revision using [canary upgrade process](https://istio.io/latest/docs/setup/upgrade/canary/). When an upgrade is initiated, the control plane of the new (canary) revision is deployed alongside the initial (stable) revision's control plane. You can then manually roll over data plane workloads while using monitoring tools to track the health of workloads during this process. If you don't observe any issues with the health of your workloads, you can complete the upgrade so that only the new revision remains on the cluster. Else, you can roll back to the previous revision of Istio.

Available upgrades depend on whether the current Istio revision and AKS cluster version are supported:

- You can upgrade to the
**next supported revision (**or skip one and upgrade to`n+1`

), as long as both are supported and compatible with the cluster version.`n+2`

- If both your current revision (
`n`

) and the next revision (`n+1`

) are unsupported, you can only upgrade to the**nearest supported revision (**, but not beyond it.`n+2`

or higher) - If the cluster version and Istio revision are both unsupported, the cluster version must be upgraded before an Istio upgrade can be initiated.

Note

Once an AKS version or mesh revision falls outside the support window, upgrading either version becomes error-prone. While such upgrades are **allowed** to recover to a supported version, **the upgrade process and the out-of-support versions themselves are both not supported by Microsoft**. We strongly recommend keeping AKS version and mesh revision up to date to avoid running into unsupported scenarios. Refer to the [Istio add-on support calendar](istio-support-policy#service-mesh-add-on-release-calendar) for estimated release and end-of-life dates and the [upstream Istio release notes](https://istio.io/latest/news/releases/) for the new revision for notable changes.

The following example illustrates how to upgrade from revision `asm-1-23`

to `asm-1-24`

with all workloads in the `default`

namespace. The steps are the same for all minor upgrades and may be used for any number of namespaces.

Use the

[az aks mesh get-upgrades](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-upgrades)command to check which revisions are available for the cluster as upgrade targets:`az aks mesh get-upgrades --resource-group $RESOURCE_GROUP --name $CLUSTER`

If you expect to see a newer revision not returned by this command, you may need to upgrade your AKS cluster first so that it's compatible with the newest revision.

If you set up

[mesh configuration](istio-meshconfig)for the existing mesh revision on your cluster, you need to create a separate ConfigMap corresponding to the new revision in the`aks-istio-system`

namespace**before initiating the canary upgrade**in the next step. This configuration is applicable the moment the new revision's control plane is deployed on cluster. More details can be found[here](istio-meshconfig#mesh-configuration-and-upgrades).Initiate a canary upgrade from revision

`asm-1-23`

to`asm-1-24`

using[az aks mesh upgrade start](/en-us/cli/azure/aks/mesh/upgrade#az-aks-mesh-upgrade-start):`az aks mesh upgrade start --resource-group $RESOURCE_GROUP --name $CLUSTER --revision asm-1-24`

A canary upgrade means the 1.24 control plane is deployed alongside the 1.23 control plane. They continue to coexist until you either complete or roll back the upgrade.

While a canary upgrade is in progress, the higher revision is considered the

*default revision*used for validation of Istio resources.Optionally, revision tags may be used to roll over the data plane to the new revision without needing to manually relabel each namespace. Manually relabeling namespaces when moving them to a new revision can be tedious and error-prone.

[Revision tags](https://istio.io/latest/docs/setup/upgrade/canary/#stable-revision-labels)solve this problem by serving as stable identifiers that point to revisions.Rather than relabeling each namespace, a cluster operator can change the tag to point to a new revision. All namespaces labeled with that tag are updated at the same time. However, you still need to restart the workloads to make sure the correct version of

`istio-proxy`

sidecars are injected.To use revision tags during an upgrade:

Create a revision tag for the initial revision. In this example, we name it

`prod-stable`

:`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system`

Create a revision tag for the revision installed during the upgrade. In this example, we name it

`prod-canary`

:`istioctl tag set prod-canary --revision asm-1-24 --istioNamespace aks-istio-system`

Label application namespaces to map to revision tags:

`# label default namespace to map to asm-1-23 kubectl label ns default istio.io/rev=prod-stable --overwrite`

You may also label namespaces with

`istio.io/rev=prod-canary`

for the newer revision. However, the workloads in those namespaces aren't updated to a new sidecar until they're restarted.If a new application is created in a namespace after it is labeled, a sidecar will be injected corresponding to the revision tag on that namespace.


Verify control plane pods corresponding to both

`asm-1-23`

and`asm-1-24`

exist:Verify

`istiod`

pods:`kubectl get pods -n aks-istio-system`

Example output:

`NAME READY STATUS RESTARTS AGE istiod-asm-1-23-55fccf84c8-dbzlt 1/1 Running 0 58m istiod-asm-1-23-55fccf84c8-fg8zh 1/1 Running 0 58m istiod-asm-1-24-f85f46bf5-7rwg4 1/1 Running 0 51m istiod-asm-1-24-f85f46bf5-8p9qx 1/1 Running 0 51m`

If ingress is enabled, verify ingress pods:

`kubectl get pods -n aks-istio-ingress`

Example output:

`NAME READY STATUS RESTARTS AGE aks-istio-ingressgateway-external-asm-1-23-58f889f99d-qkvq2 1/1 Running 0 59m aks-istio-ingressgateway-external-asm-1-23-58f889f99d-vhtd5 1/1 Running 0 58m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-ft9c8 1/1 Running 0 51m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-wcb6s 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-4cc2l 1/1 Running 0 58m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-jjc7m 1/1 Running 0 59m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-g89s4 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-krq9w 1/1 Running 0 51m`

Observe that ingress gateway pods of both revisions are deployed side-by-side. However, the service and its IP remain immutable.


Relabel the namespace so that any new pods are mapped to the Istio sidecar associated with the new revision and its control plane:

If using revision tags, overwrite the

`prod-stable`

tag itself to change its mapping:`istioctl tag set prod-stable --revision asm-1-24 --istioNamespace aks-istio-system --overwrite`

Verify the tag-to-revision mappings:

`istioctl tag list`

Both tags should point to the newly installed revision:

`TAG REVISION NAMESPACES prod-canary asm-1-24 default prod-stable asm-1-24 ...`

In this case, you don't need to relabel each namespace individually.

If not using revision tags, data plane namespaces must be relabeled to point to the new revision:

`kubectl label namespace default istio.io/rev=asm-1-24 --overwrite`


Relabeling doesn't affect your workloads until they're restarted.

Individually roll over each of your application workloads by restarting them. For example:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Check your monitoring tools and dashboards to determine whether your workloads are all running in a healthy state after the restart. Based on the outcome, you have two options:

**Complete the canary upgrade**: If you're satisfied that the workloads are all running in a healthy state as expected, you can complete the canary upgrade. Completion of the upgrade removes the previous revision's control plane and leaves behind the new revision's control plane on the cluster. Run the following command to complete the canary upgrade:`az aks mesh upgrade complete --resource-group $RESOURCE_GROUP --name $CLUSTER`

**Rollback the canary upgrade**: In case you observe any issues with the health of your workloads, you can roll back to the previous revision of Istio:

Relabel the namespace to the previous revision: If using revision tags:

`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system --overwrite`

Or, if not using revision tags:

`kubectl label namespace default istio.io/rev=asm-1-23 --overwrite`

Roll back the workloads to use the sidecar corresponding to the previous Istio revision by restarting these workloads again:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Roll back the control plane to the previous revision:

`az aks mesh upgrade rollback --resource-group $RESOURCE_GROUP --name $CLUSTER`


The

`prod-canary`

revision tag can be removed:`istioctl tag remove prod-canary --istioNamespace aks-istio-system`

If

[mesh configuration](istio-meshconfig)was previously set up for the revisions, you can now delete the ConfigMap for the revision that was removed from the cluster during complete/rollback.

### Minor revision upgrades with ingress and egress gateways

If you're currently using [Istio ingress gateways](istio-deploy-ingress) or [egress gateways](istio-deploy-egress) and are performing a minor revision upgrade, keep in mind that Istio ingress and egress gateway pods / deployments are deployed per-revision, but the service is shared across both revisions.

We provide a single `LoadBalancer`

service across all ingress gateway pods over multiple revisions, so the external/internal IP address of the ingress gateways remains unchanged throughout the course of an upgrade. Thus, during the canary upgrade, when two revisions exist simultaneously on the cluster, the ingress gateway pods of both revisions serve incoming traffic.

Likewise, during a canary upgrade, all pods for an egress gateway across both revisions will be served by a single `ClusterIP`

service.

### Minor revision upgrades with horizontal pod autoscaling customizations

If you have customized [horizontal pod autoscaling (HPA) settings for Istiod or the ingress gateways](istio-scale#horizontal-pod-autoscaling-customization), note the following behavior for how HPA settings are applied across both revisions to maintain consistency during a canary upgrade:

- If you update the HPA spec before initiating an upgrade, the settings from the existing (stable) revision will be applied to the HPAs of the canary revision when the new control plane is installed.
- If you update the HPA spec while a canary upgrade is in progress, the HPA spec of the stable revision will take precedence and be applied to the HPA of the canary revision.
- If you update the HPA of the stable revision during an upgrade, the HPA spec of the canary revision will be updated to reflect the new settings applied to the stable revision.
- If you update the HPA of the canary revision during an upgrade, the HPA spec of the canary revision will be reverted to the HPA spec of the stable revision.


## Patch version upgrade

- Istio add-on patch version availability information is published in
[AKS release notes](https://github.com/Azure/AKS/releases). - Patches are rolled out automatically for istiod and ingress pods as part of these AKS releases, which respect the
`default`

[planned maintenance window](planned-maintenance)set up for the cluster. - User needs to initiate patches to Istio proxy in their workloads by restarting the pods for reinjection:
Check the version of the Istio proxy intended for new or restarted pods. This version is the same as the version of the istiod and Istio ingress pods after they were patched:

`kubectl get cm -n aks-istio-system -o yaml | grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`"image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless", "image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless"`

Check the Istio proxy image version for all pods in a namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.23.0, mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless`

To trigger reinjection, restart the workloads. For example:

`kubectl rollout restart deployments/productpage-v1 -n default`

To verify that they're now on the newer versions, check the Istio proxy image version again for all pods in the namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.2.0, mcr.microsoft.com/oss/istio/proxyv2:1.24.0-distroless`


Note

In case of any issues encountered during upgrades, refer to [article on troubleshooting mesh revision upgrades](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-minor-revision-upgrade)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux -->

# Use the Azure Linux container host for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Linux container host for AKS is an open-source Linux distribution created by Microsoft, and it's generally available as a container host on Azure Kubernetes Service (AKS). The Azure Linux container host provides reliability and consistency from cloud to edge across the AKS, AKS-HCI, and Arc products. You can deploy Azure Linux node pools in a new cluster, add Azure Linux node pools to your existing Ubuntu clusters, or migrate your Ubuntu nodes to Azure Linux nodes. To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Why use Azure Linux

The Azure Linux container host on AKS uses a native AKS image that provides one place to do all Linux development. Every package is built from source and validated, ensuring your services run on proven components. Azure Linux is lightweight, only including the necessary set of packages needed to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At the base layer, it has a Microsoft hardened kernel tuned for Azure. Learn more about the [key capabilities of Azure Linux](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-key-benefits).

## How to use Azure Linux on AKS

To get started using the Azure Linux container host for AKS, see:

[Creating a cluster with Azure Linux](/en-us/azure/azure-linux/quickstart-azure-cli)[How to upgrade Azure Linux clusters](/en-us/azure/azure-linux/tutorial-azure-linux-upgrade)[Add an Azure Linux node pool to your existing cluster](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli)[Ubuntu to Azure Linux migration](/en-us/azure/azure-linux/tutorial-azure-linux-migration)[Azure Linux supported GPU SKUs](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-supported-gpu-skus)

## Regional availability

The Azure Linux container host is available for use in the same regions as AKS.

## Next steps

To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-nodepools -->

# Start and stop an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might not need to continuously run your AKS workloads. For example, you might have a development cluster that has node pools running specific workloads. To optimize your compute costs, you can completely stop your node pools in your AKS cluster.

## Features and limitations

- You can't stop system pools.
- Spot node pools are supported.
- Stopped node pools can be upgraded.
- The cluster and node pool must be running.
- You can't stop node pools from clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature.

Tip

You can use Azure Copilot to stop and start your node pools in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#start-and-stop-node-pools).

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Stop an AKS node pool

Stop a running AKS node pool using the

command.`az aks nodepool stop`

`az aks nodepool stop --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool stopped using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Stopped`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Stopped" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Stopping`

, your node pool is still in the process of stopping.Note

Stopping the node pool will stop its Cluster Autoscaler, and starts it back when starting the node pool. So if you manually modify the number of VMSS instances in the pool while it's stopped, Cluster Autoscaler might show inconsistencies.


## Start a stopped AKS node pool

Restart a stopped node pool using the

command.`az aks nodepool start`

`az aks nodepool start --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool started using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Running`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Running" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Starting`

, your node pool is still in the process of starting.

## Next steps

- To learn how to scale
`User`

pools to 0, see[scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to stop your cluster, see
[cluster start/stop](start-stop-cluster). - To learn how to save costs using Spot instances, see
[add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-dedicated-hosts -->

# Add Azure Dedicated Host to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Dedicated Host is a service that provides physical servers - able to host one or more virtual machines - dedicated to one Azure subscription. Dedicated hosts are the same physical servers used in our data centers, provided as a resource. You can provision dedicated hosts within a region, availability zone, and fault domain. Then, you can place VMs directly into your provisioned hosts, in whatever configuration best meets your needs.

Using Azure Dedicated Hosts for nodes with your AKS cluster has the following benefits:

- Hardware isolation at the physical server level. No other VMs will be placed on your hosts. Dedicated hosts are deployed in the same data centers and share the same network and underlying storage infrastructure as other, non-isolated hosts.
- Control over maintenance events initiated by the Azure platform. While most maintenance events have little to no impact on your virtual machines, there are some sensitive workloads where each second of pause can have an impact. With dedicated hosts, you can opt in to a maintenance window to reduce the impact to your service.

## Before you begin

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Before you start, ensure that your version of the Azure CLI is 2.39.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you integrate Azure Dedicated Host with Azure Kubernetes Service:

- Accelerated Networking
- An existing agent pool can't be converted from non-ADH to ADH or ADH to non-ADH.
- It isn't supported to update agent pool from host group A to host group B.
- Using ADH across subscriptions.

## Planning for ADH Capacity on AKS

Not all host SKUs are available in all regions, and availability zones. You can list host availability, and any offer restrictions before you start provisioning dedicated hosts.

```
az vm list-skus --location eastus --resource-type hostGroups/hosts -o table
```


Note

First, when using host group, the nodepool fault domain count is always the same as the host group fault domain count. In order to use cluster auto-scaling to work with ADH and AKS, please make sure your host group fault domain count and capacity is enough. Secondly, only change fault domain count from the default of 1 to any other number if you know what they are doing as a misconfiguration could lead to a unscalable configuration.

[Determine how many hosts you would need based on the expected VM Utilization](/en-us/azure/virtual-machines/dedicated-host-general-purpose-skus).

Evaluate [host utilization](/en-us/azure/virtual-machines/dedicated-hosts-how-to#check-the-status-of-the-host) to determine the number of allocatable VMs by size before you deploy.

```
az vm host get-instance-view --resource-group myDHResourceGroup --host-group MyHostGroup --name MyHost
```


## Add a Dedicated Host Group to an AKS cluster

A host group is a resource that represents a collection of dedicated hosts. You create a host group in a region and an availability zone, and add hosts to it. When planning for high availability, there are more options. You can use one or both of the following options with your dedicated hosts:

- Span across multiple availability zones. In this case, you're required to have a host group in each of the zones you wish to use.
- Span across multiple fault domains, which are mapped to physical racks.

In either case, you need to provide the fault domain count for your host group. If you don't want to span fault domains in your group, use a fault domain count of 1.

You can also decide to use both availability zones and fault domains.

## Create a Host Group

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

For more information about the host SKUs and pricing, see [Azure Dedicated Host pricing](https://azure.microsoft.com/pricing/details/virtual-machines/dedicated-host/).

Use az vm host create to create a host. If you set a fault domain count for your host group, you'll be asked to specify the fault domain for your host.

In this example, we'll use [az vm host group create](/en-us/cli/azure/vm/host/group#az-vm-host-group-create) to create a host group using both availability zones and fault domains.

```
az vm host group create \
--name myHostGroup \
--resource-group myDHResourceGroup \
--zone 1 \
--platform-fault-domain-count 1 \
--automatic-placement true
```


## Create a Dedicated Host

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

If you set a fault domain count for your host group, you'll need to specify the fault domain for your host.

```
az vm host create \
--host-group myHostGroup \
--name myHost \
--sku DSv3-Type1 \
--platform-fault-domain 1 \
--resource-group myDHResourceGroup
```


## Use a user-assigned Identity

Important

A user-assigned Identity with "contributor" role on the Resource Group of the Host Group is required.

First, create a Managed Identity

```
az identity create --resource-group <Resource Group> --name <Managed Identity name>
```


Assign Managed Identity

```
az role assignment create --assignee <id> --role "Contributor" --scope <Resource id>
```


## Create an AKS cluster using the Host Group

Create an AKS cluster, and add the Host Group you just configured.

```
az aks create \
--resource-group MyResourceGroup \
--name MyManagedCluster \
--location eastus \
--nodepool-name agentpool1 \
--node-count 1 \
--host-group-id <id> \
--node-vm-size Standard_D2s_v3 \
--assign-identity <id> \
--generate-ssh-keys
```


## Add a Dedicated Host Node Pool to an existing AKS cluster

Add a Host Group to an already existing AKS cluster.

```
az aks nodepool add --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup --node-count 1 --host-group-id <id> --node-vm-size Standard_D2s_v3
```


## Remove a Dedicated Host Node Pool from an AKS cluster

```
az aks nodepool delete --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup
```


## Next steps

In this article, you learned how to create an AKS cluster with a Dedicated host, and to add a dedicated host to an existing cluster. For more information about Dedicated Hosts, see [dedicated-hosts](/en-us/azure/virtual-machines/dedicated-hosts).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-communication-manager -->

# Set up the Azure Kubernetes Service communication manager

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) communication manager streamlines notifications for all your AKS maintenance tasks by using Azure Resource Notifications and Azure Resource Graph frameworks. The communication manager gives you timely alerts on event triggers and outcomes, so that you can closely monitor your upgrades.

If maintenance fails, the communication manager notifies you with the reasons for the failure. This information reduces operational hassles related to observability and follow-ups.

By following the steps in this article, you can set up notifications for all types of automatic upgrades that use maintenance windows.

## Prerequisites

Configure your cluster for either the

[automatic upgrade channel](auto-upgrade-cluster)or the[automatic upgrade channel for nodes](auto-upgrade-node-os-image).Create a

[planned maintenance window](planned-maintenance)for your configuration of automatic upgrades.

## Set up the communication manager

In the Azure portal, go to the resource.

Select

**Monitoring**>**Alerts**>**Alert Rules**, and then select**Create**.On the

**Condition**tab, for**Signal name**, select**Custom log search**.In the

**Search query**box, paste one of the following custom queries. Be sure to update the`where id contains`

path to reference your resources for subscription ID, resource group name, and cluster name.The following query is for notifications of automatic upgrades for clusters:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "K8sVersionUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

The following query is for notifications of automatic upgrades for NodeOS:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "NodeOSUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

Go to the

**Condition**tab. Configure the alert conditions with the following settings:**Measure**: Select**Table rows**.**Aggregation type**: Select**Count**.**Aggregation granularity**: Select**30 minutes**.**Threshold value**: Keep at**0**.**Split by dimensions**: For**Dimension name**, select**status**. Then select the**Include all future values**checkbox.

In the

**Split by dimensions**area, for**Dimension values**, select a value. Because you selected**status**for the dimension name, the available values are**Scheduled**,**Started**,**Completed**,**Canceled**, and**Failed**.Note

These status values appear only if your cluster previously executed automatic upgrade operations. For new clusters or for clusters that haven't undergone automatic upgrades yet, the dropdown list might appear empty or show no available dimensions. After your cluster performs its first automatic upgrade, these status values become available for selection.

Go to the

**Actions**tab. Make sure that an action group with the correct email address exists, so that you can receive the notifications:Select

**Use action groups**>**Create an action group**.For

**Notification type**, select**Email/SMS_message/Push/Voice**.Select the

**Email**checkbox, and then enter the email address in the**Email**box.

Go to the

**Details**tab. Assign a managed identity so that you can grant access to the necessary resources. In the**Identity**area, select**System assigned managed identity**.Go to the

**Review + create**tab, and then select**Create**.Now that you've created the alert rule, you can assign the appropriate roles for the managed identity:

- In the alert rule, go to
**Settings**>**Identity**>**System assigned managed identity**>**Azure role assignments**. - Select
**Add role assignment**, select the**Reader**role, and assign it to the resource group. - Select
**Add role assignment**again, select the**Reader**role, and assign it to the subscription.

Tip

If you don't see the

**Identity**option, make sure that you created your alert rule and that you have the necessary permissions.- In the alert rule, go to

After you set up the communication manager, it sends advance notices one week before maintenance starts and one day before maintenance starts. It also sends you timely alerts during the maintenance operation.

## Verify the configuration

To upgrade the cluster, wait for the automatic upgrader to start. Then verify that you promptly receive notices on the email address that you configured to receive notices.

Check the Azure Resource Graph database for the scheduled notification record. Each scheduled event notification should be listed as one record in the `ContainerServiceEventResources`

table.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/considerations-pod-sandboxing -->

# Pod Sandboxing considerations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Pod Sandboxing deployments on Azure Kubernetes Service (AKS) there are several items to consider in regard to resource management, memory management, CPU management, and security.

## Resource management

Memory and CPU management behavior with Pod Sandboxing might be unfamiliar to some users. These considerations are relevant when specifying resources in a deployment, especially for larger and resource sensitive workloads.

### Kata components

In a Kata deployment, there are generally two families of components that get deployed. You have **host components** and **guest components**.

- The main
**host components**comprise of the*Kata shim*,*Cloud Hypervisor*, and*virtiofsd*.- The
*Kata shim*manages a pod VM lifecycle. *Cloud Hypervisor*is the Virtual Machine Monitor (VMM) used by the Kata shim.*virtiofsd*is a daemon used to share files between each Pod VM and its container host.

- The
- The main
**guest components**include the*user's workloads*,*pod VM kernel*, and the*Kata agent*.- The
*Kata agent*manages containers inside of the Pod VMs

- The

### Memory management

With Kata pods, you have the ability to specify the amount of memory of the Pod VM that hosts your workloads. It's crucial that you configure the values accordingly so that a pod has sufficient resources, but doesn't result in unused memory being allocated to the pod.

### Pod VM memory size

There's an amount of memory allocated to each pod VM that runs a container. This VM memory size is inclusive of all the memory necessary to run Kata guest components. Users should take care to ensure that they buffer some extra memory beyond the expected consumption of their workloads to account for the consumption of other guest components, such as the kata agent or VM kernel. Examples are given on typical memory values later on in this article.

The pod VM memory size is equivalent to the [Kubernetes pod memory limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/#specify-a-memory-request-and-a-memory-limit) the user specifies. A user can change the value by changing their pod memory limit; if no values are specified, a default size of 512Mi is applied. Once the pod starts, this size becomes fixed.

As the pod VM memory size increases, the runtime class memory overhead should be expected to increase alongside it.

### Runtime class memory overhead

Pod Sandboxing workloads come with a default kata runtime class (`kata-vm-isolation`

) which comes with default overheads for resources. Users that want finer grain control of their resource quotas can [set up a custom runtime class](https://kubernetes.io/docs/concepts/containers/runtime-class/#setup) with specific resource overheads. When doing so, users should ensure that the memory overhead value of the runtime class is enough that covers all expected usage for the **host components** of a kata deployment. The runtime class memory overhead does *not* need to account for the expected memory consumption of the **guest components**.

You can create a specialized runtime and specify the memory overhead in your runtime class through the `overhead`

field in your `RuntimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example), let's assume I want to create a runtime for workloads I expect to be smaller in consumption:

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: small-kata-pods
handler: kata
overhead:
podFixed:
memory: "120Mi"
```


Specifying overheads isn't required, and suggested if you want finer control over the resources being set aside for your workloads. If you use the default `kata-vm-isolation`

runtime class and don't specify any overheads in your YAML, the overhead of the Pod VM size defaults to 512Mi and the runtime class overhead defaults to 600Mi. This default runtime overhead is calculated with the default pod VM size (512Mi) plus to approximate memory needed by host components for such a VM size (~88Mi).

### User workloads

When a user deploys a Kata workload, they're able to use memory up to the configured *pod VM memory size* minus the other guest components, such as the Kata agent or the guest VM kernel.

If you would like to get an approximation of the memory used by these components:

- Connect to the pod VM (either via
`kubectl exec`

or`kubectl debug`

to open a shell inside your pod). - Run the
`free`

command. - Inspect the "used" column in the output to get an idea of the memory consumed by the guest kernel/kata agent.

### Memory cgroups

When a Kata pod is scheduled to run, kubelet assigns the pod to a memory `cgroup`

. This `cgroup`

enforces the pod's memory limits/requests, allowing a user to define the resource quotas available to a pod.

Within the memory `cgroup`

, there are two important fields to consider:

`memory.current`

defines how many bytes of memory the host components and the pod VM memory size allocates.`memory.max`

optional, user defined upper limit of memory.current for pods where users want to impose a memory limit.- The kubelet computes this value as the sum of a pod's memory limit and its runtime class memory overhead.


At any point, if the `memory.current`

value exceeds that of `memory.max`

, [the kernel might trigger an OOMKill on the pod if memory pressure is detected](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#requests-and-limits).

### Reference usage values

Users can utilize these values to serve as a reference for the typical memory usage and values across the different variables covered. Pod VM memory sizes under 128Mi aren't supported.

| Pod VM Memory Size | Runtime class overhead | memory.current | memory.max | Free memory available to Host components |
|---|---|---|---|---|
| 128Mi | 16Mi | 133Mi | 144Mi | 11Mi |
| 256Mi | 32Mi | 263Mi | 288Mi | 25Mi |
| 1Gi | 128Mi | 1034Mi | 1152Mi | 118Mi |
| 2Gi | 256Mi | 2063Mi | 2304Mi | 241Mi |
| 4Gi | 374Mi | 4122Mi | 4470Mi | 348Mi |
| 8Gi | 512Mi | 8232Mi | 8704Mi | 472Mi |
| 32Gi | 640Mi | 32918Mi | 33408Mi | 490Mi |
| 64Gi | 768Mi | 65825Mi | 66304Mi | 479Mi |
| 96Gi | 896Mi | 98738Mi | 99200Mi | 462Mi |
| 128Gi | 1Gi | 131646Mi | 132096Mi | 450Mi |

## CPU management

In a similar vein to memory, you can also allocate CPU resources to your Kata workloads. Doing so is recommended; without declaring a CPU limit for your Kata pod, Kata host components are able to use any CPU capacity available on the node.

### Reserving CPU

When reserving CPUs for your Kata workloads, you have two fields you can choose to set.

- The
*runtime class CPU overhead* - The
*pod CPU limit*

When at least one of the two values is specified, the control plane reserves the specified number of CPUs on the node for your workload. Other pods on the same node can't access this reserved capacity.

### Pod CPU limit

You can declare your [pod CPU limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) in your application's manifest. A specified pod CPU limit defines the limit of the CPUs that containers in the associated pod VM can use.

If you specify fractions of CPUs for the pod CPU limit, those fractions will get rounded up to the next integer. The rounded up number becomes the number of vCPUs allocated to the Pod VM, but a `cgroup`

will limit the workload to only consume the fraction specified in the pod CPU limit.

If no number is declared, one vCPU will be allocated to the pod VM if the capacity is available on the node. There's no limit on the CPU consumption of the Kata host components.

### Runtime class CPU overhead

The runtime class overhead should be specified if you'd like to preemptively reserve some node capacity for the Kata host components.

You can specify the memory overhead in your runtime class through the `overhead`

field in your `RunTimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example):

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: custom-kata-runtime
handler: kata
overhead:
podFixed:
cpu: "250m"
```


### Best practices

#### Memory management

- Ensure you specify pod VM memory sizes (defined by the
`limits.memory`

in your manifest) and suitable resource quotas for all your deployments.- Ensure you use a nonzero
*pod request*if you want to ensure that some node capacity is reserved for the pod VM before that VM starts up. The request should account for the pod VM and containers that are expected to run on it. - Ensure you use a nonzero
*runtime class overhead*if you want to reserve some node capacity for the Kata host components before those components start up.

- Ensure you use a nonzero
- If you expect your pod workloads to be especially resource hungry, you can specify limits accordingly for the pod VM to ensure that there are ample resources available for your workloads.
- Declare a suitable runtime class memory overhead such that it gives enough memory for your host components but doesn't take too much to avoid allocating unused memory.

#### CPU management

If your node typically has plenty of free CPU capacity, these reservations might be unnecessary.

If your nodes typically run to the limit with CPU consumption, then a nonzero reservation ensures your pods can be executed more reliably.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
*not*available to other workloads on the node.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
Make sure you specify CPU requests that your infrastructure can accommodate. If your available capacity runs near 0, or your request is too large, your workloads might

[fail to start](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/#specify-a-cpu-request-that-is-too-big-for-your-nodes)Align your CPU requests with your CPU limits. The Kata shim doesn't have visibility into requests. Therefore, if no CPU limit is declared, the pod VM is limited to one vCPU. The Kata host components, which do have visibility into request values, consumes the rest of the requested CPU count and have no limit to CPU consumption.

Reserved capacity for a specific workload is

*not*available to other workloads on the node.

### Example declarations

| Runtime class CPU overhead | Pod CPU Request/Limit | Expected behavior |
|---|---|---|
| 1 | 1 | The control plane reserves two CPUs on the node. The pod VM gets one CPU, and containers on the pod can use up to the one vCPU capacity. The Kata host components and pod VM together can use up to two CPUs from the reserved capacity on the node. |
| 1 | 2.5 | The control plane reserves 3.5 CPUs on the node. The pod VM gets three vCPUs, but containers on the pod VM can use up to 2.5 vCPU capacity. The Kata host components and pod VM together can use up to 3.5 CPUs from the reserved capacity on the node. |
| None | 1 | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The Kata host components and the pod VM together are allowed to use up to one CPU from the reserved capacity on the node. One CPU is always available to the pod VM due to the CPU request. |
| 1 | None | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The kata host components and the pod VM can use any CPU capacity available on the node. At least one CPU is always available due to the overhead reservation. |

## Security

Pod Sandboxing offers users a compelling option to isolate their workloads from other workloads and the host. There are, nonetheless, important security concerns that should be taken into account.

### Privileged pods

There are scenarios in which privileged pods might be required. Users are able to spin up privileged pods, but no [host devices are attached to the pod](https://github.com/kata-containers/kata-containers/blob/main/docs/how-to/privileged.md#containerd).

Using privileged containers lead to root access in the guest VM, but remain isolated from the host.

Privileged pods, even on Pod Sandboxing, should only be used when necessary. Privileged pods should continue to be [managed by trusted users](https://kubernetes.io/docs/concepts/security/pod-security-standards/#privileged).

### Host path storage volumes

`hostPath`

volumes can be mounted into Kata pods. In Pod Sandboxing, using `hostPath`

volumes can potentially undermine the isolation that Kata provides; since part of the host filesystem is exposed directly to the container, a potential attack vector is opened. The warnings posed by [upstream](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) should be considered as relevant for Pod Sandboxing as well.

There are some exceptions; files under `/dev`

are mounted into the container from the guest system instead of the host system. This helps maintain pod isolation for situations where this path must be mounted to function.

Warning

Unless necessary, the recommendation is to *avoid* using hostPath storage volumes.

#### Blocking hostPath via Azure Policy

[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) allows users to apply at-scale enforcements and safeguards on their cluster components in a centralized, consistent manner.

There is a set of [built-in policy sets](policy-reference) for AKS that enforce best practices. Users can take advantage of one of these policies to block deployments that attempt to mount hostPaths.

## Next steps

Once you're ready, learn how to [deploy pod sandboxing on AKS](use-pod-sandboxing).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes -->

# Enable Federal Information Process Standard (FIPS) for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Federal Information Processing Standard (FIPS) 140-2 is a US government standard that defines minimum security requirements for cryptographic modules in information technology products and systems. Azure Kubernetes Service (AKS) allows you to create Linux and Windows node pools with FIPS 140-2 enabled. Deployments running on FIPS-enabled node pools can use those cryptographic modules to provide increased security and help meet security controls as part of FedRAMP compliance. For more information on FIPS 140-2, see [Federal Information Processing Standard (FIPS) 140](/en-us/azure/compliance/offerings/offering-fips-140-2).

Important

Starting on **March 17, 2027**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

Azure CLI version 2.32.0 or later installed and configured. To find the version, run `az --version`

. For more information about installing or upgrading the Azure CLI, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

AKS Monitoring Addon supports FIPS enabled node pools with Ubuntu, Azure Linux, and Windows starting with Agent version 3.1.17 (Linux) and Win-3.1.17 (Windows).

## Limitations

- FIPS-enabled node pools have the following limitations:
- FIPS-enabled node pools require Kubernetes version 1.19 and greater.
- To update the underlying packages or modules used for FIPS, you must use
[Node Image Upgrade](node-image-upgrade). - Container images on the FIPS nodes aren't assessed for FIPS compliance.
- Mounting of a CIFS share fails because FIPS disables some authentication modules. To work around this issue, see
[Errors when mounting a file share on a FIPS-enabled node pool](/en-us/troubleshoot/azure/azure-kubernetes/fail-to-mount-azure-file-share#fipsnodepool). - FIPS-enabled node pools with
[Arm64 VMs](use-arm64-vms)are only supported with Azure Linux 3.0+. - FIPS isn't supported with
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks).


Important

The FIPS-enabled Linux image is a different image than the default Linux image used for Linux-based node pools.

FIPS-enabled node images can have different version numbers, such as kernel version, than images that aren't FIPS-enabled. The update cycle for FIPS-enabled node pools and node images can differ from node pools and images that aren't FIPS-enabled.

## Supported OS Versions

You can create FIPS-enabled node pools on all supported OS types (Linux and Windows). However, not all OS versions support FIPS-enabled node pools. After a new OS version is released, there's typically a waiting period before it's FIPS compliant.

This table includes the supported OS versions:

| OS Type | OS SKU | FIPS Compliance |
|---|---|---|
| Linux | Ubuntu | Supported |
| Linux | Azure Linux | Supported |
| Windows | Windows Server 2019 | Supported |
| Windows | Windows Server 2022 | Supported |

When requesting FIPS enabled Ubuntu, if the default Ubuntu version doesn't support FIPS, AKS defaults to the most recent FIPS-supported version of Ubuntu. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support FIPS, AKS defaults to Ubuntu 20.04 for Linux FIPS-enabled node pools.

Note

Previously, you could use the GetOSOptions API to determine whether a given OS supported FIPS. The GetOSOptions API is now deprecated and it will no longer be included in new AKS API versions starting with 2024-05-01.

## Create a FIPS-enabled Linux node pool

Create a FIPS-enabled Linux node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image`

Note

You can also use the

`--enable-fips-image`

parameter with the[az aks create](/en-us/cli/azure/aks#az-aks-create)command when creating a cluster to enable FIPS on the default node pool. When adding node pools to a cluster created in this way, you still must use the`--enable-fips-image`

parameter when adding node pools to create a FIPS-enabled node pool.Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows the

*fipsnp*node pool is FIPS-enabled:`Name enableFips --------- ------------ fipsnp True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-fipsnp`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-fipsnp-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-fipsnp-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-fipsnp-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-fipsnp-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-fipsnp-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Create a FIPS-enabled Windows node pool

Create a FIPS-enabled Windows node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter. Unlike Linux-based node pools, Windows node pools share the same image set.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image \ --os-type Windows`

Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

Verify Windows node pools have access to the FIPS cryptographic libraries by

[creating an RDP connection to a Windows node](rdp)in a FIPS-enabled node pool and check the registry. From the**Run**application, enter`regedit`

.Look for

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FIPSAlgorithmPolicy`

in the registry.If

`Enabled`

is set to*1*, then FIPS is enabled.FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Update an existing node pool to enable or disable FIPS

Existing Linux node pools can be updated to enable or disable FIPS. If you're planning to migrate your node pools from non-FIPS to FIPS, first validate that your application is working properly in a test environment before migrating it to a production environment. Validating your application in a test environment should prevent issues caused by the FIPS kernel blocking some weak cipher or encryption algorithm, such as an MD4 algorithm that isn't FIPS compliant.

Note

When updating an existing Linux node pool to enable or disable FIPS, the node pool update moves between the fips and non-fips image. This node pool update triggers a reimage to complete the update. This can cause the node pool update to take a few minutes to complete.

### Prerequisites

Azure CLI version 2.64.0 or later. To find the version, run `az --version`

. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable FIPS on an existing node pool

Existing Linux node pools can be updated to enable FIPS. When you update an existing node pool, the node image changes from the current image to the recommended FIPS image of the same OS SKU.

Update a node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--enable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool is FIPS-enabled:`Name enableFips --------- ------------ np True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-np`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-np-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-np-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-np-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-np-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-np-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Disable FIPS on an existing node pool

Existing Linux node pools can be updated to disable FIPS. When updating an existing node pool, the node image changes from the current FIPS image to the recommended non-FIPS image of the same OS SKU. The node image change will occur after a reimage.

Update a Linux node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--disable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --disable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool isn't FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool isn't FIPS-enabled:`Name enableFips --------- ------------ np False nodepool1 False`


## Message of the Day

Pass the `--message-of-the-day`

flag with the location of the file to replace the Message of the Day on Linux nodes at cluster creation or node pool creation.

Create a cluster with message of the day using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


Add a node pool with message of the day using the [az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


## Next steps

To learn more about AKS security, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-monitor -->

# Monitor Azure Kubernetes Service control plane metrics (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to monitor the Azure Kubernetes Service (AKS) control plane by using control plane metrics in Azure Monitor.

AKS supports a subset of control plane metrics free through [Azure Monitor platform metrics](monitor-aks#aks-monitoring-data-metrics-logs-integrations). The control plane metrics feature gives you visibility into the availability and performance of critical control plane components like the API server, etcd, the scheduler, the autoscaler, and the controller manager in AKS. The feature is also fully compatible with the managed service for Prometheus and Azure Managed Grafana. You can use these metrics to maximize overall observability and to maintain operational excellence for your AKS cluster.

## Control plane platform metrics

AKS offers some free control plane metrics for monitoring the API server and etcd. These metrics are automatically collected for all AKS clusters at no cost. You can analyze the metrics by using the [metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics) in the Azure portal. You can also create metrics-based alerts by using the metrics data.

To see the full list of supported control plane platform metrics, see the [AKS monitoring reference](monitor-aks-reference#metrics).

## Prerequisites and limitations

- The control plane metrics (preview) feature supports only the
[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor. [Azure Private Link](/en-us/azure/azure-monitor/logs/private-link-security)isn't supported.- You can customize only the default
configmap file. No other customization is supported.`ama-metrics-settings-configmap.yaml`

- Your AKS cluster must use
[managed identity authentication](use-managed-identity).

### Install the aks-preview extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the

`aks-preview`

Azure CLI extension by using theor`az extension add`

command:`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the AzureMonitorMetricsControlPlanePreview feature flag

Register the

`AzureMonitorMetricsControlPlanePreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

It takes a few minutes for the status to show as

**Registered**.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

When the status is

**Registered**, refresh the registration of the Microsoft.ContainerService resource provider by using thecommand:`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable control plane metrics on an AKS cluster

Enable control plane metrics by using the managed service for Prometheus add-on when you create a new cluster or update an existing cluster.

Note

Unlike the metrics that are collected from cluster nodes, control plane metrics are collected by a component that isn't part of the `ama-metrics`

add-on. Enabling the `AzureMonitorMetricsControlPlanePreview`

feature flag and the managed service for Prometheus add-on ensures that control plane metrics are collected. After you enable metrics collection, it can take several minutes for the data to appear in the workspace.

### New AKS cluster

To learn how to collect managed service for Prometheus metrics from your AKS cluster, see [Enable Prometheus and Grafana for AKS clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana). For an AKS cluster, complete the steps described on the **CLI** tab.

### Existing AKS cluster

If your cluster already has the managed service for Prometheus add-on, update the cluster to ensure that it collects control plane metrics by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command:

```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Query control plane metrics

Control plane metrics are stored in an Azure Monitor workspace in the cluster's region. You can query the metrics directly in the workspace or by using the Azure Managed Grafana instance that's connected to the workspace.

In the

[Azure portal](https://portal.azure.com), go to your AKS cluster resource.On the left menu, select

**Monitor**>**Monitor Settings**.Go to the Azure Monitor workspace that is linked to the cluster.

In the Azure Monitor workspace, under

**Managed Prometheus**, query the metrics by using the Prometheus explorer.

Note

AKS provides dashboard templates to help you view and analyze your control plane telemetry data in real time. If you use Azure Managed Grafana to visualize the data, you can import the following dashboards:

## Customize control plane metrics

AKS includes a preconfigured set of metrics to collect and store for each component. Metrics for the API server and etcd are collected by default. You can customize the list of metrics that are collected by modifying the [ ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) configmap file.

Default targets include the following values:

```
controlplane-apiserver = true
controlplane-cluster-autoscaler = false
controlplace-node-auto-provisioning = false
controlplane-kube-scheduler = false
controlplane-kube-controller-manager = false
controlplane-etcd = true
```


All configmap files should be applied to the `kube-system`

namespace for any cluster.

### Customize an ingestion profile

You can customize an ingestion file for collected metrics. For more information, see [Minimal ingestion profile for control plane metrics in managed service for Prometheus](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal#minimal-ingestion-for-default-on-targets).

#### Ingest only minimal metrics from default targets

- Set
`default-targets-metrics-keep-list.minimalIngestionProfile`

to`true`

, so it ingests only the minimal set of metrics for each of the default targets:`controlplane-apiserver`

and`controlplane-etcd`

.

#### Ingest all metrics from all targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplace-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest more than minimal metrics

Using the `minimalingestionprofile`

setting helps reduce the ingestion volume of metrics. If set to `true`

, only default recording rules, default alerts, and metrics that appear in the default dashboards are collected.

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`true`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest specific metrics from specific targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets that you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file:

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

## Troubleshoot control plane metrics issues

Make sure that the `AzureMonitorMetricsControlPlanePreview`

feature flag is enabled and that the `ama-metrics`

pods are running.

Note

The [troubleshooting methods](/en-us/azure/azure-monitor/containers/prometheus-metrics-troubleshoot) for the managed service for Prometheus don't apply directly in this scenario. The components that scrape the control plane aren't included in the managed service for Prometheus add-on.

**Configmap file formatting**: Make sure that you use the correct formatting in the configmap file. Verify that the fields`default-targets-metrics-keep-list`

,`minimal-ingestion-profile`

, and`default-scrape-settings-enabled`

and other fields are correctly populated with their intended values.**Isolate the control plane from the data plane**: Start by setting some of the[node-related metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)to`true`

, and then verify that the metrics are forwarded to the workspace. Completing these steps helps you determine whether an issue is specific to scraping control plane metrics.**A change in the number of events ingested**: After you apply the changes, you can open the metrics explorer in the Azure portal. Go to the Azure Monitor overview pane for the cluster or go to the**Monitoring**section of the selected cluster. Check for an increase or a decrease in the number of events ingested per minute. This information can help you determine whether a specific metric is missing or if all metrics are missing.**A specific metric isn't exposed**: In some scenarios, a metric is documented, but it isn't exposed from the target and isn't forwarded to the Azure Monitor workspace. In this case, it's necessary to verify that other metrics are forwarded to the workspace.Note

If you want to collect the

`apiserver_request_duration_seconds`

metric or another bucket metric, you must set the entire series in the histogram family:`controlplane-apiserver = "apiserver_request_duration_seconds_bucket|apiserver_request_duration_seconds_sum|apiserver_request_duration_seconds_count"`

**No access to the Azure Monitor workspace**: When you enable the add-on, you might specify an existing workspace that you can't access. In that scenario, it appears that metrics aren't collected and forwarded. Make sure that you create a new workspace to use to collect metrics when you enable the add-on or when you create the cluster.

## Disable control plane metrics on your AKS cluster

You can disable control plane metrics at any time by disabling the managed service for Prometheus add-on and unregistering the `AzureMonitorMetricsControlPlanePreview`

feature flag.

Remove the metrics add-on that scrapes Prometheus metrics by using the

command:`az aks update`

`az aks update --disable-azure-monitor-metrics --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`

To disable scraping control plane metrics on the AKS cluster, unregister the

`AzureMonitorMetricsControlPlanePreview`

feature flag via thecommand:`az feature unregister`

`az feature unregister "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`


## Frequently asked questions

### Can I scrape control plane metrics by using self-hosted Prometheus?

No. Currently, you can't scrape control plane metrics by using self-hosted Prometheus. Self-hosted Prometheus can scrape only a single instance, depending on the load balancer, so the metrics aren't reliable. Often, multiple replicas of the control plane metrics are visible only through the managed service for Prometheus.

### Why isn't the user agent available in the control plane metrics?

In AKS, [control plane metrics](https://kubernetes.io/docs/reference/instrumentation/metrics/) don't have the user agent. The user agent is available only through the control plane logs that you access in [diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-network -->

# Best practices for network connectivity and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

As you create and manage clusters in Azure Kubernetes Service (AKS), you provide network connectivity for your nodes and applications. These network resources include IP address ranges, load balancers, and ingress controllers.

This best practices article focuses on network connectivity and security for cluster operators. In this article, you learn how to:

- Explain Azure Container Networking Interface (CNI) network mode in AKS.
- Plan for required IP addressing and connectivity.
- Distribute traffic using load balancers, ingress controllers, or a web application firewall (WAF).
- Securely connect to cluster nodes.

## Choose the appropriate network model


Best practice guidanceUse Azure CNI networking in AKS for integration with existing virtual networks or on-premises networks. This network model allows greater separation of resources and controls in an enterprise environment.


Virtual networks provide the basic connectivity for AKS nodes and customers to access your applications. There are two different ways to deploy AKS clusters into virtual networks:

**Azure CNI networking**: Deploys into a virtual network and uses the[Azure CNI](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)Kubernetes plugin. Pods receive individual IPs that can route to other network services or on-premises resources.

Azure CNI is a valid option for production deployments.

### CNI Networking

Azure CNI is a vendor-neutral protocol that lets the container runtime make requests to a network provider. It assigns IP addresses to pods and nodes, and provides IP address management (IPAM) features as you connect to existing Azure virtual networks. Each node and pod resource receives an IP address in the Azure virtual network. There's no need for extra routing to communicate with other resources or services.

Notably, Azure CNI networking for production allows for separation of control and management of resources. From a security perspective, you often want different teams to manage and secure those resources. With Azure CNI networking, you connect to existing Azure resources, on-premises resources, or other services directly via IP addresses assigned to each pod.

When you use Azure CNI networking, the virtual network resource is in a separate resource group to the AKS cluster. Delegate permissions for the AKS cluster identity to access and manage these resources. The cluster identity used by the AKS cluster must have at least [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) permissions on the subnet within your virtual network.

If you wish to define a [custom role](/en-us/azure/role-based-access-control/custom-roles) instead of using the built-in Network Contributor role, the following permissions are required:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


By default, AKS uses a managed identity for its cluster identity. However, you can use a service principal instead.

- For more information about AKS service principal delegation, see
[Delegate access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources). - For more information about managed identities, see
[Use managed identities](use-managed-identity).

As each node and pod receives its own IP address, plan out the address ranges for the AKS subnets. Keep the following criteria in mind:

- The subnet must be large enough to provide IP addresses for every node, pod, and network resource you deploy.
- With Azure CNI networking, each running node has default limits to the number of pods.

- Avoid using IP address ranges that overlap with existing network resources.
- It's necessary to allow connectivity to on-premises or peered networks in Azure.

- To handle scale-out events or cluster upgrades, you need extra IP addresses available in the assigned subnet.
- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see
[Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see

To calculate the IP address required, see [Configure Azure CNI networking in AKS](configure-azure-cni).

When creating a cluster with Azure CNI networking, you specify other address ranges for the cluster, such as the Docker bridge address, DNS service IP, and service address range. In general, make sure these address ranges don't overlap each other or any networks associated with the cluster, including any virtual networks, subnets, on-premises and peered networks.

For the specific details around limits and sizing for these address ranges, see [Configure Azure CNI networking in AKS](configure-azure-cni).

## Distribute ingress traffic


Best practice guidanceTo distribute HTTP or HTTPS traffic to your applications, use ingress resources and controllers. Compared to an Azure load balancer, ingress controllers provide extra features and can be managed as native Kubernetes resources.


While an Azure load balancer can distribute customer traffic to applications in your AKS cluster, it's limited in understanding that traffic. A load balancer resource works at *layer 4* and distributes traffic based on protocol or ports.

Most web applications using HTTP or HTTPS should use Kubernetes ingress resources and controllers, which work at *layer 7*. Ingress can distribute traffic based on the URL of the application and handle TLS/SSL termination. Ingress also reduces the number of IP addresses you expose and map.

With a load balancer, each application typically needs a public IP address assigned and mapped to the service in the AKS cluster. With an ingress resource, a single IP address can distribute traffic to multiple applications.

There are two components for ingress:

- An ingress
*resource* - An ingress
*controller*

### Ingress resource

The *ingress resource* is a YAML manifest of `kind: Ingress`

. It defines the host, certificates, and rules to route traffic to services running in your AKS cluster.

The following example YAML manifest distributes traffic for *myapp.com* to one of two services, *blogservice* or *storeservice*, and directs the customer to one service or the other based on the URL they access.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: myapp-ingress
spec:
ingressClassName: PublicIngress
tls:
- hosts:
- myapp.com
secretName: myapp-secret
rules:
- host: myapp.com
http:
paths:
- path: /blog
backend:
service:
name: blogservice
port: 80
- path: /store
backend:
service:
name: storeservice
port: 80
```


### Ingress controller

An *ingress controller* is a daemon that runs on an AKS node and watches for incoming requests. Traffic is then distributed based on the rules defined in the ingress resource. While the most common ingress controller is based on [NGINX](https://www.nginx.com/products/nginx/kubernetes-ingress-controller), AKS doesn't restrict you to a specific controller. You can use [Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), [Contour](https://github.com/heptio/contour), [HAProxy](https://www.haproxy.org), [Traefik](https://github.com/containous/traefik), etc.

Ingress controllers must be scheduled on a Linux node. Indicate that the resource should run on a Linux-based node using a node selector in your YAML manifest or Helm chart deployment. For more information, see [Use node selectors to control where pods are scheduled in AKS](concepts-clusters-workloads#node-selectors).

## Ingress with the application routing addon

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed, ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Secure traffic with a web application firewall (WAF)


Best practice guidanceTo scan incoming traffic for potential attacks, use a web application firewall (WAF) such as

[Barracuda WAF for Azure]or[Azure Application Gateway for Containers]. These more advanced network resources can also route traffic beyond just HTTP and HTTPS connections or basic TLS termination.

Typically, an ingress controller is a Kubernetes resource in your AKS cluster that distributes traffic to services and applications. The controller runs as a daemon on an AKS node, and consumes some of the node's resources, like CPU, memory, and network bandwidth. In larger environments, you may want to consider the following:

- Offload some of this traffic routing or TLS termination to a network resource outside of the AKS cluster.
- Scan incoming traffic for potential attacks.

For that extra layer of security, a web application firewall (WAF) filters the incoming traffic. With a set of rules, the Open Web Application Security Project (OWASP) watches for attacks like cross-site scripting or cookie poisoning. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) is a WAF that integrates with AKS clusters, locking in these security features before the traffic reaches your AKS cluster and applications.

Since other third-party solutions also perform these functions, you can continue to use existing investments or expertise in your preferred product.

Load balancer or ingress resources continually run in your AKS cluster and refine the traffic distribution. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) can be centrally managed as an ingress controller with a resource definition. To get started, [create an Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/quickstart-deploy-application-gateway-for-containers-alb-controller).

## Control traffic flow with network policies


Best practice guidanceUse network policies to allow or deny traffic to pods. By default, all traffic is allowed between pods within a cluster. For improved security, define rules that limit pod communication.


Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. Network policies are a cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

To use [network policies in AKS](use-network-policies), the feature can be enabled either during cluster creation or on an existing AKS cluster. If you are planning to use network policies, ensure the feature is enabled on your AKS cluster.

Note

Network policies could be used for Linux-based or Windows-based nodes and pods in AKS.

You create a network policy as a Kubernetes resource using a YAML manifest. Policies are applied to defined pods, with ingress or egress rules defining traffic flow.

The following example applies a network policy to pods with the *app: backend* label applied to them. The ingress rule only allows traffic from pods with the *app: frontend* label.

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
name: backend-policy
spec:
podSelector:
matchLabels:
app: backend
ingress:
- from:
- podSelector:
matchLabels:
app: frontend
```


To get started with policies, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Securely connect to nodes through a bastion host


Best practice guidanceDon't expose remote connectivity to your AKS nodes. Create a bastion host, or jump box, in a management virtual network. Use the bastion host to securely route traffic into your AKS cluster to remote management tasks.


You can complete most operations in AKS using the Azure management tools or through the Kubernetes API server. AKS nodes are only available on a private network and aren't connected to the public internet. To connect to nodes and provide maintenance and support, route your connections through a bastion host, or jump box. Verify this host lives in a separate, securely peered management virtual network to the AKS cluster virtual network.

You should also secure the management network for the bastion host. Use an [Azure ExpressRoute](/en-us/azure/expressroute/expressroute-introduction) or [VPN gateway](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways) to connect to an on-premises network and control access using network security groups.

## Next steps

This article focused on network connectivity and security. For more information about network basics in Kubernetes, see [Network concepts for applications in Azure Kubernetes Service (AKS)](concepts-network)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-standard-load-balancer -->

# Use multiple load balancers in Azure Kubernetes Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) normally provisions one Standard Load Balancer (SLB) for all `LoadBalancer`

Services in a cluster. Because each node NIC is limited to [ 300 inbound load‑balancing rules and 8 private‑link services](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer), large clusters or port‑heavy workloads can quickly exhaust these limits.

The **multiple SLB preview** removes that bottleneck by letting you create several SLBs inside the same cluster and shard nodes and Services across them. You define *load‑balancer configurations*, each tied to a primary agent pool and optional namespace, label, or node selectors—and AKS automatically places nodes and Services on the appropriate SLB. Outbound SNAT behavior is unchanged if `outboundType`

is `loadBalancer`

. Outbound traffic still flows through the first SLB.

Use this feature to:

- Scale beyond 300 inbound rules without adding clusters.
- Isolate tenant or workload traffic by binding a dedicated SLB to its own agent pool.
- Distribute private‑link services across multiple SLBs when you approach the per‑SLB limit.

## Prerequisites

`aks-preview`

extension 18.0.0b1 or later.- Subscription feature flag
`Microsoft.ContainerService/MultipleStandardLoadBalancersPreview`

registered. - Kubernetes version 1.28 or later.
- Cluster created with
`--load-balancer-backend-pool-type nodeIP`

or update and existing cluster using`az aks update`

.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the aks-preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension released using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `MultipleStandardLoadBalancersPreview`

feature flag

Register the

`MultipleStandardLoadBalancersPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## How AKS chooses a load balancer (node & Service placement)

AKS uses multiple inputs to determine where to place nodes and expose LoadBalancer Services. These inputs are defined in each load balancer configuration and influence which SLB is selected for each resource.

| Input type | Applies to | Description |
|---|---|---|
Primary agent pool`--primary-agent-pool-name` |
Nodes | Required. All nodes in this pool are always added to the SLB’s backend pool. Ensures each SLB has at least one healthy node. |
Node selector`--node-selector` |
Nodes | Optional. Adds any node with matching labels to the SLB, in addition to the primary pool. |
Service namespace selector`--service-namespace-selector` |
Services | Optional. Only Services in namespaces with matching labels are considered for this SLB. |
Service label selector`--service-label-selector` |
Services | Optional. Only Services with matching labels are eligible for this SLB. |
Service annotation`service.beta.kubernetes.io/azure-load-balancer-configurations` |
Services | Optional. Limits placement to one or more explicitly named SLB configurations. Without it, any matching configuration is eligible. |

Note

Selectors define eligibility. The annotation (if used) restricts the controller to a specific subset of SLBs.

### How AKS uses these inputs

The AKS control plane continuously reconciles node and Service state using the rules above:

#### Node placement

When a node is added or updated, AKS checks which SLBs it qualifies for based on primary pool and node selector.

- If multiple SLBs match, the controller picks the one with the fewest current nodes.
- The node is added to that SLB’s backend pool.

#### Service placement

When a LoadBalancer Service is created or updated:

- AKS finds SLBs whose namespace and label selectors match the Service.
- If the Service annotation is present, only those named SLBs are considered.
- SLBs that have allowServicePlacement=false or that would exceed Azure limits (300 rules or 8 private-link services) are excluded.
- Among valid options, the SLB with the fewest rules is chosen.

### externalTrafficPolicy (ETP) behavior

AKS handles Services differently depending on the value of `externalTrafficPolicy`

.

| Mode | How load balancer selection works | How backend pool membership is built | Notes |
|---|---|---|---|
Cluster (default) |
The controller follows the standard placement rules described above. A single load-balancing rule targets the shared kubernetes backend pool on the chosen SLB. |
All nodes in that SLB’s `kubernetes` pool are healthy targets. Nodes without matching Pods are removed automatically by health probes. |
Same behavior as today in single-SLB clusters. |
Local |
The controller still uses the selector-based algorithm to pick an SLB, but creates a dedicated backend pool per Service instead of using the shared pool. |
Membership is synced from the Service’s `EndpointSlice` objects, so only nodes that actually host ready Pods are added. Health probes continue to use `healthCheckNodePort` to drop unhealthy nodes. |
Guarantees client IP preservation and avoids routing through nodes that lack Pods, even when nodes are sharded across multiple SLBs. |


Why a dedicated pool for ETP Local?

In multi-SLB mode, nodes that host Pods for a given Service may reside on different SLBs from the client-facing VIP. A shared backend pool would often contain zero eligible nodes, breaking traffic. By allocating a per-Service pool and syncing it from`EndpointSlice`

, AKS ensures the Service’s SLB always points at the correct nodes.

**Impact on quotas**

- Each ETP Local Service adds one backend pool and one load-balancing rule to its SLB.
- These count toward the 300-rule limit, so monitor rule usage when you have many ETP Local Services.

**No change to outbound traffic**

Outbound SNAT still flows through the first SLB’s `aksOutboundBackendPool`

when `outboundType`

is `loadBalancer`

, independent of ETP settings.

#### Optional: Rebalancing

You can manually rebalance node distribution later using `az aks loadbalancer rebalance`

.

This design lets you define flexible, label-driven routing for both infrastructure and workloads, while AKS handles placement automatically to maintain balance and avoid quota issues.

## Add the first load balancer configuration

Add a configuration named `kubernetes`

and bind it to a *primary* agent pool that always has at least one node. Removing every configuration switches the cluster back to single‑SLB mode.

Important

To enable multiple‑SLB mode you **must** add a load‑balancer configuration named `kubernetes`

and attach it to a *primary* agent pool that always has at least one ready node.

The presence of this configuration toggles multi‑SLB support; in service selection, it has no special priority and is treated like any other load balancer configuration.

If you delete every load‑balancer configuration, the cluster automatically falls back to single‑SLB mode, which can briefly disrupt service routing or SNAT flows.

Set environment variables for use throughout this tutorial. You can replace all placeholder values with your own except

`DEFAULT_LB_NAME`

, which must remain as`kubernetes`

.`RESOURCE_GROUP="rg-aks-multislb" CLUSTER_NAME="aks-multi-slb" LOCATION="westus" DEFAULT_LB_NAME="kubernetes" PRIMARY_POOL="nodepool1"`

Create resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command.\`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME \ --load-balancer-backend-pool-type nodeIP \ --node-count 3`

Add a default load balancer using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $DEFAULT_LB_NAME \ --primary-agent-pool-name $PRIMARY_POOL \ --allow-service-placement true`


## Add additional load balancers

Create tenant‑specific configurations by specifying a different primary pool plus optional namespace, label, or node selectors.

Team 1 will run its own workloads in a separate node pool. Assign a

`tenant=team1`

label so workloads can be scheduled using selectors:`TEAM1_POOL="team1pool" TEAM1_LB_NAME="team1-lb"`

Create a second node pool for team 1 using the

command.`az aks nodepool add`

`az aks nodepool add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_POOL \ --labels tenant=team1 \ --node-count 2`

Create a load balancer for team 1 using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_LB_NAME \ --primary-agent-pool-name $TEAM1_POOL \ --service-namespace-selector "tenant=team1" \ --node-selector "tenant=team1"`

Label the target namespace (e.g.,

`team1-apps`

) to match the selector using thecommand.`az aks command invoke`

`az aks command invoke \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --command " kubectl create namespace team1-apps --dry-run=client -o yaml | kubectl apply -f - kubectl label namespace team1-apps tenant=team1 --overwrite "`

You can now list the load balancers in the cluster to see the multiple configurations using the

command.`az aks loadbalancer list`

`az aks loadbalancer list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --output table`

Example output:

`AllowServicePlacement ETag Name PrimaryAgentPoolName ProvisioningState ResourceGroup ----------------------- ------- ---------- ---------------------- ------------------- --------------- True <ETAG> kubernetes nodepool1 Succeeded rg-aks-multislb True <ETAG> team1-lb team1pool Succeeded rg-aks-multislb`


### Deploy a Service to a specific load balancer

Add the annotation `service.beta.kubernetes.io/azure-load-balancer-configurations`

with a comma‑separated list of configuration names. If the annotation is omitted, the controller chooses automatically.

```
az aks command invoke \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--command "
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
name: lb-svc-1
namespace: team1-apps
labels:
app: nginx-test
annotations:
service.beta.kubernetes.io/azure-load-balancer-configurations: \"team1-lb\"
# service.beta.kubernetes.io/azure-load-balancer-internal: "true" # If you want to create an internal load balancer.
spec:
selector:
app: nginx-test
ports:
- name: port1
port: 80
targetPort: 80
protocol: TCP
type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-test
namespace: team1-apps
labels:
app: nginx
spec:
replicas: 1
selector:
matchLabels:
app: nginx-test
template:
metadata:
labels:
app: nginx-test
spec:
containers:
- image: nginx
imagePullPolicy: Always
name: nginx
ports:
- containerPort: 80
protocol: TCP
resources:
limits:
cpu: \"150m\"
memory: \"300Mi\"
EOF
"
```


### Rebalance nodes (optional)

Run a rebalance operation after scaling if rule counts become unbalanced using the [ az aks loadbalancer rebalance](/en-us/cli/azure/aks/loadbalancer#az-aks-loadbalancer-rebalance) command. This command disrupts active flows, so schedule it during a maintenance window.

```
az aks loadbalancer rebalance --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Monitoring and troubleshooting

- Watch controller events (
`kubectl get events …`

) to confirm that Services are reconciled. - If external connectivity is blocked, open a node shell and curl the Service VIP to confirm kube‑proxy routing.

## Limitations and known issues

| Limitation | Details |
|---|---|
| Outbound SNAT | Always uses the first SLB; outbound flows aren’t sharded. |
| Backend pool type | Create or update and existing cluster to use `nodeIP` backend pools. |
| Autoscaler zeros | A primary agent pool can’t scale to 0 nodes. |
ETP `local` Rule Growth |
Each ETP `local` Service uses its own rule and backend pool, so rule counts can grow faster than with `cluster` mode. |
| Rebalance disruption | Removing a node from a backend pool drops in‑flight connections. Plan maintenance windows. |
| Configuration reload timing | After running `az aks loadbalancer` , changes may not take effect immediately. The AKS operation finishes quickly, but the cloud-controller-manager may take longer to apply updates. Wait for the `EnsuredLoadBalancer` event to confirm the changes are active. |

## Clean up resources

Delete the resource group when you’re finished to remove the cluster and load balancers using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP --yes --no-wait
```


## Next steps

The multiple SLB feature helps scale and isolate workloads at the networking layer while maintaining simplicity through Azure-managed configuration. For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-deploy-cluster -->

# Deploy and configure Microsoft Entra Workload ID on an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and configure an Azure Kubernetes Service (AKS) cluster with [Microsoft Entra Workload ID](workload-identity-overview). The steps in this article include:

- Create a new or update an existing AKS cluster using the Azure CLI with OpenID Connect (OIDC) issuer and Microsoft Entra Workload ID enabled.
- Create a workload identity and Kubernetes service account.
- Configure the managed identity for token federation.
- Deploy the workload and verify authentication with the workload identity.
- Optionally grant a pod in the cluster access to secrets in an Azure key vault.

## Prerequisites

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - This article requires version 2.47.0 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.
- Make sure that the identity that you're using to create your cluster has the appropriate minimum permissions. For more information, see
[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [Tutorial: Connect to Azure storage account in Azure Kubernetes Service (AKS) with Service Connector using Microsoft Entra Workload ID](/en-us/azure/service-connector/tutorial-python-aks-storage-workload-identity).

## Create a resource group

Create a resource group using the

command.`az group create`

`export RANDOM_ID="$(openssl rand -hex 3)" export RESOURCE_GROUP="myResourceGroup$RANDOM_ID" export LOCATION="<your-preferred-region>" az group create --name "${RESOURCE_GROUP}" --location "${LOCATION}"`


## Enable OIDC issuer and Microsoft Entra Workload ID on an AKS cluster

You can enable OIDC issuer and Microsoft Entra Workload ID on a new or existing AKS cluster.

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter to enable OIDC issuer and the`--enable-workload-identity`

parameter to enable Microsoft Entra Workload ID. The following example creates a cluster with a single node:`export CLUSTER_NAME="myAKSCluster$RANDOM_ID" az aks create \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --enable-oidc-issuer \ --enable-workload-identity \ --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Retrieve the OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the [

`az aks show`

][az-aks-show] command.`export AKS_OIDC_ISSUER="$(az aks show --name "${CLUSTER_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

The environment variable should contain the issuer URL, similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/11111111-1111-1111-1111-111111111111/`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com/{tenant_id}/{uuid}`

, where the value for`{region}`

matches the location to which the AKS cluster is deployed. The value`{uuid}`

represents the OIDC key, which is a randomly generated and immutable GUID for each cluster.

## Create a managed identity

Get your subscription ID and save it to an environment variable using the [

`az account show`

][az-account-show] command.`export SUBSCRIPTION="$(az account show --query id --output tsv)"`

Create a user-assigned managed identity using the

command.`az identity create`

`export USER_ASSIGNED_IDENTITY_NAME="myIdentity$RANDOM_ID" az identity create \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --subscription "${SUBSCRIPTION}"`

The following output example shows successful creation of a managed identity:

`{ "clientId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxxxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentityxxxxxx", "location": "eastus", "name": "myIdentityxxxxxx", "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "resourceGroup": "myResourceGroupxxxxxx", "systemData": null, "tags": {}, "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Get the client ID of the managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export USER_ASSIGNED_CLIENT_ID="$(az identity show \ --resource-group "${RESOURCE_GROUP}" \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --query 'clientId' \ --output tsv)"`


## Create a Kubernetes service account

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --name "${CLUSTER_NAME}" --resource-group "${RESOURCE_GROUP}"`

Create a Kubernetes service account and annotate it with the client ID of the managed identity by applying the following manifest using the

`kubectl apply`

command:`export SERVICE_ACCOUNT_NAME="workload-identity-sa$RANDOM_ID" export SERVICE_ACCOUNT_NAMESPACE="default" cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: "${USER_ASSIGNED_CLIENT_ID}" name: "${SERVICE_ACCOUNT_NAME}" namespace: "${SERVICE_ACCOUNT_NAMESPACE}" EOF`

The following output shows successful creation of the workload identity:

`serviceaccount/workload-identity-sa created`


## Create the federated identity credential

Create a federated identity credential between the managed identity, the service account issuer, and the subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_CREDENTIAL_NAME="myFedIdentity$RANDOM_ID" az identity federated-credential create \ --name ${FEDERATED_IDENTITY_CREDENTIAL_NAME} \ --identity-name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --issuer "${AKS_OIDC_ISSUER}" \ --subject system:serviceaccount:"${SERVICE_ACCOUNT_NAMESPACE}":"${SERVICE_ACCOUNT_NAME}" \ --audience api://AzureADTokenExchange`

Note

It takes a few seconds for the federated identity credential to propagate after it's added. If a token request is made immediately after adding the federated identity credential, the request might fail until the cache is refreshed. To avoid this issue, you can add a slight delay after adding the federated identity credential.


For more information about federated identity credentials in Microsoft Entra, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

## Create a key vault with Azure RBAC authorization

The following example shows how to use the Azure role-based access control (Azure RBAC) permission model to grant the pod access to the key vault. For more information about the Azure RBAC permission model for Azure Key Vault, see [Grant permission to applications to access an Azure key vault using Azure RBAC](/en-us/azure/key-vault/general/rbac-guide).

Create a key vault with purge protection and Azure RBAC authorization enabled using the [

`az keyvault create`

][az-keyvault-create] command. You can also use an existing key vault if it's configured for both purge protection and Azure RBAC authorization:`export KEYVAULT_NAME="keyvault-workload-id$RANDOM_ID" # Ensure the key vault name is between 3-24 characters az keyvault create \ --name "${KEYVAULT_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --enable-purge-protection \ --enable-rbac-authorization`

Get the key vault resource ID and save it to an environment variable using the [

`az keyvault show`

][az-keyvault-show] command.`export KEYVAULT_RESOURCE_ID=$(az keyvault show --resource-group "${RESOURCE_GROUP}" \ --name "${KEYVAULT_NAME}" \ --query id \ --output tsv)`


### Assign RBAC permissions for key vault management

Get the caller object ID and save it to an environment variable using the [

`az ad signed-in-user show`

][az-ad-signed-in-user-show] command.`export CALLER_OBJECT_ID=$(az ad signed-in-user show --query id -o tsv)`

Assign yourself the Azure RBAC

[Key Vault Secrets Officer](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-officer)role so that you can create a secret in the new key vault using the [`az role assignment create`

][az-role-assignment-create] command.`az role assignment create --assignee "${CALLER_OBJECT_ID}" \ --role "Key Vault Secrets Officer" \ --scope "${KEYVAULT_RESOURCE_ID}"`


### Create and configure secret access

Create a secret in the key vault using the [

`az keyvault secret set`

][az-keyvault-secret-set] command.`export KEYVAULT_SECRET_NAME="my-secret$RANDOM_ID" az keyvault secret set \ --vault-name "${KEYVAULT_NAME}" \ --name "${KEYVAULT_SECRET_NAME}" \ --value "Hello\!"`

Get the principal ID of the user-assigned managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export IDENTITY_PRINCIPAL_ID=$(az identity show \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query principalId \ --output tsv)`

Assign the

[Key Vault Secrets User](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-user)role to the user-assigned managed identity using the [`az role assignment create`

][az-role-assignment-create] command. This step gives the managed identity permission to read secrets from the key vault.`az role assignment create \ --assignee-object-id "${IDENTITY_PRINCIPAL_ID}" \ --role "Key Vault Secrets User" \ --scope "${KEYVAULT_RESOURCE_ID}" \ --assignee-principal-type ServicePrincipal`

Create an environment variable for the key vault URL using the [

`az keyvault show`

][az-keyvault-show] command:`export KEYVAULT_URL="$(az keyvault show \ --resource-group "${RESOURCE_GROUP}" \ --name ${KEYVAULT_NAME} \ --query properties.vaultUri \ --output tsv)"`


## Deploy a verification pod and test access

Deploy a pod to verify that the workload identity can access the secret in the key vault. The following example uses the

`ghcr.io/azure/azure-workload-identity/msal-go`

image, which contains a sample application that retrieves a secret from Azure Key Vault using Microsoft Entra Workload ID:`kubectl apply -f - <<EOF apiVersion: v1 kind: Pod metadata: name: sample-workload-identity-key-vault namespace: ${SERVICE_ACCOUNT_NAMESPACE} labels: azure.workload.identity/use: "true" spec: serviceAccountName: ${SERVICE_ACCOUNT_NAME} containers: - image: ghcr.io/azure/azure-workload-identity/msal-go name: oidc env: - name: KEYVAULT_URL value: ${KEYVAULT_URL} - name: SECRET_NAME value: ${KEYVAULT_SECRET_NAME} nodeSelector: kubernetes.io/os: linux EOF`

Wait for the pod to be in the

`Ready`

state using the`kubectl wait`

command.`kubectl wait --namespace ${SERVICE_ACCOUNT_NAMESPACE} --for=condition=Ready pod/sample-workload-identity-key-vault --timeout=120s`

Check that the

`SECRET_NAME`

environment variable is set in the pod using thecommand.`kubectl describe`

`kubectl describe pod sample-workload-identity-key-vault | grep "SECRET_NAME:"`

If successful, the output should be similar to the following example:

`SECRET_NAME: ${KEYVAULT_SECRET_NAME}`

Verify that pods can get a token and access the resource using the

`kubectl logs`

command.`kubectl logs sample-workload-identity-key-vault`

If successful, the output should be similar to the following example:

`I0114 10:35:09.795900 1 main.go:63] "successfully got secret" secret="Hello\\!"`

Important

Azure RBAC role assignments can take up to 10 minutes to propagate. If the pod is unable to access the secret, you might need to wait for the role assignment to propagate. For more information, see

[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#).

## Disable Microsoft Entra Workload ID on an AKS cluster

Disable Microsoft Entra Workload ID on the AKS cluster where it's been enabled and configured, update the AKS cluster using the

command with the`az aks update`

`--disable-workload-identity`

parameter.`az aks update \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --disable-workload-identity`


## Related content

In this article, you deployed a Kubernetes cluster and configured it to use Microsoft Entra Workload ID in preparation for application workloads to authenticate with that credential. Now you're ready to deploy your application and configure it to use the workload identity with the latest version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library. If you can't rewrite your application to use the latest client library version, you can [set up your application pod](workload-identity-migrate-from-pod-identity) to authenticate using managed identity with workload identity as a short-term migration solution.

The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Connect to Azure OpenAI in Foundry Models in AKS using Microsoft Entra Workload Identity](/en-us/azure/service-connector/tutorial-python-aks-openai-workload-identity) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-identity -->

# Best practices for authentication and authorization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you deploy and maintain clusters in Azure Kubernetes Service (AKS), you implement ways to manage access to resources and services. Without these controls:

- Accounts could have access to unnecessary resources and services.
- Tracking credentials used to make changes can be difficult.

In this article, we discuss what recommended practices a cluster operator can follow to manage access and identity for AKS clusters. You'll learn how to:

- Authenticate AKS cluster users with Microsoft Entra ID.
- Control access to resources with Kubernetes role-based access control (Kubernetes RBAC).
- Use Azure RBAC to granularly control access to the AKS resource, the Kubernetes API at scale, and the
`kubeconfig`

. - Use a
[workload identity](workload-identity-overview)to access Azure resources from your pods.

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

## Use Microsoft Entra ID


Best practice guidanceDeploy AKS clusters with

[Microsoft Entra integration]. Using Microsoft Entra ID centralizes the identity management layer. Any change in user account or group status is automatically updated in access to the AKS cluster. Scope users or groups to the minimum permissions amount using[Roles, ClusterRoles, or Bindings].

Your Kubernetes cluster developers and application owners need access to different resources. Kubernetes lacks an identity management solution for you to control the resources with which users can interact. Instead, you can integrate your cluster with an existing identity solution like Microsoft Entra ID, an enterprise-ready identity management solution.

With Microsoft Entra integrated clusters in AKS, you create *Roles* or *ClusterRoles* defining access permissions to resources. You then *bind* the roles to users or groups from Microsoft Entra ID. Learn more about these Kubernetes RBAC in [the next section](#use-kubernetes-role-based-access-control-kubernetes-rbac). Microsoft Entra integration and how you control access to resources can be seen in the following diagram:

- Developer authenticates with Microsoft Entra ID.
- The Microsoft Entra token issuance endpoint issues the access token.
- The developer performs an action using the Microsoft Entra token, such as
`kubectl create pod`

. - Kubernetes validates the token with Microsoft Entra ID and fetches the developer's group memberships.
- Kubernetes RBAC and cluster policies are applied.
- The developer's request is successful based on previous validation of Microsoft Entra group membership and Kubernetes RBAC and policies.

To create an AKS cluster that uses Microsoft Entra ID, see [Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id).

## Use Kubernetes role-based access control (Kubernetes RBAC)


Best practice guidanceDefine user or group permissions to cluster resources with Kubernetes RBAC. Create roles and bindings that assign the least amount of permissions required. Integrate with Microsoft Entra ID to automatically update any user status or group membership change and keep access to cluster resources current.


In Kubernetes, you provide granular access control to cluster resources. You define permissions at the cluster level, or to specific namespaces. You determine what resources can be managed and with what permissions. You then apply these roles to users or groups with a binding. For more information about *Roles*, *ClusterRoles*, and *Bindings*, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

For example, you create a role with full access to resources in the namespace named *finance-app*, as shown in the following example YAML manifest:

```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role
namespace: finance-app
rules:
- apiGroups: [""]
resources: ["*"]
verbs: ["*"]
```


You then create a *RoleBinding* and bind the Microsoft Entra user *developer1@contoso.com* to it, as shown in the following YAML manifest:

```
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role-binding
namespace: finance-app
subjects:
- kind: User
name: developer1@contoso.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: finance-app-full-access-role
apiGroup: rbac.authorization.k8s.io
```


When *developer1@contoso.com* is authenticated against the AKS cluster, they have full permissions to resources in the *finance-app* namespace. In this way, you logically separate and control access to resources. Use Kubernetes RBAC with Microsoft Entra ID-integration.

To learn how to use Microsoft Entra groups to control access to Kubernetes resources using Kubernetes RBAC, see [Control access to cluster resources using role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

## Use Azure RBAC


Best practice guidanceUse Azure RBAC to define the minimum required user and group permissions to AKS resources in one or more subscriptions.


There are two levels of access needed to fully operate an AKS cluster:

Access the AKS resource on your Azure subscription.

This access level allows you to:

- Control scaling or upgrading your cluster using the AKS APIs
- Pull your
`kubeconfig`

.

To learn how to control access to the AKS resource and the

`kubeconfig`

, see[Limit access to cluster configuration file](control-kubeconfig-access).Access to the Kubernetes API.

This access level is controlled either by:

[Kubernetes RBAC](#use-kubernetes-role-based-access-control-kubernetes-rbac)(traditionally) or- By integrating Azure RBAC with AKS for kubernetes authorization.

To learn how to granularly grant permissions to the Kubernetes API using Azure RBAC, see

[Use Azure RBAC for Kubernetes authorization](manage-azure-rbac).

## Use pod-managed identities

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

Don't use fixed credentials within pods or container images, as they are at risk of exposure or abuse. Instead, use *pod identities* to automatically request access using Microsoft Entra ID.

To access other Azure resources, like Azure Cosmos DB, Key Vault, or Blob storage, the pod needs authentication credentials. You could define authentication credentials with the container image or inject them as a Kubernetes secret. Either way, you would need to manually create and assign them. Usually, these credentials are reused across pods and aren't regularly rotated.

With pod-managed identities (preview) for Azure resources, you automatically request access to services through Microsoft Entra ID. Pod-managed identities is currently in preview for AKS. Refer to the [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (Preview)](use-azure-ad-pod-identity) documentation to get started.

Microsoft Entra pod-managed identity (preview) supports two modes of operation:

**Standard**mode: In this mode, the following 2 components are deployed to the AKS cluster:[Managed Identity Controller(MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): A Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying virtual machine scale set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the virtual machine scale set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. It redirects requests to itself and validates if the pod has access to the identity it's requesting a token for, and fetch the token from the Microsoft Entra tenant on behalf of the application.

**Managed**mode: In this mode, there's only NMI. The identity needs to be manually assigned and managed by the user. For more information, see[Pod Identity in Managed Mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/). In this mode, when you use the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command to add a pod identity to an Azure Kubernetes Service (AKS) cluster, it creates the[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)in the namespace specified by the`--namespace`

parameter, while the AKS resource provider assigns the managed identity specified by the`--identity-resource-id`

parameter to virtual machine scale set of each node pool in the AKS cluster.

Note

If you instead decide to install the Microsoft Entra pod-managed identity using the [AKS cluster add-on](use-azure-ad-pod-identity), setup uses the `managed`

mode.

The `managed`

mode provides the following advantages over the `standard`

:

- Identity assignment on the virtual machine scale set of a node pool can take up 40-60s. With cronjobs or applications that require access to the identity and can't tolerate the assignment delay, it's best to use
`managed`

mode as the identity is pre-assigned to the virtual machine scale set of the node pool. Either manually or using the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command. - In
`standard`

mode, MIC requires write permissions on the virtual machine scale set used by the AKS cluster and`Managed Identity Operator`

permission on the user-assigned managed identities. When running in`managed mode`

, since there's no MIC, the role assignments aren't required.

Instead of manually defining credentials for pods, pod-managed identities request an access token in real time, using it to access only their assigned resources. In AKS, there are two components that handle the operations to allow pods to use managed identities:

**The Node Management Identity (NMI) server**is a pod that runs as a DaemonSet on each node in the AKS cluster. The NMI server listens for pod requests to Azure services.**The Azure Resource Provider**queries the Kubernetes API server and checks for an Azure identity mapping that corresponds to a pod.

When pods request a security token from Microsoft Entra ID to access to an Azure resource, network rules redirect the traffic to the NMI server.

The NMI server:

- Identifies pods requesting access to Azure resources based on their remote address.
- Queries the Azure Resource Provider.

The Azure Resource Provider checks for Azure identity mappings in the AKS cluster.

The NMI server requests an access token from Microsoft Entra ID based on the pod's identity mapping.

Microsoft Entra ID provides access to the NMI server, which is returned to the pod.

- This access token can be used by the pod to then request access to resources in Azure.


In the following example, a developer creates a pod that uses a managed identity to request access to Azure SQL Database:

- Cluster operator creates a service account to map identities when pods request access to resources.
- The NMI server is deployed to relay any pod requests, along with the Azure Resource Provider, for access tokens to Microsoft Entra ID.
- A developer deploys a pod with a managed identity that requests an access token through the NMI server.
- The token is returned to the pod and used to access Azure SQL Database

To use Pod-managed identities, see [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity).

## Next steps

This best practices article focused on authentication and authorization for your cluster and resources. To implement some of these best practices, see the following articles:

[Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id)[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity)

For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-metrics-filtering -->

# Configure container network metrics filtering for Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure container network metrics filtering for Azure Kubernetes Service (AKS) with Cilium to optimize data collection, reduce storage costs, and focus on the metrics most relevant to your monitoring needs.

Configure container network metrics filtering enables dynamic management of Hubble metrics cardinality through Kubernetes Custom Resource Definitions (CRDs). This feature allows you to dynamically control the cardinality, dimensions, and targets of Hubble metrics without restarting Cilium agents or Prometheus servers.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is

**2.73.0**. To find your version, run`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).An AKS cluster with Cilium data plane and

[Advanced Container Networking Services](advanced-container-networking-services-overview)enabled.Kubernetes version 1.32 or later.

Container network metrics filtering works specifically with Cilium data planes.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`18.0.0b2`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az_extension_add) or

[command.](/en-us/cli/azure/extension#az_extension_update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingDynamicMetricsPreview feature flag

- First, register the AdvancedNetworkingDynamicMetricsPreview feature flag by using the
command:`az feature register`


```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- Verify successful registration by using the
command. It takes a few minutes for registration to complete.`az feature show`


```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- When the feature shows
**Registered**, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand.`az provider register`


```
az provider register --namespace Microsoft.ContainerService
```


### Create a new AKS cluster with Cilium

If you already have an existing cluster, you can skip this step.

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set environment variables
export RESOURCE_GROUP="cnm-testing-rg"
export CLUSTER_NAME="cnm-cilium-cluster"
export LOCATION="eastus2euap" # Use canary region for preview features
# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create AKS cluster with Cilium and ACNS enabled
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--location $LOCATION \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--enable-managed-identity \
--generate-ssh-keys \
--kubernetes-version 1.32
```


### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az_aks_get_credentials) command:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --overwrite-existing
```


## Configure custom resources for metrics filtering

Container network metrics filtering uses the `ContainerNetworkMetric`

Custom Resource Definition (CRD) to define filtering rules. Only one CRD can exist per cluster, and changes take approximately 30 seconds to reconcile. If the CRD is not applied, all metrics will be collected.

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: : container-network-metric # Cluster scoped
spec:
filters:
- metric: flow
includeFilters: # List of include filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
metric: dns
excludeFilters: # List of exclude filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`filters.metric` |
String | Name of the metric you would like to apply the filter on. This is mandatory. The supported values are `dns` , `flow` , `tcp` , `drop` |
Mandatory |
`includeFilters` or `excludeFilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. You must have at least one include or exclude filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . Because it's an optional parameter, if it isn't specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . Because it's an optional parameter, if it isn't specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the `ContainerNetworkMetric`

custom resource to enable log collection at the cluster:

```
kubectl apply -f <crd.yaml>
```


## Clean up and reset

To clean up filtering configuration:

```
# Delete the CRD
kubectl delete ContainerNetworkMetric container-network-metric
```


## Example filtering configuration

- Create a basic filtering configuration that focuses on DNS metrics:

```
# basic-dns-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns # Supported: dns, flow, tcp, drop
excludeFilters:
- from:
namespacedPod: ["kube-system/coredns"]
```


- Configure filtering for TCP metrics with include and exclude filters:

```
# tcp-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: tcp
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
excludeFilters:
- to:
namespacedPod: ["kube-system/metrics-server"]
```


- Configure filtering for network flow metrics:

```
# flow-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: flow
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
- to:
labelSelector:
matchLabels:
tier: "backend"
excludeFilters:
- from:
namespacedPod: ["default/test"]
```


- Configure filtering for dropped packet metrics:

```
# drop-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: drop
excludeFilters:
- from:
namespacedPod: ["kube-system/"]
```


- Configure filtering for multiple metric types in a single CRD:

```
# multi-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns
includeFilters:
- protocol: ["dns"]
excludeFilters:
- from:
namespacedPod: ["kube-system/*"]
- metric: tcp
includeFilters:
- protocol: ["tcp"]
- from:
labelSelector:
matchLabels:
environment: "production"
- metric: flow
excludeFilters:
- from:
namespacedPod: ["default/debug-*"]
- metric: drop
includeFilters:
- reason: ["Policy denied", "Invalid"]
```


## Best practices

Ensure you do not have conflicting include and exclude filter on the CRD.

Leverage Kubernetes label selectors for flexible filtering.

Always validate filtering configurations in development or staging

Regularly review filtered metrics to ensure important data isn't lost.

Remember that only one CRD can exist per cluster.


## Troubleshooting

### Common issues

**Issue**: CRD configuration not applied

**Solution**: Check that the feature flag is registered and only one CRD exists:

```
# Verify feature registration
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
# Check existing CRDs
kubectl get ContainerNetworkMetric
```


**Issue**: Metrics still showing after applying excludeFilters

**Solution**: Remember that preexisting metrics persist in Prometheus. You may need to wait for new metrics to be generated to see the filtering effects.

## Limitations

- This feature is specifically designed for Cilium data planes only
- Only one
`ContainerNetworkMetric`

CRD can exist per cluster - Preexisting metrics persist in Prometheus; new filtering rules apply to newly generated metrics
- Requires Kubernetes version 1.32 or later

## Related content

- To learn about container network metrics capabilities, see
[Container network metrics overview](container-network-observability-metrics). - To create an AKS cluster with Advanced Container Networking Services, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stateful-workload-upgrades -->

# Stateful workload upgrade patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade clusters that run databases and stateful applications without data loss by using these proven patterns.

## What this article covers

This article provides database-specific upgrade patterns for Azure Kubernetes Service (AKS) clusters with stateful workloads, such as:

- PostgreSQL Ferris wheel pattern for ~30-second downtime.
- Redis rolling replacement for zero-downtime cache upgrades.
- MongoDB step-down cascades for replica set safety.
- Emergency upgrade checklists for security responses.
- Validation and rollback procedures for data protection.

These patterns are best for use by database administrators for applications with persistent data and mission-critical stateful services.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

[Do you need an emergency upgrade?](#emergency-upgrade-checklist)[Do you need help with a PostgreSQL cluster?](#the-ferris-wheel-pattern-postgresql)[Do you need a Redis cache rolling replace?](#redis-cluster-rolling-replace)

## Choose your pattern

| Database type | Upgrade pattern | Downtime | Complexity | Best for |
|---|---|---|---|---|
| PostgreSQL |
|

[Rolling replace](#redis-cluster-rolling-replace)[Step-down cascade](#mongodb-replica-set-step-down)*(coming soon)**(coming soon)*## Emergency upgrade checklist

Do you need to upgrade now because of security issues?

Run the following commands for an immediate safety check (two minutes):

`# Verify all replicas are healthy kubectl get pods -l tier=database -o wide # Check replication lag ./scripts/check-replica-health.sh # Ensure recent backup exists kubectl get job backup-job -o jsonpath='{.status.completionTime}'`

Choose an emergency pattern (one minute):

**PostgreSQL/MySQL:**Use[Ferris wheel](#the-ferris-wheel-pattern-postgresql)(30-second downtime).**Redis/Memcached:**Use[Rolling replace](#redis-cluster-rolling-replace)(zero downtime).**MongoDB/CouchDB:**Use[Step-down cascade](#mongodb-replica-set-step-down)(10-second downtime).

Run with a safety net (15-minute to 30-minute window):

- Always test rollback procedures in advance.
- Monitor application metrics during the upgrade.
- Keep the database team on standby.


## The Ferris wheel pattern: PostgreSQL

This pattern is best for 3-node PostgreSQL clusters with primary/replica setup across availability zones.

Visual pattern:

```
Initial: [PRIMARY] [REPLICA-1] [REPLICA-2]
Step 1: [PRIMARY] [REPLICA-1] [NEW-NODE] ← Add new node
Step 2: [REPLICA-1] [NEW-NODE] [REPLICA-2] ← Promote & remove old primary
Step 3: [NEW-PRIMARY] [NEW-NODE] [REPLICA-2] ← Complete rotation
```


### Quick implementation (20 minutes)

```
# 1. Add new node to cluster
kubectl scale statefulset postgres-cluster --replicas=4
# 2. Wait for new replica to sync
kubectl wait --for=condition=ready pod postgres-cluster-3 --timeout=300s
# 3. Promote new primary and failover (30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# 4. Update service endpoint
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"app":"postgres-cluster","role":"primary","pod":"postgres-cluster-3"}}}'
# 5. Remove old primary node
kubectl delete pod postgres-cluster-0
```


**Detailed step-by-step guide**

#### Prerequisites validation

```
#!/bin/bash
# pre-upgrade-validation.sh
echo "=== PostgreSQL Cluster Health Check ==="
# Check replication status
kubectl exec postgres-primary-0 -- psql -c "SELECT * FROM pg_stat_replication;"
# Verify sync replication (must show 'sync' state)
SYNC_COUNT=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT count(*) FROM pg_stat_replication WHERE sync_state='sync';")
if [ "$SYNC_COUNT" -lt 2 ]; then
echo "ERROR: Need at least 2 synchronous replicas"
exit 1
fi
# Confirm recent backup exists
LAST_BACKUP=$(kubectl get job postgres-backup -o jsonpath='{.status.completionTime}')
echo "Last backup: $LAST_BACKUP"
# Test failover capability in staging first
echo "✅ Prerequisites validated"
```


#### Step 1: Scale up with a new node

```
# Add new node with upgraded Kubernetes version
kubectl patch statefulset postgres-cluster --patch '{
"spec": {
"replicas": 4,
"template": {
"spec": {
"nodeSelector": {
"kubernetes.io/arch": "amd64",
"aks-nodepool": "upgraded-pool"
}
}
}
}
}'
# Monitor new pod startup
kubectl get pods -l app=postgres-cluster -w
# Verify new replica joins cluster
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
```


#### Step 2: Run a controlled failover

```
#!/bin/bash
# controlled-failover.sh
echo "=== Starting Controlled Failover ==="
# Ensure minimal replication lag (< 0.1-second)
LAG=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT EXTRACT(EPOCH FROM now() - pg_last_xact_replay_timestamp());")
if (( $(echo "$LAG > 0.1" | bc -l) )); then
echo "ERROR: Replication lag too high ($LAG seconds)"
exit 1
fi
# Pause application writes (use connection pool drain)
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement max_db_connections=0"}}'
# Wait for active transactions to complete
sleep 10
# Promote new primary (this is the 30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# Update service selector to new primary
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-3"
}
}
}'
# Resume application writes
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement"}}'
echo "✅ Failover completed"
```


#### Step 3: Clean up and validate

```
# Remove old primary node
kubectl delete pod postgres-cluster-0 --force
# Scale back to 3 replicas
kubectl patch statefulset postgres-cluster --patch '{"spec":{"replicas":3}}'
# Validate cluster health
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
# Test application connectivity
kubectl run test-db-connection --image=postgres:15 --rm -it -- psql -h postgres-primary -U app_user -d app_db -c "SELECT version();"
```


### Advanced configuration

For mission-critical databases that require a <10-second downtime:

```
# Use synchronous replication with multiple standbys
# postgresql.conf
synchronous_standby_names = 'ANY 2 (standby1, standby2, standby3)'
synchronous_commit = 'remote_apply'
```


### Success validation

To validate your progress, use the following checklist:

- New primary accepts reads and writes.
- All replicas show healthy replication.
- Application reconnects automatically.
- No data loss detected.
- Backup/restore tested on new primary.

### Emergency rollback

##### For immediate issues (<2 minutes)

Redirect traffic to the previous primary:

```
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-1"
}
}
}'
```


##### For comprehensive failover recovery (5-10 minutes)

Stop writes to the current primary:

`kubectl exec postgres-primary-0 -- psql -c "SELECT pg_reload_conf();"`

Redirect service to a healthy replica:

`kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-1-0"}}}'`

Promote a replica to the new primary:

`kubectl exec postgres-replica-1-0 -- pg_ctl promote -D /var/lib/postgresql/data kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=60s`

Update connection strings:

`kubectl patch configmap postgres-config --patch '{"data":{"primary-host":"postgres-replica-1-0.postgres"}}'`

Verify that the new primary accepts writes:

`kubectl exec postgres-replica-1-0 -- psql -c "CREATE TABLE upgrade_test (id serial, timestamp timestamp default now());" kubectl exec postgres-replica-1-0 -- psql -c "INSERT INTO upgrade_test DEFAULT VALUES;"`


**Expected outcome:** Approximately 30-second downtime, zero data loss, and an upgraded node that runs the current version of Kubernetes.

#### Step 3: Upgrade Node1 (former primary)

```
#!/bin/bash
# upgrade-node1.sh
echo "=== Step 3: Upgrade Node1 (Former Primary) ==="
# Drain Node1 gracefully
kubectl drain aks-nodepool1-12345678-vmss000000 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
# Trigger node upgrade
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Monitor upgrade progress
while kubectl get node aks-nodepool1-12345678-vmss000000 -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}' | grep -q "False"; do
echo "Waiting for node upgrade to complete..."
sleep 30
done
echo "Node1 upgrade completed"
```


#### Step 4: Rejoin Node1 as a replica

```
#!/bin/bash
# rejoin-node1.sh
echo "=== Step 4: Rejoin Node1 as Replica ==="
# Wait for postgres pod to be scheduled on upgraded node
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=300s
# Reconfigure as replica pointing to new primary (Node2)
kubectl exec postgres-primary-0 -- bash -c "
echo 'standby_mode = on' >> /var/lib/postgresql/data/recovery.conf
echo 'primary_conninfo = \"host=postgres-replica-1-0.postgres port=5432\"' >> /var/lib/postgresql/data/recovery.conf
"
# Restart postgres to apply replica configuration
kubectl delete pod postgres-primary-0
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=120s
# Verify replication is working
kubectl exec postgres-replica-1-0 -- psql -c "SELECT * FROM pg_stat_replication WHERE application_name='postgres-primary-0';"
echo "Node1 successfully rejoined as replica"
```


#### Step 5: Upgrade Node3 (Replica-2)

```
#!/bin/bash
# upgrade-node3.sh
echo "=== Step 5: Upgrade Node3 (Replica-2) ==="
# Similar process for Node3
kubectl drain aks-nodepool1-12345678-vmss000002 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Wait for upgrade and pod readiness
kubectl wait --for=condition=ready pod postgres-replica-2-0 --timeout=300s
# Verify all replicas are in sync
kubectl exec postgres-replica-1-0 -- psql -c "SELECT application_name, state, sync_state FROM pg_stat_replication;"
```


#### Step 6: Final failover (Node2 → Node3)

```
#!/bin/bash
# final-failover.sh
echo "=== Step 6: Final Failover and Node2 Upgrade ==="
# Failover primary from Node2 to Node3
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-2-0"}}}'
kubectl exec postgres-replica-2-0 -- pg_ctl promote -D /var/lib/postgresql/data
# Upgrade Node2
kubectl drain aks-nodepool1-12345678-vmss000001 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Rejoin Node2 as replica
kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=300s
echo "All nodes upgraded successfully. PostgreSQL cluster operational."
```


### Validation and monitoring

```
#!/bin/bash
# post-upgrade-validation.sh
echo "=== Post-Upgrade Validation ==="
# Verify cluster topology
kubectl get pods -l app=postgres -o wide
# Check all replicas are connected
kubectl exec postgres-replica-2-0 -- psql -c "SELECT application_name, client_addr, state FROM pg_stat_replication;"
# Validate data integrity
kubectl exec postgres-replica-2-0 -- psql -c "SELECT COUNT(*) FROM upgrade_test;"
# Performance validation
kubectl exec postgres-replica-2-0 -- psql -c "EXPLAIN ANALYZE SELECT * FROM pg_stat_activity;"
echo "Upgrade validation completed successfully"
```


## Redis cluster rolling replace

In this scenario, a six-node Redis cluster (three primaries and three replicas) requires zero downtime.

### Implementation

```
#!/bin/bash
# redis-cluster-upgrade.sh
echo "=== Redis Cluster Rolling Upgrade ==="
# Get cluster topology
kubectl exec redis-0 -- redis-cli cluster nodes
# Upgrade replica nodes first (no impact to writes)
for replica in redis-1 redis-3 redis-5; do
echo "Upgrading replica: $replica"
# Remove replica from cluster temporarily
REPLICA_ID=$(kubectl exec redis-0 -- redis-cli cluster nodes | grep $replica | cut -d' ' -f1)
kubectl exec redis-0 -- redis-cli cluster forget $REPLICA_ID
# Drain and upgrade node
kubectl delete pod $replica
kubectl wait --for=condition=ready pod $replica --timeout=120s
# Rejoin cluster
kubectl exec redis-0 -- redis-cli cluster meet $(kubectl get pod $replica -o jsonpath='{.status.podIP}') 6379
echo "Replica $replica upgraded and rejoined"
done
# Upgrade master nodes with failover
for master in redis-0 redis-2 redis-4; do
echo "Upgrading master: $master"
# Trigger failover to replica
kubectl exec $master -- redis-cli cluster failover
# Wait for failover completion
sleep 10
# Upgrade the demoted master (now replica)
kubectl delete pod $master
kubectl wait --for=condition=ready pod $master --timeout=120s
echo "Master $master upgraded"
done
echo "Redis cluster upgrade completed"
```


## MongoDB replica set step-down

In this scenario, a three-member MongoDB replica set requires coordinated primary step-down.

### Implementation

```
#!/bin/bash
# MongoDB upgrade script
Echo "=== MongoDB Replica Set Upgrade ==="
# Check replica set status
kubectl exec mongo-0 --mongo --eval "rs.status()"
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

# Tutorial - Use PaaS services with an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Kubernetes, you can use PaaS services, such as [Azure Service Bus](/en-us/azure/service-bus-messaging/service-bus-messaging-overview), to develop and run your applications.

In this tutorial, you create an Azure Service Bus namespace and queue to test your application. You learn how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created a Kubernetes cluster, and deployed an application. To complete this tutorial, you need the pre-created `aks-store-quickstart.yaml`

Kubernetes manifest file. This file download was included with the application source code in a previous tutorial. Make sure you cloned the repo and changed directories into the cloned repo. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create environment variables

Create the following environment variables to use for the commands in this tutorial:

`LOC_NAME=westus2 RAND=$RANDOM RG_NAME=myResourceGroup AKS_NAME=myAKSCluster SB_NS=sb-store-demo-$RAND`


## Create Azure Service Bus namespace and queue

In previous tutorials, you used a RabbitMQ container to store orders submitted by the `order-service`

. In this tutorial, you use an Azure Service Bus namespace to provide a scoping container for the Service Bus resources within the application. You also use an Azure Service bus queue to send and receive messages between the application components. For more information on Azure Service Bus, see [Create an Azure Service Bus namespace and queue](/en-us/azure/service-bus-messaging/service-bus-quickstart-cli).

Create an Azure Service Bus namespace using the

command.`az servicebus namespace create`

`az servicebus namespace create --name $SB_NS --resource-group $RG_NAME --location $LOC_NAME`

Create an Azure Service Bus queue using the

command.`az servicebus queue create`

`az servicebus queue create --name orders --resource-group $RG_NAME --namespace-name $SB_NS`

Create an Azure Service Bus authorization rule using the

command.`az servicebus queue authorization-rule create`

`az servicebus queue authorization-rule create \ --name sender \ --namespace-name $SB_NS \ --resource-group $RG_NAME \ --queue-name orders \ --rights Send`

Get the Azure Service Bus credentials for later use by using the

and`az servicebus namespace show`

commands.`az servicebus queue authorization-rule keys list`

`az servicebus namespace show --name $SB_NS --resource-group $RG_NAME --query name -o tsv az servicebus queue authorization-rule keys list --namespace-name $SB_NS --resource-group $RG_NAME --queue-name orders --name sender --query primaryKey -o tsv`


## Update Kubernetes manifest file

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Open the

`aks-store-quickstart.yaml`

file in a text editor.Remove the existing

`rabbitmq`

StatefulSet, ConfigMap, and Service sections and replace the existing`order-service`

Deployment section with the following content:`apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: <REPLACE_WITH_YOUR_ACR_NAME>.azurecr.io/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "<REPLACE_WITH_YOUR_SB_NS_HOSTNAME>" # Example: sb-store-demo-123456.servicebus.windows.net - name: ORDER_QUEUE_PORT value: "5671" - name: ORDER_QUEUE_TRANSPORT value: "tls" - name: ORDER_QUEUE_USERNAME value: "sender" - name: ORDER_QUEUE_PASSWORD value: "<REPLACE_WITH_YOUR_SB_SENDER_PASSWORD>" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3`

Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use

[Managed Identity](use-managed-identity)to authenticate with Azure Service Bus or store your secrets in[Azure Key Vault](csi-secrets-store-driver).Save and close the updated

`aks-store-quickstart.yaml`

file.

## Deploy the updated application

Deploy the updated application using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the successfully updated resources:

`deployment.apps/order-service configured service/order-service unchanged deployment.apps/product-service unchanged service/product-service unchanged deployment.apps/store-front configured service/store-front unchanged`


## Test the application

### Place a sample order

Get the external IP address of the

`store-front`

service using the`kubectl get service`

command.`kubectl get service store-front`

Navigate to the external IP address of the

`store-front`

service in your browser using`http://<external-ip>`

.Place an order by choosing a product and selecting

**Add to cart**.Select

**Cart**to view your order, and then select**Checkout**.

### View the order in the Azure Service Bus queue

- Navigate to the Azure portal and open the Azure Service Bus namespace you created earlier.
- Under
**Entities**, select**Queues**, and then select the**orders**queue. - In the
**orders**queue, select**Service Bus Explorer**. - Select
**Peek from start**to view the order you submitted.

## Next steps

In this tutorial, you used Azure Service Bus to update and test the sample application. You learned how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

In the next tutorial, you learn how to scale an application in AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler-api-reference -->

# Vertical Pod Autoscaler API reference

This article provides the API reference for the Vertical Pod Autoscaler feature of Azure Kubernetes Service.

This reference is based on version 0.13.0 of the AKS implementation of VPA.

## VerticalPodAutoscaler

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| spec |
VerticalPodAutoscalerSpec |
The desired behavior of the Vertical Pod Autoscaler. |
| status |
VerticalPodAutoscalerStatus |
The most recently observed status of the Vertical Pod Autoscaler. |

## VerticalPodAutoscalerSpec

| Name |
Object |
Description |
| targetRef |
CrossVersionObjectReference |
Reference to the controller managing the set of pods for the autoscaler to control. For example, a Deployment or a StatefulSet. You can point a Vertical Pod Autoscaler at any controller that has a [Scale](https://v1-25.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#scalespec-v1-autoscaling) subresource. Typically, the Vertical Pod Autoscaler retrieves the pod set from the controller's ScaleStatus. |
| updatePolicy |
PodUpdatePolicy |
Specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. |
| resourcePolicy |
PodResourcePolicy |
Specifies policies for how CPU and memory requests are adjusted for individual containers. The resource policy can be used to set constraints on the recommendations for individual containers. If not specified, the autoscaler computes recommended resources for all containers in the pod, without additional constraints. |
| recommenders |
VerticalPodAutoscalerRecommenderSelector |
Recommender is responsible for generating recommendation for the VPA object. Leave empty to use the default recommender. Otherwise the list can contain exactly one entry for a user-provided alternative recommender. |

## VerticalPodAutoscalerList

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| items |
VerticalPodAutoscaler (array) |
A list of Vertical Pod Autoscaler objects. |

## PodUpdatePolicy

| Name |
Object |
Description |
| updateMode |
string |
A string that specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. Possible values are `Off` , `Initial` , `Recreate` , and `Auto` . The default is `Auto` if you don't specify a value. |
| minReplicas |
int32 |
A value representing the minimal number of replicas which need to be alive for Updater to attempt pod eviction (pending other checks like Pod Disruption Budget). Only positive values are allowed. Defaults to global `--min-replicas` flag, which is set to `2` . |

## PodResourcePolicy

| Name |
Object |
Description |
| conainerPolicies |
ContainerResourcePolicy |
An array of resource policies for individual containers. There can be at most one entry for every named container, and optionally a single wildcard entry with `containerName = '*'` , which handles all containers that do not have individual policies. |

## ContainerResourcePolicy

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the policy applies to. If not specified, the policy serves as the default policy. |
| mode |
ContainerScalingMode |
Specifies whether recommended updates are applied to the container when it is started and whether recommended updates are applied during the life of the container. Possible values are `Off` and `Auto` . The default is `Auto` if you don't specify a value. |
| minAllowed |
ResourceList |
Specifies the minimum CPU request and memory request allowed for the container. By default, there is no minimum applied. |
| maxAllowed |
ResourceList |
Specifies the maximum CPU request and memory request allowed for the container. By default, there is no maximum applied. |
| ControlledResources |
[]ResourceName |
Specifies the type of recommendations that are computed (and possibly applied) by the Vertical Pod Autoscaler. If empty, the default of [ResourceCPU, ResourceMemory] is used. |

## VerticalPodAutoscalerRecommenderSelector

| Name |
Object |
Description |
| name |
string |
A string that specifies the name of the recommender responsible for generating recommendation for this object. |

## VerticalPodAutoscalerStatus

| Name |
Object |
Description |
| recommendation |
RecommendedPodResources |
The most recently recommended CPU and memory requests. |
| conditions |
VerticalPodAutoscalerCondition |
An array that describes the current state of the Vertical Pod Autoscaler. |

## RecommendedPodResources

| Name |
Object |
Description |
| containerRecommendation |
RecommendedContainerResources |
An array of resources recommendations for individual containers. |

## RecommendedContainerResources

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the recommendation applies to. |
| target |
ResourceList |
The recommended CPU request and memory request for the container. |
| lowerBound |
ResourceList |
The minimum recommended CPU request and memory request for the container. This amount is not guaranteed to be sufficient for the application to be stable. Running with smaller CPU and memory requests is likely to have a significant impact on performance or availability. |
| upperBound |
ResourceList |
The maximum recommended CPU request and memory request for the container. CPU and memory requests higher than these values are likely to be wasted. |
| uncappedTarget |
ResourceList |
The most recent resource recommendation computed by the autoscaler, based on actual resource usage, not taking into account the **Container Resource Policy**. If actual resource usage causes the target to violate the **Container Resource Policy**, this might be different from the bounded recommendation. This field does not affect actual resource assignment. It is used only as a status indication. |

## VerticalPodAutoscalerCondition

| Name |
Object |
Description |
| type |
VerticalPodAutoscalerConditionType |
The type of condition being described. Possible values are `RecommendationProvided` , `LowConfidence` , `NoPodsMatched` , and `FetchingHistory` . |
| status |
ConditionStatus |
The status of the condition. Possible values are `True` , `False` , and `Unknown` . |
| lastTransitionTime |
Time |
The last time the condition made a transition from one status to another. |
| reason |
string |
The reason for the last transition from one status to another. |
| message |
string |
A human-readable string that gives details about the last transition from one status to another. |

## Next steps

See [Vertical Pod Autoscaler](vertical-pod-autoscaler) to understand how to improve cluster resource utilization and free up CPU and memory for other pods.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-istio-migration-guidance -->

# Migration guidance for Open Service Mesh (OSM) configurations to Istio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article aims to provide a simplistic understanding of how to identify OSM configurations and translate them to equivalent Istio configurations for migrating workloads from OSM to Istio. This by no means, is considered to be an exhaustive detailed guide.

This article provides practical guidance for mapping OSM policies to the [Istio](https://istio.io/) policies to help migrate your microservices deployments managed by OSM over to being managed by Istio. We utilize the OSM [Bookstore sample application](https://docs.openservicemesh.io/docs/getting_started/install_apps/) as a base reference for current OSM users. The following walk-through deploys the Bookstore application. The same steps are followed and explain how to apply the OSM [SMI](https://smi-spec.io/) traffic policies using the Istio equivalent.

If you are not using OSM and are new to Istio, start with [Istio's own Getting Started guide](https://istio.io/latest/docs/setup/getting-started/) to learn how to use the Istio service mesh for your applications. If you are currently using OSM, make sure you are familiar with the OSM [Bookstore sample application](https://docs.openservicemesh.io/docs/getting_started/install_apps/) walk-through on how OSM configures traffic policies. The following walk-through does not duplicate the current documentation, and reference specific topics when relevant. You should be comfortable and fully aware of the bookstore application architecture before proceeding.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI installed](/en-us/cli/azure/install-azure-cli).- The OSM AKS add-on is uninstalled from your AKS cluster
- Any existing OSM Bookstore application, including namespaces, is uninstalled and deleted from your cluster
[Install the Istio AKS service mesh add-on](istio-deploy-addon)

## Modifications needed to the OSM Sample Bookstore Application

To allow for Istio to manage the OSM bookstore application, there are a couple of changes needed in the existing manifests. Those changes are with the bookstore and the mysql services.

### Bookstore Modifications

In the OSM Bookstore walk-through, the bookstore service is deployed along with another bookstore-v2 service to demonstrate how OSM provides traffic shifting. This deployed services allowed you to split the client (`bookbuyer`

) traffic between multiple service endpoints. The first new concept to understand how Istio handles what they refer to as [Traffic Shifting](https://istio.io/latest/docs/tasks/traffic-management/traffic-shifting/).

OSM implementation of traffic shifting is based on the [SMI Traffic Split specification](https://github.com/servicemeshinterface/smi-spec/blob/main/apis/traffic-split/v1alpha4/traffic-split.md). The SMI Traffic Split specification requires the existence of multiple top-level services that are added as backends with the desired weight metric to shift client requests from one service to another. Istio accomplishes traffic shifting using a combination of a [Virtual Service](https://istio.io/latest/docs/reference/config/networking/virtual-service/) and a [Destination Rule](https://istio.io/latest/docs/reference/config/networking/destination-rule/). It is highly recommended that you familiarize yourself with both the concepts of a virtual service and destination rule.

Put simply, the Istio virtual service defines routing rules for clients that request the host (service name). Virtual Services allows for multiple versions of a deployment to be associated to one virtual service hostname for clients to target. Multiple deployments can be labeled for the same service, representing different versions of the application behind the same hostname. The Istio virtual service can then be configured to weight the request to a specific version of the service. The available versions of the service are configured to use the `subsets`

attribute in an Istio destination rule.

The modification made to the bookstore service and deployment for Istio removes the need to have an explicit second service to target, which the SMI Traffic Split needs. There's no need for another service account for the bookstore v2 service as well, since it's to be consolidated under the bookstore service. The original OSM [traffic-access-v1.yaml](https://raw.githubusercontent.com/openservicemesh/osm-docs/release-v1.2/manifests/access/traffic-access-v1.yaml) manifest modification to Istio for both the bookstore v1 and v2 are shown in the below [Create Pods, Services, and Service Accounts](#create-pods-services-and-service-accounts) section. We demonstrate how we do traffic splitting, known as traffic shifting later in the walk-through:

### MySql Modifications

Changes to the mysql stateful set are only needed in the service configuration. Under the service specification, OSM needed the `targetPort`

and `appProtocol`

attributes. These attributes are not needed for Istio. The following updated service for the mysqldb looks like:

```
apiVersion: v1
kind: Service
metadata:
name: mysqldb
labels:
app: mysqldb
service: mysqldb
spec:
ports:
- port: 3306
name: tcp
selector:
app: mysqldb
```


## Deploy the Modified Bookstore Application

Similar to the OSM Bookstore walk-through, we start with a new install of the bookstore application.

### Create the Namespaces

```
kubectl create namespace bookstore
kubectl create namespace bookbuyer
kubectl create namespace bookthief
kubectl create namespace bookwarehouse
```


### Add a namespace label for Istio sidecar injection

For OSM, using the command `osm namespace add <namespace>`

created the necessary annotations to the namespace for the OSM controller to add automatic sidecar injection. With Istio, you only need to just label a namespace to allow the Istio controller to be instructed to automatically inject the Envoy sidecar proxies.

```
kubectl label namespace bookstore istio-injection=enabled
kubectl label namespace bookbuyer istio-injection=enabled
kubectl label namespace bookthief istio-injection=enabled
kubectl label namespace bookwarehouse istio-injection=enabled
```


### Deploy the Istio Virtual Service and Destination Rule for Bookstore

As mentioned earlier in the Bookstore Modification section, Istio handles traffic shifting utilizing a VirtualService weight attribute we configure later in the walk-through. We deploy the virtual service and destination rule for the bookstore service. We deploy only the bookstore version 1 even though the bookstore version 2 is deployed. The Istio virtual service is only supplying a route to the version 1 of bookstore. Different from how OSM handles traffic shifting (traffic split), OSM deployed another service for the bookstore version 2 application. OSM needed to set up traffic to be split between client requests using a TrafficSplit. When using traffic shifting with Istio, we can reference shifting traffic to multiple Kubernetes application deployments (versions) labeled for the same service.

In this walk-though, the deployment of both bookstore versions (v1 & v2) is deployed at the same time. Only the version 1 is reachable due to the virtual service configuration. There is no need to deploy another service for bookstore version 2, we enable a route to the bookstore version 2 later when we update the bookstore virtual service and provide the necessary weight attribute to do traffic shifting.

```
kubectl apply -f - <<EOF
# Create bookstore virtual service
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
name: bookstore-virtualservice
namespace: bookstore
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
---
# Create bookstore destination rule
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
name: bookstore-destination
namespace: bookstore
spec:
host: bookstore
subsets:
- name: v1
labels:
app: bookstore
version: v1
- name: v2
labels:
app: bookstore
version: v2
EOF
```


### Create Pods, Services, and Service Accounts

We use a single manifest file that contains the modifications discussed earlier in the walk-through to deploy the `bookbuyer`

, `bookthief`

, `bookstore`

, `bookwarehouse`

, and `mysql`

applications.

```
kubectl apply -f - <<EOF
##################################################################################################
# bookbuyer service
##################################################################################################
---
# Create bookbuyer Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookbuyer
namespace: bookbuyer
---
# Create bookbuyer Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookbuyer
namespace: bookbuyer
spec:
replicas: 1
selector:
matchLabels:
app: bookbuyer
version: v1
template:
metadata:
labels:
app: bookbuyer
version: v1
spec:
serviceAccountName: bookbuyer
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookbuyer
image: openservicemesh/bookbuyer:latest-main
imagePullPolicy: Always
command: ["/bookbuyer"]
env:
- name: "BOOKSTORE_NAMESPACE"
value: bookstore
- name: "BOOKSTORE_SVC"
value: bookstore
---
##################################################################################################
# bookthief service
##################################################################################################
---
# Create bookthief ServiceAccount
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookthief
namespace: bookthief
---
# Create bookthief Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookthief
namespace: bookthief
spec:
replicas: 1
selector:
matchLabels:
app: bookthief
template:
metadata:
labels:
app: bookthief
version: v1
spec:
serviceAccountName: bookthief
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookthief
image: openservicemesh/bookthief:latest-main
imagePullPolicy: Always
command: ["/bookthief"]
env:
- name: "BOOKSTORE_NAMESPACE"
value: bookstore
- name: "BOOKSTORE_SVC"
value: bookstore
- name: "BOOKTHIEF_EXPECTED_RESPONSE_CODE"
value: "503"
---
##################################################################################################
# bookstore service version 1 & 2
##################################################################################################
---
# Create bookstore Service
apiVersion: v1
kind: Service
metadata:
name: bookstore
namespace: bookstore
labels:
app: bookstore
spec:
ports:
- port: 14001
name: bookstore-port
selector:
app: bookstore
---
# Create bookstore Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookstore
namespace: bookstore
---
# Create bookstore-v1 Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookstore-v1
namespace: bookstore
spec:
replicas: 1
selector:
matchLabels:
app: bookstore
version: v1
template:
metadata:
labels:
app: bookstore
version: v1
spec:
serviceAccountName: bookstore
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookstore
image: openservicemesh/bookstore:latest-main
imagePullPolicy: Always
ports:
- containerPort: 14001
name: web
command: ["/bookstore"]
args: ["--port", "14001"]
env:
- name: BOOKWAREHOUSE_NAMESPACE
value: bookwarehouse
- name: IDENTITY
value: bookstore-v1
---
# Create bookstore-v2 Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookstore-v2
namespace: bookstore
spec:
replicas: 1
selector:
matchLabels:
app: bookstore
version: v2
template:
metadata:
labels:
app: bookstore
version: v2
spec:
serviceAccountName: bookstore
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookstore
image: openservicemesh/bookstore:latest-main
imagePullPolicy: Always
ports:
- containerPort: 14001
name: web
command: ["/bookstore"]
args: ["--port", "14001"]
env:
- name: BOOKWAREHOUSE_NAMESPACE
value: bookwarehouse
- name: IDENTITY
value: bookstore-v2
---
##################################################################################################
# bookwarehouse service
##################################################################################################
---
# Create bookwarehouse Service Account
apiVersion: v1
kind: ServiceAccount
metadata:
name: bookwarehouse
namespace: bookwarehouse
---
# Create bookwarehouse Service
apiVersion: v1
kind: Service
metadata:
name: bookwarehouse
namespace: bookwarehouse
labels:
app: bookwarehouse
spec:
ports:
- port: 14001
name: bookwarehouse-port
selector:
app: bookwarehouse
---
# Create bookwarehouse Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
name: bookwarehouse
namespace: bookwarehouse
spec:
replicas: 1
selector:
matchLabels:
app: bookwarehouse
template:
metadata:
labels:
app: bookwarehouse
version: v1
spec:
serviceAccountName: bookwarehouse
nodeSelector:
kubernetes.io/arch: amd64
kubernetes.io/os: linux
containers:
- name: bookwarehouse
image: openservicemesh/bookwarehouse:latest-main
imagePullPolicy: Always
command: ["/bookwarehouse"]
##################################################################################################
# mysql service
##################################################################################################
---
apiVersion: v1
kind: ServiceAccount
metadata:
name: mysql
namespace: bookwarehouse
---
apiVersion: v1
kind: Service
metadata:
name: mysqldb
labels:
app: mysqldb
service: mysqldb
spec:
ports:
- port: 3306
name: tcp
selector:
app: mysqldb
---
apiVersion: apps/v1
kind: StatefulSet
metadata:
name: mysql
namespace: bookwarehouse
spec:
serviceName: mysql
replicas: 1
selector:
matchLabels:
app: mysql
template:
metadata:
labels:
app: mysql
spec:
serviceAccountName: mysql
nodeSelector:
kubernetes.io/os: linux
containers:
- image: mysql:5.6
name: mysql
env:
- name: MYSQL_ROOT_PASSWORD
value: mypassword
- name: MYSQL_DATABASE
value: booksdemo
ports:
- containerPort: 3306
name: mysql
volumeMounts:
- mountPath: /mysql-data
name: data
readinessProbe:
tcpSocket:
port: 3306
initialDelaySeconds: 15
periodSeconds: 10
volumes:
- name: data
emptyDir: {}
volumeClaimTemplates:
- metadata:
name: data
spec:
accessModes: [ "ReadWriteOnce" ]
resources:
requests:
storage: 250M
EOF
```


To view these resources on your cluster, run the following commands:

```
kubectl get pods,deployments,serviceaccounts -n bookbuyer
kubectl get pods,deployments,serviceaccounts -n bookthief
kubectl get pods,deployments,serviceaccounts,services,endpoints -n bookstore
kubectl get pods,deployments,serviceaccounts,services,endpoints -n bookwarehouse
```


### View the Application UIs

Similar to the original OSM walk-through, if you have the OSM repo cloned you can utilize the port forwarding scripts to view the UIs of each application [here](https://release-v1-2.docs.openservicemesh.io/docs/getting_started/install_apps/#view-the-application-uis). For now, we are only concerned to view the `bookbuyer`

and `bookthief`

UI.

```
cp .env.example .env
bash <<EOF
./scripts/port-forward-bookbuyer-ui.sh &
./scripts/port-forward-bookthief-ui.sh &
wait
EOF
```


In a browser, open up the following urls:

http://localhost:8080 - bookbuyer

http://localhost:8083 - bookthief

## Configure Istio's Traffic Policies

To maintain continuity with the original OSM Bookstore walk-through for the translation to Istio, we discuss [OSM's Permissive Traffic Policy Mode](https://release-v1-2.docs.openservicemesh.io/docs/getting_started/traffic_policies/#permissive-traffic-policy-mode). OSM's permissive traffic policy mode was a concept of allowing or denying traffic in the mesh without any specific [SMI Traffic Access Control rule](https://github.com/servicemeshinterface/smi-spec/blob/main/apis/traffic-access/v1alpha3/traffic-access.md) deployed. The permissive traffic mode configuration existed to allow users to onboard applications into the mesh, while gaining mTLS encryption, without requiring explicit rules to allow applications in the mesh to communicate. The permissive traffic mode feature was to avoid breaking the communications of your application as soon as OSM managed it, and provide time to define your rules while ensuring that application communications was mTLS encrypted. This setting could be set to `true`

or `false`

via OSM's MeshConfig.

Istio handles mTLS enforcement differently. Different from OSM, Istio's permissive mode automatically configures sidecar proxies to use mTLS but allow the service to accept both plaintext and mTLS traffic. The equivalent to OSM's permissive mode configuration is to utilize Istio's `PeerAuthentication`

settings. `PeerAuthentication`

can be done granularly at the namespace or for the entire mesh. For more information on Istio's enforcement of mTLS, read the [Istio Mutual TLS Migration article](https://istio.io/latest/docs/tasks/security/authentication/mtls-migration/).

### Enforce Istio Strict Mode on Bookstore Namespaces

It is important to remember, just like OSM's permissive mode, Istio's `PeerAuthentication`

configuration is only related to the use of mTLS enforcement. Actual layer-7 policies, much like those used in OSM's HTTPRouteGroups, is handled using Istio's AuthorizationPolicy configurations you see later in the walk-through.

We granularly put the `bookbuyer`

, `bookthief`

, `bookstore`

, and `bookwarehouse`

namespaces in Istio's mTLS strict mode.

```
kubectl apply -f - <<EOF
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookbuyer
namespace: bookbuyer
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookthief
namespace: bookthief
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookstore
namespace: bookstore
spec:
mtls:
mode: STRICT
---
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
name: bookwarehouse
namespace: bookwarehouse
spec:
mtls:
mode: STRICT
EOF
```


### Deploy Istio Access Control Policies

Similar to OSM's [SMI Traffic Target](https://github.com/servicemeshinterface/smi-spec/blob/v0.6.0/apis/traffic-access/v1alpha2/traffic-access.md) and [SMI Traffic Specs](https://github.com/servicemeshinterface/smi-spec/blob/v0.6.0/apis/traffic-specs/v1alpha4/traffic-specs.md) resources to define access control and routing policies for the applications to communicate, Istio accomplishes these similar fine-grain controls by using `AuthorizationPolicy`

configurations.

Let's walk through translating the bookstore TrafficTarget policy, which specifically allows the `bookbuyer`

to communicate to it, with only certain layer-7 path, headers, and methods. The following is a portion of the [traffic-access-v1.yaml](https://raw.githubusercontent.com/openservicemesh/osm-docs/release-v1.2/manifests/access/traffic-access-v1.yaml) manifest.

```
kind: TrafficTarget
apiVersion: access.smi-spec.io/v1alpha3
metadata:
name: bookstore
namespace: bookstore
spec:
destination:
kind: ServiceAccount
name: bookstore
namespace: bookstore
rules:
- kind: HTTPRouteGroup
name: bookstore-service-routes
matches:
- buy-a-book
- books-bought
sources:
- kind: ServiceAccount
name: bookbuyer
namespace: bookbuyer
---
apiVersion: specs.smi-spec.io/v1alpha4
kind: HTTPRouteGroup
metadata:
name: bookstore-service-routes
namespace: bookstore
spec:
matches:
- name: books-bought
pathRegex: /books-bought
methods:
- GET
headers:
- "user-agent": ".*-http-client/*.*"
- "client-app": "bookbuyer"
- name: buy-a-book
pathRegex: ".*a-book.*new"
methods:
- GET
```


If you notice under the TrafficTarget policy, in the spec is where you can explicitly define what source service can communicate with a destination service. We can see that we are allowing the source `bookbuyer`

to be authorized to communicate to the destination bookstore. If we translate the service-to-service authorization from an OSM `TrafficTarget`

configuration to an Istio `AuthorizationPolicy`

, it looks like this below:

```
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: bookstore
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
```


In the Istio's `AuthorizationPolicy`

, you notice how the OSM TrafficTarget policy destination service is mapped to the selector label match and the namespace the service resides in. The source service is shown under the rules section where there is a source/principles attribute that maps to the service account name for the `bookbuyer`

service.

In addition to just the source/destination configuration in the OSM TrafficTarget, OSM binds the use of an HTTPRouteGroup to further define the layer-7 authorization the source has access to. We can see in just the portion of the HTTPRouteGroup below. There are two `matches`

for the allowed source service.

```
apiVersion: specs.smi-spec.io/v1alpha4
kind: HTTPRouteGroup
metadata:
name: bookstore-service-routes
namespace: bookstore
spec:
matches:
- name: books-bought
pathRegex: /books-bought
methods:
- GET
headers:
- "user-agent": ".*-http-client/*.*"
- "client-app": "bookbuyer"
- name: buy-a-book
pathRegex: ".*a-book.*new"
methods:
- GET
```


There is a `match`

named `books-bought`

that allows the source to access path `/books-bought`

using a `GET`

method with host header user-agent and client-app information, and a `buy-a-book`

match that uses a regex express for a path containing `.*a-book.*new`

using a `GET`

method.

We can define these OSM HTTPRouteGroup configurations in the rules section of the Istio `AuthorizationPolicy`

shown below:

```
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
- source:
namespaces: ["bookbuyer"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
```


We can now deploy the OSM migrated traffic-access-v1.yaml manifest as understood by Istio below. There is not an `AuthorizationPolicy`

for the bookthief, so the bookthief UI should stop incrementing books from bookstore v1:

```
kubectl apply -f - <<EOF
##################################################################################################
# bookstore policy
##################################################################################################
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer"]
- source:
namespaces: ["bookbuyer"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
---
##################################################################################################
# bookwarehouse policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "bookwarehouse"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: bookwarehouse
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookstore/sa/bookstore"]
- source:
namespaces: ["bookstore"]
to:
- operation:
methods: ["POST"]
---
##################################################################################################
# mysql policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "mysql"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: mysql
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookwarehouse/sa/bookwarehouse"]
- source:
namespaces: ["bookwarehouse"]
to:
- operation:
ports: ["3306"]
EOF
```


### Allowing the Bookthief Application to access Bookstore

Currently there is no `AuthorizationPolicy`

that allows for the bookthief to communicate with bookstore. We can deploy the following `AuthorizationPolicy`

to allow the bookthief to communicate to the bookstore. You notice the addition for the rule for the bookstore policy that allows the bookthief authorization.

```
kubectl apply -f - <<EOF
##################################################################################################
# bookstore policy
##################################################################################################
apiVersion: "security.istio.io/v1beta1"
kind: "AuthorizationPolicy"
metadata:
name: "bookstore"
namespace: bookstore
spec:
selector:
matchLabels:
app: bookstore
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookbuyer/sa/bookbuyer", "cluster.local/ns/bookthief/sa/bookthief"]
- source:
namespaces: ["bookbuyer", "bookthief"]
to:
- operation:
methods: ["GET"]
paths: ["*/books-bought", "*/buy-a-book/new"]
- when:
- key: request.headers[User-Agent]
values: ["*-http-client/*"]
- key: request.headers[Client-App]
values: ["bookbuyer"]
---
##################################################################################################
# bookwarehouse policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "bookwarehouse"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: bookwarehouse
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookstore/sa/bookstore"]
- source:
namespaces: ["bookstore"]
to:
- operation:
methods: ["POST"]
---
##################################################################################################
# mysql policy
##################################################################################################
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
name: "mysql"
namespace: bookwarehouse
spec:
selector:
matchLabels:
app: mysql
action: ALLOW
rules:
- from:
- source:
principals: ["cluster.local/ns/bookwarehouse/sa/bookwarehouse"]
- source:
namespaces: ["bookwarehouse"]
to:
- operation:
ports: ["3306"]
EOF
```


The bookthief UI should now be incrementing books from bookstore v1.

## Configure Traffic Shifting between two Service Versions

To demonstrate how to balance traffic between two versions of a Kubernetes service, known as traffic shifting in Istio. As you recall in a previous section, OSM implementation of traffic shifting relied on two distinct services being deployed and adding those service names to the backend configuration of the `TrafficTarget`

policy. This deployment architecture is not needed for how Istio implements traffic shifting. With Istio, we can create multiple deployments that represent each version of the service application and shift traffic to those specific versions via the Istio `virtualservice`

configuration.

The currently deployed `virtualservice`

only has a route rule to the v1 version of the bookstore shown below:

```
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
```


We update the `virtualservice`

to shift 100% of the weight to the v2 version of the bookstore.

```
kubectl apply -f - <<EOF
# Create bookstore virtual service
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
name: bookstore-virtualservice
namespace: bookstore
spec:
hosts:
- bookstore
http:
- route:
- destination:
host: bookstore
subset: v1
weight: 0
- destination:
host: bookstore
subset: v2
weight: 100
EOF
```


You should now see both the `bookbuyer`

and `bookthief`

UI incrementing for the `bookstore`

v2 service only. You can continue to experiment by changing the `weigth`

attribute to shift traffic between the two `bookstore`

versions.

## Summary

We hope this walk-through provided the necessary guidance on how to migrate your current OSM policies to Istio policies. Take time and review the [Istio Concepts](https://istio.io/latest/docs/concepts/) and walking through [Istio's own Getting Started guide](https://istio.io/latest/docs/setup/getting-started/) to learn how to use the Istio service mesh to manage your applications.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-how-to -->

# Set up Container Network Observability for Azure Kubernetes Service (AKS) - Azure managed Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Container Network Observability for Azure Kubernetes Service (AKS) using Managed Prometheus and Grafana and BYO Prometheus and Grafana and to visualize the scraped metrics

You can use Container Network Observability to collect data about the network traffic of your AKS clusters. It enables a centralized platform for monitoring application and network health. Currently, metrics are stored in Prometheus and Grafana can be used to visualize them. Container Network Observability also offers the ability to enable Hubble. These capabilities are supported for both Cilium and non-Cilium clusters.

Container Network Observability is one of the features of Advanced Container Networking Services. For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see [What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview)

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- The minimum version of Azure CLI required for the steps in this article is 2.56.0. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.29 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Once you have Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Azure managed Prometheus and Grafana

Skip this Section if using BYO Prometheus and Grafana

Use the following example to install and enable Prometheus and Grafana for your AKS cluster.

### Create Azure Monitor resource

```
#Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export AZURE_MONITOR_NAME="<azure-monitor-name>"
# Create Azure monitor resource
az resource create \
--resource-group $RESOURCE_GROUP \
--namespace microsoft.monitor \
--resource-type accounts \
--name $AZURE_MONITOR_NAME \
--location eastus \
--properties '{}'
```


### Create Azure Managed Grafana instance

Use [az grafana create](/en-us/cli/azure/grafana#az-grafana-create) to create a Grafana instance. The name of the Grafana instance must be unique.

```
# Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export GRAFANA_NAME="<grafana-name>"
# Create Grafana instance
az grafana create \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP
```


### Place the Azure Managed Grafana and Azure Monitor resource IDs in variables

Use [az grafana show](/en-us/cli/azure/grafana#az-grafana-show) to place the Grafana resource ID in a variable. Use [az resource show](/en-us/cli/azure/resource#az-resource-show) to place the Azure Monitor resource ID in a variable. Replace **myGrafana** with the name of your Grafana instance.

```
grafanaId=$(az grafana show \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP \
--query id \
--output tsv)
azuremonitorId=$(az resource show \
--resource-group $RESOURCE_GROUP \
--name $AZURE_MONITOR_NAME \
--resource-type "Microsoft.Monitor/accounts" \
--query id \
--output tsv)
```


### Link Azure Monitor and Azure Managed Grafana to the AKS cluster

Use [az aks update](/en-us/cli/azure/aks#az-aks-update) to link the Azure Monitor and Grafana resources to your AKS cluster.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--enable-azure-monitor-metrics \
--azure-monitor-workspace-resource-id $azuremonitorId \
--grafana-resource-id $grafanaId
```


## Visualization

### Visualization using Azure Managed Grafana

Skip this step if using BYO Grafana

Note

The `hubble_flows_processed_total`

metric isn't scraped by default due to high metric cardinality in large scale clusters.
Because of this, the *Pods Flows* dashboards have panels with missing data. To enable this metric and populate the missing data, you need to modify the ama-metrics-settings-configmap. Specifically, update the default-targets-metrics-keep-list section. Follow the below steps to update the configmap:

- Get the latest ama-metrics-settings-configmap.(
[https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml)) - Locate the networkobservabilityHubble = ""
- Change it to networkobservabilityHubble = "hubble.*"
- Now the Pod flow metrics should populate.

To learn more about what minimal ingestion, see the [Minimal Ingestion Documentation](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Make sure the Azure Monitor pods are running using the

`kubectl get pods`

command.`kubectl get pods -o wide -n kube-system | grep ama-`

Your output should look similar to the following example output:

`ama-metrics-5bc6c6d948-zkgc9 2/2 Running 0 (21h ago) 26h ama-metrics-ksm-556d86b5dc-2ndkv 1/1 Running 0 (26h ago) 26h ama-metrics-node-lbwcj 2/2 Running 0 (21h ago) 26h ama-metrics-node-rzkzn 2/2 Running 0 (21h ago) 26h ama-metrics-win-node-gqnkw 2/2 Running 0 (26h ago) 26h ama-metrics-win-node-tkrm8 2/2 Running 0 (26h ago) 26h`

We have created sample dashboards. They can be found under the

**Dashboards > Azure Managed Prometheus**folder. They have names like**"Kubernetes / Networking /**. The suite of dashboards includes:`<name>`

"**Clusters:**shows Node-level metrics for your clusters.**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS).**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace).**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet).


### Visualization using BYO Grafana

Skip this step if using Azure managed Grafana

Add the following scrape job to your existing Prometheus configuration and restart your Prometheus server:

`- job_name: networkobservability-hubble kubernetes_sd_configs: - role: pod relabel_configs: - target_label: cluster replacement: myAKSCluster action: replace - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_pod_label_k8s_app] regex: kube-system;(retina|cilium) action: keep - source_labels: [__address__] action: replace regex: ([^:]+)(?::\d+)? replacement: $1:9965 target_label: __address__ - source_labels: [__meta_kubernetes_pod_node_name] target_label: instance action: replace metric_relabel_configs: - source_labels: [__name__] regex: '|hubble_dns_queries_total|hubble_dns_responses_total|hubble_drop_total|hubble_tcp_flags_total' # if desired, add |hubble_flows_processed_total action: keep`

In

**Targets**of Prometheus, verify the**network-obs-pods**are present.Sign in to Grafana and import following example dashboards using the following IDs:

**Clusters:**shows Node-level metrics for your clusters. (ID:[18814](https://grafana.com/grafana/dashboards/18814-kubernetes-networking-clusters/))**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.(ID:[20925](https://grafana.com/grafana/dashboards/20925-kubernetes-networking-dns-cluster/))**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS). (ID: [20926][https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/](https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/))**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).(ID:[20927](https://grafana.com/grafana/dashboards/20927-kubernetes-networking-drops-workload/)).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace). (ID:[20928](https://grafana.com/grafana/dashboards/20928-kubernetes-networking-pod-flows-namespace/))**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet). (ID:[20929](https://grafana.com/grafana/dashboards/20929-kubernetes-networking-pod-flows-workload/))

Note

- Depending on your Prometheus/Grafana instances' settings, some dashboard panels require specific tweaks to display all data.
- Cilium doesn't currently support DNS metrics/dashboards.


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable Container Network Observability for your AKS cluster.

For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).For more information on Container Network Security and its capabilities, see

[What is Container Network Security?](container-network-security-concepts).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-auto-provisioning -->

# Enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using the Azure CLI or Azure Resource Manager (ARM) templates.

If you want to create a NAP-enabled AKS cluster with a custom virtual network (VNet) and subnets, see [Create a node auto-provisioning (NAP) cluster in a custom virtual network](node-auto-provisioning-custom-vnet).

## Before you begin

Before you begin, review the [Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning) article, which details [how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work), [prerequisites](node-auto-provisioning#prerequisites) and [limitations](node-auto-provisioning#limitations-and-unsupported-features).

## Enable node auto-provisioning (NAP) on an AKS cluster

The following sections explain how to enable NAP on a new or existing AKS cluster:

Note

You can enable [control plane metrics](monitor-control-plane-metrics) to see the logs and operations from [node auto-provisioning](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Enable NAP on a new cluster

Enable node auto-provisioning on a new cluster using the

command with the`az aks create`

`--node-provisioning-mode`

flag set to`Auto`

. The following command also sets the`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Auto \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --generate-ssh-keys`


Create a file named

`nap.json`

and add the following ARM template configuration with the`properties.nodeProvisioningProfile.mode`

field set to`Auto`

, which enables NAP. (The default setting is`Manual`

.)`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Auto" } } } ] }`

Enable node auto-provisioning on a new cluster using the

command with the`az deployment group create`

`--template-file`

flag set to the path of the ARM template file.`az deployment group create --resource-group $RESOURCE_GROUP --template-file ./nap.json`


### Enable NAP on an existing cluster

Enable node auto-provisioning on an existing cluster using the

command with the`az aks update`

`--node-provisioning-mode`

flag set to`Auto`

.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --node-provisioning-mode Auto`


## Disable node auto-provisioning (NAP) on an AKS cluster

Important

You can only disable NAP on a cluster if the following conditions are met:

- There are no existing NAP nodes. You can use the
`kubectl get nodes -l karpenter.sh/nodepool`

command to check for existing NAP-managed nodes. - All existing Karpenter
have their`NodePools`

`spec.limits.cpu`

field set to`0`

. This action prevents new nodes from being created, but doesn't disrupt currently running nodes.

Set the

`spec.limits.cpu`

field to`0`

for every existing Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: limits: cpu: 0`

Important

If you don't want to ensure that every pod previously running on a NAP node is safely migrated to a non-NAP node before disabling NAP, you can skip steps 2 and 3 and instead use the

`kubectl delete node`

command for each NAP-managed node. However,**we don't recommend skipping these steps**, as it might leave some pods pending and doesn't honor Pod Disruption Budgets (PDBs).When using the

`kubectl delete node`

command, be careful to only delete NAP-managed nodes. You can identify NAP-managed nodes using the`kubectl get nodes -l karpenter.sh/nodepool`

command.Add the

`karpenter.azure.com/disable:NoSchedule`

taint to every Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: template: spec: ... taints: - key: karpenter.azure.com/disable effect: NoSchedule`

This action starts the process of migrating the workloads on the NAP-managed nodes to non-NAP nodes, honoring PDBs and disruption limits. Pods migrate to non-NAP nodes if they can fit. If there isn't enough fixed-size capacity, some node NAP-managed nodes remain.

Scale up existing fixed-size

`ManagedCluster`

`AgentPools`

or create new fixed-size`AgentPools`

to take the load from the node NAP-managed nodes. As these nodes are added to the cluster, the node NAP-managed nodes are drained, and work is migrated to the fixed-size nodes.Delete all NAP-managed nodes using the

`kubectl get nodes -l karpenter.sh/nodepool`

command. If NAP-managed nodes still exist, the cluster likely lacks fixed-size capacity. In this case, you should add more nodes so the remaining workloads can be migrated.

Update the NAP mode to

`Manual`

using theAzure CLI command with the`az aks update`

`--node-provisioning-mode`

flag set to`Manual`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Manual`


Update the

`properties.nodeProvisioningProfile.mode`

field to`Manual`

in your ARM template and redeploy it.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Manual" } } } ] }`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-ingress -->

# Ingress in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The [Kubernetes SIG Network](https://github.com/kubernetes/community/blob/master/sig-network/README.md) and the Security Response Committee [announced the upcoming retirement](https://www.kubernetes.dev/blog/2025/11/12/ingress-nginx-retirement/) of the [Ingress NGINX project](https://github.com/kubernetes/ingress-nginx/), with maintenance ending in **March 2026**. There's no immediate action required today for AKS clusters using the [Application Routing add-on with NGINX](/en-us/azure/aks/app-routing). Microsoft will provide official support for critical security patches for Application Routing add-on NGINX Ingress resources through **November 2026**.

AKS is aligning with upstream Kubernetes by moving to ** Gateway API as the long-term standard for ingress and L7 traffic management**. We recommend you start planning your migration path based on your current setup:

**Application Routing add-on users**: Production workloads remain fully supported through November 2026. AKS will continue evolving the Application Routing add-on with Gateway API alignment. You don't need to move to a different ingress product.**OSS NGINX users**have several options:- Migrate to the
[Application Routing add-on with NGINX](/en-us/azure/aks/app-routing)to benefit from official support through November 2026 while planning your long-term Gateway API migration. - Migrate to
[Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), which supports both Ingress API and Gateway API.

- Migrate to the
**Service mesh users**: If you plan to adopt a service mesh, consider the[Istio-based service mesh add-on](/en-us/azure/aks/istio-about). Use Istio Ingress today, and plan to migrate to Istio Gateway API support when it becomes GA.

Ingress in AKS is a Kubernetes resource that manages external HTTP-like traffic access to [services](concepts-network-services) within a cluster. An AKS ingress may provide services like load balancing, SSL termination, and name-based virtual hosting. For more information about Kubernetes Ingress, see the [Kubernetes Ingress documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/).

## Ingress controllers

When managing application traffic, Ingress controllers provide advanced capabilities by operating at layer 7. They can route HTTP traffic to different applications based on the inbound URL, allowing for more intelligent and flexible traffic distribution rules. For example, an ingress controller can direct traffic to different microservices depending on the URL path, enhancing the efficiency and organization of your services.

On the other hand, a LoadBalancer-type Service, when created, sets up an underlying Azure load balancer resource. This load balancer works at layer 4, distributing traffic to the pods in your Service on a specified port. However, layer 4 services are unaware of the actual applications and can't implement these types of complex routing rules.

Understanding the distinction between these two approaches helps in selecting the right tool for your traffic management needs.

## Compare ingress options

The following table lists the feature differences between the different ingress controller options:

| Feature | Application Routing addon | Application Gateway for Containers | Azure Service Mesh/Istio-based service mesh |
|---|---|---|---|
Ingress/Gateway controller |
NGINX ingress controller | Azure Application Gateway for Containers | Istio Ingress Gateway |
API |
Ingress API | Ingress API and Gateway API |
|

**Hosting****Scaling****Load balancing****SSL termination****mTLS****Static IP Address****Azure Key Vault stored SSL certificates****Azure DNS integration for DNS zone management**The following table lists the different scenarios where you might use each ingress controller:

| Ingress option | When to use |
|---|---|
Managed NGINX - Application Routing addon |
• In-cluster hosted, customizable, and scalable NGINX ingress controllers. • Basic load balancing and routing capabilities. • Internal and external load balancer configuration. • Static IP address configuration. • Integration with Azure Key Vault for certificate management. • Integration with Azure DNS Zones for public and private DNS management. • Supports the Ingress API. |
Application Gateway for Containers |
• Azure hosted ingress gateway. • Flexible deployment strategies managed by the controller or bring your own Application Gateway for Containers. • Advanced traffic management features such as automatic retries, availability zone resiliency, mutual authentication (mTLS) to backend target, traffic splitting / weighted round robin, and autoscaling. • Integration with Azure Key Vault for certificate management. • Integration with Azure DNS Zones for public and private DNS management. • Supports the Ingress and Gateway APIs. |
Istio Ingress Gateway |
• Based on Envoy, when using with Istio for a service mesh. • Advanced traffic management features such as rate limiting and circuit breaking. • Support for mTLS |

Note

Gateway API for [Istio ingress traffic](istio-deploy-ingress) is not yet supported for the Istio add-on, but is currently under active development.

## Create an Ingress resource

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Client source IP preservation

Configure your ingress controller to preserve the client source IP on requests to containers in your AKS cluster. When your ingress controller routes a client's request to a container in your AKS cluster, the original source IP of that request is unavailable to the target container. When you enable *client source IP preservation*, the source IP for the client is available in the request header under *X-Forwarded-For*.

If you're using client source IP preservation on your ingress controller, you can't use TLS pass-through. Client source IP preservation and TLS pass-through can be used with other services, such as the *LoadBalancer* type.

To learn more about client source IP preservation, see [How client source IP preservation works for LoadBalancer Services in AKS](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/how-client-source-ip-preservation-works-for-loadbalancer/ba-p/3033722#:%7E:text=Enable%20Client%20source%20IP%20preservation%201%20Edit%20loadbalancer,is%20the%20same%20as%20the%20source%20IP%20%28srjumpbox%29.).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-ip-address-planning -->

# IP address planning for your Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on IP address planning for Azure Kubernetes Service (AKS) clusters.

For specific guidance on IP address planning for individual CNI options, see the [next steps](#next-steps) section for links to plugin documentation.

## Subnet sizing

Your Azure VNet subnet must be large enough to accommodate your cluster, which depends on whether you're using an [overlay network](#overlay-networks) or a [flat network](#flat-networks).

### Overlay networks

With overlay networks, like [Azure CNI Overlay](concepts-network-azure-cni-overlay), your subnet needs to be large enough to assign IPs to your nodes. Pods are assigned IPs from a separate, private CIDR range and won't require VNet IPs. The VNet subnet you use for your cluster can be smaller than with flat networks.

It's important to ensure you allocate enough space in your private CIDR range for your pods to account for scaling. When planning your IP address range sizes, you should calculate your maximum pod count. Each node in your cluster is assigned a /24 (256 IP addresses) subnet for pods. You should plan your overlay network subnet to accommodate the maximum number of nodes you expect to run.

### Flat networks

Flat networks, like [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), require a large enough subnet to accommodate both nodes *and* pods. Since nodes and pods receive IPs from your VNet, you need to plan for the maximum number of nodes and pods you expect to run. Azure CNI Pod Subnet uses a subnet for your nodes and a separate subnet for your pods, so you need to plan for both.

## IP address sizing

### Upgrading and scaling considerations

When IP address planning for your AKS cluster, you should **consider the number of IP addresses required for upgrade and scaling operations**. If you set the IP address range to only support a fixed number of nodes, you won't be able to upgrade or scale your cluster.

When you **upgrade** your AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node, and an older node is removed from the cluster. This rolling upgrade process requires a minimum of one additional block of IP addresses to be available. Your node count is then `n + 1`

where `n`

is the number of nodes in your cluster.

When you **scale** an AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node. Your IP address range needs to take into considerations how you want to scale up the number of nodes and pods your cluster can support. A minimum of one additional node for upgrade operations or the number of nodes set by the [Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade) option should also be included. Your node count is then `n + number-of-additional-scaled-nodes-you-anticipate + max surge`

.

If you're using [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) and you expect your nodes to run the maximum number of pods and you regularly destroy and deploy pods, you should also factor in extra IP addresses per node. There can be few seconds latency required to delete a service and release its IP address for a new service to be deployed and acquire the address. The extra IP addresses account for this possibility.

The IP address plan for an AKS cluster consists of a virtual network, at least one subnet for nodes and pods, and a Kubernetes service address range.

| Azure Resource | Address Range | Limits and Sizing |
|---|---|---|
| Azure Virtual Network | Max size /8. 65,536 configured IP address limit. See
|

Use the following equation to calculate the minimum subnet size, including an extra node for upgrade operations: `(number of nodes + max surge nodes) + ((number of nodes + max surge nodes) * maximum pods per node that you configure)`


Example for a 50-node cluster: `(51) + (51 * 30 (default)) = 1,581`

(/21 or larger)

Example for a 50-node cluster, preparing to scale up an extra 10 nodes with the default max surge of 1 node: `(61) + (61 * 30 (default)) = 1,891`

(/21 or larger)

If you don't specify a maximum number of pods per node when you create your cluster, the maximum number of pods per node is set to 30. The minimum number of IP addresses required is based on that value. If you calculate your minimum IP address requirements on a different maximum value, see [Maximum pods per node](#maximum-pods-per-node) to set this value when you deploy your cluster.

*kubernetes.default.svc.cluster.local*address.## Maximum pods per node

The maximum number of pods per node in an AKS cluster is 250. The *default* maximum number of pods per node varies between *kubenet* and *Azure CNI* networking, and the method of cluster deployment.

| CNI | Default max pods | Configurable at deployment |
|---|---|---|
| Azure CNI Overlay | 250 | Yes (up to 250) |
| Azure CNI Pod subnet | 110 | Yes (up to 250) |
| Azure CNI (Legacy) | 30 | Yes (up to 250) |
| Kubenet | 110 | Yes (up to 250) |

## Configuring maximum pods per node for your clusters

You can configure the maximum number of pods per node either at cluster deployment time or as you add new node pools. You can set the maximum pods per node value as high as 250.

A minimum value for maximum pods per node is enforced to guarantee space for system pods critical to cluster health. The minimum value that can be set for maximum pods per node is 10 if and only if the configuration of each node pool has space for a minimum of 30 pods. For example, setting the maximum pods per node to the minimum of 10 requires each individual node pool to have a minimum of three nodes. This requirement applies for each new node pool created as well, so if 10 is defined as maximum pods per node each subsequent node pool added must have at least three nodes.

| Networking | Minimum | Maximum |
|---|---|---|
| Azure CNI | 10 | 250 |
| Kubenet | 10 | 250 |

Note

The minimum value in the previous table is strictly enforced by the AKS service. You cannot set a value for *maxPods* that is lower than the minimum shown, as doing so can prevent the cluster from starting.

### New clusters

You can define maximum pods per node when you create a new cluster using one of the following methods:

**Azure CLI**: Specify the`--max-pods`

argument when you deploy a cluster with thecommand.`az aks create`

**Azure Resource Manager template**: Specify the`maxPods`

property in the [ManagedClusterAgentPoolProfile] object when you deploy a cluster with an Azure Resource Manager template.**Azure portal**: Change the`Max pods per node`

field in the node pool settings when creating a cluster or adding a new node pool.

### Existing clusters

You can define maximum pods per node when you create a new node pool. If you need to increase the *maxPods* setting on an existing cluster, add a new node pool with the new desired *maxPods* count. After migrating your pods to the new pool, delete the node older pool.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-machine-learning-ops -->

# Concepts - Machine learning operations (MLOps) for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about machine learning operations (MLOps), including what types of practices and tools are involved, and how it can simplify and speed up your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What is MLOps?

Machine learning operations (MLOps) encompasses practices that facilitate collaboration between data scientists, IT operations, and business stakeholders, ensuring that machine learning models are developed, deployed, and maintained efficiently. MLOps applies DevOps principles to machine learning projects, aiming to automate and streamline the end-to-end machine learning lifecycle. This lifecycle includes training, packaging, validating, deploying, monitoring, and retraining models.

MLOps requires multiple roles and tools to work together effectively. Data scientists focus on tasks related to training the model, which is referred to as the * inner loop*. Machine learning engineers and IT operations teams handle the

*, where they apply DevOps practices to package, validate, deploy, and monitor models. When the model needs fine-tuning or retraining, the process loops back to the inner loop.*

**outer loop**### MLOps pipeline

Your MLOps pipeline may leverage various tools and microservices that are deployed sequentially or in parallel. Below are examples of key components in your pipeline that benefit from implementing the following best practices to reduce overhead and allow for faster iteration:

- Unstructured data store for new data flowing into your application
- Vector database to store and query structured, pre-processed data
- Data ingestion and indexing framework
- Vector ingestion and/or model retraining workflows
- Metrics collection and alerting tools (tracking model performance, volume of ingested data, etc.)
- Lifecycle management tools

## DevOps and MLOps

DevOps is a combination of tools and practices that enable you to create robust and reproducible applications. The goal of using DevOps is to quickly deliver value to your end users. Creating, deploying, and monitoring robust and reproducible models to deliver value to end users is the primary goal of MLOps.

There are *three* processes that are essential to MLOps:

**Machine learning workloads**for which a data scientist is responsible, including exploratory data analysis (EDA), feature engineering, and model training and tuning.**Software development practices**including planning, developing, testing, and packaging the model for deployment.**Operational aspects of deploying and maintaining the model in production**, including releasing, configuring resources, and monitoring the model.

### DevOps principles that apply to MLOps

MLOps leverages several principles from DevOps to enhance the machine learning lifecycle, such as *automation*, *continuous integration and delivery (CI/CD)*, *source control*, *Agile planning*, and *infrastructure as code (IaC)*.

#### Automation

By automating tasks, you can reduce manual errors, increase efficiency, and ensure consistency across the ML lifecycle. Automation can be applied to various stages, including data collection, model training, deployment, and monitoring. Through automation, you can also apply proactive measures in the AI pipeline to ensure data compliance with your organization's policies.

For example, your pipeline can automate:

- Model tuning/retraining at regular time intervals or when a certain amount of new data is collected in your application.
- Detection of performance degradation to kickstart fine-tuning or retraining on a different subset of data.
- Common vulnerability and exposure (CVE) scanning on base container images pulled from external container registries to ensure safe security practices.

#### Continuous integration (CI)

Continuous integration covers the *creating* and *verifying* aspects of the model development process. The goal of CI is to create the code and to verify the quality of the code and the model before deployment. This includes testing on a range of sample data sets to ensure that the model performs as expected and meets quality standards.

In MLOps, CI might involve:

- Refactoring exploratory code in Jupyter notebooks into Python or R scripts.
- Validating new input data for missing or error values.
- Unit testing and integration testing in the end-to-end pipeline.

To perform linting and unit testing, you can use automation tools like Azure Pipelines in Azure DevOps or GitHub Actions.

#### Continuous delivery (CD)

Continuous delivery involves the steps needed to safely deploy a model in production. The first step is to package and deploy the model in *pre-production environments*, such as dev and test environments. Portability of the parameters, hyperparameters, and other model artifacts is an important aspect to maintain as you promote the code through these environments. This portability is especially important when it comes to large language models (LLMs) and stable diffusion models. Once the model passes the unit tests and quality assurance (QA) tests, you can approve it for deployment in the *production environment*.

#### Source control

Source control, or *version control*, is essential for managing changes to code and models. In an ML system, this refers to data versioning, code versioning, and model versioning, which allow cross-functional teams to collaborate effectively and track changes over time. Using a Git-based source control system, like [ Azure Repos](https://azure.microsoft.com/products/devops/repos/#:%7E:text=Overview.%20Free%20private%20Git%20repositories,%20pull%20requests,%20and?msockid=182ea2d5e1ff6eb61ccbb1b8e5ff608a) in Azure DevOps or a

**GitHub repository**, enables you to programmatically maintain a history of changes, revert to previous versions, and manage branches for different experiments.

#### Agile planning

Agile planning involves isolating work into *sprints*, which are short time frames for completing specific tasks. This approach allows teams to adapt to changes quickly and deliver incremental improvements to the model. Model training can be an ongoing process, and Agile planning can help scope the project and enable better team alignment.

You can use tools like [ Azure Boards](/en-us/azure/devops/boards/get-started/what-is-azure-boards) in Azure DevOps or

**GitHub issues**to manage your Agile planning.

#### Infrastructure as code (IaC)

You use infrastructure as code to repeat and automate the infrastructure needed to train, deploy, and serve your models. In an ML system, IaC helps simplify and define the appropriate Azure resources needed for the specific job type in code, and the code is maintained in a repository. This allows you to version control your infrastructure and make changes for resource optimization, cost-effectiveness, etc. as needed.

## Next steps

Check out the following articles to learn about best practices for MLOps in your intelligent applications on AKS:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-managed-gpu-nodes -->

# Create a fully managed GPU node pool on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you run GPU workloads in Azure Kubernetes Service (AKS), you need to install and maintain several software components, including the GPU driver, Kubernetes device plugin, and GPU metrics exporter for telemetry. These components are essential for enabling GPU scheduling, container-level GPU access, observability of resource usage, and proper functioning of AKS GPU-enabled nodes. Previously, cluster operators had to either install these components manually or use open-source alternatives like the [NVIDIA GPU Operator](nvidia-gpu-operator), which can introduce complexity and operational overhead.

AKS now supports fully managed GPU nodes (preview) and installs the NVIDIA GPU driver, device plugin, and Data Center GPU Manager [(DCGM) metrics exporter](https://github.com/NVIDIA/dcgm-exporter/tree/main) by default. This feature enables one-step GPU node pool creation and makes the availability of GPU resources in AKS as simple as general purpose CPU nodes.

In this article, you learn how to provision a fully managed GPU node pool (preview) in your AKS cluster, including default installation of the NVIDIA GPU driver, device plugin, and metrics exporter.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need to
[install and upgrade to latest version of the](#install-the-aks-preview-cli-extension).`aks-preview`

extension - You need to
[register the](#register-the-managedgpuexperiencepreview-feature-flag-in-your-subscription).`ManagedGPUExperiencePreview`

feature flag in your subscription

## Limitations

- This feature currently supports
[NVIDIA GPU-enabled virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes-gpu)only. - Updating a general-purpose node pool to add a GPU VM size isn't supported on AKS.
- Windows node pools are not supported with this feature, because GPU metrics are not supported. When creating Windows GPU node pools, AKS automatically installs and manages the drivers and Directx device plugin. See
[AKS Windows GPU documentation](use-windows-gpu)for more information. - Migrating your existing
[multi-instance GPU](gpu-multi-instance)node pools to use this feature isn't supported. - In-place upgrades to use this feature on existing GPU-enabled nodes isn't supported.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

### Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `ManagedGPUExperiencePreview`

feature flag in your subscription

Register the

`ManagedGPUExperiencePreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ManagedGPUExperiencePreview`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create an AKS-managed GPU node pool (preview)

You can add a fully managed GPU node pool (preview) to an existing AKS cluster by specifying OS SKU and `--tags EnableManagedGPUExperience=true`

command. When you do this, AKS will install the GPU driver, GPU device plugin, and metrics exporter automatically.

To use the default Ubuntu operating system (OS) SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the

command with the`az aks nodepool add`

`--tags EnableManagedGPUExperience=true`

command.`az aks nodepool add \ --resource‐group MyResourceGroup \ --cluster‐name MyAKSCluster \ --name gpunp \ --node‐count 1 \ --node‐vm‐size Standard_NC6s_v3 \ --node‐taints sku=gpu:NoSchedule \ --enable‐cluster‐autoscaler \ --min‐count 1 \ --max‐count 3 \ --tags EnableManagedGPUExperience=true`

Confirm that the managed NVIDIA GPU software components are installed successfully:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \`

Your output should include the following values:

`... ... "gpuInstanceProfile": … "gpuProfile": { "driver": "Install" }, ... ...`


## Migrate existing GPU workloads to an AKS-managed GPU node pool

In-place upgrades from a standard NVIDIA GPU node pool to a fully managed NVIDIA GPU node pool (preview) on your AKS cluster isn't supported. We recommend cordoning and draining your existing GPU nodes, then redeploying your workloads to a new GPU-enabled node pool with this feature enabled. See [Resize node pools on AKS](resize-node-pool) to learn more.

## Bring your own (BYO) GPU driver

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can bypass the GPU driver installation during node pool creation. In this case, Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment. See [Skip GPU driver installation](use-nvidia-gpu#skip-gpu-driver-installation) for NVIDIA GPU-enabled nodes on AKS to learn more.

## Next steps

- Deploy a
[sample GPU workload](use-nvidia-gpu#run-a-gpu-enabled-workload)on your AKS-managed GPU-enabled nodes. - Learn about
[GPU utilization and performance metrics](monitor-gpu-metrics)from managed NVIDIA DCGM exporter on your GPU node pool.

## Related articles

- Learn about
[GPU health monitoring](gpu-health-monitoring)with Node Problem Detector (NPD) on AKS. - Run
[distributed inference on multiple AKS GPU nodes](https://blog.aks.azure.com/2025/07/08/kaito-inference-with-acstor).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-prometheus -->

# Monitor the ingress-nginx controller metrics in the application routing add-on with Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The [Kubernetes SIG Network](https://github.com/kubernetes/community/blob/master/sig-network/README.md) and the Security Response Committee [announced the upcoming retirement](https://www.kubernetes.dev/blog/2025/11/12/ingress-nginx-retirement/) of the [Ingress NGINX project](https://github.com/kubernetes/ingress-nginx/), with maintenance ending in **March 2026**. There's no immediate action required today for AKS clusters using the [Application Routing add-on with NGINX](/en-us/azure/aks/app-routing). Microsoft will provide official support for critical security patches for Application Routing add-on NGINX Ingress resources through **November 2026**.

AKS is aligning with upstream Kubernetes by moving to ** Gateway API as the long-term standard for ingress and L7 traffic management**. We recommend you start planning your migration path based on your current setup:

**Application Routing add-on users**: Production workloads remain fully supported through November 2026. AKS will continue evolving the Application Routing add-on with Gateway API alignment. You don't need to move to a different ingress product.**OSS NGINX users**have several options:- Migrate to the
[Application Routing add-on with NGINX](/en-us/azure/aks/app-routing)to benefit from official support through November 2026 while planning your long-term Gateway API migration. - Migrate to
[Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), which supports both Ingress API and Gateway API.

- Migrate to the
**Service mesh users**: If you plan to adopt a service mesh, consider the[Istio-based service mesh add-on](/en-us/azure/aks/istio-about). Use Istio Ingress today, and plan to migrate to Istio Gateway API support when it becomes GA.

The ingress-nginx controller in the application routing add-on exposes many metrics for requests, the nginx process, and the controller that can be helpful in analyzing the performance and usage of your application.

The application routing add-on exposes the Prometheus metrics endpoint at `/metrics`

on port 10254 and a private Service `nginx-metrics`

.

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster with the
[application routing add-on enabled](/en-us/azure/aks/app-routing). - A Prometheus instance, such as Azure Monitor managed service for Prometheus.

## Validating the metrics endpoint

To validate the metrics are being collected, you can set up a port forward from a local port to port 10254 on the `nginx-metrics`

service.

```
kubectl port-forward -n app-routing-system service/nginx-metrics :10254
```


```
Forwarding from 127.0.0.1:43307 -> 10254
Forwarding from [::1]:43307 -> 10254
```


Note the local port (`43307`

in this case) and open http://localhost:43307/metrics in your browser. You should see the ingress-nginx controller metrics loading.

You can now terminate the `port-forward`

process to close the forwarding.

## Configuring Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus is a fully managed Prometheus-compatible service that supports industry standard features such as PromQL, Grafana dashboards, and Prometheus alerts. This service requires configuring the metrics addon for the Azure Monitor agent, which sends data to Prometheus. If your cluster isn't configured with the add-on, you can follow this article to configure your Azure Kubernetes Service (AKS) cluster to send data to Azure Monitor managed service for Prometheus.

### Enable Service Monitor based scraping

Once your cluster is updated with the Azure Monitor agent, you need to configure the agent to enable scraping the metrics endpoint. You can [create a Pod or a Service Monitor](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-crd) to accomplish this.

The following creates a Service Monitor scrape metrics from the ingress-nginx controller deployed by the application routing add-on.

```
kubectl apply -f - <<EOF
apiVersion: azmonitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
name: nginx-monitor
namespace: app-routing-system
spec:
labelLimit: 63
labelNameLengthLimit: 511
labelValueLengthLimit: 1023
selector:
matchLabels:
app.kubernetes.io/component: ingress-controller
app.kubernetes.io/managed-by: aks-app-routing-operator
app.kubernetes.io/name: nginx
endpoints:
- port: prometheus
EOF
```


In a few minutes, the `ama-metrics`

pods in the `kube-system`

namespace should restart and pick up the new configuration.

## Review visualization of metrics in Azure Managed Grafana

Now that you have Azure Monitor managed service for Prometheus and Azure Managed Grafana configured, you should [access your Managed Grafana instance](/en-us/azure/managed-grafana/quickstart-managed-grafana-portal#access-your-managed-grafana-instance).

There are two [official ingress-nginx dashboards](https://github.com/kubernetes/ingress-nginx/tree/main/deploy/grafana/dashboards) dashboards that you can download and import into your Grafana instance:

- Ingress-nginx controller dashboard
- Request handling performance dashboard

### Ingress-nginx controller dashboard

This dashboard gives you visibility of request volume, connections, success rates, config reloads and configs out of sync. You can also use it to view the network IO pressure, memory and CPU use of the ingress controller. Finally, it also shows the P50, P95, and P99 percentile response times of your ingresses and their throughput.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/nginx.json).

### Request handling performance dashboard

This dashboard gives you visibility into the request handling performance of the different ingress upstream destinations, which are your applications' endpoints that the ingress controller is forwarding traffic to. It shows the P50, P95 and P99 percentile of total request and upstream response times. You can also view aggregates of request errors and latency. Use this dashboard to review and improve the performance and scalability of your applications.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/request-handling-performance.json).

### Importing a dashboard

To import a Grafana dashboard, expand the left menu and click on **Import** under Dashboards.

Then upload the desired dashboard file and click on **Load**.

## Next steps

- You can configure scaling your workloads using ingress metrics scraped with Prometheus using
[Kubernetes Event Driven Autoscaler (KEDA)](/en-us/azure/aks/keda-about). Learn more about[integrating KEDA with AKS](/en-us/azure/azure-monitor/essentials/integrate-keda#scalers). - Create and run a load test with
[Azure Load Testing](/en-us/azure/load-testing/quickstart-create-and-run-load-test)to test workload performance and optimize the scalability of your applications.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-ad-rbac -->

# Use Kubernetes RBAC with Microsoft Entra ID in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you sign in to an AKS cluster using a Microsoft Entra authentication token. Once authenticated, you can use the built-in Kubernetes role-based access control (RBAC) to manage access to namespaces and cluster resources based on a user's identity or group membership.

This article shows you how to:

Control access using Kubernetes RBAC in an AKS cluster based on Microsoft Entra group membership.

Create example groups and users in Microsoft Entra ID.

Create Roles and RoleBindings in an AKS cluster granting the appropriate permissions, such as to create and view resources.


## Prerequisites

You have an existing AKS cluster with Microsoft Entra integration enabled. If you need an AKS cluster with this configuration, see

[Integrate Microsoft Entra ID with AKS](managed-azure-ad).Kubernetes RBAC is enabled by default during AKS cluster creation. To upgrade an existing cluster with Microsoft Entra integration and Kubernetes RBAC, see

[Enable Microsoft Entra integration on your existing AKS cluster](managed-azure-ad#use-an-existing-cluster).Make sure that Azure CLI version 2.0.61 or later is installed and configured. To find the version, run

`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If using Terraform, install

[Terraform](/en-us/azure/developer/terraform/overview)version 2.99.0 or later.

Use the Azure portal or Azure CLI to verify Microsoft Entra integration with Kubernetes RBAC is enabled.

To verify using the Azure portal:

- Sign-in to the
[Azure portal](https://portal.azure.com)and navigate to your AKS cluster resource. - In the service menu, under
**Settings**, select**Security configuration**. - Under the
**Authentication and Authorization**section, verify the**Microsoft Entra authentication with Kubernetes RBAC**option is selected.

## Create groups in Microsoft Entra ID

This section teaches you how to create two user roles to show how Kubernetes RBAC and Microsoft Entra ID control access cluster resources. The following two example roles are:

**Application developer**- A user named
*aksdev*that's part of the*appdev*group.

- A user named
**Site reliability engineer**(SRE)- A user named
*akssre*that's part of the*opssre*group.

- A user named

In production environments, you can use existing users and groups within a Microsoft Entra tenant.

First, get the resource ID of your AKS cluster using the

command. Then, assign the resource ID to a variable named`az aks show`

*AKS_ID*so it can be referenced in other commands.`AKS_ID=$(az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query id -o tsv)`

Create the first example group in Microsoft Entra ID for the application developers using the

command. The following example creates a group named`az ad group create`

*appdev*:`APPDEV_ID=$(az ad group create --display-name appdev --mail-nickname appdev --query id -o tsv)`

Create an Azure role assignment for the

*appdev*group using thecommand. This assignment lets any member of the group use`az role assignment create`

`kubectl`

to interact with an AKS cluster by granting them the*Azure Kubernetes Service Cluster User*Role.`az role assignment create \ --assignee $APPDEV_ID \ --role "Azure Kubernetes Service Cluster User Role" \ --scope $AKS_ID`

Important

The role name you specify must exactly match the Azure role definition name, including capitalization and spacing.

Tip

If you receive an error such as

`Principal 35bfec9328bd4d8d9b54dea6dac57b82 doesn't exist in the directory a5443dcd-cd0e-494d-a387-3039b419f0d5.`

, wait a few seconds for the Microsoft Entra group object ID to propagate through the directory then try the`az role assignment create`

command again.

## Create users in Microsoft Entra ID

After you create the example Microsoft Entra ID groups for application developers and SREs, the next step is to create two corresponding user accounts. These users are used to sign in to the AKS cluster and validate the Kubernetes RBAC integration described later in this article.

Before you begin, you must set the user principal name (UPN) and password for the application developers. The UPN must include the verified domain name of your tenant. For example, an application developer user, `aksdev@contoso.com`

. In order to figure out (or set) the verified domain names in your tenant, see [Managing custom domain names in your Microsoft Entra ID](/en-us/entra/identity/users/domains-manage).

The following command prompts you for the UPN and sets it to *AAD_DEV_UPN* so it can be used in a later command:

```
echo "Please enter the UPN for application developers: " && read AAD_DEV_UPN
```


The following command prompts you for the password and sets it to *AAD_DEV_PW* for use in a later command:

```
echo "Please enter the secure password for application developers: " && read AAD_DEV_PW
```


### Create user accounts

Create the first user account in Microsoft Entra ID using the

command. The following example creates a user with the display name`az ad user create`

*AKS Dev*, the UPN, and secure password using the values in*AAD_DEV_UPN*and*AAD_DEV_PW*:`AKSDEV_ID=$(az ad user create \ --display-name "AKS Dev" \ --user-principal-name $AAD_DEV_UPN \ --password $AAD_DEV_PW \ --query id -o tsv)`

Add the user to the

*appdev*group created in the previous section using thecommand:`az ad group member add`

`az ad group member add --group appdev --member-id $AKSDEV_ID`


## Create AKS cluster resources

We have our Microsoft Entra groups, users, and Azure role assignments created. Now, you configure the AKS cluster to allow these different groups access to specific resources.

Get the cluster admin credentials using the

command. In one of the following sections, you get the regular`az aks get-credentials`

*user*cluster credentials to see the Microsoft Entra authentication flow in action.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin`

Create a namespace in the AKS cluster using the

command. The following example creates a namespace name`kubectl create namespace`

*dev*:`kubectl create namespace dev`

Note

In Kubernetes,

*Roles*define the permissions to grant, and*RoleBindings*apply them to desired users or groups. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see[Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the

**UPN**. If the user is in a different Microsoft Entra tenant, query for and use the*objectId*property instead.Create a Role for the

*dev*namespace, which grants full permissions to the namespace. In production environments, you can specify more granular permissions for different users or groups. Create a file named`role-dev-namespace.yaml`

and paste the following YAML manifest:`kind: Role apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-full-access namespace: dev rules: - apiGroups: ["", "extensions", "apps"] resources: ["*"] verbs: ["*"] - apiGroups: ["batch"] resources: - jobs - cronjobs verbs: ["*"]`

Create the Role using the

command and specify the filename of your YAML manifest.`kubectl apply`

`kubectl apply -f role-dev-namespace.yaml`

Get the resource ID for the

*appdev*group using thecommand. This group is set as the subject of a RoleBinding in the next step.`az ad group show`

`az ad group show --group appdev --query id -o tsv`

Create a RoleBinding for the

*appdev*group to use the previously created Role for namespace access. Create a file named`rolebinding-dev-namespace.yaml`

and paste the following YAML manifest. On the last line, replace*groupObjectId*with the group object ID output from the previous command.`kind: RoleBinding apiVersion: rbac.authorization.k8s.io/v1 metadata: name: dev-user-access namespace: dev roleRef: apiGroup: rbac.authorization.k8s.io kind: Role name: dev-user-full-access subjects: - kind: Group # Replace the placeholder below with the group's objectId (GUID) name: groupObjectId`

Tip

If you want to create the RoleBinding for a single user, specify

*kind: User*and replace*groupObjectId*with the UPN in the previous sample.Create the RoleBinding using the

command and specify the filename of your YAML manifest:`kubectl apply`

`kubectl apply -f rolebinding-dev-namespace.yaml`


## Access AKS cluster resources with Microsoft Entra identities

Now, test that the expected permissions work when you create and manage resources in an AKS cluster. In these examples, you schedule and view pods in the user's assigned namespace, and try to schedule and view pods outside of the assigned namespace.

Reset the

*kubeconfig*context using thecommand. In a previous section, you set the context using the cluster admin credentials. The admin user bypasses Microsoft Entra sign-in prompts. Without the`az aks get-credentials`

`--admin`

parameter, the user context is applied that requires all requests to be authenticated using Microsoft Entra ID.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule a basic NGINX pod using the

command in the`kubectl run`

*dev*namespace:`kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

Enter the credentials for the

*appdev*group account (enter*your*own credentials) at the sign-in prompt. Once you're successfully signed in, the account token is cached for future`kubectl`

commands. The NGINX is successfully scheduled as shown in the following example output:`$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code B24ZD6FP8 to authenticate. pod/nginx-dev created`

Use the

command to view pods in the`kubectl get pods`

*dev*namespace:`kubectl get pods --namespace dev`

Ensure the status of the NGINX pod is

*Running*. The output looks like the following output:`$ kubectl get pods --namespace dev NAME READY STATUS RESTARTS AGE nginx-dev 1/1 Running 0 4m`


### Test SRE access to AKS cluster resources

To confirm that our Microsoft Entra group membership and Kubernetes RBAC work correctly between different users and groups, try the previous commands when signed in as the *akssre* user.

Reset the

*kubeconfig*context using thecommand that clears the previously cached authentication token for the`az aks get-credentials`

*aksdev*user.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --overwrite-existing`

Schedule and view pods in the assigned

*SRE*namespace. When prompted, sign in with the*opssre*group account credentials (enter*your*own credentials).`kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre kubectl get pods --namespace sre`

As shown in the following example output, you can successfully create and view the pods:

`$ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre`

To sign in, use a web browser to open the page

[https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)and enter the code BM4RHP3FD to authenticate.`pod/nginx-sre created $ kubectl get pods --namespace sre NAME READY STATUS RESTARTS AGE nginx-sre 1/1 Running 0`

Try to view or schedule pods outside of assigned SRE namespace.

`kubectl get pods --all-namespaces kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev`

These

`kubectl`

commands fail, as shown in the following example output. The user's group membership and Kubernetes Role and RoleBindings don't grant permissions to create or manager resources in other namespaces.`$ kubectl get pods --all-namespaces Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot list pods at the cluster scope $ kubectl run nginx-sre --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace dev Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create pods in the namespace "dev"`


### Create and view cluster resources outside of the assigned namespace

To view pods outside of the *dev* namespace. Use the [ kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command using

`--all-namespaces`

:```
kubectl get pods --all-namespaces
```


The user's group membership doesn't have a Kubernetes Role that allows this action, as shown in the following example output:

```
Error from server (Forbidden): pods is forbidden: User "aksdev@contoso.com" cannot list resource "pods" in API group "" at the cluster scope
```


In the same way, schedule a pod in a different namespace, such as the *SRE* namespace. The user's group membership doesn't align with a Kubernetes Role and RoleBinding to grant these permissions, as shown in the following example output:

```
$ kubectl run nginx-dev --image=mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine --namespace sre
Error from server (Forbidden): pods is forbidden: User "akssre@contoso.com" cannot create resource "pods" in API group "" in the namespace "sre"
```


### Clean up cluster resources

To clean up all of the resources, run the following commands:

```
# Get the admin kubeconfig context to delete the necessary cluster resources.
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster --admin
# Delete the dev and SRE namespaces. This also deletes the pods, Roles, and RoleBindings.
kubectl delete namespace dev
kubectl delete namespace sre
# Delete the Microsoft Entra ID user accounts for aksdev and akssre.
az ad user delete --upn-or-object-id $AKSDEV_ID
az ad user delete --upn-or-object-id $AKSSRE_ID
# Delete the Microsoft Entra ID groups for appdev and opssre. This also deletes the Azure role assignments.
az ad group delete --group appdev
az ad group delete --group opssre
```


## Next steps

For more information about how to secure Kubernetes clusters, see

[Access and identity options for AKS](concepts-identity#kubernetes-rbac).For best practices on identity and resource control, see

[Best practices for authentication and authorization in AKS](operator-best-practices-identity).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/outbound-rules-control-egress -->

# Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides the necessary details that allow you to secure outbound traffic from your Azure Kubernetes Service (AKS). It contains the cluster requirements for a base AKS deployment and additional requirements for optional addons and features. You can apply this information to any outbound restriction method or appliance.

To see an example configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Background

AKS clusters are deployed on a virtual network. This network can either be customized and preconfigured by you or it can be created and managed by AKS. In either case, the cluster has **outbound**, or egress, dependencies on services outside of the virtual network.

For management and operational purposes, nodes in an AKS cluster need to access certain ports and fully qualified domain names (FQDNs). These endpoints are required for the nodes to communicate with the API server or to download and install core Kubernetes cluster components and node security updates. For example, the cluster needs to pull container images from Microsoft Artifact Registry (MAR).

The AKS outbound dependencies are almost entirely defined with FQDNs, which don't have static addresses behind them. The lack of static addresses means you can't use network security groups (NSGs) to lock down the outbound traffic from an AKS cluster.

By default, AKS clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. For outbound internet traffic, it's not recommended to set all deny rules in an NSG.

A [network isolated AKS cluster](concepts-network-isolated), provides the simplest and most secure solution for setting up outbound restrictions for a cluster out of the box. A network isolated cluster pulls the images for cluster components and add-ons from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint. The cluster operator can then incrementally set up allowed outbound traffic securely over a private network for each scenario they want to enable. This way the cluster operators have complete control over designing the allowed outbound traffic from their clusters right from the start, thus allowing them to reduce the risk of data exfiltration.

Another solution to securing outbound addresses is using a firewall device that can control outbound traffic based on domain names. Azure Firewall can restrict outbound HTTP and HTTPS traffic based on the FQDN of the destination. You can also configure your preferred firewall and security rules to allow these required ports and addresses.

Important

This document covers only how to lock down the traffic leaving the AKS subnet. AKS has no ingress requirements by default. Blocking **internal subnet traffic** using network security groups (NSGs) and firewalls isn't supported. To control and block the traffic within the cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

## Required outbound network rules and FQDNs for AKS clusters

The following network and FQDN/application rules are required for an AKS cluster. You can use them if you wish to configure a solution other than Azure Firewall.

- IP address dependencies are for non-HTTP/S traffic (both TCP and UDP traffic).
- FQDN HTTP/HTTPS endpoints can be placed in your firewall device.
- Wildcard HTTP/HTTPS endpoints are dependencies that can vary with your AKS cluster based on a number of qualifiers.
- AKS uses an admission controller to inject the FQDN as an environment variable to all deployments under kube-system and gatekeeper-system. This ensures all system communication between nodes and API server uses the API server FQDN and not the API server IP. You can get the same behavior on your own pods, in any namespace, by annotating the pod spec with an annotation named
`kubernetes.azure.com/set-kube-service-host-fqdn`

. If that annotation is present, AKS will set the KUBERNETES_SERVICE_HOST variable to the domain name of the API server instead of the in-cluster service IP. This is useful in cases where the cluster egress is via a layer 7 firewall. - If you have an app or solution that needs to talk to the API server, you must either add an
**additional**network rule to allow**TCP communication to port 443 of your API server's IP****OR**, if you have a layer 7 firewall configured to allow traffic to the API Server's domain name, set`kubernetes.azure.com/set-kube-service-host-fqdn`

in your pod specs. - On rare occasions, if there's a maintenance operation, your API server IP might change. Planned maintenance operations that can change the API server IP are always communicated in advance.
- You might notice traffic towards "md-*.blob.storage.azure.net" endpoint. This endpoint is used for internal components of Azure Managed Disks. Blocking access to this endpoint from your firewall should not cause any issues.
- You might notice traffic towards "umsa*.blob.core.windows.net" endpoint. This endpoint is used to store manifests for Azure Linux VM Agent & Extensions and is regularly checked to download new versions. You can find more details on
[VM Extensions](/en-us/azure/virtual-machines/extensions/features-linux?tabs=azure-cli#network-access).

### Azure Global required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. This isn't required for
konnectivity-agent enabled. |

`*:9000`

*Or*[ServiceTag](/en-us/azure/virtual-network/service-tags-overview#available-service-tags)-`AzureCloud.<Region>:9000`

*Or*[Regional CIDRs](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files)-`RegionCIDRs:9000`

*Or*`APIServerPublicIP:9000`

`(only known after cluster creation)`

[private clusters](private-clusters), or for clusters with the*konnectivity-agent*enabled.**or**`*:123`

**(if using Azure Firewall network rules)**`ntp.ubuntu.com:123`

`CustomDNSIP:53`

`(if using custom DNS servers)`

`APIServerPublicIP:443`

`(if running pods/deployments, like Ingress Controller, that access the API Server)`

[private clusters](private-clusters).### Azure Global required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.azmk8s.io` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. This is required for clusters with konnectivity-agent enabled. Konnectivity also uses Application-Layer Protocol Negotiation (ALPN) to communicate between agent and server. Blocking or rewriting the ALPN extension will cause a failure. This isn't required for
|
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
, `*.data.mcr.microsoft.com` `mcr-0001.mcr-msedge.net` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.azure.com` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

### Microsoft Azure operated by 21Vianet required network rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.Region:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
`*:22` Or
`AzureCloud.<Region>:22` Or
`RegionCIDRs:22` Or `APIServerPublicIP:22` `(only known after cluster creation)` |
TCP | 22 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pod/deployments would use the API IP. |

### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`*.tun.<location>.cx.prod.service.azk8s.cn` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure Content Delivery Network (CDN). |
`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.chinacloudapi.cn` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`*.azk8s.cn` |
`HTTPS:443` |
This address is for the repository required to download and install required binaries like kubenet and Azure CNI. |
, `mcr.azure.cn` `*.data.mcr.azure.cn` |
`HTTPS:443` |
Required to access images Microsoft Container Registry (MCR) in China Cloud (Mooncake). This registry serves as a cache for mcr.microsoft.com with improved reliability and performance. |

### Azure US Government required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`*:1194` Or
`AzureCloud.<Region>:1194` Or
`RegionCIDRs:1194` Or `APIServerPublicIP:1194` `(only known after cluster creation)` |
UDP | 1194 | For tunneled secure communication between the nodes and the control plane. |
`*:9000` Or
`AzureCloud.<Region>:9000` Or
`RegionCIDRs:9000` Or `APIServerPublicIP:9000` `(only known after cluster creation)` |
TCP | 9000 | For tunneled secure communication between the nodes and the control plane. |
or `*:123` (if using Azure Firewall network rules)`ntp.ubuntu.com:123` |
UDP | 123 | Required for Network Time Protocol (NTP) time synchronization on Linux nodes. |
`CustomDNSIP:53` `(if using custom DNS servers)` |
UDP | 53 | If you're using custom DNS servers, you must ensure they're accessible by the cluster nodes. |
`APIServerPublicIP:443` `(if running pods/deployments, like Ingress Controller, that access the API Server)` |
TCP | 443 | Required if running pods/deployments that access the API Server (like Ingress Controller), those pods/deployments would use the API IP. |

### Azure US Government required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`*.hcp.<location>.cx.aks.containerservice.azure.us` |
`HTTPS:443` |
Required for Node <-> API server communication. Replace <location> with the region where your AKS cluster is deployed. |
`mcr.microsoft.com` |
`HTTPS:443` |
Required to access images in Microsoft Container Registry (MCR). This registry contains first-party images/charts (for example, coreDNS, etc.). These images are required for the correct creation and functioning of the cluster, including scale and upgrade operations. |
`*.data.mcr.microsoft.com` |
`HTTPS:443` |
Required for MCR storage backed by the Azure content delivery network (CDN). |
`management.usgovcloudapi.net` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |
`packages.microsoft.com` |
`HTTPS:443` |
This address is the Microsoft packages repository used for cached apt-get operations. Example packages include Moby, PowerShell, and Azure CLI. |
`acs-mirror.azureedge.net` |
`HTTPS:443` |
This address is for the repository required to install required binaries like kubenet and Azure CNI. |
`packages.aks.azure.com` |
`HTTPS:443` |
This address will be replacing `acs-mirror.azureedge.net` in the future and will be used to download and install required Kubernetes and Azure CNI binaries. |

## Optional recommended FQDN / application rules for AKS clusters

The following FQDN / application rules aren't required, but are recommended for AKS clusters:

| Destination FQDN | Port | Use |
|---|---|---|
`security.ubuntu.com` , `azure.archive.ubuntu.com` , `changelogs.ubuntu.com` |
`HTTP:80` |
This address lets the Linux cluster nodes download the required security patches and updates. |
`snapshot.ubuntu.com` |
`HTTPS:443` |
This address lets the Linux cluster nodes download the required security patches and updates from ubuntu snapshot service. |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that node image upgrades also come with updated packages including security fixes.

## GPU enabled AKS clusters required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`nvidia.github.io` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`us.download.nvidia.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |
`download.docker.com` |
`HTTPS:443` |
This address is used for correct driver installation and operation on GPU-based nodes. |

## Windows Server based node pools required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
`onegetcdn.azureedge.net, go.microsoft.com` |
`HTTPS:443` |
To install windows-related binaries |
`*.mp.microsoft.com, www.msftconnecttest.com, ctldl.windowsupdate.com` |
`HTTP:80` |
To install windows-related binaries |

If you choose to block/not allow these FQDNs, the nodes will only receive OS updates when you do a [node image upgrade](node-image-upgrade) or [cluster upgrade](upgrade-cluster). Keep in mind that Node Image Upgrades also come with updated packages including security fixes.

## AKS features, addons, and integrations

### Workload identity

#### Required FQDN / application rules

| Destination FQDN | Port | Use |
|---|---|---|
or `login.microsoftonline.com` or `login.chinacloudapi.cn` `login.microsoftonline.us` |
`HTTPS:443` |
Required for Microsoft Entra authentication. |

### Microsoft Defender for Containers

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra Authentication. |
`*.ods.opinsights.azure.com` (Azure Government) `*.ods.opinsights.azure.us` (Azure operated by 21Vianet)`*.ods.opinsights.azure.cn` |
`HTTPS:443` |
Required for Microsoft Defender to upload security events to the cloud. |
`*.oms.opinsights.azure.com` (Azure Government) `*.oms.opinsights.azure.us` (Azure operated by 21Vianet)`*.oms.opinsights.azure.cn` |
`HTTPS:443` |
Required to authenticate with Log Analytics workspaces. |
`*.cloud.defender.microsoft.com` |
`HTTPS:443` |
NEW: Required for Microsoft Defender to upload security events to the cloud. |

### Azure Key Vault provider for Secrets Store CSI Driver

If using network isolated clusters, it's recommended to set up [private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service?tabs=portal).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`vault.azure.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server. |
`*.vault.usgovcloudapi.net` |
`HTTPS:443` |
Required for CSI Secret Store addon pods to talk to Azure KeyVault server in Azure Government. |

### Azure Monitor - Managed Prometheus, Container Insights, and Azure Monitor Application Insights Autoinstrumentation

If using network isolated clusters, it's recommended to set up [private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link#container-insights-log-analytics-workspace), which is supported for Managed Prometheus (Azure Monitor workspace), Container insights (Log Analytics workspace), and Azure Monitor Application Insights Autoinstrumentation (Application Insights resource).

If your cluster has outbound type user-defined routing and Azure Firewall, the following network rules and application rules are applicable:

#### Required network rules

| Destination Endpoint | Protocol | Port | Use |
|---|---|---|---|
`AzureMonitor:443` |

#### Azure public cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.com` |
443 | |
`*.oms.opinsights.azure.com` |
443 | |
`dc.services.visualstudio.com` |
443 | |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`*.monitoring.azure.com` |
443 | |
`login.microsoftonline.com` |
443 | |
`global.handler.control.monitor.azure.com` |
Access control service | 443 |
`*.ingest.monitor.azure.com` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.com` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |
`<cluster-region-name>.handler.control.monitor.azure.com` |
Fetch data collection rules for specific cluster | 443 |

#### Microsoft Azure operated by 21Vianet cloud required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.cn` |
Data ingestion | 443 |
`*.oms.opinsights.azure.cn` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.cn` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.cn` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.cn` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.cn` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

#### Azure Government cloud required FQDN / application rules

| Endpoint | Purpose | Port |
|---|---|---|
`*.ods.opinsights.azure.us` |
Data ingestion | 443 |
`*.oms.opinsights.azure.us` |
Azure Monitor agent (AMA) onboarding | 443 |
`dc.services.visualstudio.com` |
For agent telemetry that uses Azure Public Cloud Application Insights | 443 |
`*.in.applicationinsights.azure.com` |
Application Insights Autoinstrumentation. To limit the scope, can be changed to only allow endpoints in connection strings for the destination resources | 443 |
`global.handler.control.monitor.azure.us` |
Access control service | 443 |
`<cluster-region-name>.handler.control.monitor.azure.us` |
Fetch data collection rules for specific cluster | 443 |
`*.ingest.monitor.azure.us` |
Container Insights - logs ingestion endpoint (DCE) | 443 |
`*.metrics.ingest.monitor.azure.us` |
Azure monitor managed service for Prometheus - metrics ingestion endpoint (DCE) | 443 |

### Azure Policy

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.core.windows.net` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |
`dc.services.visualstudio.com` |
`HTTPS:443` |
Azure Policy add-on that sends telemetry data to applications insights endpoint. |

#### Microsoft Azure operated by 21Vianet required FQDN / application rules

For information about retired Microsoft Defender for Cloud features, see [Microsoft Defender for Containers](#microsoft-defender-for-containers).

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.cn` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`data.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Kubernetes policies and to report cluster compliance status to policy service. |
`store.policy.azure.us` |
`HTTPS:443` |
This address is used to pull the Gatekeeper artifacts of built-in policies. |

### AKS cost analysis add-on

#### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`management.azure.com` (Azure Government) `management.usgovcloudapi.net` (Azure operated by 21Vianet)`management.chinacloudapi.cn` |
`HTTPS:443` |
Required for Kubernetes operations against the Azure API. |
`login.microsoftonline.com` (Azure Government) `login.microsoftonline.us` (Azure operated by 21Vianet)`login.microsoftonline.cn` |
`HTTPS:443` |
Required for Microsoft Entra ID authentication. |

## Cluster extensions

### Required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.com` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |
`arcmktplaceprod.azurecr.io` |
`HTTPS:443` |
This address is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.centralindia.data.azurecr.io` |
`HTTPS:443` |
This address is for the Central India regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.japaneast.data.azurecr.io` |
`HTTPS:443` |
This address is for the East Japan regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westus2.data.azurecr.io` |
`HTTPS:443` |
This address is for the West US2 regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.westeurope.data.azurecr.io` |
`HTTPS:443` |
This address is for the West Europe regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`arcmktplaceprod.eastus.data.azurecr.io` |
`HTTPS:443` |
This address is for the East US regional data endpoint and is required to pull container images for installing marketplace extensions on AKS cluster. |
`*.ingestion.msftcloudes.com, *.microsoftmetrics.com` |
`HTTPS:443` |
This address is used to send agents metrics data to Azure. |
`marketplaceapi.microsoft.com` |
`HTTPS: 443` |
This address is used to send custom meter-based usage to the commerce metering API. |

#### Azure US Government required FQDN / application rules

| FQDN | Port | Use |
|---|---|---|
`<region>.dp.kubernetesconfiguration.azure.us` |
`HTTPS:443` |
This address is used to fetch configuration information from the Cluster Extensions service and report extension status to the service. |
`mcr.microsoft.com, *.data.mcr.microsoft.com` |
`HTTPS:443` |
This address is required to pull container images for installing cluster extension agents on AKS cluster. |

Note

For any addons that aren't explicitly stated here, the core requirements cover it.

### Istio-based service mesh add-on

In Istio=based service mesh add-on, if you are setting up istiod with a Plugin Certificate Authority (CA) or if you are setting up secure ingress gateway, Azure Key Vault provider for Secrets Store CSI Driver is required for these features. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

### Application routing add-on

Application routing add-on supports SSL termination at the ingress with certificates stored in Azure Key Vault. Outbound network requirements for Azure Key Vault provider for Secrets Store CSI Driver can be found [here](#azure-key-vault-provider-for-secrets-store-csi-driver).

## Next steps

In this article, you learned what ports and addresses to allow if you want to restrict egress traffic for the cluster.

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster see [Secure traffic between pods using network policies in AKS](use-network-policies).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-containerd -->

# Create Windows Server node pools with containerd in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Kubernetes version 1.20 and higher, you can specify [ containerd](https://containerd.io/) as the container runtime for Windows Server 2019 node pools. Starting with Kubernetes 1.23,

`containerd`

is the default and only container runtime for Windows.In this article, you learn how to create Windows Server node pools with `containerd`

in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)installed and configured. Find the version using the`az version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations and considerations

When using Windows Server node pools with `containerd`

, keep the following limitations and considerations in mind:

- Both the control plane and Windows Server 2019 node pools must use Kubernetes version 1.20 or greater.
- When you create or update a node pool to run Windows Server containers, the default value for
`--node-vm-size`

is`Standard_D2s_v3`

, which was the minimum recommended size for Windows Server 2019 node pools up to Kubernetes version 1.20. The minimum recommended size for Windows Server 2019 node pools using`containerd`

is`Standard_D4s_v3`

. When setting the`--node-vm-size`

parameter, check the[list of restricted virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes/overview). - We recommend using
[taints or labels](manage-node-pools#set-node-pool-taints)with your Windows Server 2019 node pools running`containerd`

and tolerations or node selectors with your deployments to guarantee your workloads are scheduled correctly.

## Add a Windows Server node pool with `containerd`


Add a Windows Server node pool with

`containerd`

into your existing cluster using the.`az aks nodepool add`

Note

If you don't specify the

`WindowsContainerRuntime=containerd`

custom header, the node pool still uses`containerd`

as the container runtime by default.`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $CONTAINER_D_NODE_POOL_NAME \ --node-vm-size Standard_D4s_v3 \ --kubernetes-version 1.20.5 \ --aks-custom-headers WindowsContainerRuntime=containerd \ --node-count 1`


## Upgrade an existing Windows Server node pool to `containerd`


Upgrade a specific node pool from Docker to

`containerd`

using thecommand.`az aks nodepool upgrade`

`export CONTAINER_D_NODE_POOL_NAME="mywindowsnodepool" az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name $CONTAINER_D_NODE_POOL_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Upgrade all existing Windows Server node pools to `containerd`


Upgrade all node pools from Docker to

`containerd`

using thecommand.`az aks nodepool upgrade`

`az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-os-version -->

# Upgrade operating system (OS) versions in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes OS versions available for Azure Kubernetes Service (AKS) nodes, and best practices for testing and upgrading your OS version.

Important

Starting on **March 17, 2027**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Supported OS versions

Each [node image](node-images) corresponds to an OS version, which you can specify using OS SKU. You can specify the following parameters when creating clusters and node pools:

**--os-type**: OS type, including Linux or Windows.*You can't specify the Windows OS type during cluster creation or update.***--os-sku**: Used to specify OS version or OS variant.*You can't specify the Windows OS SKU during cluster creation or update.*For more information for supported OS SKU options, see[Azure AKS CLI](/en-us/cli/azure/aks#az-aks-create)or[API](/en-us/rest/api/aks/agent-pools/create-or-update#ossku).**--kubernetes-version**: Version of Kubernetes to use for creating the node pool or cluster.


Best practice guidanceThe default OS version is the most recent validated version.


- For Ubuntu, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku Ubuntu`

. This will automatically update you to the latest default Ubuntu version based on your Kubernetes version.- For Azure Linux, we recommend creating clusters and node pools while specifying
`--os-type Linux`

and`--os-sku AzureLinux`

. This will automatically update you to the latest default Azure Linux version based on your Kubernetes version.- For Windows, we recommend creating node pools while specifying
`--os-type Windows`

and`--os-sku Windows2022`

. You need to manually update node pools to the next OS version when it's released.

| OS type | OS SKU | Supported Kubernetes versions | Default versioning |
|---|---|---|---|
| Linux | Ubuntu | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Ubuntu 22.04 is default for Kubernetes versions 1.25 to 1.34. Ubuntu 24.04 is default for Kubernetes versions 1.35+. |
| Linux | Ubuntu2404 | This OS SKU will only be supported in Kubernetes 1.32 to 1.38. | We recommend this versioned OS SKU if you want to migrate to the new OS version without upgrading your Kubernetes version. Ubuntu 24.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.35+. |
| Linux | Ubuntu2204 | This OS SKU is supported in Kubernetes versions 1.25 to 1.36. | We recommend this versioned OS SKU if you need to roll back to Ubuntu 22.04. Ubuntu 22.04 is default when using `--os-sku Ubuntu` in Kubernetes versions 1.25 to 1.35. |
| Linux | AzureLinux | This OS SKU is supported in all Kubernetes versions. | OS version for this OS SKU changes based on your Kubernetes version. Azure Linux 2.0 is default for Kubernetes version 1.27 to 1.31. Azure Linux 3.0 is default for Kubernetes version 1.32+. When the `AzureLinuxV3Preview` feature flag is enabled on AKS 1.31, `--os-sku AzureLinux` defaults to 3.0. |
| Linux | AzureLinux3 | This OS SKU is supported in Kubernetes 1.28 to 1.36. | We recommend this OS SKU if you want to test out the new OS version without upgrading your Kubernetes version. You can also use this OS SKU to migrate from Azure Linux 2.0 to Azure Linux 3.0. |
| Linux | AzureLinuxOSGuard | This OS SKU is supported in Kubernetes versions 1.32 and above. | Azure Linux with OS Guard versions are upgraded through node image upgrades. For more information, see
|

[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).## Migrate to a new OS version

When a new OS version releases on AKS, it's initially supported in preview. After testing in preview for a few months, AKS makes the new OS version generally available (GA) and then updates the default OS SKU (`Ubuntu`

or `AzureLinux`

) to the latest GA OS version. This default update occurs with a new Kubernetes version release.

We recommend testing your nonproduction workloads with the new OS version when it becomes available in preview. In order to access preview functions, make sure you have the preview extension installed. You can install the extension using the `az extension add --name aks-preview`

command.

There are two ways to migrate to a new OS version:

**Default OS SKU**: If you're using a default OS SKU such as`Ubuntu`

or`AzureLinux`

, you automatically get the latest GA version when you[upgrade your Kubernetes version](manage-node-pools). There are no manual changes required to migrate to a new OS version.**Versioned OS SKU**: If you're using a versioned OS SKU such as`Ubuntu2404`

,`AzureLinux3`

, or`Windows2025`

, you need to manually migrate to a new OS version to avoid blocked Kubernetes upgrades. If you're using a Linux OS, you can update the OS SKU on an existing node pool to manually migrate.

### Update OS SKU on an existing node pool

Update the `os-sku`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. In cases where there's a new OS version available in preview, this functionality allows you to migrate your node pool to the new OS version without needing to upgrade your Kubernetes version.

Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Migrate to Ubuntu 24.04

Ubuntu 24.04 is the default for `--os-sku Ubuntu`

in Kubernetes versions 1.35+. You can also use Ubuntu 24.04 by specifying `--os-sku Ubuntu2404`

.

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2404`

:

[FIPS](enable-fips-nodes)is not supported.- Ubuntu 24.04 is supported in Kubernetes versions 1.32 to 1.38.
- You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.39+.
`--os-sku Ubuntu2404`

is an option and is intended for testing the new OS Linux version without requiring you to upgrade your Kubernetes version. - You need the preview Azure CLI version 18.0.0b5 or later for
*preview*and version 2.82.0 for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku Ubuntu2404`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2404 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


#### Migrate to Azure Linux 3.0

Azure Linux 3.0 is the default for `--os-sku AzureLinux`

in Kubernetes versions 1.32 to 1.36. You can also use Azure Linux 3.0 by specifying `--os-sku AzureLinux3`

.

Note

Keep the following information in mind when migrating to `--os-sku AzureLinux3`

:

`--os-sku AzureLinux3`

is supported in Kubernetes versions 1.28 to 1.36.`--os-sku AzureLinux3`

is intended for migrating to Azure Linux 3.0 without upgrading your Kubernetes version. You need to update your OS SKU to a supported OS option before upgrading your Kubernetes version to 1.37+.- You need the Azure CLI version 18.0.0b36 or later for
*preview*and version 2.78.0 or later for*GA*installed and configured. To find your CLI version, run`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Update to `--os-sku AzureLinux3`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux3 \
--kubernetes-version 1.30.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Roll back your OS version

In Kubernetes versions where multiple OS versions are supported, you can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to roll back to a previous OS version.

You might want to roll back your OS version in the following scenarios:

- If you're testing a new OS version and you run into any issues.
- Once you upgrade to a Kubernetes version that supports the new OS version as default, you might want to roll back to the default
`Ubuntu`

or`AzureLinux`

OS SKU. This allows you to get future OS versions as a part of your Kubernetes upgrades instead of requiring a node pool update.

### Roll back your OS version to the default OS SKU

You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to update the

`os-sku`

on an existing node pool. In cases where there's a previous OS version supported in your Kubernetes version, this functionality can allow you to roll back your OS version.Note

The following values aren't supported for node pool update command:

`--os-sku Windows2019`

`--os-sku Windows2022`

`--os-sku Windows2025`


Instead, you need to add node pools to your cluster with the corresponding `--os-sku`

you intend to use.

| OS SKU | Default OS version |
|---|---|
| Ubuntu | When you have OS SKU `Ubuntu` , Ubuntu 22.04 is the default OS version if your Kubernetes version is 1.25 to 1.34. Ubuntu 24.04 is the default for Ubuntu in Kubernetes 1.35 to 1.37. |
| AzureLinux | When you have OS SKU `AzureLinux` , Azure Linux 2.0 is the default for AzureLinux in Kubernetes 1.26 to 1.31. Azure Linux 3.0 is the default for AzureLinux in Kubernetes 1.32 to 1.36. |

#### Update your OS SKU to Ubuntu on an existing node pool

When updating your node pool to use OS SKU `Ubuntu`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku Ubuntu`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu \
--name $NODE_POOL_NAME \
--node-count 1
```


You can use the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command to migrate between any supported Linux

`os-sku`

. The command might fail if the target OS doesn't have a supported node image for your Kubernetes version, VM size, or FIPS enablement.#### Update your OS SKU to Azure Linux on an existing node pool

When updating your node pool to use OS SKU `AzureLinux`

, you'll get the default OS version based on your Kubernetes version. This might trigger an automatic reimage if the OS version changes during the node pool update command.

Update to `--os-sku AzureLinux`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku AzureLinux \
--name $NODE_POOL_NAME \
--node-count 1
```


### Roll back to Ubuntu 22.04

Note

Keep the following information in mind when migrating to `--os-sku Ubuntu2204`

:

[FIPS](enable-fips-nodes)and[CVM](use-cvm)aren't supported.- Ubuntu 22.04 is supported in Kubernetes versions 1.25 to 1.35.
`--os-sku Ubuntu2204`

is intended for roll back to Ubuntu 22.04 on your current Kubernetes version. You need to update your OS SKU to a supported OS option to upgrade your Kubernetes version to 1.36 and above.

Roll back to `--os-sku Ubuntu2204`

on an existing node pool using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--os-sku Ubuntu2204 \
--kubernetes-version 1.32.0 \
--name $NODE_POOL_NAME \
--node-count 1
```


## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-aksnodeclass -->

# Configure AKSNodeClass resources for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure `AKSNodeClass`

resources to define Azure-specific settings for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using Karpenter. `AKSNodeClass`

allows you to customize various aspects of the nodes that Karpenter provisions, such as the virtual machine (VM) image, operating system (OS) disk size, maximum pods per node, and kubelet configurations.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-az-cli -->

# Install the Open Service Mesh (OSM) add-on using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Open Service Mesh (OSM) add-on on an Azure Kubernetes Service (AKS) cluster. The OSM add-on installs the OSM mesh on your cluster. The OSM mesh is a service mesh that provides traffic management, policy enforcement, and telemetry collection for your applications. For more information about the OSM mesh, see [Open Service Mesh](https://openservicemesh.io/).

Important

Starting on **September 30, 2027**, Azure Kubernetes Service (AKS) no longer supports the Open Service Mesh (OSM) add-on. The [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/) retired the upstream OSM project. [Migrate any existing OSM configurations to equivalent Istio configurations](/en-us/azure/aks/open-service-mesh-istio-migration-guidance). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-static-egress-gateway -->

# Configure Static Egress Gateway in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Static Egress Gateway in AKS provides a streamlined solution for configuring fixed source IP addresses for outbound traffic from your AKS workloads. This feature allows you to route egress traffic through a dedicated "gateway node pool". By using the Static Egress Gateway, you can efficiently manage and control outbound IP addresses and ensure that your AKS workloads can communicate with external systems securely and consistently, using predefined IPs.

This article provides step-by-step instructions to set up a Static Egress Gateway node pool in your AKS cluster, enabling you to configure fixed source IP addresses for outbound traffic from your Kubernetes workloads.

## Limitations and considerations

Static Egress Gateway isn't supported in clusters with

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet).Kubernetes network policies won't apply to traffic leaving the cluster through the gateway node pool.

- This shouldn't affect cluster traffic control as
**only**egress traffic from annotated pods**routed to the gateway node pool**are affected.

- This shouldn't affect cluster traffic control as
The gateway node pool isn't intended for general-purpose workloads and should be used for egress traffic only.

Windows node pools can't be used as gateway node pools.

hostNetwork pods

**cannot**be annotated to use the gateway node pool.Pods can only use a gateway node pool if they are in the same namespace as the

`StaticGatewayConfiguration`

resource.

## Create or update an AKS cluster with Static Egress Gateway

Before you can create and manage gateway node pools, you must enable the Static Egress Gateway feature for your AKS cluster. You can do this when creating a new cluster or by updating an existing cluster using `az aks update`

.

```
az aks create -n <cluster-name> -g <resource-group> --enable-static-egress-gateway
```


## Create a Gateway Node pool

After enabling the feature, create a dedicated gateway node pool. This node pool handles the egress traffic through the specified public IP prefix. The `--gateway-prefix-size`

is the size of the public IP prefix to be applied to the gateway node pool nodes. The allowed range is `28`

-`31`

.

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--gateway-prefix-size <prefix-size>
```


Note

- The number of nodes must fit within the capacity allowed by the selected prefix size. For example, a /30 prefix supports up to 4 nodes, and at least 2 nodes are required for high availability. Since you can’t adjust the node count dynamically, plan your nodes according to the fixed limit set by the prefix size.
- You can define the SKU of the VM to use in your gateway node pool with the
`--vm-size`

parameter. You should understand your specific needs and plan accordingly to ensure the right performance and cost balance.

## Scale the Gateway Node pool (Optional)

If necessary, you can resize the gateway node pool within the limits defined by the prefix size but it doesn't support autoscaling.

```
az aks nodepool scale --cluster-name <cluster-name> -n <nodepool-name> --node-count <desired-node-count>
```


## Create a Static Gateway Configuration

Define the gateway configuration by creating a `StaticGatewayConfiguration`

custom resource. This configuration specifies which node pool and public IP prefix to use.

```
apiVersion: egressgateway.kubernetes.azure.com/v1alpha1
kind: StaticGatewayConfiguration
metadata:
name: <gateway-config-name>
namespace: <namespace>
spec:
gatewayNodepoolName: <nodepool-name>
excludeCidrs: # Optional
- 10.0.0.0/8
- 172.16.0.0/12
- 169.254.169.254/32
publicIpPrefixId: /subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.Network/publicIPPrefixes/<prefix-name> # Optional
```


Tip

If you don't set `publicIpPrefixId`

, a public IP prefix will be created for you automatically. When running `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, you can see the "Egress Ip Prefix" in the status. This is the newly created public IP prefix. You can also use an existing public IP prefix by specifying its resource ID in the `publicIpPrefixId`

argument. You need to grant "Network Contributor" role to AKS cluster's identity in this case.

### Static Private IP Support (Preview)

Important

Static private IP support requires clusters running Kubernetes version 1.34 or later and a subscription with the `Microsoft.ContainerService/StaticEgressGatewayPreview`

Azure Feature Exposure Control (AFEC) flag enabled. Follow [Register preview feature](/en-us/azure/azure-resource-manager/management/preview-features#register-preview-feature) to request the feature flag before creating the Gateway VirtualMachines node pool.

If you must keep egress traffic on private addresses, enable private IP support on the gateway node pool. Use the same `az aks nodepool add`

command and set the node pool to use the VirtualMachines VM set type while disabling public IP provisioning:

```
az aks nodepool add --cluster-name <cluster-name> \
--name <nodepool-name> \
--resource-group <resource-group> \
--mode gateway \
--node-count <number-of-nodes> \
--vm-set-type VirtualMachines \
--gateway-prefix-size <prefix-size>
```


In this configuration, the `provisionPublicIps=false`

setting keeps the private IPs allocated to the gateway nodes for the lifetime of the `StaticGatewayConfiguration`

. When you run `kubectl describe StaticGatewayConfiguration <gateway-config-name> -n <namespace>`

, the `egressIpPrefix`

field shows a comma-separated list of those static private IPs. You continue to use the same APIs and manifests for the rest of the workflow, including the `StaticGatewayConfiguration`

resource and the pod annotations.

## Annotate Pods to Use the Gateway Configuration

To route traffic from specific pods through the gateway node pool, annotate the pod template in the deployment configuration.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: <deployment-name>
namespace: <namespace>
spec:
template:
metadata:
annotations:
kubernetes.azure.com/static-gateway-configuration: <gateway-config-name>
```


Note

The CNI plugin on each node will automatically configure the pod to route its traffic through the selected gateway nodepool.

## Monitor and Manage Gateway Configurations

Once deployed, you can monitor the status of your gateway configurations through the AKS cluster. The status section in the `StaticGatewayConfiguration`

resource is updated with details such as assigned IPs and WireGuard configurations.

## Delete a Gateway Node pool (Optional)

To remove a gateway node pool, ensure all associated configurations are appropriately handled before deletion.

```
az aks nodepool delete --cluster-name <cluster-name> -n <nodepool-name>
```


## Disable the Static Egress Gateway Feature (Optional)

If you no longer need the Static Egress Gateway, you can disable the feature and uninstall the operator. Ensure all gateway node pools are deleted first.

```
az aks update -n <cluster-name> -g <resource-group> --disable-static-egress-gateway
```


By following these steps, you can effectively set up and manage Static Egress Gateway configurations in your AKS cluster, enabling controlled and consistent egress traffic from your workloads.

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
- Windows 2019 nodes are not supported in Azure CNI Pod Subnet
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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-cluster-connect -->

# Establish network connectivity to a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In private AKS clusters, the API server endpoint has no public IP address. To manage the API server, you need to use a virtual machine (VM) or container that has access to the virtual network (VNet) of the AKS cluster. There are several options for establishing network connectivity to the private cluster:

- Use an
[Azure Cloud Shell](/en-us/azure/cloud-shell/vnet/overview)instance deployed into a subnet that's connected to the API server for the cluster. - Use
[Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster)'s native client tunneling feature (preview). - Use a VM in a separate network and set up
[virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview). - Use a
[private endpoint](/en-us/azure/private-link/private-endpoint-overview)connection. - Create a VM in the same VNet as the AKS cluster using the
command with the`az vm create`

`--vnet-name`

flag. - Use an
[Express Route or VPN](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways)connection. - Use the
[AKS](access-private-cluster).`command invoke`

feature

## Choose a connectivity option

Azure Cloud Shell and Azure Bastion (preview) are the easiest options. Express Route and VPNs add costs and require extra networking complexity. Virtual network peering requires you to plan your network CIDR ranges to ensure there are no overlapping ranges.

The following table outlines the key differences and limitations of using Azure Cloud Shell and Azure Bastion:

| Option | Azure Cloud Shell | Azure Bastion (preview) |
|---|---|---|
| Key differences | • Ephemeral, browser-based access. • Cost-effective. • Comes with preinstalled tools like `az cli` and `kubectl` . |
• Persistent, long-running access. • Suited for managing multiple clusters. • Use your own native client tooling. |
| Limitations | • Not supported with AKS Automatic clusters or clusters with network resource group (NRG) lockdown. • You can't have multiple Cloud Shell sessions in different VNets at the same time. |
• Not supported with AKS Automatic clusters or clusters with NRG lockdown. |

## Connect using Azure Cloud Shell

Connecting to a private AKS cluster through Azure Cloud Shell requires completing the following steps:

**Deploy required resources:**You need to deploy Cloud Shell in a VNet that can reach your private cluster. This step provisions the necessary infrastructure. While Cloud Shell is a free service, using Cloud Shell in a VNet requires some resources that incur cost. For more information, see[Deploy Cloud Shell in a virtual network](/en-us/azure/cloud-shell/vnet/deployment).**Configure the connection:**After you deploy the resources, any user in the subscription that has appropriate permissions on the cluster can configure Cloud Shell to deploy in the VNet to allow a secure connection to the private cluster.

## Deploy required resources

To deploy and configure the required resources, you must have the **Owner** role assignment on the subscription. To view and assign roles, see [List Owners of a Subscription](/en-us/azure/role-based-access-control/role-assignments-list-portal#list-owners-of-a-subscription).

You can deploy the required resources using the Azure portal or the provided ARM template if you manage infrastructure as code or have organizational policies that require specific resource naming conventions.

You can optionally leave the deployed resources in place for future connections or delete and recreate them as needed.

### Use the Azure portal (preview)

This option creates a separate VNet with the necessary resources for Cloud Shell and configures VNet peering for you.

- In the
[Azure portal](https://portal.azure.com), navigate to your private cluster resource. - On the Overview page, select
**Connect**. - On the
**Cloud Shell**tab, under**Prerequisites for private cluster connection**, select**Configure**to deploy the necessary resources.- The deployment creates a new resource group named
`RG-CloudShell-PrivateClusterConnection-{RANDOM_ID}`

.

- The deployment creates a new resource group named
- Once the deployment succeeds, under
**Set cluster context**, select**Open Cloud Shell**.


Note

If you already configured Cloud Shell in a VNet for a particular cluster, repeating these steps ensures your Cloud Shell user settings are correctly aligned with that VNet.

### Use an ARM template

To have more control over the deployment configuration, use the [provided ARM template](/en-us/azure/cloud-shell/vnet/deployment).

You can deploy Cloud Shell in the same VNet as your AKS private cluster with a dedicated subnet, or you can deploy in a new VNet and connect via [VNet peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

## Configure connection to the private cluster

After you [deploy the required resources](#deploy-required-resources), any user in the subscription can configure their Cloud Shell to deploy in the given VNet using the steps in [Configure Cloud Shell to use a virtual network](/en-us/azure/cloud-shell/vnet/deployment#5-configure-cloud-shell-to-use-a-virtual-network).

Ensure the user has appropriate Kubernetes-level access to successfully connect to the private cluster. For more information, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

## Connect using Azure Bastion (preview)

Azure Bastion is a fully managed PaaS service that you provision to securely connect to private resources via private IP addresses. To use Bastion's native client tunneling feature, see [Connect to AKS private cluster using Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster).

## Connect using virtual network (VNet) peering

To use VNet peering, you need to set up a link between the VNet and the private DNS zone. You can set up VNet peering using either the Azure portal or the Azure CLI.

### Use the Azure portal

In the

[Azure portal](https://portal.azure.com), navigate to your node resource group and select your**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for the virtual network link.**Virtual Network**: Select the virtual network that contains the VM.

Select

**Create**to create the virtual network link.Navigate to the resource group that contains the virtual network of your AKS cluster and select your

**virtual network resource**.In the service menu, under

**Settings**, select**Peerings**>**Add**.On the

**Add peering**page, configure the following settings:**Peering link name**: Enter a name for the peering link.**Virtual network**: Select the virtual network of the VM.

Select

**Add**to create the peering link.

For more information, see [Virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

### Use the Azure CLI

Create a new link to add the virtual network of the VM to the private DNS zone using the

command.`az network private-dns link vnet create`

`az network private-dns link vnet create \ --name <new-link-name> \ --resource-group <node-resource-group-name> \ --zone-name <private-dns-zone-name> \ --virtual-network <vm-virtual-network-resource-id> \ --registration-enabled false`

Create a peering between the virtual network of the VM and the virtual network of the node resource group using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-1> \ --resource-group <vm-virtual-network-resource-group-name> \ --vnet-name <vm-virtual-network-name> \ --remote-vnet <node-resource-group-virtual-network-resource-id> \ --allow-vnet-access`

Create a second peering between the virtual network of the node resource group and the virtual network of the VM using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-2> \ --resource-group <node-resource-group-name> \ --vnet-name <node-resource-group-virtual-network-name> \ --remote-vnet <vm-virtual-network-resource-id> \ --allow-vnet-access`

List the virtual network peerings you created using the

command.`az network vnet peering list`

`az network vnet peering list \ --resource-group <node-resource-group-name> \ --vnet-name <private-dns-zone-name>`


## Use a private endpoint connection

You can set up a private endpoint so that a VNet doesn't need to be peered to communicate with the private cluster. To set up a private endpoint connection, you first create a new private endpoint in the virtual network containing the consuming resources, and then create a link between your virtual network and a new private DNS zone in the same network.

Important

If the virtual network is configured with custom DNS servers, you need to set up private DNS appropriately for the environment. For more information, see the [Virtual network name resolution documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

### Create a private endpoint resource

From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private Endpoint**and select**Create**>**Private Endpoint**.Select

**Create**.On the

**Basics**tab, configure the following settings:**Project details****Subscription**: Select the subscription where your private cluster is located.**Resource group**: Select the resource group that contains your virtual network.

**Instance details****Name**: Enter a name for your private endpoint, such as*myPrivateEndpoint*.**Region**: Select the same region as your virtual network.


Select

**Next: Resource**and configure the following settings:**Connection method**: Select**Connect to an Azure resource in my directory**.**Subscription**: Select the subscription where your private cluster is located.**Resource type**: Select**Microsoft.ContainerService/managedClusters**.**Resource**: Select your private cluster.**Target sub-resource**: Select**management**.

Select

**Next: Virtual Network**and configure the following settings:**Networking****Virtual network**: Select your virtual network.**Subnet**: Select your subnet.


Select

**Next: DNS**>**Next: Tags**and (optionally) set up key-values as needed.Select

**Next: Review + create**>**Create**.

Once the resource is created, record the private IP address of the private endpoint for future use.

### Create a private DNS zone

Once you create the private endpoint, create a new private DNS zone with the same name as the private DNS zone created by the private cluster. Remember to create this DNS zone in the VNet containing the consuming resources.

In the Azure portal, navigate to your node resource group and select your

**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Recordsets**and note the following:- The name of the private DNS zone, which follows the pattern
`*.privatelink.<region>.azmk8s.io`

. - The name of the
`A`

record (excluding the private DNS name). - The time-to-live (TTL).

- The name of the private DNS zone, which follows the pattern
From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private DNS zone**and select**Create**>**Private DNS zone**.On the

**Basics**tab, configure the following settings:**Project details**- Select your
**Subscription**. - Select the
**Resource group**where you created the private endpoint.

- Select your
**Instance details****Name**: Enter the name of the DNS zone retrieved from previous steps.**Region**: Defaults to the location of your resource group.


Select

**Review + create**>**Create**.

### Create an `A`

record

Once the private DNS zone is created, create an `A`

record, which associates the private endpoint to the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Recordsets**>**Add**.On the

**Add record set**page, configure the following settings:**Name**: Enter the name retrieved from the`A`

record in the private cluster's DNS zone.**Type**: Select**A - Address record**.**TTL**: Enter the number from the`A`

record in the private cluster's DNS zone.**TTL unit**: Change the dropdown value to match the one in the`A`

record from the private cluster's DNS zone.**IP address**: Enter the**IP address of the private endpoint you created**.

Select

**Add**to create the`A`

record.

Important

When creating the `A`

record, only use the name and not the fully qualified domain name (FQDN).

### Link the private DNS zone to the virtual network

Once the `A`

record is created, link the private DNS zone to the virtual network that will access the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for your virtual network link.**Subscription**: Select the subscription where your private cluster is located.**Virtual Network**: Select the virtual network of your private cluster.

Select

**Create**to create the link.It might take a few minutes for the operation to complete. Once the virtual network link is created, you can access it from the

**Virtual Network Links**tab you used in step 2.

Warning

- If the private cluster is stopped and restarted, the private cluster's original private link service is removed and recreated, which breaks the connection between your private endpoint and the private cluster. To resolve this issue, delete and recreate any user-created private endpoints linked to the private cluster. If the recreated private endpoints have new IP addresses, you also need to update DNS records.
- If you update the DNS records in the private DNS zone, ensure the host that you're trying to connect from is using the updated DNS records. You can verify this using the
`nslookup`

command. If you notice the updates aren't reflected in the output, you might need to flush the DNS cache on your machine and try again.

## Create a VM in the same virtual network

To create a VM in the same VNet as your private AKS cluster, use the [ az vm create](/en-us/cli/azure/vm#az-vm-create) command with the

`--vnet-name`

flag to specify the VNet.```
az vm create \
--resource-group <resource-group-name> \
--name <vm-name> \
--image <image-name> \
--vnet-name <vm-virtual-network-name> \
--subnet <subnet-name> \
--admin-username <admin-username> \
--admin-password <admin-password>
```


## Use an Express Route or VPN connection

To use an Express Route or VPN connection, see [About ExpressRoute virtual network gateways](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways).

## Use the AKS `command invoke`

feature

To use the AKS `command invoke`

feature to connect to a private cluster, see [Access a private cluster using command invoke](access-private-cluster).

## Related content

For more information about private clusters in AKS, see [Create a private Azure Kubernetes Service (AKS) cluster](private-clusters).

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

## Exclude node pool from Load Balancer backend pool

In certain scenarios, you may want to prevent a node pool from being part of the load balancer’s backend pool. To do this, apply the label `node.kubernetes.io/exclude-from-external-load-balancers=true`

to the node pool.

Note

Although the label resides on individual nodes, it must be applied at the node pool level to ensure long-term persistence.

```
az aks nodepool update \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--name $NODEPOOL_NAME \
--labels node.kubernetes.io/exclude-from-external-load-balancers=true
```


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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-monitoring -->

# Monitor and visualize AI inference metrics on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Monitoring and observability play a key role in maintaining high performance and low cost of your AI workload deployments in Azure Kubernetes Service (AKS). Visibility into system and performance metrics can indicate the limits of your underlying infrastructure and motivate real-time adjustments and optimizations to reduce workload interruptions. Monitoring also provides valuable insights into resource utilization for cost-effective management of computational resources and accurate provisioning.

The Kubernetes AI Toolchain Operator (KAITO) is a managed add-on for AKS that simplifies deployment and operations for AI models in your AKS cluster.

In [KAITO version 0.4.4](https://github.com/kaito-project/kaito/releases/tag/v0.4.4) and later versions, the vLLM inference runtime is enabled by default in the AKS managed add-on. [vLLM](https://docs.vllm.ai/en/latest/) is a library for language model inference and serving. It surfaces key system performance, resource usage, and request processing for [Prometheus metrics](https://docs.vllm.ai/en/latest/design/v1/metrics.html) that you can use to evaluate your KAITO inference deployments.

In this article, you'll learn how to monitor and visualize vLLM inference metrics using the AI toolchain operator add-on with Azure Managed Prometheus and Azure Managed Grafana on your AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Install and configure Azure CLI version 2.47.0 or later. To find your version, run
`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- Install and configure kubectl, the Kubernetes command-line client. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Enable the
[AI toolchain operator add-on](ai-toolchain-operator)in your AKS cluster. - If you already have the AI toolchain operator add-on enabled, update your AKS cluster to the latest version to run KAITO v0.4.4 or later.
- Enable
[the managed service for Prometheus and Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable)in your AKS cluster. - Have permissions to
[create or update Azure Managed Grafana instances](/en-us/azure/managed-grafana/how-to-manage-access-permissions-users-identities)in your Azure subscription.

## Deploy a KAITO inference service

In this example, you collect metrics for the [Qwen-2.5-coder-7B-instruct language model](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).

Start by applying the following KAITO workspace custom resource to your cluster:

`kubectl apply -f https://raw.githubusercontent.com/Azure/kaito/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml`

Track the live resource changes in your KAITO workspace:

`kubectl get workspace workspace-qwen-2-5-coder-7b-instruct -w`

Note

Machine readiness can take up to 10 minutes, and workspace readiness can take up to 20 minutes depending on the size of your language model.

Confirm that your inference service is running and get the service IP address:

`export SERVICE_IP=$(kubectl get svc workspace-qwen-2-5-coder-7b-instruct -o jsonpath='{.spec.clusterIP}') echo $SERVICE_IP`


## Surface KAITO inference metrics to the managed service for Prometheus

Prometheus metrics are collected by default at the KAITO [ /metrics endpoint](https://github.com/kaito-project/kaito/tree/main).

Add the following label to your KAITO inference service so that a Kubernetes

`ServiceMonitor`

deployment can detect it:`kubectl label svc workspace-qwen-2-5-coder-7b-instruct App=qwen-2-5-coder`

Create a

`ServiceMonitor`

resource to define the inference service endpoints and the required configurations to scrape the vLLM Prometheus metrics. Export these metrics to the managed service for Prometheus by deploying the following`ServiceMonitor`

YAML manifest in the`kube-system`

namespace:`cat <<EOF | kubectl apply -n kube-system -f - apiVersion: azmonitoring.coreos.com/v1 kind: ServiceMonitor metadata: name: prometheus-kaito-monitor spec: selector: matchLabels: App: qwen-2-5-coder endpoints: - port: http interval: 30s path: /metrics scheme: http EOF`

Check for the following output to verify that

`ServiceMonitor`

is created:`servicemonitor.azmonitoring.coreos.com/prometheus-kaito-monitor created`

Verify that your

`ServiceMonitor`

deployment is running successfully:`kubectl get servicemonitor prometheus-kaito-monitor -n kube-system`

In the Azure portal, verify that vLLM metrics are successfully collected in the managed service for Prometheus.

In your Azure Monitor workspace, go to

**Managed Prometheus**>**Prometheus explorer**.Select the

**Grid**tab and confirm that a metrics item is associated with the job named`workspace-qwen-2-5-coder-7b-instruct`

.Note

The

`up`

value of this item should be`1`

. A value of`1`

indicates that Prometheus metrics are successfully being scraped from your AI inference service endpoint.


## Visualize KAITO inference metrics in Azure Managed Grafana

The vLLM project provides a Grafana dashboard configuration named

[grafana.json](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)for inference workload monitoring. Navigate to the bottom of this[page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file.Go to the bottom of the

[examples page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file:Complete the steps to

[import the Grafana configurations into a new dashboard](/en-us/azure/managed-grafana/how-to-create-dashboard#import-a-json-dashboard)in Azure Managed Grafana.Go to your Managed Grafana endpoint, view the available dashboards, and select the

**vLLM**dashboard.To begin collecting data for your selected model deployment, confirm that the

**datasource**value shown at the top left of the Grafana dashboard is your instance of the managed service for Prometheus you created for this example.Copy the inference preset name defined in your KAITO workspace to the

**model_name**field in the Grafana dashboard. In this example, the model name is[qwen2.5-coder-7b-instruct](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).In a few moments, verify that the metrics for your KAITO inference service appear in the vLLM Grafana dashboard.

Note

The value of these inference metrics remains

**0**until the requests are submitted to the model inference server.

## Related content

[Monitor and visualize](monitor-aks)your AKS deployments at scale.- Test and monitor
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling)on your cluster. [Fine-tune an AI model](ai-toolchain-operator-fine-tune)by using the AI toolchain operator add-on in AKS.- Learn about AKS GPU workload deployment options on
[Linux](gpu-cluster)and[Windows](use-windows-gpu)nodes.

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

Important

Starting on **September 30, 2027**, Azure Kubernetes Service (AKS) no longer supports the Open Service Mesh (OSM) add-on. The [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/) retired the upstream OSM project. [Migrate any existing OSM configurations to equivalent Istio configurations](/en-us/azure/aks/open-service-mesh-istio-migration-guidance). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/delete-node-pool -->

# Delete an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines node pool deletion in Azure Kubernetes Service (AKS), including what happens when you delete a node pool and how to delete a node pool.

## What happens when you delete a node pool?

When you delete a node pool, the following resources are deleted:

- The virtual machine scale set (VMSS) and virtual machines (VMs) for each node in the node pool
- Any node instances in the node pool along with any pods running on those nodes

## Delete a node pool

Important

Keep the following information in mind when deleting a node pool:

**You can't recover a node pool after it's deleted**. You need to create a new node pool and redeploy your applications.

Delete a node pool using the [ az aks nodepool delete](/en-us/cli/azure/aks#az-aks-nodepool-delete) command.

```
az aks nodepool delete \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name>
```


To verify that the node pool was deleted successfully, use the `kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Ignore PodDisruptionBudgets (PDBs) when removing an existing node pool

If your cluster has PodDisruptionBudgets that are preventing the deletion of the node pool, you can ignore the PodDisruptionBudget requirements by setting `--ignore-pod-disruption-budget`

to `true`

. To learn more about PodDisruptionBudgets, see:

[Plan for availability using a pod disruption budget](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)[Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)[Disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/)

Delete an existing node pool without following any PodDisruptionBudgets set on the cluster using the

command with the`az aks nodepool delete`

`--ignore-pod-disruption-budget`

flag set to`true`

:`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --ignore-pod-disruption-budget true`

To verify that the node pool was deleted successfully, use the

`kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Remove specific VMs in an existing node pool

Note

When you delete a VM with this command, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the VM you plan to delete, perform a cordon and drain on the VM before deleting. You can learn more about how to cordon and drain using the example scenario provided in the resizing node pools tutorial.

List the existing nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-mynodepool-20823458-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000002 Ready agent 63m v1.21.9`

Delete the specified VMs using the

command. Make sure to replace the placeholders with your own values.`az aks nodepool delete-machines`

`az aks nodepool delete-machines \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --machine-names <vm-name-1> <vm-name-2>`

Verify the VMs were successfully deleted using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should no longer include the VMs that you specified in the

`az aks nodepool delete-machines`

command.

## Next steps

For more information about adjusting node pool sizes in AKS, see [Resize node pools](resize-node-pool).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-secure-gateway -->

# Secure ingress gateway for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Deploy external or internal Istio Ingress](istio-deploy-ingress) article describes how to configure an ingress gateway to expose an HTTP service to external/internal traffic. This article shows how to expose a secure HTTPS service using either simple or mutual TLS.

## Prerequisites

Enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)Deploy an external Istio ingress gateway as per

[documentation](istio-deploy-ingress)

Note

This article refers to the external ingress gateway for demonstration, same steps would apply for configuring mutual TLS for internal ingress gateway.

## Required client/server certificates and keys

This article requires several certificates and keys. You can use your favorite tool to create them or you can use the following [openssl](https://man.openbsd.org/openssl.1) commands.

Create a root certificate and private key for signing the certificates for sample services:

`mkdir bookinfo_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=bookinfo Inc./CN=bookinfo.com' -keyout bookinfo_certs/bookinfo.com.key -out bookinfo_certs/bookinfo.com.crt`

Generate a certificate and private key for

`productpage.bookinfo.com`

:`openssl req -out bookinfo_certs/productpage.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/productpage.bookinfo.com.key -subj "/CN=productpage.bookinfo.com/O=product organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 0 -in bookinfo_certs/productpage.bookinfo.com.csr -out bookinfo_certs/productpage.bookinfo.com.crt`

Generate a client certificate and private key:

`openssl req -out bookinfo_certs/client.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/client.bookinfo.com.key -subj "/CN=client.bookinfo.com/O=client organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 1 -in bookinfo_certs/client.bookinfo.com.csr -out bookinfo_certs/client.bookinfo.com.crt`


## Configure a TLS ingress gateway

Create a Kubernetes TLS secret for the ingress gateway; use [Azure Key Vault](/en-us/azure/key-vault/general/basic-concepts) to host certificates/keys and [Azure Key Vault Secrets Provider add-on](csi-secrets-store-driver) to sync secrets to the cluster.

### Set up Azure Key Vault and sync secrets to the cluster

Create Azure Key Vault

You need an

[Azure Key Vault resource](/en-us/azure/key-vault/general/quick-create-cli)to supply the certificate and key inputs to the Istio add-on.`export AKV_NAME=<azure-key-vault-resource-name> az keyvault create --name $AKV_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable

[Azure Key Vault provider for Secret Store CSI Driver](csi-secrets-store-driver)add-on on your cluster.`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER`

If your Key Vault is using Azure RBAC for the permissions model, follow the instructions

[here](/en-us/azure/key-vault/general/rbac-guide#using-azure-rbac-secret-key-and-certificate-permissions-with-key-vault)to assign an Azure role of Key Vault Secrets User for the add-on's user-assigned managed identity. Alternatively, if your key vault is using the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy:`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $AKV_NAME --query 'properties.tenantId') az keyvault set-policy --name $AKV_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys.

`az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-key --file bookinfo_certs/productpage.bookinfo.com.key az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-crt --file bookinfo_certs/productpage.bookinfo.com.crt az keyvault secret set --vault-name $AKV_NAME --name test-bookinfo-crt --file bookinfo_certs/bookinfo.com.crt`

Use the following manifest to deploy SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-productpage-bookinfo-cert-pxf`

is the name of the certificate object in Azure Key Vault. Refer to[obtain certificates and keys](csi-secrets-store-identity-access?pivots=access-with-a-user-assigned-managed-identity#obtain-certificates-and-keys)section for more information.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to deploy a sample pod. The secret store CSI driver requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

as defined in the SecretProviderClass resource.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: tls Data ==== cert: 1066 bytes key: 1704 bytes`


### Configure ingress gateway and virtual service

Route HTTPS traffic via the Istio ingress gateway to the sample applications. Use the following manifest to deploy gateway and virtual service resources.

```
cat <<EOF | kubectl apply -f -
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 443
name: https
protocol: HTTPS
tls:
mode: SIMPLE
credentialName: productpage-credential
hosts:
- productpage.bookinfo.com
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: productpage-vs
spec:
hosts:
- productpage.bookinfo.com
gateways:
- bookinfo-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
port:
number: 9080
host: productpage
EOF
```


Note

In the gateway definition, `credentialName`

must match the `secretName`

in SecretProviderClass resource and `selector`

must refer to the external ingress gateway by its label, in which the key of the label is `istio`

and the value is `aks-istio-ingressgateway-external`

. For internal ingress gateway label is `istio`

and the value is `aks-istio-ingressgateway-internal`

.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export SECURE_INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="https")].port}')
export SECURE_GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$SECURE_INGRESS_PORT_EXTERNAL
echo "https://$SECURE_GATEWAY_URL_EXTERNAL/productpage"
```


### Verification

Send an HTTPS request to access the productpage service through HTTPS:

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


Note

To configure HTTPS ingress access to an HTTPS service, i.e., configure an ingress gateway to perform SNI passthrough instead of TLS termination on incoming requests, update the tls mode in the gateway definition to `PASSTHROUGH`

. This instructs the gateway to pass the ingress traffic “as is”, without terminating TLS.

## Configure a mutual TLS ingress gateway

Extend your gateway definition to support mutual TLS.

Update the ingress gateway credential by deleting the current secret and creating a new one. The server uses the CA certificate to verify its clients, and we must use the key ca.crt to hold the CA certificate.

`kubectl delete secretproviderclass productpage-credential-spc -n aks-istio-ingress kubectl delete secret/productpage-credential -n aks-istio-ingress kubectl delete pod/secrets-store-sync-productpage -n aks-istio-ingress`

Use the following manifest to recreate SecretProviderClass with CA certificate.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: opaque data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt - objectName: test-bookinfo-crt key: ca.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" - | objectName: test-bookinfo-crt objectType: secret objectAlias: "test-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to redeploy sample pod to sync secrets from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: opaque Data ==== ca.crt: 1188 bytes tls.crt: 1066 bytes tls.key: 1704 bytes`


Use the following manifest to update the gateway definition to set the TLS mode to MUTUAL.

`cat <<EOF | kubectl apply -f - apiVersion: networking.istio.io/v1beta1 kind: Gateway metadata: name: bookinfo-gateway spec: selector: istio: aks-istio-ingressgateway-external # use istio default ingress gateway servers: - port: number: 443 name: https protocol: HTTPS tls: mode: MUTUAL credentialName: productpage-credential # must be the same as secret hosts: - productpage.bookinfo.com EOF`


### Verification

Attempt to send HTTPS request using the prior approach - without passing the client certificate - and see it fail.

```
curl -v -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage"
```


Example output:

```
...
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS alert, unknown (628):
* OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
* Failed receiving HTTP2 data
* OpenSSL SSL_write: SSL_ERROR_ZERO_RETURN, errno 0
* Failed sending HTTP2 data
* Connection #0 to host productpage.bookinfo.com left intact
curl: (56) OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
```


Pass your client’s certificate with the `--cert`

flag and private key with the `--key`

flag to curl.

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt --cert bookinfo_certs/client.bookinfo.com.crt --key bookinfo_certs/client.bookinfo.com.key "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-dapr -->

# Quickstart: Deploy an application using the Dapr cluster extension for Azure Kubernetes Service (AKS) or Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the [Dapr cluster extension](dapr-overview) in an AKS or Arc-enabled Kubernetes cluster. You deploy [a hello world example](https://github.com/Azure-Samples/dapr-aks-extension-quickstart), which consists of a Python application that generates messages and a Node.js application that consumes and persists the messages.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.- An AKS Cluster with:
[Workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)enabled[Managed identity](workload-identity-deploy-cluster#create-a-managed-identity)created in the same subscription[A Kubernetes service account](workload-identity-deploy-cluster#create-a-kubernetes-service-account)[Federated identity credential](workload-identity-deploy-cluster#create-the-federated-identity-credential)[Dapr cluster extension](dapr-overview)installed on the AKS cluster

[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)installed locally.

## Clone the repository

Clone the

[Dapr quickstarts repository](https://github.com/Azure-Samples/dapr-aks-extension-quickstart)using the`git clone`

command.`git clone https://github.com/Azure-Samples/dapr-aks-extension-quickstart.git`

Change to the

`dapr-aks-extension-quickstart`

directory.

## Create and configure a Redis store

Open the [Azure portal](https://portal.azure.com/#create/Microsoft.Cache) to start the Azure Cache for Redis creation flow.

- Fill out the recommended information according to
[the "Create an open-source Redis cache" quickstart instructions](/en-us/azure/azure-cache-for-redis/quickstart-create-redis). - Select
**Create**to start the Redis instance deployment.

### Verify resource information

- Once the Redis resource is deployed, navigate to its overview page.
- Take note of:
- The hostname, found in the
**Essentials**section of the cache overview page. The hostname format looks similar to:`xxxxxx.redis.cache.windows.net`

. - The SSL port, found in the cache's
**Advanced Settings**blade. The default value is`6380`

.

- The hostname, found in the
- Navigate to the
**Authentication**blade and verify Microsoft Entra Authentication is enabled on your resource.

### Add managed identity

In the

**Authentication**blade, type the name of the[Managed Identity you created as a prerequisite](#prerequisites)in the field under**Enable Microsoft Entra Authentication**checkbox.Verify your managed identity is added as a Redis User assigned Data Owner Access Policy permissions.


### Enable public network access

For this scenario, your Redis cache uses public network access. Be sure to [clean up resources](#clean-up-resources) when you're finished with this quickstart.

- Navigate to the
**Private Endpoint**blade. - Click
**Enable public network access**from the top menu.

## Configure the Dapr components

In `redis.yaml`

, the component is configured to use Entra ID Authentication using workload identity enabled for AKS cluster. No access keys are required.

```
- name: useEntraID
value: "true"
- name: enableTLS
value: true
```


In your preferred code editor, navigate to the

`deploy`

directory in the sample and open`redis.yaml`

.For

`redisHost`

, replace the placeholder`<REDIS_HOST>:<REDIS_PORT>`

value with the Redis cache hostname and SSL port[you saved earlier from Azure portal](#verify-resource-information).`- name: redisHost value: <your-cache-name>.redis.cache.windows.net:6380`


### Apply the configuration

Apply the

`redis.yaml`

file using the`kubectl apply`

command.`kubectl apply -f ./deploy/redis.yaml`

Verify your state store was successfully configured using the

`kubectl get components.redis`

command.`kubectl get components.redis -o yaml`

**Expected output**`component.dapr.io/statestore created`


## Deploy the Node.js app with the Dapr sidecar

### Configure the Node.js app

In `node.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`node.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Apply the Node.js app deployment to your cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/node.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/nodeapp`

Access your service using the

`kubectl get svc`

command.`kubectl get svc nodeapp`

Make note of the

`EXTERNAL-IP`

in the output.

### Verify the Node.js service

Using

`curl`

, call the service with your`EXTERNAL-IP`

.`curl $EXTERNAL_IP/ports`

**Example output**`{"DAPR_HTTP_PORT":"3500","DAPR_GRPC_PORT":"50001"}`

Submit an order to the application.

`curl --request POST --data "@sample.json" --header Content-Type:application/json $EXTERNAL_IP/neworder`

Confirm the order.

`curl $EXTERNAL_IP/order`

**Expected output**`{ "orderId": "42" }`


## Deploy the Python app with the Dapr sidecar

### Configure the Python app

In `python.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`python.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Deploy the Python app to your Kubernetes cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/python.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/pythonapp`


## Observe messages and confirm persistence

Now that both the Node.js and Python applications are deployed, you can watch messages come through.

Get the logs of the Node.js app using the

`kubectl logs`

command.`kubectl logs --selector=app=node -c node --tail=-1`

**Expected output**`Got a new order! Order ID: 1 Successfully persisted state Got a new order! Order ID: 2 Successfully persisted state Got a new order! Order ID: 3 Successfully persisted state`

Using

`curl`

, call the Node.js app's order endpoint to get the latest order.`curl $EXTERNAL_IP/order`

You should see the latest JSON output in the response.


## Clean up resources

If you no longer plan to use the resources from this quickstart, you can delete all associated resources by removing the resource group.

Remove the resource group, cluster, namespace, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name MyResourceGroup
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-arm -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to deploy the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using an [ARM template](/en-us/azure/azure-resource-manager/templates/).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - This article assumes you have an existing Azure resource group. If you don't have an existing resource group, you can create one using the
command.`az group create`

- Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules). [Create an SSH key pair](#create-an-ssh-key-pair).

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

## Create an SSH key pair

Navigate to the

[Azure Cloud Shell](https://shell.azure.com/).Create an SSH key pair using the

command.`az sshkey create`

`az sshkey create --name <sshkey-name> --resource-group <resource-group-name>`


## Enable the KEDA add-on with an ARM template

Deploy the

[ARM template for an AKS cluster](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.kubernetes%2Faks%2Fazuredeploy.json).Select

**Edit template**.Enable the KEDA add-on by specifying the

`workloadAutoScalerProfile`

field in the ARM template, as shown in the following example:`"workloadAutoScalerProfile": { "keda": { "enabled": true } }`

Select

**Save**.Update the required values for the ARM template:

**Subscription**: Select the Azure subscription to use for the deployment.**Resource group**: Select the resource group to use for the deployment.**Region**: Select the region to use for the deployment.**Dns Prefix**: Enter a unique DNS name to use for the cluster.**Linux Admin Username**: Enter a username for the cluster.**SSH public key source**: Select**Use existing key stored in Azure**.**Store Keys**: Select the key pair you created earlier in the article.

Select

**Review + create**>**Create**.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local device, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client.

If you use the Azure Cloud Shell, `kubectl`

is already installed. You can also install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

- Configure
`kubectl`

to connect to your Kubernetes cluster, use the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following example gets credentials for the AKS cluster named*MyAKSCluster*in the*MyResourceGroup*:

```
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```


## Example deployment

The following snippet is a sample deployment that creates a cluster with KEDA enabled with a single node pool comprised of three `DS2_v5`

nodes.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"resources": [
{
"apiVersion": "2023-03-01",
"dependsOn": [],
"type": "Microsoft.ContainerService/managedClusters",
"location": "westcentralus",
"name": "myAKSCluster",
"properties": {
"kubernetesVersion": "1.27",
"enableRBAC": true,
"dnsPrefix": "myAKSCluster",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": 200,
"count": 3,
"enableAutoScaling": false,
"vmSize": "Standard_D2S_v5",
"osType": "Linux",
"type": "VirtualMachineScaleSets",
"mode": "System",
"maxPods": 110,
"availabilityZones": [],
"nodeTaints": [],
"enableNodePublicIP": false
}
],
"networkProfile": {
"loadBalancerSku": "standard",
"networkPlugin": "kubenet"
},
"workloadAutoScalerProfile": {
"keda": {
"enabled": true
}
}
},
"identity": {
"type": "SystemAssigned"
}
}
]
}
```


## Start scaling apps with KEDA

You can autoscale your apps with KEDA using custom resource definitions (CRDs). For more information, see the [KEDA documentation](https://keda.sh/docs/scalers/).

## Remove resources

Remove the resource group and all related resources using the

command.`az group delete`

`az group delete --name <resource-group-name>`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster, and then verify that it's installed and running. With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges -->

# Secure access to the API server using authorized IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use API server authorized IP address ranges to limit which IP addresses and CIDRs can access control plane endpoints for your Azure Kubernetes Service (AKS) workloads.

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To learn what IP addresses to include when integrating your AKS cluster with Azure DevOps, see
[Allowed IP addresses and domain URLs](/en-us/azure/devops/organizations/security/allow-list-ip-url).

Tip

From the Azure portal, you can use Azure Copilot to make changes to the IP addresses that can access your cluster. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#enable-ip-address-authorization).

## Limitations and considerations

- This feature is only supported on the Standard SKU load balancer for clusters created after October 2019. Any existing clusters on the Basic SKU load balancer with the feature enabled should continue to work properly if the Kubernetes version and control plane are upgraded. However, you can't migrate these clusters to the Standard SKU load balancer.
- You can't use this feature with
[private clusters](private-clusters). - When using this feature with clusters that use
[Node public IPs](use-node-public-ips), the node pools using the Node public IPs must use public IP prefixes. You must add the public IP prefixes as authorized ranges. - You can specify up to 200 authorized IP ranges. To go beyond this limit, consider using
[API Server VNet Integration](api-server-vnet-integration), which supports up to 2,000 authorized IP ranges.

## Overview of API server authorized IP ranges

The Kubernetes API server exposes underlying Kubernetes APIs and provides the interaction for management tools like `kubectl`

and the Kubernetes dashboard. AKS provides a single-tenant cluster control plane with a dedicated API server. The API server is assigned a public IP address by default. You can control access using Kubernetes role-based access control (Kubernetes RBAC) or Azure RBAC.

To secure access to the otherwise publicly accessible AKS control plane / API server, you can enable and use authorized IP ranges. These authorized IP ranges only allow defined IP address ranges to communicate with the API server. Any requests made to the API server from an IP address that isn't part of these authorized IP ranges is blocked. The rules can take up to two minutes to propagate. Allow up to that time when testing the connection.

## Recommended IP ranges to allow

We recommend including the following IP address ranges in your API server authorized IP ranges configuration:

- The cluster egress IP address (firewall, NAT gateway, or other address, depending on your
[outbound type](egress-outboundtype)). - Any range that represents networks that you'll administer the cluster from.

## Create an AKS cluster with API server authorized IP ranges enabled

Note

When you enable API server authorized IP ranges during cluster creation, both the API server public IP and the outbound public IP of the [Standard SKU load balancer](load-balancer-standard) are automatically allowed by default, in addition to any ranges you specify.

**Special case - 0.0.0.0/32**: This is a special value that tells AKS to allow only the outbound public IP of the Standard SKU load balancer to access the API server. The

`0.0.0.0/32`

value acts as a placeholder that:- Disables the default behavior of allowing extra client IP ranges.
- Restricts API server access to only the cluster's own outbound IP.
- Is useful for scenarios where you want the cluster to self-manage but block external access.

When creating a cluster with API server authorized IP ranges enabled, you provide a list of authorized public IP address ranges. When you specify a CIDR range, you must use the network address (first IP address in the range). For example, if you want to allow the range `137.117.106.88`

to `137.117.106.95`

, you must specify `137.117.106.88/29`

.

Create an AKS cluster with API server authorized IP ranges enabled using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled using the

cmdlet with the`New-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '73.140.245.0/24' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter the IP address ranges you want to authorize to access the API server. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Specify outbound IPs for a Standard SKU load balancer

When creating a cluster with API server authorized IP ranges enabled, you can also specify the outbound IP addresses or prefixes for the cluster using the `--load-balancer-outbound-ips`

or `--load-balancer-outbound-ip-prefixes`

parameters. All IPs provided in the parameters are allowed along with the IPs in the `--api-server-authorized-ip-ranges`

parameter.

Create an AKS cluster with API server authorized IP ranges enabled and specify the outbound IP addresses for the Standard SKU load balancer using the

`--load-balancer-outbound-ips`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*, allows the IP address range`73.140.245.0/24`

to access the API server, and specifies two outbound IP addresses for the Standard SKU load balancer. Make sure to replace the placeholders`<public-ip-id-1>`

and`<public-ip-id-2>`

with the actual resource IDs of your public IP addresses.`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --load-balancer-outbound-ips <public-ip-id-1>,<public-ip-id-2> --generate-ssh-keys`


## Allow only the outbound public IP of the Standard SKU load balancer

Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 0.0.0.0/32 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '0.0.0.0/32' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter`0.0.0.0/32`

. This setting allows only the outbound public IP of the Standard SKU load balancer. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Update the API server authorized IP ranges on an existing cluster

Update an existing cluster's API server authorized IP ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24`


## Allow multiple IP address ranges

To allow multiple IP address ranges, you can list several IP addresses, separated by commas.

Update an existing cluster's API server authorized IP ranges to allow multiple IP address ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows multiple IP address ranges:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24,193.168.1.0/24,194.168.1.0/24`


Update an existing cluster's API server authorized IP ranges using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '73.140.245.0/24'`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, update the**Authorized IP ranges**as needed. - When you're done, select
**Save**.

## Disable API server authorized IP ranges on an existing cluster

Disable API server authorized IP ranges using the

command and specify an empty range`az aks update`

`""`

for the`--api-server-authorized-ip-ranges`

parameter.`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges ""`


Disable API server authorized IP ranges using the

cmdlet and specify an empty range`Set-AzAksCluster`

`''`

for the`-ApiServerAccessAuthorizedIpRange`

parameter.`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange ''`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, deselect the**Set authorized IP ranges**checkbox. - Select
**Save**.

## Find existing API server authorized IP ranges

Find existing API server authorized IP ranges using the

command with the`az aks show`

`--query`

parameter set to`apiServerAccessProfile.authorizedIpRanges`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query apiServerAccessProfile.authorizedIpRanges`

Example output:

`[ "73.140.245.0/24" ]`


Find existing API server authorized IP ranges using the

cmdlet.`Get-AzAksCluster`

`Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster | Select-Object -ExpandProperty ApiServerAccessProfile`

Example output:

`AuthorizedIPRanges: {73.140.245.0/24} ...`


Navigate to the Azure portal and select your AKS cluster.

From the service menu, under

**Settings**, select**Networking**. The existing API server authorized IP ranges are listed under**Resource settings**.

## Access the API server from your development machine, tooling, or automation

You must add your development machines, tooling, or automation IP addresses to the AKS cluster list of approved IP ranges to access the API server from there.

Another option is to configure a jumpbox with the necessary tooling inside a separate subnet in the firewall's virtual network. This option assumes your environment has a firewall with the respective network and that you added the firewall IPs to authorized ranges. Similarly, if you forced tunneling from the AKS subnet to the firewall subnet, having the jumpbox in the cluster subnet also works.

Note

The following example adds another IP address to the approved ranges. It still includes the existing IP address. If you don't include your existing IP address, this command replaces it with the new one instead of adding it to the authorized ranges.

Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges $CURRENT_IP/24,73.140.245.0/24`


Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '$CURRENT_IP/24,73.140.245.0/24'`


Another option is to use the following command on Windows systems to get the public IPv4 address:

```
Invoke-RestMethod http://ipinfo.io/json | Select -exp ip
```


You can also follow the steps in [Find your IP address](https://support.microsoft.com/help/4026518/windows-10-find-your-ip-address) or search on *what is my IP address?* in an internet browser.

## Related content

To learn more about security in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/internal-lb -->

# Use an internal load balancer with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can create and use an internal load balancer to restrict access to your applications in Azure Kubernetes Service (AKS). An internal load balancer doesn't have a public IP and makes a Kubernetes service accessible only to applications that can reach the private IP. These applications can be within the same virtual network or in another virtual network through virtual network peering. This article shows you how to create and use an internal load balancer with AKS.

Important

Starting on **September 30, 2025**, Azure Kubernetes Service (AKS) no longer supports Basic Load Balancer. To avoid any potential service disruptions, we recommend using Standard Load Balancer for new deployments and [upgrading any existing deployments to the Standard Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance). For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5020) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.0.59 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you want to use an existing subnet or resource group, the AKS cluster identity needs permission to manage network resources. For information, see
[Configure Azure CNI networking in AKS](configure-azure-cni). If you're configuring your load balancer to use an[IP address in a different subnet](#specify-a-different-subnet), ensure the AKS cluster identity also has`Read`

access to that subnet.- For more information on permissions, see
[Delegate AKS access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources).

- For more information on permissions, see

## Create an internal load balancer

Create a service manifest named

`internal-lb.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

annotation.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster.`kubectl apply`

`kubectl apply -f internal-lb.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address. This IP address is dynamically assigned from the same subnet as the AKS cluster.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.248.59 10.240.0.7 80:30555/TCP 2m`


## Specify an IP address

When you specify an IP address for the load balancer, the specified IP address must reside in the same virtual network as the AKS cluster, but it can't already be assigned to another resource in the virtual network. For example, you shouldn't use an IP address in the range designated for the Kubernetes subnet within the AKS cluster. Using an IP address that's already assigned to another resource in the same virtual network can cause issues with the load balancer.

You can use the [ az network vnet subnet list](/en-us/cli/azure/network/vnet/subnet#az-network-vnet-subnet-list) Azure CLI command or the

[PowerShell cmdlet to get the subnets in your virtual network.](/en-us/powershell/module/az.network/get-azvirtualnetworksubnetconfig)

`Get-AzVirtualNetworkSubnetConfig`

For more information on subnets, see [Add a node pool with a unique subnet](node-pool-unique-subnet).

If you want to use a specific IP address with the load balancer, you have two options: **set service annotations** or **add the LoadBalancerIP property to the load balancer YAML manifest**.

Important

Adding the *LoadBalancerIP* property to the load balancer YAML manifest is deprecating following [upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we **highly recommend setting service annotations** instead. For more information about service annotations, see [Azure LoadBalancer supported annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations).

Set service annotations using

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-ipv4: 10.240.0.25 service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address in the

`EXTERNAL-IP`

column should reflect your specified IP address, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.184.168 10.240.0.25 80:30225/TCP 4m`


For more information on configuring your load balancer in a different subnet, see [Specify a different subnet](#specify-a-different-subnet).

## Connect Azure Private Link service to internal load balancer

### Before you begin

- You need Kubernetes version 1.22.x or later.
- You need an existing resource group with a virtual network and subnet. This resource group is where you
[create the private endpoint](#create-a-private-endpoint-to-the-private-link-service). If you don't have these resources, see[Create a virtual network and subnet](configure-kubenet#create-a-virtual-network-and-subnet).

### Create a Private Link service connection

Create a service manifest named

`internal-lb-pls.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

and`azure-pls-create`

annotations. For more options, refer to the[Azure Private Link Service Integration](https://kubernetes-sigs.github.io/cloud-provider-azure/topics/pls-integration/)design document.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-pls-create: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster. It also creates a Private Link Service object that connects to the frontend IP configuration of the load balancer associated with the Kubernetes service.`kubectl apply`

`kubectl apply -f internal-lb-pls.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.125.17.53 10.125.0.66 80:30430/TCP 64m`

View the details of the Private Link Service object using the

command.`az network private-link-service list`

`# Create a variable for the node resource group AKS_MC_RG=$(az aks show -g myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv) # View the details of the Private Link Service object az network private-link-service list -g $AKS_MC_RG --query "[].{Name:name,Alias:alias}" -o table`

Your output should look similar to the following example output:

`Name Alias -------- ------------------------------------------------------------------------- pls-xyz pls-xyz.abc123-defg-4hij-56kl-789mnop.eastus2.azure.privatelinkservice`


### Create a Private Endpoint to the Private Link service

A Private Endpoint allows you to privately connect to your Kubernetes service object via the Private Link Service you created.

Create the private endpoint using the

command.`az network private-endpoint create`

`# Create a variable for the private link service AKS_PLS_ID=$(az network private-link-service list -g $AKS_MC_RG --query "[].id" -o tsv) # Create the private endpoint $ az network private-endpoint create \ -g myOtherResourceGroup \ --name myAKSServicePE \ --vnet-name myOtherVNET \ --subnet pe-subnet \ --private-connection-resource-id $AKS_PLS_ID \ --connection-name connectToMyK8sService`


### PLS Customizations via Annotations

You can use the following annotations to customize the PLS resource:

| Annotation | Value | Description | Required | Default |
|---|---|---|---|---|
`service.beta.kubernetes.io/azure-pls-create` |
`"true"` |
Boolean indicating whether a PLS needs to be created. | Required | |
`service.beta.kubernetes.io/azure-pls-name` |
`<PLS name>` |
String specifying the name of the PLS resource to be created. | Optional | `"pls-<LB frontend config name>"` |
`service.beta.kubernetes.io/azure-pls-resource-group` |
`Resource Group name` |
String specifying the name of the Resource Group where the PLS resource is created | Optional | `MC_ resource` |
`service.beta.kubernetes.io/azure-pls-ip-configuration-subnet` |
`<Subnet name>` |
String indicating the subnet to which the PLS is deployed. This subnet must exist in the same virtual network as the backend pool. PLS NAT IPs are allocated within this subnet. | Optional | If `service.beta.kubernetes.io/azure-load-balancer-internal-subnet` , this ILB subnet is used. Otherwise, the default subnet from config file is used. |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` |
`[1-8]` |
Total number of private NAT IPs to allocate. | Optional | 1 |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address` |
`"10.0.0.7 ... 10.0.0.10"` |
A space separated list of static IPv4 IPs to be allocated. (IPv6 isn't supported right now.) Total number of IPs shouldn't be greater than the ip count specified in `service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` . If there are fewer IPs specified, the rest are dynamically allocated. The first IP in the list is set as `Primary` . |
Optional | All IPs are dynamically allocated. |
`service.beta.kubernetes.io/azure-pls-proxy-protocol` |
`"true"` or `"false"` |
Boolean indicating whether the TCP PROXY protocol should be enabled on the PLS to pass through connection information, including the link ID and source IP address. The backend service MUST support the PROXY protocol or the connections fails. | Optional | `false` |
`service.beta.kubernetes.io/azure-pls-visibility` |
`"sub1 sub2 sub3 … subN"` or `"*"` |
A space separated list of Azure subscription IDs for which the private link service is visible. Use `"*"` to expose the PLS to all subs (Least restrictive). |
Optional | Empty list `[]` indicating role-based access control only: This private link service is only available to individuals with role-based access control permissions within your directory. (Most restrictive) |
`service.beta.kubernetes.io/azure-pls-auto-approval` |
`"sub1 sub2 sub3 … subN"` |
A space separated list of Azure subscription IDs. This allows PE connection requests from the subscriptions listed to the PLS to be automatically approved. This only works when visibility is set to `"*"` . |
Optional | `[]` |

## Use private networks

When you create your AKS cluster, you can specify advanced networking settings. These settings allow you to deploy the cluster into an existing Azure virtual network and subnets. For example, you can deploy your AKS cluster into a private network connected to your on-premises environment and run services that are only accessible internally.

For more information, see [configure your own virtual network subnets with Kubenet](configure-kubenet) or [with Azure CNI](configure-azure-cni).

You don't need to make any changes to the previous steps to deploy an internal load balancer that uses a private network in an AKS cluster. The load balancer is created in the same resource group as your AKS cluster, but it's instead connected to your private virtual network and subnet, as shown in the following example:

```
$ kubectl get service internal-app
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
internal-app LoadBalancer 10.1.15.188 10.0.0.35 80:31669/TCP 1m
```


Note

The cluster identity used by the AKS cluster must at least have the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) role on the virtual network resource. You can view the cluster identity using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command, such as

`az aks show --resource-group <resource-group-name> --name <cluster-name> --query "identity"`

. You can assign the Network Contributor role using the [command, such as](/en-us/cli/azure/role/assignment#az-role-assignment-create)

`az role assignment create`

`az role assignment create --assignee <identity-resource-id> --scope <virtual-network-resource-id> --role "Network Contributor"`

.If you want to define a [custom role](/en-us/azure/role-based-access-control/custom-roles-cli) instead, you need the following permissions:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


For more information, see [Add, change, or delete a virtual network subnet](/en-us/azure/virtual-network/virtual-network-manage-subnet).

### Specify a different subnet

Add the

`azure-load-balancer-internal-subnet`

annotation to your service to specify a subnet for your load balancer. The subnet specified must be in the same virtual network as your AKS cluster. When deployed, the load balancer`EXTERNAL-IP`

address is part of the specified subnet.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "apps-subnet" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


## Delete the load balancer

The load balancer is deleted when all of its services are deleted.

As with any Kubernetes resource, you can directly delete a service, such as `kubectl delete service internal-app`

, which also deletes the underlying Azure load balancer.

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/custom-node-configuration -->

# Customize the node configuration for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Customizing your node configuration allows you to adjust operating system (OS) settings or kubelet parameters to match the needs of your workloads. When you create an AKS cluster or add a node pool to your cluster, you can customize a subset of commonly used OS and kubelet settings. To configure settings beyond this subset, you can [use a daemon set to customize your needed configurations without losing AKS support for your nodes](support-policies#shared-responsibility).

## Create custom node configuration files for AKS node pools

OS and kubelet configuration changes require you to create a new configuration file with the parameters and your desired settings. If a value for a parameter isn't specified, then the value is set to the default.

Note

The following examples show common configuration settings. You can modify the settings to meet your workload requirements. For a full list of supported custom configuration parameters, see the [Supported custom configuration parameters](#supported-custom-configuration-parameters) section.

### Kubelet configuration

Create a `linuxkubeletconfig.json`

file with the following contents:

```
{
"cpuManagerPolicy": "static",
"cpuCfsQuota": true,
"cpuCfsQuotaPeriod": "200ms",
"imageGcHighThreshold": 90,
"imageGcLowThreshold": 70,
"topologyManagerPolicy": "best-effort",
"allowedUnsafeSysctls": [
"kernel.msg*",
"net.*"
],
"failSwapOn": false
}
```


### OS configuration

Create a `linuxosconfig.json`

file with the following contents:

```
{
"transparentHugePageEnabled": "madvise",
"transparentHugePageDefrag": "defer+madvise",
"swapFileSizeMB": 1500,
"sysctls": {
"netCoreSomaxconn": 163849,
"netIpv4TcpTwReuse": true,
"netIpv4IpLocalPortRange": "32000 60000"
}
}
```


## Create an AKS cluster using custom configuration files

Note

Keep the following information in mind when using custom configuration files when creating a new AKS cluster:

- If you specify a configuration when creating a cluster, the configuration applies only to the nodes in the initial node pool. Any settings not configured in the JSON file retain their default values.
`CustomLinuxOsConfig`

isn't supported for the Windows OS type.

Create a new cluster using custom configuration files using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new cluster with the custom `./linuxkubeletconfig.json`

and `./linuxosconfig.json`

files:```
az aks create --name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json --linux-os-config ./linuxosconfig.json
```


## Add a node pool using custom configuration files

Note

Keep the following information in mind when using custom configuration files when adding a new node pool to an existing AKS cluster:

- When you add a Linux node pool to an existing cluster, you can specify the kubelet configuration, OS configuration, or both. When you add a Windows node pool to an existing cluster, you can only specify the kubelet configuration. If you specify a configuration when adding a node pool, the configuration applies only to the nodes in the new node pool. Any settings not configured in the JSON file retain their default values.
`CustomKubeletConfig`

is supported for Linux and Windows node pools.

Create a new Linux node pool using the [ az aks nodepool add](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new Linux node pool with the custom `./linuxkubeletconfig.json`

file:```
az aks nodepool add --name <node-pool-name> --cluster-name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json
```


## Confirm settings were applied

After you apply custom node configuration, you can confirm the settings were applied to the nodes by [connecting to the host](node-access) and verifying `sysctl`

or configuration changes were made on the filesystem.

## Supported custom configuration parameters

### Linux kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`cpuManagerPolicy` |
none, static | none | The static policy allows containers in
|

`cpuCfsQuota`

`cpuCfsQuotaPeriod`

`100ms`

`imageGcHighThreshold`

`imageGcLowThreshold`

`imageGcHighThreshold`

*can*trigger garbage collection.`topologyManagerPolicy`

[Control Topology Management Policies on a node](https://kubernetes.io/docs/tasks/administer-cluster/topology-manager/).`allowedUnsafeSysctls`

`kernel.shm*`

, `kernel.msg*`

, `kernel.sem`

, `fs.mqueue.*`

, `net.*`

`containerLogMaxSizeMB`

`containerLogMaxFiles`

`podMaxPids`

`seccompDefault`

`Unconfined`

, `RuntimeDefault`

`Unconfined`

`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls fail. `Unconfined`

places no restrictions on syscalls, allowing all system calls and reducing security. For more information, see the [containerd default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51). This parameter is in preview.[Register](/en-us/azure/azure-resource-manager/management/preview-features?tabs=azure-cli#register-preview-feature)the "KubeletDefaultSeccompProfilePreview" feature flag using the[command with](/en-us/cli/azure/feature#az-feature-register)`az feature register`

`--namespace "Microsoft.ContainerService"`

.### Windows kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`imageGcHighThreshold` |
0-100 | 85 | The percent of disk usage after which image garbage collection is always run. Minimum disk usage that triggers garbage collection. To disable image garbage collection, set to 100. |
`imageGcLowThreshold` |
0-100, no higher than `imageGcHighThreshold` |
80 | The percent of disk usage before which image garbage collection is never run. Minimum disk usage that can trigger garbage collection. |
`containerLogMaxSizeMB` |
Size in megabytes (MB) | 10 | The maximum size (for example, 10 MB) of a container log file before it gets rotated. |
`containerLogMaxFiles` |
≥ 2 | 5 | The maximum number of container log files that can be present for a container. |

## Linux custom OS configuration settings

Important

To simplify search and readability, the OS settings are displayed in this article by their name, but they should be added to the configuration JSON file or AKS API using the [camelCase capitalization convention](/en-us/dotnet/standard/design-guidelines/capitalization-conventions).

For example, if you modify the `vm.max_map_count setting`

, you should reformat to `vmMaxMapCount`

in the configuration JSON file.

### Linux file handle limits

When serving high amounts of traffic, that traffic commonly comes from a large number of local files. You can adjust the following kernel settings and built-in limits to allow you to handle more, at the cost of some system memory.

The following table lists the file handle limits that you can customize per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`fs.file-max` |
8192 - 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | Maximum number of file-handles that the Linux kernel allocates. This value is set to the maximum possible value (2^63-1) to prevent file descriptor exhaustion and ensure unlimited system-wide file handles for containerized workloads. |
`fs.inotify.max_user_watches` |
781250 - 2097152 | 1048576 | 1048576 | 1048576 | Maximum number of file watches allowed by the system. Each watch is roughly 90 bytes on a 32-bit kernel, and roughly 160 bytes on a 64-bit kernel. |
`fs.aio-max-nr` |
65536 - 6553500 | 65536 | 65536 | 65536 | The aio-nr shows the current system-wide number of asynchronous io requests. aio-max-nr allows you to change the maximum value aio-nr can grow to. |
`fs.nr_open` |
8192 - 20000500 | 1048576 | 1048576 | 1073741816 | The maximum number of file-handles a process can allocate. |

Note

The `fs.file-max`

parameter is set to 9223372036854775807 (the maximum value for a signed 64-bit integer) across Ubuntu and Azure Linux based on upstream defaults. This configuration:

**Prevents denial-of-service attacks**based on system-wide file descriptor exhaustion.**Ensures container workloads**are never bottlenecked by system-wide file handle limits.**Maintains security**through per-process limits (`fs.nr_open`

and`ulimit`

) which still apply to individual processes.**Optimizes for container platforms**where many containers might run simultaneously, each potentially opening many files and network connection.

### Linux socket and network tuning

For agent nodes, which are expected to handle large numbers of concurrent sessions, you can use following TCP and network options and adjust them per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`net.core.somaxconn` |
4096 - 3240000 | 16384 | 16384 | 16384 | Maximum number of connection requests that can be queued for any given listening socket. An upper limit for the value of the backlog parameter passed to the
`somaxconn` , then it's silently truncated to this limit. |

`net.core.netdev_max_backlog`

`net.core.rmem_max`

`net.core.wmem_max`

`net.core.optmem_max`

`net.ipv4.tcp_max_syn_backlog`

`net.ipv4.tcp_max_tw_buckets`

`timewait`

sockets held by system simultaneously. If this number is exceeded, time-wait socket is immediately destroyed and warning is printed.`net.ipv4.tcp_fin_timeout`

`net.ipv4.tcp_keepalive_time`

`keepalive`

messages when `keepalive`

is enabled.`net.ipv4.tcp_keepalive_probes`

`keepalive`

probes TCP sends out, until it decides that the connection is broken.`net.ipv4.tcp_keepalive_intvl`

`tcp_keepalive_probes`

it makes up the time to kill a connection that isn't responding, after probes started.`net.ipv4.tcp_tw_reuse`

`TIME-WAIT`

sockets for new connections when it's safe from protocol viewpoint.`net.ipv4.ip_local_port_range`

`net.ipv4.neigh.default.gc_thresh1`

`net.ipv4.neigh.default.gc_thresh2`

`net.ipv4.neigh.default.gc_thresh3`

`net.netfilter.nf_conntrack_max`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_max`

is the maximum number of nodes in the hash table, that is, the maximum number of connections supported by the `nf_conntrack`

module or the size of connection tracking table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

(or `RAM_in_MB * 64`

). For example, a VM with 8 GB RAM has a default of approximately 524,288 connections. Actual values vary based on the VM size and available memory.`net.netfilter.nf_conntrack_buckets`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_buckets`

is the size of hash table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

, with a minimum of 1,024 buckets and a maximum of 262,144 buckets. The default `nf_conntrack_max`

is typically set to `nf_conntrack_buckets * 4`

. Actual values vary based on the VM size and available memory.### Linux worker limits

Like file descriptor limits, the number of workers or threads that a process can create are limited by both a kernel setting and user limits. The user limit on AKS is unlimited. The following table lists the kernel setting that you can customize per node pool:

| Setting | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|
`kernel.threads-max` |
Dynamically calculated | Dynamically calculated | Dynamically calculated | Processes can spin up worker threads. The maximum number of all threads that can be created is set with the kernel setting `kernel.threads-max` . Default value is dynamically calculated based on system memory using the formula: `total_ram_pages / 4` (where each page is typically 4 KB). Actual values vary based on the VM size and available memory. |

### Linux virtual memory

The following table lists the kernel settings that you can customize per node pool to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the `writeout`

of dirty data to disk:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`vm.max_map_count` |
65530 | 1048576 | 1048576 | This file contains the maximum number of memory map areas a process can have. Memory map areas are used as a side-effect of calling `malloc` , directly by `mmap` , `mprotect` , and `madvise` , and also when loading shared libraries. |
|
`vm.vfs_cache_pressure` |
1 - 100 | 100 | 100 | 100 | This percentage value controls the tendency of the kernel to reclaim the memory, which is used for caching of directory and inode objects. |
`vm.swappiness` |
0 - 100 | 60 | 60 | 60 | This control is used to define how aggressively the kernel swaps memory pages. Higher values increase aggressiveness, lower values decrease the amount of swap. A value of 0 instructs the kernel not to initiate swap until the amount of free and file-backed pages is less than the high water mark in a zone. |
`swapFileSizeMB` |
1 MB - Size of the
|

`transparentHugePageEnabled`

`always`

, `madvise`

, `never`

`always`

`always`

`madvise`

[Transparent Hugepages](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html#admin-guide-transhuge)is a Linux kernel feature intended to improve performance by making more efficient use of your processor's memory-mapping hardware. When enabled the kernel attempts to allocate`hugepages`

whenever possible and any Linux process receives 2-MB pages if the `mmap`

region is 2 MB naturally aligned. In certain cases when `hugepages`

are enabled system wide, applications might end up allocating more memory resources. An application might `mmap`

a large region but only touch 1 byte of it, in that case a 2-MB page might be allocated instead of a 4k page for no good reason. This scenario is why it's possible to disable `hugepages`

system-wide or to only have them inside `MADV_HUGEPAGE madvise`

regions.`transparentHugePageDefrag`

`always`

, `defer`

, `defer+madvise`

, `madvise`

, `never`

`madvise`

`madvise`

`madvise`

`hugepages`

available.## Related content

- Learn
[how to configure your AKS cluster](concepts-clusters-workloads). - Learn how
[upgrade the node images](node-image-upgrade)in your cluster. - See
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-cluster)to learn how to upgrade your cluster to the latest version of Kubernetes. - See the list of
[Frequently asked questions about AKS](faq)to find answers to some common AKS questions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring Your Own (BYO) CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## IP address planning considerations

When using a Bring Your Own CNI (BYO CNI) plugin with AKS, IP address planning responsibilities are split between AKS and the customer-managed CNI. Unlike AKS-managed CNI plugins, AKS doesn't allocate or manage pod IP addresses when a BYO CNI is used.

Note

The [IP address planning for your Azure Kubernetes Service (AKS) clusters](concepts-network-ip-address-planning) article focuses on AKS-managed networking plugins. In BYO CNI scenarios, only guidance related to node subnet sizing, upgrade and scaling behavior, and Kubernetes service address ranges is applicable. Pod IP address allocation, routing, and scaling behavior are determined by the selected CNI plugin.

### Virtual network and subnet sizing

AKS still requires a virtual network and subnet to host cluster nodes. Subnet sizing should account for:

- The maximum number of nodes per node pool
- Additional nodes required for upgrade and scale operations, such as surge upgrades
- Azure resources that allocate IP addresses from subnets in the virtual network, such as internal load balancers

AKS upgrades and scaling operations remain node-based. During these operations, AKS might temporarily provision additional nodes, so the subnet must be large enough to accommodate the maximum node count.

Pod IP addresses are not allocated from the AKS subnet when using BYO CNI unless explicitly implemented by the CNI plugin.


### Kubernetes service address range

All AKS clusters, including those using BYO CNI, require a Kubernetes service address range (`serviceCIDR`

) and a DNS service IP address (`dnsServiceIP`

). The following constraints apply:

- The service address range must not overlap with the virtual network or any connected network.
- The service CIDR must be smaller than /12.
- The DNS service IP must be within the service CIDR range and must not be the first IP address in the range.

These requirements are independent of the CNI plugin.

### Pod networking and IP management

With BYO CNI, pod IP address management (IPAM), routing, and scaling behavior are determined by the CNI plugin.

AKS doesn't:

- Allocate pod IP addresses
- Preassign per-node pod CIDR ranges
- Enforce pod IP reuse or release behavior

Guidance related to overlay or flat networking models, per-node pod CIDR sizing, or subnet sizing formulas that include pod counts doesn't apply to BYO CNI scenarios.

### Maximum pods per node

AKS enforces a configurable maximum number of pods per node (`maxPods`

) at the kubelet level. When using BYO CNI, this setting limits pod scheduling density but doesn't determine IP capacity. You're responsible for ensuring that the selected CNI plugin can support the configured pod density and cluster scale.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication might fail or be misrouted. You must select a pod CIDR that doesn't conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that's unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap occurs if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-cli -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using the Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to install the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using the Azure CLI.

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

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

## Install the KEDA add-on with Azure CLI

To install the KEDA add-on, use `--enable-keda`

when creating or updating a cluster.

## Enable the KEDA add-on on your AKS cluster

Note

While KEDA provides various customization options, the KEDA add-on currently provides basic common configuration.

If you require custom configurations, you can manually edit the KEDA YAML files to customize the installation. **Azure doesn't offer support for custom configurations**.

### Create a new AKS cluster with KEDA add-on enabled

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster using the

command and enable the KEDA add-on using the`az aks create`

`--enable-keda`

flag.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda \ --generate-ssh-keys`


### Enable the KEDA add-on on an existing AKS cluster

Update an existing cluster using the

command and enable the KEDA add-on using the`az aks update`

`--enable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the KEDA add-on is installed on your cluster

Verify the KEDA add-on is installed on your cluster using the

command and set the`az aks show`

`--query`

parameter to`workloadAutoScalerProfile.keda.enabled`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query "workloadAutoScalerProfile.keda.enabled"`

The following example output shows the KEDA add-on is installed on the cluster:

`true`


## Verify KEDA is running on your cluster

Verify the KEDA add-on is running on your cluster using the

`kubectl get pods`

command.`kubectl get pods -n kube-system`

The following example output shows the KEDA operator, admissions hook, and metrics API server are installed on the cluster:

`keda-admission-webhooks-**********-2n9zl 1/1 Running 0 3d18h keda-admission-webhooks-**********-69dkg 1/1 Running 0 3d18h keda-operator-*********-4hb5n 1/1 Running 0 3d18h keda-operator-*********-pckpx 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-gqg4s 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-trfcb 1/1 Running 0 3d18h`


## Verify the KEDA version on your cluster

To verify the version of your KEDA, use `kubectl get crd/scaledobjects.keda.sh -o yaml `

. For example:

```
kubectl get crd/scaledobjects.keda.sh -o yaml
```


The following example output shows the configuration of KEDA in the `app.kubernetes.io/version`

label:

```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
annotations:
controller-gen.kubebuilder.io/version: v0.9.0
meta.helm.sh/release-name: aks-managed-keda
meta.helm.sh/release-namespace: kube-system
creationTimestamp: "2023-08-09T15:58:56Z"
generation: 1
labels:
app.kubernetes.io/component: operator
app.kubernetes.io/managed-by: Helm
app.kubernetes.io/name: keda-operator
app.kubernetes.io/part-of: keda-operator
app.kubernetes.io/version: 2.10.1
helm.toolkit.fluxcd.io/name: keda-adapter-helmrelease
helm.toolkit.fluxcd.io/namespace: 64d3b6fd3365790001260647
name: scaledobjects.keda.sh
resourceVersion: "1421"
uid: 29109c8c-638a-4bf5-ac1b-c28ad9aa11fa
spec:
conversion:
strategy: None
group: keda.sh
names:
kind: ScaledObject
listKind: ScaledObjectList
plural: scaledobjects
shortNames:
- so
singular: scaledobject
scope: Namespaced
# Redacted due to length
```


## Disable the KEDA add-on on your AKS cluster

Disable the KEDA add-on on your cluster using the

command with the`az aks update`

`--disable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-keda`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster using the Azure CLI.

With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/planned-maintenance -->

# Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use planned maintenance to schedule and control cluster and node image upgrades in Azure Kubernetes Service (AKS).

Regular maintenance is performed on your AKS cluster automatically. There are two types of maintenance operations:

**AKS-initiated maintenance**involves the weekly releases that AKS performs to keep your cluster up to date with the latest features and fixes.**User-initiated maintenance**includes[cluster auto-upgrades](upgrade-cluster)and[node operating system (OS) automatic security updates](auto-upgrade-node-image).

When you use the feature of planned maintenance in AKS, you can run both types of maintenance in a cadence of your choice to minimize workload impact.

Note

You can use planned maintenance to schedule the timing of automatic upgrades, but enabling or disabling planned maintenance doesn't enable or disable automatic upgrades.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, see
[Create an AKS cluster](learn/quick-kubernetes-deploy-cli). - If you're using the Azure CLI, upgrade to the latest version using the
command.`az upgrade`


## Considerations

When you use planned maintenance, the following considerations apply:

- AKS reserves the right to break planned maintenance windows for unplanned, reactive maintenance operations that are urgent or critical. These maintenance operations might even run during the
`notAllowedTime`

or`notAllowedDates`

periods defined in your configuration. - Maintenance operations are considered
*best effort only*and aren't guaranteed to occur within a specified window.

## Schedule configuration types for planned maintenance

Three schedule configuration types are available for planned maintenance:

`default`

is a basic configuration for controlling AKS releases, which covers control plane components and system add-ons upgrade. The releases can take up to two weeks to roll out to all regions from the initial time of shipping, because of Azure safe deployment practices.Choose

`default`

to schedule these updates in a manner that's least disruptive for you. You can monitor the status of an ongoing AKS release by region with the[weekly release tracker](release-tracker).`aksManagedAutoUpgradeSchedule`

controls when to perform cluster upgrades scheduled by your designated auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on cluster auto-upgrade, see[Automatically upgrade an Azure Kubernetes Service cluster](upgrade-cluster).`aksManagedNodeOSUpgradeSchedule`

controls when to perform the node OS security patching scheduled by your node OS auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on node OS auto-upgrade channels, see[Automatically patch and update AKS cluster node images](auto-upgrade-node-image).

We recommend using `aksManagedAutoUpgradeSchedule`

for all cluster Kubernetes version upgrade scenarios and `aksManagedNodeOSUpgradeSchedule`

for all node OS security patching scenarios.

The `default`

option is meant exclusively for AKS weekly releases. Use `default`

if you want to control the upgrade schedule for AKS control plane components (such as API Server, ETCD, etc.) and add-ons (such as CoreDNS, Metrics Server, etc.).

All three types of configurations can coexist.

## Create a maintenance window

Note

When you're using auto-upgrade, to ensure proper functionality, use a maintenance window with a duration of four hours or more.

Note

From the 2023-05-01 API version onwards, use the properties in the following table for `default`

configuration.

An `aksManagedAutoUpgradeSchedule`

or `aksManagedNodeOSUpgradeSchedule`

maintenance window and `default`

configuration from 2023-05-01 API version onwards has the following properties:

| Name | Description | Default value |
|---|---|---|
`utcOffset` |
The time zone for cluster maintenance. | `+00:00` |
`startDate` |
The date on which the maintenance window begins to take effect. | The current date at creation time |
`startTime` |
The time for maintenance to begin, based on the time zone determined by `utcOffset` . |
Not applicable |
`schedule` |
The upgrade frequency. Three types are available: `Weekly` , `AbsoluteMonthly` , and `RelativeMonthly` . |
Not applicable |
`intervalDays` |
The interval in days for maintenance runs. It's applicable only to `aksManagedNodeOSUpgradeSchedule` . |
Not applicable |
`intervalWeeks` |
The interval in weeks for maintenance runs. | Not applicable |
`intervalMonths` |
The interval in months for maintenance runs. | Not applicable |
`dayOfWeek` |
The specified day of the week for maintenance to begin. | Not applicable |
`durationHours` |
The duration of the window for maintenance to run. | Not applicable |
`notAllowedDates` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. It's applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Deprecated properties

Note

If you create a `default`

configuration with the following deprecated properties, it migrates automatically to the new properties shown in the previous table.

**[Deprecated]** A `default`

maintenance window has the following legacy properties:

| Name | Description | Default value |
|---|---|---|
`timeInWeek` |
In a `default` configuration, this property contains the `day` and `hourSlots` values that define a maintenance window. |
Not applicable |
`timeInWeek.day` |
The day of the week to perform maintenance in a `default` configuration. |
Not applicable |
`timeInWeek.hourSlots` |
A list of hour-long time slots to perform maintenance on a particular day in a `default` configuration. |
Not applicable |
`notAllowedTime` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. This property is applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Schedule types

Four schedule types are supported: `Daily`

, `Weekly`

, `AbsoluteMonthly`

, and `RelativeMonthly`

.

The following table shows which types are available for each maintenance-configuration option:

| Schedule type | `default` |
`aksManagedClusterAutoUpgradeSchedule` |
`aksManagedNodeOSUpgradeSchedule` |
|---|---|---|---|
| Daily | Unsupported ❌ | Supported ✅ (after Jun 2025) | Supported ✅ |
| Weekly | Supported ✅ | Supported ✅ | Supported ✅ |
| AbsoluteMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |
| RelativeMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |

All of the fields shown for each schedule type are required.

A `Daily`

schedule might look like "every three days":

```
"schedule": {
"daily": {
"intervalDays": 3
}
}
```


A `Weekly`

schedule might look like "every two weeks on Friday":

```
"schedule": {
"weekly": {
"intervalWeeks": 2,
"dayOfWeek": "Friday"
}
}
```


An `AbsoluteMonthly`

schedule might look like "every three months on the first day of the month":

```
"schedule": {
"absoluteMonthly": {
"intervalMonths": 3,
"dayOfMonth": 1
}
}
```


A `RelativeMonthly`

schedule might look like "every two months on the last Monday":

```
"schedule": {
"relativeMonthly": {
"intervalMonths": 2,
"dayOfWeek": "Monday",
"weekIndex": "Last"
}
}
```


Valid values for `weekIndex`

include `First`

, `Second`

, `Third`

, `Fourth`

, and `Last`

.

## Add a maintenance window configuration

Add a maintenance window configuration to an AKS cluster using the [ az aks maintenanceconfiguration add](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-add) command.

The first example adds a new `default`

configuration that schedules maintenance to run from 1:00 AM to 5:00 AM every Monday in the `UTC`

time zone. The second example adds a new `aksManagedAutoUpgradeSchedule`

configuration that schedules maintenance to run every third Friday between 12:00 AM and 8:00 AM in the `UTC+5:30`

time zone.

```
# Add a new default configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Monday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 01:00
# Add a new aksManagedAutoUpgradeSchedule configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule --schedule-type Weekly --day-of-week Friday --interval-weeks 3 --duration 8 --utc-offset +05:30 --start-time 00:00
```


## Update an existing maintenance window

Update an existing maintenance configuration using the [ az aks maintenanceconfiguration update](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-update) command.

The following example updates the `default`

configuration to schedule maintenance to run from 2:00 AM to 6:00 AM every Friday:

```
az aks maintenanceconfiguration update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Friday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 02:00
```


## List all maintenance windows in an existing cluster

List the current maintenance configuration windows in your AKS cluster using the [ az aks maintenanceconfiguration list](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-list) command:

```
az aks maintenanceconfiguration list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Show a specific maintenance configuration window in an existing cluster

View a specific maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration show](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-show) command with the

`--name`

parameter:```
az aks maintenanceconfiguration show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule
```


The following example output shows the maintenance window for `aksManagedAutoUpgradeSchedule`

:

```
{
"id": "/subscriptions/<subscription>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/maintenanceConfigurations/aksManagedAutoUpgradeSchedule",
"maintenanceWindow": {
"durationHours": 4,
"notAllowedDates": [
{
"end": "2024-01-05",
"start": "2023-12-23"
}
],
"schedule": {
"absoluteMonthly": {
"dayOfMonth": 1,
"intervalMonths": 3
},
"daily": null,
"relativeMonthly": null,
"weekly": null
},
"startDate": "2023-01-20",
"startTime": "09:00",
"utcOffset": "-08:00"
},
"name": "aksManagedAutoUpgradeSchedule",
"notAllowedTime": null,
"resourceGroup": "myResourceGroup",
"systemData": null,
"timeInWeek": null,
"type": null
}
```


## Delete a maintenance configuration window in an existing cluster

Delete a maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration delete](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-delete) command.

The following example deletes the `autoUpgradeSchedule`

maintenance configuration:

```
az aks maintenanceconfiguration delete --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name autoUpgradeSchedule
```


## Frequently asked questions (FAQ)

### How can I check the existing maintenance configurations in my cluster?

Use the `az aks maintenanceconfiguration show`

command.

### Can reactive, unplanned maintenance happen during the `notAllowedDates`

periods too?

Yes. AKS reserves the right to break these windows for unplanned, reactive maintenance operations that are urgent or critical.

### How can I tell if a maintenance event occurred?

For releases, check your cluster's region and look up information in [weekly releases](release-tracker) to see if it matches your maintenance schedule. To view the status of your automatic upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events, as mentioned in [Upgrade an AKS cluster](upgrade-cluster).

AKS also emits upgrade-related Azure Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I use more than one maintenance configuration at the same time?

Yes, you can run all three configurations simultaneously: `default`

, `aksManagedAutoUpgradeSchedule`

, and `aksManagedNodeOSUpgradeSchedule`

. If the windows overlap, AKS decides the running order.

### I configured a maintenance window, but the upgrade didn't happen. Why?

AKS auto-upgrade needs a certain amount of time, usually not more than 15 minutes, to take the maintenance window into consideration. We recommend at least 15 minutes between the creation or update of a maintenance configuration and the scheduled start time.

Also, ensure that your cluster is started when the planned maintenance window starts. If the cluster is stopped, its control plane is deallocated and no operations can be performed.

### Why was one of my agent pools upgraded outside the maintenance window?

If an agent pool isn't upgraded (for example, because pod disruption budgets prevented it), it might be upgraded later, outside the maintenance window. This scenario is referred to as a *catch-up upgrade*. It avoids letting agent pools be upgraded with a different version from the AKS control plane.

Another reason why an agent pool could be upgraded unexpectedly is when there's no defined maintenance configuration or if it was deleted. In that case, a cluster with auto-upgrade *but without a maintenance configuration* is upgraded at random times (*fallback schedule*), which might be an undesired timeframe.

### Are there any best practices for the maintenance configurations?

We recommend setting the [node OS security updates](auto-upgrade-node-image) schedule to a weekly cadence if you're using the `NodeImage`

channel, because a new node image is shipped every week. You can also opt in for the `SecurityPatch`

channel to receive daily security updates.

You can set the [auto-upgrade](auto-upgrade-cluster) schedule to a monthly cadence to stay current with the Kubernetes N-2 [support policy](support-policies).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

### Can I configure all my clusters in a single subscription to use the same maintenance configuration?

We don't recommend using the same maintenance configuration for multiple clusters in a single subscription, as doing so can lead to ARM throttling errors causing cluster upgrades to fail. Instead, we recommend staggering the maintenance windows for each cluster to avoid these errors.

### Why did my node pools get upgraded twice during the same maintenance window?

If a newer version of the node image becomes available during the maintenance window, AKS performs a second upgrade to ensure that your node pools are running the latest version. This behavior is normal and doesn't indicate an issue.

## Related content

To get started with upgrading your AKS cluster, see [Upgrade options for AKS clusters](upgrade-cluster).
