---
merged_at: 2026-01-25T02:11:58.372552
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-create-app-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-create-app-portal -->

# Quickstart: Create a demo search app in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the **Create demo app** wizard in the Azure portal to generate a downloadable, "localhost"-style web app that runs in a browser. Depending on how you configure it, the generated app is operational on first use, with a live read-only connection to an index on your search service. A default app can include a search box, results area, sidebar filters, and typeahead support.

A demo app can help you visualize how an index functions in a client app, but it isn't intended for production scenarios. Production apps should include security, error handling, and hosting logic that the demo app doesn't provide.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. For this quickstart, you can use a free service.A

[search index](search-what-is-an-index)to use as the basis of your generated application.This quickstart uses the hotels-sample index. Follow the instructions in

[this quickstart](search-import-data-portal)to create the index.

## Start the wizard

To start the wizard for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Search management**>**Indexes**.Select

**hotels-sample-index**from the list.At the top of the index page, select

**Create demo app**.Select

**Enable CORS and continue**to add CORS support to your index definition.

## Configure search results

The wizard provides a basic layout for the rendered search results, including space for a thumbnail image, title, and description. Each element is backed by a field in your index that provides the necessary data.

To configure the search results:

Skip

**Thumbnail**because the index doesn't have image URLs.However, if your index contains a field populated with URLs that resolve to publicly available images, you should specify that field for the thumbnail.

For

**Title**, choose a field that conveys the uniqueness of each document. Our example uses**HotelName**.For

**Description**, choose a field that might help someone decide whether to drill down to that particular document. Our example uses**Description**.Select

**Next**.

## Add a sidebar

The search service supports faceted navigation, which is often rendered as a sidebar. Facets are based on fields attributed as filterable and facetable in your index schema.

Tip

To view field attributes, select the **Fields** tab on the index page in the Azure portal. Only fields marked as filterable and facetable can be used in the sidebar.

In Azure AI Search, faceted navigation is a cumulative filtering experience. Within a category, selecting multiple filters expands the results, such as selecting both `Seattle`

and `Bellevue`

within the `City`

filter. Across categories, selecting multiple filters narrows the results.

To customize the sidebar:

Review the list of filterable and facetable fields in the index.

To shorten the sidebar and prevent scrolling in the finished app, delete some fields.

Select

**Next**.

## Add suggestions

Suggestions are automated query prompts that appear in the search box. The demo app supports suggestions that provide a dropdown list of potential matching documents based on partial text inputs.

To customize the suggestions:

Choose the fields you want to display as suggested queries. Use shorter string fields instead of verbose fields, such as descriptions.

Use the

**Show Field Name**checkbox to include or exclude labels for the suggestions.

## Create, download, and execute

To finish the wizard and use the demo app:

Select

**Create demo app**to generate the HTML file.When prompted, select

**Download**to download the file.Open the file in a browser.

Select the search button to run an empty query (

`*`

) that returns an arbitrary result set.Enter a term in the search box and use the sidebar filters to narrow the results.

Tip

If you don't see suggested queries, check your browser settings or try a different browser.


## Clean up resources

When you work in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

In the Azure portal, you can find and manage resources by selecting **All resources** or **Resource groups** from the left pane.

Remember that a free search service is limited to three indexes, three indexers, and three data sources. To stay under the limit, you can delete these items individually in the Azure portal.

## Next step

The demo app is useful for prototyping because it simulates the end-user experience without requiring JavaScript or front-end code. As you approach the proof-of-concept stage of your own project, review the end-to-end code samples that more closely resemble a real-world app:


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-pii-detection.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-pii-detection -->

# Personally Identifiable Information (PII) Detection cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **PII Detection** skill extracts personal information from an input text and gives you the option of masking it. This skill uses the [detection models](/en-us/azure/ai-services/language-service/personally-identifiable-information/overview) provided in [Azure Language in Foundry Tools](/en-us/azure/ai-services/language-service/overview).

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.PIIDetectionSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). You can use

[Text Split skill](cognitive-search-skill-textsplit)for data chunking. Set the page length to 5000 for the best results.

## Skill parameters

Parameters are case sensitive and all are optional.

| Parameter name | Description |
|---|---|
`defaultLanguageCode` |
(Optional) The language code to apply to documents that don't specify language explicitly. If the default language code isn't specified, English (en) is the default language code. See the
|
`minimumPrecision` |
A value between 0.0 and 1.0. If the confidence score (in the `piiEntities` output) is lower than the set `minimumPrecision` value, the entity isn't returned or masked. The default is 0.0. |
`maskingMode` |
A parameter that provides various ways to mask the personal information detected in the input text. The following options are supported:
|
`maskingCharacter` |
The character used to mask the text if the `maskingMode` parameter is set to `replace` . The following option is supported: `*` (default). This parameter can only be `null` if `maskingMode` isn't set to `replace` . |
`domain` |
(Optional) A string value, if specified, sets the domain to a subset of the entity categories. Possible values include: `"phi"` (detect confidential health information only), `"none"` . |
`piiCategories` |
(Optional) If you want to specify which entities are detected and returned, use this optional parameter (defined as a list of strings) with the appropriate entity categories. This parameter can also let you detect entities that aren't enabled by default for your document language. See
|

`modelVersion`

[version of the model](/en-us/azure/ai-services/language-service/concepts/model-lifecycle)to use when calling personally identifiable information detection. It defaults to the most recent version when not specified. We recommend you don't specify this value unless it's necessary.## Skill inputs

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
`piiEntities` |
An array of complex types that contains the following fields:
See
|
`maskedText` |
This output varies depending `maskingMode` . If `maskingMode` is `replace` , output is the string result of the masking performed over the input text, as described by the `maskingMode` . If `maskingMode` is `none` , there's no output. |

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.PIIDetectionSkill",
"defaultLanguageCode": "en",
"minimumPrecision": 0.5,
"maskingMode": "replace",
"maskingCharacter": "*",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "piiEntities"
},
{
"name": "maskedText"
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
"text": "Microsoft employee with ssn 859-98-0987 is using our awesome API's."
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
"piiEntities":[
{
"text":"859-98-0987",
"type":"U.S. Social Security Number (SSN)",
"subtype":"",
"offset":28,
"length":11,
"score":0.65
}
],
"maskedText": "Microsoft employee with ssn *********** is using our awesome API's."
}
}
]
}
```


The offsets returned for entities in the output of this skill are directly returned from the [Language Service APIs](/en-us/azure/ai-services/language-service/overview), which means if you're using them to index into the original string, you should use the [StringInfo](/en-us/dotnet/api/system.globalization.stringinfo) class in .NET in order to extract the correct content. For more information, see [Multilingual and emoji support in Language service features](/en-us/azure/ai-services/language-service/concepts/multilingual-emoji-support).

## Errors and warnings

If the language code for the document is unsupported, a warning is returned and no entities are extracted. If your text is empty, a warning is returned. If your text is larger than 50,000 characters, only the first 50,000 characters are analyzed and a warning is issued.

If the skill returns a warning, the output `maskedText`

may be empty, which can impact any downstream skills that expect the output. For this reason, be sure to investigate all warnings related to missing output when writing your skillset definition.
