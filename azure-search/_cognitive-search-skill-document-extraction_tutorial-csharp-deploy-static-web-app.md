---
merged_at: 2026-01-25T02:11:58.407489
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-document-extraction.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-document-extraction -->

# Document Extraction cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Document Extraction** skill extracts content from a file in the [enrichment pipeline](cognitive-search-concept-intro). By default, content extraction or retrieval is built into the enrichment pipeline. However, by using the Document Extraction skill, you can control how parameters are set, and how extracted content is named in the enrichment tree.

For [vector](vector-search-overview) and [multimodal search](multimodal-search-overview), Document Extraction combined with the [Text Split skill](cognitive-search-skill-textsplit) is more affordable than other [data chunking approaches](vector-search-how-to-chunk-documents). The following tutorials demonstrate skill usage for different scenarios:

Note

This skill isn't bound to Foundry Tools and has no Foundry Tools key requirement.

This skill extracts text and images. Text extraction is free. Image extraction is [billable by Azure AI Search](https://azure.microsoft.com/pricing/details/search/). On a free search service, the cost of 20 transactions per indexer per day is absorbed so that you can complete quickstarts, tutorials, and small projects at no charge. For basic and higher tiers, image extraction is billable.

## @odata.type

Microsoft.Skills.Util.DocumentExtractionSkill

## Supported document formats

The DocumentExtractionSkill can extract text from the following document formats:

- CSV (see
[Indexing CSV blobs](search-how-to-index-azure-blob-csv)) - EML
- EPUB
- GZ
- HTML
- JSON (see
[Indexing JSON blobs](search-how-to-index-azure-blob-json)) - KML (XML for geographic representations)
- Markdown
- Microsoft Office formats: DOCX/DOC/DOCM, XLSX/XLS/XLSM, PPTX/PPT/PPTM, MSG (Outlook emails), XML (both 2003 and 2006 WORD XML)
- Open Document formats: ODT, ODS, ODP
- Plain text files (see also
[Indexing plain text](search-how-to-index-azure-blob-plaintext)) - RTF
- XML
- ZIP

## Skill parameters

Parameters are case sensitive.

| Inputs | Allowed Values | Description |
|---|---|---|
`parsingMode` |
`default` `text` `json` |
Set to `default` for document extraction from files that aren't pure text or json. For source files that contain mark up (such as PDF, HTML, RTF, and Microsoft Office files), use the default to extract just the text, minus any markup language or tags. If `parsingMode` isn't defined explicitly, it will be set to `default` . Set to `text` if source files are TXT. This parsing mode improves performance on plain text files. If files include markup, this mode will preserve the tags in the final output. Set to `json` to extract structured content from json files. |
`dataToExtract` |
`contentAndMetadata` `allMetadata` |
Set to `contentAndMetadata` to extract all metadata and textual content from each file. If `dataToExtract` isn't defined explicitly, it will be set to `contentAndMetadata` . Set to `allMetadata` to extract only the
|
`configuration` |
See below. | A dictionary of optional parameters that adjust how the document extraction is performed. See the below table for descriptions of supported configuration properties. |

| Configuration Parameter | Allowed Values | Description |
|---|---|---|
`imageAction` |
`none` `generateNormalizedImages` `generateNormalizedImagePerPage` |
Set to `none` to ignore embedded images or image files in the data set, or if the source data doesn't include image files. This is the default. For
`generateNormalizedImages` to have the skill create an array of normalized images as part of
`parsingMode` is set to `default` and `dataToExtract` is set to `contentAndMetadata` . A normalized image refers to extra processing resulting in uniform image output, sized and rotated to promote consistent rendering when you include images in visual search results (for example, same-size photographs in a graph control as seen in the
`generateNormalizedImagePerPage` , PDF files are treated differently in that instead of extracting embedded images, each page is rendered as an image and normalized accordingly. Non-PDF file types are treated the same as if `generateNormalizedImages` was set. |
`normalizedImageMaxWidth` |
Any integer between 50-10000 | The maximum width (in pixels) for normalized images generated. The default is 2000. |
`normalizedImageMaxHeight` |
Any integer between 50-10000 | The maximum height (in pixels) for normalized images generated. The default is 2000. |

Note

The default of 2000 pixels for the normalized images maximum width and height is based on the maximum sizes supported by the [OCR skill](cognitive-search-skill-ocr) and the [image analysis skill](cognitive-search-skill-image-analysis). The [OCR skill](cognitive-search-skill-ocr) supports a maximum width and height of 4200 for non-English languages, and 10000 for English. If you increase the maximum limits, processing could fail on larger images depending on your skillset definition and the language of the documents.

## Skill inputs

| Input name | Description |
|---|---|
`file_data` |
The file that content should be extracted from. |

The "file_data" input must be an object defined as:

```
{
"$type": "file",
"data": "BASE64 encoded string of the file"
}
```


Alternatively, it can be defined as:

```
{
"$type": "file",
"url": "URL to download file",
"sasToken": "OPTIONAL: SAS token for authentication if the URL provided is for a file in blob storage"
}
```


The file reference object can be generated one of three ways:

Setting the

`allowSkillsetToReadFileData`

parameter on your indexer definition to "true". This creates a path`/document/file_data`

that is an object representing the original file data downloaded from your blob data source. This parameter only applies to files in Blob storage.Setting the

`imageAction`

parameter on your indexer definition to a value other than`none`

. This creates an array of images that follows the required convention for input to this skill if passed individually (that is,`/document/normalized_images/*`

).Having a custom skill return a json object defined EXACTLY as above. The

`$type`

parameter must be set to exactly`file`

and the`data`

parameter must be the base 64 encoded byte array data of the file content, or the`url`

parameter must be a correctly formatted URL with access to download the file at that location.

## Skill outputs

| Output name | Description |
|---|---|
`content` |
The textual content of the document. |
`normalized_images` |
When the `imageAction` is set to a value other than `none` , the new normalized_images field contains an array of images. See
|

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Util.DocumentExtractionSkill",
"parsingMode": "default",
"dataToExtract": "contentAndMetadata",
"configuration": {
"imageAction": "generateNormalizedImages",
"normalizedImageMaxWidth": 2000,
"normalizedImageMaxHeight": 2000
},
"context": "/document",
"inputs": [
{
"name": "file_data",
"source": "/document/file_data"
}
],
"outputs": [
{
"name": "content",
"targetName": "extracted_content"
},
{
"name": "normalized_images",
"targetName": "extracted_normalized_images"
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
"file_data": {
"$type": "file",
"data": "aGVsbG8="
}
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
"data": {
"content": "hello",
"normalized_images": []
}
}
]
}
```


---

<!-- DOCUMENTO FUSIONADO: tutorial-csharp-deploy-static-web-app.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/tutorial-csharp-deploy-static-web-app -->

# Step 3 - Deploy the search-enabled .NET website

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Deploy the search-enabled website as an Azure Static Web Apps site. This deployment includes both the React app for the web pages, and the Function app for search operations.

The static web app pulls the information and files for deployment from GitHub using your fork of the azure-search-static-web-app repository.

## Create a Static Web App in Visual Studio Code

In Visual Studio Code, make sure you're at the repository root, and not the bulk-insert folder (for example,

`azure-search-static-web-app`

).Select

**Azure**from the Activity Bar, then open**Resources**from the side bar.Right-click

**Static Web Apps**and then select**Create Static Web App (Advanced)**. If you don't see this option, verify that you have the Azure Functions extension for Visual Studio Code.If you see a pop-up window asking you to commit your changes, don't do this. The secrets from the bulk import step shouldn't be committed to the repository.

To roll back the changes, in Visual Studio Code select the Source Control icon in the Activity bar, then select each changed file in the Changes list and select the

**Discard changes**icon.Follow the prompts to create the static web app:

Prompt Enter Select a resource group for new resources. Create a new resource group for the static app. Enter the name for the new Static Web App. Give your static app a name, such as `my-demo-static-web-app`

.Select a SKU Select the free SKU for this tutorial. Select a location for new resources. Choose a region near you. Choose build preset to configure default project structure. Select **Custom**.Select the location of your client application code `client`


This is the path, from the root of the repository, to your static web app.Enter the path of your build output... `build`


This is the path, from your static web app, to your generated files.If you get an error about an incorrect region, make sure the resource group and static web app resource are in one of the supported regions listed in the error response.

When the static web app is created, a GitHub workflow YML file is also created locally and on GitHub in your fork. This workflow executes in your fork, building and deploying the static web app and functions.

Check the status of static web app deployment using any of these approaches:

Select

**Open Actions in GitHub**from the Notifications. This opens a browser window pointed to your forked repo.Select the

**Actions**tab in your forked repository. You should see a list of all workflows on your fork.Select the

**Azure: Activity Log**in Visual Code. You should see a message similar to the following screenshot.


## Get the Azure AI Search query key in Visual Studio Code

While you might be tempted to reuse your search admin key for query purposes that isn't following the principle of least privilege. The Azure Function should use the query key to conform to least privilege.

In Visual Studio Code, open a new terminal window.

Get the query API key with this Azure CLI command:

`az search query-key list --resource-group YOUR-SEARCH-SERVICE-RESOURCE-GROUP --service-name YOUR-SEARCH-SERVICE-NAME`

Keep this query key to use in the next section. The query key authorizes read access to a search index.


## Add environment variables in Azure portal

The Azure Function app won't return search data until the search secrets are in settings.

Select

**Azure**from the Activity Bar.Right-click on your Static Web Apps resource then select

**Open in Portal**.Select

**Environment variables**then select**+ Add application setting**.Add each of the following settings:

Setting Your Search resource value SearchApiKey Your search query key SearchServiceName Your search resource name SearchIndexName `good-books`

SearchFacets `authors*,language_code`

Azure AI Search requires different syntax for filtering collections than it does for strings. Add a

`*`

after a field name to denote that the field is of type`Collection(Edm.String)`

. This allows the Azure Function to add filters correctly to queries.Check your settings to make sure they look like the following screenshot.

Return to Visual Studio Code.

Refresh your static web app to see the application settings and functions.


If you don't see the application settings, revisit the steps for updating and relaunching the GitHub workflow.

## Use search in your static web app

In Visual Studio Code, open the

[Activity bar](https://code.visualstudio.com/docs/getstarted/userinterface), and select the Azure icon.In the Side bar,

**right-click on your Azure subscription**under the`Static Web Apps`

area and find the static web app you created for this tutorial.Right-click the static web app name and select

**Browse site**.Select

**Open**in the pop-up dialog.In the website search bar, enter a search query such as

`code`

, so the suggest feature suggests book titles. Select a suggestion or continue entering your own query. Press enter when you've completed your search query.Review the results then select one of the books to see more details.


## Troubleshooting

If the web app didn't deploy or work, use the following list to determine and fix the issue:

**Did the deployment succeed?**In order to determine if your deployment succeeded, you need to go to

*your*fork of the sample repo and review the success or failure of the GitHub action. There should be only one action and it should have static web app settings for the`app_location`

,`api_location`

, and`output_location`

. If the action didn't deploy successfully, dive into the action logs and look for the last failure.**Does the client (front-end) application work?**You should be able to get to your web app and it should successfully display. If the deployment succeeded but the website doesn't display, this might be an issue with how the static web app is configured for rebuilding the app, once it is on Azure.

**Does the API (serverless back-end) application work?**You should be able to interact with the client app, searching for books and filtering. If the form doesn't return any values, open the browser's developer tools, and determine if the HTTP calls to the API were successful. If the calls weren't successful, the most likely reason if the static web app configurations for the API endpoint name and search query key are incorrect.

If the path to the Azure function code (

`api_location`

) isn't correct in the YML file, the application loads but won't call any of the functions that provide integration with Azure AI Search. Revisit the deployment section to make sure paths are correct.

## Clean up resources

To clean up the resources created in this tutorial, delete the resource group or individual resources.

In Visual Studio Code, open the

[Activity bar](https://code.visualstudio.com/docs/getstarted/userinterface), and select the Azure icon.In the Side bar,

**right-click on your Azure subscription**under the`Static Web Apps`

area and find the app you created for this tutorial.Right-click the app name then select

**Delete**.If you no longer want the GitHub fork of the sample, remember to delete that on GitHub. Go to your fork's

**Settings**then delete the repository.To delete Azure AI Search,

[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)and select**Delete**at the top of the page.
