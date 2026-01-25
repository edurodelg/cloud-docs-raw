---
merged_at: 2026-01-25T03:18:13.740900
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-entity-linking-v3.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-entity-linking-v3 -->

# Entity Linking cognitive skill (v3)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Entity Linking** skill (v3) returns a list of recognized entities with links to articles in a well-known knowledge base (Wikipedia).

Note

This skill is bound to the [Entity Linking](/en-us/azure/ai-services/language-service/entity-linking/overview) machine learning models in [Azure Vision in Foundry Tools](/en-us/azure/ai-services/language-service/overview). It requires a [billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.V3.EntityLinkingSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the EntityLinking skill, consider using the

[Text Split skill](cognitive-search-skill-textsplit). If you do use a text split skill, set the page length to 5000 for the best performance.

## Skill parameters

Parameter names are case-sensitive and are all optional.

| Parameter name | Description |
|---|---|
`defaultLanguageCode` |
Language code of the input text. If the default language code isn't specified, English (en) is used as the default language code. See the
|
`minimumPrecision` |
A value between 0 and 1. If the confidence score (in the `entities` output) is lower than this value, the entity isn't returned. The default is 0. |
`modelVersion` |
(Optional) Specifies the
|

## Skill inputs

| Input name | Description |
|---|---|
`languageCode` |
A string indicating the language of the records. If this parameter isn't specified, the default language code is used to analyze the records. See the
|
`text` |
The text to analyze. |

## Skill outputs

| Output name | Description |
|---|---|
`entities` |
An array of complex types that contains the following fields:
|

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityLinkingSkill",
"context": "/document",
"defaultLanguageCode": "en",
"minimumPrecision": 0.5,
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/language"
}
],
"outputs": [
{
"name": "entities",
"targetName": "entities"
}
]
}
```


## Sample input

```
{
"values": [
{
"recordId": "1",
"data":
{
"text": "Microsoft is liked by many.",
"languageCode": "en"
}
}
]
}
```


## Sample output

```
{
"values": [
{
"recordId": "1",
"data" :
{
"entities": [
{
"name": "Microsoft",
"id": "Microsoft",
"language": "en",
"url": "https://en.wikipedia.org/wiki/Microsoft",
"bingId": "a093e9b9-90f5-a3d5-c4b8-5855e1b01f85",
"dataSource": "Wikipedia",
"matches": [
{
"text": "Microsoft",
"offset": 0,
"length": 9,
"confidenceScore": 0.13
}
]
}
],
}
}
]
}
```


The offsets returned for entities in the output of this skill are directly returned from the [Language Service APIs](/en-us/azure/ai-services/language-service/overview), which means if you're using them to index into the original string, you should use the [StringInfo](/en-us/dotnet/api/system.globalization.stringinfo) class in .NET in order to extract the correct content. For more information, see [Multilingual and emoji support in Language service features](/en-us/azure/ai-services/language-service/concepts/multilingual-emoji-support).

## Warning cases

If the language code for the document is unsupported, a warning is returned and no entities are extracted.


---

<!-- DOCUMENTO FUSIONADO: search-indexer-howto-access-trusted-service-exception.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-howto-access-trusted-service-exception -->

# Make indexer connections to Azure Storage as a trusted service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, indexers that access Azure blobs can use the [trusted service exception](/en-us/azure/storage/common/storage-network-security#exceptions) to securely access blobs. This mechanism offers customers who are unable to grant [indexer access using IP firewall rules](search-indexer-howto-access-ip-restricted) a simple, secure, and free alternative for accessing data in storage accounts.

Note

If Azure Storage is behind a firewall and in the same region as Azure AI Search, you won't be able to create an inbound rule that admits requests from your search service. The solution for this scenario is for search to connect as a trusted service, as described in this article.

## Prerequisites

A search service with a system-assigned managed identity. See

[Check service identity](#check-service-identity).A storage account with the

**Allow trusted Microsoft services to access this storage account**network option. See[Check network settings](#check-network-settings).An Azure role assignment in Azure Storage that grants permissions to the search service system-assigned managed identity. See

[Check permissions](#check-permissions).

Note

In Azure AI Search, a trusted service connection is limited to blobs and ADLS Gen2 on Azure Storage. It's unsupported for indexer connections to Azure Table Storage and Azure Files.

A trusted service connection must use a system-assigned managed identity. A user-assigned managed identity isn't currently supported for this scenario.

## Check service identity

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).From the left pane, select

**Settings**>**Identity**.[Enable a system-assigned identity](search-how-to-managed-identities). Remember that user-assigned managed identities don't work for a trusted service connection.

## Check network settings

Sign in to the

[Azure portal](https://portal.azure.com)and[find your storage account](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Storage%2storageAccounts/).From the left pane, select

**Security + networking**>**Networking**.On the

**Public access**tab, select**Manage**.Under

**Public network access scope**, select**Enable from selected networks**.Under

**Exceptions**, select**Allow trusted Microsoft services to access this resource**.Assuming your search service has role-based access to the storage account, it can access data even when connections to Azure Storage are secured by IP firewall rules.


## Check permissions

A system-assigned managed identity is a Microsoft Entra service principal. The assignment needs **Storage Blob Data Reader** at a minimum.

In the left pane under

**Access Control**, view all role assignments and make sure that**Storage Blob Data Reader**is assigned to the search service system identity.Add

**Storage Blob Data Contributor**if write access is required.Features that require write access include

[enrichment caching](enrichment-cache-how-to-configure),[debug sessions](cognitive-search-debug-session), and[knowledge store](knowledge-store-concept-intro).

## Set up and test the connection

The easiest way to test the connection is by running the **Import data** wizard.

Start the

**Import data**wizard, selecting Azure Blob Storage or Azure Data Lake Storage Gen2.Choose a connection to your storage account, and then select

**System-assigned**. Select**Next**to invoke a connection. If the index schema is detected, the connection succeeded.
