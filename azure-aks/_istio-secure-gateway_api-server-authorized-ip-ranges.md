---
merged_at: 2026-01-25T12:06:27.863557
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-secure-gateway.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-secure-gateway -->

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

<!-- DOCUMENTO FUSIONADO: api-server-authorized-ip-ranges.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges -->

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
