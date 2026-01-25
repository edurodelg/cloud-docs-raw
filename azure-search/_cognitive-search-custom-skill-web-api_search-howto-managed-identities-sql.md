---
merged_at: 2026-01-25T02:11:58.417253
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-custom-skill-web-api.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-custom-skill-web-api -->

# Custom Web API skill in an Azure AI Search enrichment pipeline

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Custom Web API** skill allows you to extend AI enrichment by calling out to a Web API endpoint providing custom operations. Similar to built-in skills, a **Custom Web API** skill has inputs and outputs. Depending on the inputs, your Web API receives a JSON payload when the indexer runs, and outputs a JSON payload as a response, along with a success status code. The response is expected to have the outputs specified by your custom skill. Any other response is considered an error and no enrichments are performed. The structure of the JSON payload is described further down in this document.

The **Custom Web API** skill is also used in the implementation of [Azure OpenAI On Your Data](/en-us/azure/ai-services/openai/concepts/use-your-data) feature. If Azure OpenAI is [configured for role-based access](/en-us/azure/ai-services/openai/how-to/use-your-data-securely#configure-azure-openai) and you get `403 Forbidden`

calls when creating the vector index, verify that Azure AI Search has a [system assigned identity](search-how-to-managed-identities#create-a-system-managed-identity) and runs as a [trusted service](/en-us/azure/ai-services/openai/how-to/use-your-data-securely#enable-trusted-service) on Azure OpenAI.

Note

The indexer retries twice for certain standard HTTP status codes returned from the Web API. These HTTP status codes are:

`502 Bad Gateway`

`503 Service Unavailable`

`429 Too Many Requests`


## @odata.type

Microsoft.Skills.Custom.WebApiSkill

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`uri` |
The URI of the Web API to which the JSON payload is sent. Only the https URI scheme is allowed. |
`authResourceId` |
(Optional) A string that if set, indicates that this skill should use a system managed identity on the connection to the function or app hosting the code. This property takes an application (client) ID or app's registration in Microsoft Entra ID, in any of these formats: `api://<appId>` , `<appId>/.default` , `api://<appId>/.default` . This value is used to scope the authentication token retrieved by the indexer, and is sent along with the custom Web skill API request to the function or app. Setting this property requires that your search service is
`api-version=2023-10-01-Preview` . |
`authIdentity` |
(Optional) A user-managed identity used by the search service for connecting to the function or app hosting the code. You can use either a
`authIdentity` blank. |

`httpMethod`

`PUT`

or `POST`

`httpHeaders`

`Accept`

, `Accept-Charset`

, `Accept-Encoding`

, `Content-Length`

, `Content-Type`

, `Cookie`

, `Host`

, `TE`

, `Upgrade`

, `Via`

.`timeout`

[ISO 8601 duration](https://www.w3.org/TR/xmlschema11-2/#dayTimeDuration)value). For example,`PT60S`

for 60 seconds. If not set, a default value of 30 seconds is chosen. The timeout can be set to a maximum of 230 seconds and a minimum of 1 second.`batchSize`

`degreeOfParallelism`

`degreeOfParallelism`

can be set to a maximum of 10 and a minimum of 1.## Skill inputs

There are no predefined inputs for this skill. The inputs are any existing field, or any [node in the enrichment tree](cognitive-search-working-with-skillsets#enrichment-tree) that you want to pass to your custom skill.

## Skill outputs

There are no predefined outputs for this skill. Be sure to [define an output field mapping](cognitive-search-output-field-mapping) in the indexer if the skill's output should be sent to a field in the search index.

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "A custom skill that can identify positions of different phrases in the source text",
"uri": "https://contoso.count-things.com",
"batchSize": 4,
"context": "/document",
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "language",
"source": "/document/languageCode"
},
{
"name": "phraseList",
"source": "/document/keyphrases"
}
],
"outputs": [
{
"name": "hitPositions"
}
]
}
```


## Sample input JSON structure

This JSON structure represents the payload that is sent to your Web API. It always follows these constraints:

The top-level entity is called

`values`

and is an array of objects. The number of such objects are at most the`batchSize`

.Each object in the

`values`

array has:A

`recordId`

property that is a**unique**string, used to identify that record.A

`data`

property that is a JSON object. The fields of the`data`

property correspond to the "names" specified in the`inputs`

section of the skill definition. The values of those fields are from the`source`

of those fields (which could be from a field in the document, or potentially from another skill).


```
{
"values": [
{
"recordId": "0",
"data":
{
"text": "Este es un contrato en Inglés",
"language": "es",
"phraseList": ["Este", "Inglés"]
}
},
{
"recordId": "1",
"data":
{
"text": "Hello world",
"language": "en",
"phraseList": ["Hi"]
}
},
{
"recordId": "2",
"data":
{
"text": "Hello world, Hi world",
"language": "en",
"phraseList": ["world"]
}
},
{
"recordId": "3",
"data":
{
"text": "Test",
"language": "es",
"phraseList": []
}
}
]
}
```


## Sample output JSON structure

The "output" corresponds to the response returned from your Web API. The Web API should only return a JSON payload (verified by looking at the `Content-Type`

response header) and should satisfy the following constraints:

There should be a top-level entity called

`values`

, which should be an array of objects.The number of objects in the array should be the same as the number of objects sent to the Web API.

Each object should have:

A

`recordId`

property.A

`data`

property, which is an object where the fields are enrichments matching the "names" in the`output`

and whose value is considered the enrichment.An

`errors`

property, an array listing any errors encountered that is added to the indexer execution history. This property is required, but can have a`null`

value.A

`warnings`

property, an array listing any warnings encountered that is added to the indexer execution history. This property is required, but can have a`null`

value.

The ordering of objects in the

`values`

in either the request or response isn't important. However, the`recordId`

is used for correlation so any record in the response containing a`recordId`

, which wasn't part of the original request to the Web API is discarded.

```
{
"values": [
{
"recordId": "3",
"data": {
},
"errors": [
{
"message" : "'phraseList' should not be null or empty"
}
],
"warnings": null
},
{
"recordId": "2",
"data": {
"hitPositions": [6, 16]
},
"errors": null,
"warnings": null
},
{
"recordId": "0",
"data": {
"hitPositions": [0, 23]
},
"errors": null,
"warnings": null
},
{
"recordId": "1",
"data": {
"hitPositions": []
},
"errors": null,
"warnings": [
{
"message": "No occurrences of 'Hi' were found in the input text"
}
]
},
]
}
```


## Error cases

In addition to your Web API being unavailable, or sending out non-successful status codes the following are considered erroneous cases:

If the Web API returns a success status code but the response indicates that it isn't

`application/json`

then the response is considered invalid and no enrichments are performed.If there are invalid records (for example,

`recordId`

is missing or duplicated) in the response`values`

array, no enrichment is performed for the invalid records. It's important to adhere to the Web API skill contract when developing custom skills. You can refer to[this example](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Common/WebAPISkillContract.cs)provided in the[Power Skill repository](https://github.com/Azure-Samples/azure-search-power-skills/tree/main)that follows the expected contract.

For cases when the Web API is unavailable or returns an HTTP error, a friendly error with any available details about the HTTP error is added to the indexer execution history.


---

<!-- DOCUMENTO FUSIONADO: search-howto-managed-identities-sql.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-managed-identities-sql -->

# Set up an indexer connection to Azure SQL using a managed identity

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to set up an indexer connection to Azure SQL Database using a managed identity instead of providing credentials in the connection string.

You can use a system-assigned managed identity or a user-assigned managed identity (preview). Managed identities are Microsoft Entra logins and require Azure role assignments to access data in Azure SQL.

## Prerequisites

[Create a managed identity](search-how-to-managed-identities)for your search service.[Assign an Azure admin role on SQL](/en-us/azure/azure-sql/database/authentication-aad-configure). The identity used on the indexer connection needs read permissions. You must be a Microsoft Entra admin with a server in SQL Database or SQL Managed Instance to grant read permissions on a database.You should be familiar with

[indexer concepts](search-indexer-overview)and[configuration](search-how-to-index-sql-database).

## 1 - Assign permissions to read the database

Follow the below steps to assign the search service or user-assigned managed identity permission to read the database.

Connect to Visual Studio.

Authenticate with your Microsoft Entra account.

Execute the following commands:

Include the brackets around your search service name or user-assigned managed identity name.

`CREATE USER [insert your search service name here or user-assigned managed identity name] FROM EXTERNAL PROVIDER; EXEC sp_addrolemember 'db_datareader', [insert your search service name here or user-assigned managed identity name];`


If you later change the search service identity or user-assigned identity after assigning permissions, you must remove the role membership and remove the user in the SQL database, then repeat the permission assignment. Removing the role membership and user can be accomplished by running the following commands:

```
sp_droprolemember 'db_datareader', [insert your search service name or user-assigned managed identity name];
DROP USER IF EXISTS [insert your search service name or user-assigned managed identity name];
```


## 2 - Add a role assignment

In this section you'll, give your Azure AI Search service permission to read data from your SQL Server. For detailed steps, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

In the Azure portal, navigate to your Azure SQL Server page.

Select

**Access control (IAM)**.Select

**Add > Add role assignment**.On the

**Role**tab, select the appropriate**Reader**role.On the

**Members**tab, select**Managed identity**, and then select**Select members**.Select your Azure subscription.

If you're using a system-assigned managed identity, select

**System-assigned managed identity**, search for your search service, and then select it.Otherwise, if you're using a user-assigned managed identity, select

**User-assigned managed identity**, search for the name of the user-assigned managed identity, and then select it.On the

**Review + assign**tab, select**Review + assign**to assign the role.

## 3 - Create the data source

Create the data source and provide either a system-assigned managed identity or a user-assigned managed identity (preview).

### System-assigned managed identity

The [REST API](/en-us/rest/api/searchservice/data-sources/create), Azure portal, and the Azure SDKs support system-assigned managed identity.

When you're connecting with a system-assigned managed identity, the only change to the data source definition is the format of the "credentials" property. You'll provide an Initial Catalog or Database name and a ResourceId that has no account key or password. The ResourceId must include the subscription ID of Azure SQL Database, the resource group of SQL Database, and the name of the SQL database.

Here's an example of how to create a data source to index data from a storage account using the [Create Data Source](/en-us/rest/api/searchservice/data-sources/create) REST API and a managed identity connection string. The managed identity connection string format is the same for the REST API, .NET SDK, and the Azure portal.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "sql-datasource",
"type" : "azuresql",
"credentials" : {
"connectionString" : "Database=[SQL database name];ResourceId=/subscriptions/[subscription ID]/resourceGroups/[resource group name]/providers/Microsoft.Sql/servers/[SQL Server name];Connection Timeout=30;"
},
"container" : {
"name" : "my-table"
}
}
```


### User-assigned managed identity (preview)

Preview REST APIs support connections based on a user-assigned managed identity. When you're connecting with a user-assigned managed identity, there are two changes to the data source definition:

First, the format of the "credentials" property is an Initial Catalog or Database name and a ResourceId that has no account key or password. The ResourceId must include the subscription ID of Azure SQL Database, the resource group of SQL Database, and the name of the SQL database. This is the same format as the system-assigned managed identity.

Second, add an "identity" property that contains the collection of user-assigned managed identities. Only one user-assigned managed identity should be provided when creating the data source. Set it to type "userAssignedIdentities".


Here's an example of how to create an indexer data source object using the most recent preview API version for [Create or Update Data Source](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true):

```
POST https://[service name].search.windows.net/datasources?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [admin key]
{
"name" : "sql-datasource",
"type" : "azuresql",
"credentials" : {
"connectionString" : "Database=[SQL database name];ResourceId=/subscriptions/[subscription ID]/resourceGroups/[resource group name]/providers/Microsoft.Sql/servers/[SQL Server name];Connection Timeout=30;"
},
"container" : {
"name" : "my-table"
},
"identity" : {
"@odata.type": "#Microsoft.Azure.Search.DataUserAssignedIdentity",
"userAssignedIdentity" : "/subscriptions/[subscription ID]/resourcegroups/[resource group name]/providers/Microsoft.ManagedIdentity/userAssignedIdentities/[managed identity name]"
}
}
```


## 4 - Create the index

The index specifies the fields in a document, attributes, and other constructs that shape the search experience.

Here's a [Create Index](/en-us/rest/api/searchservice/indexes/create) REST API call with a searchable `booktitle`

field:

```
POST https://[service name].search.windows.net/indexes?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-target-index",
"fields": [
{ "name": "id", "type": "Edm.String", "key": true, "searchable": false },
{ "name": "booktitle", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
]
}
```


## 5 - Create the indexer

An indexer connects a data source with a target search index, and provides a schedule to automate the data refresh. Once the index and data source have been created, you're ready to create the indexer. If the indexer is successful, the connection syntax and role assignments are valid.

Here's a [Create Indexer](/en-us/rest/api/searchservice/indexers/create) REST API call with an Azure SQL indexer definition. The indexer runs when you submit the request.

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "sql-indexer",
"dataSourceName" : "sql-datasource",
"targetIndexName" : "my-target-index"
}
```


If you get an error when the indexer tries to connect to the data source that says that the client isn't allowed to access the server, take a look at [common indexer errors](search-indexer-troubleshooting).
