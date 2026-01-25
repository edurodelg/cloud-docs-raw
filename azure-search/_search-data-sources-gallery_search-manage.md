---
merged_at: 2026-01-25T03:18:13.772144
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-data-sources-gallery.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-data-sources-gallery -->

# Data sources gallery

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Find a data connector from Microsoft or a partner that works with [an indexer](search-indexer-overview) to simplify data ingestion into a search index.

Note

The connectors mentioned in this article represent one method for indexing data in Azure AI Search. You also have the option of developing your own connector using the [Push REST API or An Azure SDK](search-what-is-data-import#pushing-data-to-an-index).

## Generally available data sources by Azure AI Search

Pull in content from other Azure services using indexers and the following data source connectors.

### Azure Blob Storage

Extract blob metadata and content, serialized into JSON documents, and imported into a search index as search documents. Set properties in both data source and indexer definitions to optimize for various blob content types. Change detection is supported automatically.


### Azure Table Storage

Extract rows from an Azure Table, serialized into JSON documents, and imported into a search index as search documents.


### Azure Data Lake Storage Gen2

Connect to Azure Storage through Azure Data Lake Storage Gen2 to extract content from a hierarchy of directories and nested subdirectories.


### Azure Cosmos DB for NoSQL

Connect to Azure Cosmos DB through the SQL API to extract items from a container, serialized into JSON documents, and imported into a search index as search documents. Configure change tracking to refresh the search index with the latest changes in your database.


### Azure SQL Database

Extract field values from a single table or view, serialized into JSON documents, and imported into a search index as search documents. Configure change tracking to refresh the search index with the latest changes in your database.


### Microsoft OneLake files

Connect to a OneLake lakehouse to extract supported files content from a hierarchy of directories and nested subdirectories.


## Logic app connectors

Pull in content [using logic app workflows](search-how-to-index-logic-apps) and the following supported data sources. Note that the Logic Apps artifacts mentioned below, they have a pre-built workflow, however, you can use [any connectors listed under Logic Apps](/en-us/connectors/connector-reference/connector-reference-logicapps-connectors) that pull data from sources and create your own indexing pipeline workflow that pushes data to [Azure AI Search via a Logic App connector](/en-us/azure/logic-apps/connectors/azure-ai#azure-ai-search).

### SharePoint

By [Logic Apps](/en-us/connectors/sharepointonline)

SharePoint helps organizations share and collaborate with colleagues, partners, and customers. You can connect to SharePoint in Microsoft 365 or to an on-premises SharePoint 2016 or 2019 farm using the On-Premises Data Gateway to manage documents and list items.


### OneDrive

By [Logic Apps](/en-us/connectors/onedrive/)

Connect to OneDrive to manage your files. You can perform various actions such as upload, update, get, and delete on files in OneDrive.

### OneDrive for Business

By [Logic Apps](/en-us/connectors/onedriveforbusiness/)

OneDrive for Business is a cloud storage, file hosting service that allows users to sync files and later access them from a web browser or mobile device. Connect to OneDrive for Business to manage your files. You can perform various actions such as upload, update, get, and delete files.

### Azure File Storage

By [Logic Apps](/en-us/connectors/azurefile/)

Microsoft Azure Storage provides a massively scalable, durable, and highly available storage for data on the cloud, and serves as the data storage solution for modern applications. Connect to File Storage to perform various operations such as create, update, get and delete on files in your Azure Storage account.

### Azure Queues

By [Logic Apps](/en-us/connectors/azurequeues/)

Azure Queue storage provides cloud messaging between application components. Queue storage also supports managing asynchronous tasks and building process work flows.

### Service Bus

By [Logic Apps](/en-us/connectors/servicebus/)

Connect to Azure Service Bus to send and receive messages. You can perform actions such as send to queue, send to topic, receive from queue, receive from subscription, etc.

## Preview data sources by Azure AI Search

New data sources are issued as preview features. [Sign up](https://aka.ms/azure-cognitive-search/indexer-preview) to get started.

### Azure Files

Connect to Azure Storage through Azure Files share to extract content serialized into JSON documents, and imported into a search index as search documents.


### Azure Cosmos DB for Apache Gremlin

Connect to Azure Cosmos DB for Apache Gremlin to extract items from a container, serialized into JSON documents, and imported into a search index as search documents. Configure change tracking to refresh the search index with the latest changes in your database.


### Azure Cosmos DB for MongoDB

Connect to Azure Cosmos DB for MongoDB to extract items from a container, serialized into JSON documents, and imported into a search index as search documents. Configure change tracking to refresh the search index with the latest changes in your database.


### SharePoint

Connect to a SharePoint site and index documents from one or more document libraries, for accounts and search services in the same tenant. Text and normalized images are extracted by default. Optionally, you can configure a skillset for more content transformation and enrichment, or configure change tracking to refresh a search index with new or changed content in SharePoint.


### Azure MySQL

Connect to MySQL database on Azure to extract rows in a table, serialized into JSON documents, and imported into a search index as search documents. On subsequent runs, assuming High Water Mark change detection policy is configured, the indexer takes all changes, uploads, and delete and reflect those changes in your search index.


## Data sources from our partners

The following Microsoft partners offer custom third-party data connectors. Each partner implements and supports these connectors, which aren't part of Azure AI Search built-in indexers. Before you use a custom connector, review the partner's licensing and usage instructions.


---

<!-- DOCUMENTO FUSIONADO: search-manage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-manage -->

# Configure your Azure AI Search service in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Configuring your new Azure AI Search service involves several tasks to optimize security, access, and performance. This article provides a day-one checklist to help you set up your service in the [Azure portal](https://portal.azure.com).

After you create a search service, we recommend that you:

## Configure role-based access

Portal access is based on [role assignments](search-security-rbac). By default, new search services have at least one service administrator or owner. Service administrators, co-administrators, and owners have permission to create more administrators and assign other roles. They also have access to all portal pages and operations on default search services.

Tip

By default, any administrator or owner can create or delete services. To prevent accidental deletions, consider [locking your resources](/en-us/azure/azure-resource-manager/management/lock-resources).

Each search service comes with [API keys](search-security-api-keys) and uses key-based authentication by default. However, we recommend using Microsoft Entra ID and role-based access control (RBAC) for improved security. RBAC eliminates the need to store and pass API keys in plain text.

When you switch from key-based authentication to keyless authentication, service administrators must assign themselves data plane roles for full access to objects and data. These roles include Search Service Contributor, Search Index Data Contributor, and Search Index Data Reader.

To configure role-based access:

[Enable roles](search-security-enable-roles)on your search service. We recommend using both API keys and roles.[Assign data plane roles](search-security-rbac)to replace the functionality lost when you disable API keys. An owner only needs Search Index Data Reader, but developers need[more roles](search-security-rbac#assign-roles).Role assignments can take several minutes to take effect. Until then, portal pages used for data plane operations display the following message:

[Assign more roles](search-security-rbac)for solution developers and apps.

## Configure a managed identity

If you plan to use indexers for automated indexing, applied AI, or integrated vectorization, you should [configure your search service to use a managed identity](search-how-to-managed-identities). You can then assign roles on other Azure services that authorize your search service to access data and operations.

For integrated vectorization, your search service identity needs the following roles:

- Storage Blob Data Reader on Azure Storage
- Cognitive Services Data User on a Microsoft Foundry resource

Role assignments can take several minutes to take effect.

Before you move on to network security, consider testing all points of connection to validate role assignments. Run an [import wizard](search-get-started-portal) to test permissions.

## Configure network security

By default, a search service accepts authenticated and authorized requests over public internet connections. You have two options for enhancing network security:

[Configure firewall rules](service-configure-firewall)to restrict network access by IP address.[Configure a private endpoint](service-create-private-endpoint)to only allow traffic from Azure virtual networks. Note that when you turn off the public endpoint, the import wizards won't run.

To learn about inbound and outbound calls in Azure AI Search, see [Security in Azure AI Search](search-security-overview).

## Check capacity and understand billing

By default, a search service is created with one replica and one partition. You can [add capacity](search-capacity-planning) by adding replicas and partitions, but we recommend waiting until volumes require it. Many customers run production workloads on the minimum configuration.

Semantic ranker can increase the cost of running your service if you opt into the standard plan. If you don't want to use this feature, you can [disable semantic ranker](semantic-how-to-enable-disable) at the service level.

To learn about other features that affect billing, see [How you're charged for Azure AI Search](search-sku-manage-costs#how-youre-charged-for-the-base-service).

## Enable diagnostic logging

[Enable diagnostic logging](search-monitor-enable-logging) to track user activity. If you skip this step, you still get [activity logs](/en-us/azure/azure-monitor/essentials/activity-log) and [platform metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics#types-of-metrics) automatically. However, if you want index and query usage information, you should enable diagnostic logging and choose a destination for logged operations. We recommend Log Analytics Workspace for durable storage so that you can run system queries in the Azure portal.

Internally, Microsoft collects telemetry data about your service and the platform. To learn more about data retention, see [Retention of metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

To learn more about data location and privacy, see [Data residency](search-security-overview#data-residency).

## Enable semantic ranker

Semantic ranker is free for the first 1,000 requests per month. It's enabled by default on newer search services.

To enable semantic ranker in the portal, select **Settings** > **Premium features** from the left pane, and then select the **Free** plan. For more information, see [Enable semantic ranker](semantic-how-to-enable-disable).

## Provide connection information to developers

To connect to Azure AI Search, developers need:

- An endpoint or URL from the
**Overview**page. - An API key from the
**Keys**page or a role assignment. We recommend Search Service Contributor, Search Index Data Contributor, and Search Index Data Reader.

We recommend portal access for the [import wizards](search-get-started-portal) and [Search explorer](search-explorer). You must be a contributor or higher to run the wizards.

## Related content

For programmatic support for service administration, see the following APIs and modules:

You can also use the management client libraries in the Azure SDKs for .NET, Python, Java, and JavaScript.

There's feature parity across all modalities and languages, except for preview management features. As a general rule, preview management features are released through the Management REST API first.
