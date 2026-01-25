---
merged_at: 2026-01-25T15:16:21.136572
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___node-autoprovision_node-auto-provisioning_create-nginx-ingress-private-contro_a05ab1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __node-autoprovision_node-auto-provisioning_create-nginx-ingress-private-control_51c857.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _node-autoprovision_node-auto-provisioning.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-autoprovision.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision -->

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

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning -->

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

<!-- DOCUMENTO FUSIONADO: create-nginx-ingress-private-controller.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/create-nginx-ingress-private-controller -->

# Configure NGINX ingress controller to support Azure private DNS zone with application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure an NGINX ingress controller to work with an Azure internal load balancer. It also explains how to configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains.

## Before you begin

An AKS cluster with the

[application routing add-on](app-routing).To attach an Azure private DNS Zone, you need the

[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner),[Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or[Azure coadministrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles)role on your Azure subscription.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell, `kubectl`

is already installed.

The following example configures connecting to your cluster named *aks-cluster* in the *test-rg* using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials \
--resource-group test-rg \
--name aks-cluster
```


## Create a virtual network

To publish a private DNS zone to your virtual network, specify a list of virtual networks that are allowed to resolve records within the zone with [virtual network links](/en-us/azure/dns/private-dns-virtual-network-links).

The following example creates a virtual network named *vnet-1* in the *test-rg* resource group, and one subnet named *subnet-1* to create within the virtual network with a specific address prefix.

```
az network vnet create \
--name vnet-1 \
--resource-group test-rg \
--location eastus \
--address-prefix 10.2.0.0/16 \
--subnet-name subnet-1 \
--subnet-prefixes 10.2.0.0/24
```


## Create an Azure private DNS zone

Note

You can configure the application routing add-on to automatically create records on one or more Azure global and private DNS zones for hosts defined on ingress resources. All global Azure DNS zones and all private Azure DNS zones must be in the same resource group.

Create a DNS zone using the [az network private-dns zone create](/en-us/cli/azure/network/private-dns/zone?#az-network-private-dns-zone-create) command, specifying the name of the zone and the resource group to create it in. The following example creates a DNS zone named *private.contoso.com* in the *test-rg* resource group.

```
az network private-dns zone create \
--resource-group test-rg \
--name private.contoso.com
```


You create a virtual network link to the DNS zone created earlier using the [az network private-dns link vnet create](/en-us/cli/azure/network/private-dns/link/vnet#az-network-private-dns-link-vnet-create) command. The following example creates a link named *dns-link* to the zone *private.contoso.com* for the virtual network *vnet-1*. Include the `--registration-enabled`

parameter to specify the link isn't registration enabled.

```
az network private-dns link vnet create \
--resource-group test-rg \
--name dns-link \
--zone-name private.contoso.com \
--virtual-network vnet-1 \
--registration-enabled false
```


The Azure DNS private zone auto registration feature manages DNS records for virtual machines deployed in a virtual network. When you link a virtual network with a private DNS zone with this setting enabled, a DNS record gets created for each Azure virtual machine for your AKS node deployed in the virtual network.

## Attach an Azure private DNS zone to the application routing add-on

Note

The `az aks approuting zone add`

command uses the permissions of the user running the command to create the [Azure DNS Zone](/en-us/azure/dns/dns-protect-private-zones-recordsets) role assignment. The **Private DNS Zone Contributor** role is a built-in role for managing private DNS resources and is assigned to the add-on's managed identity. For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Retrieve the resource ID for the DNS zone using the

command and set the output to a variable named`az network dns zone show`

`ZONEID`

. The following example queries the zone*private.contoso.com*in the resource group*test-rg*.`ZONEID=$(az network private-dns zone show \ --resource-group test-rg \ --name private.contoso.com \ --query "id" \ --output tsv)`

Update the add-on to enable integration with Azure DNS using the

command. You can pass a comma-separated list of DNS zone resource IDs. The following example updates the AKS cluster`az aks approuting zone`

*aks-cluster*in the resource group*test-rg*.`az aks approuting zone add \ --resource-group test-rg \ --name aks-cluster \ --ids=${ZONEID} \ --attach-zones`


## Create an NGINX ingress controller with a private IP address and an internal load balancer

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://aka.ms/aks/approuting/nginxingresscontrollercrd) to configure NGINX ingress controllers. You can create more ingress controllers or modify an existing configuration.

`NginxIngressController`

CRD has a `loadBalancerAnnotations`

field to control the behavior of the NGINX ingress controller's service by setting load balancer annotations. For more information about load balancer annotations, see [Customizations via Kubernetes annotations](configure-load-balancer-standard#customizations-via-kubernetes-annotations).

Perform the following steps to create an NGINX ingress controller with an internal facing Azure Load Balancer with a private IP address.

Copy the following YAML manifest into a new file named

**nginx-internal-controller.yaml**and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`

Verify the ingress controller was created

You can verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller`

The following example output shows the created resource. It might take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE default webapprouting.kubernetes.azure.com nginx True nginx-internal nginx-internal nginx-internal True`


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest creates the necessary deployments and services for the AKS store application.

## Create the Ingress resource that uses a host name on the Azure private DNS zone and a private IP address

Update ** host** with the name of your DNS host, for example,

**store-front.private.contoso.com**. Verify you're specifying nginx-internal for the ingressClassName.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: nginx-internal rules: - host: store-front.private.contoso.com http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the [ kubectl get ingress](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front nginx-internal store-front.private.contoso.com 80 10s
```


## Verify the Azure private DNS zone was updated

In a few minutes, run the [az network private-dns record-set a list](/en-us/cli/azure/network/private-dns/record-set/a#az-network-private-dns-record-set-a-list) command to view the A records for your Azure private DNS zone. Specify the name of the resource group and the name of the DNS zone. In this example, the resource group is *test-rg* and DNS zone is *private.contoso.com*.

```
az network private-dns record-set a list \
--resource-group test-rg \
--zone-name private.contoso.com
```


The following example output shows the created record:

```
[
{
"aRecords": [
{
"ipv4Address": "10.224.0.7"
}
],
"etag": "ecc303c5-4577-4ca2-b545-d34e160d1c2d",
"fqdn": "store-front.private.contoso.com.",
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/test-rg/providers/Microsoft.Network/privateDnsZones/private.contoso.com/A/store-front",
"isAutoRegistered": false,
"name": "store-front",
"resourceGroup": "test-rg",
"ttl": 300,
"type": "Microsoft.Network/privateDnsZones/A"
}
]
```


## Next steps

For other configuration information related to SSL encryption other advanced NGINX ingress controller and ingress resource configuration, review [DNS and SSL configuration](app-routing-dns-ssl) and [application routing add-on configuration](app-routing-nginx-configuration).


---

<!-- DOCUMENTO FUSIONADO: _ai-toolchain-operator-mcp_egress-outboundtype.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator-mcp.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-mcp -->

# Integrate an MCP server with an LLM Inference Service on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you connect an MCP-compliant tool server with an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS), enabling secure and modular tool calling for LLM applications. You also learn how to validate end-to-end tool invocation by integrating the model with the MCP server and monitoring real-time function execution through structured responses.

## Model Context Protocol (MCP)

As an extension of [KAITO inference with tool calling](ai-toolchain-operator-tool-calling), the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) provides a standardized way to define and expose tools for language models to call.

Tool calling with MCP makes it easier to connect language models to real services and actions without tightly coupling logic into the model itself. Instead of embedding every function or API call into your application code, MCP lets you run a standalone tool server that exposes standardized tools or APIs that any compatible LLM can use. This clean separation means you can update tools independently, share them across models, and manage them like any other microservice.

You can bring-your-own (BYO) internal or connect external MCP servers seamlessly with your KAITO inference workspace on AKS.

## MCP with AI toolchain operator (KAITO) on AKS

You can register an external MCP server in a uniform, schema-driven format and serve it to any compatible inference endpoint, including those [deployed with a KAITO workspace](https://kaito-project.github.io/kaito/docs/tool-calling/#model-context-protocol-mcp). This approach allows for externalizing business logic, decoupling model behavior from tool execution, and reusing tools across agents, models, and environments.

In this guide, you register a pre-defined MCP server, test real calls issued by an LLM running in a KAITO inference workspace, and confirm the entire tool execution path (from model prompt to MCP function invocation) works as intended. You have flexibility to scale or swap tools independent of your model.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - You have the
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster and a[KAITO workspace with tool calling support](ai-toolchain-operator-tool-calling)deployed on your cluster. - An external MCP server available at an accessible URL (e.g.,
`https://mcp.example.com/mcp`

) that returns valid`/list_tools`

and has`stream`

transport.

## Connect to a reference MCP server

In this example, we'll use a reference [Time MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/time#time-mcp-server), which provides time zone conversion capabilities and enables LLMs to get current time information and perform conversions using standardized names.

## Port-forward the KAITO inference service

Confirm that your KAITO workspace is ready and retrieve the inference service endpoint using the

`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check

`/v1/models`

endpoint to confirm that`Phi-4-mini-instruct`

LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

Your

`Phi-4-mini-instruct`

OpenAI-compatible inference API will be available at:`http://localhost:8000/v1/chat/completions`


## Confirm the reference MCP server is valid

This example assumes that the Time MCP server is hosted at `https://mcp.example.com`

.

Confirm the server returns tools using

`curl`

.`curl https://mcp.example.com/mcp/list_tools`

Expected output:

`{ "tools": [ { "name": "get_current_time", "description": "Get the current time in a specific timezone", "arguments": { "timezone": "string" } }, { "name": "convert_time", "description": "Convert time between two timezones", "arguments": { "source_timezone": "string", "time": "string", "target_timezone": "string" } } ] }`


## Connect MCP server to the KAITO workspace using API request

KAITO automatically fetches tool definitions from **tools declared in API requests** or registered dynamically inside the inference runtime (vLLM + MCP tool loader).

In this guide, we create a Python virtual environment to send a tool-calling request to the `Phi-4-mini-instruct`

inference endpoint using the MCP definition and pointing to the server.

Define a new working directory for this test project.

`mkdir kaito-mcp cd kaito-mcp`

Create a Python virtual environment and activate it so that all packages are local to your test project.

`uv venv source .venv/bin/activate`

Use the open-source

[Autogen](https://microsoft.github.io/autogen/stable//index.html)framework to test the tool calling functionality and install its dependencies:`uv pip install "autogen-ext[openai]" "autogen-agentchat" "autogen-ext[mcp]"`

Create a test file named

`test.py`

that:- Connects to the Time MCP server and loads
`get_current_time`

tool. - Connects to your KAITO inference service running at
`localhost:8000`

. - Sends an example query like “What time is it in Europe/Paris?”
- Enables automatic selection and calling of the
`get_current_time`

tool.

`import asyncio from autogen_agentchat.agents import AssistantAgent from autogen_agentchat.ui import Console from autogen_core import CancellationToken from autogen_core.models import ModelFamily, ModelInfo from autogen_ext.models.openai import OpenAIChatCompletionClient from autogen_ext.tools.mcp import (StreamableHttpMcpToolAdapter, StreamableHttpServerParams) from openai import OpenAI async def main() -> None: # Create server params for the Time MCP service server_params = StreamableHttpServerParams( url="https://mcp.example.com/mcp", timeout=30.0, terminate_on_close=True, ) # Load the get_current_time tool from the server adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "get_current_time") # Fetch model name from KAITO's local OpenAI-compatible API model = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy").models.list().data[0].id model_info: ModelInfo = { "vision": False, "function_calling": True, "json_output": True, "family": ModelFamily.UNKNOWN, "structured_output": True, "multiple_system_messages": True, } # Connect to the KAITO inference workspace model_client = OpenAIChatCompletionClient( base_url="http://localhost:8000/v1", api_key="dummy", model=model, model_info=model_info ) # Define the assistant agent agent = AssistantAgent( name="time-assistant", model_client=model_client, tools=[adapter], system_message="You are a helpful assistant that can provide time information." ) # Run a test task that invokes the tool await Console( agent.run_stream( task="What time is it in Europe/Paris?", cancellation_token=CancellationToken() ) ) if __name__ == "__main__": asyncio.run(main())`

- Connects to the Time MCP server and loads
Run the test script in your virtual environment.

`uv run test.py`

In the output of this test, you should expect the following:

- The model correctly generates a tool call using the MCP name and expected arguments.
- Autogen sends the tool call to the MCP server, the MCP server runs the logic and returns a result.
- The
`Phi-4-mini-instruct`

LLM interprets the raw tool output and provides a natural language response.

`---------- TextMessage (user) ---------- What time is it in Europe/Paris? ---------- ToolCallRequestEvent (time-assistant) ---------- [FunctionCall(id='chatcmpl-tool-xxxx', arguments='{"timezone": "Europe/Paris"}', name='get_current_time')] ---------- ToolCallExecutionEvent (time-assistant) ---------- [FunctionExecutionResult(content='{"timezone":"Europe/Paris","datetime":"2025-09-17T17:43:05+02:00","is_dst":true}', name='get_current_time', call_id='chatcmpl-tool-xxxx', is_error=False)] ---------- ToolCallSummaryMessage (time-assistant) ---------- The current time in Europe/Paris is 5:43 PM (CEST).`


## Experiment with more MCP tools

You can test the various tools available to this MCP server, such as `convert_time`

.

In your

`test.py`

file from the previous step, update your`adapter`

definition to the following:`adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "convert_time")`

Update your

`task`

definition to invoke the new tool. For example:`task="Convert 9:30 AM New York time to Tokyo time."`

Save and run the Python script.

`uv run test.py`

Expected output:

`9:30 AM in New York is 10:30 PM in Tokyo.`


## Troubleshooting

The following table outlines common errors when testing KAITO inference with an external MCP server and how to resolve them:

| Error | How to resolve |
|---|---|
`Tool not found` |
Ensure that your tool name matches the one declared in `/mcp/list_tools` . |
`401 Unauthorized` |
If your MCP server requires an Auth token, make sure to update `server_params` to include headers with the Auth token. |
`connection refused` |
Ensure the KAITO inference service is port-forwarded properly (e.g. to `localhost:8000` ). |
`tool call ignored` |
Review the
|

## Next steps

In this article, you learned how to connect a KAITO workspace to an external reference MCP server using Autogen to enable tool calling through the OpenAI-compatible API. You also validated that the LLM could discover, invoke, and integrate results from MCP-compliant tools on AKS. To learn more, see the following resources:

[Deploy and test tool calls](ai-toolchain-operator-tool-calling)with the AI toolchain operator add-on on AKS.- KAITO tool calling and
[MCP official documentation](https://kaito-project.github.io/kaito/docs/tool-calling).


---

<!-- DOCUMENTO FUSIONADO: egress-outboundtype.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/egress-outboundtype -->

# Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

After [31 March 2026](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access), new AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

).

This setting **does not impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It may affect **unsupported scenarios**, such as deploying other resources (e.g., VMs) into the same subnet.

**Clusters using BYO VNets are unaffected** by this change. In supported configurations, no action is required.

You can customize egress for an AKS cluster to fit specific scenarios. By default, AKS creates a Standard Load Balancer to be set up and used for egress. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or extra hops are required for egress.

This article covers the various types of outbound connectivity that are available in AKS clusters.

Note

You can now update the `outboundType`

after cluster creation.

Important

In nonprivate clusters, API server cluster traffic is routed and processed through the clusters outbound type. To prevent API server traffic from being processed as public traffic, consider using a [private cluster](private-clusters), or check out the [API Server VNet Integration](api-server-vnet-integration) feature.

## Limitations

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and`load-balancer-sku`

of`Standard`

.

## Outbound types in AKS

You can configure an AKS cluster using the following outbound types: load balancer, NAT gateway, or user-defined routing. The outbound type impacts only the egress traffic of your cluster. For more information, see [setting up ingress controllers](ingress-basic).

### Outbound type of `loadBalancer`


The load balancer is used for egress through an AKS-assigned public IP. An outbound type of `loadBalancer`

supports Kubernetes services of type `loadBalancer`

, which expect egress out of the load balancer created by the AKS resource provider.

If `loadBalancer`

is set, AKS automatically completes the following configuration:

- A public IP address is created for cluster egress.
- The public IP address is assigned to the load balancer resource.
- Backend pools for the load balancer are set up for agent nodes in the cluster.

For more information, see [using a standard load balancer in AKS](load-balancer-standard).

### Outbound type of `managedNatGateway`

or `userAssignedNatGateway`


If `managedNatGateway`

or `userAssignedNatGateway`

are selected for `outboundType`

, AKS relies on [Azure Networking NAT gateway](/en-us/azure/virtual-network/nat-gateway/manage-nat-gateway) for cluster egress.

- Select
`managedNatGateway`

when using managed virtual networks. AKS provisions a NAT gateway and attach it to the cluster subnet. - Select
`userAssignedNatGateway`

when using bring-your-own virtual networking. This option requires that you have a NAT gateway created before cluster creation.

For more information, see [using NAT gateway with AKS](nat-gateway).

### Outbound type of `userDefinedRouting`


Note

The `userDefinedRouting`

outbound type is an advanced networking scenario and requires proper network configuration.

If `userDefinedRouting`

is set, AKS doesn't automatically configure egress paths. The egress setup is completed by you.

You must deploy the AKS cluster into an existing virtual network with a subnet that is configured. Since you're not using a standard load balancer (SLB) architecture, you must establish explicit egress. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, proxy or to allow NAT to be done by a public IP assigned to the standard load balancer or appliance.

For more information, see [configuring cluster egress via user-defined routing](egress-udr).

### Outbound type of `none`


Important

The `none`

outbound type is only available with [Network Isolated Cluster](concepts-network-isolated) and requires careful planning to ensure the cluster operates as expected without unintended dependencies on external services. For fully isolated clusters, see [isolated cluster considerations](concepts-network-isolated).

If `none`

is set, AKS won't automatically configure egress paths. This option is similar to `userDefinedRouting`

but does **not** require a default route as part of validation.

The `none`

outbound type is supported in both bring-your-own (BYO) virtual network scenarios and managed VNet scenarios. However, you must ensure that the AKS cluster is deployed into a network environment where explicit egress paths are defined if needed. For BYO VNet scenarios, the cluster must be deployed into an existing virtual network with a subnet that is already configured. Since AKS doesn't create a standard load balancer or any egress infrastructure, you must establish explicit egress paths if needed. Egress options can include routing traffic to a firewall, proxy, gateway, or other custom network configurations.

### Outbound type of `block`

(Preview)

Important

The `block`

outbound type is only available with [Network Isolated Cluster](concepts-network-isolated) and requires careful planning to ensure no unintended network dependencies exist. For fully isolated clusters, see [isolated cluster considerations](concepts-network-isolated).

If `block`

is set, AKS configures network rules to **actively block all egress traffic** from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted.

When using `block`

:

- AKS ensures that no public internet traffic can leave the cluster through network security group (NSG) rules. VNet traffic isn't affected.
- You must explicitly allow any required egress traffic through extra network configurations.

The `block`

option provides another level of network isolation but requires careful planning to avoid breaking workloads or dependencies.

## Updating `outboundType`

after cluster creation

Changing the outbound type after cluster creation deploys or removes resources as required to put the cluster into the new egress configuration.

The following tables show the supported migration paths between outbound types for managed and BYO virtual networks.

### Supported Migration Paths for Managed VNet

Each row shows whether the outbound type can be migrated to the types listed across the top. "Supported" means migration is possible, while "Not Supported" or "N/A" means it isn't.

| From|To | `loadBalancer` |
`managedNATGateway` |
`userAssignedNATGateway` |
`userDefinedRouting` |
`none` |
`block` |
|---|---|---|---|---|---|---|
`loadBalancer` |
N/A | Supported | Not Supported | Not Supported | Supported | Supported |
`managedNATGateway` |
Supported | N/A | Not Supported | Not Supported | Supported | Supported |
`userAssignedNATGateway` |
Not Supported | Not Supported | N/A | Not Supported | Not Supported | Not Supported |
`none` |
Supported | Supported | Not Supported | Not Supported | N/A | Supported |
`block` |
Supported | Supported | Not Supported | Not Supported | Supported | N/A |

### Supported Migration Paths for BYO VNet

| From|To | `loadBalancer` |
`managedNATGateway` |
`userAssignedNATGateway` |
`userDefinedRouting` |
`none` |
`block` |
|---|---|---|---|---|---|---|
`loadBalancer` |
N/A | Not Supported | Supported | Supported | Supported | Not Supported |
`managedNATGateway` |
Not Supported | N/A | Not Supported | Not Supported | Not Supported | Not Supported |
`userAssignedNATGateway` |
Supported | Not Supported | N/A | Supported | Supported | Not Supported |
`userDefinedRouting` |
Supported | Not Supported | Supported | N/A | Supported | Not Supported |
`none` |
Supported | Not Supported | Supported | Supported | N/A | Not Supported |

Migration is only supported between `loadBalancer`

, `managedNATGateway`

(if using a managed virtual network), `userAssignedNATGateway`

and `userDefinedRouting`

(if using a custom virtual network).

Warning

Migrating the outbound type to user managed types (`userAssignedNATGateway`

or `userDefinedRouting`

) will change the outbound public IP addresses of the cluster.
if [Authorized IP ranges](api-server-authorized-ip-ranges) is enabled, ensure new outbound IP range is appended to authorized IP range.

Warning

Changing the outbound type on a cluster is disruptive to network connectivity and results in a change of the cluster's egress IP address. If any firewall rules are configured to restrict traffic from the cluster, you need to update them to match the new egress IP address.

### Update cluster to use a new outbound type

Note

You must use a version >= 2.56 of Azure CLI to migrate outbound type. Use `az upgrade`

to update to the latest version of Azure CLI.

- Update the outbound configuration of your cluster using the
command.`az aks update`


### Update cluster from loadbalancer to managedNATGateway

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type managedNATGateway --nat-gateway-managed-outbound-ip-count <number of managed outbound ip>
```


### Update cluster from managedNATGateway to loadbalancer

```
az aks update --resource-group <resourceGroup> --name <clusterName> \
--outbound-type loadBalancer \
<--load-balancer-managed-outbound-ip-count <number of managed outbound ip>| --load-balancer-outbound-ips <outbound ip ids> | --load-balancer-outbound-ip-prefixes <outbound ip prefix ids> >
```


Warning

Don't reuse an IP address that is already in use in prior outbound configurations.

### Update cluster from managedNATGateway to userDefinedRouting

- Add route
`0.0.0.0/0`

default route table. Please see[Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)](egress-udr)

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type userDefinedRouting
```


### Update cluster from loadbalancer to userAssignedNATGateway in BYO vnet scenario

- Associate nat gateway with subnet where the workload is associated with. Refer to
[Create a managed or user-assigned NAT gateway](nat-gateway)

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type userAssignedNATGateway
```


---

<!-- DOCUMENTO FUSIONADO: _azure-netapp-files-smb_concepts-storage.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files-smb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-smb -->

# Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), SMB, and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning SMB volumes statically or dynamically.
- For information about provisioning NFS volumes statically or dynamically, see
[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use SMB volumes

This section describes how to create an SMB volume on Azure NetApp Files and expose the volume statically to Kubernetes for a containerized application to consume.

### Create an SMB Volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*, and*virtnetid*with an appropriate value for your environment. The filepath must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are standard, premium, and ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command.`az netappfiles volume create`

`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types CIFS`


### Create a secret with the domain credentials

Create a secret on your AKS cluster to access the Active Directory (AD) server using the

command. This secret will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command to create the secret, replacing`kubectl create secret`

`USERNAME`

with your username,`PASSWORD`

with your password, and`DOMAIN_NAME`

with your domain name for your AD.`kubectl create secret generic smbcreds --from-literal=username=USERNAME --from-literal=password="PASSWORD" --from-literal=domain='DOMAIN_NAME'`

Check the secret has been created.

`kubectl get secret NAME TYPE DATA AGE smbcreds Opaque 2 20h`


### Install an SMB CSI driver

You must install a Container Storage Interface (CSI) driver to create a Kubernetes SMB `PersistentVolume`

.

Install the SMB CSI driver on your cluster using helm. Be sure to set the

`windows.enabled`

option to`true`

:`helm repo add csi-driver-smb https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/charts helm install csi-driver-smb csi-driver-smb/csi-driver-smb --namespace kube-system --version v1.13.0 --set windows.enabled=true`

For other methods of installing the SMB CSI Driver, see

[Install SMB CSI driver master version on a Kubernetes cluster](https://github.com/kubernetes-csi/csi-driver-smb/blob/master/docs/install-csi-driver-master.md).Verify that the

`csi-smb`

controller pod is running and each worker node has a pod running using thecommand:`kubectl get pods`

`kubectl get pods -n kube-system | grep csi-smb csi-smb-controller-68df7b4758-xf2m9 3/3 Running 0 3m46s csi-smb-node-s6clj 3/3 Running 0 3m47s csi-smb-node-win-tfxvk 3/3 Running 0 3m47s`


### Create the persistent volume

List the details of your volume using

. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myvolname", ... "mountTargets": [ { ... " "smbServerFqdn": "ANF-1be3.contoso.com", ... } ], ... }`

Create a file named

`pv-smb.yaml`

and copy in the following YAML. If necessary, replace`myvolname`

with the`creationToken`

and replace`ANF-1be3.contoso.com\myvolname`

with the value of`smbServerFqdn`

from the previous step. Be sure to include your AD credentials secret along with the namespace where the secret is located that you created in a prior step.`apiVersion: v1 kind: PersistentVolume metadata: name: anf-pv-smb spec: storageClassName: "" capacity: storage: 100Gi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain mountOptions: - dir_mode=0777 - file_mode=0777 - vers=3.0 csi: driver: smb.csi.k8s.io readOnly: false volumeHandle: myvolname # make sure it's a unique name in the cluster volumeAttributes: source: \\ANF-1be3.contoso.com\myvolname nodeStageSecretRef: name: smbcreds namespace: default`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-smb.yaml`

Verify the status of the persistent volume is

*Available*using thecommand:`kubectl describe`

`kubectl describe pv pv-smb`


### Create a persistent volume claim

Create a file name

`pvc-smb.yaml`

and copy in the following YAML.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany volumeName: anf-pv-smb storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-smb.yaml`

Verify the status of the persistent volume claim is

*Bound*by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pvc pvc-smb`


### Mount with a pod

Create a file named

`iis-smb.yaml`

and copy in the following YAML. This file will be used to create an Internet Information Services pod to mount the volume to path`/inetpub/wwwroot`

.`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f iis-smb.yaml`

Verify the pod is

*Running*and`/inetpub/wwwroot`

is mounted from SMB by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 09:34:41 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.248 IPs: IP: 10.225.5.248 Containers: web: Container ID: containerd://39a1659b6a2b6db298df630237b2b7d959d1b1722edc81ce9b1bc7f06237850c Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 09:34:55 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mbnv8 (ro) ...`

Verify your volume has been mounted on the pod by using the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command to connect to the pod, and then use`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/04/2023 08:15 PM <DIR> . 05/04/2023 08:15 PM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,838,336 bytes free`


## Dynamically configure for applications that use SMB volumes

This section covers how to use Trident to dynamically create an SMB volume on Azure NetApp Files and automatically mount it to a containerized windows application.

### Install Trident

To dynamically provision SMB volumes, you need to install Trident version 22.10 or later. Dynamically provisioning SMB volumes requires windows worker nodes.

Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html). If you have windows worker nodes in the cluster, ensure to enable windows with any installation method.

To install Trident using Helm for a cluster with windows worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident –-set windows=true`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 14:23:05 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: true Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 74s trident-operator.netapp.io Installing Trident Normal Installed 46s trident-operator.netapp.io Trident installed`


### Create a backend

A backend must be created to instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes. For more information about backends, see [Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).

Create a file named

`backend-secret-smb.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf-smb.yaml`

and copy in the following YAML. Change the`ClientID`

,`clientSecret`

,`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. The`tenantID`

,`clientID`

, and`clientSecret`

can be found from an application registration in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The Azure location must contain at least one delegated subnet. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf-smb spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret nasType: smb`

Create the secret and backend using the

command.`kubectl apply`

Create the secret:

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Create the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Verify the backend was created by running the following command:

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-9shfq backend-tbc-anf-smb 09cc2d43-8197-475f-8356-da7707bae203`


### Create a secret with the domain credentials for SMB

Create a secret on your AKS cluster to access the AD server using the

command. This information will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command, replacing`kubectl create secret`

`DOMAIN_NAME\USERNAME`

with your domain name and username and`PASSWORD`

with your password.`kubectl create secret generic smbcreds --from-literal=username=DOMAIN_NAME\USERNAME –from-literal=password="PASSWORD"`

Verify that the secret has been created.

`kubectl get secret`

The output resembles the following example:

`NAME TYPE DATA AGE smbcreds Opaque 2 2h`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass-smb.yaml`

and copy in the following YAML.`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: anf-sc-smb provisioner: csi.trident.netapp.io allowVolumeExpansion: true parameters: backendType: "azure-netapp-files" trident.netapp.io/nasType: "smb" csi.storage.k8s.io/node-stage-secret-name: "smbcreds" csi.storage.k8s.io/node-stage-secret-namespace: "default"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass-smb.yaml`

The output of the command resembles the following example:

`storageclass/anf-sc-smb created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc anf-sc-smb NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE anf-sc-smb csi.trident.netapp.io Delete Immediate true 13s`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files SMB share and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc-smb.yaml`

and copy the following YAML. In this example, a 100-GiB volume is created with`ReadWriteMany`

access and uses the storage class created in[Create a storage class](#create-a-storage-class).`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany resources: requests: storage: 100Gi storageClassName: anf-sc-smb`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc-smb.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc-smb created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc-smb Bound pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX anf-sc-smb 5m38s`

To view the persistent volume created by Trident, run the following

command:`kubectl get`

`kubectl get pv NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX Delete Bound default/anf-pvc-smb anf-sc-smb 5m52s`


### Use the persistent volume

After the PVC is created, a pod can be spun up to access the Azure NetApp Files volume. The following manifest can be used to define an Internet Information Services (IIS) pod that mounts the Azure NetApp Files SMB share created in the previous step. In this example, the volume is mounted at `/inetpub/wwwroot`

.

Create a file named

`anf-iis-pod.yaml`

and copy in the following YAML:`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the deployment using the

command:`kubectl apply`

`kubectl apply -f anf-iis-deploy-pod.yaml`

The output of the command resembles the following example:

`pod/iis-pod created`

Verify that the pod is running and is mounted via SMB to

`/inetpub/wwwroot`

by using thecommand:`kubectl describe`

`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 15:16:36 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.252 IPs: IP: 10.225.5.252 Containers: web: Container ID: containerd://1e4959f2b49e7ad842b0ec774488a6142ac9152ca380c7ba4d814ae739d5ed3e Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 15:16:44 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zznzs (ro)`

Verify that your volume has been mounted on the pod by using

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)to connect to the pod. And then use the`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/05/2023 01:38 AM <DIR> . 05/05/2023 01:38 AM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,862,912 bytes free C:\inetpub\wwwroot>exit`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:


---

<!-- DOCUMENTO FUSIONADO: concepts-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-storage -->

# Storage options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Applications running in Azure Kubernetes Service (AKS) might need to store and retrieve data. While some application workloads can use local, fast storage on unneeded, emptied nodes, others require storage that persists on more regular data volumes within the Azure platform.

Multiple pods might need to:

- Share the same data volumes.
- Reattach data volumes if the pod is rescheduled on a different node.

You also might need to collect and store sensitive data or application configuration information into pods.

This article introduces the core concepts that provide storage to your applications in AKS:

## Default OS disk sizing

### Ephemeral OS disks

If you select a VM SKU that supports Ephemeral OS disks but don't specify an OS disk size, AKS by default provisions an Ephemeral OS disk with a size that scales according to the total temp storage of the VM SKU so long as the temp is *at least 128GiB*. For example, the `Standard_D8ds_v5`

SKU with a temp disk size of 300GiB will receive a 300GiB Ephemeral OS disk by default if the disk parameters are unspecified.

If you want to use the temp storage of the VM SKU, you need to specify the OS disk size during deployment, otherwise it's consumed by default.

Important

Default Ephemeral OS disk sizing is only used on new clusters or node pools where Ephemeral OS disks are supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. This default Ephemeral sizing affects clusters or node pools created in March 2025 or later.

### Managed OS disks

When you create a new cluster or add a new node pool to an existing cluster, the number for vCPUs by default determines the OS disk size. The number of vCPUs is based on the VM SKU. The following table lists the default OS disk size for each VM SKU:

| VM SKU Cores (vCPUs) | Default OS Disk Tier | Provisioned IOPS | Provisioned Throughput (Mbps) |
|---|---|---|---|
| 1 - 7 | P10/128G | 500 | 100 |
| 8 - 15 | P15/256G | 1100 | 125 |
| 16 - 63 | P20/512G | 2300 | 150 |
| 64+ | P30/1024G | 5000 | 200 |

Important

Default Managed OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks aren't supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. We recommend a minimum disk size of 512G if ephemeral OS disk cannot be used. This default Managed sizing affects clusters or node pools created in July 2022 or later.

## Ephemeral OS disk

By default, Azure automatically replicates the operating system disk for a virtual machine to Azure Storage to avoid data loss when the VM is relocated to another host. However, since containers aren't designed to have local state persisted, this behavior offers limited value while providing some drawbacks. These drawbacks include, but aren't limited to, slower node provisioning and higher read/write latency.

By contrast, Ephemeral OS disks are stored only on the host machine, just like a temporary disk. With this configuration, you get lower read/write latency with faster node scaling and cluster upgrades. Therefore, we strongly **recommend using Ephemeral OS disks whenever possible**.

Note

When you don't explicitly request [Azure managed disks](/en-us/azure/virtual-machines/managed-disks-overview) for the OS, AKS defaults to ephemeral OS if possible for a given node pool configuration.

Size requirements and recommendations for ephemeral OS disks are available in the [Azure VM documentation](/en-us/azure/virtual-machines/ephemeral-os-disks). The following are some general sizing considerations:

If you chose to use the AKS default VM size

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with the default OS disk size of 100 GiB, the default VM size supports ephemeral OS, but only has 86 GiB of cache size. This configuration would default to managed disks if you don't explicitly specify it. If you do request an ephemeral OS, you receive a validation error.If you request the same

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with a 60-GiB OS disk, this configuration would default to ephemeral OS. The requested size of 60 GiB is smaller than the maximum cache size of 86 GiB.If you select the

[Standard_D8s_v3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)SKU with 100-GB OS disk, this VM size supports ephemeral OS and has 200 GiB of cache space. If you don't specify the OS disk type, the node pool would receive ephemeral OS by default.

The latest generation of VM series doesn't have a dedicated cache, but only temporary storage. For example, if you selected the [Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series) VM size with the default OS disk size of 100 GiB, it supports ephemeral OS disks, but only has 75 GB of temporary storage. This configuration would default to managed OS disks if you don't explicitly specify it. If you do request an ephemeral OS disk, you receive a validation error.

If you request the same

[Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)VM size with a 60-GiB OS disk, this configuration defaults to ephemeral OS disks. The requested size of 60 GiB is smaller than the maximum temporary storage of 75 GiB.If you select

[Standard_E4bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)SKU with 100-GiB OS disk, this VM size supports ephemeral OS and has 150 GiB of temporary storage. If you don't specify the OS disk type, by default Azure provisions an ephemeral OS disk to the node pool.

### Customer-managed keys

You can manage encryption for your ephemeral OS disk with your own keys on an AKS cluster. For more information, see [Use Customer Managed key with Azure disk on AKS](azure-disk-customer-managed-keys).

## Ephemeral NVMe data disks

Ephemeral NVMe data disks provide high-performance, low-latency storage directly attached to the physical host of your Azure VM. These disks are ideal for workloads that require fast, temporary storage for intermediate data processing, such as caching, scratch space, or high-throughput analytics.

Ephemeral NVMe data disks were initially available only on Azure VM L-series, E-series, and GPU VMs. With the introduction of Azure VM v6 and v7 generations, support for ephemeral NVMe data disks has expanded to a much wider range of VM sizes, including D-series, F-series, H-series, and more. NVMe disks deliver significantly higher IOPS and throughput compared to traditional HDD or SSD options. However, data stored on these disks is temporary and will be lost if the VM is deallocated or redeployed.

To simplify management and provisioning of ephemeral NVMe data disks in AKS, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction). Azure Container Storage can automatically detect and orchestrate NVMe data disks, allowing you to create and manage persistent volumes for your Kubernetes workloads with minimal configuration. This approach is recommended for scenarios where high-performance, temporary storage is required, such as:

- High-speed caching layers, such as datasets and checkpoints for AI training, or model files used for AI inference
- High-performance, self-hosted databases that include built-in replication and backup features
- Data-intensive analytics and processing pipelines that require fast, temporary storage
- Temporary scratch space for batch jobs

Important

Ephemeral NVMe data disks are not suitable for storing critical or persistent data. Ensure your application can tolerate data loss and that important data is stored on persistent volumes backed by Azure Disk, Azure Files, or other durable storage options.

For more information on using Azure Container Storage with ephemeral NVMe data disks, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).

## Volumes

Kubernetes typically treats individual pods as ephemeral, disposable resources. Applications have different approaches available to them for using and persisting data. A *volume* represents a way to store, retrieve, and persist data across pods and through the application lifecycle.

Traditional volumes are created as Kubernetes resources backed by Azure Storage. You can manually create data volumes to be assigned to pods directly or have Kubernetes automatically create them. Data volumes can use: [Azure Disk](/en-us/azure/virtual-machines/disks-types), [Azure Files](/en-us/azure/storage/files/storage-files-planning), [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-service-levels), or [Azure Blobs](/en-us/azure/storage/common/storage-account-overview).

Note

Depending on the VM SKU you're using, the Azure Disk CSI driver might have a per-node volume limit. For some high performance VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

To help determine best fit for your workload between Azure Files and Azure NetApp Files, review the information provided in the article [Azure Files and Azure NetApp Files comparison](/en-us/azure/storage/files/storage-files-netapp-comparison).

### Azure Disk

Use [Azure Disk](azure-disk-csi) to create a Kubernetes *DataDisk* resource. Disks types include:

- Premium SSDs (recommended for most workloads)
- Ultra disks
- Standard SSDs
- Standard HDDs

Tip

For most production and development workloads, use Premium SSDs.

Because an Azure Disk is mounted as *ReadWriteOnce*, it's only available to a single node. For storage volumes accessible by pods on multiple nodes simultaneously, use Azure Files.

### Azure Files

Use [Azure Files](azure-files-csi) to mount a Server Message Block (SMB) version 3.1.1 share or Network File System (NFS) version 4.1 share. Azure Files let you share data across multiple nodes and pods and can use:

- Azure Premium storage backed by high-performance SSDs
- Azure Standard storage backed by regular HDDs

### Azure NetApp Files

- Ultra Storage
- Premium Storage
- Standard Storage

### Azure Blob Storage

Use [Azure Blob Storage](azure-blob-csi) to create a blob storage container and mount it using the NFS v3.0 protocol or BlobFuse.

- Block blobs

### Volume types

Kubernetes volumes represent more than just a traditional disk for storing and retrieving information. Kubernetes volumes can also be used as a way to inject data into a pod for use by its containers.

Common volume types in Kubernetes include:

#### emptyDir

Commonly used as temporary space for a pod. All containers within a pod can access the data on the volume. Data written to this volume type persists only for the lifespan of the pod. Once you delete the pod, the volume is deleted. This volume typically uses the underlying local node disk storage, though it can also exist only in the node's memory.

#### secret

You can use *secret* volumes to inject sensitive data into pods, such as passwords.

- Create a secret using the Kubernetes API.
- Define your pod or deployment and request a specific secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a secret, the secret is deleted from the node's tmpfs.
- Secrets are stored within a given namespace and are only accessed by pods within the same namespace.


#### configMap

You can use *configMap* to inject key-value pair properties into pods, such as application configuration information. Define application configuration information as a Kubernetes resource, easily updated and applied to new instances of pods as they're deployed.

Like using a secret:

- Create a ConfigMap using the Kubernetes API.
- Request the ConfigMap when you define a pod or deployment.
- ConfigMaps are stored within a given namespace and are only accessed by pods within the same namespace.


## Persistent volumes

Volumes defined and created as part of the pod lifecycle only exist until you delete the pod. Pods often expect their storage to remain if a pod is rescheduled on a different host during a maintenance event, especially in StatefulSets. A *persistent volume* (PV) is a storage resource created and managed by the Kubernetes API that can exist beyond the lifetime of an individual pod.

You can use the following Azure Storage services to provide the persistent volume:

As noted in the [Volumes](#volumes) section, the choice of Azure Disks or Azure Files is often determined by the need for concurrent access to the data or the performance tier.

A cluster administrator can *statically* create a persistent volume, or a volume can be created *dynamically* by the Kubernetes API server. If a pod is scheduled and requests storage that is currently unavailable, Kubernetes can create the underlying Azure Disk or File storage and attach it to the pod. Dynamic provisioning uses a *storage class* to identify what type of resource needs to be created.

Important

Persistent volumes can't be shared by Windows and Linux pods due to differences in file system support between the two operating systems.

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Storage classes

To specify different tiers of storage, such as premium or standard, you can create a *storage class*.

A storage class also defines a *reclaim policy*. When you delete the persistent volume, the reclaim policy controls the behavior of the underlying Azure Storage resource. The underlying resource can either be deleted or kept for use with a future pod.

For clusters using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), you'll see an additional storage class called `acstor-<storage-pool-name>`

. An internal storage class is also created.

For clusters using [Container Storage Interface (CSI) drivers](csi-storage-drivers), the following extra storage classes are created:

| Storage class | Description |
|---|---|
`managed-csi` |
Uses Azure Standard SSD locally redundant storage (LRS) to create a managed disk. The reclaim policy ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. The storage class also configures the persistent volumes to be expandable. You can edit the persistent volume claim to specify the new size. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Standard SSD zone-redundant storage (ZRS) to create managed disks. |
`managed-csi-premium` |
Uses Azure Premium locally redundant storage (LRS) to create a managed disk. The reclaim policy again ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. Similarly, this storage class allows for persistent volumes to be expanded. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Premium zone-redundant storage (ZRS) to create managed disks. |
`azurefile-csi` |
Uses Azure Standard storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azurefile-csi-premium` |
Uses Azure Premium storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azureblob-nfs-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using the NFS v3 protocol. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |
`azureblob-fuse-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using BlobFuse. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |

Unless you specify a storage class for a persistent volume, the default storage class is used. Ensure volumes use the appropriate storage you need when requesting persistent volumes.

Important

Starting with Kubernetes version 1.21, AKS uses CSI drivers by default, and CSI migration is enabled. While existing in-tree persistent volumes continue to function, starting with version 1.26, AKS will no longer support volumes created using in-tree driver and storage provisioned for files and disk.

The `default`

class will be the same as `managed-csi`

.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes. ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the `skuname`

parameter set to LRS. You can then use the new storage class in your Persistent Volume Claim (PVC).

You can create a storage class for other needs using `kubectl`

. The following example uses premium managed disks and specifies that the underlying Azure Disk should be *retained* when you delete the pod:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: managed-premium-retain
provisioner: disk.csi.azure.com
parameters:
skuName: Premium_ZRS
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


Note

AKS reconciles the default storage classes and will overwrite any changes you make to those storage classes.

For more information about storage classes, see [StorageClass in Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

## Persistent volume claims

A persistent volume claim (PVC) requests storage of a particular storage class, access mode, and size. The Kubernetes API server can dynamically provision the underlying Azure Storage resource if no existing resource can fulfill the claim based on the defined storage class.

The pod definition includes the volume mount once the volume has been connected to the pod.

Once an available storage resource has been assigned to the pod requesting storage, the persistent volume is *bound* to a persistent volume claim. Persistent volumes are mapped to claims in a 1:1 mapping.

The following example YAML manifest shows a persistent volume claim that uses the *managed-premium* storage class and requests an Azure Disk that is *5Gi* in size:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-premium-retain
resources:
requests:
storage: 5Gi
```


When you create a pod definition, you also specify:

- The persistent volume claim to request the desired storage.
- The
*volume mount*for your applications to read and write data.

The following example YAML manifest shows how the previous persistent volume claim can be used to mount a volume at */mnt/azure*:

```
kind: Pod
apiVersion: v1
metadata:
name: nginx
spec:
containers:
- name: myfrontend
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: azure-managed-disk
```


For mounting a volume in a Windows container, specify the drive letter and path. For example:

```
...
volumeMounts:
- mountPath: "d:"
name: volume
- mountPath: "c:\k"
name: k-dir
...
```


## Next steps

For associated best practices, see [Best practices for storage and backups in AKS](operator-best-practices-storage) and [AKS storage considerations](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage).

For more information on Azure Container Storage, see the following articles:

For more information on using CSI drivers, see the following articles:

[Container Storage Interface (CSI) drivers for Azure Disk, Azure Files, and Azure Blob storage on Azure Kubernetes Service](csi-storage-drivers)[Use Azure Disk CSI driver in Azure Kubernetes Service](azure-disk-csi)[Use Azure Files CSI driver in Azure Kubernetes Service](azure-files-csi)[Use Azure Blob storage CSI driver in Azure Kubernetes Service](azure-blob-csi)[Configure Azure NetApp Files with Azure Kubernetes Service](azure-netapp-files)

For more information on core Kubernetes and AKS concepts, see the following articles:
