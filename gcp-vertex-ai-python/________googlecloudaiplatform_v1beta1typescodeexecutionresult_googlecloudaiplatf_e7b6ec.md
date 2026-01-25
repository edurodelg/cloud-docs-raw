---
merged_at: 2026-01-25T21:47:44.365911
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatfo_9f4663.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatfor_741b19.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatform_857488.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatform__c75510.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatform_v_ee7055.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatform_v1_b87cff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescodeexecutionresult_googlecloudaiplatform_v1b_41d5dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescodeexecutionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CodeExecutionResult -->

# Class CodeExecutionResult (1.134.0)

`CodeExecutionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Result of executing the [ExecutableCode].

Always follows a `part`

containing the [ExecutableCode].

## Attributes |
|
|---|---|
Name |
Description |
`outcome` |
Required. Outcome of the code execution. |
`output` |
`str`
Optional. Contains stdout when code execution is successful, stderr or other description otherwise. |

## Classes

### Outcome

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

## Methods

### CodeExecutionResult

`CodeExecutionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Result of executing the [ExecutableCode].

Always follows a `part`

containing the [ExecutableCode].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessuggesttrialsmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SuggestTrialsMetadata -->

# Class SuggestTrialsMetadata (1.134.0)

`SuggestTrialsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform Trials suggestion.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for suggesting Trials. |
`client_id` |
`str`
The identifier of the client that is requesting the suggestion. If multiple SuggestTrialsRequests have the same `client_id` , the service will return the identical
suggested Trial if the Trial is pending, and provide a new
Trial if the last suggested Trial was completed.
|

## Methods

### SuggestTrialsMetadata

`SuggestTrialsMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of operations that perform Trials suggestion.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespscinterfaceconfig_googlecloudaiplatform_v1typesse_50ead9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespscinterfaceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PscInterfaceConfig -->

# Class PscInterfaceConfig (1.134.0)

`PscInterfaceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for PSC-I.

## Attributes |
|
|---|---|
Name |
Description |
`network_attachment` |
`str`
Optional. The name of the Compute Engine `network attachment |
`dns_peering_configs` |
`MutableSequence[`
Optional. DNS peering configurations. When specified, Vertex AI will attempt to configure DNS peering zones in the tenant project VPC to resolve the specified domains using the target network's Cloud DNS. The user must grant the dns.peer role to the Vertex AI Service Agent on the target project. |

## Methods

### PscInterfaceConfig

`PscInterfaceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for PSC-I.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchdataitemsrequestorderbyannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsRequest.OrderByAnnotation -->

# Class OrderByAnnotation (1.134.0)

`OrderByAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Expression that allows ranking results based on annotation's property.

## Attributes |
|
|---|---|
Name |
Description |
`saved_query` |
`str`
Required. Saved query of the Annotation. Only Annotations belong to this saved query will be considered for ordering. |
`order_by` |
`str`
A comma-separated list of annotation fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Must also specify saved_query. |

## Methods

### OrderByAnnotation

`OrderByAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Expression that allows ranking results based on annotation's property.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessearchdataitemsrequestorderbyannotation_goog_3df990.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchdataitemsrequestorderbyannotation_googl_b25e6f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchdataitemsrequestorderbyannotation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsRequest.OrderByAnnotation -->

# Class OrderByAnnotation (1.134.0)

`OrderByAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Expression that allows ranking results based on annotation's property.

## Attributes |
|
|---|---|
Name |
Description |
`saved_query` |
`str`
Required. Saved query of the Annotation. Only Annotations belong to this saved query will be considered for ordering. |
`order_by` |
`str`
A comma-separated list of annotation fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Must also specify saved_query. |

## Methods

### OrderByAnnotation

`OrderByAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Expression that allows ranking results based on annotation's property.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprobeexecaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.ExecAction -->

# Class ExecAction (1.134.0)

`ExecAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecAction specifies a command to execute.

## Attribute |
|
|---|---|
Name |
Description |
`command` |
`MutableSequence[str]`
Command is the command line to execute inside the container, the working directory for the command is root ('/') in the container's filesystem. The command is simply exec'd, it is not run inside a shell, so traditional shell instructions ('\|', etc) won't work. To use a shell, you need to explicitly call out to that shell. Exit status of 0 is treated as live/healthy and non-zero is unhealthy. |

## Methods

### ExecAction

`ExecAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ExecAction specifies a command to execute.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescounttokensrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CountTokensRequest -->

# Class CountTokensRequest (1.134.0)

`CountTokensRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.CountTokens.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to perform token counting. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Optional. The name of the publisher model requested to serve the prediction. Format: `projects/{project}/locations/{location}/publishers/*/models/*`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model. |
`contents` |
`MutableSequence[`
Optional. Input content. |
`system_instruction` |
Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph. This field is a member of `oneof` _ `_system_instruction` .
|
`tools` |
`MutableSequence[`
Optional. A list of `Tools` the model may use to generate
the next response.
A `Tool` is a piece of code that enables the system to
interact with external systems to perform an action, or set
of actions, outside of knowledge and scope of the model.
|
`generation_config` |
Optional. Generation config that the model will use to generate the response. This field is a member of `oneof` _ `_generation_config` .
|

## Methods

### CountTokensRequest

`CountTokensRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.CountTokens.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesrougespec_googlecloudaiplatform_v1typescontainer_c8b9e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesrougespec_googlecloudaiplatform_v1typescontainers_daa9ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrougespec_googlecloudaiplatform_v1typescontainersp_bea2e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrougespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RougeSpec -->

# Class RougeSpec (1.134.0)

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

## Attributes |
|
|---|---|
Name |
Description |
`rouge_type` |
`str`
Optional. Supported rouge types are rougen[1-9], rougeL, and rougeLsum. |
`use_stemmer` |
`bool`
Optional. Whether to use stemmer to compute rouge score. |
`split_summaries` |
`bool`
Optional. Whether to split summaries while using rougeLsum. |

## Methods

### RougeSpec

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescontainerspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ContainerSpec -->

# Class ContainerSpec (1.134.0)

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. The URI of a container image in the Container Registry that is to be run on each worker replica. |
`command` |
`MutableSequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided. |
`args` |
`MutableSequence[str]`
The arguments to be passed when starting the container. |
`env` |
`MutableSequence[`
Environment variables to be passed to the container. Maximum limit is 100. |

## Methods

### ContainerSpec

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescounttokensrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CountTokensRequest -->

# Class CountTokensRequest (1.134.0)

`CountTokensRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.CountTokens][].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to perform token counting. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Optional. The name of the publisher model requested to serve the prediction. Format: `projects/{project}/locations/{location}/publishers/*/models/*`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model. |
`contents` |
`MutableSequence[`
Optional. Input content. |
`system_instruction` |
Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph. This field is a member of `oneof` _ `_system_instruction` .
|
`tools` |
`MutableSequence[`
Optional. A list of `Tools` the model may use to generate
the next response.
A `Tool` is a piece of code that enables the system to
interact with external systems to perform an action, or set
of actions, outside of knowledge and scope of the model.
|
`generation_config` |
Optional. Generation config that the model will use to generate the response. This field is a member of `oneof` _ `_generation_config` .
|

## Methods

### CountTokensRequest

`CountTokensRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.CountTokens][].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbigquerydestination_googlecloudaiplatform_v1beta1_e3ebbe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbigquerydestination_googlecloudaiplatform_v1beta1t_f61e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbigquerydestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BigQueryDestination -->

# Class BigQueryDestination (1.134.0)

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri` |
`str`
Required. BigQuery URI to a project or table, up to 2000 characters long. When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist. Accepted forms: - BigQuery path. For example: `bq://projectId` or
`bq://projectId.bqDatasetId` or
`bq://projectId.bqDatasetId.bqTableId` .
|

## Methods

### BigQueryDestination

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesextensionoperation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionOperation -->

# Class ExtensionOperation (1.134.0)

`ExtensionOperation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Operation of an extension.

## Attributes |
|
|---|---|
Name |
Description |
`operation_id` |
`str`
Operation ID that uniquely identifies the operations among the extension. See: "Operation Object" in https://swagger.io/specification/. This field is parsed from the OpenAPI spec. For HTTP extensions, if it does not exist in the spec, we will generate one from the HTTP method and path. |
`function_declaration` |
Output only. Structured representation of a function declaration as defined by the OpenAPI Spec. |

## Methods

### ExtensionOperation

`ExtensionOperation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Operation of an extension.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesgen_ai_cache_service_googlecloudaiplatform_v1ty_22e8cf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_cache_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service -->

# Package gen_ai_cache_service (1.134.0)

API documentation for `aiplatform_v1.services.gen_ai_cache_service`

package.

## Classes

[GenAiCacheServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient)

Service for managing Vertex AI's CachedContent resource.

[GenAiCacheServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.GenAiCacheServiceClient)

Service for managing Vertex AI's CachedContent resource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.pagers)

API documentation for `aiplatform_v1.services.gen_ai_cache_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeaturestoreRequest -->

# Class DeleteFeaturestoreRequest (1.134.0)

`DeleteFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Featurestore to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`force` |
`bool`
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) |

## Methods

### DeleteFeaturestoreRequest

`DeleteFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescreatedatasetversionrequest_googlecloudaiplatfo_b4f83b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescreatedatasetversionrequest_googlecloudaiplatfor_1b76f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreatedatasetversionrequest_googlecloudaiplatform_74cfe0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreatedatasetversionrequest_googlecloudaiplatform__e8075c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatedatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetVersionRequest -->

# Class CreateDatasetVersionRequest (1.134.0)

`CreateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDatasetVersion.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Dataset resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`dataset_version` |
Required. The version to be created. The same CMEK policies with the original Dataset will be applied the dataset version. So here we don't need to specify the EncryptionSpecType here. |

## Methods

### CreateDatasetVersionRequest

`CreateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.CreateDatasetVersion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest -->

# Class DeleteFeaturestoreRequest (1.134.0)

`DeleteFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Featurestore to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`force` |
`bool`
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) |

## Methods

### DeleteFeaturestoreRequest

`DeleteFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningengine.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngine -->

# Class ReasoningEngine (1.134.0)

`ReasoningEngine(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`display_name` |
`str`
Required. The display name of the ReasoningEngine. |
`description` |
`str`
Optional. The description of the ReasoningEngine. |
`spec` |
Optional. Configurations of the ReasoningEngine |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ReasoningEngine was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ReasoningEngine was most recently updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`context_spec` |
Optional. Configuration for how Agent Engine sub-resources should manage context. |
`encryption_spec` |
Customer-managed encryption key spec for a ReasoningEngine. If set, this ReasoningEngine and all sub-resources of this ReasoningEngine will be secured by this key. |
`labels` |
`MutableMapping[str, str]`
Labels for the ReasoningEngine. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### ReasoningEngine

`ReasoningEngine(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


ReasoningEngine provides a customizable runtime for models to determine which actions to take and in which order.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbatchpredictionjobinputconfig__googlecloudaiplatfo_4988eb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchpredictionjobinputconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchPredictionJob.InputConfig -->

# Class InputConfig (1.134.0)

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_source` |
The Cloud Storage location for the input instances. This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
The BigQuery location of the input table. The schema of the table should be in the format described by the given context OpenAPI Schema, if one is provided. The table may contain additional columns that are not described by the schema, and they will be ignored. This field is a member of `oneof` _ `source` .
|
`instances_format` |
`str`
Required. The format in which instances are given, must be one of the [Model's][google.cloud.aiplatform.v1.BatchPredictionJob.model] supported_input_storage_formats. |

## Methods

### InputConfig

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatemodeldeploymentmonitoringjobrequest_goo_19d22d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelDeploymentMonitoringJobRequest -->

# Class CreateModelDeploymentMonitoringJobRequest (1.134.0)

```
CreateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateModelDeploymentMonitoringJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
|
`model_deployment_monitoring_job` |
Required. The ModelDeploymentMonitoringJob to create |

## Methods

### CreateModelDeploymentMonitoringJobRequest

```
CreateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeletefeaturegrouprequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureGroupRequest -->

# Class DeleteFeatureGroupRequest (1.134.0)

`DeleteFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.DeleteFeatureGroup.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureGroup to be deleted. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`force` |
`bool`
If set to true, any Features under this FeatureGroup will also be deleted. (Otherwise, the request will only work if the FeatureGroup has no Features.) |

## Methods

### DeleteFeatureGroupRequest

`DeleteFeatureGroupRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.DeleteFeatureGroup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvid_e513e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvide_7f8e49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideo_b856e7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideoobjecttracking.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTracking -->

# Class AutoMlVideoObjectTracking (1.134.0)

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlVideoObjectTracking

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

### AutoMlVideoObjectTracking

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeaturesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse -->

# Class ListFeaturesResponse (1.134.0)

`ListFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturesResponse

`ListFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationpolar_b4887e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadatavisualizationpolarity.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.Polarity -->

# Class Polarity (1.134.0)

`Polarity(value)`


Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.

## Enums |
|
|---|---|
Name |
Description |
`POLARITY_UNSPECIFIED` |
Default value. This is the same as POSITIVE. |
`POSITIVE` |
Highlights the pixels/outlines that were most influential to the model's prediction. |
`NEGATIVE` |
Setting polarity to negative highlights areas that does not lead to the models's current prediction. |
`BOTH` |
Shows both positive and negative attributions. |

## Methods

### Polarity

`Polarity(value)`


Whether to only highlight pixels with positive contributions, negative or both. Defaults to POSITIVE.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfigpersistentresourceruntimedetailtaskresourceunavailabletimeoutbehavior.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.PersistentResourceRuntimeDetail.TaskResourceUnavailableTimeoutBehavior -->

# Class TaskResourceUnavailableTimeoutBehavior (1.134.0)

`TaskResourceUnavailableTimeoutBehavior(value)`


An enum that specifies the behavior to take if the timeout is reached.

## Enums |
|
|---|---|
Name |
Description |
`TASK_RESOURCE_UNAVAILABLE_TIMEOUT_BEHAVIOR_UNSPECIFIED` |
Unspecified. Behavior is same as `FAIL`. |
`FAIL` |
Fail the task if the timeout is reached. |
`FALL_BACK_TO_ON_DEMAND` |
Fall back to on-demand execution if the timeout is reached. |

## Methods

### TaskResourceUnavailableTimeoutBehavior

`TaskResourceUnavailableTimeoutBehavior(value)`


An enum that specifies the behavior to take if the timeout is reached.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistdeploymentresourcepoolsresponse_googlecl_200ecc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistdeploymentresourcepoolsresponse_googleclo_93bd1b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistdeploymentresourcepoolsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse -->

# Class ListDeploymentResourcePoolsResponse (1.134.0)

```
ListDeploymentResourcePoolsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ListDeploymentResourcePools method.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_resource_pools` |
`MutableSequence[`
The DeploymentResourcePools from the specified location. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|

## Methods

### ListDeploymentResourcePoolsResponse

```
ListDeploymentResourcePoolsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ListDeploymentResourcePools method.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateModelDeploymentMonitoringJobRequest -->

# Class CreateModelDeploymentMonitoringJobRequest (1.134.0)

```
CreateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateModelDeploymentMonitoringJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
|
`model_deployment_monitoring_job` |
Required. The ModelDeploymentMonitoringJob to create |

## Methods

### CreateModelDeploymentMonitoringJobRequest

```
CreateModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CreateModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeleteentitytyperequest_googlecloudaiplatform_7fa71e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteentitytyperequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEntityTypeRequest -->

# Class DeleteEntityTypeRequest (1.134.0)

`DeleteEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeaturestoreService.DeleteEntityTypes][].

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the EntityType to be deleted. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|
`force` |
`bool`
If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.) |

## Methods

### DeleteEntityTypeRequest

`DeleteEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [FeaturestoreService.DeleteEntityTypes][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestensorboardtimeseriesmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`max_step` |
`int`
Output only. Max step index of all data points within a TensorboardTimeSeries. |
`max_wall_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Max wall clock timestamp of all data points within a TensorboardTimeSeries. |
`max_blob_sequence_length` |
`int`
Output only. The largest blob sequence length (number of blobs) of all data points in this time series, if its ValueType is BLOB_SEQUENCE. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesreadtensorboardblobdatarequest_googlecloudaipl_7303f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesreadtensorboardblobdatarequest_googlecloudaipla_4f47b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesreadtensorboardblobdatarequest_googlecloudaiplat_9a1e37.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreadtensorboardblobdatarequest_googlecloudaiplatf_c909e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreadtensorboardblobdatarequest_googlecloudaiplatfo_4b5ced.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardblobdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardBlobDataRequest -->

# Class ReadTensorboardBlobDataRequest (1.134.0)

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`blob_ids` |
`MutableSequence[str]`
IDs of the blobs to read. |

## Methods

### ReadTensorboardBlobDataRequest

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespurgecontextsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeContextsResponse -->

# Class PurgeContextsResponse (1.134.0)

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Contexts that this request deleted (or, if `force` is false, the number of Contexts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Context names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeContextsResponse

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchpredictionjobinputconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob.InputConfig -->

# Class InputConfig (1.134.0)

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`gcs_source` |
The Cloud Storage location for the input instances. This field is a member of `oneof` _ `source` .
|
`bigquery_source` |
The BigQuery location of the input table. The schema of the table should be in the format described by the given context OpenAPI Schema, if one is provided. The table may contain additional columns that are not described by the schema, and they will be ignored. This field is a member of `oneof` _ `source` .
|
`instances_format` |
`str`
Required. The format in which instances are given, must be one of the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] supported_input_storage_formats. |

## Methods

### InputConfig

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespurgeexecutionsresponse_googlecloudaiplatform_v1t_55ac7b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespurgeexecutionsresponse_googlecloudaiplatform_v1ty_3447ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespurgeexecutionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeExecutionsResponse -->

# Class PurgeExecutionsResponse (1.134.0)

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Executions that this request deleted (or, if `force` is false, the number of Executions that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Execution names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeExecutionsResponse

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesharmcategory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.HarmCategory -->

# Class HarmCategory (1.134.0)

`HarmCategory(value)`


Harm categories that will block the content.

## Enums |
|
|---|---|
Name |
Description |
`HARM_CATEGORY_UNSPECIFIED` |
The harm category is unspecified. |
`HARM_CATEGORY_HATE_SPEECH` |
The harm category is hate speech. |
`HARM_CATEGORY_DANGEROUS_CONTENT` |
The harm category is dangerous content. |
`HARM_CATEGORY_HARASSMENT` |
The harm category is harassment. |
`HARM_CATEGORY_SEXUALLY_EXPLICIT` |
The harm category is sexually explicit content. |
`HARM_CATEGORY_CIVIC_INTEGRITY` |
Deprecated: Election filter is not longer supported. The harm category is civic integrity. |
`HARM_CATEGORY_JAILBREAK` |
The harm category is for jailbreak prompts. |

## Methods

### HarmCategory

`HarmCategory(value)`


Harm categories that will block the content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfunctionresponsepart.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionResponsePart -->

# Class FunctionResponsePart (1.134.0)

`FunctionResponsePart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a `FunctionResponse`

message.

A `FunctionResponsePart`

consists of data which has an associated
datatype. A `FunctionResponsePart`

can only contain one of the
accepted types in `FunctionResponsePart.data`

.

A `FunctionResponsePart`

must have a fixed IANA MIME type
identifying the type and subtype of the media if the `inline_data`

field is filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`inline_data` |
Inline media bytes. This field is a member of `oneof` _ `data` .
|
`file_data` |
URI based data. This field is a member of `oneof` _ `data` .
|

## Methods

### FunctionResponsePart

`FunctionResponsePart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a `FunctionResponse`

message.

A `FunctionResponsePart`

consists of data which has an associated
datatype. A `FunctionResponsePart`

can only contain one of the
accepted types in `FunctionResponsePart.data`

.

A `FunctionResponsePart`

must have a fixed IANA MIME type
identifying the type and subtype of the media if the `inline_data`

field is filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespipelinejob___googlecloudaiplatform_v1beta1typesmi_ef2126.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinejob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineJob -->

# Class PipelineJob (1.134.0)

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PipelineJob. |
`display_name` |
`str`
The display name of the Pipeline. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline creation time. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline start time. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Pipeline end time. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this PipelineJob was most recently updated. |
`pipeline_spec` |
`google.protobuf.struct_pb2.Struct`
The spec of the pipeline. |
`state` |
Output only. The detailed state of the job. |
`job_detail` |
Output only. The details of pipeline run. Not available in the list view. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during pipeline execution. Only populated when the pipeline's state is FAILED or CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize PipelineJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. Note there is some reserved label key for Vertex AI Pipelines. - `vertex-ai-pipelines-run-billing-id` , user set value
will get overrided.
|
`runtime_config` |
Runtime config of the pipeline. |
`encryption_spec` |
Customer-managed encryption key spec for a pipelineJob. If set, this PipelineJob and all of its sub-resources will be secured by this key. |
`service_account` |
`str`
The service account that the pipeline workload runs as. If not specified, the Compute Engine default service account in the project will be used. See https://cloud.google.com/compute/docs/access/service-accounts#default_service_account Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`network` |
`str`
The full name of the Compute Engine `network ` __
to which the Pipeline Job's workload should be peered. For
example, `projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
Private services access must already be configured for the
network. Pipeline job will apply the network configuration
to the Google Cloud resources being launched, if applied,
such as Vertex AI Training or Dataflow job. If left
unspecified, the workload is not peered with any network.
|
`reserved_ip_ranges` |
`MutableSequence[str]`
A list of names for the reserved ip ranges under the VPC network that can be used for this Pipeline Job's workload. If set, we will deploy the Pipeline Job's workload within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for PipelineJob. |
`template_uri` |
`str`
A template uri from where the PipelineJob.pipeline_spec, if empty, will be downloaded. Currently, only uri from Vertex Template Registry & Gallery is supported. Reference to https://cloud.google.com/vertex-ai/docs/pipelines/create-pipeline-template. |
`template_metadata` |
Output only. Pipeline template metadata. Will fill up fields if PipelineJob.template_uri is from supported template registry. |
`schedule_name` |
`str`
Output only. The schedule resource name. Only returned if the Pipeline is created by Schedule API. |
`preflight_validations` |
`bool`
Optional. Whether to do component level validations before job creation. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime config of a PipelineJob.

## Methods

### PipelineJob

`PipelineJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a machine learning PipelineJob.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmigratableresourcemlenginemodelversion_googl_129d41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmigratableresourcemlenginemodelversion_google_09302e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigratableresourcemlenginemodelversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource.MlEngineModelVersion -->

# Class MlEngineModelVersion (1.134.0)

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
The ml.googleapis.com endpoint that this model Version currently lives in. Example values: - ml.googleapis.com - us-centrall-ml.googleapis.com - europe-west4-ml.googleapis.com - asia-east1-ml.googleapis.com |
`version` |
`str`
Full resource name of ml engine model Version. Format: `projects/{project}/models/{model}/versions/{version}` .
|

## Methods

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service -->

# Package vertex_rag_data_service (1.134.0)

API documentation for `aiplatform_v1.services.vertex_rag_data_service`

package.

## Classes

[VertexRagDataServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceAsyncClient)

A service for managing user data for RAG.

[VertexRagDataServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.VertexRagDataServiceClient)

A service for managing user data for RAG.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers)

API documentation for `aiplatform_v1.services.vertex_rag_data_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrougespec_googlecloudaiplatform_v1beta1typesc_4e577f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrougespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeSpec -->

# Class RougeSpec (1.134.0)

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

## Attributes |
|
|---|---|
Name |
Description |
`rouge_type` |
`str`
Optional. Supported rouge types are rougen[1-9], rougeL, and rougeLsum. |
`use_stemmer` |
`bool`
Optional. Whether to use stemmer to compute rouge score. |
`split_summaries` |
`bool`
Optional. Whether to split summaries while using rougeLsum. |

## Methods

### RougeSpec

`RougeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontainerspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContainerSpec -->

# Class ContainerSpec (1.134.0)

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Required. The URI of a container image in the Container Registry that is to be run on each worker replica. |
`command` |
`MutableSequence[str]`
The command to be invoked when the container is started. It overrides the entrypoint instruction in Dockerfile when provided. |
`args` |
`MutableSequence[str]`
The arguments to be passed when starting the container. |
`env` |
`MutableSequence[`
Environment variables to be passed to the container. Maximum limit is 100. |

## Methods

### ContainerSpec

`ContainerSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of a Container.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistfeaturesresponse_googlecloudaiplatform_54e6c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistfeaturesresponse_googlecloudaiplatformv_f2fadc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistfeaturesresponse_googlecloudaiplatformv1_80e758.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeaturesresponse_googlecloudaiplatformv1s_052cc5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse -->

# Class ListFeaturesResponse (1.134.0)

`ListFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
The Features matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturesResponse

`ListFeaturesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageclassificationmetadatasuccessfulstopreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictRequest -->

# Class PredictRequest (1.134.0)

`PredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Predict.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] parameters_schema_uri. |
`labels` |
`MutableMapping[str, str]`
Optional. The user labels for Imagen billing usage only. Only Imagen supports labels. For other use cases, it will be ignored. |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### PredictRequest

`PredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Predict.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodeldeploymentresourcestype_googlecloudaiplatfor_c73ee6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentresourcestype_googlecloudaiplatform_5a2a7c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentresourcestype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.DeploymentResourcesType -->

# Class DeploymentResourcesType (1.134.0)

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_RESOURCES_TYPE_UNSPECIFIED` |
Should not be used. |
`DEDICATED_RESOURCES` |
Resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. |
`AUTOMATIC_RESOURCES` |
Resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. |
`SHARED_RESOURCES` |
Resources that can be shared by multiple DeployedModels. A pre-configured DeploymentResourcePool is required. |

## Methods

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnotebookruntimetemplatesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse -->

# Class ListNotebookRuntimeTemplatesResponse (1.134.0)

```
ListNotebookRuntimeTemplatesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimeTemplates.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtime_templates` |
`MutableSequence[`
List of NotebookRuntimeTemplates in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimeTemplatesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimeTemplatesResponse

```
ListNotebookRuntimeTemplatesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimeTemplates.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoobjecttrac_f188d7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoobjecttracking.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTracking -->

# Class AutoMlVideoObjectTracking (1.134.0)

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlVideoObjectTracking

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

### AutoMlVideoObjectTracking

`AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltextclassification.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassification -->

# Class AutoMlTextClassification (1.134.0)

`AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Classification Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextClassification

`AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Classification Model.

### AutoMlTextClassification

`AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Classification Model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesfeatureviewoptimizedconfig_googlecloudaipla_045f25.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureviewoptimizedconfig_googlecloudaiplat_b42ad0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewoptimizedconfig_googlecloudaiplatf_885e6c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewoptimizedconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.OptimizedConfig -->

# Class OptimizedConfig (1.134.0)

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.

## Attribute |
|
|---|---|
Name |
Description |
`automatic_resources` |
Optional. A description of resources that the FeatureView uses, which to large degree are decided by Vertex AI, and optionally allows only a modest additional configuration. If min_replica_count is not set, the default value is 2. If max_replica_count is not set, the default value is 6. The max allowed replica count is 1000. |

## Methods

### OptimizedConfig

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnastrialdetailsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsRequest -->

# Class ListNasTrialDetailsRequest (1.134.0)

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListNasTrialDetailsResponse.next_page_token of the previous JobService.ListNasTrialDetails call. |

## Methods

### ListNasTrialDetailsRequest

`ListNasTrialDetailsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasTrialDetails.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessegment_googlecloudaiplatformv1schematraining_3dafd6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessegment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Segment -->

# Class Segment (1.134.0)

`Segment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Segment of the content.

## Attributes |
|
|---|---|
Name |
Description |
`part_index` |
`int`
Output only. The index of a Part object within its parent Content object. |
`start_index` |
`int`
Output only. Start index in the given Part, measured in bytes. Offset from the start of the Part, inclusive, starting at zero. |
`end_index` |
`int`
Output only. End index in the given Part, measured in bytes. Offset from the start of the Part, exclusive, starting at zero. |
`text` |
`str`
Output only. The text corresponding to the segment from the response. |

## Methods

### Segment

`Segment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Segment of the content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentationmetadatasuccessfulstopreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvide_4098fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideo_68d992.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlvideoclassification.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassification -->

# Class AutoMlVideoClassification (1.134.0)

`AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video Classification Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlVideoClassification

`AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video Classification Model.

### AutoMlVideoClassification

`AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Video Classification Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdeploymentresourcepoolsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDeploymentResourcePoolsResponse -->

# Class ListDeploymentResourcePoolsResponse (1.134.0)

```
ListDeploymentResourcePoolsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ListDeploymentResourcePools method.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_resource_pools` |
`MutableSequence[`
The DeploymentResourcePools from the specified location. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|

## Methods

### ListDeploymentResourcePoolsResponse

```
ListDeploymentResourcePoolsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ListDeploymentResourcePools method.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_garden_service_googlecloudaiplatform_ab721e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_garden_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service -->

# Package model_garden_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.model_garden_service`

package.

## Classes

[ModelGardenServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceAsyncClient)

The interface of Model Garden Service.

[ModelGardenServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.ModelGardenServiceClient)

The interface of Model Garden Service.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers)

API documentation for `aiplatform_v1beta1.services.model_garden_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequestmigrateautomldatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateAutomlDatasetConfig -->

# Class MigrateAutomlDatasetConfig (1.134.0)

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Required. Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
Required. Display name of the Dataset in Vertex AI. System will pick a display name if unspecified. |

## Methods

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicedatasetserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient -->

# Class DatasetServiceClient (1.134.0)

```
DatasetServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that manages Vertex AI Dataset and its child resources.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`DatasetServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### DatasetServiceClient

```
DatasetServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.dataset_service.transports.base.DatasetServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the dataset service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,DatasetServiceTransport,Callable[..., DatasetServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the DatasetServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### annotation_path

```
annotation_path(
project: str, location: str, dataset: str, data_item: str, annotation: str
) -> str
```


Returns a fully-qualified annotation string.

### annotation_spec_path

```
annotation_spec_path(
project: str, location: str, dataset: str, annotation_spec: str
) -> str
```


Returns a fully-qualified annotation_spec string.

### assemble_data

```
assemble_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssembleDataRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Assembles each row of a multimodal dataset and writes the result into a BigQuery table.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_assemble_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AssembleDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssembleDataRequest.html)(
name="name_value",
)
# Make the request
operation = client.[assemble_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_assemble_data)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.AssembleData. Used only for MULTIMODAL datasets. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### assess_data

```
assess_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.AssessDataRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Assesses the state or validity of the dataset with respect to a given use case.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_assess_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
tuning_validation_assessment_config = aiplatform_v1beta1.[TuningValidationAssessmentConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.TuningValidationAssessmentConfig.html)()
tuning_validation_assessment_config.model_name = "model_name_value"
tuning_validation_assessment_config.dataset_usage = "SFT_VALIDATION"
request = aiplatform_v1beta1.[AssessDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AssessDataRequest.html)(
tuning_validation_assessment_config=tuning_validation_assessment_config,
name="name_value",
)
# Make the request
operation = client.[assess_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_assess_data)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.AssessData. Used only for MULTIMODAL datasets. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### cached_content_path

`cached_content_path(project: str, location: str, cached_content: str) -> str`


Returns a fully-qualified cached_content string.

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### create_dataset

```
create_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Creates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetRequest.html)(
parent="parent_value",
dataset=dataset,
)
# Make the request
operation = client.[create_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_create_dataset)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.CreateDataset. |
`parent` |
`str`
Required. The resource name of the Location to create the Dataset in. Format: |
`dataset` |
Required. The Dataset to create. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### create_dataset_version

```
create_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.CreateDatasetVersionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Create a version from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[CreateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateDatasetVersionRequest.html)(
parent="parent_value",
dataset_version=dataset_version,
)
# Make the request
operation = client.[create_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_create_dataset_version)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.CreateDatasetVersion. |
`parent` |
`str`
Required. The name of the Dataset resource. Format: |
`dataset_version` |
Required. The version to be created. The same CMEK policies with the original Dataset will be applied the dataset version. So here we don't need to specify the EncryptionSpecType here. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### data_item_path

`data_item_path(project: str, location: str, dataset: str, data_item: str) -> str`


Returns a fully-qualified data_item string.

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

### dataset_version_path

```
dataset_version_path(
project: str, location: str, dataset: str, dataset_version: str
) -> str
```


Returns a fully-qualified dataset_version string.

### delete_dataset

```
delete_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_dataset)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.DeleteDataset. |
`name` |
`str`
Required. The resource name of the Dataset to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_dataset_version

```
delete_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteDatasetVersionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_dataset_version)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.DeleteDatasetVersion. |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_saved_query

```
delete_saved_query(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.DeleteSavedQueryRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a SavedQuery.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_saved_query():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteSavedQueryRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteSavedQueryRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_saved_query](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_delete_saved_query)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.DeleteSavedQuery. |
`name` |
`str`
Required. The resource name of the SavedQuery to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_data

```
export_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ExportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
export_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.ExportDataConfig
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Exports data from a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_export_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
export_config = aiplatform_v1beta1.[ExportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataConfig.html)()
export_config.gcs_destination.output_uri_prefix = "output_uri_prefix_value"
request = aiplatform_v1beta1.[ExportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportDataRequest.html)(
name="name_value",
export_config=export_config,
)
# Make the request
operation = client.[export_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_export_data)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ExportData. |
`name` |
`str`
Required. The name of the Dataset resource. Format: |
`export_config` |
Required. The desired output location. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`DatasetServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`DatasetServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`DatasetServiceClient` |
The constructed client. |

### get_annotation_spec

```
get_annotation_spec(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetAnnotationSpecRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.annotation_spec.AnnotationSpec
```


Gets an AnnotationSpec.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_annotation_spec():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetAnnotationSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_annotation_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_annotation_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetAnnotationSpec. |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Identifies a concept with which DataItems may be annotated with. |

### get_dataset

```
get_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Gets a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetDataset. |
`name` |
`str`
Required. The name of the Dataset resource. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of DataItems and Annotations on them. |

### get_dataset_version

```
get_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.GetDatasetVersionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Gets a Dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_get_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.GetDatasetVersion. |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Describes the dataset version. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### import_data

```
import_data(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ImportDataRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
import_configs: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.dataset.ImportDataConfig
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Imports data into a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_data():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
import_configs = aiplatform_v1beta1.[ImportDataConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataConfig.html)()
import_configs.gcs_source.uris = ['uris_value1', 'uris_value2']
import_configs.import_schema_uri = "import_schema_uri_value"
request = aiplatform_v1beta1.[ImportDataRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportDataRequest.html)(
name="name_value",
import_configs=import_configs,
)
# Make the request
operation = client.[import_data](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_import_data)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ImportData. |
`name` |
`str`
Required. The name of the Dataset resource. Format: |
`import_configs` |
`MutableSequence[`
Required. The desired input locations. The contents of all input locations will be imported in one batch. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### list_annotations

```
list_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListAnnotationsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListAnnotationsPager
)
```


Lists Annotations belongs to a dataitem.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_annotations():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_annotations)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ListAnnotations. |
`parent` |
`str`
Required. The resource name of the DataItem to list Annotations from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListAnnotations. Iterating over this object will yield results and resolve additional pages automatically. |

### list_data_items

```
list_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsPager
```


Lists DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_data_items)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ListDataItems. |
`parent` |
`str`
Required. The resource name of the Dataset to list DataItems from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

### list_dataset_versions

```
list_dataset_versions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsPager
)
```


Lists DatasetVersions in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_dataset_versions():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_dataset_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_dataset_versions)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ListDatasetVersions. |
`parent` |
`str`
Required. The resource name of the Dataset to list DatasetVersions from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDatasetVersions. Iterating over this object will yield results and resolve additional pages automatically. |

### list_datasets

```
list_datasets(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsPager
```


Lists Datasets in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_datasets():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListDatasetsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_datasets](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_datasets)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ListDatasets. |
`parent` |
`str`
Required. The name of the Dataset's parent resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListDatasets. Iterating over this object will yield results and resolve additional pages automatically. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_saved_queries

```
list_saved_queries(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesPager
)
```


Lists SavedQueries in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_saved_queries():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListSavedQueriesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_saved_queries](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_list_saved_queries)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.ListSavedQueries. |
`parent` |
`str`
Required. The resource name of the Dataset to list SavedQueries from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.ListSavedQueries. Iterating over this object will yield results and resolve additional pages automatically. |

### parse_annotation_path

`parse_annotation_path(path: str) -> typing.Dict[str, str]`


Parses a annotation path into its component segments.

### parse_annotation_spec_path

`parse_annotation_spec_path(path: str) -> typing.Dict[str, str]`


Parses a annotation_spec path into its component segments.

### parse_cached_content_path

`parse_cached_content_path(path: str) -> typing.Dict[str, str]`


Parses a cached_content path into its component segments.

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_data_item_path

`parse_data_item_path(path: str) -> typing.Dict[str, str]`


Parses a data_item path into its component segments.

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_dataset_version_path

`parse_dataset_version_path(path: str) -> typing.Dict[str, str]`


Parses a dataset_version path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### parse_saved_query_path

`parse_saved_query_path(path: str) -> typing.Dict[str, str]`


Parses a saved_query path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### restore_dataset_version

```
restore_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.RestoreDatasetVersionRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Restores a dataset version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_restore_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RestoreDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[restore_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_restore_dataset_version)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.RestoreDatasetVersion. |
`name` |
`str`
Required. The name of the DatasetVersion resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### saved_query_path

```
saved_query_path(
project: str, location: str, dataset: str, saved_query: str
) -> str
```


Returns a fully-qualified saved_query string.

### search_data_items

```
search_data_items(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsPager
)
```


Searches DataItems in a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_data_items():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchDataItemsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsRequest.html)(
order_by_data_item="order_by_data_item_value",
dataset="dataset_value",
)
# Make the request
page_result = client.[search_data_items](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_search_data_items)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.SearchDataItems. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for DatasetService.SearchDataItems. Iterating over this object will yield results and resolve additional pages automatically. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### update_dataset

```
update_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetRequest,
dict,
]
] = None,
*,
dataset: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset.Dataset
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.dataset.Dataset
```


Updates a Dataset.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_dataset():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset = aiplatform_v1beta1.[Dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Dataset.html)()
dataset.display_name = "display_name_value"
dataset.metadata_schema_uri = "metadata_schema_uri_value"
dataset.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetRequest.html)(
dataset=dataset,
)
# Make the request
response = client.[update_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_update_dataset)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.UpdateDataset. |
`dataset` |
Required. The Dataset which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A collection of DataItems and Annotations on them. |

### update_dataset_version

```
update_dataset_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.dataset_service.UpdateDatasetVersionRequest,
dict,
]
] = None,
*,
dataset_version: typing.Optional[
google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.dataset_version.DatasetVersion
```


Updates a DatasetVersion.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_dataset_version():
# Create a client
client = aiplatform_v1beta1.
```[DatasetServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html)()
# Initialize request argument(s)
dataset_version = aiplatform_v1beta1.[DatasetVersion](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetVersion.html)()
dataset_version.metadata.null_value = "NULL_VALUE"
request = aiplatform_v1beta1.[UpdateDatasetVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest.html)(
dataset_version=dataset_version,
)
# Make the request
response = client.[update_dataset_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient.html#google_cloud_aiplatform_v1beta1_services_dataset_service_DatasetServiceClient_update_dataset_version)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for DatasetService.UpdateDatasetVersion. |
`dataset_version` |
Required. The DatasetVersion which replaces the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Describes the dataset version. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesindex_serviceindexserviceasyncclient______goog_70c1e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_serviceindexserviceasyncclient______googl_1c2b16.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_serviceindexserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient -->

# Class IndexServiceAsyncClient (1.134.0)

```
IndexServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Index resources.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`IndexServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### IndexServiceAsyncClient

```
IndexServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,IndexServiceTransport,Callable[..., IndexServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### create_index

```
create_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.CreateIndexRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Creates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_create_index)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.CreateIndex. |
`parent` |
Required. The resource name of the Location to create the Index in. Format: |
`index` |
Required. The Index to create. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### delete_index

```
delete_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.DeleteIndexRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Deletes an Index. An Index can only be deleted when all its xref_DeployedIndexes had been undeployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_delete_index)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.DeleteIndex. |
`name` |
Required. The name of the Index resource to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`IndexServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`IndexServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`IndexServiceAsyncClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_index

```
get_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.GetIndexRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.index.Index
```


Gets an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_get_index)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.GetIndex |
`name` |
Required. The name of the Index resource. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.index_service.transports.base.IndexServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

### index_path

`index_path(project: str, location: str, index: str) -> str`


Returns a fully-qualified index string.

### list_indexes

```
list_indexes(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.ListIndexesRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.services.index_service.pagers.ListIndexesAsyncPager
```


Lists Indexes in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_indexes():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_list_indexes)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.ListIndexes. |
`parent` |
Required. The resource name of the Location from which to list the Indexes. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for IndexService.ListIndexes. Iterating over this object will yield results and resolve additional pages automatically. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_index_endpoint_path

`parse_index_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a index_endpoint path into its component segments.

### parse_index_path

`parse_index_path(path: str) -> typing.Dict[str, str]`


Parses a index path into its component segments.

### remove_datapoints

```
remove_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.index_service.RemoveDatapointsResponse
```


Remove Datapoints from an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_remove_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_remove_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.RemoveDatapoints |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for IndexService.RemoveDatapoints |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### update_index

```
update_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.UpdateIndexRequest, dict
]
] = None,
*,
index: typing.Optional[google.cloud.aiplatform_v1.types.index.Index] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Updates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_index():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
index = aiplatform_v1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_update_index)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.UpdateIndex. |
`index` |
Required. The Index which updates the resource on the server. This corresponds to the |
`update_mask` |
The update mask applies to the resource. For the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### upsert_datapoints

```
upsert_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsRequest, dict
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.index_service.UpsertDatapointsResponse
```


Add/update Datapoints into an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1.
```[IndexServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = await client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_service.IndexServiceAsyncClient.html#google_cloud_aiplatform_v1_services_index_service_IndexServiceAsyncClient_upsert_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for IndexService.UpsertDatapoints |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for IndexService.UpsertDatapoints |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesfeatureonlinestorestate_googlecloudaiplatformv_833217.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeatureonlinestorestate_googlecloudaiplatformv1_93db9f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeatureonlinestorestate_googlecloudaiplatformv1s_e6668a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeatureonlinestorestate_googlecloudaiplatformv1sc_2b2f08.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureonlinestorestate_googlecloudaiplatformv1sch_27fff2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestorestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.State -->

# Class State (1.134.0)

`State(value)`


Possible states a featureOnlineStore can have.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Default value. This value is unused. |
`STABLE` |
State when the featureOnlineStore configuration is not being updated and the fields reflect the current configuration of the featureOnlineStore. The featureOnlineStore is usable in this state. |
`UPDATING` |
The state of the featureOnlineStore configuration when it is being updated. During an update, the fields reflect either the original configuration or the updated configuration of the featureOnlineStore. The featureOnlineStore is still usable in this state. |

## Methods

### State

`State(value)`


Possible states a featureOnlineStore can have.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageobjectdetectionmetadatasuccessfulstopreason.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoremonitoringconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig -->

# Class FeaturestoreMonitoringConfig (1.134.0)

```
FeaturestoreMonitoringConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration of how features in Featurestore are monitored.

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_analysis` |
The config for Snapshot Analysis Based Feature Monitoring. |
`import_features_analysis` |
The config for ImportFeatures Analysis Based Feature Monitoring. |
`numerical_threshold_config` |
Threshold for numerical features of anomaly detection. This is shared by all objectives of Featurestore Monitoring for numerical features (i.e. Features with type (Feature.ValueType) DOUBLE or INT64). |
`categorical_threshold_config` |
Threshold for categorical features of anomaly detection. This is shared by all types of Featurestore Monitoring for categorical features (i.e. Features with type (Feature.ValueType) BOOL or STRING). |

## Classes

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

### SnapshotAnalysis

`SnapshotAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's Snapshot Analysis Based Monitoring. This type of analysis generates statistics for each Feature based on a snapshot of the latest feature value of each entities every monitoring_interval.

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### FeaturestoreMonitoringConfig

```
FeaturestoreMonitoringConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration of how features in Featurestore are monitored.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesqueryexecutioninputsandoutputsrequest_google_4ab313.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesqueryexecutioninputsandoutputsrequest_googlec_de64a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesqueryexecutioninputsandoutputsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExecutionInputsAndOutputsRequest -->

# Class QueryExecutionInputsAndOutputsRequest (1.134.0)

```
QueryExecutionInputsAndOutputsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryExecutionInputsAndOutputs.

## Attribute |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution whose input and output Artifacts should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### QueryExecutionInputsAndOutputsRequest

```
QueryExecutionInputsAndOutputsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryExecutionInputsAndOutputs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service -->

# Package dataset_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.dataset_service`

package.

## Classes

[DatasetServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceAsyncClient)

The service that manages Vertex AI Dataset and its child resources.

[DatasetServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.DatasetServiceClient)

The service that manages Vertex AI Dataset and its child resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers)

API documentation for `aiplatform_v1beta1.services.dataset_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesindex_endpoint_service_googlecloudaiplatform_v1_05acc8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_endpoint_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service -->

# Package index_endpoint_service (1.134.0)

API documentation for `aiplatform_v1.services.index_endpoint_service`

package.

## Classes

[IndexEndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceAsyncClient)

A service for managing Vertex AI's IndexEndpoints.

[IndexEndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.IndexEndpointServiceClient)

A service for managing Vertex AI's IndexEndpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers)

API documentation for `aiplatform_v1.services.index_endpoint_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespurgeartifactsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.134.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesrayspec__googlecloudaiplatform_v1beta1typesdeploy_e76e67.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesrayspec__googlecloudaiplatform_v1beta1typesdeploye_2303c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesrayspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RaySpec -->

# Class RaySpec (1.134.0)

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.

## Attributes |
|
|---|---|
Name |
Description |
`image_uri` |
`str`
Optional. Default image for user to choose a preferred ML framework (for example, TensorFlow or Pytorch) by choosing from `Vertex prebuilt images |
`resource_pool_images` |
`MutableMapping[str, str]`
Optional. Required if image_uri isn't set. A map of resource_pool_id to prebuild Ray image if user need to use different images for different head/worker pools. This map needs to cover all the resource pool ids. Example: { "ray_head_node_pool": "head image" "ray_worker_node_pool1": "worker image" "ray_worker_node_pool2": "another worker image" } |
`head_node_resource_pool_id` |
`str`
Optional. This will be used to indicate which resource pool will serve as the Ray head node(the first node within that pool). Will use the machine from the first workerpool as the head node by default if this field isn't set. |
`ray_metric_spec` |
Optional. Ray metrics configurations. |
`ray_logs_spec` |
Optional. OSS Ray logging configurations. |

## Classes

### ResourcePoolImagesEntry

`ResourcePoolImagesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### RaySpec

`RaySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration information for the Ray cluster. For experimental launch, Ray cluster creation and Persistent cluster creation are 1:1 mapping: We will provision all the nodes within the Persistent cluster as Ray nodes.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployedindexauthconfig_googlecloudaiplatform_24c4bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedindexauthconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.134.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportmodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelOperationMetadata -->

# Class ExportModelOperationMetadata (1.134.0)

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |
`output_info` |
Output only. Information further describing the output of this Model export. |

## Classes

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Methods

### ExportModelOperationMetadata

```
ExportModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of ModelService.ExportModel operation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfunctionresponsepart__googlecloudaiplatform_v_18d7e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctionresponsepart.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponsePart -->

# Class FunctionResponsePart (1.134.0)

`FunctionResponsePart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a `FunctionResponse`

message.

A `FunctionResponsePart`

consists of data which has an associated
datatype. A `FunctionResponsePart`

can only contain one of the
accepted types in `FunctionResponsePart.data`

.

A `FunctionResponsePart`

must have a fixed IANA MIME type
identifying the type and subtype of the media if the `inline_data`

field is filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`inline_data` |
Inline media bytes. This field is a member of `oneof` _ `data` .
|
`file_data` |
URI based data. This field is a member of `oneof` _ `data` .
|

## Methods

### FunctionResponsePart

`FunctionResponsePart(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a `FunctionResponse`

message.

A `FunctionResponsePart`

consists of data which has an associated
datatype. A `FunctionResponsePart`

can only contain one of the
accepted types in `FunctionResponsePart.data`

.

A `FunctionResponsePart`

must have a fixed IANA MIME type
identifying the type and subtype of the media if the `inline_data`

field is filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmodeldeploymentmonitoringjobsresponse_goo_092439.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodeldeploymentmonitoringjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsResponse -->

# Class ListModelDeploymentMonitoringJobsResponse (1.134.0)

```
ListModelDeploymentMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListModelDeploymentMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_jobs` |
`MutableSequence[`
A list of ModelDeploymentMonitoringJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListModelDeploymentMonitoringJobsResponse

```
ListModelDeploymentMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListModelDeploymentMonitoringJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinputmodelmonitoringdatasetmodelmonitoringgcssource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.ModelMonitoringDataset.ModelMonitoringGcsSource -->

# Class ModelMonitoringGcsSource (1.134.0)

`ModelMonitoringGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset spec for data stored in Google Cloud Storage.

## Attributes |
|
|---|---|
Name |
Description |
`gcs_uri` |
`str`
Google Cloud Storage URI to the input file(s). May contain wildcards. For more information on wildcards, see https://cloud.google.com/storage/docs/wildcards. |
`format_` |
Data format of the dataset. |

## Classes

### DataFormat

`DataFormat(value)`


Supported data format.

## Methods

### ModelMonitoringGcsSource

`ModelMonitoringGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset spec for data stored in Google Cloud Storage.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesupdatedatasetversionrequest_googlecloudaip_30d519.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatedatasetversionrequest_googlecloudaipl_5478ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatedatasetversionrequest_googlecloudaipla_0e6474.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatedatasetversionrequest_googlecloudaiplat_58e19d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatedatasetversionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest -->

# Class UpdateDatasetVersionRequest (1.134.0)

`UpdateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDatasetVersion.

## Attributes |
|
|---|---|
Name |
Description |
`dataset_version` |
Required. The DatasetVersion which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
Updatable fields:
- `display_name`
|

## Methods

### UpdateDatasetVersionRequest

`UpdateDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDatasetVersion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardtimeseriesmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.Metadata -->

# Class Metadata (1.134.0)

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`max_step` |
`int`
Output only. Max step index of all data points within a TensorboardTimeSeries. |
`max_wall_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Max wall clock timestamp of all data points within a TensorboardTimeSeries. |
`max_blob_sequence_length` |
`int`
Output only. The largest blob sequence length (number of blobs) of all data points in this time series, if its ValueType is BLOB_SEQUENCE. |

## Methods

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes metadata for a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigrateautomldatasetcon_ecfff6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmigrateresourcerequestmigrateautomldatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateAutomlDatasetConfig -->

# Class MigrateAutomlDatasetConfig (1.134.0)

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
`str`
Required. Full resource name of automl Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}` .
|
`dataset_display_name` |
`str`
Required. Display name of the Dataset in Vertex AI. System will pick a display name if unspecified. |

## Methods

### MigrateAutomlDatasetConfig

`MigrateAutomlDatasetConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for migrating Dataset in automl.googleapis.com to Vertex AI's Dataset.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespurgecontextsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsResponse -->

# Class PurgeContextsResponse (1.134.0)

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Contexts that this request deleted (or, if `force` is false, the number of Contexts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Context names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeContextsResponse

`PurgeContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeContexts.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeploymentresourcepool__googlecloudaiplatform_v1be_99ec5f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeploymentresourcepool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeploymentResourcePool -->

# Class DeploymentResourcePool (1.134.0)

`DeploymentResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. The resource name of the DeploymentResourcePool. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|
`dedicated_resources` |
Required. The underlying DedicatedResources that the DeploymentResourcePool uses. |
`encryption_spec` |
Customer-managed encryption key spec for a DeploymentResourcePool. If set, this DeploymentResourcePool will be secured by this key. Endpoints and the DeploymentResourcePool they deploy in need to have the same EncryptionSpec. |
`service_account` |
`str`
The service account that the DeploymentResourcePool's container(s) run as. Specify the email address of the service account. If this service account is not specified, the container(s) run as a service account that doesn't have access to the resource project. Users deploying the Models to this DeploymentResourcePool must have the `iam.serviceAccounts.actAs` permission on
this service account.
|
`disable_container_logging` |
`bool`
If the DeploymentResourcePool is deployed with custom-trained Models or AutoML Tabular Models, the container(s) of the DeploymentResourcePool will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DeploymentResourcePool was created. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Methods

### DeploymentResourcePool

`DeploymentResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbigquerydestination_googlecloudaiplatformv1be_d0e475.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbigquerydestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQueryDestination -->

# Class BigQueryDestination (1.134.0)

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri` |
`str`
Required. BigQuery URI to a project or table, up to 2000 characters long. When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist. Accepted forms: - BigQuery path. For example: `bq://projectId` or
`bq://projectId.bqDatasetId` or
`bq://projectId.bqDatasetId.bqTableId` .
|

## Methods

### BigQueryDestination

`BigQueryDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The BigQuery location for the output content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlimagesegmentation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentation -->

# Class AutoMlImageSegmentation (1.134.0)

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlImageSegmentation

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

### AutoMlImageSegmentation

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfig__googlecloudaip_36b497.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfig__googlecloudaipl_bd1d15.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig -->

# Class FeaturestoreMonitoringConfig (1.134.0)

```
FeaturestoreMonitoringConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration of how features in Featurestore are monitored.

## Attributes |
|
|---|---|
Name |
Description |
`snapshot_analysis` |
The config for Snapshot Analysis Based Feature Monitoring. |
`import_features_analysis` |
The config for ImportFeatures Analysis Based Feature Monitoring. |
`numerical_threshold_config` |
Threshold for numerical features of anomaly detection. This is shared by all objectives of Featurestore Monitoring for numerical features (i.e. Features with type (Feature.ValueType) DOUBLE or INT64). |
`categorical_threshold_config` |
Threshold for categorical features of anomaly detection. This is shared by all types of Featurestore Monitoring for categorical features (i.e. Features with type (Feature.ValueType) BOOL or STRING). |

## Classes

### ImportFeaturesAnalysis

`ImportFeaturesAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's ImportFeature Analysis Based Monitoring. This type of analysis generates statistics for values of each Feature imported by every ImportFeatureValues operation.

### SnapshotAnalysis

`SnapshotAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's Snapshot Analysis Based Monitoring. This type of analysis generates statistics for each Feature based on a snapshot of the latest feature value of each entities every monitoring_interval.

### ThresholdConfig

`ThresholdConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for Featurestore Monitoring threshold.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### FeaturestoreMonitoringConfig

```
FeaturestoreMonitoringConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Configuration of how features in Featurestore are monitored.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistexamplestoresrequest_googlecloudaiplatfor_02c8e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistexamplestoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest -->

# Class ListExampleStoresRequest (1.134.0)

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ExampleStores from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListExampleStoresRequest

`ListExampleStoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.ListExampleStores.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexporttensorboardtimeseriesdataresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportTensorboardTimeSeriesDataResponse -->

# Class ExportTensorboardTimeSeriesDataResponse (1.134.0)

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series_data_points` |
`MutableSequence[`
The returned time series data points. |
`next_page_token` |
`str`
A token, which can be sent as page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ExportTensorboardTimeSeriesDataResponse

```
ExportTensorboardTimeSeriesDataResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for TensorboardService.ExportTensorboardTimeSeriesData.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesmetadata_64965f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesmetadata__37c039.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata -->

# Class AutoMlTablesMetadata (1.134.0)

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.

### AutoMlTablesMetadata

`AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Tables.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesqueryexecutioninputsandoutputsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryExecutionInputsAndOutputsRequest -->

# Class QueryExecutionInputsAndOutputsRequest (1.134.0)

```
QueryExecutionInputsAndOutputsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryExecutionInputsAndOutputs.

## Attribute |
|
|---|---|
Name |
Description |
`execution` |
`str`
Required. The resource name of the Execution whose input and output Artifacts should be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|

## Methods

### QueryExecutionInputsAndOutputsRequest

```
QueryExecutionInputsAndOutputsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryExecutionInputsAndOutputs.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeployedindexauthconfig_googlecloudaiplatform_v1be_bf04f7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedindexauthconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndexAuthConfig -->

# Class DeployedIndexAuthConfig (1.134.0)

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.

## Attribute |
|
|---|---|
Name |
Description |
`auth_provider` |
Defines the authentication provider that the DeployedIndex uses. |

## Classes

### AuthProvider

`AuthProvider(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for an authentication provider, including support for
```
JSON Web Token
(JWT) <https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32>
```

__.

## Methods

### DeployedIndexAuthConfig

`DeployedIndexAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used to set up the auth on the DeployedIndex's private endpoint.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmemory_bank_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service -->

# Package memory_bank_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.memory_bank_service`

package.

## Classes

[MemoryBankServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceAsyncClient)

A service for managing memories for LLM applications.

[MemoryBankServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.MemoryBankServiceClient)

A service for managing memories for LLM applications.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers)

API documentation for `aiplatform_v1beta1.services.memory_bank_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicespersistent_resource_servicepersistentresou_57aa8f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespersistent_resource_servicepersistentresourceserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient -->

# Class PersistentResourceServiceClient (1.134.0)

```
PersistentResourceServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning PersistentResource.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`PersistentResourceServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### PersistentResourceServiceClient

```
PersistentResourceServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the persistent resource service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,PersistentResourceServiceTransport,Callable[..., PersistentResourceServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the PersistentResourceServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If mutual TLS transport creation failed for any reason. |

### __exit__

`__exit__(type, value, traceback)`


Releases underlying transport's resources.

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### create_persistent_resource

```
create_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
] = None,
persistent_resource_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Creates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_create_persistent_resource)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PersistentResourceService.CreatePersistentResource. |
`parent` |
`str`
Required. The resource name of the Location to create the PersistentResource in. Format: |
`persistent_resource` |
Required. The PersistentResource to create. This corresponds to the |
`persistent_resource_id` |
`str`
Required. The ID to use for the PersistentResource, which become the final component of the PersistentResource's resource name. The maximum length is 63 characters, and valid characters are |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### delete_persistent_resource

```
delete_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.DeletePersistentResourceRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Deletes a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_delete_persistent_resource)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PersistentResourceService.DeletePersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`PersistentResourceServiceClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`PersistentResourceServiceClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`PersistentResourceServiceClient` |
The constructed client. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Deprecated. Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_persistent_resource

```
get_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.GetPersistentResourceRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
```


Gets a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_get_persistent_resource)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PersistentResourceService.GetPersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents long-lasting resources that are dedicated to users to runs custom workloads. A PersistentResource can have multiple node pools and each node pool can have its own machine spec. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### list_persistent_resources

```
list_persistent_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesPager
)
```


Lists PersistentResources in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_list_persistent_resources)(request=request)
# Handle the response
for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [PersistentResourceService.ListPersistentResource][]. |
`parent` |
`str`
Required. The resource name of the Location to list the PersistentResources from. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for PersistentResourceService.ListPersistentResources Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_persistent_resource_path

`parse_persistent_resource_path(path: str) -> typing.Dict[str, str]`


Parses a persistent_resource path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### persistent_resource_path

```
persistent_resource_path(
project: str, location: str, persistent_resource: str
) -> str
```


Returns a fully-qualified persistent_resource string.

### reboot_persistent_resource

```
reboot_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.RebootPersistentResourceRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Reboots a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_reboot_persistent_resource)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for PersistentResourceService.RebootPersistentResource. |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### update_persistent_resource

```
update_persistent_resource(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1beta1.types.persistent_resource.PersistentResource
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
```


Updates a PersistentResource.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1beta1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1beta1_services_persistent_resource_service_PersistentResourceServiceClient_update_persistent_resource)(request=request)
print("Waiting for operation to complete...")
response = operation.result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for UpdatePersistentResource method. |
`persistent_resource` |
Required. The PersistentResource to update. The PersistentResource's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Specify the fields to be overwritten in the PersistentResource by the update method. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation.Operation` |
An object representing a long-running operation. The result type for the operation will be
|

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesschema___googlecloudaiplatform_v1beta1types_4fe51a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesschema___googlecloudaiplatform_v1beta1typesp_8a824e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesschema___googlecloudaiplatform_v1beta1typespu_fc2229.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Schema -->

# Class Schema (1.134.0)

`Schema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema is used to define the format of input/output data. Represents
a select subset of an ```
OpenAPI 3.0 schema
object <https://spec.openapis.org/oas/v3.0.3#schema-object>
```

__. More
fields may be added in the future as needed.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Optional. The type of the data. |
`format_` |
`str`
Optional. The format of the data. Supported formats: for NUMBER type: "float", "double" for INTEGER type: "int32", "int64" for STRING type: "email", "byte", etc |
`title` |
`str`
Optional. The title of the Schema. |
`description` |
`str`
Optional. The description of the data. |
`nullable` |
`bool`
Optional. Indicates if the value may be null. |
`default` |
`google.protobuf.struct_pb2.Value`
Optional. Default value of the data. |
`items` |
`google.cloud.aiplatform_v1beta1.types.Schema`
Optional. SCHEMA FIELDS FOR TYPE ARRAY Schema of the elements of Type.ARRAY. |
`min_items` |
`int`
Optional. Minimum number of the elements for Type.ARRAY. |
`max_items` |
`int`
Optional. Maximum number of the elements for Type.ARRAY. |
`enum` |
`MutableSequence[str]`
Optional. Possible values of the element of Type.STRING with enum format. For example we can define an Enum Direction as : {type:STRING, format:enum, enum:["EAST", NORTH", "SOUTH", "WEST"]} |
`properties` |
`MutableMapping[str, google.cloud.aiplatform_v1beta1.types.Schema]`
Optional. SCHEMA FIELDS FOR TYPE OBJECT Properties of Type.OBJECT. |
`property_ordering` |
`MutableSequence[str]`
Optional. The order of the properties. Not a standard field in open api spec. Only used to support the order of the properties. |
`required` |
`MutableSequence[str]`
Optional. Required properties of Type.OBJECT. |
`min_properties` |
`int`
Optional. Minimum number of the properties for Type.OBJECT. |
`max_properties` |
`int`
Optional. Maximum number of the properties for Type.OBJECT. |
`minimum` |
`float`
Optional. SCHEMA FIELDS FOR TYPE INTEGER and NUMBER Minimum value of the Type.INTEGER and Type.NUMBER |
`maximum` |
`float`
Optional. Maximum value of the Type.INTEGER and Type.NUMBER |
`min_length` |
`int`
Optional. SCHEMA FIELDS FOR TYPE STRING Minimum length of the Type.STRING |
`max_length` |
`int`
Optional. Maximum length of the Type.STRING |
`pattern` |
`str`
Optional. Pattern of the Type.STRING to restrict a string to a regular expression. |
`example` |
`google.protobuf.struct_pb2.Value`
Optional. Example of the object. Will only populated when the object is the root. |
`any_of` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.Schema]`
Optional. The value should be validated against any (one or more) of the subschemas in the list. |
`additional_properties` |
`google.protobuf.struct_pb2.Value`
Optional. Can either be a boolean or an object; controls the presence of additional properties. |
`ref` |
`str`
Optional. Allows indirect references between schema nodes. The value should be a valid reference to a child of the root `defs` .
For example, the following schema defines a reference to a
schema node named "Pet":
type: object properties: pet: ref: #/defs/Pet defs: Pet:
type: object properties: name: type: string
The value of the "pet" property is a reference to the schema
node named "Pet". See details in
https://json-schema.org/understanding-json-schema/structuring
|
`defs` |
`MutableMapping[str, google.cloud.aiplatform_v1beta1.types.Schema]`
Optional. A map of definitions for use by `ref` Only
allowed at the root of the schema.
|

## Classes

### DefsEntry

`DefsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### PropertiesEntry

`PropertiesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### Schema

`Schema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema is used to define the format of input/output data. Represents
a select subset of an ```
OpenAPI 3.0 schema
object <https://spec.openapis.org/oas/v3.0.3#schema-object>
```

__. More
fields may be added in the future as needed.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespurgeartifactsresponse_googlecloudaiplatform_c9b65a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespurgeartifactsresponse_googlecloudaiplatform__73e30d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespurgeartifactsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsResponse -->

# Class PurgeArtifactsResponse (1.134.0)

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Artifacts that this request deleted (or, if `force` is false, the number of Artifacts that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Artifact names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeArtifactsResponse

`PurgeArtifactsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeArtifacts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeatureonlinestoresresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse -->

# Class ListFeatureOnlineStoresResponse (1.134.0)

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.

## Attributes |
|
|---|---|
Name |
Description |
`feature_online_stores` |
`MutableSequence[`
The FeatureOnlineStores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureOnlineStoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureOnlineStoresResponse

```
ListFeatureOnlineStoresResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnasjobspecmultitrialalgorithmspectraintrialsp_912720.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnasjobspecmultitrialalgorithmspectraintrialspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec.MultiTrialAlgorithmSpec.TrainTrialSpec -->

# Class TrainTrialSpec (1.134.0)

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.

## Attributes |
|
|---|---|
Name |
Description |
`train_trial_job_spec` |
Required. The spec of a train trial job. The same spec applies to all train trials. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`frequency` |
`int`
Required. Frequency of search trials to start train stage. Top N [TrainTrialSpec.max_parallel_trial_count] search trials will be trained for every M [TrainTrialSpec.frequency] trials searched. |

## Methods

### TrainTrialSpec

`TrainTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for train trials.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplainresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplainResponse -->

# Class ExplainResponse (1.134.0)

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`MutableSequence[`
The explanations of the Model's PredictResponse.predictions. It has the same number of elements as instances to be explained. |
`deployed_model_id` |
`str`
ID of the Endpoint's DeployedModel that served this explanation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
The predictions that are the output of the predictions call. Same as PredictResponse.predictions. |

## Methods

### ExplainResponse

`ExplainResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.Explain.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmenta_301125.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentat_a6f48b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentati_e59a31.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentation -->

# Class AutoMlImageSegmentation (1.134.0)

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |
`metadata` |
The metadata information. |

## Methods

### AutoMlImageSegmentation

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

### AutoMlImageSegmentation

`AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigratableresourcemlenginemodelversion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigratableResource.MlEngineModelVersion -->

# Class MlEngineModelVersion (1.134.0)

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
The ml.googleapis.com endpoint that this model Version currently lives in. Example values: - ml.googleapis.com - us-centrall-ml.googleapis.com - europe-west4-ml.googleapis.com - asia-east1-ml.googleapis.com |
`version` |
`str`
Full resource name of ml engine model Version. Format: `projects/{project}/models/{model}/versions/{version}` .
|

## Methods

### MlEngineModelVersion

`MlEngineModelVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents one model Version in ml.googleapis.com.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesspeculativedecodingspecngramspeculation_googleclou_369ef0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesspeculativedecodingspecngramspeculation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeculativeDecodingSpec.NgramSpeculation -->

# Class NgramSpeculation (1.134.0)

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.

## Attribute |
|
|---|---|
Name |
Description |
`ngram_size` |
`int`
The number of last N input tokens used as ngram to search/match against the previous prompt sequence. This is equal to the N in N-Gram. The default value is 3 if not specified. |

## Methods

### NgramSpeculation

`NgramSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


N-Gram speculation works by trying to find matching tokens in the previous prompt sequence and use those as speculation for generating new tokens.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetfeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest -->

# Class GetFeatureRequest (1.134.0)

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Feature resource. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|

## Methods

### GetFeatureRequest

`GetFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesliststudiesrequest_googlecloudaiplatform_v1t_3d45a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesliststudiesrequest_googlecloudaiplatform_v1ty_bcbed3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesliststudiesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesRequest -->

# Class ListStudiesRequest (1.134.0)

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`
|
`page_token` |
`str`
Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages. |
`page_size` |
`int`
Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default. |

## Methods

### ListStudiesRequest

`ListStudiesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.ListStudies.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewserviceagenttype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.ServiceAgentType -->

# Class ServiceAgentType (1.134.0)

`ServiceAgentType(value)`


Service agent type used during data sync.

## Enums |
|
|---|---|
Name |
Description |
`SERVICE_AGENT_TYPE_UNSPECIFIED` |
By default, the project-level Vertex AI Service Agent is enabled. |
`SERVICE_AGENT_TYPE_PROJECT` |
Indicates the project-level Vertex AI Service Agent (https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents) will be used during sync jobs. |
`SERVICE_AGENT_TYPE_FEATURE_VIEW` |
Enable a FeatureView service account to be created by Vertex AI and output in the field `service_account_email`. This service account will be used to read from the source BigQuery table during sync. |

## Methods

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during data sync.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistfeaturestoresrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresRequest -->

# Class ListFeaturestoresRequest (1.134.0)

`ListFeaturestoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list Featurestores. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the featurestores that match the filter expression. The following fields are supported: - `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `online_serving_config.fixed_node_count` : Supports
`=` , `!=` , , `>` , `<>` , and `>=`
comparisons.
- `labels` : Supports key-value equality and key presence.
Examples:
- `create_time > "2020-01-01" OR update_time > "2020-01-01"`
Featurestores created or updated after 2020-01-01.
- `labels.env = "prod"` Featurestores with label "env" set
to "prod".
|
`page_size` |
`int`
The maximum number of Featurestores to return. The service may return fewer than this value. If unspecified, at most 100 Featurestores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListFeaturestores call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListFeaturestores must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields: - `create_time`
- `update_time`
- `online_serving_config.fixed_node_count`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListFeaturestoresRequest

`ListFeaturestoresRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeaturestores.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfiltersplit__googlecloudaiplatform_v1beta1typesr_67bfde.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfiltersplit__googlecloudaiplatform_v1beta1typesre_77698c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfiltersplit__googlecloudaiplatform_v1beta1typesret_1d3e44.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfiltersplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FilterSplit -->

# Class FilterSplit (1.134.0)

`FilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`validation_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`test_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |

## Methods

### FilterSplit

`FilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesretrievalmetadata_googlecloudaiplatform_v1bet_382b63.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievalmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrievalMetadata -->

# Class RetrievalMetadata (1.134.0)

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.

## Attribute |
|
|---|---|
Name |
Description |
`google_search_dynamic_retrieval_score` |
`float`
Optional. Score indicating how likely information from Google Search could help answer the prompt. The score is in the range `[0, 1]` , where 0 is the least likely and 1 is
the most likely. This score is only populated when Google
Search grounding and dynamic retrieval is enabled. It will
be compared to the threshold to determine whether to trigger
Google Search.
|

## Methods

### RetrievalMetadata

`RetrievalMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata related to retrieval in the grounding flow.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_cache_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service -->

# Package gen_ai_cache_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.gen_ai_cache_service`

package.

## Classes

[GenAiCacheServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceAsyncClient)

Service for managing Vertex AI's CachedContent resource.

[GenAiCacheServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.GenAiCacheServiceClient)

Service for managing Vertex AI's CachedContent resource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers)

API documentation for `aiplatform_v1beta1.services.gen_ai_cache_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodeldeploymentresourcestype_googlecloudaipl_8caa92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentresourcestype_googlecloudaipla_432994.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentresourcestype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.DeploymentResourcesType -->

# Class DeploymentResourcesType (1.134.0)

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_RESOURCES_TYPE_UNSPECIFIED` |
Should not be used. |
`DEDICATED_RESOURCES` |
Resources that are dedicated to the DeployedModel, and that need a higher degree of manual configuration. |
`AUTOMATIC_RESOURCES` |
Resources that to large degree are decided by Vertex AI, and require only a modest additional configuration. |
`SHARED_RESOURCES` |
Resources that can be shared by multiple DeployedModels. A pre-configured DeploymentResourcePool is required. |

## Methods

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnotebookruntimetemplatesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse -->

# Class ListNotebookRuntimeTemplatesResponse (1.134.0)

```
ListNotebookRuntimeTemplatesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimeTemplates.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtime_templates` |
`MutableSequence[`
List of NotebookRuntimeTemplates in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimeTemplatesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimeTemplatesResponse

```
ListNotebookRuntimeTemplatesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimeTemplates.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfunctioncallingconfigmode_googlecloudaiplatform_v1_ef3aee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfunctioncallingconfigmode.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionCallingConfig.Mode -->

# Class Mode (1.134.0)

`Mode(value)`


Function calling mode.

## Enums |
|
|---|---|
Name |
Description |
`MODE_UNSPECIFIED` |
Unspecified function calling mode. This value should not be used. |
`AUTO` |
Default model behavior, model decides to predict either function calls or natural language response. |
`ANY` |
Model is constrained to always predicting function calls only. If "allowed_function_names" are set, the predicted function calls will be limited to any one of "allowed_function_names", else the predicted function calls will be any one of the provided "function_declarations". |
`NONE` |
Model will not predict any function calls. Model behavior is same as when not passing any function declarations. |

## Methods

### Mode

`Mode(value)`


Function calling mode.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardblobdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardBlobDataRequest -->

# Class ReadTensorboardBlobDataRequest (1.134.0)

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.

## Attributes |
|
|---|---|
Name |
Description |
`time_series` |
`str`
Required. The resource name of the TensorboardTimeSeries to list Blobs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|
`blob_ids` |
`MutableSequence[str]`
IDs of the blobs to read. |

## Methods

### ReadTensorboardBlobDataRequest

```
ReadTensorboardBlobDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ReadTensorboardBlobData.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeploymentresourcepool__googlecloudaiplatfor_5594c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeploymentresourcepool__googlecloudaiplatform_5ea8c6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploymentresourcepool.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentResourcePool -->

# Class DeploymentResourcePool (1.134.0)

`DeploymentResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. The resource name of the DeploymentResourcePool. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|
`dedicated_resources` |
Required. The underlying DedicatedResources that the DeploymentResourcePool uses. |
`encryption_spec` |
Customer-managed encryption key spec for a DeploymentResourcePool. If set, this DeploymentResourcePool will be secured by this key. Endpoints and the DeploymentResourcePool they deploy in need to have the same EncryptionSpec. |
`service_account` |
`str`
The service account that the DeploymentResourcePool's container(s) run as. Specify the email address of the service account. If this service account is not specified, the container(s) run as a service account that doesn't have access to the resource project. Users deploying the Models to this DeploymentResourcePool must have the `iam.serviceAccounts.actAs` permission on
this service account.
|
`disable_container_logging` |
`bool`
If the DeploymentResourcePool is deployed with custom-trained Models or AutoML Tabular Models, the container(s) of the DeploymentResourcePool will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DeploymentResourcePool was created. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Methods

### DeploymentResourcePool

`DeploymentResourcePool(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A description of resources that can be shared by multiple DeployedModels, whose underlying specification consists of a DedicatedResources.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistragcorporarequest_googlecloudaiplatform_v1beta_a304e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistragcorporarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagCorporaRequest -->

# Class ListRagCorporaRequest (1.134.0)

`ListRagCorporaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagCorpora.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the RagCorpora. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListRagCorporaResponse.next_page_token of the previous VertexRagDataService.ListRagCorpora call. |

## Methods

### ListRagCorporaRequest

`ListRagCorporaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.ListRagCorpora.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespurgeexecutionsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsResponse -->

# Class PurgeExecutionsResponse (1.134.0)

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`purge_count` |
`int`
The number of Executions that this request deleted (or, if `force` is false, the number of Executions that will be
deleted). This can be an estimate.
|
`purge_sample` |
`MutableSequence[str]`
A sample of the Execution names that will be deleted. Only populated if `force` is set to false. The maximum number
of samples is 100 (it is possible to return fewer).
|

## Methods

### PurgeExecutionsResponse

`PurgeExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.PurgeExecutions.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestrainingconfig_googlecloudaiplatform_v1typesexpor_70f666.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestrainingconfig_googlecloudaiplatform_v1typesexport_34e6f0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrainingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TrainingConfig -->

# Class TrainingConfig (1.134.0)

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.

## Attribute |
|
|---|---|
Name |
Description |
`timeout_training_milli_hours` |
`int`
The timeout hours for the CMLE training job, expressed in milli hours i.e. 1,000 value in this field means 1 hour. |

## Methods

### TrainingConfig

`TrainingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


CMLE training config. For every active learning labeling iteration, system will train a machine learning model on CMLE. The trained model will be used by data sampling algorithm to select DataItems.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest -->

# Class ExportModelRequest (1.134.0)

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. |
`output_config` |
Required. The desired output location and configuration. |

## Classes

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Methods

### ExportModelRequest

`ExportModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ExportModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfiltersplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FilterSplit -->

# Class FilterSplit (1.134.0)

`FilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`validation_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |
`test_filter` |
`str`
Required. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. |

## Methods

### FilterSplit

`FilterSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the given filters, data pieces not matched by any filter are ignored. Currently only supported for Datasets containing DataItems. If any of the filters in this message are to match nothing, then they can be set as '-' (the minus sign).

Supported only for unstructured Datasets.
