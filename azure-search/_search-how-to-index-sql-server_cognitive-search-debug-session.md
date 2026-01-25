---
merged_at: 2026-01-25T03:18:13.793604
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-sql-server.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-sql-server -->

# Configure an indexer connection to a SQL Server instance on an Azure virtual machine

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When configuring an [Azure SQL indexer](search-how-to-index-sql-database) to extract content from a database on an Azure virtual machine, extra steps are required for secure connections.

A connection from Azure AI Search to SQL Server instance on a virtual machine is a public internet connection. In order for secure connections to succeed, perform the following steps:

Obtain a certificate from a

[Certificate Authority provider](https://en.wikipedia.org/wiki/Certificate_authority#Providers)for the fully qualified domain name of the SQL Server instance on the virtual machine.Install the certificate on the virtual machine.


After you install the certificate on your VM, you're ready to complete the following steps in this article.

Note

[Always Encrypted](/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) columns are not currently supported by Azure AI Search indexers.

## Enable encrypted connections

Azure AI Search requires an encrypted channel for all indexer requests over a public internet connection. This section lists the steps to make this work.

Check the properties of the certificate to verify the subject name is the fully qualified domain name (FQDN) of the Azure VM.

You can use a tool like CertUtils or the Certificates snap-in to view the properties. You can get the FQDN from the VM service page Essentials section, in the

**Public IP address/DNS name label**field, in the[Azure portal](https://portal.azure.com/).The FQDN is typically formatted as

`<your-VM-name>.<region>.cloudapp.azure.com`

Configure SQL Server to use the certificate using the Registry Editor (regedit).

Although SQL Server Configuration Manager is often used for this task, you can't use it for this scenario. It won't find the imported certificate because the FQDN of the VM on Azure doesn't match the FQDN as determined by the VM (it identifies the domain as either the local computer or the network domain to which it's joined). When names don't match, use regedit to specify the certificate.

In regedit, browse to this registry key:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`

.The

`[MSSQL13.MSSQLSERVER]`

part varies based on version and instance name.Set the value of the

**Certificate**key to the**thumbprint**(without spaces) of the TLS/SSL certificate you imported to the VM.For example, copy the hexadecimal characters to text editor, such as Notepad. Delete all spaces from the thumbprint string. If the thumbprint is

`c0 d0 f2 70 95 b0 3d 43 17 e2 19 84 10 24 32 8c ef 24 87 79`

, then change it to`c0d0f27095b03d4317e219841024328cef248779`

.There are several ways to get the thumbprint, some better than others. If you copy it from the

**Certificates**snap-in in MMC, you might pick up an invisible leading character, which results in an error when you attempt a connection. Several workarounds exist for correcting this problem. The easiest is to backspace over and then retype the first character of the thumbprint to remove the leading character in the key value field in regedit. Alternatively, you can use a different tool to copy the thumbprint. For more information, see[Certificate thumbprint displayed in MMC certificate snap-in has extra invisible unicode character](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra).

Grant permissions to the service account.

Make sure the SQL Server service account is granted appropriate permission on the private key of the TLS/SSL certificate. If you overlook this step, SQL Server doesn't start. You can use the

**Certificates**snap-in or**CertUtils**for this task.Restart the SQL Server service.


## Connect to SQL Server

After you set up the encrypted connection required by Azure AI Search, connect to the instance through its public endpoint. The following article explains the connection requirements and syntax:

## Configure the network security group

It's a best practice to configure the [network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview) and corresponding Azure endpoint or Access Control List (ACL) to make your Azure VM accessible to other parties. Chances are you've done this before to allow your own application logic to connect to your SQL Azure VM. It's no different for an Azure AI Search connection to your SQL Azure VM.

The following steps and links provide instructions on NSG configuration for VM deployments. Use these instructions to ACL a search service endpoint based on its IP address.

Obtain the IP address of your search service. See the

[following section](#restrict-network-access-to-azure-ai-search)for instructions.Add the search IP address to the IP filter list of the security group. Either one of following articles explains the steps:


IP addressing can pose a few challenges that are easily overcome if you're aware of the issue and potential workarounds. The remaining sections provide recommendations for handling issues related to IP addresses in the ACL.

### Restrict network access to Azure AI Search

We strongly recommend that you restrict the access to the IP address of your search service and the IP address range of `AzureCognitiveSearch`

[service tag](/en-us/azure/virtual-network/service-tags-overview#available-service-tags) in the ACL instead of making your SQL Azure VMs open to all connection requests.

You can find out the IP address by pinging the FQDN (for example, `<your-search-service-name>.search.windows.net`

) of your search service. Although it's possible for the search service IP address to change, it's unlikely that it will change. The IP address tends to be static for the lifetime of the service.

You can find out the IP address range of `AzureCognitiveSearch`

[service tag](/en-us/azure/virtual-network/service-tags-overview#available-service-tags) by either using [Downloadable JSON files](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files) or via the [Service Tag Discovery API](/en-us/azure/virtual-network/service-tags-overview#use-the-service-tag-discovery-api). The IP address range is updated weekly.

### Include the Azure portal IP addresses

If you're using the Azure portal to create an indexer, you must grant the Azure portal inbound access to your SQL Azure virtual machine. An inbound rule in the firewall requires that you provide the IP address of the Azure portal.

To get the Azure portal IP address, ping `stamp2.ext.search.windows.net`

, which is the domain of the traffic manager. The request times out, but the IP address is visible in the status message. For example, in the message "Pinging azsyrie.northcentralus.cloudapp.azure.com [52.252.175.48]", the IP address is "52.252.175.48".

Clusters in different regions connect to different traffic managers. Regardless of the domain name, the IP address returned from the ping is the correct one to use when defining an inbound firewall rule for the Azure portal in your region.

## Supplement network security with token authentication

Firewalls and network security are a first step in preventing unauthorized access to data and operations. Authorization should be your next step.

We recommend role-based access, where Microsoft Entra ID users and groups are assigned to roles that determine read and write access to your service. See [Connect to Azure AI Search using role-based access controls](search-security-rbac) for a description of built-in roles and instructions for creating custom roles.

If you don't need key-based authentication, we recommend that you disable API keys and use role assignments exclusively.

## Next steps

With configuration out of the way, you can now specify a SQL Server on Azure VM as the data source for an Azure AI Search indexer. For more information, see [Index data from Azure SQL](search-how-to-index-sql-database).


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-debug-session.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-debug-session -->

# Debug Sessions in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Debug Sessions is a visual editor that works with an existing skillset in the Azure portal, exposing the structure and content of a single enriched document as it's produced by an indexer and skillset for the duration of the session. Because you're working with a live document, the session is interactive - you can identify errors, modify and invoke skill execution, and validate the results in real time. If your changes resolve the problem, you can commit them to a published skillset to apply the fixes globally.

This article explains supported scenarios and how the editor is organized. Tabs and sections of the editor unpack different layers of the skillset so that you can examine skillset structure, flow, and the content it generates at run time.

## Supported scenarios

Use Debug Sessions to investigate and resolve problems with:

Built-in skills used for

[AI enrichment](cognitive-search-concept-intro), such as OCR, image analysis, entity recognition, and keyword extraction.Built-in skills used for

[integrated vectorization](vector-search-integrated-vectorization), with data chunking through Text Split, and vectorization through an embedding skill.Custom skills used to integrate external processing that you provide.


Compare the following debug session images for the first two scenarios. For both scenarios, the surface area shows the progression of skills that generate or transform content en route from the source document to the search index. The flow includes index mapping options, and you can trace the arrows to follow the processing trail. The details pane to the right is context-sensitive. It shows a representation of the enriched document that's created by the pipeline, or the details of a skill or mapping.

The first image shows a pattern for applied AI enrichment (no vectors). Skills can run sequentially or in parallel if there are no dependencies. Index mappings show how enriched or generated content travels from in-memory data structures to fields in an index. Enriched document shows the data structure that the skillset creates.

The second image shows a typical pattern for integrated vectorization. Skills for integrated vectorization usually include a Text Split skill and an embedding skill. A Text Split skill divides a document into chunks. An embedding skill calls an embedding API to vectorize those chunks. This particular skillset chunks content into an array of "pages". For integrated vectorization, projection mappings control how chunks are mapped to fields in the index.

## Limitations

Debug Sessions work with all generally available [indexer data sources](search-data-sources-gallery) and most preview data sources, with the following exceptions:

SharePoint indexer.

Azure Cosmos DB for MongoDB indexer.

For the Azure Cosmos DB for NoSQL, if a row fails during index and there's no corresponding metadata, the debug session might not pick the correct row.

For the SQL API of Azure Cosmos DB, if a partitioned collection was previously non-partitioned, the debug session won't find the document.

For custom skills, a user-assigned managed identity isn't supported for a debug session connection to Azure Storage. As stated in the prerequisites, you can use a system managed identity, or specify a full access connection string that includes a key. For more information, see

[Connect a search service to other Azure resources using a managed identity](search-how-to-managed-identities).Data sources with encryption enabled via

[customer managed keys (CMK)](search-security-manage-encryption-keys).Currently, the ability to select which document to debug is unavailable. This limitation isn't permanent and should be lifted soon. At this time, Debug Sessions selects the first document in the source data container or folder.


## How a debug session works

When you start a session, the search service creates a copy of the skillset, indexer, and a data source containing a single document used to test the skillset. All session state is saved to a new blob container created by the Azure AI Search service in an Azure Storage account that you provide. The name of the generated container has a prefix of `ms-az-cognitive-search-debugsession`

. The prefix is required because it mitigates the chance of accidentally exporting session data to another container in your account.

A cached copy of the enriched document and skillset is loaded into the visual editor so that you can inspect the content and metadata of the enriched document, with the ability to check each document node and edit any aspect of the skillset definition. Any changes made within the session are cached. Those changes won't affect the published skillset unless you commit them. Committing changes will overwrite the production skillset.

If the enrichment pipeline doesn't have any errors, a debug session can be used to incrementally enrich a document, test and validate each change before committing the changes.

Debug sessions help identify the root cause of errors or warnings by analyzing the data, skill inputs and outputs, and field mappings. If the indexer encounters configuration issues, such as incorrect network setup, permission-related access errors, or similar, please review the specific error message along with the linked documentation provided. For troubleshooting guidance, refer to the [common indexer errors and warnings](cognitive-search-common-errors-warnings).

## Debug Sessions with private connectivity

If your AI enrichment pipeline uses shared private links to access Azure resources, additional configuration is required to ensure indexer and debug sessions work correctly. This includes permissions, trusted access, and network setup.

- If you're using
[managed identity](search-how-to-managed-identities), assign the necessary roles to your search service identity, including`Storage Blob Data Contributor`

, so debug sessions can write session data to your storage account. - Ensure the search service has access to all resources referenced in the
[skillset definition](cognitive-search-working-with-skillsets), including any used in the debug session. - In your storage account,
[enable trusted services](search-indexer-howto-access-trusted-service-exception)to allow access from Azure AI Search. - Set
`"executionEnvironment" = "private"`

property in the indexer definition to ensure the[indexer runs in a private context](search-indexer-howto-access-private?#4---configure-the-indexer-to-run-in-the-private-environment). - Create a
[shared private link](search-indexer-howto-access-private)for each resource accessed by the search service, including: your data source, if configured to indexer AI enrichment cache and knowledge store, and any other resources configured in your skillset. - For other troubleshooting guidance, refer to the
[common indexer errors and warnings](cognitive-search-common-errors-warnings).

## Debug session layout

The visual editor is organized into a surface area showing a progression of operations, starting with document cracking, followed by skills, mappings, and an index.

Select any skill or mapping, and a pane opens to side showing relevant information.

Follow the links to drill further into skills processing. For example, the following screenshot shows the output of the first iteration of the Text Split skill.

### Skill details pane

The **Skill details** pane has the following sections:

**Iterations**: Shows you how many times a skill executes. You can check the inputs and outputs of each one.**Skill Settings**: View or edit the JSON skillset definition.**Errors and warnings**: Shows the errors or warnings specific to this skill.

### Enriched data structure pane

The **Enriched Data Structure** pane slides out to the side when you select the blue show or hide arrow symbol. It's a human readable representation of what the enriched document contains. Previous screenshots in this article show examples of the enriched data structure.

## Next steps

Now that you understand the elements of debug sessions, start your first debug session on an existing skillset.
