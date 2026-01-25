---
merged_at: 2026-01-25T03:18:14.107731
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-network-security-perimeter.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-network-security-perimeter -->

# Add a search service to a network security perimeter

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A [network security perimeter](/en-us/azure/private-link/network-security-perimeter-concepts) is a logical network boundary around your platform as a service (PaaS) resources that you deploy outside of a virtual network. It establishes a perimeter for controlling public network access to resources like Azure AI Search, [Azure Storage](/en-us/azure/storage/common/storage-network-security-perimeter), and [Azure OpenAI](/en-us/azure/ai-foundry/openai/how-to/network-security-perimeter).

This article explains how to join an Azure AI Search service to a network security perimeter to control network access to your search service. By joining a network security perimeter, you can:

- Log all access to your search service in context with other Azure resources in the same perimeter.
- Block any data exfiltration from a search service to other services outside the perimeter.
- Allow access to your search service by using the inbound and outbound access capabilities of the network security perimeter.

You can add a search service to a network security perimeter in the Azure portal, as described in this article. Alternatively, you can use the [Azure Virtual Network Manager REST API](/en-us/rest/api/networkmanager/) to join a search service, and use the [Search Management REST APIs](/en-us/rest/api/searchmanagement/network-security-perimeter-configurations?view=rest-searchmanagement-2025-05-01&preserve-view=true) to view and synchronize the configuration settings.

## Prerequisites

An existing network security perimeter. You can

[create one to associate with your search service](/en-us/azure/private-link/create-network-security-perimeter-portal).[Azure AI Search](search-create-service-portal), any billable tier, in any region.

## Limitations

For search services within a network security perimeter, indexers must use a

[system or user-assigned managed identity](search-how-to-managed-identities)and have a role assignment that permits read access to data sources.Supported indexer data sources are currently limited to

[Azure Blob Storage](search-how-to-index-azure-blob-storage),[Azure Cosmos DB for NoSQL](search-how-to-index-cosmosdb-sql), and[Azure SQL Database](search-how-to-index-sql-database).Currently, within the perimeter, indexer connections to Azure PaaS for data retrieval is the primary use case. For outbound skills-driven API calls to Foundry Tools, Azure OpenAI, or the Microsoft Foundry model catalog, or for inbound calls from Foundry for "chat with your data" scenarios, you must

[configure inbound and outbound rules](#add-an-inbound-access-rule)to allow the requests through the perimeter. If you require private connections for[structure-aware chunking](search-how-to-semantic-chunking)and vectorization, you should[create a shared private link](search-indexer-howto-access-private)and a private network.

## Assign a search service to a network security perimeter

By using Azure Network Security Perimeter, administrators can define a logical network isolation boundary for PaaS resources, such as Azure Storage and Azure SQL Database, that are deployed outside virtual networks. It restricts communication to resources within the perimeter, and it allows non-perimeter public traffic through inbound and outbound access rules.

You can add Azure AI Search to a network security perimeter so that all indexing and query requests occur within the security boundary.

In the Azure portal, find the network security perimeter service for your subscription.

From the left pane, select

**Settings**>**Associated resources**.Select

**Add**>**Associate resources with an existing profile**.Select the profile you created when you created the network security perimeter for

**Profile**.Select

**Add**, and then select your search service.Select

**Associate**in the lower-left corner to create the association.

### Network security perimeter access modes

Network security perimeter supports two different access modes for associated resources:

| Mode | Description |
|---|---|
| Learning mode | This is the default access mode. In learning mode, network security perimeter logs all traffic to the search service that would be denied if the perimeter was in enforced mode. This access mode allows network administrators to understand the existing access patterns of the search service before implementing enforcement of access rules. |
| Enforced mode | In enforced mode, network security perimeter logs and denies all traffic that isn't explicitly allowed by access rules. |

#### Network security perimeter and search service networking settings

The `publicNetworkAccess`

setting determines search service association with a network security perimeter.

In learning mode, the

`publicNetworkAccess`

setting controls public access to the resource.In enforced mode, the network security perimeter rules override the

`publicNetworkAccess`

setting. For example, if a search service with a`publicNetworkAccess`

setting of`enabled`

is associated with a network security perimeter in enforced mode, access to the search service is still controlled by network security perimeter access rules.

#### Change the network security perimeter access mode

Go to your network security perimeter resource in the Azure portal.

From the left pane, select

**Settings**>**Associated resources**.Find your search service in the table.

Select the three dots at the end of the row, and then select

**Change access mode**.Select your desired access mode, and then select

**Apply**.

## Enable logging network access

Go to your network security perimeter resource in the Azure portal.

From the left pane, select

**Monitoring**>**Diagnostic settings**.Select

**Add diagnostic setting**.Enter any name, such as "diagnostic," for

**Diagnostic setting name**.Under

**Logs**, select**allLogs**.**allLogs**ensures all inbound and outbound network access to resources in your network security perimeter is logged.Under

**Destination details**, select**Archive to a storage account**or**Send to Log Analytics workspace**. The storage account must be in the same region as the network security perimeter. You can either use an existing storage account or create a new one. A Log Analytics workspace can be in a different region than the one used by the network security perimeter. You can also select any of the other applicable destinations.Select

**Save**to create the diagnostic setting and start logging network access.

### Reading network access logs

#### Log Analytics workspace

The `network-security-perimeterAccessLogs`

table contains all the logs for every log category, such as `network-security-perimeterPublicInboundResourceRulesAllowed`

. Each log contains a record of the network security perimeter network access that matches the log category.

Here's an example of the `network-security-perimeterPublicInboundResourceRulesAllowed`

log format:

| Column Name | Meaning | Example Value |
|---|---|---|
| ResultDescription | Name of the network access operation. | POST /indexes/my-index/docs/search |
| Profile | Which network security perimeter the search service was associated with. | defaultProfile |
| ServiceResourceId | Resource ID of the search service. | `search-service-resource-id` |
| Matched Rule | JSON description of the rule that the log matched. | `{ "accessRule": "IP firewall" }` |
| SourceIPAddress | Source IP of the inbound network access, if applicable. | 1.1.1.1 |
| AccessRuleVersion | Version of the network-security-perimeter access rules used to enforce the network access rules. | 0 |

#### Storage Account

The storage account has containers for every log category, such as `insights-logs-network-security-perimeterpublicinboundperimeterrulesallowed`

. The folder structure inside the container matches the resource ID of the network security perimeter and the time the logs were taken. Each line on the JSON log file contains a record of the network security perimeter network access that matches the log category.

For example, the inbound perimeter rules allowed category log uses the following format:

```
"properties": {
"ServiceResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/network-security-perimeter/providers/Microsoft.Search/searchServices/network-security-perimeter-search",
"Profile": "defaultProfile",
"MatchedRule": {
"AccessRule": "myaccessrule"
},
"Source": {
"IpAddress": "255.255.255.255",
}
}
```


## Add an access rule for your search service

A network security perimeter profile specifies rules that allow or deny access through the perimeter.

Within the perimeter, all resources have mutual access at the network level. You must still set up authentication and authorization, but at the network level, connection requests from inside the perimeter are accepted.

For resources outside of the network security perimeter, you must specify inbound and outbound access rules. Inbound rules specify which connections to allow in, and outbound rules specify which requests are allowed out.

A search service accepts inbound requests from apps like the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs), Azure Machine Learning prompt flow, and any app that sends indexing or query requests. A search service sends outbound requests during indexer-based indexing and skillset execution. This section explains how to set up inbound and outbound access rules for Azure AI Search scenarios.

Note

When you authenticate access by using [managed identities and role assignments](/en-us/entra/identity/managed-identities-azure-resources/overview), any service associated with a network security perimeter implicitly allows inbound and outbound access to any other service associated with the same network security perimeter. You only need to create access rules when you allow access outside of the network security perimeter or for access authenticated by using API keys.

### Add an inbound access rule

Inbound access rules can allow the internet and resources outside the perimeter to connect with resources inside the perimeter.

Network security perimeter supports two types of inbound access rules:

IP address ranges. IP addresses or ranges must be in the Classless Inter-Domain Routing (CIDR) format. An example of CIDR notation is 192.0.2.0/24, which represents the IPs that range from 192.0.2.0 to 192.0.2.255. This type of rule allows inbound requests from any IP address within the range.

Subscriptions. This type of rule allows inbound access authenticated by using any managed identity from the subscription.


To add an inbound access rule in the Azure portal:

Go to your network security perimeter resource in the Azure portal.

From the left pane, select

**Settings**>**Profiles**.Select the profile you're using with your network security perimeter.

From the left pane, select

**Settings**>**Inbound access rules**.Select

**Add**.Enter or select the following values:

Setting Value Rule name The name for the inbound access rule, such as `MyInboundAccessRule`

.Source type Valid values are **IP address ranges**or**Subscriptions**.Allowed sources If you selected **IP address ranges**, enter the IP address range in CIDR format that you want to allow inbound access from. Azure IP ranges are available at[this link](https://www.microsoft.com/download/details.aspx?id=56519). If you selected**Subscriptions**, use the subscription you want to allow inbound access from.Select

**Add**to create the inbound access rule.

### Add an outbound access rule

A search service makes outbound calls during indexer-based indexing and skillset execution. If your indexer data sources, Foundry Tools, or custom skill logic is outside of the network security perimeter, you should create an outbound access rule that allows your search service to make the connection.

Currently, Azure AI Search can only connect to Azure Storage or Azure Cosmos DB within the security perimeter. If your indexers use other data sources, you need an outbound access rule to support that connection.

The network security perimeter supports outbound access rules based on the Fully Qualified Domain Name (FQDN) of the destination. For example, you can allow outbound access from any service associated with your network security perimeter to an FQDN such as `mystorageaccount.blob.core.windows.net`

.

To add an outbound access rule in the Azure portal:

Go to your network security perimeter resource in the Azure portal.

From the left pane, select

**Settings**>**Profiles**.Select the profile you're using with your network security perimeter.

From the left pane, select

**Settings**>**Outbound access rules**.Select

**Add**.Enter or select the following values:

Setting Value Rule name The name for the outbound access rule, such as "MyOutboundAccessRule." Destination type Leave as **FQDN**.Allowed destinations Enter a comma-separated list of FQDNs you want to allow outbound access to. Select

**Add**to create the outbound access rule.

## Test your connection through network security perimeter

To test your connection through network security perimeter, you need access to a web browser, either on a local computer with an internet connection or an Azure VM.

Change your network security perimeter association to

[enforced mode](#network-security-perimeter-access-modes)to start enforcing network security perimeter requirements for network access to your search service.Decide if you want to use a local computer or an Azure VM.

- If you're using a local computer, you need to know your public IP address.
- If you're using an Azure VM, you can either use
[private link](/en-us/azure/private-link/private-link-overview)or[check the IP address using the Azure portal](/en-us/azure/virtual-network/ip-services/virtual-network-network-interface-addresses).

Using the IP address, create an

[inbound access rule](#add-an-inbound-access-rule)for that IP address to allow access. You can skip this step if you're using private link.Finally, try navigating to the search service in the Azure portal. If you can view the indexes successfully, then the network security perimeter is configured correctly.


## View and manage network security perimeter configuration

Use the [Network Security Perimeter Configuration REST APIs](/en-us/rest/api/searchmanagement/network-security-perimeter-configurations?view=rest-searchmanagement-2025-05-01&preserve-view=true) to review and reconcile perimeter configurations.

Be sure to use the 2025-05-01 REST API version, which is the latest stable version of the Search Management REST APIs. For more information, see [Manage your Azure AI Search service using REST APIs](search-manage-rest).


---

<!-- DOCUMENTO FUSIONADO: search-query-troubleshoot-collection-filters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-troubleshoot-collection-filters -->

# Troubleshooting OData collection filters in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To [filter](query-odata-filter-orderby-syntax) on collection fields in Azure AI Search, you can use the [ any and all operators](search-query-odata-collection-operators) together with


**lambda expressions**. A lambda expression is a subfilter that is applied to each element of a collection.

Not every feature of filter expressions is available inside a lambda expression. Which features are available differs depending on the data type of the collection field that you want to filter. This can result in an error if you try to use a feature in a lambda expression that isn't supported in that context. If you're encountering such errors while trying to write a complex filter over collection fields, this article will help you troubleshoot the problem.

## Common collection filter errors

The following table lists errors that you might encounter when trying to execute a collection filter. These errors happen when you use a feature of filter expressions that isn't supported inside a lambda expression. Each error gives some guidance on how you can rewrite your filter to avoid the error. The table also includes a link to the relevant section of this article that provides more information on how to avoid that error.

| Error message | Situation | Details |
|---|---|---|
The function `ismatch` has no parameters bound to the range variable 's'. Only bound field references are supported inside lambda expressions ('any' or 'all'). However, you can change your filter so that the `ismatch` function is outside the lambda expression and try again. |
Using `search.ismatch` or `search.ismatchscoring` inside a lambda expression |
|

`Collection(Edm.String)`

[Rules for filtering string collections](#bkmk_strings)`(a and b) or (c and d)`

where a, b, c, and d are comparison or equality subexpressions. For 'all', use expressions that are 'ANDs of ORs', also known as Conjunctive Normal Form. For example: `(a or b) and (c or d)`

where a, b, c, and d are comparison or inequality subexpressions. Examples of comparison expressions: 'x gt 5', 'x le 2'. Example of an equality expression: 'x eq 5'. Example of an inequality expression: 'x ne 5'.`Collection(Edm.DateTimeOffset)`

, `Collection(Edm.Double)`

, `Collection(Edm.Int32)`

, or `Collection(Edm.Int64)`

[Rules for filtering comparable collections](#bkmk_comparables)`Collection(Edm.GeographyPoint)`

[Rules for filtering GeographyPoint collections](#bkmk_geopoints)`Collection(Edm.String)`

or `Collection(Edm.GeographyPoint)`

[Rules for filtering string collections](#bkmk_strings)[Rules for filtering GeographyPoint collections](#bkmk_geopoints)`Collection(Edm.String)`

[Rules for filtering string collections](#bkmk_strings)## How to write valid collection filters

The rules for writing valid collection filters are different for each data type. The following sections describe the rules by showing examples of which filter features are supported and which aren't:

[Rules for filtering string collections](#bkmk_strings)[Rules for filtering Boolean collections](#bkmk_bools)[Rules for filtering GeographyPoint collections](#bkmk_geopoints)[Rules for filtering comparable collections](#bkmk_comparables)[Rules for filtering complex collections](#bkmk_complex)

## Rules for filtering string collections

Inside lambda expressions for string collections, the only comparison operators that can be used are `eq`

and `ne`

.

Note

Azure AI Search does not support the `lt`

/`le`

/`gt`

/`ge`

operators for strings, whether inside or outside a lambda expression.

The body of an `any`

can only test for equality while the body of an `all`

can only test for inequality.

It's also possible to combine multiple expressions via `or`

in the body of an `any`

, and via `and`

in the body of an `all`

. Since the `search.in`

function is equivalent to combining equality checks with `or`

, it's also allowed in the body of an `any`

. Conversely, `not search.in`

is allowed in the body of an `all`

.

For example, these expressions are allowed:

`tags/any(t: t eq 'books')`

`tags/any(t: search.in(t, 'books, games, toys'))`

`tags/all(t: t ne 'books')`

`tags/all(t: not (t eq 'books'))`

`tags/all(t: not search.in(t, 'books, games, toys'))`

`tags/any(t: t eq 'books' or t eq 'games')`

`tags/all(t: t ne 'books' and not (t eq 'games'))`


While these expressions aren't allowed:

`tags/any(t: t ne 'books')`

`tags/any(t: not search.in(t, 'books, games, toys'))`

`tags/all(t: t eq 'books')`

`tags/all(t: search.in(t, 'books, games, toys'))`

`tags/any(t: t eq 'books' and t ne 'games')`

`tags/all(t: t ne 'books' or not (t eq 'games'))`


## Rules for filtering Boolean collections

The type `Edm.Boolean`

supports only the `eq`

and `ne`

operators. As such, it doesn’t make much sense to allow combining such clauses that check the same range variable with `and`

/`or`

since that would always lead to tautologies or contradictions.

Here are some examples of filters on Boolean collections that are allowed:

`flags/any(f: f)`

`flags/all(f: f)`

`flags/any(f: f eq true)`

`flags/any(f: f ne true)`

`flags/all(f: not f)`

`flags/all(f: not (f eq true))`


Unlike string collections, Boolean collections have no limits on which operator can be used in which type of lambda expression. Both `eq`

and `ne`

can be used in the body of `any`

or `all`

.

Expressions such as the following aren't allowed for Boolean collections:

`flags/any(f: f or not f)`

`flags/any(f: f or f)`

`flags/all(f: f and not f)`

`flags/all(f: f and f eq true)`


## Rules for filtering GeographyPoint collections

Values of type `Edm.GeographyPoint`

in a collection can’t be compared directly to each other. Instead, they must be used as parameters to the `geo.distance`

and `geo.intersects`

functions. The `geo.distance`

function in turn must be compared to a distance value using one of the comparison operators `lt`

, `le`

, `gt`

, or `ge`

. These rules also apply to noncollection Edm.GeographyPoint fields.

Like string collections, `Edm.GeographyPoint`

collections have some rules for how the geo-spatial functions can be used and combined in the different types of lambda expressions:

- Which comparison operators you can use with the
`geo.distance`

function depends on the type of lambda expression. For`any`

, you can use only`lt`

or`le`

. For`all`

, you can use only`gt`

or`ge`

. You can negate expressions involving`geo.distance`

, but you have to change the comparison operator (`geo.distance(...) lt x`

becomes`not (geo.distance(...) ge x)`

and`geo.distance(...) le x`

becomes`not (geo.distance(...) gt x)`

). - In the body of an
`all`

, the`geo.intersects`

function must be negated. Conversely, in the body of an`any`

, the`geo.intersects`

function must not be negated. - In the body of an
`any`

, geo-spatial expressions can be combined using`or`

. In the body of an`all`

, such expressions can be combined using`and`

.

The above limitations exist for similar reasons as the equality/inequality limitation on string collections. See [Understanding OData collection filters in Azure AI Search](search-query-understand-collection-filters) for a deeper look at these reasons.

Here are some examples of filters on `Edm.GeographyPoint`

collections that are allowed:

`locations/any(l: geo.distance(l, geography'POINT(-122 49)') lt 10)`

`locations/any(l: not (geo.distance(l, geography'POINT(-122 49)') ge 10) or geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`

`locations/all(l: geo.distance(l, geography'POINT(-122 49)') ge 10 and not geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`


Expressions such as the following aren't allowed for `Edm.GeographyPoint`

collections:

`locations/any(l: l eq geography'POINT(-122 49)')`

`locations/any(l: not geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`

`locations/all(l: geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`

`locations/any(l: geo.distance(l, geography'POINT(-122 49)') gt 10)`

`locations/all(l: geo.distance(l, geography'POINT(-122 49)') lt 10)`

`locations/any(l: geo.distance(l, geography'POINT(-122 49)') lt 10 and geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`

`locations/all(l: geo.distance(l, geography'POINT(-122 49)') le 10 or not geo.intersects(l, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))`


## Rules for filtering comparable collections

This section applies to all the following data types:

`Collection(Edm.DateTimeOffset)`

`Collection(Edm.Double)`

`Collection(Edm.Int32)`

`Collection(Edm.Int64)`


Types such as `Edm.Int32`

and `Edm.DateTimeOffset`

support all six of the comparison operators: `eq`

, `ne`

, `lt`

, `le`

, `gt`

, and `ge`

. Lambda expressions over collections of these types can contain simple expressions using any of these operators. This applies to both `any`

and `all`

. For example, these filters are allowed:

`ratings/any(r: r ne 5)`

`dates/any(d: d gt 2017-08-24T00:00:00Z)`

`not margins/all(m: m eq 3.5)`


However, there are limitations on how such comparison expressions can be combined into more complex expressions inside a lambda expression:

- Rules for
`any`

:Simple inequality expressions can't be usefully combined with any other expressions. For example, this expression is allowed:

`ratings/any(r: r ne 5)`


but this expression isn't:

`ratings/any(r: r ne 5 and r gt 2)`


and while this expression is allowed, it isn't useful because the conditions overlap:

`ratings/any(r: r ne 5 or r gt 7)`


Simple comparison expressions involving

`eq`

,`lt`

,`le`

,`gt`

, or`ge`

can be combined with`and`

/`or`

. For example:`ratings/any(r: r gt 2 and r le 5)`

`ratings/any(r: r le 5 or r gt 7)`


Comparison expressions combined with

`and`

(conjunctions) can be further combined using`or`

. This form is known in Boolean logic as "[Disjunctive Normal Form](https://en.wikipedia.org/wiki/Disjunctive_normal_form)" (DNF). For example:`ratings/any(r: (r gt 2 and r le 5) or (r gt 7 and r lt 10))`


- Rules for
`all`

:Simple equality expressions can't be usefully combined with any other expressions. For example, this expression is allowed:

`ratings/all(r: r eq 5)`


but this expression isn't:

`ratings/all(r: r eq 5 or r le 2)`


and while this expression is allowed, it isn't useful because the conditions overlap:

`ratings/all(r: r eq 5 and r le 7)`


Simple comparison expressions involving

`ne`

,`lt`

,`le`

,`gt`

, or`ge`

can be combined with`and`

/`or`

. For example:`ratings/all(r: r gt 2 and r le 5)`

`ratings/all(r: r le 5 or r gt 7)`


Comparison expressions combined with

`or`

(disjunctions) can be further combined using`and`

. This form is known in Boolean logic as "[Conjunctive Normal Form](https://en.wikipedia.org/wiki/Conjunctive_normal_form)" (CNF). For example:`ratings/all(r: (r le 2 or gt 5) and (r lt 7 or r ge 10))`


## Rules for filtering complex collections

Lambda expressions over complex collections support a much more flexible syntax than lambda expressions over collections of primitive types. You can use any filter construct inside such a lambda expression that you can use outside one, with only two exceptions.

First, the functions `search.ismatch`

and `search.ismatchscoring`

aren't supported inside lambda expressions. For more information, see [Understanding OData collection filters in Azure AI Search](search-query-understand-collection-filters).

Second, referencing fields that aren't *bound* to the range variable (so-called *free variables*) isn't allowed. For example, consider the following two equivalent OData filter expressions:

`stores/any(s: s/amenities/any(a: a eq 'parking')) and details/margin gt 0.5`

`stores/any(s: s/amenities/any(a: a eq 'parking' and details/margin gt 0.5))`


The first expression is allowed, while the second form is rejected because `details/margin`

isn't bound to the range variable `s`

.

This rule also extends to expressions that have variables bound in an outer scope. Such variables are free with respect to the scope in which they appear. For example, the first expression is allowed, while the second equivalent expression isn't allowed because `s/name`

is free with respect to the scope of the range variable `a`

:

`stores/any(s: s/amenities/any(a: a eq 'parking') and s/name ne 'Flagship')`

`stores/any(s: s/amenities/any(a: a eq 'parking' and s/name ne 'Flagship'))`


This limitation shouldn't be a problem in practice since it's always possible to construct filters such that lambda expressions contain only bound variables.

## Cheat sheet for collection filter rules

The following table summarizes the rules for constructing valid filters for each collection data type.

| Data type | Features allowed in lambda expressions with `any` |
Features allowed in lambda expressions with `all` |
|---|---|---|
`Collection(Edm.ComplexType)` |
Everything except `search.ismatch` and `search.ismatchscoring` |
Same |
`Collection(Edm.String)` |
Comparisons with `eq` or `search.in` Combining sub-expressions with `or` |
Comparisons with `ne` or `not search.in()` Combining sub-expressions with `and` |
`Collection(Edm.Boolean)` |
Comparisons with `eq` or `ne` |
Same |
`Collection(Edm.GeographyPoint)` |
Using `geo.distance` with `lt` or `le` `geo.intersects` Combining sub-expressions with `or` |
Using `geo.distance` with `gt` or `ge` `not geo.intersects(...)` Combining sub-expressions with `and` |
`Collection(Edm.DateTimeOffset)` , `Collection(Edm.Double)` , `Collection(Edm.Int32)` , `Collection(Edm.Int64)` |
Comparisons using `eq` , `ne` , `lt` , `gt` , `le` , or `ge` Combining comparisons with other sub-expressions using `or` Combining comparisons except `ne` with other sub-expressions using `and` Expressions using combinations of `and` and `or` in
|
Comparisons using `eq` , `ne` , `lt` , `gt` , `le` , or `ge` Combining comparisons with other sub-expressions using `and` Combining comparisons except `eq` with other sub-expressions using `or` Expressions using combinations of `and` and `or` in
|

For examples of how to construct valid filters for each case, see [How to write valid collection filters](#bkmk_examples).

If you write filters often, and understanding the rules from first principles would help you more than just memorizing them, see [Understanding OData collection filters in Azure AI Search](search-query-understand-collection-filters).
