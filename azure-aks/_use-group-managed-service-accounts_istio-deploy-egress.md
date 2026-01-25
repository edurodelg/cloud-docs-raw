---
merged_at: 2026-01-25T12:06:27.874243
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-group-managed-service-accounts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-group-managed-service-accounts -->

# Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Group Managed Service Accounts (GMSA)](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) is a managed domain account for multiple servers that provides automatic password management, simplified service principal name (SPN) management, and the ability to delegate management to other administrators. With Azure Kubernetes Service (AKS), you can enable GMSA on your Windows Server nodes, which allows containers running on Windows Server nodes to integrate with and be managed by GMSA.

## Prerequisites

- Kubernetes 1.19 or greater. To check your version, see
[Check for available upgrades](upgrade-aks-cluster#check-for-available-aks-cluster-upgrades). To upgrade your version, see[Upgrade AKS cluster](upgrade-aks-cluster). - Azure CLI version 2.35.0 or greater. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Managed identities](use-managed-identity)enabled on your AKS cluster.- Permissions to create or update an Azure Key Vault.
- Permissions to configure GMSA on Active Directory Domain Service or on-premises Active Directory.
- The domain controller must have Active Directory Web Services enabled and must be reachable on port 9389 by the AKS cluster.

Note

Microsoft also provides a purpose-built PowerShell module to configure gMSA on AKS. For more information, see [gMSA on Azure Kubernetes Service](/en-us/virtualization/windowscontainers/manage-containers/gmsa-aks-ps-module).

## Configure GMSA on Active Directory domain controller

To use GMSA with AKS, you need a standard domain user credential to access the GMSA credential configured on your domain controller. To configure GMSA on your domain controller, see [Get started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts). For the standard domain user credential, you can use an existing user or create a new one, as long as it has access to the GMSA credential.

Important

You must use either Active Directory Domain Service or on-premises Active Directory. At this time, you can't use Microsoft Entra ID to configure GMSA with an AKS cluster.

## Store the standard domain user credentials in Azure Key Vault

Your AKS cluster uses the standard domain user credentials to access the GMSA credentials from the domain controller. To provide secure access to those credentials for the AKS cluster, you should store them in Azure Key Vault.

If you don't already have an Azure key vault, create one using the

command.`az keyvault create`

`az keyvault create --resource-group myResourceGroup --name myGMSAVault`

Store the standard domain user credential as a secret in your key vault using the

command. The following example stores the domain user credential with the key`az keyvault secret set`

*GMSADomainUserCred*in the*myGMSAVault*key vault.`az keyvault secret set --vault-name myGMSAVault --name "GMSADomainUserCred" --value "$Domain\\$DomainUsername:$DomainUserPassword"`

Note

Make sure to use the fully qualified domain name for the domain.


### Optional: Use a custom virtual network with custom DNS

You need to configure your domain controller through DNS so it's reachable by the AKS cluster. You can configure your network and DNS outside of your AKS cluster to allow your cluster to access the domain controller. Alternatively, you can use Azure CNI to configure a custom virtual network with a custom DNS on your AKS cluster to provide access to your domain controller. For more information, see [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](configure-azure-cni).

### Optional: Configure more than one DNS server

If you want to configure more than one DNS server for Windows GMSA in your AKS cluster, don't specify `--gmsa-dns-server`

or `v--gmsa-root-domain-name`

. Instead, you can add multiple DNS servers in the virtual network by selecting *Custom DNS* and adding the DNS servers.

### Optional: Use your own kubelet identity for your cluster

To provide the AKS cluster access to your key vault, the cluster kubelet identity needs access to your key vault. When you create a cluster with managed identity enabled, a kubelet identity is automatically created by default.

You can either [grant access to your key vault for the identity after cluster creation](#enable-gmsa-on-existing-cluster) or create your own identity before cluster creation using the following steps:

Create a kubelet identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group myResourceGroup`

Get the ID of the identity using the

command and set it to a variable named`az identity list`

`MANAGED_ID`

.`MANAGED_ID=$(az identity list --query "[].id" -o tsv)`

Grant the identity access to your key vault using the

command.`az keyvault set-policy`

`az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get`


## Enable GMSA on a new AKS cluster

Create administrator credentials to use during cluster creation. The following commands prompt you for a username and set it to

`WINDOWS_USERNAME`

for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create an AKS cluster using the

command with the following parameters:`az aks create`

`--enable-windows-gmsa`

: Enables GMSA for the cluster.`--gmsa-dns-server`

: The IP address of the DNS server.`--gmsa-root-domain-name`

: The root domain name of the DNS server.

`DNS_SERVER=<IP address of DNS server> ROOT_DOMAIN_NAME="contoso.com" az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure \ --load-balancer-sku standard \ --windows-admin-username $WINDOWS_USERNAME \ --enable-windows-gmsa \ --gmsa-dns-server $DNS_SERVER \ --gmsa-root-domain-name $ROOT_DOMAIN_NAME \ --generate-ssh-keys`

Note

If you're using a custom virtual network, you need to specify the virtual network ID using the

`vnet-subnet-id`

parameter, and you might need to also add the`docker-bridge-address`

,`dns-service-ip`

, and`service-cidr`

parameters depending on your configuration.If you created your own identity for the kubelet identity, use the

`assign-kubelet-identity`

parameter to specify your identity.When you specify the

`--gmsa-dns-server`

and`--gmsa-root-domain-name`

parameters, a DNS forward rule is added to the`kube-system/coredns`

ConfigMap. This rule forwards the DNS requests for`$ROOT_DOMAIN_NAME`

from the pods to the`$DNS_SERVER`

.`$ROOT_DOMAIN_NAME:53 { errors cache 30 log forward . $DNS_SERVER }`


Add a Windows Server node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --node-count 1`


### Enable GMSA on existing cluster

Enable GMSA on an existing cluster with Windows Server nodes and managed identities enabled using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--enable-windows-gmsa \
--gmsa-dns-server $DNS_SERVER \
--gmsa-root-domain-name $ROOT_DOMAIN_NAME
```


## Grant access to your key vault for the kubelet identity

Note

Skip this step if you provided your own identity for the kubelet identity.

Grant access to your key vault for the kubelet identity using the [ az keyvault set-policy](/en-us/cli/azure/keyvault#az-keyvault-set-policy) command.

```
MANAGED_ID=$(az aks show -g myResourceGroup -n myAKSCluster --query "identityProfile.kubeletidentity.objectId" -o tsv)
az keyvault set-policy --name "myGMSAVault" --object-id $MANAGED_ID --secret-permissions get
```


## Install GMSA cred spec

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Create a new YAML named

*gmsa-spec.yaml*and paste in the following YAML. Make sure you replace the placeholders with your own values. Placeholders are indicated with angle brackets (`<>`

), for example replace`<GMSA_ACCOUNT_USERNAME>`

with an account name like`gmsa-account`

.`apiVersion: windows.k8s.io/v1 kind: GMSACredentialSpec metadata: name: aks-gmsa-spec # This name can be changed, but it will be used as a reference in the pod spec credspec: ActiveDirectoryConfig: GroupManagedServiceAccounts: - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso - Name: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account Scope: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com HostAccountConfig: PluginGUID: '{CCC2A336-D7F3-4818-A213-272B7924213E}' PortableCcgVersion: "1" PluginInput: "ObjectId=<MANAGED_IDENTITY_OBJECT_ID>;SecretUri=https://<KEY_VAULT_NAME>.vault.azure.net/secrets/<KEY_VAULT_SECRET_NAME>" # MANAGED_IDENTITY_OBJECT_ID is managed identity object ID GUID # KEY_VAULT_NAME is the name of your key vault, like myGMSAVault # KEY_VAULT_SECRET_NAME is the name of the key vault secret you created, like GMSADomainUserCred CmsPlugins: - ActiveDirectory DomainJoinConfig: DnsName: <DNS_DOMAIN_NAME> # Fully qualified domain name like contoso.com DnsTreeName: <DNS_ROOT_DOMAIN_NAME> # Root domain name like contoso.com Guid: <AD_DOMAIN_OBJECT_GUID> # Domain object GUID like 66aa66aa-bb77-cc88-dd99-00ee00ee00ee MachineAccountName: <GMSA_ACCOUNT_USERNAME> # GMSA account username like gmsa-account NetBiosName: <NETBIOS_DOMAIN_NAME> # NetBIOS domain name like contoso Sid: <AD_DOMAIN_OBJECT_SID> # Domain object SID like S-1-5-21-1111111111-2222222222-3333333333`


Note

AKS upgraded the `apiVersion`

of `GMSACredentialSpec`

from `windows.k8s.io/v1alpha1`

to `windows.k8s.io/v1`

in release v20230903.

Create a new YAML named

*gmsa-role.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRole metadata: name: aks-gmsa-role rules: - apiGroups: ["windows.k8s.io"] resources: ["gmsacredentialspecs"] verbs: ["use"] resourceNames: ["aks-gmsa-spec"]`

Create a new YAML file named

*gmsa-role-binding.yaml*and paste in the following YAML.`apiVersion: rbac.authorization.k8s.io/v1 kind: RoleBinding metadata: name: allow-default-svc-account-read-on-aks-gmsa-spec namespace: default subjects: - kind: ServiceAccount name: default namespace: default roleRef: kind: ClusterRole name: aks-gmsa-role apiGroup: rbac.authorization.k8s.io`

Apply the changes from

*gmsa-spec.yaml*,*gmsa-role.yaml*, and*gmsa-role-binding.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-spec.yaml kubectl apply -f gmsa-role.yaml kubectl apply -f gmsa-role-binding.yaml`


## Verify GMSA installation

Create a new YAML named

*gmsa-demo.yaml*and paste in the following YAML.`--- kind: ConfigMap apiVersion: v1 metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default data: run.ps1: | $ErrorActionPreference = "Stop" Write-Output "Configuring IIS with authentication." # Add required Windows features, since they are not installed by default. Install-WindowsFeature "Web-Windows-Auth", "Web-Asp-Net45" # Create simple ASP.NET page. New-Item -Force -ItemType Directory -Path 'C:\inetpub\wwwroot\app' Set-Content -Path 'C:\inetpub\wwwroot\app\default.aspx' -Value 'Authenticated as <B><%=User.Identity.Name%></B>, Type of Authentication: <B><%=User.Identity.AuthenticationType%></B>' # Configure IIS with authentication. Import-Module IISAdministration Start-IISCommitDelay (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/windowsAuthentication').Attributes['enabled'].value = $true (Get-IISConfigSection -SectionPath 'system.webServer/security/authentication/anonymousAuthentication').Attributes['enabled'].value = $false (Get-IISServerManager).Sites[0].Applications[0].VirtualDirectories[0].PhysicalPath = 'C:\inetpub\wwwroot\app' Stop-IISCommitDelay Write-Output "IIS with authentication is ready." C:\ServiceMonitor.exe w3svc --- apiVersion: apps/v1 kind: Deployment metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: replicas: 1 selector: matchLabels: app: gmsa-demo template: metadata: labels: app: gmsa-demo spec: securityContext: windowsOptions: gmsaCredentialSpecName: aks-gmsa-spec containers: - name: iis image: mcr.microsoft.com/windows/servercore/iis:windowsservercore-ltsc2019 imagePullPolicy: IfNotPresent command: - powershell args: - -File - /gmsa-demo/run.ps1 volumeMounts: - name: gmsa-demo mountPath: /gmsa-demo volumes: - configMap: defaultMode: 420 name: gmsa-demo name: gmsa-demo nodeSelector: kubernetes.io/os: windows --- apiVersion: v1 kind: Service metadata: labels: app: gmsa-demo name: gmsa-demo namespace: default spec: ports: - port: 80 targetPort: 80 selector: app: gmsa-demo type: LoadBalancer`

Apply the changes from

*gmsa-demo.yaml*using the`kubectl apply`

command.`kubectl apply -f gmsa-demo.yaml`

Get the IP address of the sample application using the

`kubectl get service`

command.`kubectl get service gmsa-demo --watch`

Initially, the

`EXTERNAL-IP`

for the`gmsa-demo`

service shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gmsa-demo LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

`EXTERNAL-IP`

address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`gmsa-demo LoadBalancer 10.0.37.27 EXTERNAL-IP 80:30572/TCP 2m`

Open a web browser to the external IP address of the

`gmsa-demo`

service.Authenticate with the

`$NETBIOS_DOMAIN_NAME\$AD_USERNAME`

and password and confirm you see`Authenticated as $NETBIOS_DOMAIN_NAME\$AD_USERNAME, Type of Authentication: Negotiate`

.

### Disable GMSA on an existing cluster

Disable GMSA on an existing cluster with Windows Server nodes using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--resource-group myResourceGroup \
--name myAKSCluster \
--disable-windows-gmsa
```


You can reenable GMSA on an existing cluster by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

## Troubleshooting

### No authentication is prompted when loading the page

If the page loads, but you aren't prompted to authenticate, use the `kubectl logs POD_NAME`

command to display the logs of your pod and verify you see *IIS with authentication is ready*.

Windows containers don't show logs on kubectl by default. To enable Windows containers to show logs, you need to embed the Log Monitor tool on your Windows image. For more information, see [Windows Container Tools](https://github.com/microsoft/windows-container-tools).

### Connection timeout when trying to load the page

If you receive a connection timeout when trying to load the page, verify the sample app is running using the `kubectl get pods --watch`

command. Sometimes the external IP address for the sample app service is available before the sample app pod is running.

### Pod fails to start and a winapi error shows in the pod events

If your pod doesn't start after running the `kubectl get pods --watch`

command and waiting several minutes, use the `kubectl describe pod POD_NAME`

command. If you see a *winapi error* in the pod events, it's likely an error in your GMSA cred spec configuration. Verify all the replacement values in *gmsa-spec.yaml* are correct, rerun `kubectl apply -f gmsa-spec.yaml`

, and redeploy the sample application.

### Container Credential Guard event logs show the directory service isn't available errors

If you see this error message, it might indicate that DNS queries are failing due to blocked TCP fallback.

When gMSA is enabled, the system performs DNS lookups to locate domain controllers, for example `_ldap._tcp.dc._msdcs.<domain>`

. In large Active Directory environments, these responses can exceed the 512-byte UDP limit. When the UDP limit is reached, the DNS server sets the truncated (TC) flag, prompting CoreDNS to retry the query over TCP, as required by [RFC5966](https://datatracker.ietf.org/doc/html/rfc5966). This fallback to TCP is essential for completing the authentication flow. If network security group (NSG) or firewall rules block TCP traffic on port 53, the DNS resolution, and therefore gMSA sign in fails.

To verify if this error is occurring in your environment, enable [CoreDNS query logging](coredns-custom) and use the `kubectl logs --namespace kube-system -l k8s-app=kube-dns`

command to view CoreDNS logs.

Look for patterns like this, where UDP responses are truncated and TCP retries fail:

```
[INFO] 10.123.123.200:62380 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. udp 49 false 512" NOERROR qr,aa,tc,rd,ra 1357 0.003399698s
[INFO] 10.123.123.200:64233 - 2 "ANY IN _ldap._tcp.dc._msdcs.contoso.com. tcp 49 false 65535" - - 0 6.009670817s
[ERROR] plugin/errors: 2 _ldap._tcp.dc._msdcs.contoso.com. ANY: read tcp 10.123.123.11:55216-><DNS server IP>:53: i/o timeout
```


To resolve this error, we recommend updating your NSG or firewall rules to explicitly allow DNS traffic over TCP on port 53. This update will ensure that large DNS responses can be successfully retried over TCP, enabling the authentication flow to complete as expected.

## Next steps

For more information, see [Windows containers considerations with Azure Kubernetes Service (AKS)](windows-vs-linux-containers).


---

<!-- DOCUMENTO FUSIONADO: istio-deploy-egress.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-egress -->

# Deploy egress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy egress gateways for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

## Overview

The Istio egress gateway can serve as a centralized point to monitor and restrict outbound traffic from applications in the mesh. With the Istio add-on, you can deploy multiple egress gateways across different namespaces, allowing you to set up an egress gateway topology of your choice: egress gateways per-cluster, per-namespace, per-workload, etc. While AKS manages the provisioning and lifecycle of the Istio add-on egress gateways, you must create Istio custom resources to route traffic from applications in the mesh through the egress gateway and apply policies and telemetry collection.

The Istio add-on egress gateway also builds on top of and requires the [Static Egress Gateway](configure-static-egress-gateway) feature, which assigns a fixed source IP address prefix to the Istio egress Pods. You can use this predicable egress IP range for firewall rules and other outbound traffic filtering mechanisms. By using Istio egress gateway on top of Static Egress Gateway, you can apply Istio L7, identity-based policies, and IP-based restrictions for defense-in-depth egress traffic control. Additionally, directing outbound traffic through the Istio egress gateway allows multiple workloads to route traffic via the Static Egress Gateway node pools without modifying those application pods/deployments directly.

## Limitations and requirements

- You can enable a maximum of
`500`

Istio add-on egress gateways per cluster. - Istio add-on egress gateway names must be unique per namespace.
- Istio add-on egress gateway names must be between
`1-53`

characters, must only consist of lowercase alphanumerical characters, '-' and '.,' and must start and end with an alphanumerical character. Names should also be a valid Domain Name System (DNS) name. The regex used for name validation is`^[a-z0-9]([-a-z0-9]*[a-z0-9])?(\.[a-z0-9]([-a-z0-9]*[a-z0-9])?)*$`

. - Using the
[Kubernetes Gateway API](istio-gateway-api)for egress traffic management with the Istio add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - Because Static Egress Gateway is currently not supported on
[Azure CNI Pod Subnet clusters](concepts-network-azure-cni-pod-subnet), the Istio add-on egress gateway isn't supported on Pod Subnet clusters either.

## Prerequisites

### Enable Istio add-on

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster.

### Update Azure CLI version

You must use `azure-cli`

version `2.80.0`

or higher. Run `az --version`

to find your `azure-cli`

version, and run `az upgrade`

to upgrade.

### Enable and configure Static Egress Gateway

Follow the instructions in the [Static Egress Gateway documentation](configure-static-egress-gateway) to enable Static Egress Gateway on your cluster, create a node pool of mode `gateway`

, and create a `StaticGatewayConfiguration`

resource.

## Enable an Istio egress gateway

Note

The Istio add-on egress gateway pods don't get scheduled onto the `gateway`

node pool. The `gateway`

node pool is only used to route egress traffic and doesn't serve general-purpose workloads. If you need the egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-egress-gateway`

to enable an Istio egress gateway on your AKS cluster. You must specify a name for the Istio egress gateway and the name of the `StaticGatewayConfiguration`

that you created in the [prerequisites](#prerequisites) step. You can also specify a namespace to deploy the Istio egress gateway in, which must be the same namespace that the `StaticGatewayConfiguration`

was created in. If you don't specify a namespace, the egress gateway gets provisioned in the `aks-istio-egress`

namespace.

As a best-practice, you should wait until the `StaticGatewayConfiguration`

is assigned an `egressIpPrefix`

before enabling the Istio egress gateway using that gateway configuration.

```
az aks mesh enable-egress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --istio-egressgateway-name $ISTIO_EGRESS_NAME --istio-egressgateway-namespace $ISTIO_EGRESS_NAMESPACE --gateway-configuration-name $ISTIO_SGC_NAME
```


Verify that the service gets created for the egress gateway.

```
kubectl get svc $ISTIO_EGRESS_NAME -n $ISTIO_EGRESS_NAMESPACE
```


You should see a `ClusterIP`

service for the egress gateway:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
asm-egress-test ClusterIP 10.0.128.17 <none> 15021/TCP,80/TCP,443/TCP 6d4h
```


You can also verify that a deployment gets created for the Istio egress gateway and that the egress gateway pods have the `kubernetes.azure.com/static-gateway-configuration`

annotation set to the `gatewayConfigurationName`

.

```
ASM_REVISION=$(az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME | jq '.serviceMeshProfile.istio.revisions[0]' | sed 's/"//g')
kubectl get deployment $ISTIO_EGRESS_NAME-$ASM_REVISION -n $ISTIO_EGRESS_NAMESPACE -o jsonpath={.spec.template.metadata.annotations."kubernetes\.azure\.com\/static-gateway-configuration"}
```


You can run the `az aks mesh enable-egress-gateway`

command again to create another Istio egress gateway.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for each egress gateway gets created for the new control plane revision.

## Route traffic through the Istio egress gateway

### Set `outboundTrafficPolicy.mode`


By default, the Istio `outboundTrafficPolicy.mode`

is set to `ALLOW_ANY`

, meaning that Envoy passes through requests for unknown services. As a security best-practice, you should set the Istio `outboundTrafficPolicy.mode`

to `REGISTRY_ONLY`

so that the Istio proxy blocks requests to services that weren't added to Istio's Service Registry. You can add hosts outside of the cluster to Istio's service registry with a `ServiceEntry`

.

You can configure the `outboundTrafficPolicy.mode`

on a mesh-wide level using the Istio add-on [shared MeshConfig](istio-meshconfig), or use the [Sidecar Custom Resource](https://istio.io/latest/docs/reference/config/networking/sidecar/#OutboundTrafficPolicy) to target specific namespaces or workloads.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: istio-shared-configmap-asm-1-27
namespace: aks-istio-system
data:
mesh: |-
outboundTrafficPolicy:
mode: REGISTRY_ONLY
```


### Deploy sample application

In this example, we deploy the `curl`

application in the same namespace as the Istio add-on egress gateway. Remember to label the `ISTIO_EGRESS_NAMESPACE`

with the `istio.io/rev`

label so that the deployed application pod gets injected with a sidecar:

```
kubectl label namespace $ISTIO_EGRESS_NAMESPACE istio.io/rev=$ASM_REVISION
```


Then, deploy the sample application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.27/samples/curl/curl.yaml -n $ISTIO_EGRESS_NAMESPACE
```


You should see the `curl`

pod running with an injected sidecar container:

```
NAME READY STATUS RESTARTS AGE
curl-5b549b49b8-bcgts 2/2 Running 0 13s
```


Try sending a request from `curl`

directly to `edition.cnn.com`

:

```
SOURCE_POD=$(kubectl get pod -n $ISTIO_EGRESS_NAMESPACE -l app=curl -o jsonpath={.items..metadata.name})
kubectl exec -n $ISTIO_EGRESS_NAMESPACE "$SOURCE_POD" -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


If you set `outboundTrafficPolicy.mode`

to `REGISTRY_ONLY`

, then the `curl`

request should fail because you didn't create a `ServiceEntry`

for `edition.cnn.com`

. If `outboundTrafficPolicy.mode`

is `ALLOW_ANY`

, then the request should succeed.

To actually route requests to `edition.cnn.com`

from the `curl`

pod to the Istio add-on egress gateway, you need to create a `ServiceEntry`

and configure other Istio custom resources. Follow instructions one of the subsequent sections to configure an [HTTP Egress Gateway](#configure-an-http-istio-egress-gateway), [HTTPS Egress Gateway](#configure-an-https-istio-egress-gateway), or an [Egress Gateway that originates a Transport Layer Security (TLS) connection](#configure-an-istio-egress-gateway-to-perform-tls-origination).

Before starting any of the following scenarios, set these environment variables:

```
ISTIO_EGRESS_DEPLOYMENT=$ISTIO_EGRESS_NAME-$ASM_REVISION
EGRESS_GTW_SELECTOR=$(kubectl get deployment $ISTIO_EGRESS_DEPLOYMENT -n $ISTIO_EGRESS_NAMESPACE -o jsonpath={.metadata.labels.istio})
```


You can also [enable Envoy access logging](https://istio.io/latest/docs/tasks/observability/logs/access-log/) either through the [MeshConfig](istio-meshconfig) or [Telemetry API](istio-telemetry). Once you have access logging enabled, you can verify that traffic is flowing through the egress gateway by inspecting the `istio-proxy`

container logs:

```
kubectl logs -l istio=$EGRESS_GTW_SELECTOR -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an HTTP Istio egress gateway

- Create a
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 80
name: http-port
protocol: HTTP
- number: 443
name: https
protocol: HTTPS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway. Be sure to set the gateway selector and service Fully Qualified Domain Name (FQDN) accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- edition.cnn.com
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- istio-egressgateway
- mesh
http:
- match:
- gateways:
- mesh
port: 80
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 80
weight: 100
- match:
- gateways:
- istio-egressgateway
port: 80
route:
- destination:
host: edition.cnn.com
port:
number: 80
weight: 100
EOF
```


- Try sending an HTTP request from the
`curl`

pod to`edition.cnn.com`

:

```
kubectl exec -n $ISTIO_EGRESS_NAMESPACE "$SOURCE_POD" -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


You should see an `HTTP/2 200`

response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an HTTPS Istio egress gateway

- Create an HTTPS
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 443
name: tls
protocol: TLS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway. Be sure to set the gateway selector and service FQDN accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 443
name: tls
protocol: TLS
hosts:
- edition.cnn.com
tls:
mode: PASSTHROUGH
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- mesh
- istio-egressgateway
tls:
- match:
- gateways:
- mesh
port: 443
sniHosts:
- edition.cnn.com
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 443
- match:
- gateways:
- istio-egressgateway
port: 443
sniHosts:
- edition.cnn.com
route:
- destination:
host: edition.cnn.com
port:
number: 443
weight: 100
EOF
```


- Try sending an HTTPS request from
`curl`

to`edition.cnn.com`

:

```
kubectl exec "$SOURCE_POD" -n $ISTIO_EGRESS_NAMESPACE -c curl -- curl -sSL -o /dev/null -D - https://edition.cnn.com/politics
```


You should see an `HTTP/2 200`

response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


### Configure an Istio egress gateway to perform TLS Origination

- Create a
`ServiceEntry`

for`edition.cnn.com`

:

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: cnn
spec:
hosts:
- edition.cnn.com
ports:
- number: 80
name: http
protocol: HTTP
- number: 443
name: https
protocol: HTTPS
resolution: DNS
EOF
```


- Create the
`Gateway`

,`VirtualService`

, and`DestinationRule`

to route HTTP traffic from the`curl`

application to`edition.cnn.com`

through the egress gateway, and to perform TLS origination at the egress gateway. Be sure to set the gateway selector and service FQDN accordingly based on the`istio`

label selector in the egress gateway deployment.

```
kubectl apply -n $ISTIO_EGRESS_NAMESPACE -f - <<EOF
apiVersion: networking.istio.io/v1
kind: Gateway
metadata:
name: istio-egressgateway
spec:
selector:
istio: $EGRESS_GTW_SELECTOR
servers:
- port:
number: 80
name: https-port-for-tls-origination
protocol: HTTPS
hosts:
- edition.cnn.com
tls:
mode: ISTIO_MUTUAL
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: egressgateway-for-cnn
spec:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subsets:
- name: cnn
trafficPolicy:
loadBalancer:
simple: ROUND_ROBIN
portLevelSettings:
- port:
number: 80
tls:
mode: ISTIO_MUTUAL
sni: edition.cnn.com
---
apiVersion: networking.istio.io/v1
kind: VirtualService
metadata:
name: direct-cnn-through-egress-gateway
spec:
hosts:
- edition.cnn.com
gateways:
- istio-egressgateway
- mesh
http:
- match:
- gateways:
- mesh
port: 80
route:
- destination:
host: $ISTIO_EGRESS_NAME.$ISTIO_EGRESS_NAMESPACE.svc.cluster.local
subset: cnn
port:
number: 80
weight: 100
- match:
- gateways:
- istio-egressgateway
port: 80
route:
- destination:
host: edition.cnn.com
port:
number: 443
weight: 100
---
apiVersion: networking.istio.io/v1
kind: DestinationRule
metadata:
name: originate-tls-for-edition-cnn-com
spec:
host: edition.cnn.com
trafficPolicy:
loadBalancer:
simple: ROUND_ROBIN
portLevelSettings:
- port:
number: 443
tls:
mode: SIMPLE # initiates HTTPS for connections to edition.cnn.com
EOF
```


- Try sending a request form
`curl`

to`edition.cnn.com`

with the egress gateway performing TLS origination;

```
kubectl exec "${SOURCE_POD}" -n $ISTIO_EGRESS_NAMESPACE -c curl -- curl -sSL -o /dev/null -D - http://edition.cnn.com/politics
```


You should see a `200`

status response.

- Clean up resources

```
kubectl delete serviceentry cnn -n $ISTIO_EGRESS_NAMESPACE
kubectl delete gateway istio-egressgateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete virtualservice direct-cnn-through-egress-gateway -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule originate-tls-for-edition-cnn-com -n $ISTIO_EGRESS_NAMESPACE
kubectl delete destinationrule egressgateway-for-cnn -n $ISTIO_EGRESS_NAMESPACE
```


## Disable the Istio egress gateway

Run the `az aks mesh disable-egress-gateway`

command to disable the Istio add-on egress gateway that you created:

```
az aks mesh disable-egress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --istio-egressgateway-name $ISTIO_EGRESS_NAME --istio-egressgateway-namespace $ISTIO_EGRESS_NAMESPACE
```


Once you disable the Istio egress gateway, you should be able to delete the `StaticGatewayConfiguration`

, namespace, and `gateway`

node pool that the egress gateway was using if no other Istio egress gateway is using them.

## Next steps

[Configure ingress for Istio service mesh add-on with the Kubernetes Gateway API](istio-gateway-api)[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Configure egress gateway Horizontal Pod Autoscaler (HPA)](istio-scale#scaling)

Note

If there are any issues encountered with deploying the Istio egress gateway or configuring egress traffic routing, refer to [article on troubleshooting Istio add-on egress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-egress-gateway)
