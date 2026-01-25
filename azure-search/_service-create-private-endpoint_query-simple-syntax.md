---
merged_at: 2026-01-25T03:18:14.059881
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: service-create-private-endpoint.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/service-create-private-endpoint -->

# Create a private endpoint for a secure connection to Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure a private connection to Azure AI Search so that it admits requests from clients in a virtual network instead of over a public internet connection.

## Prerequisites

[Azure AI Search service](search-create-service-portal)(Basic tier or higher). Private endpoints aren't supported on the Free tier.**Contributor**or**Owner**role on the resource group where you create resources.- A
[common region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/table)with availability for Azure AI Search, a virtual network, and a virtual machine. All three resources must reside in the same region. - Familiarity with
[Azure Virtual Network](/en-us/azure/virtual-network/virtual-networks-overview)concepts (optional but recommended).

## Overview

This article walks you through these steps:

[Create an Azure virtual network](#create-the-virtual-network)(or use an existing one)[Configure a search service with a private endpoint](#create-a-search-service-with-a-private-endpoint)[Create an Azure virtual machine](#create-a-virtual-machine)in the same virtual network[Test the connection](#connect-to-the-vm)from the virtual machine

Private endpoints are provided by [Azure Private Link](/en-us/azure/private-link/private-link-overview), as a separate billable service. For more information about costs, see [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/).

You can create a private endpoint using the Azure portal (described in this article), [Management REST API](/en-us/rest/api/searchmanagement/), [Azure PowerShell](/en-us/powershell/module/az.search), or [Azure CLI](/en-us/cli/azure/search).

## Why use a private endpoint?

[Private endpoints](/en-us/azure/private-link/private-endpoint-overview) for Azure AI Search allow a client on a virtual network to securely access data in a search index over a [Private Link](/en-us/azure/private-link/private-link-overview). The private endpoint uses an IP address from the [virtual network address space](/en-us/azure/virtual-network/ip-services/private-ip-addresses) for your search service. Network traffic between the client and the search service traverses over the virtual network and a private link on the Microsoft backbone network, eliminating exposure from the public internet. For a list of other PaaS services that support Private Link, check the [availability section](/en-us/azure/private-link/private-link-overview#availability) in the product documentation.

Private endpoints for your search service allow you to:

- Block all connections on the public endpoint for your search service.
- Increase security for the virtual network, by letting you block exfiltration of data from the virtual network.
- Securely connect to your search service from on-premises networks that connect to the virtual network using
[VPN](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways)or[ExpressRoutes](/en-us/azure/expressroute/expressroute-locations)with private-peering.

## Create the virtual network

In this section, you create a virtual network and subnet to host the VM that will be used to access your search service's private endpoint.

From the Azure portal home tab, select

**Create a resource**>**Infrastructure Services**>**Virtual network**.In

**Create virtual network**, enter or select the following values:Setting Value Subscription Select your subscription Resource group Select **Create new**, enter a name, such as*myResourceGroup*, then select**OK**Name Enter a name, such as *MyVirtualNetwork*Region Select a region Accept the defaults for the rest of the settings. Select

**Review + create**and then**Create**.

## Create a search service with a private endpoint

In this section, you create a new Azure AI Search service with a private endpoint.

On the upper-left side of the screen in the Azure portal, select

**Create a resource**>**Machine learning**>**AI Search**.In

**Create a search service - Basics**, enter or select the following values:Setting Value **PROJECT DETAILS**Subscription Select your subscription Resource group Use the resource group that you created in the previous step **INSTANCE DETAILS**URL Enter a unique name Location Select your region. [Choose a region](search-region-support)that provides Azure AI Search.Pricing tier Select **Change Pricing Tier**and choose your desired service tier. Private endpoints aren't supported on the**Free**tier. You must select**Basic**or higher.Select

**Next: Scale**.Accept the defaults and select

**Next: Networking**.In

**Create a search service - Networking**, select**Private**for**Endpoint connectivity (data)**.Select

**+ Add**under**Private endpoint**.In

**Create private endpoint**, enter or select values that associate your search service with the virtual network you created:Setting Value Subscription Select your subscription Resource group Use the resource group that you created in the previous step Location Select a region. Choose the same region used by the virtual network. Name Enter a name, such as *myPrivateEndpoint*Target subresource Accept the default **searchService****NETWORKING**Virtual network Select the virtual network you created in the previous step Subnet Select the default **PRIVATE DNS INTEGRATION**Integrate with private DNS zone Select **Yes**.Private DNS zone Accept the default **(New) privatelink.search.windows.net**Select

**Add**.Select

**Review + create**. You're taken to the**Review + create**page where Azure validates your configuration.When you see the

**Validation passed**message, select**Create**.Once provisioning of your new service is complete, browse to the resource that you created.

Select

**Settings**>**Keys**from the left content menu.Copy the

**Primary admin key**for later, when connecting to the service.

## Create a virtual machine

On the upper-left side of the screen in the Azure portal, select

**Create a resource**>**Infrastructure Services**>**Virtual machine**.In

**Create a virtual machine - Basics**, enter or select the following values:Setting Value **PROJECT DETAILS**Subscription Select your subscription Resource group Use the resource group that you created in the previous section **INSTANCE DETAILS**Virtual machine name Enter a name, such as *my-vm*Region Select your region Availability options You can choose **No infrastructure redundancy required**, or select another option if you need the functionalitySecurity type Accept the default **Trusted launch virtual machines**Image Select **Windows Server 2025 Datacenter: Azure Edition - x64 Gen2**VM architecture Accept the default **x64**Size Accept the default **Standard D2S v3****ADMINISTRATOR ACCOUNT**Username Enter the user name of the administrator. Use an account that's valid for your Azure subscription. Sign in to the Azure portal from the VM so that you can manage your search service. Password Enter the account password. The password must be at least 12 characters long and meet the [defined complexity requirements](/en-us/azure/virtual-machines/windows/faq?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm-).Confirm Password Reenter password **INBOUND PORT RULES**Public inbound ports Accept the default **Allow selected ports**Select inbound ports Accept the default **RDP (3389)**Select

**Next: Disks**.In

**Create a virtual machine - Disks**, accept the defaults and select**Next: Networking**.In

**Create a virtual machine - Networking**, provide the following values:Setting Value Virtual network Select the virtual network you created in a previous step Subnet Accept the default **10.1.0.0/24**Public IP Accept the default NIC network security group Accept the default **Basic**Public inbound ports Select the default **Allow selected ports**Select inbound ports Select **HTTP 80**,**HTTPS (443)**, and**RDP (3389)**Select

**Review + create**for a validation check.When you see the

**Validation passed**message, select**Create**.

## Connect to the VM

Download and then connect to the virtual machine as follows:

In the Azure portal's search bar, search for the virtual machine created in the previous step.

Select

**Connect**. After selecting the**Connect**button,**Connect to virtual machine**opens.Select

**Download RDP File**. Azure creates a Remote Desktop Protocol (*.rdp*) file and downloads it to your computer.Open the downloaded

*.rdp*file.If prompted, select

**Connect**.Enter the username and password you specified when creating the VM.

Note

You might need to select

**More choices**>**Use a different account**, to specify the credentials you entered when you created the VM.

Select

**OK**.You might receive a certificate warning during the sign-in process. If you receive a certificate warning, select

**Yes**or**Continue**.Once the VM desktop appears, minimize it to go back to your local desktop.


## Test connections

In this section, you verify private network access to the search service and connect privately to the using the Private Endpoint.

When the search service endpoint is private, some portal features are disabled. You can view and manage service level settings, but portal access to index data and various other components in the service, such as the index, indexer, and skillset definitions, is restricted for security reasons.

In the Remote Desktop of

*myVM*, open PowerShell.Enter

`nslookup [search service name].search.windows.net`

.You'll receive a message similar to this:

`Server: UnKnown Address: 168.63.129.16 Non-authoritative answer: Name: [search service name].privatelink.search.windows.net Address: 10.0.0.5 Aliases: [search service name].search.windows.net`

The

`privatelink`

in the Name field and the private IP address (10.x.x.x) in the Address field confirm that the private endpoint is configured correctly.From the VM, connect to the search service and create an index. You can follow this

[quickstart](search-get-started-text)to create a new search index in your service using the REST API. Setting up requests from a Web API test tool requires the search service endpoint`(https://[search service name].search.windows.net)`

and the admin api-key you copied in a previous step.**Reference:**[Create Index (REST API)](/en-us/rest/api/searchservice/indexes/create)Completing the quickstart from the VM is your confirmation that the service is fully operational.

Close the remote desktop connection to

*myVM*.To verify that your service isn't accessible on a public endpoint, open a REST client on your local workstation and attempt the first several tasks in the quickstart. If you receive an error that the remote server doesn't exist, you successfully configured a private endpoint for your search service.


## Use the Azure portal to access a private search service

When the search service endpoint is private, some portal features are disabled. You can view and manage service level information, but index, indexer, and skillset information are hidden for security reasons.

To work around this restriction, connect to Azure portal from a browser on a virtual machine inside the virtual network. The Azure portal uses the private endpoint on the connection and gives you visibility into content and operations.

Follow the

[steps to provision a VM that can access the search service through a private endpoint](#create-virtual-machine-private-endpoint).On a virtual machine in your virtual network, open a browser and sign in to the Azure portal. the Azure portal uses the private endpoint attached to the virtual machine to connect to your search service.


## Disable public network access

You can lock down a search service to prevent it from admitting any request from the public internet. You can use the Azure portal for this step.

In the Azure portal, on the leftmost pane of your search service page, select

**Networking**.Select

**Disabled**on the**Firewalls and virtual networks**tab.

You can also use the [Azure CLI](/en-us/cli/azure/search/service?view=azure-cli-latest#az-search-service-update&preserve-view=true), [Azure PowerShell](/en-us/powershell/module/az.search/set-azsearchservice), or the [Management REST API](/en-us/rest/api/searchmanagement/), by setting `public-access`

or `public-network-access`

to `disabled`

.

## Clean up resources

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money.

You can delete individual resources or the resource group to delete everything you created in this exercise. Select the resource group on any resource's overview page, and then select **Delete**.

## Next step

In this article, you created a VM on a virtual network and a search service with a private endpoint. You connected to the VM from the internet and securely communicated to the search service using Private Link. To learn more about private endpoints, see [What is a private endpoint?](/en-us/azure/private-link/private-endpoint-overview)


---

<!-- DOCUMENTO FUSIONADO: query-simple-syntax.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/query-simple-syntax -->

# Simple query syntax in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For full text search scenarios, Azure AI Search implements two Lucene-based query languages, each one aligned to a query parser. The [Simple Query Parser](https://lucene.apache.org/core/6_6_1/queryparser/org/apache/lucene/queryparser/simple/SimpleQueryParser.html) is the default. It covers common use cases and attempts to interpret a request even if it's not perfectly composed. The other parser is [Lucene Query Parser](https://lucene.apache.org/core/6_6_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html) and it supports more advanced query constructions.

This article is the query syntax reference for the simple query parser.

Query syntax for both parsers applies to query expressions passed in the `search`

parameter of a [query request](search-query-create), not to be confused with the [OData syntax](query-odata-filter-orderby-syntax), with its own syntax and rules for [ filter](search-filters) and

[expressions in the same request.](search-query-odata-orderby)

`orderby`

Although the simple parser is based on the [Apache Lucene Simple Query Parser](https://lucene.apache.org/core/6_6_1/queryparser/org/apache/lucene/queryparser/simple/SimpleQueryParser.html) class, its implementation in Azure AI Search excludes fuzzy search. If you need [fuzzy search](search-query-fuzzy), consider the alternative [full Lucene query syntax](query-lucene-syntax) instead.

## Example (simple syntax)

This example shows a simple query, distinguished by `"queryType": "simple"`

and valid syntax. Although query type is set below, it's the default and can be omitted unless you're reverting from an alternative type. The following example is a search over independent terms, with a requirement that all matching documents include "pool".

```
POST https://{{service-name}}.search.windows.net/indexes/hotel-rooms-sample/docs/search?api-version=2025-09-01
{
"queryType": "simple",
"search": "budget hotel +pool",
"searchMode": "all"
}
```


The `searchMode`

parameter is relevant in this example. Whenever boolean operators are on the query, you should generally set `searchMode=all`

to ensure that *all* of the criteria are matched. Otherwise, you can use the default `searchMode=any`

that favors recall over precision.

For more examples, see [Simple query syntax examples](search-query-simple-examples). For details about the query request and parameters, see [Search Documents (REST API)](/en-us/rest/api/searchservice/documents/search-post).

## Keyword search on terms and phrases

Strings passed to the `search`

parameter can include terms or phrases in any supported language, boolean operators, precedence operators, wildcard or prefix characters for "starts with" queries, escape characters, and URL encoding characters. The `search`

parameter is optional. Unspecified, search (`search=*`

or `search=" "`

) returns the top 50 documents in arbitrary (unranked) order.

A

*term search*is a query of one or more terms, where any of the terms are considered a match.A

*phrase search*is an exact phrase enclosed in quotation marks`" "`

. For example, while`Roach Motel`

(without quotes) would search for documents containing`Roach`

and/or`Motel`

anywhere in any order,`"Roach Motel"`

(with quotes) will only match documents that contain that whole phrase together and in that order (lexical analysis still applies).

Depending on your search client, you might need to escape the quotation marks in a phrase search. For example, in a POST request, a phrase search on `"Roach Motel"`

in the request body might be specified as `"\"Roach Motel\""`

. If you're using the Azure SDKs, the search client escapes the quotation marks when it serializes the search text. Your search phrase can be sent be as "Roach Motel".

By default, all strings passed in the `search`

parameter undergo lexical analysis. Make sure you understand the tokenization behavior of the analyzer you're using. Often, when query results are unexpected, the reason can be traced to how terms are tokenized at query time. You can [test tokenization on specific strings](/en-us/rest/api/searchservice/indexes/analyze) to confirm the output.

Any text input with one or more terms is considered a valid starting point for query execution. Azure AI Search will match documents containing any or all of the terms, including any variations found during analysis of the text.

As straightforward as this sounds, there's one aspect of query execution in Azure AI Search that *might* produce unexpected results, increasing rather than decreasing search results as more terms and operators are added to the input string. Whether this expansion actually occurs depends on the inclusion of a NOT operator, combined with a `searchMode`

parameter setting that determines how NOT is interpreted in terms of `AND`

or `OR`

behaviors. For more information, see the `NOT`

operator under [Boolean operators](#boolean-operators).

## Boolean operators

You can embed Boolean operators in a query string to improve the precision of a match. In the simple syntax, boolean operators are character-based. Text operators, such as the word AND, aren't supported.

| Character | Example | Usage |
|---|---|---|
`+` |
`pool + ocean` |
An `AND` operation. For example, `pool + ocean` stipulates that a document must contain both terms. |
`|` |
`pool | ocean` |
An `OR` operation finds a match when either term is found. In the example, the query engine will return a match on documents containing either `pool` or `ocean` or both. Because `OR` is the default conjunction operator, you could also leave it out, such that `pool ocean` is the equivalent of `pool | ocean` . |
`-` |
`pool – ocean` |
A `NOT` operation returns matches on documents that exclude the term. The `searchMode` parameter on a query request controls whether a term with the `NOT` operator is `AND` ed or `OR` ed with other terms in the query (assuming there's no boolean operators on the other terms). Valid values include `any` or `all` . `searchMode=any` increases the recall of queries by including more results, and by default `-` will be interpreted as "OR NOT". For example, `pool - ocean` will match documents that either contain the term `pool` or those that don't contain the term `ocean` . `searchMode=all` increases the precision of queries by including fewer results, and by default `-` will be interpreted as "AND NOT". For example, with `searchMode=any` , the query `pool - ocean` will match documents that contain the term "pool" and all documents that don't contain the term "ocean". This is arguably a more intuitive behavior for the `-` operator. Therefore, you should consider using `searchMode=all` instead of `searchMode=any` if you want to optimize searches for precision instead of recall, and Your users frequently use the `-` operator in searches. When deciding on a `searchMode` setting, consider the user interaction patterns for queries in various applications. Users who are searching for information are more likely to include an operator in a query, as opposed to e-commerce sites that have more built-in navigation structures. |

## Prefix queries

For "starts with" queries, add a suffix operator (`*`

) as the placeholder for the remainder of a term. A prefix query must begin with at least one plain text character before you can add the suffix operator.

| Character | Example | Usage |
|---|---|---|
`*` |
`lingui*` will match on "linguistic" or "linguini" |
The asterisk (`*` ) represents one or more characters of arbitrary length, ignoring case. |

Similar to filters, a prefix query looks for an exact match. As such, there's no relevance scoring (all results receive a search score of 1.0). Be aware that prefix queries can be slow, especially if the index is large and the prefix consists of a small number of characters. An alternative methodology, such as edge n-gram tokenization, might perform faster. Terms using prefix search can't be longer than 1000 characters.

Simple syntax supports prefix matching only. For suffix or infix matching against the end or middle of a term, use the [full Lucene syntax for wildcard search](query-lucene-syntax#bkmk_wildcard).

## Escaping search operators

In the simple syntax, search operators include these characters: `+ | " ( ) ' \`


If any of these characters are part of a token in the index, escape it by prefixing it with a single backslash (`\`

) in the query. For example, suppose you used a custom analyzer for whole term tokenization, and your index contains the string "Luxury+Hotel". To get an exact match on this token, insert an escape character: `search=luxury\+hotel`

.

To make things simple for the more typical cases, there are two exceptions to this rule where escaping isn't needed:

The NOT operator

`-`

only needs to be escaped if it's the first character after a whitespace. If the`-`

appears in the middle (for example, in`3352CDD0-EF30-4A2E-A512-3B30AF40F3FD`

), you can skip escaping.The suffix operator

`*`

only needs to be escaped if it's the last character before a whitespace. If the`*`

appears in the middle (for example, in`4*4=16`

), no escaping is needed.

Note

By default, the standard analyzer will delete and break words on hyphens, whitespace, ampersands, and other characters during [lexical analysis](search-lucene-query-architecture#stage-2-lexical-analysis). If you require special characters to remain in the query string, you might need an analyzer that preserves them in the index. Some choices include Microsoft natural [language analyzers](index-add-language-analyzers), which preserves hyphenated words, or a custom analyzer for more complex patterns. For more information, see [Partial terms, patterns, and special characters](search-query-partial-matching).

## Encoding unsafe and reserved characters in URLs

Ensure all unsafe and reserved characters are encoded in a URL. For example, '#' is an unsafe character because it's a fragment/anchor identifier in a URL. The character must be encoded to `%23`

if used in a URL. '&' and '=' are examples of reserved characters as they delimit parameters and specify values in Azure AI Search. For more information, see [RFC1738: Uniform Resource Locators (URL)](https://www.ietf.org/rfc/rfc1738.txt).

Unsafe characters are `" ` < > # % { } | \ ^ ~ [ ]`

. Reserved characters are `; / ? : @ = + &`

.

## Special characters

Special characters can range from currency symbols like '$' or '€', to emojis. Many analyzers, including the default standard analyzer, will exclude special characters during indexing, which means they won't be represented in your index.

If you need special character representation, you can assign an analyzer that preserves them:

The whitespace analyzer considers any character sequence separated by white spaces as tokens (so the '❤' emoji would be considered a token).

A

[language analyzer](search-language-support), such as the Microsoft English analyzer (`en.microsoft`

), would take the '$' or '€' string as a token.

For confirmation, you can [test an analyzer](/en-us/rest/api/searchservice/indexes/analyze) to see what tokens are generated for a given string. As you might expect, you might not get full tokenization from a single analyzer. A workaround is to create multiple fields that contain the same content, but with different analyzer assignments (for example, `description_en`

, `description_fr`

, and so forth for language analyzers).

When using Unicode characters, make sure symbols are properly escaped in the query url (for instance for '❤' would use the escape sequence `%E2%9D%A4+`

). Some web clients do this translation automatically.

## Precedence (grouping)

You can use parentheses to create subqueries, including operators within the parenthetical statement. For example, `motel+(wifi|luxury)`

will search for documents containing the "motel" term and either "wifi" or "luxury" (or both).

## Query size limits

If your application generates search queries programmatically, we recommend designing it in such a way that it doesn't generate queries of unbounded size.

For GET, the length of the URL can't exceed 8 KB.

For POST (and any other request), where the body of the request includes

`search`

and other parameters such as`filter`

and`orderby`

, the maximum size is 16 MB. Additional limits include:- The maximum length of the search clause is 100,000 characters.
- The maximum number of clauses in
`search`

(expressions separated by AND or OR) is 1024. - The maximum search term size is 1000 characters for
[prefix search](#prefix-queries). - There's also a limit of approximately 32 KB on the size of any individual term in a query.


For more information on query limits, see [API request limits](search-limits-quotas-capacity#api-request-limits).

## Next steps

If you'll be constructing queries programmatically, review [Full text search in Azure AI Search](search-lucene-query-architecture) to understand the stages of query processing and the implications of text analysis.

You can also review the following articles to learn more about query construction:
