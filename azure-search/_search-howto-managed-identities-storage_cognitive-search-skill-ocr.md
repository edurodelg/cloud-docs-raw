---
merged_at: 2026-01-25T02:11:58.388274
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-howto-managed-identities-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-managed-identities-storage -->

# Connect to Azure Storage using a managed identity (Azure AI Search)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure a search service connection to an Azure Storage account using a managed identity instead of providing credentials in the connection string.

You can use a system-assigned managed identity or a user-assigned managed identity. Managed identities are Microsoft Entra logins and require role assignments for access to Azure Storage.

## Prerequisites

- Azure AI Search, Basic tier or higher, with a
[managed identity](search-how-to-managed-identities).

Note

If storage is network-protected and in the same region as your search service, you must use a system-assigned managed identity and either one of the following network options: [connect as a trusted service](search-indexer-howto-access-trusted-service-exception), or [connect using the resource instance rule](/en-us/azure/storage/common/storage-network-security#grant-access-from-azure-resource-instances).

## Create a role assignment in Azure Storage

Sign in to Azure portal and find your storage account.

Select

**Access control (IAM)**.Select

**Add**and then select**Role assignment**.From the list of job function roles, select the roles needed for your search service:

Task Role assignment Blob indexing using an indexer Add **Storage Blob Data Reader**ADLS Gen2 indexing using an indexer Add **Storage Blob Data Reader**Table indexing using an indexer Add **Storage Table Data Reader**File indexing using an indexer Add **Reader and Data Access**Write to a [knowledge store](knowledge-store-concept-intro)Add **Storage Blob Data Contributor**for object and file projections, and**Reader and Data Access**for table projections.Write to an [enrichment cache](enrichment-cache-how-to-configure)Add **Storage Blob Data Contributor**and**Storage Table Data Contributor**Save [debug session state](cognitive-search-debug-session)Add **Storage Blob Data Contributor**Select

**Next**.Select

**Managed identity**and then select**Members**.Filter by system-assigned managed identities or user-assigned managed identities. You should see the managed identity that you previously created for your search service. If you don't have one, see

[Configure search to use a managed identity](search-how-to-managed-identities). If you already set one up but it's not available, give it a few minutes.Select the identity and save the role assignment.


## Specify a managed identity in a connection string

Once you have a role assignment, you can set up a connection to Azure Storage that operates under that role.

[Indexers](search-indexer-overview) use a data source object for connections to an external data source. This section explains how to specify a system-assigned managed identity or a user-assigned managed identity on a data source connection string. You can find more [connection string examples](search-how-to-managed-identities#connection-string-examples) in the managed identity article.

Tip

You can create a data source connection to Azure Storage in the Azure portal, specifying either a system or user-assigned managed identity, and then view the JSON definition to see how the connection string is formulated.

### System-assigned managed identity

You must have a [system-assigned managed identity already configured](search-how-to-managed-identities), and it must have a role-assignment on Azure Storage.

For connections made using a system-assigned managed identity, the only change to the [data source definition](/en-us/rest/api/searchservice/data-sources/create) is the format of the `credentials`

property.

Provide a connection string that contains a `ResourceId`

, with no account key or password. The `ResourceId`

must include the subscription ID of the storage account, the resource group of the storage account, and the storage account name.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-09-01
{
"name" : "blob-datasource",
"type" : "azureblob",
"credentials" : {
"connectionString" : "ResourceId=/subscriptions/00000000-0000-0000-0000-00000000/resourceGroups/MY-DEMO-RESOURCE-GROUP/providers/Microsoft.Storage/storageAccounts/MY-DEMO-STORAGE-ACCOUNT/;"
},
"container" : {
"name" : "my-container", "query" : "<optional-virtual-directory-name>"
}
}
```


### User-assigned managed identity (preview)

You must have a [user-assigned managed identity already configured](search-how-to-managed-identities) and associated with your search service, and the identity must have a role-assignment on Azure Storage.

Connections made through user-assigned managed identities use the same credentials as a system-assigned managed identity, plus an extra identity property that contains the collection of user-assigned managed identities. Only one user-assigned managed identity should be provided when creating the data source.

Provide a connection string that contains a `ResourceId`

, with no account key or password. The `ResourceId`

must include the subscription ID of the storage account, the resource group of the storage account, and the storage account name.

Provide an `identity`

using the syntax shown in the following example. Set `userAssignedIdentity`

to the user-assigned managed identity.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-11-01-preview
{
"name" : "blob-datasource",
"type" : "azureblob",
"credentials" : {
"connectionString" : "ResourceId=/subscriptions/00000000-0000-0000-0000-00000000/resourceGroups/MY-DEMO-RESOURCE-GROUP/providers/Microsoft.Storage/storageAccounts/MY-DEMO-STORAGE-ACCOUNT/;"
},
"container" : {
"name" : "my-container", "query" : "<optional-virtual-directory-name>"
},
"identity" : {
"@odata.type": "#Microsoft.Azure.Search.DataUserAssignedIdentity",
"userAssignedIdentity" : "/subscriptions/00000000-0000-0000-0000-00000000/resourcegroups/MY-DEMO-RESOURCE-GROUP/providers/Microsoft.ManagedIdentity/userAssignedIdentities/MY-DEMO-USER-MANAGED-IDENTITY"
}
}
```


Connection information and permissions on the remote service are validated at run time during indexer execution. If the indexer is successful, the connection syntax and role assignments are valid. For more information, see [Run or reset indexers, skills, or documents](search-howto-run-reset-indexers).

## Accessing network secured data in storage accounts

Azure storage accounts can be further secured using firewalls and virtual networks. If you want to index content from a storage account that is secured using a firewall or virtual network, see [Make indexer connections to Azure Storage as a trusted service](search-indexer-howto-access-trusted-service-exception).


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-ocr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-ocr -->

# OCR cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **optical character recognition (OCR)** skill recognizes printed and handwritten text in image files. This article is the reference documentation for the OCR skill. See [Extract text from images](cognitive-search-concept-image-scenarios) for usage instructions.

The **OCR** skill uses the machine learning models provided by [Azure Vision in Foundry Tools](/en-us/azure/ai-services/computer-vision/overview) API [v3.2](https://westus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2/operations/5d986960601faab4bf452005). The **OCR** skill maps to the following functionality:

For the languages listed under

[Azure Vision language support](/en-us/azure/ai-services/computer-vision/language-support#optical-character-recognition-ocr), the[Read API](/en-us/azure/ai-services/computer-vision/overview-ocr)is used.For Greek and Serbian Cyrillic, the legacy

[OCR in version 3.2](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/cognitiveservices/data-plane/ComputerVision/stable/v3.2)API is used.

The **OCR** skill extracts text from image files and embedded images. Supported file formats include:

- .JPEG
- .JPG
- .PNG
- .BMP
- .TIFF

Supported data sources for OCR and image analysis are blobs in Azure Blob Storage and Azure Data Lake Storage (ADLS) Gen2, and image content in Microsoft OneLake. Images can be standalone files or embedded images in a PDF or other files.

Note

This skill is bound to Foundry Tools and requires a [billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

In addition, image extraction is [billable by Azure AI Search](https://azure.microsoft.com/pricing/details/search/).

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`detectOrientation` |
Detects image orientation. Valid values are `true` or `false` . This parameter only applies if the
|
`defaultLanguageCode` |
Language code of the input text. Supported languages include all of the
`unk` (Unknown). If the language code is unspecified or null, the language is set to English. If the language is explicitly set to `unk` , all languages found are auto-detected and returned. |

`lineEnding`

In previous versions, there was a parameter called "textExtractionAlgorithm" to specify extraction of "printed" or "handwritten" text. This parameter is deprecated because the current Read API algorithm extracts both types of text at once. If your skill includes this parameter, you don't need to remove it, but it won't be used during skill execution.

## Skill inputs

| Input name | Description |
|---|---|
`image` |
Complex Type. Currently only works with "/document/normalized_images" field, produced by the Azure blob indexer when `imageAction` is set to a value other than `none` . |

## Skill outputs

| Output name | Description |
|---|---|
`text` |
Plain text extracted from the image. |
`layoutText` |
Complex type that describes the extracted text and the location where the text was found. |

If you call OCR on images embedded in PDFs or other application files, the OCR output will be located at the bottom of the page, after any text that was extracted and processed.

## Sample definition

```
{
"skills": [
{
"description": "Extracts text (plain and structured) from image.",
"@odata.type": "#Microsoft.Skills.Vision.OcrSkill",
"context": "/document/normalized_images/*",
"defaultLanguageCode": null,
"detectOrientation": true,
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "text",
"targetName": "myText"
},
{
"name": "layoutText",
"targetName": "myLayoutText"
}
]
}
]
}
```


## Sample text and layoutText output

```
{
"text": "Hello World. -John",
"layoutText":
{
"language" : "en",
"text" : "Hello World. -John",
"lines" : [
{
"boundingBox":
[ {"x":10, "y":10}, {"x":50, "y":10}, {"x":50, "y":30},{"x":10, "y":30}],
"text":"Hello World."
},
{
"boundingBox": [ {"x":110, "y":10}, {"x":150, "y":10}, {"x":150, "y":30},{"x":110, "y":30}],
"text":"-John"
}
],
"words": [
{
"boundingBox": [ {"x":110, "y":10}, {"x":150, "y":10}, {"x":150, "y":30},{"x":110, "y":30}],
"text":"Hello"
},
{
"boundingBox": [ {"x":110, "y":10}, {"x":150, "y":10}, {"x":150, "y":30},{"x":110, "y":30}],
"text":"World."
},
{
"boundingBox": [ {"x":110, "y":10}, {"x":150, "y":10}, {"x":150, "y":30},{"x":110, "y":30}],
"text":"-John"
}
]
}
}
```


## Sample: Merging text extracted from embedded images with the content of the document

Document cracking, the first step in skillset execution, separates text and image content. A common use case for Text Merger is merging the textual representation of images (text from an OCR skill, or the caption of an image) into the content field of a document. This is for scenarios where the source document is a PDF or Word document that combines text with embedded images.

The following example skillset creates a *merged_text* field. This field contains the textual content of your document and the OCRed text from each of the images embedded in that document.

#### Request Body Syntax

```
{
"description": "Extract text from images and merge with content text to produce merged_text",
"skills":
[
{
"description": "Extract text (plain and structured) from image.",
"@odata.type": "#Microsoft.Skills.Vision.OcrSkill",
"context": "/document/normalized_images/*",
"defaultLanguageCode": "en",
"detectOrientation": true,
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "text"
}
]
},
{
"@odata.type": "#Microsoft.Skills.Text.MergeSkill",
"description": "Create merged_text, which includes all the textual representation of each image inserted at the right location in the content field.",
"context": "/document",
"insertPreTag": " ",
"insertPostTag": " ",
"inputs": [
{
"name":"text",
"source": "/document/content"
},
{
"name": "itemsToInsert",
"source": "/document/normalized_images/*/text"
},
{
"name":"offsets",
"source": "/document/normalized_images/*/contentOffset"
}
],
"outputs": [
{
"name": "mergedText",
"targetName" : "merged_text"
}
]
}
]
}
```


The above skillset example assumes that a normalized-images field exists. To generate this field, set the *imageAction* configuration in your indexer definition to *generateNormalizedImages* as shown below:

```
{
//...rest of your indexer definition goes here ...
"parameters": {
"configuration": {
"dataToExtract":"contentAndMetadata",
"imageAction":"generateNormalizedImages"
}
}
}
```
