---
merged_at: 2026-01-25T02:11:58.375247
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-text-translation.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-text-translation -->

# Text Translation cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Text Translation** skill evaluates text and, for each record, returns the text translated to the specified target language. This skill uses the [Translator Text API v3.0](/en-us/azure/ai-services/translator/reference/v3-0-translate) available in Foundry Tools.

This capability is useful if you expect that your documents may not all be in one language, in which case you can normalize the text to a single language before indexing for search by translating it. It's also useful for localization use cases, where you might want to have copies of the same text available in multiple languages.

The [Translator Text API v3.0](/en-us/azure/ai-services/translator/reference/v3-0-reference) is a non-regional Foundry Tool, meaning that your data isn't guaranteed to stay in the same region as your Azure AI Search or attached Microsoft Foundry resource.

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

When using this skill, all documents in the source are processed and billed for translation, even if the source and target languages are the same. This behavior is useful for multi-language support within the same document, but it can result in unnecessary processing. To avoid unexpected billing charges from documents that don't need processing, move them out of the data source container prior to running the skill.

## @odata.type

Microsoft.Skills.Text.TranslationSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the text translation skill, consider using the

[Text Split skill](cognitive-search-skill-textsplit). If you do use a text split skill, set the page length to 5000 for the best performance.

## Skill parameters

Parameters are case sensitive.

| Inputs | Description |
|---|---|
| defaultToLanguageCode | (Required) The language code to translate documents into for documents that don't specify the "to" language explicitly. See the
|
| defaultFromLanguageCode | (Optional) The language code to translate documents from for documents that don't specify the "from" language explicitly. If the defaultFromLanguageCode isn't specified, the automatic language detection provided by the Translator Text API will be used to determine the "from" language. See the
|
| suggestedFrom | (Optional) The language code to translate documents from if `fromLanguageCode` or `defaultFromLanguageCode` are unspecified, and the automatic language detection is unsuccessful. If the suggestedFrom language isn't specified, English (en) will be used as the suggestedFrom language. See the
|

## Skill inputs

| Input name | Description |
|---|---|
| text | The text to be translated. |
| toLanguageCode | A string indicating the language the text should be translated to. If this input isn't specified, the defaultToLanguageCode will be used to translate the text. See the
|
| fromLanguageCode | A string indicating the current language of the text. If this parameter isn't specified, the defaultFromLanguageCode (or automatic language detection if the defaultFromLanguageCode isn't provided) will be used to translate the text. See the
|

## Skill outputs

| Output name | Description |
|---|---|
| translatedText | The string result of the text translation from the translatedFromLanguageCode to the translatedToLanguageCode. |
| translatedToLanguageCode | A string indicating the language code the text was translated to. Useful if you're translating to multiple languages and want to be able to keep track of which text is which language. |
| translatedFromLanguageCode | A string indicating the language code the text was translated from. Useful if you opted for the automatic language detection option as this output will give you the result of that detection. |

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.TranslationSkill",
"defaultToLanguageCode": "fr",
"suggestedFrom": "en",
"context": "/document",
"inputs": [
{
"name": "text",
"source": "/document/text"
}
],
"outputs": [
{
"name": "translatedText",
"targetName": "translatedText"
},
{
"name": "translatedFromLanguageCode",
"targetName": "translatedFromLanguageCode"
},
{
"name": "translatedToLanguageCode",
"targetName": "translatedToLanguageCode"
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
"text": "We hold these truths to be self-evident, that all men are created equal."
}
},
{
"recordId": "2",
"data":
{
"text": "Estamos muy felices de estar con ustedes."
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
"data":
{
"translatedText": "Nous tenons ces vérités pour évidentes, que tous les hommes sont créés égaux.",
"translatedFromLanguageCode": "en",
"translatedToLanguageCode": "fr"
}
},
{
"recordId": "2",
"data":
{
"translatedText": "Nous sommes très heureux d'être avec vous.",
"translatedFromLanguageCode": "es",
"translatedToLanguageCode": "fr"
}
}
]
}
```


## Errors and warnings

If you provide an unsupported language code for either the "to" or "from" language, an error is generated, and text isn't translated. If your text is empty, a warning will be produced. If your text is larger than 50,000 characters, only the first 50,000 characters will be translated, and a warning will be issued.


---

<!-- DOCUMENTO FUSIONADO: search-get-started-arm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-arm -->

# Quickstart: Deploy Azure AI Search using an Azure Resource Manager template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use an Azure Resource Manager (ARM) template to deploy an Azure AI Search service in the Azure portal.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Only those properties included in the template are used in the deployment. If more customization is required, such as [setting up network security](search-security-overview#network-security), you can update the service as a post-deployment task. To customize an existing service with the fewest steps, use [Azure CLI](search-manage-azure-cli) or [Azure PowerShell](search-manage-powershell). If you're evaluating preview features, use the [Management REST API](search-manage-rest).

Assuming your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template will open in the Azure portal.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/azure-search-create/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.5.6.12127",
"templateHash": "11257266040777038564"
}
},
"parameters": {
"name": {
"type": "string",
"maxLength": 60,
"minLength": 2,
"metadata": {
"description": "Service name must only contain lowercase letters, digits or dashes, cannot use dash as the first two or last one characters, cannot contain consecutive dashes, and is limited between 2 and 60 characters in length."
}
},
"sku": {
"type": "string",
"defaultValue": "standard",
"metadata": {
"description": "The pricing tier of the search service you want to create (for example, basic or standard)."
},
"allowedValues": [
"free",
"basic",
"standard",
"standard2",
"standard3",
"storage_optimized_l1",
"storage_optimized_l2"
]
},
"replicaCount": {
"type": "int",
"defaultValue": 1,
"maxValue": 12,
"minValue": 1,
"metadata": {
"description": "Replicas distribute search workloads across the service. You need at least two replicas to support high availability of query workloads (not applicable to the free tier)."
}
},
"partitionCount": {
"type": "int",
"defaultValue": 1,
"allowedValues": [
1,
2,
3,
4,
6,
12
],
"metadata": {
"description": "Partitions allow for scaling of document count as well as faster indexing by sharding your index over multiple search units."
}
},
"hostingMode": {
"type": "string",
"defaultValue": "default",
"allowedValues": [
"default",
"highDensity"
],
"metadata": {
"description": "Applicable only for SKUs set to standard3. You can set this property to enable a single, high density partition that allows up to 1000 indexes, which is much higher than the maximum indexes allowed for any other SKU."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "Location for all resources."
}
}
},
"resources": [
{
"type": "Microsoft.Search/searchServices",
"apiVersion": "2020-08-01",
"name": "[parameters('name')]",
"location": "[parameters('location')]",
"sku": {
"name": "[parameters('sku')]"
},
"properties": {
"replicaCount": "[parameters('replicaCount')]",
"partitionCount": "[parameters('partitionCount')]",
"hostingMode": "[parameters('hostingMode')]"
}
}
]
}
```


The Azure resource defined in this template:

[Microsoft.Search/searchServices](/en-us/azure/templates/Microsoft.Search/searchServices): create an Azure AI Search service

## Deploy the template

Select the following image to sign in to Azure and open a template. The template creates an Azure AI Search resource.

The Azure portal displays a form that allows you to easily provide parameter values. Some parameters are prefilled with the default values from the template. Provide your subscription, resource group, location, and service name. If you want to use Foundry Tools in an [AI enrichment](cognitive-search-concept-intro) pipeline, such as analyzing binary image files for text, choose a location that offers both Azure AI Search and Foundry Tools. Unless you use a keyless connection (preview), your Azure AI Search service and Microsoft Foundry resource must be in the same region for AI enrichment workloads. After you complete the form, agree to the terms and conditions, and then select the purchase button to complete your deployment.

## Review deployed resources

When your deployment is complete, you can access your new resource group and new search service in the Azure portal.

## Clean up resources

Other Azure AI Search quickstarts and tutorials build upon this quickstart. If you plan to continue on to work with subsequent quickstarts and tutorials, you may wish to leave this resource in place. When no longer needed, you can delete the resource group, which deletes the Azure AI Search service and related resources.

## Related content

In this quickstart, you created an Azure AI Search service using an ARM template and then validated the deployment. To learn more about Azure AI Search and Azure Resource Manager, see the following articles:
