---
merged_at: 2026-01-25T12:25:33.950617
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: keda-workload-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/keda-workload-identity -->

# Securely scale your applications using the KEDA add-on and workload identity on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to securely scale your applications with the Kubernetes Event-driven Autoscaling (KEDA) add-on and workload identity on Azure Kubernetes Service (AKS).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

## Create a resource group

Create a resource group using the

command. Make sure you replace the placeholder values with your own values.`az group create`

`LOCATION=<azure-region> RG_NAME=<resource-group-name> az group create --name $RG_NAME --location $LOCATION`


## Create an AKS cluster

Create an AKS cluster with the KEDA add-on, workload identity, and OIDC issuer enabled using the

command with the`az aks create`

`--enable-workload-identity`

,`--enable-keda`

, and`--enable-oidc-issuer`

flags. Make sure you replace the placeholder value with your own value.`AKS_NAME=<cluster-name> az aks create \ --name $AKS_NAME \ --resource-group $RG_NAME \ --enable-workload-identity \ --enable-oidc-issuer \ --enable-keda \ --generate-ssh-keys`

Validate the deployment was successful and make sure the cluster has KEDA, workload identity, and OIDC issuer enabled using the

command with the`az aks show`

`--query`

flag set to`"[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

.`az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query "[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --name $AKS_NAME \ --resource-group $RG_NAME \ --overwrite-existing`


## Create an Azure Service Bus

Create an Azure Service Bus namespace using the

command. Make sure to replace the placeholder value with your own value.`az servicebus namespace create`

`SB_NAME=<service-bus-name> SB_HOSTNAME="${SB_NAME}.servicebus.windows.net" az servicebus namespace create \ --name $SB_NAME \ --resource-group $RG_NAME \ --disable-local-auth`

Create an Azure Service Bus queue using the

command. Make sure to replace the placeholder value with your own value.`az servicebus queue create`

`SB_QUEUE_NAME=<service-bus-queue-name> az servicebus queue create \ --name $SB_QUEUE_NAME \ --namespace $SB_NAME \ --resource-group $RG_NAME`


## Create a managed identity

Create a managed identity using the

command. Make sure to replace the placeholder value with your own value.`az identity create`

`MI_NAME=<managed-identity-name> MI_CLIENT_ID=$(az identity create \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "clientId" \ --output tsv)`

Get the OIDC issuer URL using the

command with the`az aks show`

`--query`

flag set to`oidcIssuerProfile.issuerUrl`

.`AKS_OIDC_ISSUER=$(az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query oidcIssuerProfile.issuerUrl \ --output tsv)`

Create a federated credential between the managed identity and the namespace and service account used by the workload using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_WORKLOAD=<federated-credential-workload-name> az identity federated-credential create \ --name $FED_WORKLOAD \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:default:$MI_NAME \ --audience api://AzureADTokenExchange`

Create a second federated credential between the managed identity and the namespace and service account used by the keda-operator using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_KEDA=<federated-credential-keda-name> az identity federated-credential create \ --name $FED_KEDA \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:kube-system:keda-operator \ --audience api://AzureADTokenExchange`


## Create role assignments

Get the object ID for the managed identity using the

command with the`az identity show`

`--query`

flag set to`"principalId"`

.`MI_OBJECT_ID=$(az identity show \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "principalId" \ --output tsv)`

Get the Service Bus namespace resource ID using the

command with the`az servicebus namespace show`

`--query`

flag set to`"id"`

.`SB_ID=$(az servicebus namespace show \ --name $SB_NAME \ --resource-group $RG_NAME \ --query "id" \ --output tsv)`

Assign the Azure Service Bus Data Owner role to the managed identity using the

command.`az role assignment create`

`az role assignment create \ --role "Azure Service Bus Data Owner" \ --assignee-object-id $MI_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $SB_ID`


## Enable Workload Identity on KEDA operator

After creating the federated credential for the

`keda-operator`

ServiceAccount, you will need to manually restart the`keda-operator`

pods to ensure Workload Identity environment variables are injected into the pod.`kubectl rollout restart deploy keda-operator -n kube-system`

Confirm the keda-operator pods restart

`kubectl get pod -n kube-system -lapp=keda-operator -w`

Once you've confirmed the keda-operator pods have finished rolling hit

`Ctrl+c`

to break the previous watch command then confirm the Workload Identity environment variables have been injected.`KEDA_POD_ID=$(kubectl get po -n kube-system -l app.kubernetes.io/name=keda-operator -ojsonpath='{.items[0].metadata.name}') kubectl describe po $KEDA_POD_ID -n kube-system`

You should see output similar to the following under

**Environment**.`--- AZURE_CLIENT_ID: AZURE_TENANT_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx AZURE_FEDERATED_TOKEN_FILE: /var/run/secrets/azure/tokens/azure-identity-token AZURE_AUTHORITY_HOST: https://login.microsoftonline.com/ ---`

Deploy a KEDA TriggerAuthentication resource that includes the User-Assigned Managed Identity's Client ID.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: TriggerAuthentication metadata: name: azure-servicebus-auth namespace: default # this must be same namespace as the ScaledObject/ScaledJob that will use it spec: podIdentity: provider: azure-workload identityId: $MI_CLIENT_ID EOF`

Note

With the TriggerAuthentication in place, KEDA will be able to authenticate via workload identity. The

`keda-operator`

Pods use the`identityId`

to authenticate against Azure resources when evaluating scaling triggers.

## Publish messages to Azure Service Bus

At this point everything is configured for scaling with KEDA and Microsoft Entra Workload Identity. We will test this by deploying producer and consumer workloads.

Create a new ServiceAccount for the workloads.

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: $MI_CLIENT_ID name: $MI_NAME EOF`

Deploy a Job to publish 100 messages.

`kubectl apply -f - <<EOF apiVersion: batch/v1 kind: Job metadata: name: myproducer spec: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myproducer resources: {} env: - name: OPERATION_MODE value: "producer" - name: MESSAGE_COUNT value: "100" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never EOF`


## Consume messages from Azure Service Bus

Now that we have published messages to the Azure Service Bus queue, we will deploy a ScaledJob to consume the messages. This ScaledJob will use the KEDA TriggerAuthentication resource to authenticate against the Azure Service Bus queue using the workload identity and scale out every 10 messages.

Deploy a ScaledJob resource to consume the messages. The scale trigger will be configured to scale out every 10 messages. The KEDA scaler will create 10 jobs to consume the 100 messages.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: ScaledJob metadata: name: myconsumer-scaledjob spec: jobTargetRef: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myconsumer env: - name: OPERATION_MODE value: "consumer" - name: MESSAGE_COUNT value: "10" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never triggers: - type: azure-servicebus metadata: queueName: $SB_QUEUE_NAME namespace: $SB_NAME messageCount: "10" authenticationRef: name: azure-servicebus-auth EOF`

Note

ScaledJob creates a Kubernetes Job resource whenever a scaling event occurs and thus a Job template needs to be passed in when creating the resource. As new Jobs are created, Pods will be deployed with workload identity bits to consume messages.

Verify the KEDA scaler worked as intended.

`kubectl describe scaledjob myconsumer-scaledjob`

You should see events similar to the following.

`Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal KEDAScalersStarted 10m scale-handler Started scalers watch Normal ScaledJobReady 10m keda-operator ScaledJob is ready for scaling Warning KEDAScalerFailed 10m scale-handler context canceled Normal KEDAJobsCreated 10m scale-handler Created 10 jobs`


## Clean up resources

After you verify that the deployment is successful, you can clean up the resources to avoid incurring Azure costs.

Delete the Azure resource group and all resources in it using the [

`az group delete`

][az-group-delete] command.`az group delete --name $RG_NAME --yes --no-wait`


## Next steps

This article showed you how to securely scale your applications using the KEDA add-on and workload identity in AKS.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more about KEDA, see the [upstream KEDA docs](https://keda.sh/docs/2.12/).


---

<!-- DOCUMENTO FUSIONADO: ha-dr-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ha-dr-overview -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:
