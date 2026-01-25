---
merged_at: 2026-01-25T02:11:58.481751
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-create-service-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-create-service-portal -->

# Create an Azure AI Search service in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure AI Search](search-what-is-azure-search) is an information retrieval platform for the enterprise. It supports traditional search and conversational, AI-driven search for "chat with your data" experiences across your proprietary content.

The easiest way to create a search service is through the [Azure portal](https://portal.azure.com/), which is covered in this article.

You can also use:

## Before you start

Some properties are fixed for the lifetime of the search service. Before you create your service, decide on the following properties:

| Property | Description |
|---|---|
|

[Region](search-region-support)[Tier](search-sku-tier)[switch between Basic and Standard (S1, S2, and S3) tiers](search-capacity-planning#change-your-pricing-tier).[Compute type](search-security-overview#data-in-use)## Subscribe to Azure

Azure AI Search requires a free or Standard Azure subscription.

To try Azure AI Search for free, [start a trial subscription](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and then [create your search service on the Free tier](#choose-a-tier). Each Azure subscription can have one free search service, which is intended for short-term, non-production evaluation of the product. You can complete all of our quickstarts and most of our tutorials on the Free tier. For more information, see [Try Azure AI Search for free](search-try-for-free).

Important

To make room for other services, Microsoft might delete free services that are inactive for an extended period of time.

## Find the Azure AI Search offering

Sign in to the

[Azure portal](https://portal.azure.com/).In the upper-left corner of your dashboard, select

**Create a resource**.Use the search box to find

**Azure AI Search**.

## Choose a subscription

If you have multiple Azure subscriptions, choose one for your search service.

If you're implementing [customer-managed encryption](search-security-manage-encryption-keys) or using other features that rely on managed service identities for [external data access](search-indexer-securing-resources), choose the same subscription you use for Azure Key Vault or other services that use managed identities.

## Set a resource group

A resource group is a container that holds related resources for an Azure solution. Use it to consolidate same-solution resources, monitor costs, and check the creation date of your search service.

Over time, you can track current and projected costs for individual resources and for the overall resource group. The following screenshot shows the cost information that's available when you combine multiple resources into one group:

## Name your service

Enter a name for your search service. The name is part of the endpoint against which API calls are issued: `https://your-service-name.search.windows.net`

. For example, if you enter `myservice`

, the endpoint becomes `https://myservice.search.windows.net`

.

When naming your service, follow these rules:

- Use a name that's unique within the
`search.windows.net`

namespace. - Use between 2 and 60 characters.
- Use only lowercase letters, digits, and dashes (-).
- Don't use dashes as the first two characters or the last character.
- Don't use consecutive dashes.

Tip

If you have multiple search services, it's helpful to include the region in the service name. For example, when deciding how to combine or attach resources, the name `myservice-westus`

might save you a trip to the Properties page.

## Choose a region

Important

Due to high demand, Azure AI Search is currently unavailable for new instances in some regions.

If you use multiple Azure services, putting all of them in the same region minimizes or voids bandwidth charges. There are no charges for data egress among same-region services.

In most cases, choose a region near you, unless any of the following apply:

Your nearest region is

[at capacity](search-region-support), which is indicated by the footnotes of each table. The Azure portal has the advantage of hiding unavailable regions and tiers during resource setup.You want to use integrated data chunking and vectorization or built-in skills for AI enrichment. Integrated operations have region requirements.

You want to use Azure Storage for indexer-based indexing, or you want to store application data that isn't in an index. Debug session state, enrichment caches, and knowledge stores are Azure AI Search features that depend on Azure Storage. The region you choose for Azure Storage has implications for network security. If you're setting up a firewall, you should place the resources in separate regions. For more information, see

[Outbound connections from Azure AI Search to Azure Storage](search-indexer-securing-resources).

### Checklist for choosing a region

Is Azure AI Search available in a nearby region? Check the

[list of supported regions](search-region-support).Do you have a specific tier in mind? Check

[region availability by tier](search-sku-tier#region-availability-by-tier).Do you have business continuity and disaster recovery (BCDR) requirements? Create two or more search services in different Azure regions, each with two or more replicas so that they can be spread across multiple

[availability zones](/en-us/azure/reliability/reliability-ai-search#availability-zone-support). For example, if you're operating in North America, you might choose East US and West US, or North Central US and South Central US, for each search service. For more information, see[Multi-region deployments in Azure AI Search](search-multi-region).Do you need

[AI enrichment](cognitive-search-concept-intro),[integrated data chunking and vectorization](vector-search-integrated-vectorization), or[multimodal search](multimodal-search-overview)powered by Foundry Tools? For billing purposes, you must[attach your Microsoft Foundry resource](cognitive-search-attach-cognitive-services)to your search service via a keyless connection (preview) or key-based connection. Key-based connections require both services to be in the same region.Check

[Azure AI Search regions](search-region-support#azure-public-regions). If you're using OCR, entity recognition, or other skills backed by Azure AI, the**AI enrichment**column indicates whether Azure AI Search and Microsoft Foundry are in the same region.Check

[Azure Vision in Foundry Tools regions](/en-us/azure/ai-services/computer-vision/overview-image-analysis#region-availability)for multimodal APIs that enable text and image vectorization. These APIs are powered by Azure Vision and accessed through a Microsoft Foundry resource. However, they're generally available in fewer regions than the Microsoft Foundry resource itself.


## Choose a tier

Azure AI Search is offered in multiple [pricing tiers](https://azure.microsoft.com/pricing/details/search/):

- Free
- Basic
- Standard
- Storage Optimized

Each tier has its own [capacity and limits](search-limits-quotas-capacity), and some features are tier dependent. For information about computing characteristics, feature availability, and region availability, see [Choose a service tier for Azure AI Search](search-sku-tier).

The Basic and Standard tiers are the most common for production workloads, but many customers start with the Free tier. The billable tiers differ primarily in partition size, partition speed, and limits on the number of objects you can create.

Note

Services created after April 3, 2024 have larger partitions and higher vector quotas at every billable tier.

## Choose a compute type

The compute type determines the virtualization and security model used to deploy your search service. There are two compute types:

**Default**(base cost) deploys your search service on standard Azure infrastructure, encrypting data at rest and in transit but not in use. Recommended for most search workloads.**Confidential**(10% surcharge) uses[Azure confidential computing](/en-us/azure/confidential-computing/use-cases-scenarios)to isolate processing in a hardware-based trusted execution environment, protecting unencrypted data in use from unauthorized access. Recommended only if you have advanced privacy, compliance, or regulatory requirements.

Confidential computing has limited regional availability, disables or restricts certain features, and increases the cost of running your search service. For a detailed comparison of both compute types, see [Data in use](search-security-overview#data-in-use).

## Create your service

After providing the necessary inputs, create your search service.

Your service is deployed within minutes, and you can monitor its progress with Azure notifications. Consider pinning the service to your dashboard for easy access in the future.

## Configure authentication

When you create a search service, key-based authentication is the default, but it's not the most secure option. We recommend that you replace it with role-based access.

To enable role-based access for your service:

Go to your search service in the

[Azure portal](https://portal.azure.com/).From the left pane, select

**Settings**>**Keys**. You can connect to your service using[API keys](search-security-api-keys),[Azure roles](search-security-rbac), or both. Select**Both**until you assign roles, after which you can select**Role-based access control**.

## Scale your service

After deploying your search service, you can [scale it to meet your needs](search-limits-quotas-capacity). Azure AI Search offers two scaling dimensions: *replicas* and *partitions*. Replicas allow your service to handle a higher load of search queries, while partitions allow your service to store and search through more documents.

Scaling is available only on billable tiers. On the Free tier, you can't scale your service or configure replicas and partitions.

Important

Your service must have [two replicas for read-only SLA and three replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Adding resources will increase your monthly bill. Use the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) to understand the billing implications. You can adjust resources based on load, such as increasing resources for initial indexing and decreasing them later for incremental indexing.

To scale your service:

Go to your search service in the

[Azure portal](https://portal.azure.com/).From the left pane, select

**Settings**>**Scale**.Use the sliders to add replicas and partitions.


## When to add a second service

Most customers use a single search service at a tier [sufficient for the expected load](search-capacity-planning). One service can host multiple indexes, each isolated from the others, within the [maximum limits of your chosen tier](search-limits-quotas-capacity#index-limits). In Azure AI Search, you can direct requests to only one index, reducing the chance of retrieving data from other indexes in the same service.

However, you might need a second service for the following operational requirements:

- Region outages. In the unlikely event of a full region outage, Azure AI Search doesn't provide instant failover. You must implement your own multi-region solution and failover approach. For more information, see
[Multi-region deployments in Azure AI Search](search-multi-region). [Multitenant architectures](search-modeling-multitenant-saas-applications)that require two or more services.- Globally deployed applications that require services in each geography to minimize latency.

Note

In Azure AI Search, you can't separate indexing and querying operations, so don't create multiple services for separate workloads. An index is always queried on the service in which it was created, and you can't copy an index to another service.

A second service isn't required for high availability. You achieve high availability for queries by using two or more replicas in the same service. Because the replicas are updated sequentially, at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## Add more services to your subscription

Azure AI Search limits the [number of search services](search-limits-quotas-capacity#subscription-limits) you can initially create in a subscription. If you reach your limit, you can request more quotas.

You must have Owner or Contributor permissions for the subscription to request quota. Depending on your region and data center capacity, you might be able to automatically request quota to add services to your subscription. If the request fails, reduce the number or file a support ticket. Expect a one-month turnaround for a large quota increase, such as more than 30 extra services.

To request more subscription quota:

Go to your dashboard in the

[Azure portal](https://portal.azure.com/).Use the search box to find the

**Quotas**service.On the

**Overview**tab, select the**Search**tile.Set filters to review the existing quota for search services in your current subscription. We recommend filtering by usage.

Next to the tier and region that need more quotas, select

**Request adjustment**.In

**New Quota Request**, enter a new limit for your subscription quota. The new limit must be greater than your current limit. If regional capacity is constrained, your request won't be automatically approved, and an incident report will be generated on your behalf for investigation and resolution.Submit your request.

Monitor notifications in the Azure portal for updates on the new limit. Most requests are approved within 24 hours.


## Next steps

Now that you've deployed your search service, continue in the Azure portal to create your first index:

Want to optimize and save on your cloud spending?


---

<!-- DOCUMENTO FUSIONADO: search-synapseml-cognitive-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-synapseml-cognitive-services -->

# Tutorial: Index large data from Apache Spark using SynapseML and Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Azure AI Search tutorial, you learn how to index and query large data loaded from a Spark cluster. You set up a Jupyter Notebook to:

- Load various forms (invoices) into a data frame in an Apache Spark session
- Analyze the forms to determine their features
- Assemble the resulting output into a tabular data structure
- Write the output to a search index hosted in Azure AI Search
- Explore and query over the content you created

This tutorial takes a dependency on [SynapseML](https://microsoft.github.io/SynapseML/), an open-source library that supports massively parallel machine learning over big data. In SynapseML, search indexing and machine learning are exposed through *transformers* that perform specialized tasks. Transformers tap into a wide range of AI capabilities. In this exercise, you use the **AzureSearchWriter** APIs for analysis and AI enrichment.

Although Azure AI Search has native [AI enrichment](cognitive-search-concept-intro), this tutorial shows you how to access AI capabilities outside of Azure AI Search. By using SynapseML instead of indexers or skills, you're not subject to data limits or other constraints associated with those objects.

Tip

Watch a [short video of this demo](https://www.youtube.com/watch?v=iXnBLwp7f88). The video expands on this tutorial with more steps and visuals.

## Prerequisites

You need the `synapseml`

library and several Azure resources. If possible, use the same subscription and region for your Azure resources and put everything into one resource group for simple cleanup later. The following links are for portal installs. The sample data is imported from a public site.

[SynapseML package](https://microsoft.github.io/SynapseML/docs/Get%20Started/Install%20SynapseML/#python)1[Azure AI Search](search-create-service-portal)(any tier)2[Microsoft Foundry resource](/en-us/azure/ai-services/multi-service-resource)(any tier) with an**API Kind**of`AIServices`

3[Azure Databricks](/en-us/azure/databricks/scenarios/quickstart-create-databricks-workspace-portal?tabs=azure-portal)(any tier) with Apache Spark 3.3.0 runtime4

1 This link resolves to a tutorial for loading the package.

2 You can use the Free tier to index the sample data, but [choose a higher tier](search-sku-tier) if your data volumes are large. For billable tiers, provide the [search API key](search-security-api-keys#find-existing-keys) in the [Set up dependencies](#set-up-dependencies) step further on.

3 This tutorial uses Document Intelligence and Translator from Foundry Tools. In the instructions that follow, provide a [Foundry resource](/en-us/azure/ai-services/multi-service-resource) key and the region. The same key works for both services. **For this tutorial, it's important that you use a Foundry resource with an API kind of AIServices**. You can check the API kind in the Azure portal on the

**Overview**page of your Foundry resource. For more information about API kind, see

[Attach a Foundry resource in Azure AI Search](cognitive-search-attach-cognitive-services).

4 In this tutorial, Azure Databricks provides the Spark computing platform. We used the [portal instructions](/en-us/azure/databricks/scenarios/quickstart-create-databricks-workspace-portal?tabs=azure-portal) to set up the cluster and workspace.

Note

The preceding Azure resources support security features in the Microsoft Identity platform. For simplicity, this tutorial assumes key-based authentication, using endpoints and keys copied from the Azure portal pages of each service. If you implement this workflow in a production environment or share the solution with others, remember to replace hard-coded keys with integrated security or encrypted keys.

## Create a Spark cluster and notebook

In this section, you create a cluster, install the `synapseml`

library, and create a notebook to run the code.

In the Azure portal, find your Azure Databricks workspace and select

**Launch workspace**.On the left menu, select

**Compute**.Select

**Create compute**.Accept the default configuration. It takes several minutes to create the cluster.

Verify the cluster is operational and running. A green dot by the cluster name confirms its status.

After the cluster is created, install the

`synapseml`

library:Select

**Libraries**from the tabs at the top of the cluster's page.Select

**Install new**.Select

**Maven**.In

**Coordinates**, search for`com.microsoft.azure:synapseml_2.12:1.0.9`

.Select

**Install**.

On the left menu, select

**Create**>**Notebook**.Give the notebook a name, select

**Python**as the default language, and select the cluster that has the`synapseml`

library.Create seven consecutive cells. In the following sections, you paste code in these cells.


## Set up dependencies

Paste the following code into the first cell of your notebook.

Replace the placeholders with endpoints and access keys for each resource. Provide a name for a new search index to be created for you. No other modifications are required, so run the code when you're ready.

This code imports multiple packages and sets up access to the Azure resources used in this tutorial.

```
import os
from pyspark.sql.functions import udf, trim, split, explode, col, monotonically_increasing_id, lit
from pyspark.sql.types import StringType
from synapse.ml.core.spark import FluentAPI
cognitive_services_key = "placeholder-azure-ai-foundry-key"
cognitive_services_region = "placeholder-azure-ai-foundry-region"
search_service = "placeholder-search-service-name"
search_key = "placeholder-search-service-admin-api-key"
search_index = "placeholder-for-new-search-index-name"
```


## Load data into Spark

Paste the following code into the second cell. No modifications are required, so run the code when you're ready.

This code loads a few external files from an Azure storage account. The files are various invoices that are read into a data frame.

```
def blob_to_url(blob):
[prefix, postfix] = blob.split("@")
container = prefix.split("/")[-1]
split_postfix = postfix.split("/")
account = split_postfix[0]
filepath = "/".join(split_postfix[1:])
return "https://{}/{}/{}".format(account, container, filepath)
df2 = (spark.read.format("binaryFile")
.load("wasbs://publicwasb@mmlspark.blob.core.windows.net/form_subset/*")
.select("path")
.limit(10)
.select(udf(blob_to_url, StringType())("path").alias("url"))
.cache())
display(df2)
```


## Add document intelligence

Paste the following code into the third cell. No modifications are required, so run the code when you're ready.

This code loads the [AnalyzeInvoices transformer](https://mmlspark.blob.core.windows.net/docs/1.0.9/pyspark/synapse.ml.services.form.html#module-synapse.ml.services.form.AnalyzeInvoices) and passes a reference to the data frame containing the invoices. It calls the prebuilt [invoice model](/en-us/azure/ai-services/document-intelligence/concept-invoice) of Azure Document Intelligence in Foundry Tools to extract information from the invoices.

```
from synapse.ml.services import AnalyzeInvoices
analyzed_df = (AnalyzeInvoices()
.setSubscriptionKey(cognitive_services_key)
.setLocation(cognitive_services_region)
.setImageUrlCol("url")
.setOutputCol("invoices")
.setErrorCol("errors")
.setConcurrency(5)
.transform(df2)
.cache())
display(analyzed_df)
```


The output should look similar to the following screenshot. Notice how the forms analysis is packed into a densely structured column, which is difficult to work with. The next transformation resolves this issue by parsing the column into rows and columns.


## Restructure document intelligence output

Paste the following code into the fourth cell and run it. No modifications are required.

This code loads [FormOntologyLearner](https://mmlspark.blob.core.windows.net/docs/0.10.0/pyspark/synapse.ml.cognitive.html#module-synapse.ml.cognitive.FormOntologyTransformer), a transformer that analyzes the output of Azure Document Intelligence transformers and infers a tabular data structure. The output of AnalyzeInvoices is dynamic and varies based on the features detected in your content. Furthermore, the transformer consolidates the output into a single column. Because the output is dynamic and consolidated, it's difficult to use in downstream transformations that require more structure.

FormOntologyLearner extends the utility of the AnalyzeInvoices transformer by looking for patterns that can be used to create a tabular data structure. Organizing the output into multiple columns and rows makes the content consumable in other transformers, like AzureSearchWriter.

```
from synapse.ml.cognitive import FormOntologyLearner
itemized_df = (FormOntologyLearner()
.setInputCol("invoices")
.setOutputCol("extracted")
.fit(analyzed_df)
.transform(analyzed_df)
.select("url", "extracted.*").select("*", explode(col("Items")).alias("Item"))
.drop("Items").select("Item.*", "*").drop("Item"))
display(itemized_df)
```


Notice how this transformation recasts the nested fields into a table, which enables the next two transformations. This screenshot is trimmed for brevity. If you're following along in your own notebook, you have 19 columns and 26 rows.


## Add translations

Paste the following code into the fifth cell. No modifications are required, so run the code when you're ready.

This code loads [Translate](https://microsoft.github.io/SynapseML/docs/Explore%20Algorithms/AI%20Services/Overview/#translator-sample), a transformer that calls Azure Translator in Foundry Tools. The original text, which is in English in the "Description" column, is machine-translated into various languages. All of the output is consolidated into the "output.translations" array.

```
from synapse.ml.cognitive import Translate
translated_df = (Translate()
.setSubscriptionKey(cognitive_services_key)
.setLocation(cognitive_services_region)
.setTextCol("Description")
.setErrorCol("TranslationError")
.setOutputCol("output")
.setToLanguage(["zh-Hans", "fr", "ru", "cy"])
.setConcurrency(5)
.transform(itemized_df)
.withColumn("Translations", col("output.translations")[0])
.drop("output", "TranslationError")
.cache())
display(translated_df)
```


Tip

To check for translated strings, scroll to the end of the rows.


## Add a search index with AzureSearchWriter

Paste the following code in the sixth cell and run it. No modifications are required.

This code loads [AzureSearchWriter](https://microsoft.github.io/SynapseML/docs/Explore%20Algorithms/AI%20Services/Overview/#azure-cognitive-search-sample). It consumes a tabular dataset and infers a search index schema that defines one field for each column. Because the translations structure is an array, it's articulated in the index as a complex collection with subfields for each language translation. The generated index has a document key and uses the default values for fields created using the [Create Index REST API](/en-us/rest/api/searchservice/indexes/create).

```
from synapse.ml.cognitive import *
(translated_df.withColumn("DocID", monotonically_increasing_id().cast("string"))
.withColumn("SearchAction", lit("upload"))
.writeToAzureSearch(
subscriptionKey=search_key,
actionCol="SearchAction",
serviceName=search_service,
indexName=search_index,
keyCol="DocID",
))
```


To explore the index definition created by AzureSearchWriter, check the search service pages in the Azure portal.

Note

If you can't use the default search index, you can provide an external custom definition in JSON, passing its URI as a string in the "indexJson" property. Generate the default index first so that you know which fields to specify, and then follow with customized properties if you need specific analyzers, for example.

## Query the index

Paste the following code into the seventh cell and run it. No modifications are required, except that you might want to vary the syntax or try more examples to further explore your content:

There's no transformer or module that issues queries. This cell is a simple call to the [Search Documents REST API](/en-us/rest/api/searchservice/documents/search-post).

This particular example is searching for the word "door" (`"search": "door"`

). It also returns a "count" of the number of matching documents and selects just the contents of the "Description' and "Translations" fields for the results. If you want to see the full list of fields, remove the "select" parameter.

```
import requests
url = "https://{}.search.windows.net/indexes/{}/docs/search?api-version=2025-09-01".format(search_service, search_index)
requests.post(url, json={"search": "door", "count": "true", "select": "Description, Translations"}, headers={"api-key": search_key}).json()
```


The following screenshot shows the cell output for sample script.


## Clean up resources

When you're working in your own subscription, at the end of a project, it's a good idea to remove the resources that you no longer need. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the **All resources** or **Resource groups** link in the left-navigation pane.

## Next steps

In this tutorial, you learned about the [AzureSearchWriter](https://microsoft.github.io/SynapseML/docs/Explore%20Algorithms/AI%20Services/Overview/#azure-cognitive-search-sample) transformer in SynapseML, which is a new way of creating and loading search indexes in Azure AI Search. The transformer takes structured JSON as an input. FormOntologyLearner can provide the necessary structure for output produced by the Azure Document Intelligence transformers in SynapseML.

As a next step, review the other SynapseML tutorials that produce transformed content you might want to explore through Azure AI Search:
