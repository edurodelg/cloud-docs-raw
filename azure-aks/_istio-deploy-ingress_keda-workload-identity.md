---
merged_at: 2026-01-25T12:06:27.830645
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-deploy-ingress.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
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
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
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
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways:

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports health probe annotations for ports 80 and 443. Learn more about the usage of ports [here](/en-us/azure/aks/load-balancer-standard#customize-the-load-balancer-health-probe).

### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)


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
