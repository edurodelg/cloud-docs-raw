---
merged_at: 2026-01-25T02:11:58.421686
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index-add-language-analyzers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/index-add-language-analyzers -->

# Add language analyzers to string fields in an Azure AI Search index

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A *language analyzer* is a specific type of [text analyzer](search-analyzers) that performs lexical analysis using the linguistic rules of the target language. Every searchable string field has an **analyzer** property. If your content consists of translated strings, such as separate fields for English and Chinese text, you could specify language analyzers on each field to access the rich linguistic capabilities of those analyzers.

## When to use a language analyzer

You should consider a language analyzer in classic search workflows that don't include large language models and their awareness of linguistic rules and multilingual content.

In class search, you might add a language analyzer when awareness of word or sentence structure adds value to text parsing. A common example is the association of irregular verb forms ("bring" and "brought) or plural nouns ("mice" and "mouse"). Without linguistic awareness, these strings are parsed on physical characteristics alone, which fails to catch the connection. Since large chunks of text are more likely to have this content, fields consisting of descriptions, reviews, or summaries are good candidates for a language analyzer.

You might also consider language analyzers when content consists of non-Western language strings. While the [default analyzer (Standard Lucene)](search-analyzers#default-analyzer) is language-agnostic, the concept of using spaces and special characters (hyphens and slashes) to separate strings is more applicable to Western languages than non-Western ones.

For example, in Chinese, Japanese, Korean (CJK), and other Asian languages, a space isn't necessarily a word delimiter. Consider the following Japanese string. Because it has no spaces, a language-agnostic analyzer would likely analyze the entire string as one token, when in fact the string is actually a phrase.

```
これは私たちの銀河系の中ではもっとも重く明るいクラスの球状星団です。
(This is the heaviest and brightest group of spherical stars in our galaxy.)
```


For the example above, a successful query would have to include the full token, or a partial token using a suffix wildcard, resulting in an unnatural and limiting search experience.

A better experience is to search for individual words: 明るい (Bright), 私たちの (Our), 銀河系 (Galaxy). Using one of the Japanese analyzers available in Azure AI Search is more likely to unlock this behavior because those analyzers are better equipped at splitting the chunk of text into meaningful words in the target language.

## Comparing Lucene and Microsoft Analyzers

Azure AI Search supports 35 language analyzers backed by Lucene, and 50 language analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.

Some developers might prefer the open-source solution of Lucene. Lucene language analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finnish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers). If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit. You can use [Analyze API](/en-us/rest/api/searchservice/indexes/analyze) to see the tokens generated from a given text using a specific analyzer.

Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language. Search performance shouldn't be significantly affected for average size queries.

### English analyzers

The default analyzer is Standard Lucene, which works well for English, but perhaps not as well as Lucene's English analyzer or Microsoft's English analyzer.

Lucene's English analyzer extends the Standard analyzer. It removes possessives (trailing 's) from words, applies stemming as per Porter Stemming algorithm, and removes English stop words.

Microsoft's English analyzer performs lemmatization instead of stemming. This means it can handle inflected and irregular word forms much better which results in more relevant search results.


## How to specify a language analyzer

Set the analyzer during index creation before it's loaded with data.

In the field definition, make sure the field is attributed as "searchable" and is of type Edm.String.

Set the "analyzer" property to one of the language analyzers from the

[supported analyzers list](#language-analyzer-list).The "analyzer" property is the only property that will accept a language analyzer, and it's used for both indexing and queries. Other analyzer-related properties ("searchAnalyzer" and "indexAnalyzer") won't accept a language analyzer.


Language analyzers can't be customized. If an analyzer isn't meeting your requirements, create a [custom analyzer](cognitive-search-working-with-skillsets) with the microsoft_language_tokenizer or microsoft_language_stemming_tokenizer, and then add filters for pre- and post-tokenization processing.

The following example illustrates a language analyzer specification in an index:

```
{
"name": "hotels-sample-index",
"fields": [
{
"name": "Description",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": "en.microsoft",
"indexAnalyzer": null,
"searchAnalyzer": null
},
{
"name": "Description_fr",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": "fr.microsoft",
"indexAnalyzer": null,
"searchAnalyzer": null
},
```


For more information about creating an index and setting field properties, see [Create Index (REST)](/en-us/rest/api/searchservice/indexes/create). For more information about text analysis, see [Analyzers in Azure AI Search](search-analyzers).

## Supported language analyzers

Below is the list of supported languages, with Lucene and Microsoft analyzer names.

| Language | Microsoft Analyzer Name | Lucene Analyzer Name |
|---|---|---|
| Arabic | ar.microsoft | ar.lucene |
| Armenian | hy.lucene | |
| Bangla | bn.microsoft | |
| Basque | eu.lucene | |
| Bulgarian | bg.microsoft | bg.lucene |
| Catalan | ca.microsoft | ca.lucene |
| Chinese Simplified | zh-Hans.microsoft | zh-Hans.lucene |
| Chinese Traditional | zh-Hant.microsoft | zh-Hant.lucene |
| Croatian | hr.microsoft | |
| Czech | cs.microsoft | cs.lucene |
| Danish | da.microsoft | da.lucene |
| Dutch | nl.microsoft | nl.lucene |
| English | en.microsoft | en.lucene |
| Estonian | et.microsoft | |
| Finnish | fi.microsoft | fi.lucene |
| French | fr.microsoft | fr.lucene |
| Galician | gl.lucene | |
| German | de.microsoft | de.lucene |
| Greek | el.microsoft | el.lucene |
| Gujarati | gu.microsoft | |
| Hebrew | he.microsoft | |
| Hindi | hi.microsoft | hi.lucene |
| Hungarian | hu.microsoft | hu.lucene |
| Icelandic | is.microsoft | |
| Indonesian (Bahasa) | id.microsoft | id.lucene |
| Irish | ga.lucene | |
| Italian | it.microsoft | it.lucene |
| Japanese | ja.microsoft | ja.lucene |
| Kannada | kn.microsoft | |
| Korean | ko.microsoft | ko.lucene |
| Latvian | lv.microsoft | lv.lucene |
| Lithuanian | lt.microsoft | |
| Malayalam | ml.microsoft | |
| Malay (Latin) | ms.microsoft | |
| Marathi | mr.microsoft | |
| Norwegian | nb.microsoft | no.lucene |
| Persian | fa.lucene | |
| Polish | pl.microsoft | pl.lucene |
| Portuguese (Brazil) | pt-Br.microsoft | pt-Br.lucene |
| Portuguese (Portugal) | pt-Pt.microsoft | pt-Pt.lucene |
| Punjabi | pa.microsoft | |
| Romanian | ro.microsoft | ro.lucene |
| Russian | ru.microsoft | ru.lucene |
| Serbian (Cyrillic) | sr-cyrillic.microsoft | |
| Serbian (Latin) | sr-latin.microsoft | |
| Slovak | sk.microsoft | |
| Slovenian | sl.microsoft | |
| Spanish | es.microsoft | es.lucene |
| Swedish | sv.microsoft | sv.lucene |
| Tamil | ta.microsoft | |
| Telugu | te.microsoft | |
| Thai | th.microsoft | th.lucene |
| Turkish | tr.microsoft | tr.lucene |
| Ukrainian | uk.microsoft | |
| Urdu | ur.microsoft | |
| Vietnamese | vi.microsoft |

All analyzers with names annotated with **Lucene** are powered by [Apache Lucene's language analyzers](https://lucene.apache.org/core/6_6_1/core/overview-summary.html).


---

<!-- DOCUMENTO FUSIONADO: search-indexer-howto-access-ip-restricted.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-howto-access-ip-restricted -->

# Configure IP firewall rules to allow indexer connections from Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search makes external, outbound calls during indexer processing for content and skills, and for agentic retrieval requests that include calls to large language models (LLMs). If the target Azure resource uses IP firewall rules to filter incoming calls, you must create an inbound rule in your firewall that admits requests from Azure AI Search.

This article explains how to find the IP address of your search service and configure an inbound IP rule on an Azure Storage account. While specific to Azure Storage, this approach also works for other Azure resources that use IP firewall rules for data access, such as Azure Cosmos DB and Azure SQL.

## Prerequisites

[Azure AI Search service](search-create-service-portal)(Basic tier or higher). You can't set firewall rules on the Free tier.- An existing target Azure resource protected by a firewall.
**Contributor**or**Owner**role on the search service.

Note

Applicable to Azure Storage only. To define IP firewall rules, your storage account and search service must be in different regions. If your setup doesn't permit different regions, try the

[trusted service exception](search-indexer-howto-access-trusted-service-exception)or[resource instance rule](/en-us/azure/storage/common/storage-network-security#grant-access-from-azure-resource-instances)instead.For private connections from indexers to any supported Azure resource, we recommend setting up a

[shared private link](search-indexer-howto-access-private). Private connections travel the Microsoft backbone network, bypassing the public internet completely.

## Get a search service IP address

Sign in to the

[Azure portal](https://portal.azure.com)and select your search service.From the left pane, select

**Overview**.Copy the fully qualified domain name (FQDN) of your search service, which should look like

`my-search-service.search.windows.net`

.Look up the IP address of the search service by performing an

`nslookup`

(or a`ping`

) of the FQDN on a command prompt. Make sure you remove the`https://`

prefix.Copy the IP address for use in the next step. In the following example, the IP address that you copy is

`150.0.0.1`

.`nslookup my-search-service.search.windows.net Server: server.example.org Address: 10.50.10.50 Non-authoritative answer: Name: <name> Address: 150.0.0.1 aliases: my-search-service.search.windows.net`

The IP address in the

`Address`

field under "Non-authoritative answer" (150.0.0.1 in this example) is the value you need for the firewall rule.

## Allow access from your client IP address

Client applications that push indexing and query requests to the search service must be represented in an IP range. On Azure, you can generally determine the IP address by pinging the FQDN of a service. For example, `ping <your-search-service-name>.search.windows.net`

returns the IP address of a search service.

Add your client IP address to allow access to the service from the Azure portal on your current computer.

In the Azure portal, select your search service.

From the left pane, select

**Settings**>**Networking**.On the

**Firewall and virtual networks**tab, set**Public network access**to**Selected IP addresses**.Under

**IP Firewall**, select**Add your client IP address**.Save your changes.


## Get the Azure portal IP address

If you're using the Azure portal or an [import wizard](search-import-data-portal) to create an indexer, you need an inbound rule for the Azure portal as well.

To get the Azure portal's IP address, perform `nslookup`

(or `ping`

) on `stamp2.ext.search.windows.net`

, which is the domain of the traffic manager. For nslookup, the IP address is visible in the "Non-authoritative answer" portion of the response.

In the following example, the IP address that you should copy is `52.252.175.48`

.

```
$ nslookup stamp2.ext.search.windows.net
Server: ZenWiFi_ET8-0410
Address: 192.168.50.1
Non-authoritative answer:
Name: azsyrie.northcentralus.cloudapp.azure.com
Address: 52.252.175.48
Aliases: stamp2.ext.search.windows.net
azs-ux-prod.trafficmanager.net
azspncuux.management.search.windows.net
```


The `Address`

field (52.252.175.48) is the Azure portal IP address for your region.

Services in different regions connect to different traffic managers. Regardless of the domain name, the IP address returned from the ping is the correct one to use when defining an inbound firewall rule for the Azure portal in your region.

For ping, the request times out, but the IP address is visible in the response. For example, in the message `Pinging azsyrie.northcentralus.cloudapp.azure.com [52.252.175.48]`

, the IP address is `52.252.175.48`

.

## Get IP addresses for "AzureCognitiveSearch" service tag

You'll also need to create an inbound rule that allows requests from the [multitenant execution environment](search-indexer-securing-resources#network-access-and-indexer-execution-environments). This environment is managed by Microsoft and it's used to offload processing intensive jobs that could otherwise overwhelm your search service. This section explains how to get the range of IP addresses needed to create this inbound rule.

An IP address range is defined for each region that supports Azure AI Search. Specify the full range to ensure the success of requests originating from the multitenant execution environment.

You can get this IP address range from the `AzureCognitiveSearch`

service tag.

Use either the

[discovery API](/en-us/azure/virtual-network/service-tags-overview#use-the-service-tag-discovery-api)or the[downloadable JSON file](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files). If the search service is the Azure Public cloud, download the[Azure Public JSON file](https://www.microsoft.com/download/details.aspx?id=56519).Open the JSON file and search for "AzureCognitiveSearch". For a search service in WestUS2, the IP addresses for the multitenant indexer execution environment are:

`{ "name": "AzureCognitiveSearch.WestUS2", "id": "AzureCognitiveSearch.WestUS2", "properties": { "changeNumber": 1, "region": "westus2", "regionId": 38, "platform": "Azure", "systemService": "AzureCognitiveSearch", "addressPrefixes": [ "20.42.129.192/26", "40.91.93.84/32", "40.91.127.116/32", "40.91.127.241/32", "51.143.104.54/32", "51.143.104.90/32", "2603:1030:c06:1::180/121" ], "networkFeatures": null } },`

Copy all IP addresses in the

`addressPrefixes`

array for your region.For IP addresses having the "/32" suffix, drop the "/32" (40.91.93.84/32 becomes 40.91.93.84 in the rule definition). All other IP addresses can be used verbatim.

Copy all of the IP addresses for the region.


## Add IP addresses to IP firewall rules

After you get the necessary IP addresses, set up the inbound rules. The easiest way to add IP address ranges to a storage account's firewall rule is through the Azure portal.

In the Azure portal, select your storage account.

From the left pane, select

**Security + networking**>**Networking**.On the

**Public access**tab, select**Manage**.Under

**Public network access scope**, select**Enable from selected networks**.Add the IP addresses you obtained previously, and then select

**Save**. You should have rules for the search service, the Azure portal (optional), and all of the IP addresses for the "AzureCognitiveSearch" service tag for your region.It can take five to ten minutes for the firewall rules to update. After the update, indexers can access storage account data behind the firewall.


## Supplement network security with token authentication

Firewalls and network security are a first step in preventing unauthorized access to data and operations. Authorization should be your next step.

We recommend role-based access, where Microsoft Entra ID users and groups are assigned to roles that determine read and write access to your service. For a description of built-in roles and instructions for creating custom roles, see [Connect to Azure AI Search using role-based access controls](search-security-rbac).

If you don't need key-based authentication, we recommend that you disable API keys and use role assignments exclusively.
