---
merged_at: 2026-01-25T03:18:14.118509
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-reliability.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-reliability -->

# Reliability in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure AI Search](/en-us/azure/search/search-what-is-azure-search) is a scalable search infrastructure that indexes heterogeneous content and enables retrieval through APIs, applications, and AI agents. It's suitable for enterprise search scenarios and AI-powered customer experiences that require dynamic content generation through chat completion models. As an Azure service, AI Search provides a range of capabilities to support your reliability requirements.

When you use Azure, [reliability is a shared responsibility](/en-us/azure/reliability/concept-shared-responsibility). Microsoft provides a range of capabilities to support resiliency and recovery. You're responsible for understanding how those capabilities work within all of the services you use, and selecting the capabilities you need to meet your business objectives and uptime goals.

This article describes how to make Azure AI Search resilient to a variety of potential outages and problems, including transient faults, availability zone outages, region outages, and service maintenance. It also describes how you can use backups to recover from other types of problems, and highlights some key information about the Azure AI Search service level agreement (SLA).

## Production deployment recommendations for reliability

For production workloads, we recommend that you:

- Use a
[billable tier](/en-us/azure/search/search-sku-tier)that has at least[two replicas](/en-us/azure/search/search-capacity-planning#add-or-remove-partitions-and-replicas). This configuration makes your search service more resilient to transient faults and maintenance operations. It also meets the[service-level agreement (SLA)](#service-level-agreement)for AI Search. The SLA requires two replicas for read-only workloads and three or more replicas for read-write workloads. - Don't use the Free tier for production use. AI Search doesn't provide an SLA for the Free tier, which is limited to one replica.

## Reliability architecture overview

When you use AI Search, you create a *search service*. Each search service supports many *search indexes* that store your searchable content.

AI Search isn't designed as a primary data store. Instead, you use *indexers* to connect your search service to external data sources. An indexer crawls the source data, invokes *skills* that perform processing and enrichment, and populates your index with the skill outputs.

You also configure the number of *replicas* for your service. In AI Search, a replica is a copy of your service's search engine. You can think of a replica as representing a single virtual machine (VM). Each search service can have between 1 and 12 replicas.

The addition of multiple replicas allows AI Search to:

Increase the availability of your search service.

Perform maintenance on one replica while queries continue to run on other replicas.

Handle higher indexing and query workloads.

Improve resiliency by attempting to provision replicas in different availability zones, if your region supports them.


AI Search automatically assigns one replica to be the *primary replica*. All write operations are performed against that replica. The other replicas are used for read operations.

The following diagram illustrates how a search service with three replicas might be spread across three availability zones:


You can also configure the number of *partitions*, which represent the storage that the search indexes use.

It's important to understand the impact of adding replicas and partitions because they each affect read and write performance in different ways. For more information about replicas and partitions, see [Estimate and manage capacity of a search service](/en-us/azure/search/search-capacity-planning).

## Resilience to transient faults

Transient faults are short, intermittent failures in components. They occur frequently in a distributed environment like the cloud, and they're a normal part of operations. Transient faults correct themselves after a short period of time. It's important that your applications can handle transient faults, usually by retrying affected requests.

All cloud-hosted applications should follow the Azure transient fault handling guidance when they communicate with any cloud-hosted APIs, databases, and other components. For more information, see [Recommendations for handling transient faults](/en-us/azure/well-architected/reliability/handle-transient-faults).

AI Search indexers have built-in transient fault handling. If a data source is briefly unavailable, the indexer is designed to recover and retry. It uses change tracking to resume indexing from the last successfully indexed document.

Search services might experience transient faults during standard, unscheduled maintenance operations. Azure AI Search doesn't provide advance notification or allow scheduling of maintenance at specific times. Although every effort is made to minimize downtime, even for single-replica services, brief interruptions can still occur. To improve resiliency against these transient faults, we recommend that you use two or more replicas.

If you build any applications that interact with AI Search, they should handle transient faults. Use a retry strategy with exponential backoffs for both read and write operations.

## Resilience to availability zone failures

[Availability zones](/en-us/azure/reliability/availability-zones-overview) are physically separate groups of datacenters within an Azure region. When one zone fails, services can fail over to one of the remaining zones.

AI Search is zone redundant, which means that your replicas are distributed across multiple availability zones within the search service region.

When you add two or more replicas to your service, AI Search attempts to place each replica in a different availability zone. For services that have more replicas than available zones, replicas are distributed across zones as evenly as possible.

The following diagram illustrates how an example search service with four replicas might be deployed across three availability zones:


Important

AI Search doesn't guarantee the exact placement of replicas. Placement is subject to capacity constraints, scaling operations, and other factors.

### Requirements

Zone redundancy is automatically enabled when your search service meets all of the following criteria:

**Region support:**Support for availability zones depends on infrastructure and storage. For a list of supported regions, see[Choose a region for AI Search](/en-us/azure/search/search-region-support).**Tier:**Your service must be on the[Basic tier or higher](/en-us/azure/search/search-sku-tier)**Number of replicas:**Your service must have[at least two replicas](/en-us/azure/search/search-capacity-planning#add-or-remove-partitions-and-replicas)Note

AI Search attempts to distribute replicas across multiple zones when you have two or more replicas. However, for read-write workloads, you should use three or more replicas so that you receive the highest possible availability SLA.


### Instance distribution across zones

AI Search attempts to place replicas across different availability zones. However, there are occasionally situations where all of the replicas of a search service might be placed into the same availability zone. This situation can happen when replicas are removed from your service, such as when you *scale in* by configuring your service to use fewer replicas. Replica removal doesn't trigger the remaining replicas to rebalance across the availability zones.

To reduce the likelihood of all of your replicas being placed into a single availability zone, you can manually trigger a scale-out operation immediately after a scale-in operation. For example, suppose that your search service has 10 replicas and you want to scale in to 7 replicas. Instead of performing a single scale operation, you can temporarily scale to 6 instances and then immediately scale to 7 instances to trigger zone rebalancing.

### Cost

Each search service starts with one replica. Zone redundancy requires two or more replicas, which increases the cost to run the service. To understand the billing implications of replicas, use the [pricing calculator](https://azure.microsoft.com/pricing/calculator/).

### Configure availability zone support

If your search service meets the [requirements for zone redundancy](#requirements), no extra configuration is necessary. Whenever possible, AI Search attempts to place your replicas in different availability zones.

### Capacity planning and management

To prepare for availability zone failure, consider *overprovisioning* the number of replicas. Overprovisioning allows the search service to tolerate some capacity loss and continue to function without degraded performance. Adding replicas during an outage is challenging, so overprovisioning helps ensure that your search service can handle normal request volumes, even with reduced capacity. For more information, see [Manage capacity by overprovisioning](/en-us/azure/reliability/concept-redundancy-replication-backup#manage-capacity-with-over-provisioning).

### Behavior when all zones are healthy

This section describes what to expect when search services are configured for zone redundancy and all availability zones are operational.

**Traffic routing between zones:**AI Search performs automatic load balancing of all queries and writes across all of the available replicas. AI Search can send read operations to any replica in any availability zone. It sends write operations to a single primary replica that the AI Search service selects.**Data replication between zones:**Changes in data are automatically replicated between replicas across availability zones. Replication occurs asynchronously, which means that writes are committed to one primary replica before they're replicated to other replicas.

### Behavior during a zone failure

This section describes what to expect when search services are configured for zone redundancy and an availability zone outage occurs.

**Detection and response:**AI Search is responsible for detecting a failure in an availability zone. You don't need to do anything to initiate a zone failover.

**Notification**: Microsoft doesn't automatically notify you when a zone is down. However, you can use[Azure Resource Health](/en-us/azure/service-health/resource-health-overview)to monitor for the health of an individual resource, and you can set up[Resource Health alerts](/en-us/azure/service-health/resource-health-alert-arm-template-guide)to notify you of problems. You can also use[Azure Service Health](/en-us/azure/service-health/overview)to understand the overall health of the service, including any zone failures, and you can set up[Service Health alerts](/en-us/azure/service-health/resource-health-alert-arm-template-guide)to notify you of problems.

**Active requests:**Requests that replicas process in the failed zone are terminated. Clients should retry the requests by following the guidance for[handling transient faults](#resilience-to-transient-faults).**Expected data loss:**If the affected availability zone only contains read replicas, no data loss is expected.If the primary replica is lost because it was in the affected zone, then any write operations that haven't yet been replicated might be lost.

**Expected downtime:**In most situations, a zone failure isn't expected to cause downtime to your search service for read operations because read replicas in other availability zones continue to serve requests.If the primary replica is lost because it was in the affected zone, AI Search automatically promotes another replica to become the new primary so that write operations can resume. It typically takes a few seconds for the replica promotion to occur. During this time, write operations might not succeed. Ensure that your applications are prepared by following

[transient fault handling guidance](#resilience-to-transient-faults).However, there are some unlikely situations where all of your search service's replicas might be in a single availability zone. In this scenario, you might experience downtime until the zone recovers. For more information, and to understand a workaround, see

[Instance distribution](#instance-distribution-across-zones).**Traffic rerouting:**When a zone fails, AI Search detects the failure and routes requests to active replicas in the surviving zones. If the primary replica is lost, another replica is promoted to be the new primary.

### Zone recovery

When the availability zone recovers, AI Search automatically restores normal operations and begins routing traffic to available replicas across all zones, including the recovered zone.

### Test for zone failures

AI Search manages traffic routing for zone-redundant services. You don't need to initiate or validate any zone failure processes.

## Resilience to region-wide failures

AI Search is a single-region service. If the region becomes unavailable, your search service also becomes unavailable.

### Custom multi-region solutions for resiliency

You can optionally deploy multiple AI Search services in different regions. You're responsible for deploying and configuring separate services in each region. If you create an identical deployment in a secondary Azure region that uses a multi-region architecture, your application becomes less susceptible to a single-region disaster.

When you follow this approach, you must synchronize indexes across regions to recover the last application state. You must also configure load balancing and failover policies.

To optimize the performance of your overall solution, look for opportunities to perform indexing on read-only replicas of your data sources. For example, some indexers support reading from a geo-distributed data source's read replicas.

For more information, see [Multi-region deployments in Azure AI Search](/en-us/azure/search/search-multi-region).

## Backup and restore

Because AI Search isn't a primary data storage solution, it doesn't provide self-service backup and restore options. However, you can use the `index-backup-restore`

sample for [.NET](https://github.com/Azure-Samples/azure-search-dotnet-utilities/tree/main/index-backup-restore) or [Python](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python/code/utilities/index-backup-restore) to back up your index definition and its documents to a series of JSON files, which are then used to restore the index.

However, if you accidentally delete the index and don't have a backup, you can [rebuild the index](/en-us/azure/search/search-howto-reindex). Rebuilding involves recreating the index on your search service and then reloading it by retrieving data from your primary data store.

## Service-level agreement

The service-level agreement (SLA) for Azure services describes the expected availability of each service and the conditions that your solution must meet to achieve that availability expectation. For more information, see [SLAs for online services](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services).

In AI Search, the availability SLA applies to search services that:

- Are configured to use
[a billable tier](/en-us/azure/search/search-sku-tier). - Have at least two
[replicas](/en-us/azure/search/search-capacity-planning#add-or-remove-partitions-and-replicas)for read-only workloads (queries). - Have at least three replicas for read-write workloads (queries and indexing).


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-defining-skillset.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset -->

# Create a skillset in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].


A skillset defines operations that generate vector and textual content and structure from documents that contain images or raw content. Examples are chunking skills, embedding (vectorization) skills, image verbalization, and other processes like optical character recognition (OCR) for images, entity recognition for undifferentiated text, and text translation. A skillset executes after raw content is extracted from an external data source, and after [field mappings](search-indexer-field-mappings) are processed.

This article explains how to create a skillset using [REST APIs](/en-us/rest/api/searchservice/skillsets/create), but the same concepts and steps apply to other programming languages.

Rules for skillset definition include:

- Must have a unique name within the skillset collection. A skillset is a top-level resource that can be used by any indexer.
- Must have at least one skill. Three to five skills are typical. The maximum is 30.
- A skillset can repeat skills of the same type. For example, a skillset can have multiple Shaper skills.
- A skillset supports chained operations, looping, and branching.

A skillset is attached to an indexer. To use the skillset, reference it in an [indexer](search-howto-create-indexers) and then run the indexer to import data, invoke skills processing, and send output to an [index](search-what-is-an-index). A skillset is high-level resource, but it's operational only within indexer processing. As a high-level resource, you can reference it in multiple indexers.

Tip

Enable [enrichment caching](enrichment-cache-how-to-configure) to reuse the content you've already processed and lower the cost of development.

## Add a skillset definition

Creating a skillset adds it to your search service. Updating a skillset fully overwrites an existing skillset with the contents of the request payload. A best practice for updates is to retrieve the skillset definition with a GET, modify it, and then update with PUT.

Start with the basic structure. In the [Create Skillset REST API](/en-us/rest/api/searchservice/skillsets/create), the body of the request is authored in JSON and has the following sections:

```
{
"name":"skillset-template",
"description":"A description makes the skillset self-documenting (comments aren't allowed in JSON itself)",
"skills":[
],
"cognitiveServices":{
"@odata.type":"#Microsoft.Azure.Search.CognitiveServicesByKey",
"description":"A Microsoft Foundry resource in the same region as Azure AI Search",
"key":"<Your-Azure-AI-Foundry-Resource-Key>"
},
"knowledgeStore":{
"storageConnectionString":"<Your-Azure-Storage-Connection-String>",
"projections":[
{
"tables":[ ],
"objects":[ ],
"files":[ ]
}
]
},
"encryptionKey":{ }
}
```


After the name and description, a skillset has four main properties:

`skills`

array, an unordered[collection of skills](cognitive-search-predefined-skills). Skills are either standalone or chained together through input-output associations, where the output of one transform becomes input to another. Skills can be utilitarian (like splitting text), transformational (based on AI from Azure OpenAI or Foundry Tools), or custom skills that you provide. An example of a skills array is provided in the next section.`cognitiveServices`

is used for[billable skills](cognitive-search-predefined-skills)that call Foundry Tools APIs. Remove this section if you aren't using billable skills or Custom Entity Lookup. If you are, attach[a Foundry resource](cognitive-search-attach-cognitive-services).`knowledgeStore`

(optional) specifies an Azure Storage account and settings for projecting skillset output into tables, blobs, and files in Azure Storage. Remove this section if you don't need it, otherwise[specify a knowledge store](knowledge-store-create-rest).`encryptionKey`

(optional) specifies an Azure Key Vault and[customer-managed keys](search-security-manage-encryption-keys)used to encrypt sensitive content (descriptions, connection strings, keys) in a skillset definition. Remove this property if you aren't using customer-managed encryption.

## Add skills

Inside the skillset definition, the skills array specifies which skills to execute. Three to five skills are common, but you can add as many skills as necessary, subject to [service limits](search-limits-quotas-capacity#indexer-limits).

The end result of an enrichment pipeline is textual content in either a search index or a knowledge store. For this reason, most skills either create text from images (OCR text, captions, tags), or analyze existing text to create new information (entities, key phrases, sentiment). Skills that operate independently are processed in parallel. Skills that depend on each other specify the output of one skill (such as key phrases) as the input of a second skill (such as text translation). The search service determines the order of skill execution and the [execution environment](search-howto-run-reset-indexers#indexer-execution-environment).

All skills have a type, context, inputs, and outputs. A skill might optionally have a name and description. The following example shows two unrelated [built-in skills](cognitive-search-predefined-skills) so that you can compare the basic structure.

```
"skills": [
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityRecognitionSkill",
"name": "#1",
"description": "This skill detects organizations in the source content",
"context": "/document",
"categories": [
"Organization"
],
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "organizations",
"targetName": "orgs"
}
]
},
{
"name": "#2",
"description": "This skill detects corporate logos in the source files",
"@odata.type": "#Microsoft.Skills.Vision.ImageAnalysisSkill",
"context": "/document/normalized_images/*",
"visualFeatures": [
"brands"
],
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "brands"
}
]
}
]
```


Each skill is unique in terms of its input values and the parameters that it takes. [Skill reference documentation](cognitive-search-predefined-skills) describes all of the parameters and properties of a given skill. Although there are differences, most skills share a common set and are similarly patterned.

Note

You can build complex skillsets with looping and branching using the [Conditional cognitive skill](cognitive-search-skill-conditional) to create the expressions. The syntax is based on the [JSON Pointer](https://tools.ietf.org/html/rfc6901) path notation, with a few modifications to identify nodes in the enrichment tree. A `"/"`

traverses a level lower in the tree and `"*"`

acts as a for-each operator in the context. Numerous examples in this article illustrate [the syntax](cognitive-search-skill-annotation-language).

## Set skill context

Each skill has a [context property](cognitive-search-working-with-skillsets#skill-context) that determines the level at which operations take place. If the `context`

property isn't explicitly set, the default is `"/document"`

, where the context is the whole document (the skill is called once per document).

```
"skills":[
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityRecognitionSkill",
"context": "/document",
"inputs": [],
"outputs": []
},
{
"@odata.type": "#Microsoft.Skills.Vision.ImageAnalysisSkill",
"context": "/document/normalized_images/*",
"visualFeatures": [],
"inputs": [],
"outputs": []
}
]
```


The `context`

property is usually set to one of the following examples:

| Context example | Description |
|---|---|
`context` : `/document` |
(Default) Inputs and outputs are at the document level. |
`context` : `/document/pages/*` |
Some skills like sentiment analysis perform better over smaller chunks of text. If you're splitting a large content field into pages or sentences, the context should be over each component part. |
`context` : `/document/normalized_images/*` |
For image content, inputs and outputs are one per image in the parent document. |

Context also determines where outputs are produced in the [enrichment tree](cognitive-search-working-with-skillsets#enrichment-tree). For example, the Entity Recognition skill returns a property called `organizations`

, captured as `orgs`

. If the context is `"/document"`

, then an `organizations`

node is added as a child of `"/document"`

. If you then want to reference this node in downstream skills, the path is `"/document/orgs"`

.

## Define inputs

Skills read from and write to an enriched document. Skill inputs specify the origin of the incoming data. It's often the root node of the enriched document. For blobs, a typical skill input is the document's content property.

[Skill reference documentation](cognitive-search-predefined-skills) for each skill describes the inputs it can consume. Each input has a `name`

that identifies a specific input, and a `source`

that specifies the location of the data in the enriched document. The following example is from the Entity Recognition skill:

```
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/language"
}
]
```


Skills can have multiple inputs. The

`name`

is the specific input. For Entity Recognition, the specific inputs are*text*and*languageCode*.The

`source`

property specifies which field or row provides the content to be processed. For text-based skills, the source is a field in the document or row that provides text. For image-based skills, the node providing the input is normalized images.Source example Description `source`

:`/document`

For a tabular data set, a document corresponds to a row. `source`

:`/document/content`

For blobs, the source is usually the blob's content property. `source`

:`/document/some-named-field`

For text-based skills, such as entity recognition or key phrase extraction, the origin should be a field that contains sufficient text to be analyzed, such as a *description*or*summary*.`source`

:`/document/normalized_images/*`

For image content, the source is image that's been normalized during document cracking.

If the skill iterates over an array, both context and input source should include `/*`

in the correct positions. For more information about the complete syntax, see [Skill context and input annotation language](cognitive-search-skill-annotation-language).

## Define outputs

Each skill is designed to emit specific kinds of output, which are referenced by name in the skillset. A skill output has a `name`

and an optional `targetName`

.

[Skill reference documentation](cognitive-search-predefined-skills) for each skill describes the outputs it can produce. The following example is from the Entity Recognition skill:

```
"outputs": [
{
"name": "persons",
"targetName": "people"
},
{
"name": "organizations",
"targetName": "orgs"
},
{
"name": "locations",
"targetName": "places"
}
]
```


Skills can have multiple outputs. The

`name`

property identifies a specific output. For example, for Entity Recognition, output can be*persons*,*locations*,*organizations*, among others.The

`targetName`

property specifies the name you would like this node to have in the enriched document. This is useful if skill outputs have the same name. If you have multiple skills that return the same output, use`targetName`

for name disambiguation in enrichment node paths. If the target name is unspecified, the name property is used for both.

Some situations call for referencing each element of an array separately. For example, suppose you want to pass *each element* of `"/document/orgs"`

separately to another skill. To do so, add an asterisk to the path: `"/document/orgs/*"`

.

Skill output is written to the enriched document as a new node in the enrichment tree. It might be a simple value, such as a sentiment score or language code. It could also be a collection, such as a list of organizations, people, or locations. Skill output can also be a complex structure, as is the case with the Shaper skill. The inputs of the skill determine the composition of the shape, but the output is the named object, which can be referenced in a search index, a knowledge store projection, or another skill by its name.

## Add a custom skill

This section includes an example of a [custom skill](cognitive-search-custom-skill-web-api). The URI points to an Azure Function, which in turn invokes the model or transformation that you provide. For more information, see [Add a custom skill to an Azure AI Search enrichment pipeline](cognitive-search-custom-skill-interface).

Although the custom skill executes code that is external to the pipeline, in a skills array, it's just another skill. Like the built-in skills, it has a type, context, inputs, and outputs. It also reads and writes to an enrichment tree, just as the built-in skills do. Notice that the `context`

field is set to `"/document/orgs/*"`

with an asterisk, meaning the enrichment step is called *for each* organization under `"/document/orgs"`

.

Output, such as the company description in this example, is generated for each organization that's identified. When referring to the node in a downstream step (for example, in key phrase extraction), you would use the path `"/document/orgs/*/companyDescription"`

to do so.

```
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "This skill calls an Azure function, which in turn calls custom code",
"uri": "https://indexer-e2e-webskill.azurewebsites.net/api/InvokeCode?code=foo",
"httpHeaders": {
"Ocp-Apim-Subscription-Key": "foobar"
},
"context": "/document/orgs/*",
"inputs": [
{
"name": "query",
"source": "/document/orgs/*"
}
],
"outputs": [
{
"name": "description",
"targetName": "companyDescription"
}
]
}
```


## Send output to a destination

Although skill output can be optionally cached for reuse purposes, it's usually temporary and exists only while skill execution is in progress.

To send output to a field in a search index,

[create an output field mapping](cognitive-search-output-field-mapping)in an indexer.To send output to a knowledge store,

[create a projection](knowledge-store-projection-overview).To send output to a downstream skill, reference the output by its node name, such as

`"/document/organization"`

, in the downstream skill's input source property. See[Reference an annotation](cognitive-search-concept-annotations-syntax)for examples.

## Tips for a first skillset

Try the

or**Import data**wizard.**Import data (new)**wizardThe wizards automate several steps that can be challenging the first time around. It defines the skillset, index, and indexer, including field mappings and output field mappings. It also defines projections in a knowledge store if you're using one. For some skills, such as OCR or image analysis, the wizard adds utility skills that merge the image and text content that was separated during document cracking.

After the wizard runs, you can open each object in the Azure portal to view its JSON definition.

Try

[Debug Sessions](cognitive-search-debug-session)to invoke skillset execution over a target document and inspect the enriched document that the skillset creates. You can view and modify input and output settings and values. This tutorial is a good place to start:[Tutorial: Debug a skillset using Debug Sessions](cognitive-search-tutorial-debug-sessions).

## Next step

Context and input source fields are paths to nodes in an enrichment tree. As a next step, learn more about the path syntax for nodes in an enrichment tree.
