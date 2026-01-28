---
merged_at: 2026-01-28T07:16:09.848855
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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-support-help -->

# Support and troubleshooting for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

## Self help troubleshooting


The [AKS troubleshooting documentation](/en-us/troubleshoot/azure/azure-kubernetes/welcome-azure-kubernetes) provides guidance for how to diagnose and resolve issues that you might encounter when using AKS. These articles cover how to troubleshoot deployment failures, security-related problems, connection issues, and more.

## Post a question on Microsoft Q&A


Azure's preferred destination for community support, [Microsoft Q&A](/en-us/answers/products/azure), allows you to ask technical questions and engage with Azure engineers, Most Valuable Professionals (MVPs), partners, and customers. When you ask a question, make sure you use the `azure-kubernetes-service`

tag. You can also submit your own answers and help other community members with their questions.

If you can't find an answer to your problem using search, you can submit a new question to Microsoft Q&A and tag it with the appropriate Azure service and area.

The following table lists the tags for AKS and related services:

## Create an Azure support request


Explore the range of [Azure support options](https://azure.microsoft.com/support/plans) and choose a plan that best fits your needs. Azure customers can create and manage support requests in the Azure portal.

If you already have an Azure Support Plan, you can [open a support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## Create a GitHub issue


If you need help with the languages and tools for developing and managing AKS, you can open an issue in its GitHub repository.

The following table lists the GitHub repositories for AKS and related services:

| Library | GitHub issues URL |
|---|---|
| Azure PowerShell |
|

[https://github.com/Azure/azure-cli/issues](https://github.com/Azure/azure-cli/issues)[https://github.com/Azure/azure-rest-api-specs/issues](https://github.com/Azure/azure-rest-api-specs/issues)[https://github.com/Azure/azure-sdk-for-java/issues](https://github.com/Azure/azure-sdk-for-java/issues)[https://github.com/Azure/azure-sdk-for-python/issues](https://github.com/Azure/azure-sdk-for-python/issues)[https://github.com/Azure/azure-sdk-for-net/issues](https://github.com/Azure/azure-sdk-for-net/issues)[https://github.com/Azure/azure-sdk-for-js/issues](https://github.com/Azure/azure-sdk-for-js/issues)[https://github.com/Azure/terraform/issues](https://github.com/Azure/terraform/issues)## Stay informed of updates and new releases


Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?searchterms=compute). For information about Azure Virtual Machines, see the [Azure blog](https://azure.microsoft.com/blog/product/virtual-machines/).

## Next steps

Visit the [Azure Kubernetes Service (AKS) documentation](./).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-v2 -->

# Migrate to Key Management Service (KMS) v2 in Azure Kubernetes Service (AKS) (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article applies to clusters using the legacy KMS experience that need to migrate from KMS v1 to KMS v2. For clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

In this article, you learn how to migrate to KMS v2 for clusters with versions older than 1.27. Beginning in AKS version 1.27, turning on the KMS feature configures KMS v2. With KMS v2, you aren't limited to the 2,000 secrets that earlier versions support. For more information, see [KMS v2 improvements](https://kubernetes.io/blog/2023/05/16/kms-v2-moves-to-beta/).

Important

If your cluster version is older than 1.27 and you already turned on KMS, the upgrade to cluster version 1.27 or later is blocked.

## Turn off KMS

Disable KMS on an existing cluster using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Upgrade your AKS cluster and turn on KMS

Upgrade your AKS cluster to version 1.27 or later using the

command with the`az aks upgrade`

`--kubernetes-version`

parameter set to your desired version. The following example upgrades to version`1.27.1`

:`az aks upgrade --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --kubernetes-version 1.27.1`

Once the upgrade completes, you can turn on KMS for a public or private key vault using one of the following resources:

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-managed-namespaces -->

# Overview of managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes namespaces form the logical isolation boundary for workloads and resources. Performing logical isolation involves implementing scripts and processes to create namespaces, set resource limits, apply network policies, and grant team access via role-based access control. Learn how to use managed namespaces in Azure Kubernetes Service (AKS) to simplify namespace management, cluster multi-tenancy, and resource isolation.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with [cluster autoscaler](cluster-autoscaler) or [Node Auto Provisioning](node-autoprovision), you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

## Network policies

[Network Policies](use-network-policies) are Kubernetes resources you can use to control the flow of traffic between pods, namespaces, and external endpoints. Network policies allow you to define rules for ingress (incoming) and egress (outgoing) traffic, ensuring that only authorized communication is permitted. By applying network policies, you can enhance the security and isolation of workloads within your cluster.

Note

The default ingress network policy rule of **Allow same namespace** opts for a secure by default stance. If you need your Kubernetes Services, ingresses, or gateways to be accessible from outside of the namespace where they're deployed, for example from an ingress controller deployed in a separate namespace, you need to select **Allow all**. You might then apply your own network policy to restrict ingress to be from that namespace only.

Managed namespaces come with a set of built-in policies.

**Allow all**: Allows all network traffic.**Allow same namespace**: Allows all network traffic within the same namespace.**Deny all**: Denies all network traffic.

You can apply any of the built-in policies on both **ingress** and **egress** rules and they have the following default values.

| Policy | Default value |
|---|---|
| Ingress | Allow same namespace |
| Egress | Allow all |

Note

Users with a `Microsoft.ContainerService/managedClusters/networking.k8s.io/networkpolicies/write`

action, such as `Azure Kubernetes Service RBAC Writer`

, on the Microsoft Entra ID role they're assigned can add more network policies through the Kubernetes API.

For example, if an admin applies a `Deny All`

policy for ingress/egress, and a user applies an `Allow`

policy for a namespace via the Kubernetes API, the `Allow`

policy takes priority over the `Deny All`

policy, and traffic is allowed to flow for the namespace.

## Resource quotas

[Resource Quotas](operator-best-practices-scheduler#enforce-resource-quotas) are Kubernetes resources that are used to manage and limit the resource consumption of namespaces within a cluster. They allow administrators to define constraints on the amount of CPU, memory, storage, or other resources that are used by workloads in a namespace. By applying resource quotas, you can ensure fair resource distribution, prevent resource overuse, and maintain cluster stability.

Managed namespaces can be created with the following resource quotas:

**CPU requests and limits**: Define the minimum and maximum amount of CPU resources that workloads in the namespace can request or consume. The quota ensures that workloads have sufficient CPU resources to operate while preventing overuse that could affect other namespaces. The quota is defined in the[milliCPU form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu).**Memory requests and limits**: Specify the minimum and maximum amount of memory resources that workloads in the namespace can request or consume. The quota helps maintain stability by avoiding memory overcommitment and ensuring fair resource allocation across namespaces. The quota is defined in[power-of-two equivalents form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory)such as`Ei`

,`Pi`

,`Ti`

,`Gi`

,`Mi`

,`Ki`

.

## Labels and annotations

Kubernetes [Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) and [Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) are metadata attached to Kubernetes objects, such as namespaces, to provide additional information. Labels are key-value pairs used to organize and select resources, enabling efficient grouping and querying. Annotations store nonidentifying metadata, such as configuration details or operational instructions, that are consumed by tools or systems.

You can optionally set Kubernetes Labels and Annotations to be applied on the namespace.

## Adoption policy

The adoption policy determines how an existing namespace in Kubernetes is handled when creating a managed namespace.

Warning

Onboarding an existing namespace to be managed can cause disruption. If the **resource quota** applied is less than what is already being requested by pods, new deployments and pods that exceed the quota is denied. Existing deployments aren't affected, but scaling is denied. Applying **network policies** to an existing namespace can affect existing traffic. Ensure that the policies are tested and validated to avoid unintended disruptions to communication between pods or external endpoints.

The following options are available:

**Never**: If the namespace already exists in the cluster, attempts to create that namespace as a managed namespace fails.**IfIdentical**: Take over the existing namespace to be managed, provided there are no differences between the existing namespace and the desired configuration.**Always**: Always take over the existing namespace to be managed, even if some fields in the namespace might be overwritten.

## Delete policy

The delete policy specifies how the Kubernetes namespace is handled when the managed namespace resource is deleted.

Warning

Deleting a managed namespace with the **Delete** policy causes all resources within that namespace, such as Deployments, Services, Ingresses, and other Kubernetes objects, to be deleted. Ensure that you back up or migrate any critical resources before proceeding.

The following options are available:

**Keep**: Only delete the managed namespace resource while keeping the Kubernetes namespace intact. Additionally, the`ManagedByARM`

label is removed from the namespace.**Delete**: Delete both the managed namespace resource and the Kubernetes namespace together.

## Managed namespaces built-in roles

Managed namespaces uses the following built-in roles for the control plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service Namespace User](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-namespace-user)Managed namespaces uses the following built-in roles for the data plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service RBAC Writer](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-writer)[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-admin)## Managed namespaces use cases

Properly setting up [namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) with associated [quotas](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/) or [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource) can be complex and time-consuming. Managed namespaces allow you to set up preconfigured namespaces in your AKS clusters that you can interact with using the Azure CLI.

The following sections outline some common use cases for managed namespaces.

### Manage teams and resources on AKS

Let's say you're an admin at a small startup. You have an AKS cluster provisioned and want to set up namespaces for developers from your *finance*, *legal*, and *design* teams. As you're setting up your company's environment, you want to make sure that access is tightly controlled, resources are rightly scoped, and environments are organized properly.

The

*finance*team intakes forms and files from teams all across the company, but they hold sensitive information that ideally shouldn't leave their environment. Their applications and workflows are lighter on the computing side but consume a lot of memory. As a result, you decide to set up a namespace that allows for all network ingress, network egress only within their namespace, and scope their resources accordingly. A label to the namespace helps easily identify which team is using it.`az aks namespace add \ --name $FINANCE_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 512Mi \ --memory-limit 2Gi \ --ingress-policy AllowAll \ --egress-policy AllowSameNamespace \ --labels team=finance`

The

*legal*team deals primarily with sensitive data. Their applications use a fair amount of memory but require little compute resources. You decide to set up a namespace that's extremely restrictive for both the ingress/egress policies, and scope their resource quotas accordingly.`az aks namespace add \ --name $LEGAL_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 2Gi \ --memory-limit 5Gi \ --ingress-policy DenyAll \ --egress-policy DenyAll \ --labels team=legal`

The

*design*team needs the ability to freely flow data to showcase their work across the company. They also encourage teams to send them content for reference. Their applications are intensive and require a large chunk of memory and CPU. You decide to set them up with a minimally restrictive namespace and allocate a sizeable amount of resources for them.`az aks namespace add \ --name $DESIGN_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 2000m \ --cpu-limit 2500m \ --memory-request 5Gi \ --memory-limit 8Gi \ --ingress-policy AllowAll \ --egress-policy AllowAll \ --labels team=design`


With these namespaces set up, you now have environments for the three teams in your organization that should allow each team to get up and running in an environment that best suits their needs. Admins can use [Azure CLI calls](/en-us/cli/azure/aks/namespace) to update the namespaces as needs shift.

### View managed namespaces

As the number of teams you deal with expands, or as your organization grows, you might find yourself needing to review the namespaces you set up.

Let's say you want to review the namespaces in your cluster from the [previous section](#manage-teams-and-resources-on-aks) to ensure there are three namespaces.

Use the [ az aks namespace list](/en-us/cli/azure/aks/namespace#az-aks-namespace-list) command to review your namespaces.

```
az aks namespace list \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--output table
```


Your output should look similar to the following example output:

```
Name ResourceGroup Location
------------------ --------------- ----------
$CLUSTER_NAME/$DESIGN_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$LEGAL_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$FINANCE_NAMESPACE $RESOURCE_GROUP <LOCATION>
```


### Control access to managed namespaces

You can further use [Azure RBAC roles](#managed-namespaces-built-in-roles), scoped to each namespace, to determine which users have access to certain actions within the namespace. With the proper configuration, you can ensure users have all the access they need within the namespace, while limiting their access to other namespaces or cluster-wide resources.

## Next steps

- Learn how to
[create and use managed namespaces on Azure Kubernetes Service (AKS)](managed-namespaces). - Learn about
[multi-cluster managed namespaces](../kubernetes-fleet/concepts-fleet-managed-namespace)with Azure Kubernetes Fleet Manager.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-overview -->

# Use Microsoft Entra Workload ID with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Workloads deployed on an AKS cluster require Microsoft Entra application credentials or managed identities to access Microsoft Entra protected resources, such as Azure Key Vault and Microsoft Graph. Microsoft Entra Workload ID integrates with the capabilities native to Kubernetes to federate with external identity providers, allowing you to assign workload identities to your workloads to authenticate and access other services and resources.

[Microsoft Entra Workload ID](/en-us/azure/active-directory/develop/workload-identities-overview) uses [Service Account Token Volume Projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection) (or a *service account*), to enable pods to use a Kubernetes identity. A Kubernetes token is issued and [OpenID Connect (OIDC) federation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens) enables Kubernetes applications to access Azure resources securely with Microsoft Entra ID, based on annotated service accounts.

You can use Microsoft Entra Workload ID with [Azure Identity client libraries](#azure-identity-client-libraries) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL) collection, together with [application registration](/en-us/azure/active-directory/develop/application-model#register-an-application), to seamlessly authenticate and access Azure cloud resources.

Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [What is Service Connector?](/en-us/azure/service-connector/overview)

## Prerequisites

- AKS supports Microsoft Entra Workload ID on version 1.22 and higher.
- The Azure CLI version 2.47.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- You can have a maximum of
[20 federated identity credentials](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#general-federated-identity-credential-considerations)per managed identity. - It takes a few seconds for the federated identity credential to propagate after being initially added.
- The
[virtual nodes](virtual-nodes)add-on, based on the open source project[Virtual Kubelet](https://virtual-kubelet.io/docs/), isn't supported. - Creation of federated identity credentials isn't supported on user-assigned managed identities in
[these regions](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#unsupported-regions-user-assigned-managed-identities).

## Azure Identity client libraries

In the Azure Identity client libraries, choose one of the following approaches:

- Use
`DefaultAzureCredential`

, which attempts to use the`WorkloadIdentityCredential`

. - Create a
`ChainedTokenCredential`

instance that includes`WorkloadIdentityCredential`

. - Use
`WorkloadIdentityCredential`

directly.

The following table provides the **minimum** package version required for each language ecosystem's client library:

| Ecosystem | Library | Minimum version |
|---|---|---|
| .NET |
|

[azure-identity-cpp](https://github.com/Azure/azure-sdk-for-cpp/blob/main/sdk/identity/azure-identity/README.md)[azidentity](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity)[azure-identity](/en-us/java/api/overview/azure/identity-readme)[@azure/identity](/en-us/javascript/api/overview/azure/identity-readme)[azure-identity](/en-us/python/api/overview/azure/identity-readme)## Azure Identity client library code samples

The following code samples use the `DefaultAzureCredential`

. This credential type uses the environment variables injected by the workload identity mutating [webhook](#webhook-certificate-auto-rotation) to authenticate with Azure Key Vault. To see samples using one of the other approaches, refer to the [ecosystem-specific client libraries](#azure-identity-client-libraries).

```
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;
string keyVaultUrl = Environment.GetEnvironmentVariable("<key-vault-url>");
string secretName = Environment.GetEnvironmentVariable("<secret-name>");
var client = new SecretClient(
new Uri(keyVaultUrl),
new DefaultAzureCredential());
KeyVaultSecret secret = await client.GetSecretAsync(secretName);
```


## Microsoft Authentication Library (MSAL)

The following client libraries are the **minimum** version required:

| Ecosystem | Library | Image | Example | Has Windows |
|---|---|---|---|---|
| .NET |
|

`ghcr.io/azure/azure-workload-identity/msal-net:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-net/akvdotnet)[Microsoft Authentication Library-for-go](https://github.com/AzureAD/microsoft-authentication-library-for-go)`ghcr.io/azure/azure-workload-identity/msal-go:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-go)[Microsoft Authentication Library-for-java](https://github.com/AzureAD/microsoft-authentication-library-for-java)`ghcr.io/azure/azure-workload-identity/msal-java:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-java)[Microsoft Authentication Library-for-js](https://github.com/AzureAD/microsoft-authentication-library-for-js)`ghcr.io/azure/azure-workload-identity/msal-node:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-node)[Microsoft Authentication Library-for-python](https://github.com/AzureAD/microsoft-authentication-library-for-python)`ghcr.io/azure/azure-workload-identity/msal-python:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-python)## How it works

In this security model, the AKS cluster acts as the token issuer. Microsoft Entra ID uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library or the MSAL.

The following table describes the required OIDC issuer endpoints for Microsoft Entra Workload ID:

| Endpoint | Description |
|---|---|
`{IssuerURL}/.well-known/openid-configuration` |
Also known as the OIDC discovery document. This contains the metadata about the issuer's configurations. |
`{IssuerURL}/openid/v1/jwks` |
This contains the public signing key(s) that Microsoft Entra ID uses to verify the authenticity of the service account token. |

The following diagram summarizes the authentication sequence using OIDC:

### Webhook certificate auto-rotation

Similar to other webhook add-ons, the [cluster certificate auto-rotation](certificate-rotation#certificate-autorotation) operation rotates the certificate.

## Service account labels and annotations

Microsoft Entra Workload ID supports the following mappings related to a service account:

**One-to-one**, where a service account references a Microsoft Entra object.**Many-to-one**, where multiple service accounts reference the same Microsoft Entra object.**One-to-many**, where a service account references multiple Microsoft Entra objects by changing the client ID annotation. For more information, see[How to federate multiple identities with a Kubernetes service account](https://azure.github.io/azure-workload-identity/docs/faq.html#how-to-federate-multiple-identities-with-a-kubernetes-service-account).

Note

If you update the service account annotations, you must restart the pod for the changes to take effect.

If you've used [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity), think of a service account as an Azure security principal, except that a service account is part of the core Kubernetes API, rather than a [Custom Resource Definition](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) (CRD). The following sections describe a list of available labels and annotations that you can use to configure the behavior when exchanging the service account token for a Microsoft Entra access token.

### Service account annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/client-id` |
Represents the Microsoft Entra application client ID to be used with the pod. |
|
`azure.workload.identity/tenant-id` |
Represents the Azure tenant ID where the Microsoft Entra application is registered. |
AZURE_TENANT_ID environment variable extracted from `azure-wi-webhook-config` ConfigMap. |
`azure.workload.identity/service-account-token-expiration` |
Represents the `expirationSeconds` field for the projected service account token. It's an optional field that you configure to prevent any downtime caused by errors during service account token refresh. Kubernetes service account token expiry isn't correlated with Microsoft Entra tokens. Microsoft Entra tokens expire in 24 hours after they're issued. |
3600 Supported range is 3600-86400. |

### Pod labels

Note

For applications using Microsoft Entra Workload ID, it's required to add the label `azure.workload.identity/use: "true"`

to the pod spec for AKS to move the workload identity to a *Fail Close* scenario to provide a consistent and reliable behavior for pods that need to use workload identity. Otherwise, the pods fail after they're restarted.

| Label | Description | Recommended value | Required |
|---|---|---|---|
`azure.workload.identity/use` |
This label is required in the pod template spec. Only pods with this label are mutated by the azure-workload-identity mutating admission webhook to inject the Azure specific environment variables and the projected service account token volume. | true | Yes |

### Pod annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/service-account-token-expiration` |
See
Pod annotations take precedence over service account annotations. |

Supported range is 3600-86400.

`azure.workload.identity/skip-containers`

`container1;container2`

.`azure.workload.identity/use: true`

.`azure.workload.identity/inject-proxy-sidecar`

`azure.workload.identity/proxy-sidecar-port`

## Migrate to Microsoft Entra Workload ID

You can configure clusters already running a pod-managed identity to use Microsoft Entra Workload ID using one of two ways:

- Use the same configuration you implemented for pod-managed identity. You can annotate the service account within the namespace with the identity to enable Microsoft Entra Workload ID and inject the annotations into the pods.
- Rewrite your application to use the latest version of the Azure Identity client library.

To help streamline and ease the migration process, we developed a migration sidecar that converts the Instance Metadata Service (IMDS) transactions your application makes over to [OIDC](/en-us/azure/active-directory/develop/v2-protocols-oidc). The migration sidecar isn't intended to be a long-term solution, but a way to get up and running quickly on Microsoft Entra Workload ID. Running the migration sidecar within your application proxies the application IMDS transactions over to OIDC. The alternative approach is to upgrade to a supported version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library, which supports OIDC authentication.

The following table summarizes our migration or deployment recommendations for your AKS cluster:

| Scenario | Description |
|---|---|
| New or existing cluster deployment
|

Sample deployment resources:

[Deploy and configure Microsoft Entra Workload ID on a new cluster](workload-identity-deploy-cluster)[migration sidecar](workload-identity-migrate-from-pod-identity).## Next steps

- To learn how to set up your pod to authenticate using a workload identity as a migration option, see
[Modernize application authentication with Microsoft Entra Workload ID](workload-identity-migrate-from-pod-identity). - See
[Deploy and configure an AKS cluster with Microsoft Entra Workload ID](workload-identity-deploy-cluster), which helps you deploy a cluster and configure a sample application to use a workload identity.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-scheduler -->

# Best practices for basic scheduler features in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. The Kubernetes scheduler lets you control the distribution of compute resources, or limit the impact of maintenance events.

This best practices article focuses on basic Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use resource quotas to provide a fixed amount of resources to teams or workloads
- Limit the impact of scheduled maintenance using pod disruption budgets

## Enforce resource quotas


Best practice guidancePlan and apply resource quotas at the namespace level. If pods don't define resource requests and limits, reject the deployment. Monitor resource usage and adjust quotas as needed.


Resource requests and limits are placed in the pod specification. Requests are used by the Kubernetes scheduler at deployment time to find an available node in the cluster. Limits and requests work at the individual pod level. For more information about how to define these values, see [Define pod resource requests and limits](developer-best-practices-resource-management#define-pod-resource-requests-and-limits).

To provide a way to reserve and limit resources across a development team or project, you should use *resource quotas*. These quotas are defined on a namespace, and can be used to set quotas on the following basis:

**Compute resources**, such as CPU and memory, or GPUs.**Storage resources**, including the total number of volumes or amount of disk space for a given storage class.**Object count**, such as maximum number of secrets, services, or jobs can be created.

Kubernetes doesn't overcommit resources. Once your cumulative resource request total passes the assigned quota, all further deployments will be unsuccessful.

When you define resource quotas, all pods created in the namespace must provide limits or requests in their pod specifications. If they don't provide these values, you can reject the deployment. Instead, you can [configure default requests and limits for a namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/).

The following example YAML manifest named *dev-app-team-quotas.yaml* sets a hard limit of a total of *10* CPUs, *20Gi* of memory, and *10* pods:

```
apiVersion: v1
kind: ResourceQuota
metadata:
name: dev-app-team
spec:
hard:
cpu: "10"
memory: 20Gi
pods: "10"
```


This resource quota can be applied by specifying the namespace, such as *dev-apps*:

```
kubectl apply -f dev-app-team-quotas.yaml --namespace dev-apps
```


Work with your application developers and owners to understand their needs and apply the appropriate resource quotas.

For more information about available resource objects, scopes, and priorities, see [Resource quotas in Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/).

## Plan for availability using pod disruption budgets


Best practice guidanceTo maintain the availability of applications, define Pod Disruption Budgets (PDBs) to make sure that a minimum number of pods are available in the cluster.


There are two disruptive events that cause pods to be removed:

### Involuntary disruptions

*Involuntary disruptions* are events beyond the typical control of the cluster operator or application owner. Include:

- Hardware failure on the physical machine
- Kernel panic
- Deletion of a node VM

Involuntary disruptions can be mitigated by:

- Using multiple replicas of your pods in a deployment.
- Running multiple nodes in the AKS cluster.

### Voluntary disruptions

*Voluntary disruptions* are events requested by the cluster operator or application owner. Include:

- Cluster upgrades
- Updated deployment template
- Accidentally deleting a pod

Kubernetes provides *pod disruption budgets* for voluntary disruptions, letting you plan for how deployments or replica sets respond when a voluntary disruption event occurs. Using pod disruption budgets, cluster operators can define a minimum available or maximum unavailable resource count.

If you upgrade a cluster or update a deployment template, the Kubernetes scheduler will schedule extra pods on other nodes before allowing voluntary disruption events to continue. The scheduler waits to reboot a node until the defined number of pods are successfully scheduled on other nodes in the cluster.

Let's look at an example of a replica set with five pods that run NGINX. The pods in the replica set are assigned the label `app: nginx-frontend`

. During a voluntary disruption event, such as a cluster upgrade, you want to make sure at least three pods continue to run. The following YAML manifest for a *PodDisruptionBudget* object defines these requirements:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
minAvailable: 3
selector:
matchLabels:
app: nginx-frontend
```


You can also define a percentage, such as *60%*, which allows you to automatically compensate for the replica set scaling up the number of pods.

You can define a maximum number of unavailable instances in a replica set. Again, a percentage for the maximum unavailable pods can also be defined. The following pod disruption budget YAML manifest defines that no more than two pods in the replica set be unavailable:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
maxUnavailable: 2
selector:
matchLabels:
app: nginx-frontend
```


Once your pod disruption budget is defined, you create it in your AKS cluster as with any other Kubernetes object:

```
kubectl apply -f nginx-pdb.yaml
```


Work with your application developers and owners to understand their needs and apply the appropriate pod disruption budgets.

For more information about using pod disruption budgets, see [Specify a disruption budget for your application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

## Next steps

This article focused on basic Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux -->

# Use the Azure Linux container host for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Linux container host for AKS is an open-source Linux distribution created by Microsoft, and it's generally available as a container host on Azure Kubernetes Service (AKS). The Azure Linux container host provides reliability and consistency from cloud to edge across the AKS, AKS-HCI, and Arc products. You can deploy Azure Linux node pools in a new cluster, add Azure Linux node pools to your existing Ubuntu clusters, or migrate your Ubuntu nodes to Azure Linux nodes. To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-managed-namespaces -->

# Overview of managed namespaces in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic ✔️ AKS Standard

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes namespaces form the logical isolation boundary for workloads and resources. Performing logical isolation involves implementing scripts and processes to create namespaces, set resource limits, apply network policies, and grant team access via role-based access control. Learn how to use managed namespaces in Azure Kubernetes Service (AKS) to simplify namespace management, cluster multi-tenancy, and resource isolation.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with [cluster autoscaler](cluster-autoscaler) or [Node Auto Provisioning](node-autoprovision), you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

## Network policies

[Network Policies](use-network-policies) are Kubernetes resources you can use to control the flow of traffic between pods, namespaces, and external endpoints. Network policies allow you to define rules for ingress (incoming) and egress (outgoing) traffic, ensuring that only authorized communication is permitted. By applying network policies, you can enhance the security and isolation of workloads within your cluster.

Note

The default ingress network policy rule of **Allow same namespace** opts for a secure by default stance. If you need your Kubernetes Services, ingresses, or gateways to be accessible from outside of the namespace where they're deployed, for example from an ingress controller deployed in a separate namespace, you need to select **Allow all**. You might then apply your own network policy to restrict ingress to be from that namespace only.

Managed namespaces come with a set of built-in policies.

**Allow all**: Allows all network traffic.**Allow same namespace**: Allows all network traffic within the same namespace.**Deny all**: Denies all network traffic.

You can apply any of the built-in policies on both **ingress** and **egress** rules and they have the following default values.

| Policy | Default value |
|---|---|
| Ingress | Allow same namespace |
| Egress | Allow all |

Note

Users with a `Microsoft.ContainerService/managedClusters/networking.k8s.io/networkpolicies/write`

action, such as `Azure Kubernetes Service RBAC Writer`

, on the Microsoft Entra ID role they're assigned can add more network policies through the Kubernetes API.

For example, if an admin applies a `Deny All`

policy for ingress/egress, and a user applies an `Allow`

policy for a namespace via the Kubernetes API, the `Allow`

policy takes priority over the `Deny All`

policy, and traffic is allowed to flow for the namespace.

## Resource quotas

[Resource Quotas](operator-best-practices-scheduler#enforce-resource-quotas) are Kubernetes resources that are used to manage and limit the resource consumption of namespaces within a cluster. They allow administrators to define constraints on the amount of CPU, memory, storage, or other resources that are used by workloads in a namespace. By applying resource quotas, you can ensure fair resource distribution, prevent resource overuse, and maintain cluster stability.

Managed namespaces can be created with the following resource quotas:

**CPU requests and limits**: Define the minimum and maximum amount of CPU resources that workloads in the namespace can request or consume. The quota ensures that workloads have sufficient CPU resources to operate while preventing overuse that could affect other namespaces. The quota is defined in the[milliCPU form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu).**Memory requests and limits**: Specify the minimum and maximum amount of memory resources that workloads in the namespace can request or consume. The quota helps maintain stability by avoiding memory overcommitment and ensuring fair resource allocation across namespaces. The quota is defined in[power-of-two equivalents form](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory)such as`Ei`

,`Pi`

,`Ti`

,`Gi`

,`Mi`

,`Ki`

.

## Labels and annotations

Kubernetes [Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) and [Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) are metadata attached to Kubernetes objects, such as namespaces, to provide additional information. Labels are key-value pairs used to organize and select resources, enabling efficient grouping and querying. Annotations store nonidentifying metadata, such as configuration details or operational instructions, that are consumed by tools or systems.

You can optionally set Kubernetes Labels and Annotations to be applied on the namespace.

## Adoption policy

The adoption policy determines how an existing namespace in Kubernetes is handled when creating a managed namespace.

Warning

Onboarding an existing namespace to be managed can cause disruption. If the **resource quota** applied is less than what is already being requested by pods, new deployments and pods that exceed the quota is denied. Existing deployments aren't affected, but scaling is denied. Applying **network policies** to an existing namespace can affect existing traffic. Ensure that the policies are tested and validated to avoid unintended disruptions to communication between pods or external endpoints.

The following options are available:

**Never**: If the namespace already exists in the cluster, attempts to create that namespace as a managed namespace fails.**IfIdentical**: Take over the existing namespace to be managed, provided there are no differences between the existing namespace and the desired configuration.**Always**: Always take over the existing namespace to be managed, even if some fields in the namespace might be overwritten.

## Delete policy

The delete policy specifies how the Kubernetes namespace is handled when the managed namespace resource is deleted.

Warning

Deleting a managed namespace with the **Delete** policy causes all resources within that namespace, such as Deployments, Services, Ingresses, and other Kubernetes objects, to be deleted. Ensure that you back up or migrate any critical resources before proceeding.

The following options are available:

**Keep**: Only delete the managed namespace resource while keeping the Kubernetes namespace intact. Additionally, the`ManagedByARM`

label is removed from the namespace.**Delete**: Delete both the managed namespace resource and the Kubernetes namespace together.

## Managed namespaces built-in roles

Managed namespaces uses the following built-in roles for the control plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service Namespace User](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-namespace-user)Managed namespaces uses the following built-in roles for the data plane.

| Role | Description |
|---|---|
|

[Azure Kubernetes Service RBAC Writer](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-writer)[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles/containers#azure-kubernetes-service-rbac-admin)## Managed namespaces use cases

Properly setting up [namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/) with associated [quotas](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/) or [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/#networkpolicy-resource) can be complex and time-consuming. Managed namespaces allow you to set up preconfigured namespaces in your AKS clusters that you can interact with using the Azure CLI.

The following sections outline some common use cases for managed namespaces.

### Manage teams and resources on AKS

Let's say you're an admin at a small startup. You have an AKS cluster provisioned and want to set up namespaces for developers from your *finance*, *legal*, and *design* teams. As you're setting up your company's environment, you want to make sure that access is tightly controlled, resources are rightly scoped, and environments are organized properly.

The

*finance*team intakes forms and files from teams all across the company, but they hold sensitive information that ideally shouldn't leave their environment. Their applications and workflows are lighter on the computing side but consume a lot of memory. As a result, you decide to set up a namespace that allows for all network ingress, network egress only within their namespace, and scope their resources accordingly. A label to the namespace helps easily identify which team is using it.`az aks namespace add \ --name $FINANCE_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 512Mi \ --memory-limit 2Gi \ --ingress-policy AllowAll \ --egress-policy AllowSameNamespace \ --labels team=finance`

The

*legal*team deals primarily with sensitive data. Their applications use a fair amount of memory but require little compute resources. You decide to set up a namespace that's extremely restrictive for both the ingress/egress policies, and scope their resource quotas accordingly.`az aks namespace add \ --name $LEGAL_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 250m \ --cpu-limit 500m \ --memory-request 2Gi \ --memory-limit 5Gi \ --ingress-policy DenyAll \ --egress-policy DenyAll \ --labels team=legal`

The

*design*team needs the ability to freely flow data to showcase their work across the company. They also encourage teams to send them content for reference. Their applications are intensive and require a large chunk of memory and CPU. You decide to set them up with a minimally restrictive namespace and allocate a sizeable amount of resources for them.`az aks namespace add \ --name $DESIGN_NAMESPACE \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --cpu-request 2000m \ --cpu-limit 2500m \ --memory-request 5Gi \ --memory-limit 8Gi \ --ingress-policy AllowAll \ --egress-policy AllowAll \ --labels team=design`


With these namespaces set up, you now have environments for the three teams in your organization that should allow each team to get up and running in an environment that best suits their needs. Admins can use [Azure CLI calls](/en-us/cli/azure/aks/namespace) to update the namespaces as needs shift.

### View managed namespaces

As the number of teams you deal with expands, or as your organization grows, you might find yourself needing to review the namespaces you set up.

Let's say you want to review the namespaces in your cluster from the [previous section](#manage-teams-and-resources-on-aks) to ensure there are three namespaces.

Use the [ az aks namespace list](/en-us/cli/azure/aks/namespace#az-aks-namespace-list) command to review your namespaces.

```
az aks namespace list \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--output table
```


Your output should look similar to the following example output:

```
Name ResourceGroup Location
------------------ --------------- ----------
$CLUSTER_NAME/$DESIGN_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$LEGAL_NAMESPACE $RESOURCE_GROUP <LOCATION>
$CLUSTER_NAME/$FINANCE_NAMESPACE $RESOURCE_GROUP <LOCATION>
```


### Control access to managed namespaces

You can further use [Azure RBAC roles](#managed-namespaces-built-in-roles), scoped to each namespace, to determine which users have access to certain actions within the namespace. With the proper configuration, you can ensure users have all the access they need within the namespace, while limiting their access to other namespaces or cluster-wide resources.

## Next steps

- Learn how to
[create and use managed namespaces on Azure Kubernetes Service (AKS)](managed-namespaces). - Learn about
[multi-cluster managed namespaces](../kubernetes-fleet/concepts-fleet-managed-namespace)with Azure Kubernetes Fleet Manager.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-overview -->

# Use Microsoft Entra Workload ID with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Workloads deployed on an AKS cluster require Microsoft Entra application credentials or managed identities to access Microsoft Entra protected resources, such as Azure Key Vault and Microsoft Graph. Microsoft Entra Workload ID integrates with the capabilities native to Kubernetes to federate with external identity providers, allowing you to assign workload identities to your workloads to authenticate and access other services and resources.

[Microsoft Entra Workload ID](/en-us/azure/active-directory/develop/workload-identities-overview) uses [Service Account Token Volume Projection](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection) (or a *service account*), to enable pods to use a Kubernetes identity. A Kubernetes token is issued and [OpenID Connect (OIDC) federation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens) enables Kubernetes applications to access Azure resources securely with Microsoft Entra ID, based on annotated service accounts.

You can use Microsoft Entra Workload ID with [Azure Identity client libraries](#azure-identity-client-libraries) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL) collection, together with [application registration](/en-us/azure/active-directory/develop/application-model#register-an-application), to seamlessly authenticate and access Azure cloud resources.

Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [What is Service Connector?](/en-us/azure/service-connector/overview)

## Prerequisites

- AKS supports Microsoft Entra Workload ID on version 1.22 and higher.
- The Azure CLI version 2.47.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- You can have a maximum of
[20 federated identity credentials](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#general-federated-identity-credential-considerations)per managed identity. - It takes a few seconds for the federated identity credential to propagate after being initially added.
- The
[virtual nodes](virtual-nodes)add-on, based on the open source project[Virtual Kubelet](https://virtual-kubelet.io/docs/), isn't supported. - Creation of federated identity credentials isn't supported on user-assigned managed identities in
[these regions](/en-us/azure/active-directory/workload-identities/workload-identity-federation-considerations#unsupported-regions-user-assigned-managed-identities).

## Azure Identity client libraries

In the Azure Identity client libraries, choose one of the following approaches:

- Use
`DefaultAzureCredential`

, which attempts to use the`WorkloadIdentityCredential`

. - Create a
`ChainedTokenCredential`

instance that includes`WorkloadIdentityCredential`

. - Use
`WorkloadIdentityCredential`

directly.

The following table provides the **minimum** package version required for each language ecosystem's client library:

| Ecosystem | Library | Minimum version |
|---|---|---|
| .NET |
|

[azure-identity-cpp](https://github.com/Azure/azure-sdk-for-cpp/blob/main/sdk/identity/azure-identity/README.md)[azidentity](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity)[azure-identity](/en-us/java/api/overview/azure/identity-readme)[@azure/identity](/en-us/javascript/api/overview/azure/identity-readme)[azure-identity](/en-us/python/api/overview/azure/identity-readme)## Azure Identity client library code samples

The following code samples use the `DefaultAzureCredential`

. This credential type uses the environment variables injected by the workload identity mutating [webhook](#webhook-certificate-auto-rotation) to authenticate with Azure Key Vault. To see samples using one of the other approaches, refer to the [ecosystem-specific client libraries](#azure-identity-client-libraries).

```
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;
string keyVaultUrl = Environment.GetEnvironmentVariable("<key-vault-url>");
string secretName = Environment.GetEnvironmentVariable("<secret-name>");
var client = new SecretClient(
new Uri(keyVaultUrl),
new DefaultAzureCredential());
KeyVaultSecret secret = await client.GetSecretAsync(secretName);
```


## Microsoft Authentication Library (MSAL)

The following client libraries are the **minimum** version required:

| Ecosystem | Library | Image | Example | Has Windows |
|---|---|---|---|---|
| .NET |
|

`ghcr.io/azure/azure-workload-identity/msal-net:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-net/akvdotnet)[Microsoft Authentication Library-for-go](https://github.com/AzureAD/microsoft-authentication-library-for-go)`ghcr.io/azure/azure-workload-identity/msal-go:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-go)[Microsoft Authentication Library-for-java](https://github.com/AzureAD/microsoft-authentication-library-for-java)`ghcr.io/azure/azure-workload-identity/msal-java:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-java)[Microsoft Authentication Library-for-js](https://github.com/AzureAD/microsoft-authentication-library-for-js)`ghcr.io/azure/azure-workload-identity/msal-node:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-node)[Microsoft Authentication Library-for-python](https://github.com/AzureAD/microsoft-authentication-library-for-python)`ghcr.io/azure/azure-workload-identity/msal-python:latest`

[Link](https://github.com/Azure/azure-workload-identity/tree/main/examples/msal-python)## How it works

In this security model, the AKS cluster acts as the token issuer. Microsoft Entra ID uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library or the MSAL.

The following table describes the required OIDC issuer endpoints for Microsoft Entra Workload ID:

| Endpoint | Description |
|---|---|
`{IssuerURL}/.well-known/openid-configuration` |
Also known as the OIDC discovery document. This contains the metadata about the issuer's configurations. |
`{IssuerURL}/openid/v1/jwks` |
This contains the public signing key(s) that Microsoft Entra ID uses to verify the authenticity of the service account token. |

The following diagram summarizes the authentication sequence using OIDC:

### Webhook certificate auto-rotation

Similar to other webhook add-ons, the [cluster certificate auto-rotation](certificate-rotation#certificate-autorotation) operation rotates the certificate.

## Service account labels and annotations

Microsoft Entra Workload ID supports the following mappings related to a service account:

**One-to-one**, where a service account references a Microsoft Entra object.**Many-to-one**, where multiple service accounts reference the same Microsoft Entra object.**One-to-many**, where a service account references multiple Microsoft Entra objects by changing the client ID annotation. For more information, see[How to federate multiple identities with a Kubernetes service account](https://azure.github.io/azure-workload-identity/docs/faq.html#how-to-federate-multiple-identities-with-a-kubernetes-service-account).

Note

If you update the service account annotations, you must restart the pod for the changes to take effect.

If you've used [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity), think of a service account as an Azure security principal, except that a service account is part of the core Kubernetes API, rather than a [Custom Resource Definition](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) (CRD). The following sections describe a list of available labels and annotations that you can use to configure the behavior when exchanging the service account token for a Microsoft Entra access token.

### Service account annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/client-id` |
Represents the Microsoft Entra application client ID to be used with the pod. |
|
`azure.workload.identity/tenant-id` |
Represents the Azure tenant ID where the Microsoft Entra application is registered. |
AZURE_TENANT_ID environment variable extracted from `azure-wi-webhook-config` ConfigMap. |
`azure.workload.identity/service-account-token-expiration` |
Represents the `expirationSeconds` field for the projected service account token. It's an optional field that you configure to prevent any downtime caused by errors during service account token refresh. Kubernetes service account token expiry isn't correlated with Microsoft Entra tokens. Microsoft Entra tokens expire in 24 hours after they're issued. |
3600 Supported range is 3600-86400. |

### Pod labels

Note

For applications using Microsoft Entra Workload ID, it's required to add the label `azure.workload.identity/use: "true"`

to the pod spec for AKS to move the workload identity to a *Fail Close* scenario to provide a consistent and reliable behavior for pods that need to use workload identity. Otherwise, the pods fail after they're restarted.

| Label | Description | Recommended value | Required |
|---|---|---|---|
`azure.workload.identity/use` |
This label is required in the pod template spec. Only pods with this label are mutated by the azure-workload-identity mutating admission webhook to inject the Azure specific environment variables and the projected service account token volume. | true | Yes |

### Pod annotations

All annotations are optional. If the annotation isn't specified, the default value is used.

| Annotation | Description | Default |
|---|---|---|
`azure.workload.identity/service-account-token-expiration` |
See
Pod annotations take precedence over service account annotations. |

Supported range is 3600-86400.

`azure.workload.identity/skip-containers`

`container1;container2`

.`azure.workload.identity/use: true`

.`azure.workload.identity/inject-proxy-sidecar`

`azure.workload.identity/proxy-sidecar-port`

## Migrate to Microsoft Entra Workload ID

You can configure clusters already running a pod-managed identity to use Microsoft Entra Workload ID using one of two ways:

- Use the same configuration you implemented for pod-managed identity. You can annotate the service account within the namespace with the identity to enable Microsoft Entra Workload ID and inject the annotations into the pods.
- Rewrite your application to use the latest version of the Azure Identity client library.

To help streamline and ease the migration process, we developed a migration sidecar that converts the Instance Metadata Service (IMDS) transactions your application makes over to [OIDC](/en-us/azure/active-directory/develop/v2-protocols-oidc). The migration sidecar isn't intended to be a long-term solution, but a way to get up and running quickly on Microsoft Entra Workload ID. Running the migration sidecar within your application proxies the application IMDS transactions over to OIDC. The alternative approach is to upgrade to a supported version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library, which supports OIDC authentication.

The following table summarizes our migration or deployment recommendations for your AKS cluster:

| Scenario | Description |
|---|---|
| New or existing cluster deployment
|

Sample deployment resources:

[Deploy and configure Microsoft Entra Workload ID on a new cluster](workload-identity-deploy-cluster)[migration sidecar](workload-identity-migrate-from-pod-identity).## Next steps

- To learn how to set up your pod to authenticate using a workload identity as a migration option, see
[Modernize application authentication with Microsoft Entra Workload ID](workload-identity-migrate-from-pod-identity). - See
[Deploy and configure an AKS cluster with Microsoft Entra Workload ID](workload-identity-deploy-cluster), which helps you deploy a cluster and configure a sample application to use a workload identity.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-support-help -->

# Support and troubleshooting for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

## Self help troubleshooting


The [AKS troubleshooting documentation](/en-us/troubleshoot/azure/azure-kubernetes/welcome-azure-kubernetes) provides guidance for how to diagnose and resolve issues that you might encounter when using AKS. These articles cover how to troubleshoot deployment failures, security-related problems, connection issues, and more.

## Post a question on Microsoft Q&A


Azure's preferred destination for community support, [Microsoft Q&A](/en-us/answers/products/azure), allows you to ask technical questions and engage with Azure engineers, Most Valuable Professionals (MVPs), partners, and customers. When you ask a question, make sure you use the `azure-kubernetes-service`

tag. You can also submit your own answers and help other community members with their questions.

If you can't find an answer to your problem using search, you can submit a new question to Microsoft Q&A and tag it with the appropriate Azure service and area.

The following table lists the tags for AKS and related services:

## Create an Azure support request


Explore the range of [Azure support options](https://azure.microsoft.com/support/plans) and choose a plan that best fits your needs. Azure customers can create and manage support requests in the Azure portal.

If you already have an Azure Support Plan, you can [open a support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).

## Create a GitHub issue


If you need help with the languages and tools for developing and managing AKS, you can open an issue in its GitHub repository.

The following table lists the GitHub repositories for AKS and related services:

| Library | GitHub issues URL |
|---|---|
| Azure PowerShell |
|

[https://github.com/Azure/azure-cli/issues](https://github.com/Azure/azure-cli/issues)[https://github.com/Azure/azure-rest-api-specs/issues](https://github.com/Azure/azure-rest-api-specs/issues)[https://github.com/Azure/azure-sdk-for-java/issues](https://github.com/Azure/azure-sdk-for-java/issues)[https://github.com/Azure/azure-sdk-for-python/issues](https://github.com/Azure/azure-sdk-for-python/issues)[https://github.com/Azure/azure-sdk-for-net/issues](https://github.com/Azure/azure-sdk-for-net/issues)[https://github.com/Azure/azure-sdk-for-js/issues](https://github.com/Azure/azure-sdk-for-js/issues)[https://github.com/Azure/terraform/issues](https://github.com/Azure/terraform/issues)## Stay informed of updates and new releases


Learn about important product updates, roadmap, and announcements in [Azure Updates](https://azure.microsoft.com/updates/?searchterms=compute). For information about Azure Virtual Machines, see the [Azure blog](https://azure.microsoft.com/blog/product/virtual-machines/).

## Next steps

Visit the [Azure Kubernetes Service (AKS) documentation](./).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-v2 -->

# Migrate to Key Management Service (KMS) v2 in Azure Kubernetes Service (AKS) (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article applies to clusters using the legacy KMS experience that need to migrate from KMS v1 to KMS v2. For clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

In this article, you learn how to migrate to KMS v2 for clusters with versions older than 1.27. Beginning in AKS version 1.27, turning on the KMS feature configures KMS v2. With KMS v2, you aren't limited to the 2,000 secrets that earlier versions support. For more information, see [KMS v2 improvements](https://kubernetes.io/blog/2023/05/16/kms-v2-moves-to-beta/).

Important

If your cluster version is older than 1.27 and you already turned on KMS, the upgrade to cluster version 1.27 or later is blocked.

## Turn off KMS

Disable KMS on an existing cluster using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Upgrade your AKS cluster and turn on KMS

Upgrade your AKS cluster to version 1.27 or later using the

command with the`az aks upgrade`

`--kubernetes-version`

parameter set to your desired version. The following example upgrades to version`1.27.1`

:`az aks upgrade --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --kubernetes-version 1.27.1`

Once the upgrade completes, you can turn on KMS for a public or private key vault using one of the following resources:

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-scheduler -->

# Best practices for basic scheduler features in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. The Kubernetes scheduler lets you control the distribution of compute resources, or limit the impact of maintenance events.

This best practices article focuses on basic Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use resource quotas to provide a fixed amount of resources to teams or workloads
- Limit the impact of scheduled maintenance using pod disruption budgets

## Enforce resource quotas


Best practice guidancePlan and apply resource quotas at the namespace level. If pods don't define resource requests and limits, reject the deployment. Monitor resource usage and adjust quotas as needed.


Resource requests and limits are placed in the pod specification. Requests are used by the Kubernetes scheduler at deployment time to find an available node in the cluster. Limits and requests work at the individual pod level. For more information about how to define these values, see [Define pod resource requests and limits](developer-best-practices-resource-management#define-pod-resource-requests-and-limits).

To provide a way to reserve and limit resources across a development team or project, you should use *resource quotas*. These quotas are defined on a namespace, and can be used to set quotas on the following basis:

**Compute resources**, such as CPU and memory, or GPUs.**Storage resources**, including the total number of volumes or amount of disk space for a given storage class.**Object count**, such as maximum number of secrets, services, or jobs can be created.

Kubernetes doesn't overcommit resources. Once your cumulative resource request total passes the assigned quota, all further deployments will be unsuccessful.

When you define resource quotas, all pods created in the namespace must provide limits or requests in their pod specifications. If they don't provide these values, you can reject the deployment. Instead, you can [configure default requests and limits for a namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/).

The following example YAML manifest named *dev-app-team-quotas.yaml* sets a hard limit of a total of *10* CPUs, *20Gi* of memory, and *10* pods:

```
apiVersion: v1
kind: ResourceQuota
metadata:
name: dev-app-team
spec:
hard:
cpu: "10"
memory: 20Gi
pods: "10"
```


This resource quota can be applied by specifying the namespace, such as *dev-apps*:

```
kubectl apply -f dev-app-team-quotas.yaml --namespace dev-apps
```


Work with your application developers and owners to understand their needs and apply the appropriate resource quotas.

For more information about available resource objects, scopes, and priorities, see [Resource quotas in Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/).

## Plan for availability using pod disruption budgets


Best practice guidanceTo maintain the availability of applications, define Pod Disruption Budgets (PDBs) to make sure that a minimum number of pods are available in the cluster.


There are two disruptive events that cause pods to be removed:

### Involuntary disruptions

*Involuntary disruptions* are events beyond the typical control of the cluster operator or application owner. Include:

- Hardware failure on the physical machine
- Kernel panic
- Deletion of a node VM

Involuntary disruptions can be mitigated by:

- Using multiple replicas of your pods in a deployment.
- Running multiple nodes in the AKS cluster.

### Voluntary disruptions

*Voluntary disruptions* are events requested by the cluster operator or application owner. Include:

- Cluster upgrades
- Updated deployment template
- Accidentally deleting a pod

Kubernetes provides *pod disruption budgets* for voluntary disruptions, letting you plan for how deployments or replica sets respond when a voluntary disruption event occurs. Using pod disruption budgets, cluster operators can define a minimum available or maximum unavailable resource count.

If you upgrade a cluster or update a deployment template, the Kubernetes scheduler will schedule extra pods on other nodes before allowing voluntary disruption events to continue. The scheduler waits to reboot a node until the defined number of pods are successfully scheduled on other nodes in the cluster.

Let's look at an example of a replica set with five pods that run NGINX. The pods in the replica set are assigned the label `app: nginx-frontend`

. During a voluntary disruption event, such as a cluster upgrade, you want to make sure at least three pods continue to run. The following YAML manifest for a *PodDisruptionBudget* object defines these requirements:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
minAvailable: 3
selector:
matchLabels:
app: nginx-frontend
```


You can also define a percentage, such as *60%*, which allows you to automatically compensate for the replica set scaling up the number of pods.

You can define a maximum number of unavailable instances in a replica set. Again, a percentage for the maximum unavailable pods can also be defined. The following pod disruption budget YAML manifest defines that no more than two pods in the replica set be unavailable:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
maxUnavailable: 2
selector:
matchLabels:
app: nginx-frontend
```


Once your pod disruption budget is defined, you create it in your AKS cluster as with any other Kubernetes object:

```
kubectl apply -f nginx-pdb.yaml
```


Work with your application developers and owners to understand their needs and apply the appropriate pod disruption budgets.

For more information about using pod disruption budgets, see [Specify a disruption budget for your application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

## Next steps

This article focused on basic Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux -->

# Use the Azure Linux container host for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Linux container host for AKS is an open-source Linux distribution created by Microsoft, and it's generally available as a container host on Azure Kubernetes Service (AKS). The Azure Linux container host provides reliability and consistency from cloud to edge across the AKS, AKS-HCI, and Arc products. You can deploy Azure Linux node pools in a new cluster, add Azure Linux node pools to your existing Ubuntu clusters, or migrate your Ubuntu nodes to Azure Linux nodes. To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

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
<!-- Source: N/A -->

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
