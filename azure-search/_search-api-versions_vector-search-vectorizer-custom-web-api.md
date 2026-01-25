---
merged_at: 2026-01-25T02:11:58.360984
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-api-versions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-api-versions -->

# API versions in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search rolls out feature updates regularly. Sometimes, but not always, these updates require a new version of the API to preserve backward compatibility. Publishing a new version allows you to control when and how you integrate search service updates in your code.

As a rule, the REST APIs and libraries are versioned only when necessary, since it can involve some effort to upgrade your code to use a new API version. A new version is needed only if some aspect of the API has changed in a way that breaks backward compatibility. Such changes can happen because of fixes to existing features, or because of new features that change existing API surface area.

For more information about the deprecation path, see the [Azure SDK lifecycle and support policy](https://azure.github.io/azure-sdk/policies_support.html).

## Deprecated versions

**2023-07-01-preview** was deprecated on April 8, 2024 and won't be supported after July 8, 2024.

This was the first REST API that offered vector search support. Newer API versions have a different vector configuration. You should [migrate to a newer version](search-api-migration) as soon as possible.

## Discontinued versions

Some API versions are discontinued and are no longer documented or supported:

**2015-02-28****2015-02-28-Preview****2014-07-31-Preview****2014-10-20-Preview**

All SDKs are based on REST API versions. If a REST version is discontinued, SDK packages based on that version are also discontinued. All Azure AI Search .NET SDKs older than [ 3.0.0-rc](https://www.nuget.org/packages/Microsoft.Azure.Search/3.0.0-rc) are now obsolete.

Support for the above-listed versions ended on October 15, 2020. If you have code that uses a discontinued version, you can [migrate existing code](search-api-migration) to a newer [REST API version](/en-us/rest/api/searchservice/) or to a newer Azure SDK.

## REST APIs

| REST API | Link |
|---|---|
| Search Service (data plane) | See
|

[API versions](/en-us/rest/api/searchmanagement/management-api-versions)in the REST API reference.## Azure SDK for .NET

The following table provides links to more recent SDK versions.

| SDK version | Status | Change log | Description |
|---|---|---|---|
|

[Change Log](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/CHANGELOG.md)[Azure.ResourceManager.Search](https://www.nuget.org/packages/Microsoft.Azure.Management.Search/4.0.0)[Change Log](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.ResourceManager.Search/CHANGELOG.md)## Azure SDK for Java

| SDK version | Status | Change log | Description |
|---|---|---|---|
|

[Change Log](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/CHANGELOG.md)Use the`azure-search-documents`

client library for data plane operations.[azure-resourcemanager-search 2](/en-us/java/api/overview/azure/resourcemanager-search-readme)[Change Log](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-resourcemanager-search/CHANGELOG.md)`azure-resourcemanager-search`

client library for control plane operations.## Azure SDK for JavaScript

| SDK version | Status | Change log | Description |
|---|---|---|---|
|

[Change Log](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/CHANGELOG.md)`@azure/search-documents`

client library for data plane operations.[@azure/arm-search 4](/en-us/javascript/api/overview/azure/arm-search-readme)[Change Log](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/arm-search/CHANGELOG.md)`@azure/arm-search`

package for control plane operations.## Azure SDK for Python

| SDK version | Status | Change log | Description |
|---|---|---|---|
|

[Change Log](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md)`azure-search-documents`

client library for data plane operations.[azure-mgmt-search 9](https://pypi.org/project/azure-mgmt-search/)[Change Log](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-mgmt-search/CHANGELOG.md)`azure-mgmt-search`

client library for control plane operations.## All Azure SDKs

If you're looking for beta client libraries and documentation, [this page](https://azure.github.io/azure-sdk/releases/latest/index.html) contains links to all of the Azure SDK library packages, code, and docs.


---

<!-- DOCUMENTO FUSIONADO: vector-search-vectorizer-custom-web-api.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-vectorizer-custom-web-api -->

# Custom Web API vectorizer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **custom web API** vectorizer allows you to configure your search queries to call out to a Web API endpoint to generate embeddings at query time. The structure of the JSON payload required to be implemented in the provided endpoint is described further down in this document. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

Although vectorizers are used at query time, you specify them in index definitions and reference them on vector fields through a vector profile. For more information, see [Configure a vectorizer in a search index](vector-search-how-to-configure-vectorizer).

The custom web API vectorizer is called `WebApiVectorizer`

in the REST API. Use the latest stable version of [Indexes - Create (REST API)](/en-us/rest/api/searchservice/indexes/create) or an Azure SDK package that provides the feature.

## Vectorizer parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`uri` |
The URI of the Web API to which the JSON payload is sent. Only the https URI scheme is allowed. |
`httpMethod` |
The method to use while sending the payload. Allowed methods are `PUT` or `POST` |
`httpHeaders` |
A collection of key-value pairs where the keys represent header names and values represent header values that are sent to your Web API along with the payload. The following headers are prohibited from being in this collection: `Accept` , `Accept-Charset` , `Accept-Encoding` , `Content-Length` , `Content-Type` , `Cookie` , `Host` , `TE` , `Upgrade` , `Via` . |
`authResourceId` |
(Optional) A string that if set, indicates that this vectorizer should use a managed identity on the connection to the function or app hosting the code. This property takes an application (client) ID or app's registration in Microsoft Entra ID, in any of these formats: `api://<appId>` , `<appId>/.default` , `api://<appId>/.default` . This value is used to scope the authentication token retrieved by the indexer, and is sent along with the custom Web API request to the function or app. Setting this property requires that your search service is
|
`authIdentity` |
(Optional) A user-managed identity used by the search service for connecting to the function or app hosting the code. You can use either a
`authIdentity` blank. |

`timeout`

[ISO 8601 duration](https://www.w3.org/TR/xmlschema11-2/#dayTimeDuration)value). For example,`PT60S`

for 60 seconds. If not set, a default value of 30 seconds is chosen. The timeout can be set to a maximum of 230 seconds and a minimum of 1 second.## Supported vector query types

The Custom Web API vectorizer supports `text`

, `imageUrl`

, and `imageBinary`

vector queries.

## Sample definition

```
"vectorizers": [
{
"name": "my-custom-web-api-vectorizer",
"kind": "customWebApi",
"customWebApiParameters": {
"uri": "https://contoso.embeddings.com",
"httpMethod": "POST",
"httpHeaders": {
"api-key": "0000000000000000000000000000000000000"
},
"timeout": "PT60S",
"authResourceId": null,
"authIdentity": null
},
}
]
```


## JSON payload structure

The required JSON payload structure that is expected for an endpoint when using it with the custom web API vectorizer is the same as that of the custom web API skill, which is discussed in more detail in [the documentation for the skill](cognitive-search-custom-skill-web-api#sample-input-json-structure).

There are the following other considerations to make when implementing a web API endpoint to use with the custom web API vectorizer.

The vectorizer sends only one record at a time in the

`values`

array when making a request to the endpoint.The vectorizer passes the data to be vectorized in a specific key in the

`data`

JSON object in the request payload. That key is`text`

,`imageUrl`

, or`imageBinary`

, depending on which type of vector query was requested.The vectorizer expects the resulting embedding to be under the

`vector`

key in the`data`

JSON object in the response payload.Any errors or warnings returned by the endpoint are ignored by the vectorizer and not obtainable for debugging purposes at query time.

If an

`imageBinary`

vector query was requested, the request payload sent to the endpoint is the following:`{ "values": [ { "recordId": "0", "data": { "imageBinary": { "data": "<base 64 encoded image binary data>" } } } ] }`
