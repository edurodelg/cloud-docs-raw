---
merged_at: 2026-01-25T02:11:58.472786
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-create-custom-skill-example.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-create-custom-skill-example -->

# Example: Create a custom skill using the Bing Entity Search API

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this example, learn how to create a web API custom skill. This skill will accept locations, public figures, and organizations, and return descriptions for them. The example uses an [Azure Function](https://azure.microsoft.com/services/functions/) to wrap the [Bing Entity Search API](/en-us/previous-versions/bing/search-apis/bing-entity-search/overview) so that it implements the custom skill interface.

## Prerequisites

Read about

[custom skill interface](cognitive-search-custom-skill-interface)article if you aren't familiar with the input/output interface that a custom skill should implement.Create a

[Bing Search resource](https://portal.azure.com/#create/Microsoft.BingSearch)through the Azure portal. A free tier is available and sufficient for this example.Install

[Visual Studio](https://www.visualstudio.com/vs/)or later.

## Create an Azure Function

Although this example uses an Azure Function to host a web API, it isn't required. As long as you meet the [interface requirements for a cognitive skill](cognitive-search-custom-skill-interface), the approach you take is immaterial. Azure Functions, however, make it easy to create a custom skill.

### Create a project

In Visual Studio, select

**New**>**Project**from the File menu.Choose

**Azure Functions**as the template and select**Next**. Type a name for your project, and select**Create**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other special characters.Select a framework that has long term support.

Choose

**HTTP Trigger**for the type of function to add to the project.Choose

**Function**for the authorization level.Select

**Create**to create the function project and HTTP triggered function.

### Add code to call the Bing Entity API

Visual Studio creates a project with boilerplate code for the chosen function type. The *FunctionName* attribute on the method sets the name of the function. The *HttpTrigger* attribute specifies that the function is triggered by an HTTP request.

Replace the contents of *Function1.cs* with the following code:

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace SampleSkills
{
/// <summary>
/// Sample custom skill that wraps the Bing entity search API to connect it with a
/// AI enrichment pipeline.
/// </summary>
public static class BingEntitySearch
{
#region Credentials
// IMPORTANT: Make sure to enter your credential and to verify the API endpoint matches yours.
static readonly string bingApiEndpoint = "https://api.bing.microsoft.com/v7.0/entities";
static readonly string key = "<enter your api key here>";
#endregion
#region Class used to deserialize the request
private class InputRecord
{
public class InputRecordData
{
public string Name { get; set; }
}
public string RecordId { get; set; }
public InputRecordData Data { get; set; }
}
private class WebApiRequest
{
public List<InputRecord> Values { get; set; }
}
#endregion
#region Classes used to serialize the response
private class OutputRecord
{
public class OutputRecordData
{
public string Name { get; set; } = "";
public string Description { get; set; } = "";
public string Source { get; set; } = "";
public string SourceUrl { get; set; } = "";
public string LicenseAttribution { get; set; } = "";
public string LicenseUrl { get; set; } = "";
}
public class OutputRecordMessage
{
public string Message { get; set; }
}
public string RecordId { get; set; }
public OutputRecordData Data { get; set; }
public List<OutputRecordMessage> Errors { get; set; }
public List<OutputRecordMessage> Warnings { get; set; }
}
private class WebApiResponse
{
public List<OutputRecord> Values { get; set; }
}
#endregion
#region Classes used to interact with the Bing API
private class BingResponse
{
public BingEntities Entities { get; set; }
}
private class BingEntities
{
public BingEntity[] Value { get; set; }
}
private class BingEntity
{
public class EntityPresentationinfo
{
public string[] EntityTypeHints { get; set; }
}
public class License
{
public string Url { get; set; }
}
public class ContractualRule
{
public string _type { get; set; }
public License License { get; set; }
public string LicenseNotice { get; set; }
public string Text { get; set; }
public string Url { get; set; }
}
public ContractualRule[] ContractualRules { get; set; }
public string Description { get; set; }
public string Name { get; set; }
public EntityPresentationinfo EntityPresentationInfo { get; set; }
}
#endregion
#region The Azure Function definition
[FunctionName("EntitySearch")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequest req,
ILogger log)
{
log.LogInformation("Entity Search function: C# HTTP trigger function processed a request.");
var response = new WebApiResponse
{
Values = new List<OutputRecord>()
};
string requestBody = new StreamReader(req.Body).ReadToEnd();
var data = JsonConvert.DeserializeObject<WebApiRequest>(requestBody);
// Do some schema validation
if (data == null)
{
return new BadRequestObjectResult("The request schema does not match expected schema.");
}
if (data.Values == null)
{
return new BadRequestObjectResult("The request schema does not match expected schema. Could not find values array.");
}
// Calculate the response for each value.
foreach (var record in data.Values)
{
if (record == null || record.RecordId == null) continue;
OutputRecord responseRecord = new OutputRecord
{
RecordId = record.RecordId
};
try
{
responseRecord.Data = GetEntityMetadata(record.Data.Name).Result;
}
catch (Exception e)
{
// Something bad happened, log the issue.
var error = new OutputRecord.OutputRecordMessage
{
Message = e.Message
};
responseRecord.Errors = new List<OutputRecord.OutputRecordMessage>
{
error
};
}
finally
{
response.Values.Add(responseRecord);
}
}
return (ActionResult)new OkObjectResult(response);
}
#endregion
#region Methods to call the Bing API
/// <summary>
/// Gets metadata for a particular entity based on its name using Bing Entity Search
/// </summary>
/// <param name="entityName">The name of the entity to extract data for.</param>
/// <returns>Asynchronous task that returns entity data. </returns>
private async static Task<OutputRecord.OutputRecordData> GetEntityMetadata(string entityName)
{
var uri = bingApiEndpoint + "?q=" + entityName + "&mkt=en-us&count=10&offset=0&safesearch=Moderate";
var result = new OutputRecord.OutputRecordData();
using (var client = new HttpClient())
using (var request = new HttpRequestMessage {
Method = HttpMethod.Get,
RequestUri = new Uri(uri)
})
{
request.Headers.Add("Ocp-Apim-Subscription-Key", key);
HttpResponseMessage response = await client.SendAsync(request);
string responseBody = await response?.Content?.ReadAsStringAsync();
BingResponse bingResult = JsonConvert.DeserializeObject<BingResponse>(responseBody);
if (bingResult != null)
{
// In addition to the list of entities that could match the name, for simplicity let's return information
// for the top match as additional metadata at the root object.
return AddTopEntityMetadata(bingResult.Entities?.Value);
}
}
return result;
}
private static OutputRecord.OutputRecordData AddTopEntityMetadata(BingEntity[] entities)
{
if (entities != null)
{
foreach (BingEntity entity in entities.Where(
entity => entity?.EntityPresentationInfo?.EntityTypeHints != null
&& (entity.EntityPresentationInfo.EntityTypeHints[0] == "Person"
|| entity.EntityPresentationInfo.EntityTypeHints[0] == "Organization"
|| entity.EntityPresentationInfo.EntityTypeHints[0] == "Location")
&& !String.IsNullOrEmpty(entity.Description)))
{
var rootObject = new OutputRecord.OutputRecordData
{
Description = entity.Description,
Name = entity.Name
};
if (entity.ContractualRules != null)
{
foreach (var rule in entity.ContractualRules)
{
switch (rule._type)
{
case "ContractualRules/LicenseAttribution":
rootObject.LicenseAttribution = rule.LicenseNotice;
rootObject.LicenseUrl = rule.License.Url;
break;
case "ContractualRules/LinkAttribution":
rootObject.Source = rule.Text;
rootObject.SourceUrl = rule.Url;
break;
}
}
}
return rootObject;
}
}
return new OutputRecord.OutputRecordData();
}
#endregion
}
}
```


Make sure to enter your own *key* value in the `key`

constant based on the key you got when signing up for the Bing Entity search API.

## Test the function from Visual Studio

Press **F5** to run the program and test function behaviors. In this case, we'll use the function below to look up two entities. Use a REST client to issue a call like the one shown below:

```
POST https://localhost:7071/api/EntitySearch
```


### Request body

```
{
"values": [
{
"recordId": "e1",
"data":
{
"name": "Pablo Picasso"
}
},
{
"recordId": "e2",
"data":
{
"name": "Microsoft"
}
}
]
}
```


### Response

You should see a response similar to the following example:

```
{
"values": [
{
"recordId": "e1",
"data": {
"name": "Pablo Picasso",
"description": "Pablo Ruiz Picasso was a Spanish painter [...]",
"source": "Wikipedia",
"sourceUrl": "http://en.wikipedia.org/wiki/Pablo_Picasso",
"licenseAttribution": "Text under CC-BY-SA license",
"licenseUrl": "http://creativecommons.org/licenses/by-sa/3.0/"
},
"errors": null,
"warnings": null
},
"..."
]
}
```


## Publish the function to Azure

When you're satisfied with the function behavior, you can publish it.

In

**Solution Explorer**, right-click the project and select**Publish**. Choose**Create New**>**Publish**.If you haven't already connected Visual Studio to your Azure account, select

**Add an account....**Follow the on-screen prompts. You're asked to specify a unique name for your app service, the Azure subscription, the resource group, the hosting plan, and the storage account you want to use. You can create a new resource group, a new hosting plan, and a storage account if you don't already have these. When finished, select

**Create**After the deployment is complete, notice the Site URL. It is the address of your function app in Azure.

In the

[Azure portal](https://portal.azure.com), navigate to the Resource Group, and look for the`EntitySearch`

Function you published. Under the**Manage**section, you should see Host Keys. Select the**Copy**icon for the*default*host key.

## Test the function in Azure

Now that you have the default host key, test your function as follows:

```
POST https://[your-entity-search-app-name].azurewebsites.net/api/EntitySearch?code=[enter default host key here]
```


### Request Body

```
{
"values": [
{
"recordId": "e1",
"data":
{
"name": "Pablo Picasso"
}
},
{
"recordId": "e2",
"data":
{
"name": "Microsoft"
}
}
]
}
```


This example should produce the same result you saw previously when running the function in the local environment.

## Connect to your pipeline

Now that you have a new custom skill, you can add it to your skillset. The example below shows you how to call the skill to add descriptions to organizations in the document (this could be extended to also work on locations and people). Replace `[your-entity-search-app-name]`

with the name of your app.

```
{
"skills": [
"[... your existing skills remain here]",
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "Our new Bing entity search custom skill",
"uri": "https://[your-entity-search-app-name].azurewebsites.net/api/EntitySearch?code=[enter default host key here]",
"context": "/document/merged_content/organizations/*",
"inputs": [
{
"name": "name",
"source": "/document/merged_content/organizations/*"
}
],
"outputs": [
{
"name": "description",
"targetName": "description"
}
]
}
]
}
```


Here, we're counting on the built-in [entity recognition skill](cognitive-search-skill-entity-recognition-v3) to be present in the skillset and to have enriched the document with the list of organizations. For reference, here's an entity extraction skill configuration that would be sufficient in generating the data we need:

```
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityRecognitionSkill",
"name": "#1",
"description": "Organization name extraction",
"context": "/document/merged_content",
"categories": [ "Organization" ],
"defaultLanguageCode": "en",
"inputs": [
{
"name": "text",
"source": "/document/merged_content"
},
{
"name": "languageCode",
"source": "/document/language"
}
],
"outputs": [
{
"name": "organizations",
"targetName": "organizations"
}
]
},
```


## Next steps

Congratulations! You've created your first custom skill. Now you can follow the same pattern to add your own custom functionality. Click the following links to learn more.


---

<!-- DOCUMENTO FUSIONADO: troubleshoot-shared-private-link-resources.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/troubleshoot-shared-private-link-resources -->

# Troubleshoot issues with shared private links in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A shared private link allows Azure AI Search to make secure outbound connections over a private endpoint when accessing customer resources in a virtual network. This article can help you resolve errors that might occur.

Creating a shared private link is a search service control plane operation. You can [create a shared private link](search-indexer-howto-access-private) using either the Azure portal or a [Management REST API](/en-us/rest/api/searchmanagement/shared-private-link-resources/create-or-update). During provisioning, the state of the request is `Updating`

. After the operation completes successfully, status is `Succeeded`

. A private endpoint to the resource, along with any DNS zones and mappings, is created. This endpoint is used exclusively by your search service instance and is managed through Azure AI Search.

The following are common errors that occur during the creation phase.

## Request validation failures

Unsupported SKU: Shared private links are supported on the Basic tier and higher. For indexers with skillsets, the minimum tier is Standard 1 (S1). For more information, see

[Shared private link resource limits](search-limits-quotas-capacity#shared-private-link-resource-limits).Invalid name: Naming rules for a shared private link are:

- Length should be between 1 to 60 characters
- Alphanumeric characters
- Names can include underscore
`_`

, period`.`

, and hyphen`-`

as long as it's not the first character in the name

Invalid group ID: Group IDs are case-sensitive and must be one of the following values.

Azure resource Group ID First available API version Azure Storage - Blob (or) ADLS Gen 2 `blob`

`2020-08-01`

Azure Storage - Tables `table`

`2020-08-01`

Azure Cosmos DB for NoSQL `Sql`

`2020-08-01`

Azure SQL Database `sqlServer`

`2020-08-01`

Azure Database for MySQL (preview) `mysqlServer`

`2020-08-01-Preview`

Azure Key Vault `vault`

`2020-08-01`

Azure Functions (preview) `sites`

`2020-08-01-Preview`

Resources marked with "(preview)" must be created using a preview version of the Management REST API versions.

`privateLinkResourceId`

type validation: Similar to`groupId`

, Azure AI Search validates that the "correct" resource type is specified in the`privateLinkResourceId`

. The following are valid resource types:Azure resource Resource type First available API version Azure Storage `Microsoft.Storage/storageAccounts`

`2020-08-01`

Azure Cosmos DB `Microsoft.DocumentDb/databaseAccounts`

`2020-08-01`

Azure SQL Database `Microsoft.Sql/servers`

`2020-08-01`

Azure Key Vault `Microsoft.KeyVault/vaults`

`2020-08-01`

Azure Database for MySQL (preview) `Microsoft.DBforMySQL/servers`

`2020-08-01-Preview`

Azure Functions (preview) `Microsoft.Web/sites`

`2020-08-01-Preview`

Azure SQL Managed Instance (preview) `Microsoft.Sql/managedInstance`

`2020-08-01-Preview`

In addition, the specified

`groupId`

needs to be valid for the specified resource type. For example,`groupId`

"blob" is valid for type`Microsoft.Storage/storageAccounts`

, it can't be used with any other resource type. For a given search management API version, customers can find out the supported`groupId`

and resource type details by utilizing the[List supported API](/en-us/rest/api/searchmanagement/private-link-resources/list-supported).Quota limit enforcement: Search services have quotas imposed on the distinct number of shared private link resources that can be created and the number of various target resource types that are being used (based on

`groupId`

). For more information, see[Shared private link resource limits](search-limits-quotas-capacity#shared-private-link-resource-limits).

## Deployment failures

A search service initiates the request to create a shared private link, but Azure Resource Manager performs the actual work. You can [check the deployment's status](search-indexer-howto-access-private#1---create-a-shared-private-link) in the Azure portal or by query, and address any errors that might occur.

Shared private link resources that fail Azure Resource Manager deployment show up in [List](/en-us/rest/api/searchmanagement/shared-private-link-resources/list-by-service) and [Get](/en-us/rest/api/searchmanagement/shared-private-link-resources/get) API calls, but they have a "Provisioning State" of `Failed`

. Once the reason of the Azure Resource Manager deployment failure is ascertained, delete the `Failed`

resource and re-create it after applying the appropriate resolution from the following table.

| Deployment failure reason | Description | Resolution |
|---|---|---|
| "LinkedAuthorizationFailed" | The error message states that the client has permission to create the shared private link on the search service, but doesn't have permission to perform action 'privateEndpointConnectionApproval/action' on the linked scope. | Recheck the private link ID in the request to make sure there are no errors or omissions in the URI. If Azure AI Search and the Azure PaaS resource are in different subscriptions, and if you're using REST or a command line interface, ensure the
|

`Microsoft.Network`

resource provider (RP). If the subscription that hosts the target resource ("target subscription") isn't registered with `Microsoft.Network`

RP, then the Azure Resource Manager deployment can fail.[register the resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider)using the Azure portal, PowerShell, or CLI.`groupId`

for the target resource`groupId`

for shared private link resources. When a shared private link of type "Sql" is created for a `privateLinkResourceId`

pointing to a non-Sql database account, the Azure Resource Manager deployment fails because of the `groupId`

mismatch. The Azure resource ID of an Azure Cosmos DB account isn't sufficient to determine the API type that is being used. Azure AI Search tries to create the private endpoint, which Azure Cosmos DB then denies.`privateLinkResourceId`

of the specified Azure Cosmos DB resource is for a database account of "Sql" API type`privateLinkResourceId`

is checked only during the commencement of the Azure Resource Manager deployment. If the target resource is no longer available, then the deployment fails.## Issues approving the backing private endpoint

A private endpoint is created to the target Azure resource as specified in the shared private link creation request. This is one of the final steps in the asynchronous Azure Resource Manager deployment operation, but Azure AI Search needs to link the private endpoint's private IP address as part of its network configuration. Once this link is done, the `provisioningState`

of the shared private link resource goes to a terminal success state `Succeeded`

. Customers should only approve or deny(or in general modify the configuration of the backing private endpoint) after the state transitions to `Succeeded`

. Modifying the private endpoint in any way before this could result in an incomplete deployment operation and can cause the shared private link resource to end up (either immediately, or usually within a few hours) in a `Failed`

state.

## Search service network connectivity change stalled in an "Updating" state

Shared private links and private endpoints are used when search service **Public Network Access** is **Disabled**. Typically, changing network connectivity should succeed in a few minutes after the request is accepted. In some circumstances, Azure AI Search might take several hours to complete the connectivity change operation.


If you observe that the connectivity change operation is taking a significant amount of time, wait for a few hours. Connectivity change operations involve operations such as updating DNS records which might take longer than expected.

If **Public Network Access** is changed, existing shared private links and private endpoints might not work correctly. If existing shared private links and private endpoints stop working during a connectivity change operation, wait a few hours for the operation to complete. If they're still not working, try deleting and recreating them.

## Shared private link resource stalled in an "Updating" or "Incomplete" state

Typically, a shared private link resource should go a terminal state (`Succeeded`

or `Failed`

) in a few minutes after the request is accepted.

In rare circumstances, Azure AI Search can fail to correctly mark the state of the shared private link resource to a terminal state (`Succeeded`

or `Failed`

). This usually occurs due to an unexpected failure. Shared private link resources are automatically transitioned to a `Failed`

state if it's "stuck" in a nonterminal state for more than a few hours.

If the shared private link resource doesn't transition to a terminal state, wait for a few hours to ensure that it becomes `Failed`

before you can delete it and re-create it. Alternatively, instead of waiting you can try to create another shared private link resource with a different name (keeping all other parameters the same).

## Updating a shared private link resource

An existing shared private link resource can be updated using the [Create or Update API](/en-us/rest/api/searchmanagement/shared-private-link-resources/create-or-update). Search only allows for narrow updates to the shared private link resource - only the request message can be modified via this API.

It isn't possible to update any of the "core" properties of an existing shared private link resource (such as

`privateLinkResourceId`

or`groupId`

) and this will always be unsupported. If any other property besides the request message needs to be changed, we advise customers to delete and re-create the shared private link resource.Updating the request message of a shared private link resource is only possible if it reaches the provisioning state of

`Succeeded`

.

## Deleting a shared private link resource

Customers can delete an existing shared private link resource via the [Delete API](/en-us/rest/api/searchmanagement/shared-private-link-resources/delete). Similar to the process of creation (or update), this is also an asynchronous operation with four steps:

You request a search service to delete the shared private link resource.

The search service validates that the resource exists and is in a state valid for deletion. If so, it initiates an Azure Resource Manager delete operation to remove the resource.

Search queries for the completion of the operation (which usually takes a few minutes). At this point, the shared private link resource would have a provisioning state of

`Deleting`

.Once the operation completes successfully, the backing private endpoint and any associated DNS mappings are removed. The resource doesn't show up as part of

[List](/en-us/rest/api/searchmanagement/shared-private-link-resources/list-by-service)operation and attempting a[Get](/en-us/rest/api/searchmanagement/shared-private-link-resources/get)operation on this resource results in a 404 Not Found.

The following are common errors that occur during the deletion phase.

| Failure Type | Description | Resolution |
|---|---|---|
| Resource is in nonterminal state | A shared private link resource that's not in a terminal state (`Succeeded` or `Failed` ) can't be deleted. It's possible (rare) for a shared private link resource to be stuck in a nonterminal state for up to 8 hours. |
Wait until the resource reaches a terminal state and retry the delete request. |
| Delete operation failed with error "Conflict" | The Azure Resource Manager operation to delete a shared private link resource reaches out to the resource provider of the target resource specified in `privateLinkResourceId` ("target RP") before it can remove the private endpoint and DNS mappings. Customers can utilize
|
Customers should remove the lock on the target resource before retrying the deletion operation. Note: This problem can also occur when customers try to delete a search service with shared private link resources that point to "locked" target resources |
| Delete operation failed | The asynchronous Azure Resource Manager delete operation can fail in rare cases. When this operation fails, querying the state of the asynchronous operation presents an error message and appropriate details. | Retry the operation at a later time, or reach out to Azure Support if the problem persists. |
| Resource stuck in "Deleting" state | In rare cases, a shared private link resource might be stuck in "Deleting" state for up to 8 hours, likely due to some catastrophic failure on the search RP. | Wait for 8 hours, after which the resource would transition to `Failed` state and then reissue the request. |

## Next steps

Learn more about shared private link resources and how to use it for secure access to protected content.
