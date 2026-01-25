---
merged_at: 2026-01-25T03:28:16.221090
merged_files: 10
---

# Documentos Fusionados

Este archivo contiene 10 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: package-usehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/package-use.html -->

# Uses of Packagecom.google.adk.tools.applicationintegrationtoolset

# Uses of Package

com.google.adk.tools.applicationintegrationtoolset

-
ClassDescriptionRepresents the schema for an action.Represents details of a connection.Represents the schema and available operations for an entity.


---

<!-- DOCUMENTO FUSIONADO: package-summaryhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/package-summary.html -->

# Package com.google.adk.tools.applicationintegrationtoolset

package com.google.adk.tools.applicationintegrationtoolset

-
ClassDescriptionApplication Integration ToolsetUtility class for interacting with the Google Cloud Connectors API.Represents the schema for an action.Represents details of a connection.Represents the schema and available operations for an entity.Utility class for interacting with Google Cloud Application Integration.Application Integration Tool


---

<!-- DOCUMENTO FUSIONADO: connectionsclientconnectiondetailshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/ConnectionsClient.ConnectionDetails.html -->

# Class ConnectionsClient.ConnectionDetails

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.applicationintegrationtoolset.ConnectionsClient.ConnectionDetails

- Enclosing class:
[ConnectionsClient](ConnectionsClient.html)

Represents details of a connection.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### name

-
### serviceName

-
### host


-
-
## Constructor Details

-
### ConnectionDetails

public ConnectionDetails()

-


---

<!-- DOCUMENTO FUSIONADO: connectionsclientactionschemahtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/ConnectionsClient.ActionSchema.html -->

# Class ConnectionsClient.ActionSchema

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.applicationintegrationtoolset.ConnectionsClient.ActionSchema

- Enclosing class:
[ConnectionsClient](ConnectionsClient.html)

Represents the schema for an action.

-
## Field Summary

Modifier and TypeFieldDescription -
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### inputSchema

-
### outputSchema

-
### description

-
### displayName


-
-
## Constructor Details

-
### ActionSchema

public ActionSchema()

-


---

<!-- DOCUMENTO FUSIONADO: integrationclienthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/IntegrationClient.html -->

# Class IntegrationClient

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.applicationintegrationtoolset.IntegrationClient

Utility class for interacting with Google Cloud Application Integration.

This class provides methods for retrieving OpenAPI spec for an integration or a connection.

-
## Field Summary

Modifier and TypeFieldDescription`static final com.fasterxml.jackson.databind.ObjectMapper`

-
## Method Summary


-
## Field Details

-
### OBJECT_MAPPER

public static final com.fasterxml.jackson.databind.ObjectMapper OBJECT_MAPPER

-


---

<!-- DOCUMENTO FUSIONADO: connectionscliententityschemaandoperationshtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/ConnectionsClient.EntitySchemaAndOperations.html -->

# Class ConnectionsClient.EntitySchemaAndOperations

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.applicationintegrationtoolset.ConnectionsClient.EntitySchemaAndOperations

- Enclosing class:
[ConnectionsClient](ConnectionsClient.html)

Represents the schema and available operations for an entity.

-
## Field Summary

-
## Constructor Summary

-
## Method Summary


-
## Field Details

-
### schema

-
### operations


-
-
## Constructor Details

-
### EntitySchemaAndOperations

public EntitySchemaAndOperations()

-


---

<!-- DOCUMENTO FUSIONADO: integrationconnectortoolhtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/IntegrationConnectorTool.html -->

# Class IntegrationConnectorTool

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

[com.google.adk.tools.BaseTool](../BaseTool.html)

com.google.adk.tools.applicationintegrationtoolset.IntegrationConnectorTool

Application Integration Tool

-
## Method Summary

### Methods inherited from class com.google.adk.tools.

[BaseTool](../BaseTool.html)[description](../BaseTool.html#description()),[longRunning](../BaseTool.html#longRunning()),[name](../BaseTool.html#name()),[processLlmRequest](../BaseTool.html#processLlmRequest(com.google.adk.models.LlmRequest.Builder,com.google.adk.tools.ToolContext))

-
## Method Details

-
### declaration

Description copied from class:[BaseTool](../BaseTool.html#declaration())Gets the`FunctionDeclaration`

representation of this tool.- Overrides:

in class[declaration](../BaseTool.html#declaration())[BaseTool](../BaseTool.html)

-
### runAsync


-


---

<!-- DOCUMENTO FUSIONADO: package-treehtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/package-tree.html -->

# Hierarchy For Package com.google.adk.tools.applicationintegrationtoolset

## Class Hierarchy

- java.lang.
[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)- com.google.adk.tools.applicationintegrationtoolset.
[ApplicationIntegrationToolset](ApplicationIntegrationToolset.html)(implements com.google.adk.tools.[BaseToolset](../BaseToolset.html)) - com.google.adk.tools.
[BaseTool](../BaseTool.html)- com.google.adk.tools.applicationintegrationtoolset.
[IntegrationConnectorTool](IntegrationConnectorTool.html)

- com.google.adk.tools.applicationintegrationtoolset.
- com.google.adk.tools.applicationintegrationtoolset.
[ConnectionsClient](ConnectionsClient.html) - com.google.adk.tools.applicationintegrationtoolset.
[ConnectionsClient.ActionSchema](ConnectionsClient.ActionSchema.html) - com.google.adk.tools.applicationintegrationtoolset.
[ConnectionsClient.ConnectionDetails](ConnectionsClient.ConnectionDetails.html) - com.google.adk.tools.applicationintegrationtoolset.
[ConnectionsClient.EntitySchemaAndOperations](ConnectionsClient.EntitySchemaAndOperations.html) - com.google.adk.tools.applicationintegrationtoolset.
[IntegrationClient](IntegrationClient.html)

- com.google.adk.tools.applicationintegrationtoolset.


---

<!-- DOCUMENTO FUSIONADO: applicationintegrationtoolsethtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/ApplicationIntegrationToolset.html -->

# Class ApplicationIntegrationToolset

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

- All Implemented Interfaces:

,[BaseToolset](../BaseToolset.html)[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)

-
## Field Summary

Modifier and TypeFieldDescription`static final com.fasterxml.jackson.databind.ObjectMapper`

-
## Constructor Summary

ConstructorDescription[ApplicationIntegrationToolset](#%3Cinit%3E(java.lang.String,java.lang.String,java.lang.String,java.util.List,java.lang.String,java.util.Map,java.util.List,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)integration,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> triggers,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)connection,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> entityOperations,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> actions,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)serviceAccountJson,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolNamePrefix,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)ApplicationIntegrationToolset generates tools from a given Application Integration resource. -
## Method Summary

Modifier and TypeMethodDescription`void`

[close](#close())()Performs cleanup and releases resources held by the toolset.`io.reactivex.rxjava3.core.Flowable`

< [BaseTool](../BaseTool.html)>[getTools](#getTools(com.google.adk.agents.ReadonlyContext))(@Nullable [ReadonlyContext](../../agents/ReadonlyContext.html)readonlyContext)Return all tools in the toolset based on the provided context.### Methods inherited from class java.lang.

[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)[clone](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#clone()),[equals](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#equals(java.lang.Object)),[finalize](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#finalize()),[getClass](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#getClass()),[hashCode](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#hashCode()),[notify](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notify()),[notifyAll](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#notifyAll()),[toString](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#toString()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait()),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long)),[wait](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html#wait(long,int))### Methods inherited from interface com.google.adk.tools.

[BaseToolset](../BaseToolset.html)[isToolSelected](../BaseToolset.html#isToolSelected(com.google.adk.tools.BaseTool,java.util.Optional,java.util.Optional))

-
## Field Details

-
### OBJECT_MAPPER

public static final com.fasterxml.jackson.databind.ObjectMapper OBJECT_MAPPER

-
-
## Constructor Details

-
### ApplicationIntegrationToolset

public ApplicationIntegrationToolset( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)integration,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> triggers,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)connection,[Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)>> entityOperations,[List](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/List.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)> actions,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)serviceAccountJson,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolNamePrefix,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)ApplicationIntegrationToolset generates tools from a given Application Integration resource.Example Usage:

integrationTool = new ApplicationIntegrationToolset( project="test-project", location="us-central1", integration="test-integration", triggers=ImmutableList.of("api_trigger/test_trigger", "api_trigger/test_trigger_2", serviceAccountJson="{....}"),connection=null,enitityOperations=null,actions=null,toolNamePrefix="test-integration-tool",toolInstructions="This tool is used to get response from test-integration.");

connectionTool = new ApplicationIntegrationToolset( project="test-project", location="us-central1", integration=null, triggers=null, connection="test-connection", entityOperations=ImmutableMap.of("Entity1", ImmutableList.of("LIST", "GET", "UPDATE")), "Entity2", ImmutableList.of()), actions=ImmutableList.of("ExecuteCustomQuery"), serviceAccountJson="{....}", toolNamePrefix="test-tool", toolInstructions="This tool is used to list, get and update issues in Jira.");

- Parameters:
`project`

- The GCP project ID.`location`

- The GCP location of integration.`integration`

- The integration name.`triggers`

- (Optional) The list of trigger ids in the integration.`connection`

- (Optional) The connection name.`entityOperations`

- (Optional) The entity operations.`actions`

- (Optional) The actions.`serviceAccountJson`

- (Optional) The service account configuration as a dictionary. Required if not using default service credential. Used for fetching the Application Integration or Integration Connector resource.`toolNamePrefix`

- (Optional) The tool name prefix.`toolInstructions`

- (Optional) The tool instructions.


-
-
## Method Details

-
### getTools

public io.reactivex.rxjava3.core.Flowable<[BaseTool](../BaseTool.html)> getTools(@Nullable [ReadonlyContext](../../agents/ReadonlyContext.html)readonlyContext)Description copied from interface:[BaseToolset](../BaseToolset.html#getTools(com.google.adk.agents.ReadonlyContext))Return all tools in the toolset based on the provided context.- Specified by:

in interface[getTools](../BaseToolset.html#getTools(com.google.adk.agents.ReadonlyContext))[BaseToolset](../BaseToolset.html)- Parameters:
`readonlyContext`

- Context used to filter tools available to the agent.- Returns:
- A Single emitting a list of tools available under the specified context.

-
### close

Description copied from interface:[BaseToolset](../BaseToolset.html#close())Performs cleanup and releases resources held by the toolset.NOTE: This method is invoked, for example, at the end of an agent server's lifecycle or when the toolset is no longer needed. Implementations should ensure that any open connections, files, or other managed resources are properly released to prevent leaks.

- Specified by:

in interface[close](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html#close())[AutoCloseable](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/AutoCloseable.html)- Specified by:

in interface[close](../BaseToolset.html#close())[BaseToolset](../BaseToolset.html)- Throws:
[Exception](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Exception.html)


-


---

<!-- DOCUMENTO FUSIONADO: connectionsclienthtml.md -->
<!-- URL ORIGINAL: https://google.github.io/adk-docs/api-reference/java/com/google/adk/tools/applicationintegrationtoolset/ConnectionsClient.html -->

# Class ConnectionsClient

[java.lang.Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)

com.google.adk.tools.applicationintegrationtoolset.ConnectionsClient

Utility class for interacting with the Google Cloud Connectors API.

This class provides methods to fetch connection details, schemas for entities and actions, and to generate OpenAPI specifications for creating tools based on these connections.

-
## Nested Class Summary

Modifier and TypeClassDescription`static class`

Represents the schema for an action.`static class`

Represents details of a connection.`static class`

Represents the schema and available operations for an entity. -
## Constructor Summary

ConstructorDescription[ConnectionsClient](#%3Cinit%3E(java.lang.String,java.lang.String,java.lang.String,com.google.adk.tools.applicationintegrationtoolset.IntegrationConnectorTool.HttpExecutor,com.fasterxml.jackson.databind.ObjectMapper))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)connection, com.google.adk.tools.applicationintegrationtoolset.IntegrationConnectorTool.HttpExecutor httpExecutor, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Initializes the ConnectionsClient. -
## Method Summary

Modifier and TypeMethodDescription[actionRequest](#actionRequest(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)action)[actionResponse](#actionResponse(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)action)[connectorPayload](#connectorPayload(java.util.Map))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> jsonSchema)[convertJsonSchemaToOpenApiSchema](#convertJsonSchemaToOpenApiSchema(java.util.Map))( [Map](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Map.html)<[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html),[Object](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Object.html)> jsonSchema)Converts a JSON Schema dictionary to an OpenAPI schema dictionary.[createOperation](#createOperation(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[createOperationRequest](#createOperationRequest(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity)[deleteOperation](#deleteOperation(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[getActionOperation](#getActionOperation(java.lang.String,java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)action,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)operation,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)actionDisplayName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[getActionSchema](#getActionSchema(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)action)Retrieves the input and output JSON schema for a given action.Retrieves service details for a given connection.[getEntitySchemaAndOperations](#getEntitySchemaAndOperations(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity)Retrieves the JSON schema and available operations for a given entity.[getOperation](#getOperation(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)schemaAsString,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[listOperation](#listOperation(java.lang.String,java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)schemaAsString,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[updateOperation](#updateOperation(java.lang.String,java.lang.String,java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolName,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)toolInstructions)[updateOperationRequest](#updateOperationRequest(java.lang.String))( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity)

-
## Constructor Details

-
### ConnectionsClient

public ConnectionsClient( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)project,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)location,[String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)connection, com.google.adk.tools.applicationintegrationtoolset.IntegrationConnectorTool.HttpExecutor httpExecutor, com.fasterxml.jackson.databind.ObjectMapper objectMapper)Initializes the ConnectionsClient.- Parameters:
`project`

- The Google Cloud project ID.`location`

- The Google Cloud location (e.g., us-central1).`connection`

- The connection name.


-
-
## Method Details

-
### getConnectionDetails

public[ConnectionsClient.ConnectionDetails](ConnectionsClient.ConnectionDetails.html)getConnectionDetails() throws[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html),[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)Retrieves service details for a given connection.- Returns:
- A
object with the connection's info.`ConnectionsClient.ConnectionDetails`

- Throws:

- If there is an issue with network communication or credentials.[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html)

- If the thread is interrupted during the API call.[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)

-
### getEntitySchemaAndOperations

public[ConnectionsClient.EntitySchemaAndOperations](ConnectionsClient.EntitySchemaAndOperations.html)getEntitySchemaAndOperations( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)entity) throws[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html),[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)Retrieves the JSON schema and available operations for a given entity.- Parameters:
`entity`

- The entity name.- Returns:
- A
object.`ConnectionsClient.EntitySchemaAndOperations`

- Throws:

- If there is an issue with network communication or credentials.[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html)

- If the thread is interrupted during polling.[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)

-
### getActionSchema

public[ConnectionsClient.ActionSchema](ConnectionsClient.ActionSchema.html)getActionSchema( [String](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)action) throws[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html),[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)Retrieves the input and output JSON schema for a given action.- Parameters:
`action`

- The action name.- Returns:
- An
object.`ConnectionsClient.ActionSchema`

- Throws:

- If there is an issue with network communication or credentials.[IOException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/io/IOException.html)

- If the thread is interrupted during polling.[InterruptedException](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/InterruptedException.html)

-
### convertJsonSchemaToOpenApiSchema

-
### connectorPayload

-
### getConnectorBaseSpec

-
### getActionOperation

-
### listOperation

-
### getOperation

-
### createOperation

-
### updateOperation

-
### deleteOperation

-
### createOperationRequest

-
### updateOperationRequest

-
### getOperationRequest

-
### deleteOperationRequest

-
### listOperationRequest

-
### actionRequest

-
### actionResponse

-
### executeCustomQueryRequest


-
