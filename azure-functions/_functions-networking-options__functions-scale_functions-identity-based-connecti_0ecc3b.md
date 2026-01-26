---
merged_at: 2026-01-26T23:29:57.711017
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-options -->

# Azure Functions networking options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the networking features available across the hosting options for Azure Functions. The following networking options can be categorized as inbound and outbound networking features. Inbound features allow you to restrict access to your app, whereas outbound features allow you to connect your app to resources secured by a virtual network and control how outbound traffic is routed.

The [hosting models](functions-scale) have different levels of network isolation available. Choosing the correct one helps you meet your network isolation requirements.

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Quickstart resources

Use the following resources to quickly get started with Azure Functions networking scenarios. These resources are referenced throughout the article.

- ARM templates, Bicep files, and Terraform templates:
- ARM templates only:
- Tutorials:

## Inbound networking features

The following features let you filter inbound requests to your function app.

### Inbound access restrictions

You can use access restrictions to define a priority-ordered list of IP addresses that are allowed or denied access to your app. The list can include IPv4 and IPv6 addresses, or specific virtual network subnets using [service endpoints](#use-service-endpoints). When there are one or more entries, an implicit "deny all" exists at the end of the list. IP restrictions work with all function-hosting options.

Access restrictions are available in the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium](functions-premium-plan), [Consumption](consumption-plan), and [App Service](dedicated-plan).

Note

With network restrictions in place, you can deploy only from within your virtual network, or when you put the IP address of the machine you're using to access the Azure portal on the **Safe Recipients** list. However, you can still manage the function using the portal.

To learn more, see [Azure App Service static access restrictions](../app-service/app-service-ip-restrictions).

### Private endpoints

[Azure Private Endpoint](../private-link/private-endpoint-overview) is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network.

You can use Private Endpoint for your functions hosted in the [Flex Consumption](flex-consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) plans.

If you want to make calls to Private Endpoints, then you must make sure that your DNS lookups resolve to the private endpoint. You can enforce this behavior in one of the following ways:

- Integrate with Azure DNS private zones. When your virtual network doesn't have a custom DNS server, this is done automatically.
- Manage the private endpoint in the DNS server used by your app. To manage a private endpoint, you must know the endpoint address and use an A record to reference the endpoint you're trying to reach.
- Configure your own DNS server to forward to
[Azure DNS private zones](../dns/private-dns-privatednszone).

To learn more, see [using Private Endpoints for Web Apps](../app-service/networking/private-endpoint).

To call other services that have a private endpoint connection, such as storage or service bus, be sure to configure your app to make [outbound calls to private endpoints](#private-endpoints). For more details on using private endpoints with the storage account for your function app, visit [restrict your storage account to a virtual network](#restrict-your-storage-account-to-a-virtual-network).

### Service endpoints

Using service endpoints, you can restrict many Azure services to selected virtual network subnets to provide a higher level of security. Regional virtual network integration enables your function app to reach Azure services that are secured with service endpoints. This configuration is supported on all [plans](functions-scale#networking-features) that support virtual network integration. Follow these steps to access a secured service endpoint:

- Configure regional virtual network integration with your function app to connect to a specific subnet.
- Go to the destination service and configure service endpoints against the integration subnet.

To learn more, see [Virtual network service endpoints](../virtual-network/virtual-network-service-endpoints-overview).

#### Use Service Endpoints

To restrict access to a specific subnet, create a restriction rule with a **Virtual Network** type. You can then select the subscription, virtual network, and subnet that you want to allow or deny access to.

If service endpoints aren't already enabled with `Microsoft.Web`

for the subnet that you selected, they're automatically enabled unless you select the **Ignore missing Microsoft.Web service endpoints** check box. The scenario where you might want to enable service endpoints on the app but not the subnet depends mainly on whether you have the permissions to enable them on the subnet.

If you need someone else to enable service endpoints on the subnet, select the **Ignore missing Microsoft.Web service endpoints** check box. Your app is configured for service endpoints, which you enable later on the subnet.

You can't use service endpoints to restrict access to apps that run in an App Service Environment. When your app is in an App Service Environment, you can control access to it by applying IP access rules.

To learn how to set up service endpoints, see [Establish Azure Functions private site access](functions-create-private-site-access).

## Outbound networking features

You can use the features in this section to manage outbound connections made by your app.

### Virtual network integration

This section details the features that Functions supports to control data outbound from your app.

Virtual network integration gives your function app access to resources in your virtual network. Once integrated, your app routes outbound traffic through the virtual network. This allows your app to access private endpoints or resources with rules allowing traffic from only select subnets. When the destination is an IP address outside of the virtual network, the source IP will still be sent from the one of the addresses listed in your app's properties, unless you've configured a NAT Gateway.

Azure Functions supports two kinds of virtual network integration:

[Regional virtual network integration](#regional-virtual-network-integration)for apps running on the[Flex Consumption](flex-consumption-plan),[Elastic Premium](functions-premium-plan),[Dedicated (App Service)](dedicated-plan), and[Container Apps](functions-container-apps-hosting)hosting plans (recommended)[Gateway-required virtual network integration](../app-service/configure-gateway-required-vnet-integration)for apps running on the[Dedicated (App Service)](dedicated-plan)hosting plan

To learn how to set up virtual network integration, see [Enable virtual network integration](#enable-virtual-network-integration).

### Regional virtual network integration

Using regional virtual network integration enables your app to access:

- Resources in the same virtual network as your app.
- Resources in virtual networks peered to the virtual network your app is integrated with.
- Service endpoint secured services.
- Resources across Azure ExpressRoute connections.
- Resources across peered connections, which include Azure ExpressRoute connections.
- Private endpoints

When you use regional virtual network integration, you can use the following Azure networking features:

: You can block outbound traffic with an NSG that's placed on your integration subnet. The inbound rules don't apply because you can't use virtual network integration to provide inbound access to your app.[Network security groups (NSGs)](#network-security-groups): You can place a route table on the integration subnet to send outbound traffic where you want.[Route tables (UDRs)](#routes)

Note

When you route all of your outbound traffic into your virtual network, it's subject to the NSGs and UDRs that are applied to your integration subnet. When virtual network integrated, your function app's outbound traffic to public IP addresses is still sent from the addresses that are listed in your app properties, unless you provide routes that direct the traffic elsewhere.

Regional virtual network integration isn't able to use port 25.

Considerations for the [Flex Consumption](flex-consumption-plan) plan:

- The app and the virtual network must be in the same region.
- Ensure that the
`Microsoft.App`

Azure resource provider is enabled for your subscription by[following these instructions](../azure-resource-manager/management/resource-providers-and-types#register-resource-provider). This is needed for subnet delegation. The Azure portal and Azure CLI enforce this registration when you create a Flex Consumption app, since virtual network integration can be enabled at any point after your app is created. - The subnet delegation required when running in a Flex Consumption plan is
`Microsoft.App/environments`

. This differs from the Elastic Premium and Dedicated (App Service) plans, which have a different delegation requirement. - You can plan for 40 IP addresses to be used at the most for one function app, even if the app scales beyond 40. For example, if you have 15 Flex Consumption function apps that are integrated in the same subnet, you must plan for 15x40 = 600 IP addresses used at the most. This limit is subject to change, and isn't enforced.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to any other hosting plan or service). While you can share the same subnet with multiple Flex Consumption apps, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- The Flex Consumption plan currently doesn't support subnets with names that contain underscore (
`_`

) characters.

Considerations for the [Elastic Premium](functions-premium-plan), [Dedicated (App Service)](dedicated-plan), and [Container Apps](functions-container-apps-hosting) plans:

- The feature is available for Elastic Premium and App Service Premium V2 and Premium V3. It's also available in Standard but only from newer App Service deployments. If you are on an older deployment, you can only use the feature from a Premium V2 App Service plan. If you want to make sure you can use the feature in a Standard App Service plan, create your app in a Premium V3 App Service plan. Those plans are only supported on our newest deployments. You can scale down if you desire after that.
- The feature can't be used by Isolated plan apps that are in an App Service Environment.
- The app and the virtual network must be in the same region.
- The feature requires an unused subnet that's a /28 or larger in an Azure Resource Manager virtual network.
- The integration subnet can be used by only one App Service plan.
- You can have up to two regional virtual network integrations per App Service plan. Multiple apps in the same App Service plan can use the same integration subnet.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to the Flex Consumption plan or any other service). While you can share the same subnet with multiple apps in the same App Service plan, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't delete a virtual network with an integrated app. Remove the integration before you delete the virtual network.
- You can't change the subscription of an app or a plan while there's an app that's using regional virtual network integration.

### Enable virtual network integration

In your function app in the

[Azure portal](https://portal.azure.com), select**Networking**, then under**VNet Integration**select**Click here to configure**.Select

**Add VNet**.The drop-down list contains all of the Azure Resource Manager virtual networks in your subscription in the same region. Select the virtual network you want to integrate with.

The Flex Consumption and Elastic Premium hosting plans only support regional virtual network integration. If the virtual network is in the same region, either create a new subnet or select an empty, pre-existing subnet.

To select a virtual network in another region, you must have a virtual network gateway provisioned with point to site enabled. Virtual network integration across regions is only supported for Dedicated plans, but global peerings work with regional virtual network integration.


During the integration, your app is restarted. When integration is finished, you see details on the virtual network you're integrated with. By default, Route All is enabled, and all traffic is routed into your virtual network.

If you prefer to only have your private traffic ([RFC1918](https://datatracker.ietf.org/doc/html/rfc1918#section-3) traffic) routed, follow the steps in this [App Service article](../app-service/overview-vnet-integration#application-routing).

### Subnets

Virtual network integration depends on a dedicated subnet. When you provision a subnet, Azure reserves the first five IP addresses for internal use. The way remaining IP addresses are consumed depends on your hosting plan. Since subnet size can't be changed after assignment, use a subnet that's large enough to accommodate whatever scale your app might reach.

#### Elastic Premium and Dedicated Plans

In Elastic Premium and Dedicated (App Service) plans, each running instance of your function app consumes one IP address from the subnet. When you scale up or down, the required address space may temporarily double to accommodate the transition. If multiple apps share the same subnet, the total IP address usage is the sum of all instances across those apps, plus the temporary doubling during scaling events.

**IP Consumption Scenarios**

| Scenario | IP Address Consumption |
|---|---|
| 1 app, 1 instance | 1 IP address |
| 1 app, 5 instances | 5 IP addresses |
| 1 app, scaling from 5 to 10 instances | Up to 20 IP addresses (temporary, during scale operation) |
| 3 apps, 5 instances each | 15 IP addresses |

**CIDR Range Recommendations**

| CIDR block size | Max available addresses | Max horizontal scale (instances)1 |
|---|---|---|
| /28 | 11 | 5 |
| /27 | 27 | 13 |
| /26 | 59 | 29 |
| /25 | 123 | 612 |
| /24 | 251 | 1253 |

1Assumes that you need to scale up or down in either size or SKU at some point.

2 Although the number of IP addresses supports 61 instances, individual apps on the Dedicated plan have a [30 instance maximum](functions-scale#scale).

2 Although the number of IP addresses supports 125 instances, individual apps on the Elastic Premium plan have a [100 instance maximum](functions-scale#scale).

**Additional Considerations**

For function apps on the Elastic Premium or Dedicated plans:

- To avoid any issues with subnet capacity for Functions Elastic Premium plans, you should use a /24 with 256 addresses for Windows and a /26 with 64 addresses for Linux. When creating subnets in Azure portal as part of integrating with the virtual network, a minimum size of /24 and /26 is required for Windows and Linux respectively.
- Each App Service plan can support up to two subnets that can be used for VNet integration. Multiple apps from a single App Service plan can join the same subnet, but apps from a different plan can't use that same subnet.

#### Flex Consumption Plan

In the Flex Consumption plan, outbound network traffic from function app instances are routed through shared gateways that are dedicated to the subnet. Each shared gateway consumes 1 IP address from the subnet. Regardless of how many apps are integrated with a single subnet, at most 27 shared gateways (27 IP addresses) will be used to support all instances. When selecting a subnet size, what matters is the total number of instances across all apps integrated with the subnet. When a subnet is used for too many instances or for apps performing I/O intensive workloads, network capacity issues may occur such as increased average latency and timeouts. The scale-out of apps will not be affected.

A /27 subnet size (27 usable IP addresses) is recommended to support a single function app, which can scale-out to a maximum of 1,000 instances.

If you expect your single function app to scale beyond 1,000 instances or expect the total instance count of multiple function apps to exceed 1,000 instances, then use a /26 subnet and contact the product group to request an increase to your maximum instance count.

Important

Integrating Flex Consumption function apps with a subnet size less than /27 or integrating multiple apps with a /27 size subnet reduces the available outbound network capacity for them. If you plan to do so, load test your apps with production-scale workloads to ensure network capacity constraints are not observed.

**IP Consumption Scenarios**

| Scenario | Maximum IP Address Consumption |
|---|---|
| 1 app | Up to 27 IP addresses (/27 subnet size) |
| 2 apps | Up to 27 IP addresses (/27 subnet size) |
| 10 apps | Up to 27 IP addresses (/27 subnet size) |

### Network security groups

You can use [network security groups](../virtual-network/network-security-groups-overview) to control traffic between resources in your virtual network. For example, you can create a security rule that blocks your app's outbound traffic from reaching a resource in your virtual network or from leaving the network. These security rules apply to apps that have configured virtual network integration. To block traffic to public addresses, you must have virtual network integration and Route All enabled. The inbound rules in an NSG don't apply to your app because virtual network integration affects only outbound traffic from your app.

To control inbound traffic to your app, use the Access Restrictions feature. An NSG that's applied to your integration subnet is in effect regardless of any routes applied to your integration subnet. If your function app is virtual network integrated with [Route All](../app-service/configure-vnet-integration-routing#configure-application-routing) enabled, and you don't have any routes that affect public address traffic on your integration subnet, all of your outbound traffic is still subject to NSGs assigned to your integration subnet. When Route All isn't enabled, NSGs are only applied to RFC1918 traffic.

### Routes

You can use route tables to route outbound traffic from your app to wherever you want. By default, route tables only affect your RFC1918 destination traffic. When [Route All](../app-service/overview-vnet-integration#application-routing) is enabled, all of your outbound calls are affected. When Route All is disabled, only private traffic (RFC1918) is affected by your route tables. Routes that are set on your integration subnet won't affect replies to inbound app requests. Common destinations can include firewall devices or gateways.

If you want to route all outbound traffic on-premises, you can use a route table to send all outbound traffic to your ExpressRoute gateway. If you do route traffic to a gateway, be sure to set routes in the external network to send any replies back.

Border Gateway Protocol (BGP) routes also affect your app traffic. If you have BGP routes from something like an ExpressRoute gateway, your app outbound traffic is affected. By default, BGP routes affect only your RFC1918 destination traffic. When your function app is virtual network integrated with **Route All** enabled, all outbound traffic can be affected by your BGP routes.

### Outbound IP restrictions

Outbound IP restrictions are available in a Flex Consumption plan, Elastic Premium plan, App Service plan, or App Service Environment. You can configure outbound restrictions for the virtual network where your App Service Environment is deployed.

When you integrate a function app in an Elastic Premium plan or an App Service plan with a virtual network, the app can still make outbound calls to the internet by default. By integrating your function app with a virtual network with Route All enabled, you force all outbound traffic to be sent into your virtual network, where network security group rules can be used to restrict traffic. For Flex Consumption all traffic is already routed through the virtual network and **Route All** isn't needed.

To learn how to control the outbound IP using a virtual network, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### Azure DNS private zones

After your app integrates with your virtual network, it uses the same DNS server that your virtual network is configured with and will work with the Azure DNS private zones linked to the virtual network.

### Automation

The following APIs let you programmatically manage regional virtual network integrations:

**Azure CLI**: Use thecommands to add, list, or remove a regional virtual network integration.`az functionapp vnet-integration`

**ARM templates**: Regional virtual network integration can be enabled by using an Azure Resource Manager template. For a full example, see[this Functions quickstart template](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/).

## Hybrid Connections

[Hybrid Connections](../azure-relay/relay-hybrid-connections-protocol) is a feature of Azure Relay that you can use to access application resources in other networks. It provides access from your app to an application endpoint. You can't use it to access your application. Hybrid Connections is available to functions that run on Windows in all but the Consumption plan.

As used in Azure Functions, each hybrid connection correlates to a single TCP host and port combination. This means that the hybrid connection's endpoint can be on any operating system and any application as long as you're accessing a TCP listening port. The Hybrid Connections feature doesn't know or care what the application protocol is or what you're accessing. It just provides network access.

To learn more, see the [App Service documentation for Hybrid Connections](../app-service/app-service-hybrid-connections). These same configuration steps support Azure Functions.

Important

Hybrid Connections is only supported when your function app runs on Windows. Linux apps aren't supported.

## Connecting to Azure Services through a virtual network

Virtual network integration enables your function app to access resources in a virtual network. This section overviews things you should consider when attempting to connect your app to certain services.

### Restrict your storage account to a virtual network

Note

To quickly deploy a function app with private endpoints enabled on the storage account, refer to the following template: [Function app with Azure Storage private endpoints](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-storage-private-endpoints).

When you create a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. You can replace this storage account with one that is secured with service endpoints or private endpoints.

You can use a network restricted storage account with function apps on the Flex Consumption, Elastic Premium, and Dedicated (App Service) plans; the Consumption plan isn't supported. For Elastic Premium and Dedicated plans, you have to ensure that private [content share routing](../app-service/configure-vnet-integration-routing#content-share) is configured. To learn how to configure your function app with a storage account secured with a virtual network, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

### Use Key Vault references

You can use Azure Key Vault references to use secrets from Azure Key Vault in your Azure Functions application without requiring any code changes. Azure Key Vault is a service that provides centralized secrets management, with full control over access policies and audit history.

If virtual network integration is configured for the app, [Key Vault references](../app-service/app-service-key-vault-references) can be used to retrieve secrets from a network-restricted vault.

### Virtual network triggers (non-HTTP)

Your workload might require your app to be triggered from an event source protected by a virtual network. There's two options if you want your app to dynamically scale based on the number of events received from non-HTTP trigger sources:

- Run your function app in a
[Flex Consumption](flex-consumption-plan). - Run your function app in an
[Elastic Premium plan](functions-premium-plan)and enable virtual network trigger support.

Function apps running on the [Dedicated (App Service)](dedicated-plan) plans don't dynamically scale based on events. Rather, scale out is dictated by [autoscale](dedicated-plan#scaling) rules you define.

#### Elastic Premium plan with virtual network triggers

The [Elastic Premium plan](functions-premium-plan) lets you create functions that are triggered by services secured by a virtual network. These non-HTTP triggers are known as *virtual network triggers*.

By default, virtual network triggers don't cause your function app to scale beyond their prewarmed instance count. However, certain extensions support virtual network triggers that cause your function app to scale dynamically. You can enable this *dynamic scale monitoring* in your function app for supported extensions in one of these ways:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Under

**Settings**select**Configuration**, then in the**Function runtime settings**tab set**Runtime Scale Monitoring**to**On**.Select

**Save**to update the function app configuration and restart the app.


Tip

Enabling the monitoring of virtual network triggers can affect the performance of your application, though the impact is likely to be small.

Support for dynamic scale monitoring of virtual network triggers isn't available in version 1.x of the Functions runtime.

The extensions in this table support dynamic scale monitoring of virtual network triggers. To get the best scaling performance, you should upgrade to versions that also support [target-based scaling](functions-target-based-scaling#premium-plan-with-runtime-scale-monitoring-enabled).

| Extension (minimum version) | Runtime scale monitoring only | With
|
|---|

[Microsoft.Azure.WebJobs.Extensions.CosmosDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB)[Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask)[Microsoft.Azure.WebJobs.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs)[Microsoft.Azure.WebJobs.Extensions.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage/)** Queue storage only.

Important

When you enable virtual network trigger monitoring, only triggers for these extensions can cause your app to scale dynamically. You can still use triggers from extensions that aren't in this table, but they won't cause scaling beyond their prewarmed instance count. For a complete list of all trigger and binding extensions, see [Triggers and bindings](functions-triggers-bindings#supported-bindings).

#### App Service plan and App Service Environment with virtual network triggers

When your function app runs in either an App Service plan or an App Service Environment, you can write functions that are triggered by resources secured by a virtual network. For your functions to get triggered correctly, your app must be connected to a virtual network with access to the resource defined in the trigger connection.

For example, assume you want to configure Azure Cosmos DB to accept traffic only from a virtual network. In this case, you must deploy your function app in an App Service plan that provides virtual network integration with that virtual network. Integration enables a function to be triggered by that Azure Cosmos DB resource.

## Testing considerations

When testing functions in a function app with private endpoints, you must do your testing from within the same virtual network, such as on a virtual machine (VM) in that network. To use the **Code + Test** option in the portal from that VM, you need to add following [CORS origins](functions-how-to-use-azure-function-app-settings?tabs=portal#cors) to your function app:

`https://functions-next.azure.com`

`https://functions-staging.azure.com`

`https://functions.azure.com`

`https://portal.azure.com`


When you restrict access to your function app with private endpoints or any other access restriction, you also must add the service tag `AzureCloud`

to the allowed list. To update the allowed list:

Navigate to your function app and select

**Settings**>**Networking**and then select**Inbound access configuration**>**Public network access**.Make sure that

**Public network access**is set to**Enabled from select virtual networks and IP addresses**.**Add a rule**under Site access and rules:Select

`Service Tag`

as the Source settings**Type**and`AzureCloud`

as the**Service Tag**.Make sure the action is

**Allow**, and set your desired name and priority.


## Troubleshooting

The feature is easy to set up, but that doesn't mean your experience will be problem free. If you encounter problems accessing your desired endpoint, there are some utilities you can use to test connectivity from the app console. There are two consoles that you can use. One is the Kudu console, and the other is the console in the Azure portal. To reach the Kudu console from your app, go to **Tools** > **Kudu**. You can also reach the Kudo console at [sitename].scm.azurewebsites.net. After the website loads, go to the **Debug console** tab. To get to the Azure portal-hosted console from your app, go to **Tools** > **Console**.

#### Tools

In native Windows apps, the tools **ping**, **nslookup**, and **tracert** won't work through the console because of security constraints (they work in [custom Windows containers](../app-service/quickstart-custom-container)). To fill the void, two separate tools are added. To test DNS functionality, we added a tool named **nameresolver.exe**. The syntax is:

```
nameresolver.exe hostname [optional: DNS Server]
```


You can use nameresolver to check the hostnames that your app depends on. This way you can test if you have anything misconfigured with your DNS or perhaps don't have access to your DNS server. You can see the DNS server that your app uses in the console by looking at the environmental variables WEBSITE_DNS_SERVER and WEBSITE_DNS_ALT_SERVER.

Note

The nameresolver.exe tool currently doesn't work in custom Windows containers.

You can use the next tool to test for TCP connectivity to a host and port combination. This tool is called **tcpping** and the syntax is:

```
tcpping.exe hostname [optional: port]
```


The **tcpping** utility tells you if you can reach a specific host and port. It can show success only if there's an application listening at the host and port combination, and there's network access from your app to the specified host and port.

#### Debug access to virtual network-hosted resources

A number of things can prevent your app from reaching a specific host and port. Most of the time it's one of these things:

**A firewall is in the way.**If you have a firewall in the way, you hit the TCP timeout. The TCP timeout is 21 seconds in this case. Use the**tcpping**tool to test connectivity. TCP timeouts can be caused by many things beyond firewalls, but start there.**DNS isn't accessible.**The DNS timeout is 3 seconds per DNS server. If you have two DNS servers, the timeout is 6 seconds. Use nameresolver to see if DNS is working. You can't use nslookup, because that doesn't use the DNS your virtual network is configured with. If inaccessible, you could have a firewall or NSG blocking access to DNS or it could be down.

If those items don't answer your problems, look first for things like:

**Regional virtual network integration**

- Is your destination a non-RFC1918 address and you don't have
**Route All**enabled? - Is there an NSG blocking egress from your integration subnet?
- If you're going across Azure ExpressRoute or a VPN, is your on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Do you have enough permissions to set delegation on the integration subnet? During regional virtual network integration configuration, your integration subnet is delegated to Microsoft.Web/serverFarms. The VNet integration UI delegates the subnet to Microsoft.Web/serverFarms automatically. If your account doesn't have sufficient networking permissions to set delegation, you'll need someone who can set attributes on your integration subnet to delegate the subnet. To manually delegate the integration subnet, go to the Azure Virtual Network subnet UI and set the delegation for Microsoft.Web/serverFarms.

**Gateway-required virtual network integration**

- Is the point-to-site address range in the RFC 1918 ranges (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255)?
- Does the gateway show as being up in the portal? If your gateway is down, then bring it back up.
- Do certificates show as being in sync, or do you suspect that the network configuration was changed? If your certificates are out of sync or you suspect that a change was made to your virtual network configuration that wasn't synced with your ASPs, select
**Sync Network**. - If you're going across a VPN, is the on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Are you trying to use a coexistence gateway that supports both point to site and ExpressRoute? Coexistence gateways aren't supported with virtual network integration.

Debugging networking issues is a challenge because you can't see what's blocking access to a specific host:port combination. Some causes include:

- You have a firewall up on your host that prevents access to the application port from your point-to-site IP range. Crossing subnets often requires public access.
- Your target host is down.
- Your application is down.
- You had the wrong IP or hostname.
- Your application is listening on a different port than what you expected. You can match your process ID with the listening port by using "netstat -aon" on the endpoint host.
- Your network security groups are configured in such a manner that they prevent access to your application host and port from your point-to-site IP range.

You don't know what address your app actually uses. It could be any address in the integration subnet or point-to-site address range, so you need to allow access from the entire address range.

More debug steps include:

- Connect to a VM in your virtual network and attempt to reach your resource host:port from there. To test for TCP access, use the PowerShell command
**Test-NetConnection**. The syntax is:

```
Test-NetConnection hostname [optional: -Port]
```


- Bring up an application on a VM and test access to that host and port from the console from your app by using
**tcpping**.

#### On-premises resources

If your app can't reach a resource on-premises, check if you can reach the resource from your virtual network. Use the **Test-NetConnection** PowerShell command to check for TCP access. If your VM can't reach your on-premises resource, your VPN or ExpressRoute connection might not be configured properly.

If your virtual network-hosted VM can reach your on-premises system but your app can't, the cause is likely one of the following reasons:

- Your routes aren't configured with your subnet or point-to-site address ranges in your on-premises gateway.
- Your network security groups are blocking access for your point-to-site IP range.
- Your on-premises firewalls are blocking traffic from your point-to-site IP range.
- You're trying to reach a non-RFC 1918 address by using the regional virtual network integration feature.

#### Deleting the App Service plan or web app before disconnecting the VNet integration

If you deleted the web app or the App Service plan without disconnecting the VNet integration first, you will not be able to do any update/delete operations on the virtual network or subnet that was used for the integration with the deleted resource. A subnet delegation 'Microsoft.Web/serverFarms' will remain assigned to your subnet and will prevent the update/delete operations.

In order to do update/delete the subnet or virtual network again you need to re-create the VNet integration and then disconnect it:

- Re-create the App Service plan and web app (it is mandatory to use the exact same web app name as before).
- Navigate to the 'Networking' blade on the web app and configure the VNet integration.
- After the VNet integration is configured, select the 'Disconnect' button.
- Delete the App Service plan or web app.
- Update/Delete the subnet or virtual network.

If you still encounter issues with the VNet integration after following the steps above, please contact Microsoft Support.

### Network troubleshooter

You can also use the Network troubleshooter to resolve connection issues. To open the network troubleshooter, go to the app in the Azure portal. Select **Diagnostic and solve problem**, and then search for **Network troubleshooter**.

**Connection issues** - It checks the status of the virtual network integration, including checking if the Private IP has been assigned to all instances of the plan and the DNS settings. If a custom DNS isn't configured, default Azure DNS is applied. The troubleshooter also checks for common Function app dependencies including connectivity for Azure Storage and other binding dependencies.


**Configuration issues** - This troubleshooter checks if your subnet is valid for virtual network integration.


**Subnet/VNet deletion issue** - This troubleshooter checks if your subnet has any locks and if it has any unused Service Association Links that might be blocking the deletion of the VNet/subnet.

## Next steps

To learn more about networking and Azure Functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Read the Functions networking FAQ](functions-networking-faq)[Learn more about virtual network integration with App Service/Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)[Connect to individual on-premises resources without firewall changes by using Hybrid Connections](../app-service/app-service-hybrid-connections)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale -->

# Azure Functions hosting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app in Azure, you must choose a hosting option for your app. Azure provides you with these hosting options for your function code:

| Hosting option | Service | Availability | Container support |
|---|---|---|---|
|
Azure Functions | Generally available (GA) | None |
|
Azure Functions | GA | Linux |
|
Azure Functions | GA | Linux |
|
Azure Container Apps | GA | Linux |
|
Azure Functions | Windows - GA Linux - Retired |
None |

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

The Azure App Service infrastructure on both Linux and Windows virtual machines facilitates the Azure Functions hosting options. The hosting option you choose dictates the following behaviors:

- How your function app is scaled.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.
- Support for Linux containers.

The plan you choose also impacts the costs for running your function code. For more information, see [Billing](#billing).

This article provides a detailed comparison between the various hosting options. To learn more about running and managing your function code in Linux containers, see [Linux container support in Azure Functions](container-concepts).

## Overview of plans

The following table summarizes the benefits of the various options for Azure functions hosting.

| Option | Benefits |
|---|---|
|
Experience fast horizontal scaling, with flexible compute options, virtual network integration, and serverless pay-as-you-go billing. In the Flex Consumption plan, function instances dynamically scale out (up to 1,000) based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Consider the Flex Consumption plan when: ✔ You need a serverless host for your function code, paying only for on-demand executions. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ Your workloads are variable and can go from no activity to demanding rapid, event-driven scaling. ✔ You want to customize compute with memory sizes (512 MB, 2,048 MB, or 4,096 MB) and reduce cold starts via one or more pre-provisioned (always-ready) instances. |
|
Automatically scales based on demand using prewarmed workers, which run applications with no delay after being idle, runs on more powerful instances, and connects to virtual networks. Consider the Azure Functions Premium plan in the following situations: ✔ Your function apps run continuously, or nearly continuously. ✔ You want more control of your instances and want to deploy multiple function apps on the same plan with event-driven scaling. ✔ You have a high number of small executions and a high execution bill, but low GB seconds in the Consumption plan. ✔ You need more CPU or memory options than are provided by consumption plans. ✔ Your code needs to run longer than the maximum execution time allowed on the Consumption plan. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ You want to provide a custom Linux image in which to run your functions. |
|
Run your functions within an App Service plan at regular
Best for long-running scenarios where
✔ You have existing and underutilized virtual machines that are already running other App Service instances. ✔ You must have fully predictable billing, or you need to manually scale instances. ✔ You want to run multiple web apps and function apps on the same plan ✔ You need access to larger compute size choices. ✔ Full compute isolation and secure network access provided by an App Service Environment (ASE). ✔ Very high memory usage and high scale (ASE). |

[Container Apps](../container-apps/functions-overview)Use the Azure Functions programming model to build event-driven, serverless, cloud native function apps. Run your functions alongside other microservices, APIs, websites, and workflows as container-hosted programs. Consider hosting your functions on Container Apps in the following situations:

✔ You want control of the container image and want to package custom libraries with your function code to support line-of-business apps.

✔ You need to migrate code execution from on-premises or legacy apps to cloud native microservices running in containers.

✔ When you want to avoid the overhead and complexity of managing Kubernetes clusters and dedicated compute.

✔ Your functions need high-end processing power provided by dedicated GPU compute resources.

[Consumption plan](consumption-plan)On the Consumption plan, function instances are dynamically added and removed based on the number of incoming events.

Consider the Consumption plan when:

✔ You have a dependency on Windows. For example, using the v1 runtime, the full .NET Framework, or Windows-specific features like certain PowerShell modules.

✔ You want a serverless billing model and pay only when your functions are running.

The remaining tables in this article compare hosting options based on various features and behaviors.

## Operating system support

This table shows operating system support for the hosting options.

| Hosting | Linux1 deployment |
Windows2 deployment |
|---|---|---|
|
✅ Code-only ❌ Container (not supported) |
❌ Not supported |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Container-only | ❌ Not supported |
3 |
✅ Code-only (Retired) ❌ Container (not supported) |
✅ Code-only |

- Linux is the only supported operating system for the
[Python runtime stack](functions-reference-python). - Windows deployments are code-only. Azure Functions doesn't currently support Windows containers.
- The ability to run your app on Linux in a Consumption plan will be retired on 30 September 2028. For more information, see
[Consumption plan](consumption-plan).

## Function app timeout duration

The `functionTimeout`

property in the [host.json](functions-host-json#functiontimeout) project file sets the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return or respond within the timeout duration. When an execution exceeds this duration, a timeout error occurs and the language worker process restarts. For C# apps running in-process, the host process itself restarts. To avoid timeouts and subsequent process restarts, it's important to [write robust functions](functions-best-practices#write-robust-functions). For more information, see [Improve Azure Functions performance and reliability](performance-reliability#make-sure-background-tasks-complete).

The following table shows the default and maximum values (in minutes) for specific plans:

| Plan | Default | Maximum1 |
|---|---|---|
|
30 | Unbounded2 |
|
304 |
Unbounded2 |
|
304 |
Unbounded3 |
|
30 | Unbounded5 |
|
5 | 10 |

- Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request. This limit exists because of the
[default idle timeout of Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds). For longer processing times, consider using the[Durable Functions async pattern](durable/durable-functions-overview#async-http)or[defer the actual work and return an immediate response](performance-reliability#avoid-long-running-functions). - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)for the Flex Consumption and Premium plans, and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates. - The default timeout for version 1.x of the Functions host runtime is
*unbounded*. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app.

These values assume that the Azure Functions host process starts and runs correctly. There's a maximum timeout of 60 seconds for the language-specific worker process to also start. The worker process startup timeout isn't currently configurable.

## Language support

For details on current native language stack support in Functions, see [Supported languages in Azure Functions](supported-languages).

## Scale

The following table compares the scaling behaviors of the various hosting plans.

Maximum instances are given on a per-function app (Consumption) or per-plan (Premium/Dedicated) basis, unless otherwise indicated.

| Plan | Scale out | Max # instances |
|---|---|---|
|
Fast event-driven scaling decisions are calculated on a per-function basis, called
|

1[Premium plan](functions-premium-plan)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.**Windows:**1006**Linux:**20-1002,6[Dedicated plan](dedicated-plan)3100 (ASE)

[Container Apps](../container-apps/functions-overview)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.4[Consumption plan](consumption-plan)[Event driven](event-driven-scaling). Automatic scale based on the source of events. Functions infrastructure scales resources by adding more instances of the function host, based on the number of incoming trigger events.**Windows:**200**Linux:**1005- Flex Consumption plan has a regional subscription quota that limits the total memory usage of all instances across a given region. For more information, see
[Regional subscription memory quotas](flex-consumption-plan#regional-subscription-memory-quotas). Flex Consumption plans currently only support Linux. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. For more information, see[Quotas for Azure Container Apps](/en-us/azure/container-apps/quotas). When you create your function app from the Azure portal, you're limited to 300 instances. - During scale-out, there's currently a limit of 500 instances per subscription per hour for Linux apps on a Consumption plan.
- For private endpoint restricted http triggers, scaling out is limited to at most 20 instances.

## Cold start behavior

| Plan | Details |
|---|---|
|
Improved cold start even when scaled to zero. Supports
|

[Premium plan](functions-premium-plan)[always ready instances](functions-premium-plan#always-ready-instances)to avoid cold starts by letting you maintain one or more*perpetually warm*instances.[Dedicated plan](dedicated-plan)[Container Apps](../container-apps/functions-overview)[minimum number of replicas](../container-apps/scale-app#scale-definition):• When set to zero: apps can scale to zero when idle and some requests might have more latencies at startup.

• When set to one or more: the host process runs continuously, which means that cold start isn't an issue.

[Consumption plan](consumption-plan)## Service limits

| Resource |
|
|---|

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/overview)

[Container Apps](../container-apps/functions-overview)

[Consumption plan](consumption-plan)

[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)116[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)99217[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits)333[ACU](/en-us/azure/virtual-machines/acu)per instance10[varies](/en-us/azure/container-apps/billing)14[varies](/en-us/azure/container-apps/billing)1511181344[App Service plans](/en-us/azure/app-service/overview-hosting-plans)[region](https://azure.microsoft.com/global-infrastructure/regions/)[Deployment slots](/en-us/azure/azure-functions/functions-deployment-slots)per app121157116,788[TSL/SSL support](/en-us/azure/app-service/configure-ssl-bindings)Notes on service limits:

- By default, the time-out for the Functions 1.x runtime in an App Service plan is unbounded.
- Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). Pay at standard[rates](https://azure.microsoft.com/pricing/details/app-service/). A grace period of 10 minutes is given for HTTP triggered functions during platform updates but not for other triggers. - These limits are
[set in the host](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script.WebHost/web.config). - The actual number of function apps that you can host depends on the activity of the apps, the size of the machine instances, and the corresponding resource utilization.
- The storage limit is the total content size in temporary storage across all apps in the same App Service plan. For Consumption plans on Linux, the storage is currently 1.5 GB.
- Consumption plan uses an Azure Files share for persisted storage. When you provide your own Azure Files share, the specific share size limits depend on the storage account you set for
[WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](/en-us/azure/azure-functions/functions-app-settings#website_contentazurefileconnectionstring). - On Linux, you must
[explicitly mount your own Azure Files share](/en-us/azure/azure-functions/storage-considerations#mount-file-shares). - When your function app is hosted in a
[Consumption plan](/en-us/azure/azure-functions/consumption-plan), only the CNAME option is supported. For function apps in a[Premium plan](/en-us/azure/azure-functions/functions-premium-plan)or an[App Service plan](/en-us/azure/azure-functions/dedicated-plan), you can map a custom domain using either a CNAME or an A record. - There's no maximum execution time-out duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)and 10 minutes during platform updates. - Workers are roles that host customer apps. Workers are available in three fixed sizes: One vCPU/3.5 GB RAM; Two vCPU/7 GB RAM; Four vCPU/14 GB RAM.
- See
[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#app-service-limits)for details. - Including the production slot.
- There's currently a limit of 5,000 function apps in a given subscription.
- Flex Consumption plan instance sizes are currently defined as 512 MB, 2,048 MB, or 4,096 MB. For more information, see
[Instance memory](/en-us/azure/azure-functions/flex-consumption-plan#instance-sizes). - For details, see
[Scale](functions-scale#scale)in the Hosting comparison article. - When the
[minimum number of replicas](/en-us/azure/container-apps/scale-app#scale-definition)is set to zero, the default time-out depends on the specific triggers used in the app. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to one or more.

## Networking features

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Billing

| Plan | Details |
|---|---|
|
Billing is based on number of executions, the memory of instances when they're actively executing functions, plus the cost of any
|

[Premium plan](functions-premium-plan)[Dedicated plan](dedicated-plan)For an ASE, there's a flat monthly rate that pays for the infrastructure and doesn't change with the size of the environment. There's also a cost per App Service plan vCPU. All apps hosted in an ASE are in the Isolated pricing model. For more information, see the

[ASE overview article](../app-service/environment/overview#pricing).[Container Apps](../container-apps/functions-overview)[Billing in Azure Container Apps](../container-apps/billing).[Consumption plan](consumption-plan)For a direct cost comparison between dynamic hosting plans (Consumption, Flex Consumption, and Premium), see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For pricing of the various Dedicated plan options, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service). For pricing Container Apps hosting, see [Azure Container Apps pricing](https://azure.microsoft.com/pricing/details/container-apps/).

## Limitations for creating new function apps in an existing resource group

In some cases, when trying to create a new hosting plan for your function app in an existing resource group you might receive one of the following errors:

- The pricing tier isn't allowed in this resource group
- <SKU_name> workers aren't available in resource group <resource_group_name>

These errors can occur when the following conditions are met:

- You create a function app in an existing resource group that has yet to contain another function app or web app. For example, Linux Consumption apps aren't supported in the same resource group as Linux Dedicated or Linux Premium plans.
- Your new function app is created in the same region as the previous app.
- The previous app is in some way incompatible with your new app. This incompatibility can occur between versions, operating systems, or is due to other platform-level features, such as availability zone support.

Function app and web app plans are mapped to different pools of resources when they're created. Different plans require a different set of infrastructure capabilities. When you create an app in a resource group, that resource group is mapped and assigned to a specific pool of resources. If you try to create another plan in that resource group and the mapped pool doesn't have the required resources, the previously mentioned errors occur.

If this situation happens, create your function app and hosting plan in a new resource group instead.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-based-connections-tutorial -->

# Tutorial: Create a function app that connects to Azure services using identities instead of secrets

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to configure a function app using Microsoft Entra identities instead of secrets or connection strings, where possible. Using identities helps you avoid accidentally leaking sensitive secrets and can provide better visibility into how data is accessed. To learn more about identity-based connections, see [configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

While the procedures shown work generally for all languages, this tutorial currently supports C# class library functions on Windows specifically.

In this tutorial, you learn how to:

- Create a function app in Azure using an ARM template
- Enable both system-assigned and user-assigned managed identities on the function app
- Create role assignments that give permissions to other resources
- Move secrets that can't be replaced with identities into Azure Key Vault
- Configure an app to connect to the default host storage using its managed identity

After you complete this tutorial, you should complete the follow-on tutorial that shows how to [use identity-based connections instead of secrets with triggers and bindings](functions-identity-based-connections-tutorial-2).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Why use identity?

Managing secrets and credentials is a common challenge for teams of all sizes. Secrets need to be secured against theft or accidental disclosure, and they might need to be periodically rotated. Many Azure services allow you to instead use an identity in [Microsoft Entra ID](../active-directory/fundamentals/active-directory-whatis) to authenticate clients and check against permissions, which can be modified and revoked quickly. Doing so allows for greater control over application security with less operational overhead. An identity could be a human user, such as the developer of an application, or a running application in Azure with a [managed identity](../active-directory/managed-identities-azure-resources/overview).

Because some services don't support Microsoft Entra authentication, your applications might still require secrets in certain cases. However, these secrets can be stored in [Azure Key Vault](/en-us/azure/key-vault/general/overview), which helps simplify the management lifecycle for your secrets. Access to a key vault is also controlled with identities.

By understanding how to use identities instead of secrets when you can, and to use Key Vault when you can't, you reduce risk, decrease operational overhead, and generally improve the security posture for your applications.

## Create a function app that uses Key Vault for necessary secrets

Azure Files is an example of a service that doesn't yet support Microsoft Entra authentication for Server Message Block (SMB) file shares. Azure Files is the default file system for Windows deployments on Premium and Consumption plans. While we could [remove Azure Files entirely](storage-considerations#create-an-app-without-azure-files), doing so introduces limitations you might not want. Instead, you move the Azure Files connection string into Azure Key Vault. That way it's centrally managed, with access controlled by the identity.

### Create an Azure Key Vault

First you need a key vault to store secrets in. You configure it to use [Azure role-based access control (RBAC)](../role-based-access-control/overview) for determining who can read secrets from the vault.

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Security**>**Key Vault**.On the

**Basics**page, use the following table to configure the key vault.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Key vault name**Globally unique name Name that identifies your new key vault. The vault name must only contain alphanumeric characters and dashes and can't start with a number. **Pricing Tier**Standard Options for billing. Standard is sufficient for this tutorial. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.Use the default selections for the "Recovery options" sections.

Make a note of the name you used, for use later.

Select

**Next: Access Policy**to navigate to the**Access Policy**tab.Under

**Permission model**, choose**Azure role-based access control**Select

**Review + create**. Review the configuration, and then select**Create**.

### Set up an identity and permissions for the app

In order to use Azure Key Vault, your app needs to have an identity that can be granted permission to read secrets. This app uses a user-assigned identity so that the permissions can be set up before the app is even created. For more information about managed identities for Azure Functions, see [How to use managed identities in Azure Functions](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json).

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Identity**>**User Assigned Managed Identity**.On the

**Basics**page, use the following table to configure the identity.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Name**Globally unique name Name that identifies your new user-assigned identity. Select

**Review + create**. Review the configuration, and then select**Create**.When the identity is created, navigate to it in the portal. Select

**Properties**, and make note of the**Resource ID**for use later.Select

**Azure Role Assignments**, and select**Add role assignment (Preview)**.In the

**Add role assignment (Preview)**page, use options as shown in the following table.Option Suggested value Description **Scope**Key Vault Scope is a set of resources that the role assignment applies to. Scope has levels that are inherited at lower levels. For example, if you select a subscription scope, the role assignment applies to all resource groups and resources in the subscription. **Subscription**Your subscription Subscription under which this new function app is created. **Resource**Your key vault The key vault you created earlier. **Role**Key Vault Secrets User A role is a collection of permissions that are being granted. Key Vault Secrets User gives permission for the identity to read secret values from the vault. Select

**Save**. It might take a minute or two for the role to show up when you refresh the role assignments list for the identity.

The identity is now able to read secrets stored in the key vault. Later in the tutorial, you add additional role assignments for different purposes.

### Generate a template for creating a function app

Because the portal experience for creating a function app doesn't interact with Azure Key Vault, you need to generate and edit an Azure Resource Manager template. You can then use this template to create your function app referencing the Azure Files connection string from your key vault.

Important

Don't create the function app until after you edit the ARM template. The Azure Files configuration needs to be set up at app creation time.

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.Select

**Review + create**. Your app uses the default values on the**Hosting**and**Monitoring**page. Review the default options, which are included in the ARM template that you generate.Instead of creating your function app here, choose

**Download a template for automation**, which is to the right of the**Next**button.In the template page, select

**Deploy**, then in the Custom deployment page, select**Edit template**.

### Edit the template

You now edit the template to store the Azure Files connection string in Key Vault and allow your function app to reference it. Make sure that you have the following values from the earlier sections before proceeding:

- The resource ID of the user-assigned identity
- The name of your key vault

Note

If you were to create a full template for automation, you would want to include definitions for the identity and role assignment resources, with the appropriate `dependsOn`

clauses. This would replace the earlier steps which used the portal. Consult the [Azure Resource Manager guidance](../azure-resource-manager/templates/syntax) and the documentation for each service.

In the editor, find where the

`resources`

array begins. Before the function app definition, add the following section, which puts the Azure Files connection string into Key Vault. Substitute "VAULT_NAME" with the name of your key vault.`{ "type": "Microsoft.KeyVault/vaults/secrets", "apiVersion": "2016-10-01", "name": "VAULT_NAME/azurefilesconnectionstring", "properties": { "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2019-06-01').keys[0].value,';EndpointSuffix=','core.windows.net')]" }, "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]" ] },`

In the definition for the function app resource (which has

`type`

set to`Microsoft.Web/sites`

), add`Microsoft.KeyVault/vaults/VAULT_NAME/secrets/azurefilesconnectionstring`

to the`dependsOn`

array. Again, substitute "VAULT_NAME" with the name of your key vault. Doing so prevents your app from being created before the secret is defined. The`dependsOn`

array should look like the following example:`{ "type": "Microsoft.Web/sites", "apiVersion": "2018-11-01", "name": "[parameters('name')]", "location": "[parameters('location')]", "tags": null, "dependsOn": [ "microsoft.insights/components/idcxntut", "Microsoft.KeyVault/vaults/VAULT_NAME/secrets/azurefilesconnectionstring", "[concat('Microsoft.Web/serverfarms/', parameters('hostingPlanName'))]", "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]" ], // ... }`

Add the

`identity`

block from the following example into the definition for your function app resource. Substitute "IDENTITY_RESOURCE_ID" for the resource ID of your user-assigned identity.`{ "apiVersion": "2018-11-01", "name": "[parameters('name')]", "type": "Microsoft.Web/sites", "kind": "functionapp", "location": "[parameters('location')]", "identity": { "type": "SystemAssigned,UserAssigned", "userAssignedIdentities": { "IDENTITY_RESOURCE_ID": {} } }, "tags": null, // ... }`

This

`identity`

block also sets up a system-assigned identity, which you use later in this tutorial.Add the

`keyVaultReferenceIdentity`

property to the`properties`

object for the function app, as in the following example. Substitute "IDENTITY_RESOURCE_ID" for the resource ID of your user-assigned identity.`{ // ... "properties": { "name": "[parameters('name')]", "keyVaultReferenceIdentity": "IDENTITY_RESOURCE_ID", // ... } }`

You need this configuration because an app could have multiple user-assigned identities configured. Whenever you want to use a user-assigned identity, you must specify it with an ID. System-assigned identities don't need to be specified this way, because an app can only ever have one. Many features that use managed identity assume they should use the system-assigned one by default.

Find the JSON objects that define the

`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

application setting, which should look like the following example:`{ "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING", "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2019-06-01').keys[0].value,';EndpointSuffix=','core.windows.net')]" },`

Replace the

`value`

field with a reference to the secret as shown in the following example. Substitute "VAULT_NAME" with the name of your key vault.`{ "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING", "value": "[concat('@Microsoft.KeyVault(SecretUri=', reference(resourceId('Microsoft.KeyVault/vaults/secrets', 'VAULT_NAME', 'azurefilesconnectionstring')).secretUri, ')')]" },`

Select

**Save**to save the updated ARM template.

### Deploy the modified template

Make sure that your create options, including

**Resource Group**, are still correct and select**Review + create**.After your template validates, make a note of your

**Storage Account Name**, since you'll use this account later. Finally, select**Create**to create your Azure resources and deploy your code to the function app.After deployment completes, select

**Go to resource group**and then select the new function app.

Congratulations! You've successfully created your function app to reference the Azure Files connection string from Azure Key Vault.

Whenever your app would need to add a reference to a secret, you would just need to define a new application setting pointing to the value stored in Key Vault. For more information, see [Key Vault references for Azure Functions](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json).

Tip

The [Application Insights connection string](/en-us/azure/azure-monitor/app/sdk-connection-string) and its included instrumentation key are not considered secrets and can be retrieved from App Insights using [Reader](../role-based-access-control/built-in-roles#reader) permissions. You do not need to move them into an Azure Key Vault instance, although you certainly can. If you choose to use Key Vault, your function app must have a managed identity that can be used to securely retrieve the secret [using a Key Vault reference in the app settings](../app-service/app-service-key-vault-references).

## Use managed identity for AzureWebJobsStorage

Next, you use the system-assigned identity you configured in the previous steps for the `AzureWebJobsStorage`

connection. `AzureWebJobsStorage`

is used by the Functions runtime and by several triggers and bindings to coordinate between multiple running instances. It's required for your function app to operate, and like Azure Files, is configured with a connection string by default when you create a new function app.

### Grant the system-assigned identity access to the storage account

Similar to the steps you previously followed with the user-assigned identity and your key vault, you now create a role assignment granting the system-assigned identity access to your storage account.

In the

[Azure portal](https://portal.azure.com), navigate to the storage account that was created with your function app earlier.Select

**Access Control (IAM)**. This page is where you can view and configure who has access to the resource.Select

**Add**and select**add role assignment**.Search for

**Storage Blob Data Owner**, select it, and select**Next**On the

**Members**tab, under**Assign access to**, choose**Managed Identity**Select

**Select members**to open the**Select managed identities**panel.Confirm that the

**Subscription**is the one in which you created the resources earlier.In the

**Managed identity**selector, choose**Function App**from the**System-assigned managed identity**category. The**Function App**label might have a number in parentheses next to it, indicating the number of apps in the subscription with system-assigned identities.Your app should appear in a list below the input fields. If you don't see it, you can use the

**Select**box to filter the results with your app's name.Select your application. It should move down into the

**Selected members**section. Choose**Select**.On the

**Add role assignment**screen, select**Review + assign**. Review the configuration, and then select**Review + assign**.

Tip

If you intend to use the function app for a blob-triggered function, you will need to repeat these steps for the **Storage Account Contributor** and **Storage Queue Data Contributor** roles over the account used by AzureWebJobsStorage. To learn more, see [Blob trigger identity-based connections](functions-bindings-storage-blob-trigger#identity-based-connections).

### Edit the AzureWebJobsStorage configuration

Next you update your function app to use its system-assigned identity when it uses the blob service for host storage.

Important

The `AzureWebJobsStorage`

configuration is used by some triggers and bindings, and those extensions must be able to use identity-based connections, too. Apps that use blob triggers or event hub triggers may need to update those extensions. Because no functions have been defined for this app, there isn't a concern yet. To learn more about this requirement, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

Similarly, `AzureWebJobsStorage`

is used for deployment artifacts when using server-side build in Linux Consumption. When you enable identity-based connections for `AzureWebJobsStorage`

in Linux Consumption, you will need to deploy via [an external deployment package](run-functions-from-deployment-package).

In the

[Azure portal](https://portal.azure.com), navigate to your function app.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select the**AzureWebJobsStorage**app setting, and edit it according to the following table:Option Suggested value Description **Name**AzureWebJobsStorage__accountName Change the name from **AzureWebJobsStorage**to the exact name`AzureWebJobsStorage__accountName`

. This setting instructs the host to use the identity instead of searching for a stored secret. The new setting uses a double underscore (`__`

), which is a special character in application settings.**Value**Your account name Update the name from the connection string to just your **StorageAccountName**.This configuration tells the system to use an identity to connect to the resource.

Select

**Apply**, and then select**Apply**and**Confirm**to save your changes and restart the app function.

You've now removed the storage connection string requirement for AzureWebJobsStorage by configuring your app to instead connect to blobs using managed identities.

Note

The `__accountName`

syntax is unique to the AzureWebJobsStorage connection and cannot be used for other storage connections. To learn to define other connections, check the reference for each trigger and binding your app uses.

## Next steps

This tutorial showed how to create a function app without storing secrets in its configuration.

Advance to the next tutorial to learn how to use identities in trigger and binding connections.
