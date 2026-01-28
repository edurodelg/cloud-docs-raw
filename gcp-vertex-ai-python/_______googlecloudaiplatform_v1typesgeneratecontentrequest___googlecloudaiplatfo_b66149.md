---
merged_at: 2026-01-28T15:11:44.722417
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentRequest -->

# Class GenerateContentRequest (1.134.0)

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`
Tuned model endpoint format:
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. |
`system_instruction` |
Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph. This field is a member of `oneof` _ `_system_instruction` .
|
`cached_content` |
`str`
Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`
|
`tools` |
`MutableSequence[`
Optional. A list of `Tools` the model may use to generate
the next response.
A `Tool` is a piece of code that enables the system to
interact with external systems to perform an action, or set
of actions, outside of knowledge and scope of the model.
|
`tool_config` |
Optional. Tool config. This config is shared for all tools provided in the request. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only. Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter. |
`safety_settings` |
`MutableSequence[`
Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates. |
`model_armor_config` |
Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety_settings must not be supplied. |
`generation_config` |
Optional. Generation config. |

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

### GenerateContentRequest

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateAutomlDatasetConfig -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryExecutionInputsAndOutputsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig -->

# Class VectorSearchConfig (1.134.0)

`VectorSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated. Use IndexConfig instead.

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
`tree_ah_config` |
Optional. Configuration options for the tree-AH algorithm (Shallow tree + Asymmetric Hashing). Please refer to this paper for more details: https://arxiv.org/abs/1908.10396 This field is a member of `oneof` _ `algorithm_config` .
|
`brute_force_config` |
`google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.BruteForceConfig`
Optional. Configuration options for using brute force search, which simply implements the standard linear search in the database for each query. It is primarily meant for benchmarking and to generate the ground truth for approximate search. This field is a member of `oneof` _ `algorithm_config` .
|
`embedding_column` |
`str`
Optional. Column of embedding. This column contains the source data to create index for vector search. embedding_column must be set when using vector search. |
`filter_columns` |
`MutableSequence[str]`
Optional. Columns of features that're used to filter vector search results. |
`crowding_column` |
`str`
Optional. Column of crowding. This column contains crowding attribute which is a constraint on a neighbor list produced by FeatureOnlineStoreService.SearchNearestEntities to diversify search results. If NearestNeighborQuery.per_crowding_attribute_neighbor_count is set to K in SearchNearestEntitiesRequest, it's guaranteed that no more than K entities of the same crowding attribute are returned in the response. |
`embedding_dimension` |
`int`
Optional. The number of dimensions of the input embedding. This field is a member of `oneof` _ `_embedding_dimension` .
|
`distance_measure_type` |
Optional. The distance measure used in nearest neighbor search. |

## Classes

### DistanceMeasureType

`DistanceMeasureType(value)`


```
We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.
```


### TreeAHConfig

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### VectorSearchConfig

`VectorSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated. Use IndexConfig instead.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJob -->

# Class CustomJob (1.134.0)

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a CustomJob. |
`display_name` |
`str`
Required. The display name of the CustomJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`job_spec` |
Required. Job spec. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### CustomJob

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentRequest -->

# Class GenerateContentRequest (1.134.0)

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The fully qualified name of the publisher model or tuned model endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`
Tuned model endpoint format:
`projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`contents` |
`MutableSequence[`
Required. The content of the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history + latest request. |
`system_instruction` |
Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph. This field is a member of `oneof` _ `_system_instruction` .
|
`cached_content` |
`str`
Optional. The name of the cached content used as context to serve the prediction. Note: only used in explicit caching, where users can have control over caching (e.g. what content to cache) and enjoy guaranteed cost savings. Format: `projects/{project}/locations/{location}/cachedContents/{cachedContent}`
|
`tools` |
`MutableSequence[`
Optional. A list of `Tools` the model may use to generate
the next response.
A `Tool` is a piece of code that enables the system to
interact with external systems to perform an action, or set
of actions, outside of knowledge and scope of the model.
|
`tool_config` |
Optional. Tool config. This config is shared for all tools provided in the request. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only. Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter. |
`safety_settings` |
`MutableSequence[`
Optional. Per request settings for blocking unsafe content. Enforced on GenerateContentResponse.candidates. |
`model_armor_config` |
Optional. Settings for prompt and response sanitization using the Model Armor service. If supplied, safety_settings must not be supplied. |
`generation_config` |
Optional. Generation config. |

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

### GenerateContentRequest

`GenerateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [PredictionService.GenerateContent].

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeaturestoreRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.OptimizedConfig -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.CorpusTypeConfig -->

# Class CorpusTypeConfig (1.134.0)

`CorpusTypeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the corpus type of the RagCorpus.

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
`document_corpus` |
Optional. Config for the document corpus. This field is a member of `oneof` _ `corpus_type_config` .
|
`memory_corpus` |
Optional. Config for the memory corpus. This field is a member of `oneof` _ `corpus_type_config` .
|

## Classes

### DocumentCorpus

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

### MemoryCorpus

`MemoryCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the memory corpus.

## Methods

### CorpusTypeConfig

`CorpusTypeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the corpus type of the RagCorpus.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MachineSpec -->

# Class MachineSpec (1.134.0)

`MachineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a single machine.

## Attributes |
|
|---|---|
Name |
Description |
`machine_type` |
`str`
Immutable. The type of the machine. See the `list of machine types supported for prediction |
`accelerator_type` |
Immutable. The type of accelerator(s) that may be attached to the machine as per accelerator_count. |
`accelerator_count` |
`int`
The number of accelerators to attach to the machine. |
`gpu_partition_size` |
`str`
Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to `Nvidia GPU Partitioning |
`tpu_topology` |
`str`
Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1"). |
`multihost_gpu_node_count` |
`int`
Optional. Immutable. The number of nodes per replica for multihost GPU deployments. |
`reservation_affinity` |
Optional. Immutable. Configuration controlling how this resource pool consumes reservation. |
`min_gpu_driver_version` |
`str`
Optional. Immutable. The minimum GPU driver version that this machine requires. For example, "535.104.06". If not specified, the default GPU driver version will be used by the underlying infrastructure. |

## Methods

### MachineSpec

`MachineSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification of a single machine.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionMetadata.SuccessfulStopReason -->

# Class SuccessfulStopReason (1.134.0)

Further training of the Model ceased to increase its quality, since it already has converged.

Methods

SuccessfulStopReason

SuccessfulStopReason(value)

SuccessfulStopReason

SuccessfulStopReason(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDatasetVersionRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.DeploymentResourcesType -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient -->

# Class ReasoningEngineExecutionServiceAsyncClient (1.134.0)

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for executing queries on Reasoning Engine.

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
`ReasoningEngineExecutionServiceTransport` |
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

### ReasoningEngineExecutionServiceAsyncClient

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineExecutionServiceTransport,Callable[..., ReasoningEngineExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport
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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### query_reasoning_engine

```
query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.QueryReasoningEngineRequest,
dict,
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
) -> (
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.QueryReasoningEngineResponse
)
```


Queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_query_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_query_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.Query][]. |
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
Response message for [ReasoningEngineExecutionService.Query][] |

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### stream_query_reasoning_engine

```
stream_query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.reasoning_engine_execution_service.StreamQueryReasoningEngineRequest,
dict,
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
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Streams queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_stream_query_reasoning_engine():
# Create a client
client = aiplatform_v1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[StreamQueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StreamQueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
stream = await client.[stream_query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_stream_query_reasoning_engine)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.StreamQuery][]. |
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
`AsyncIterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient -->

# Class EndpointServiceAsyncClient (1.134.0)

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Endpoints.

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
`EndpointServiceTransport` |
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

### EndpointServiceAsyncClient

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the endpoint service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EndpointServiceTransport,Callable[..., EndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_endpoint

```
create_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
endpoint_id: typing.Optional[str] = None,
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


Creates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_create_endpoint)(request=request)
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
The request object. Request message for EndpointService.CreateEndpoint. |
`parent` |
Required. The resource name of the Location to create the Endpoint in. Format: |
`endpoint` |
Required. The Endpoint to create. This corresponds to the |
`endpoint_id` |
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are |
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

### delete_endpoint

```
delete_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeleteEndpointRequest,
dict,
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


Deletes an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_delete_endpoint)(request=request)
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
The request object. Request message for EndpointService.DeleteEndpoint. |
`name` |
Required. The name of the Endpoint resource to be deleted. Format: |
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

### deploy_model

```
deploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Deploys a Model into this Endpoint, creating a DeployedModel within it.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_deploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_deploy_model)(request=request)
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
The request object. Request message for EndpointService.DeployModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to deploy a Model. Format: |
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. This corresponds to the |
`traffic_split` |
`:class:`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. This corresponds to the |
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

### deployment_resource_pool_path

```
deployment_resource_pool_path(
project: str, location: str, deployment_resource_pool: str
) -> str
```


Returns a fully-qualified deployment_resource_pool string.

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### fetch_publisher_model_config

```
fetch_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.FetchPublisherModelConfigRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
```


Fetches the configs of publisher models.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_fetch_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[fetch_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_fetch_publisher_model_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.FetchPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
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
This message contains configs of a publisher model. |

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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
The constructed client. |

### get_endpoint

```
get_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.GetEndpointRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Gets an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_get_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.GetEndpoint |
`name` |
Required. The name of the Endpoint resource. Format: |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

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
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport
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

### list_endpoints

```
list_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
dict,
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
) -> (
google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager
)
```


Lists Endpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_list_endpoints)(request=request)
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
The request object. Request message for EndpointService.ListEndpoints. |
`parent` |
Required. The resource name of the Location from which to list the Endpoints. Format: |
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
Response message for EndpointService.ListEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### model_deployment_monitoring_job_path

```
model_deployment_monitoring_job_path(
project: str, location: str, model_deployment_monitoring_job: str
) -> str
```


Returns a fully-qualified model_deployment_monitoring_job string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### mutate_deployed_model

```
mutate_deployed_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
] = None,
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


Updates an existing deployed model. Updatable fields include
`min_replica_count`

, `max_replica_count`

,
`required_replica_count`

, `autoscaling_metric_specs`

,
`disable_container_logging`

(v1 only), and
`enable_container_logging`

(v1beta1 only).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_mutate_deployed_model)(request=request)
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
The request object. Request message for EndpointService.MutateDeployedModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: |
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - |
`update_mask` |
Required. The update mask applies to the resource. See |
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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

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

### set_publisher_model_config

```
set_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.SetPublisherModelConfigRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
publisher_model_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
] = None,
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


Sets (creates or updates) configs of publisher models. For example, sets the request/response logging config.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_set_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SetPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
operation = client.[set_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_set_publisher_model_config)(request=request)
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
The request object. Request message for EndpointService.SetPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
`publisher_model_config` |
Required. The publisher model config. This corresponds to the |
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

### undeploy_model

```
undeploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UndeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_undeploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_undeploy_model)(request=request)
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
The request object. Request message for EndpointService.UndeployModel. |
`endpoint` |
Required. The name of the Endpoint resource from which to undeploy a Model. Format: |
`deployed_model_id` |
Required. The ID of the DeployedModel to be undeployed from the Endpoint. This corresponds to the |
`traffic_split` |
`:class:`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. This corresponds to the |
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

### update_endpoint

```
update_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Updates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = await client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.UpdateEndpoint. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. See |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

### update_endpoint_long_running

```
update_endpoint_long_running(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
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


Updates an Endpoint with a long running operation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint_long_running)(request=request)
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
The request object. Request message for EndpointService.UpdateEndpointLongRunning. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJob -->

# Class CustomJob (1.134.0)

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a CustomJob. |
`display_name` |
`str`
Required. The display name of the CustomJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`job_spec` |
Required. Job spec. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the CustomJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

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

### WebAccessUrisEntry

`WebAccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### CustomJob

`CustomJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a job that runs custom workloads such as a Docker container or a Python package. A CustomJob can have multiple worker pools and each worker pool can have its own machine and input spec. A CustomJob will be cleaned up once the job enters terminal state (failed or succeeded).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEntityTypeRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.Metadata -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BigQueryDestination -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionOperation -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WorkerPoolSpec -->

# Class WorkerPoolSpec (1.134.0)

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

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
`container_spec` |
The custom container task. This field is a member of `oneof` _ `task` .
|
`python_package_spec` |
The Python packaged task. This field is a member of `oneof` _ `task` .
|
`machine_spec` |
Optional. Immutable. The specification of a single machine. |
`replica_count` |
`int`
Optional. The number of worker replicas to use for this worker pool. |
`nfs_mounts` |
`MutableSequence[`
Optional. List of NFS mount spec. |
`lustre_mounts` |
`MutableSequence[`
Optional. List of Lustre mounts. |
`disk_spec` |
Disk spec. |

## Methods

### WorkerPoolSpec

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource.MlEngineModelVersion -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateAutomlDatasetConfig -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsResponse -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExecutionInputsAndOutputsRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob -->

# Class AutoMLTextTrainingJob (1.134.0)

```
AutoMLTextTrainingJob(
display_name: str,
prediction_type: str,
multi_label: bool = False,
sentiment_max: int = 10,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a AutoML Text Training Job.

## Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`prediction_type` |
`str`
The type of prediction the Model is to produce, one of: "classification" - A classification model analyzes text data and returns a list of categories that apply to the text found in the data. Vertex AI offers both single-label and multi-label text classification models. "extraction" - An entity extraction model inspects text data for known entities referenced in the data and labels those entities in the text. "sentiment" - A sentiment analysis model inspects text data and identifies the prevailing emotional opinion within it, especially to determine a writer's attitude as positive, negative, or neutral. |
`multi_label` |
`bool`
Required and only applicable for text classification task. If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each text snippet just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each text snippet multiple annotations may be applicable). |
`sentiment_max` |
`int`
Required and only applicable for sentiment task. A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive). |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.text_dataset.TextDataset,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Data filter splits:
Assigns input data to training, validation, and test sets
based on the given filters, data pieces not matched by any
filter are ignored. Currently only supported for Datasets
containing DataItems.
If any of the filters in this message are to match nothing, then
they can be set as '-' (the minus sign).
If using filter splits, all of `training_filter_split`, `validation_filter_split` and
`test_filter_split` must be provided.
Supported only for unstructured Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TextDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`training_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`validation_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`test_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`model_display_name` |
`str`
Optional. The display name of the managed Vertex AI Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient -->

# Class MigrationServiceClient (1.134.0)

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`MigrationServiceTransport` |
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

### MigrationServiceClient

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the migration service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MigrationServiceTransport,Callable[..., MigrationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MigrationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotated_dataset_path

`annotated_dataset_path(project: str, dataset: str, annotated_dataset: str) -> str`


Returns a fully-qualified annotated_dataset string.

### batch_migrate_resources

```
batch_migrate_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.BatchMigrateResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
migrate_resource_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.migration_service.MigrateResourceRequest
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


Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_migrate_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
migrate_resource_requests = aiplatform_v1.[MigrateResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.html)()
migrate_resource_requests.migrate_ml_engine_model_version_config.endpoint = "endpoint_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_version = "model_version_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_display_name = "model_display_name_value"
request = aiplatform_v1.[BatchMigrateResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesRequest.html)(
parent="parent_value",
migrate_resource_requests=migrate_resource_requests,
)
# Make the request
operation = client.[batch_migrate_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_batch_migrate_resources)(request=request)
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
The request object. Request message for MigrationService.BatchMigrateResources. |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: |
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. This corresponds to the |
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

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_annotated_dataset_path

`parse_annotated_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a annotated_dataset path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_version_path

`parse_version_path(path: str) -> typing.Dict[str, str]`


Parses a version path into its component segments.

### search_migratable_resources

```
search_migratable_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
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
google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesPager
)
```


Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Vertex AI's given location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_migratable_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchMigratableResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[search_migratable_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_search_migratable_resources)(request=request)
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
The request object. Request message for MigrationService.SearchMigratableResources. |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: |
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
Response message for MigrationService.SearchMigratableResources. Iterating over this object will yield results and resolve additional pages automatically. |

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

### version_path

`version_path(project: str, model: str, version: str) -> str`


Returns a fully-qualified version string.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient -->

# Class ReasoningEngineExecutionServiceAsyncClient (1.134.0)

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for executing queries on Reasoning Engine.

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
`ReasoningEngineExecutionServiceTransport` |
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

### ReasoningEngineExecutionServiceAsyncClient

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineExecutionServiceTransport,Callable[..., ReasoningEngineExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport
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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### query_reasoning_engine

```
query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineRequest,
dict,
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
) -> (
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineResponse
)
```


Queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[QueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_query_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.Query][]. |
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
Response message for [ReasoningEngineExecutionService.Query][] |

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### stream_query_reasoning_engine

```
stream_query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.StreamQueryReasoningEngineRequest,
dict,
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
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Streams queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stream_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamQueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
stream = await client.[stream_query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_stream_query_reasoning_engine)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.StreamQuery][]. |
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
`AsyncIterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetVersionRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs -->

# Class AutoMlTextExtractionInputs (1.134.0)

`AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.CorpusTypeConfig.DocumentCorpus -->

# Class DocumentCorpus (1.134.0)

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

## Methods

### DocumentCorpus

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.DeploymentResourcesType -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest -->

# Class FetchFeatureValuesRequest (1.134.0)

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Simple ID. The whole string will be used as is to identify Entity to fetch feature values for. This field is a member of `oneof` _ `entity_id` .
|
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`data_key` |
Optional. The request key to fetch feature values for. |
`data_format` |
Optional. Response data format. If not set, FeatureViewDataFormat.KEY_VALUE will be used. |
`format_` |
Specify response data format. If not set, KeyValue format will be used. Deprecated. Use FetchFeatureValuesRequest.data_format. |

## Classes

### Format

`Format(value)`


Format of the response data.

## Methods

### FetchFeatureValuesRequest

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.OptimizedConfig -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentation -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service -->

# Package gen_ai_tuning_service (1.134.0)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service`

package.

## Classes

[GenAiTuningServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceAsyncClient)

A service for creating and managing GenAI Tuning Jobs.

[GenAiTuningServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.GenAiTuningServiceClient)

A service for creating and managing GenAI Tuning Jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_tuning_service.pagers)

API documentation for `aiplatform_v1.services.gen_ai_tuning_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.persistent_resource_service.pagers`

module.

## Classes

[ListPersistentResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager)

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPersistentResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesPager)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient -->

# Class EndpointServiceAsyncClient (1.135.0)

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's Endpoints.

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
`EndpointServiceTransport` |
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

### EndpointServiceAsyncClient

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the endpoint service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,EndpointServiceTransport,Callable[..., EndpointServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the EndpointServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_endpoint

```
create_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
endpoint_id: typing.Optional[str] = None,
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


Creates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_create_endpoint)(request=request)
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
The request object. Request message for EndpointService.CreateEndpoint. |
`parent` |
Required. The resource name of the Location to create the Endpoint in. Format: |
`endpoint` |
Required. The Endpoint to create. This corresponds to the |
`endpoint_id` |
Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are |
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

### delete_endpoint

```
delete_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeleteEndpointRequest,
dict,
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


Deletes an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_delete_endpoint)(request=request)
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
The request object. Request message for EndpointService.DeleteEndpoint. |
`name` |
Required. The name of the Endpoint resource to be deleted. Format: |
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

### deploy_model

```
deploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.DeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Deploys a Model into this Endpoint, creating a DeployedModel within it.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_deploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_deploy_model)(request=request)
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
The request object. Request message for EndpointService.DeployModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to deploy a Model. Format: |
`deployed_model` |
Required. The DeployedModel to be created within the Endpoint. Note that Endpoint.traffic_split must be updated for the DeployedModel to start receiving traffic, either as part of this call, or via EndpointService.UpdateEndpoint. This corresponds to the |
`traffic_split` |
`:class:`
A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If this field is non-empty, then the Endpoint's traffic_split will be overwritten with it. To refer to the ID of the just being deployed Model, a "0" should be used, and the actual ID of the new DeployedModel will be filled in its place by this method. The traffic percentage values must add up to 100. If this field is empty, then the Endpoint's traffic_split is not updated. This corresponds to the |
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

### deployment_resource_pool_path

```
deployment_resource_pool_path(
project: str, location: str, deployment_resource_pool: str
) -> str
```


Returns a fully-qualified deployment_resource_pool string.

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### fetch_publisher_model_config

```
fetch_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.FetchPublisherModelConfigRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
```


Fetches the configs of publisher models.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_fetch_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
response = await client.[fetch_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_fetch_publisher_model_config)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.FetchPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
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
This message contains configs of a publisher model. |

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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
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
`EndpointServiceAsyncClient` |
The constructed client. |

### get_endpoint

```
get_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.GetEndpointRequest,
dict,
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
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Gets an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_get_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.GetEndpoint |
`name` |
Required. The name of the Endpoint resource. Format: |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

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
google.cloud.aiplatform_v1beta1.services.endpoint_service.transports.base.EndpointServiceTransport
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

### list_endpoints

```
list_endpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
dict,
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
) -> (
google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager
)
```


Lists Endpoints in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_endpoints():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_list_endpoints)(request=request)
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
The request object. Request message for EndpointService.ListEndpoints. |
`parent` |
Required. The resource name of the Location from which to list the Endpoints. Format: |
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
Response message for EndpointService.ListEndpoints. Iterating over this object will yield results and resolve additional pages automatically. |

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

### model_deployment_monitoring_job_path

```
model_deployment_monitoring_job_path(
project: str, location: str, model_deployment_monitoring_job: str
) -> str
```


Returns a fully-qualified model_deployment_monitoring_job string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### mutate_deployed_model

```
mutate_deployed_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.DeployedModel
] = None,
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


Updates an existing deployed model. Updatable fields include
`min_replica_count`

, `max_replica_count`

,
`required_replica_count`

, `autoscaling_metric_specs`

,
`disable_container_logging`

(v1 only), and
`enable_container_logging`

(v1beta1 only).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1beta1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1beta1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_mutate_deployed_model)(request=request)
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
The request object. Request message for EndpointService.MutateDeployedModel. |
`endpoint` |
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: |
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - |
`update_mask` |
Required. The update mask applies to the resource. See |
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

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

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

### parse_deployment_resource_pool_path

`parse_deployment_resource_pool_path(path: str) -> typing.Dict[str, str]`


Parses a deployment_resource_pool path into its component segments.

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_deployment_monitoring_job_path

`parse_model_deployment_monitoring_job_path(path: str) -> typing.Dict[str, str]`


Parses a model_deployment_monitoring_job path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

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

### set_publisher_model_config

```
set_publisher_model_config(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.SetPublisherModelConfigRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
publisher_model_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.PublisherModelConfig
] = None,
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


Sets (creates or updates) configs of publisher models. For example, sets the request/response logging config.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_set_publisher_model_config():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SetPublisherModelConfigRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigRequest.html)(
name="name_value",
)
# Make the request
operation = client.[set_publisher_model_config](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_set_publisher_model_config)(request=request)
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
The request object. Request message for EndpointService.SetPublisherModelConfig. |
`name` |
Required. The name of the publisher model, in the format of |
`publisher_model_config` |
Required. The publisher model config. This corresponds to the |
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

### undeploy_model

```
undeploy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UndeployModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model_id: typing.Optional[str] = None,
traffic_split: typing.Optional[typing.MutableMapping[str, int]] = None,
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


Undeploys a Model from an Endpoint, removing a DeployedModel from it, and freeing all resources it's using.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_undeploy_model():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_undeploy_model)(request=request)
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
The request object. Request message for EndpointService.UndeployModel. |
`endpoint` |
Required. The name of the Endpoint resource from which to undeploy a Model. Format: |
`deployed_model_id` |
Required. The ID of the DeployedModel to be undeployed from the Endpoint. This corresponds to the |
`traffic_split` |
`:class:`
If this field is provided, then the Endpoint's traffic_split will be overwritten with it. If last DeployedModel is being undeployed from the Endpoint, the [Endpoint.traffic_split] will always end up empty when this call returns. A DeployedModel will be successfully undeployed only if it doesn't have any traffic assigned to it when this method executes, or if this field unassigns any traffic to it. This corresponds to the |
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

### update_endpoint

```
update_endpoint(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
```


Updates an Endpoint.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = await client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for EndpointService.UpdateEndpoint. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. See |
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
Models are deployed into it, and afterwards Endpoint is called to obtain predictions and explanations. |

### update_endpoint_long_running

```
update_endpoint_long_running(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1beta1.types.endpoint.Endpoint
] = None,
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


Updates an Endpoint with a long running operation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1beta1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1beta1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint_long_running)(request=request)
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
The request object. Request message for EndpointService.UpdateEndpointLongRunning. |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob -->

# Class AutoMLTextTrainingJob (1.135.0)

```
AutoMLTextTrainingJob(
display_name: str,
prediction_type: str,
multi_label: bool = False,
sentiment_max: int = 10,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a AutoML Text Training Job.

## Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`prediction_type` |
`str`
The type of prediction the Model is to produce, one of: "classification" - A classification model analyzes text data and returns a list of categories that apply to the text found in the data. Vertex AI offers both single-label and multi-label text classification models. "extraction" - An entity extraction model inspects text data for known entities referenced in the data and labels those entities in the text. "sentiment" - A sentiment analysis model inspects text data and identifies the prevailing emotional opinion within it, especially to determine a writer's attitude as positive, negative, or neutral. |
`multi_label` |
`bool`
Required and only applicable for text classification task. If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each text snippet just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each text snippet multiple annotations may be applicable). |
`sentiment_max` |
`int`
Required and only applicable for sentiment task. A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive). |
`project` |
`str`
Optional. Project to run training in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run training in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call training service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize TrainingPipelines. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`training_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the training pipeline. Has the form: |
`model_encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Optional. The time when the training job entered the
`PIPELINE_STATE_SUCCEEDED`

, `PIPELINE_STATE_FAILED`

, or
`PIPELINE_STATE_CANCELLED`

state.

### error

Optional. Detailed error information for this training job resource.
Error information is created only when the state of the training job is
`PIPELINE_STATE_FAILED`

or `PIPELINE_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### has_failed

Returns `true`

if the training job failed, otherwise `false`

.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Optional. The time when the training job first entered the
`PIPELINE_STATE_RUNNING`

state.

### state

Current training state.

### update_time

Time this resource was last updated.

## Methods

### cancel

`cancel() -> None`


Asynchronously attempts to cancel a training job.

The server makes a best effort to cancel the job, but the training job
can't always be cancelled. If the training job is canceled, its state
transitions to `CANCELLED`

and it's not deleted.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If this training job isn't running, then a runtime error is raised. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.training_jobs._TrainingJob
```


Gets a training job using the `resource_name`

that's passed in.

Parameters |
|
|---|---|
Name |
Description |
`resource_name` |
`str`
Required. A fully-qualified resource name or ID. |
`project` |
`str`
Optional. The name of the Google Cloud project to retrieve the training job from. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job is retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload this model. These credentials override the credentials set by |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A `ValueError` is raised if the task definition of the retrieved training job doesn't match the custom training task definition. |

### get_model

`get_model(sync=True) -> google.cloud.aiplatform.models.Model`


Returns the Vertex AI model produced by this training job.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
If set to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
A runtime error is raised if the training job failed or if a model wasn't produced by the training job. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


Lists all instances of this training job resource.

The following shows an example of how to call `CustomTrainingJob.list`

:

```
aiplatform.CustomTrainingJob.list(
filter='display_name="experiment_a27"',
order_by='create_time desc'
)
```


Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names, snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields used to sort the returned traing job resources. The defauilt sorting order is ascending. To sort by a field name in descending order, use |
`project` |
`str`
Optional. The name of the Google Cloud project to which to retrieve the list of training job resources. This overrides the project that was set by |
`location` |
`str`
Optional. The Google Cloud region from where the training job resources are retrieved. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to retrieve list. These credentials override the credentials set by |

Returns |
|
|---|---|
Type |
Description |
`List[VertexAiResourceNoun]` |
A list of training job resources. |

### run

```
run(
dataset: google.cloud.aiplatform.datasets.text_dataset.TextDataset,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
training_filter_split: typing.Optional[str] = None,
validation_filter_split: typing.Optional[str] = None,
test_filter_split: typing.Optional[str] = None,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Runs the training job and returns a model.

If training on a Vertex AI dataset, you can use one of the following split configurations:
Data fraction splits:
Any of `training_fraction_split`

, `validation_fraction_split`

and
`test_fraction_split`

may optionally be provided, they must sum to up to 1. If
the provided ones sum to less than 1, the remainder is assigned to sets as
decided by Vertex AI. If none of the fractions are set, by default roughly 80%
of data will be used for training, 10% for validation, and 10% for test.

```
Data filter splits:
Assigns input data to training, validation, and test sets
based on the given filters, data pieces not matched by any
filter are ignored. Currently only supported for Datasets
containing DataItems.
If any of the filters in this message are to match nothing, then
they can be set as '-' (the minus sign).
If using filter splits, all of `training_filter_split`, `validation_filter_split` and
`test_filter_split` must be provided.
Supported only for unstructured Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TextDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`training_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to train the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`validation_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to validate the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`test_filter_split` |
`str`
Optional. A filter on DataItems of the Dataset. DataItems that match this filter are used to test the Model. A filter with same syntax as the one used in DatasetService.ListDataItems may be used. If a single DataItem is matched by more than one of the FilterSplit filters, then it is assigned to the first set that applies to it in the training, validation, test order. This is ignored if Dataset is not provided. |
`model_display_name` |
`str`
Optional. The display name of the managed Vertex AI Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
`model_labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`model_id` |
`str`
Optional. The ID to use for the Model produced by this job, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model. The new model uploaded by this job will be a version of |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of the model produced by this job without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the model version produced by this job will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`model_version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that the model version uploaded by this job can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`model_version_description` |
`str`
Optional. The description of the model version being uploaded by this job. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If Training job has already been run or is waiting to run. |

Returns |
|
|---|---|
Type |
Description |
`model` |
The trained Vertex AI Model resource. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until the resource has been created.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardTimeSeries.Metadata -->

# Class Metadata (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BigQueryDestination -->

# Class BigQueryDestination (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.WorkerPoolSpec -->

# Class WorkerPoolSpec (1.135.0)

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

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
`container_spec` |
The custom container task. This field is a member of `oneof` _ `task` .
|
`python_package_spec` |
The Python packaged task. This field is a member of `oneof` _ `task` .
|
`machine_spec` |
Optional. Immutable. The specification of a single machine. |
`replica_count` |
`int`
Optional. The number of worker replicas to use for this worker pool. |
`nfs_mounts` |
`MutableSequence[`
Optional. List of NFS mount spec. |
`lustre_mounts` |
`MutableSequence[`
Optional. List of Lustre mounts. |
`disk_spec` |
Disk spec. |

## Methods

### WorkerPoolSpec

`WorkerPoolSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a worker pool in a job.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionOperation -->

# Class ExtensionOperation (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigratableResource.MlEngineModelVersion -->

# Class MlEngineModelVersion (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service -->

# Package vertex_rag_data_service (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.MigrateAutomlDatasetConfig -->

# Class MigrateAutomlDatasetConfig (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsResponse -->

# Class PurgeContextsResponse (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExecutionInputsAndOutputsRequest -->

# Class QueryExecutionInputsAndOutputsRequest (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesRequest -->

# Class FetchFeatureValuesRequest (1.135.0)

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Simple ID. The whole string will be used as is to identify Entity to fetch feature values for. This field is a member of `oneof` _ `entity_id` .
|
`feature_view` |
`str`
Required. FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|
`data_key` |
Optional. The request key to fetch feature values for. |
`data_format` |
Optional. Response data format. If not set, FeatureViewDataFormat.KEY_VALUE will be used. |
`format_` |
Specify response data format. If not set, KeyValue format will be used. Deprecated. Use FetchFeatureValuesRequest.data_format. |

## Classes

### Format

`Format(value)`


Format of the response data.

## Methods

### FetchFeatureValuesRequest

`FetchFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreService.FetchFeatureValues. All the features under the requested feature view will be returned.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsRequest -->

# Class ListNasTrialDetailsRequest (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateDatasetVersionRequest -->

# Class CreateDatasetVersionRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service -->

# Package dataset_service (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.OptimizedConfig -->

# Class OptimizedConfig (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient -->

# Class MigrationServiceClient (1.135.0)

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`MigrationServiceTransport` |
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

### MigrationServiceClient

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the migration service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MigrationServiceTransport,Callable[..., MigrationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MigrationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotated_dataset_path

`annotated_dataset_path(project: str, dataset: str, annotated_dataset: str) -> str`


Returns a fully-qualified annotated_dataset string.

### batch_migrate_resources

```
batch_migrate_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.BatchMigrateResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
migrate_resource_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.migration_service.MigrateResourceRequest
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


Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_migrate_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
migrate_resource_requests = aiplatform_v1.[MigrateResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.html)()
migrate_resource_requests.migrate_ml_engine_model_version_config.endpoint = "endpoint_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_version = "model_version_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_display_name = "model_display_name_value"
request = aiplatform_v1.[BatchMigrateResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchMigrateResourcesRequest.html)(
parent="parent_value",
migrate_resource_requests=migrate_resource_requests,
)
# Make the request
operation = client.[batch_migrate_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_batch_migrate_resources)(request=request)
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
The request object. Request message for MigrationService.BatchMigrateResources. |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: |
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. This corresponds to the |
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

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_annotated_dataset_path

`parse_annotated_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a annotated_dataset path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_version_path

`parse_version_path(path: str) -> typing.Dict[str, str]`


Parses a version path into its component segments.

### search_migratable_resources

```
search_migratable_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
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
google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesPager
)
```


Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Vertex AI's given location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_migratable_resources():
# Create a client
client = aiplatform_v1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchMigratableResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[search_migratable_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1_services_migration_service_MigrationServiceClient_search_migratable_resources)(request=request)
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
The request object. Request message for MigrationService.SearchMigratableResources. |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: |
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
Response message for MigrationService.SearchMigratableResources. Iterating over this object will yield results and resolve additional pages automatically. |

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

### version_path

`version_path(project: str, model: str, version: str) -> str`


Returns a fully-qualified version string.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient -->

# Class ReasoningEngineExecutionServiceAsyncClient (1.135.0)

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for executing queries on Reasoning Engine.

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
`ReasoningEngineExecutionServiceTransport` |
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

### ReasoningEngineExecutionServiceAsyncClient

```
ReasoningEngineExecutionServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the reasoning engine execution service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ReasoningEngineExecutionServiceTransport,Callable[..., ReasoningEngineExecutionServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ReasoningEngineExecutionServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
`ReasoningEngineExecutionServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.transports.base.ReasoningEngineExecutionServiceTransport
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

### parse_reasoning_engine_path

`parse_reasoning_engine_path(path: str) -> typing.Dict[str, str]`


Parses a reasoning_engine path into its component segments.

### query_reasoning_engine

```
query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineRequest,
dict,
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
) -> (
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.QueryReasoningEngineResponse
)
```


Queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[QueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
response = await client.[query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_query_reasoning_engine)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.Query][]. |
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
Response message for [ReasoningEngineExecutionService.Query][] |

### reasoning_engine_path

`reasoning_engine_path(project: str, location: str, reasoning_engine: str) -> str`


Returns a fully-qualified reasoning_engine string.

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

### stream_query_reasoning_engine

```
stream_query_reasoning_engine(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_execution_service.StreamQueryReasoningEngineRequest,
dict,
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
) -> typing.Awaitable[typing.AsyncIterable[google.api.httpbody_pb2.HttpBody]]
```


Streams queries using a reasoning engine.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_stream_query_reasoning_engine():
# Create a client
client = aiplatform_v1beta1.
```[ReasoningEngineExecutionServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[StreamQueryReasoningEngineRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamQueryReasoningEngineRequest.html)(
name="name_value",
)
# Make the request
stream = await client.[stream_query_reasoning_engine](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_reasoning_engine_execution_service_ReasoningEngineExecutionServiceAsyncClient_stream_query_reasoning_engine)(request=request)
# Handle the response
async for response in stream:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [ReasoningEngineExecutionService.StreamQuery][]. |
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
`AsyncIterable[google.api.httpbody_pb2.HttpBody]` |
Message that represents an arbitrary HTTP body. It should only be used for payload formats that can't be represented as JSON, such as raw binary or an HTML page. This message can be used both in streaming and non-streaming API methods in the request as well as the response. It can be used as a top-level request field, which is convenient if one wants to extract parameters from either the URL or HTTP template into the request fields and also want access to the raw HTTP body. Example: message GetResourceRequest { // A unique request id. string request_id = 1; // The raw HTTP body is bound to this field. google.api.HttpBody http_body = 2; } service ResourceService { rpc GetResource(GetResourceRequest) returns (google.api.HttpBody); rpc UpdateResource(google.api.HttpBody) returns (google.protobuf.Empty); } Example with streaming methods: service CaldavService { rpc GetCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); rpc UpdateCalendar(stream google.api.HttpBody) returns (stream google.api.HttpBody); } Use of this type only changes how the request and response bodies are handled, all other features will continue to work unchanged. |

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/ -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest -->

# Class DeleteFeaturestoreRequest (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs -->

# Class AutoMlTextExtractionInputs (1.135.0)

`AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs`

class.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagCorpus.CorpusTypeConfig.DocumentCorpus -->

# Class DocumentCorpus (1.135.0)

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

## Methods

### DocumentCorpus

`DocumentCorpus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the document corpus.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.DeploymentResourcesType -->

# Class DeploymentResourcesType (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse -->

# Class ListNotebookRuntimeTemplatesResponse (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetVersionRequest -->

# Class UpdateDatasetVersionRequest (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardTimeSeries.Metadata -->

# Class Metadata (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BigQueryDestination -->

# Class BigQueryDestination (1.135.0)

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentation -->

# Class AutoMlImageSegmentation (1.135.0)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers -->

# Module pagers (1.135.0)

API documentation for `aiplatform_v1.services.persistent_resource_service.pagers`

module.

## Classes

[ListPersistentResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesAsyncPager)

```
ListPersistentResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPersistentResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesPager)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Index -->

# Class Index (1.135.0)

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Index. |
`display_name` |
`str`
Required. The display name of the Index. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Index. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Index, that is specific to it. Unset if the Index does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
An additional information about the Index; the schema of the metadata can be found in metadata_schema. |
`deployed_indexes` |
`MutableSequence[`
Output only. The pointers to DeployedIndexes created from this Index. An Index can be only deleted if all its DeployedIndexes had been undeployed first. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Indexes. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Index was most recently updated. This also includes any update to the contents of the Index. Note that Operations working on this Index may have their [Operations.metadata.generic_metadata.update_time] [google.cloud.aiplatform.v1.GenericOperationMetadata.update_time] a little after the value of this timestamp, yet that does not mean their results are not already reflected in the Index. Result of any successfully completed Operation on the Index is reflected in it. |
`index_stats` |
Output only. Stats of the index resource. |
`index_update_method` |
Immutable. The update method to use with this Index. If not set, BATCH_UPDATE will be used by default. |
`encryption_spec` |
Immutable. Customer-managed encryption key spec for an Index. If set, this Index and all sub-resources of this Index will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### IndexUpdateMethod

`IndexUpdateMethod(value)`


The update method of an Index.

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

### Index

`Index(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A representation of a collection of database items organized in a way that allows for approximate nearest neighbor (a.k.a ANN) algorithms search.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/prediction -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/[a-z0-9-]{0,61}[a-z0-9] -->

# Vertex AI SDK for Python

## Gemini API and Generative AI on Vertex AI

**NOTE**: For Gemini API and Generative AI on Vertex AI, please reference [Vertex Generative AI SDK for Python](https://cloud.google.com/vertex-ai/generative-ai/docs/reference/python/latest)

[Vertex AI](https://cloud.google.com/vertex-ai/docs): Google Vertex AI is an integrated suite of machine learning tools and services for building and using ML models with AutoML or custom code. It offers both novices and experts the best workbench for the entire machine learning development lifecycle.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-aiplatform
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-aiplatform
```


#### Supported Python Versions

Python >= 3.8

#### Deprecated Python Versions

Python <= 3.7.

The last version of this library compatible with Python 3.6 is google-cloud-aiplatform==1.12.1.

### Overview

This section provides a brief overview of the Vertex AI SDK for Python. You can also reference the notebooks in [vertex-ai-samples](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/notebooks/community/sdk) for examples.

All publicly available SDK features can be found in the `google/cloud/aiplatform`

directory.
Under the hood, Vertex SDK builds on top of GAPIC, which stands for Google API CodeGen.
The GAPIC library code sits in `google/cloud/aiplatform_v1`

and `google/cloud/aiplatform_v1beta1`

,
and it is auto-generated from Google’s service proto files.

For most developers’ programmatic needs, they can follow these steps to figure out which libraries to import:

Look through

`google/cloud/aiplatform`

first – Vertex SDK’s APIs will almost always be easier to use and more concise comparing with GAPICIf the feature that you are looking for cannot be found there, look through

`aiplatform_v1`

to see if it’s available in GAPICIf it is still in beta phase, it will be available in

`aiplatform_v1beta1`


If none of the above scenarios could help you find the right tools for your task, please feel free to open a github issue and send us a feature request.

#### Importing

Vertex AI SDK resource based functionality can be used by importing the following namespace:

```
from google.cloud import aiplatform
```


#### Initialization

Initialize the SDK to store common configurations that you use with the SDK.

```
aiplatform.init(
# your Google Cloud Project ID or number
# environment default used is not set
project='my-project',
# the Vertex AI region you will use
# defaults to us-central1
location='us-central1',
# Google Cloud Storage bucket in same region as location
# used to stage artifacts
staging_bucket='gs://my_staging_bucket',
# custom google.auth.credentials.Credentials
# environment default credentials used if not set
credentials=my_credentials,
# customer managed encryption key resource name
# will be applied to all Vertex AI resources if set
encryption_spec_key_name=my_encryption_key_name,
# the name of the experiment to use to track
# logged metrics and parameters
experiment='my-experiment',
# description of the experiment above
experiment_description='my experiment description'
)
```


#### Datasets

Vertex AI provides managed tabular, text, image, and video datasets. In the SDK, datasets can be used downstream to train models.

To create a tabular dataset:

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


You can also create and import a dataset in separate steps:

```
from google.cloud import aiplatform
my_dataset = aiplatform.TextDataset.create(
display_name="my-dataset")
my_dataset.import_data(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
)
```


To get a previously created Dataset:

```
dataset = aiplatform.ImageDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
```


Vertex AI supports a variety of dataset schemas. References to these schemas are available under the
`aiplatform.schema.dataset`

namespace. For more information on the supported dataset schemas please refer to the
[Preparing data docs](https://cloud.google.com/ai-platform-unified/docs/datasets/prepare).

#### Training

The Vertex AI SDK for Python allows you train Custom and AutoML Models.

You can train custom models using a custom Python script, custom Python package, or container.

**Preparing Your Custom Code**

Vertex AI custom training enables you to train on Vertex AI datasets and produce Vertex AI models. To do so your script must adhere to the following contract:

It must read datasets from the environment variables populated by the training service:

```
os.environ['AIP_DATA_FORMAT'] # provides format of data
os.environ['AIP_TRAINING_DATA_URI'] # uri to training split
os.environ['AIP_VALIDATION_DATA_URI'] # uri to validation split
os.environ['AIP_TEST_DATA_URI'] # uri to test split
```


Please visit [Using a managed dataset in a custom training application](https://cloud.google.com/vertex-ai/docs/training/using-managed-datasets) for a detailed overview.

It must write the model artifact to the environment variable populated by the training service:

```
os.environ['AIP_MODEL_DIR']
```


**Running Training**

```
job = aiplatform.CustomTrainingJob(
display_name="my-training-job",
script_path="training_script.py",
container_uri="us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
model_serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
model = job.run(my_dataset,
replica_count=1,
machine_type="n1-standard-4",
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


In the code block above my_dataset is managed dataset created in the Dataset section above. The model variable is a managed Vertex AI model that can be deployed or exported.

## AutoMLs

The Vertex AI SDK for Python supports AutoML tabular, image, text, video, and forecasting.

To train an AutoML tabular model:

```
dataset = aiplatform.TabularDataset('projects/my-project/location/us-central1/datasets/{DATASET_ID}')
job = aiplatform.AutoMLTabularTrainingJob(
display_name="train-automl",
optimization_prediction_type="regression",
optimization_objective="minimize-rmse",
)
model = job.run(
dataset=dataset,
target_column="target_column_name",
training_fraction_split=0.6,
validation_fraction_split=0.2,
test_fraction_split=0.2,
budget_milli_node_hours=1000,
model_display_name="my-automl-model",
disable_early_stopping=False,
)
```


## Models

To get a model:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
```


To upload a model:

```
model = aiplatform.Model.upload(
display_name='my-model',
artifact_uri="gs://python/to/my/model/dir",
serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/tf2-cpu.2-2:latest",
)
```


To deploy a model:

```
endpoint = model.deploy(machine_type="n1-standard-4",
min_replica_count=1,
max_replica_count=5
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


Please visit [Importing models to Vertex AI](https://cloud.google.com/vertex-ai/docs/general/import-model) for a detailed overview:

## Model Evaluation

The Vertex AI SDK for Python currently supports getting model evaluation metrics for all AutoML models.

To list all model evaluations for a model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
evaluations = model.list_model_evaluations()
```


To get the model evaluation resource for a given model:

```
model = aiplatform.Model('projects/my-project/locations/us-central1/models/{MODEL_ID}')
# returns the first evaluation with no arguments, you can also pass the evaluation ID
evaluation = model.get_model_evaluation()
eval_metrics = evaluation.metrics
```


You can also create a reference to your model evaluation directly by passing in the resource name of the model evaluation:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name='projects/my-project/locations/us-central1/models/{MODEL_ID}/evaluations/{EVALUATION_ID}')
```


Alternatively, you can create a reference to your evaluation by passing in the model and evaluation IDs:

```
evaluation = aiplatform.ModelEvaluation(
evaluation_name={EVALUATION_ID},
model_id={MODEL_ID})
```


## Batch Prediction

To create a batch prediction job:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
batch_prediction_job = model.batch_predict(
job_display_name='my-batch-prediction-job',
instances_format='csv',
machine_type='n1-standard-4',
gcs_source=['gs://path/to/my/file.csv'],
gcs_destination_prefix='gs://path/to/my/batch_prediction/results/',
service_account='my-sa@my-project.iam.gserviceaccount.com'
)
```


You can also create a batch prediction job asynchronously by including the sync=False argument:

```
batch_prediction_job = model.batch_predict(..., sync=False)
# wait for resource to be created
batch_prediction_job.wait_for_resource_creation()
# get the state
batch_prediction_job.state
# block until job is complete
batch_prediction_job.wait()
```


## Endpoints

To create an endpoint:

```
endpoint = aiplatform.Endpoint.create(display_name='my-endpoint')
```


To deploy a model to a created endpoint:

```
model = aiplatform.Model('/projects/my-project/locations/us-central1/models/{MODEL_ID}')
endpoint.deploy(model,
min_replica_count=1,
max_replica_count=5,
machine_type='n1-standard-4',
accelerator_type='NVIDIA_TESLA_K80',
accelerator_count=1)
```


To get predictions from endpoints:

```
endpoint.predict(instances=[[6.7, 3.1, 4.7, 1.5], [4.6, 3.1, 1.5, 0.2]])
```


To undeploy models from an endpoint:

```
endpoint.undeploy_all()
```


To delete an endpoint:

```
endpoint.delete()
```


## Pipelines

To create a Vertex AI Pipeline run and monitor until completion:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Execute pipeline in Vertex AI and monitor until completion
pl.run(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
# Whether this function call should be synchronous (wait for pipeline run to finish before terminating)
# or asynchronous (return immediately)
sync=True
)
```


To create a Vertex AI Pipeline without monitoring until completion, use submit instead of run:

```
# Instantiate PipelineJob object
pl = PipelineJob(
display_name="My first pipeline",
# Whether or not to enable caching
# True = always cache pipeline step result
# False = never cache pipeline step result
# None = defer to cache option for each pipeline component in the pipeline definition
enable_caching=False,
# Local or GCS path to a compiled pipeline definition
template_path="pipeline.json",
# Dictionary containing input parameters for your pipeline
parameter_values=parameter_values,
# GCS path to act as the pipeline root
pipeline_root=pipeline_root,
)
# Submit the Pipeline to Vertex AI
pl.submit(
# Email address of service account to use for the pipeline run
# You must have iam.serviceAccounts.actAs permission on the service account to use it
service_account=service_account,
)
```


## Explainable AI: Get Metadata

To get metadata in dictionary format from TensorFlow 1 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v1 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder(
'gs://python/to/my/model/dir', tags=[tf.saved_model.tag_constants.SERVING]
)
generated_md = builder.get_metadata()
```


To get metadata in dictionary format from TensorFlow 2 models:

```
from google.cloud.aiplatform.explain.metadata.tf.v2 import saved_model_metadata_builder
builder = saved_model_metadata_builder.SavedModelMetadataBuilder('gs://python/to/my/model/dir')
generated_md = builder.get_metadata()
```


To use Explanation Metadata in endpoint deployment and model upload:

```
explanation_metadata = builder.get_metadata_protobuf()
# To deploy a model to an endpoint with explanation
model.deploy(..., explanation_metadata=explanation_metadata)
# To deploy a model to a created endpoint with explanation
endpoint.deploy(..., explanation_metadata=explanation_metadata)
# To upload a model with explanation
aiplatform.Model.upload(..., explanation_metadata=explanation_metadata)
```


## Cloud Profiler

Cloud Profiler allows you to profile your remote Vertex AI Training jobs on demand and visualize the results in Vertex AI Tensorboard.

To start using the profiler with TensorFlow, update your training script to include the following:

```
from google.cloud.aiplatform.training_utils import cloud_profiler
...
cloud_profiler.init()
```


Next, run the job with with a Vertex AI TensorBoard instance. For full details on how to do this, visit [https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview](https://cloud.google.com/vertex-ai/docs/experiments/tensorboard-overview)

Finally, visit your TensorBoard in your Google Cloud Console, navigate to the “Profile” tab, and click the Capture Profile button. This will allow users to capture profiling statistics for the running jobs.

### Next Steps

Read the

[Client Library Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest)for Vertex AI API to see other available methods on the client.Read the

[Vertex AI API Product documentation](https://cloud.google.com/vertex-ai/docs)to learn more about the product and see How-to Guides.View this

[README](https://github.com/googleapis/google-cloud-python/blob/main/README.rst)to see the full list of Cloud APIs that we cover.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient -->

# Class MigrationServiceClient (1.135.0)

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

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
`MigrationServiceTransport` |
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

### MigrationServiceClient

```
MigrationServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.migration_service.transports.base.MigrationServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the migration service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MigrationServiceTransport,Callable[..., MigrationServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MigrationServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### annotated_dataset_path

`annotated_dataset_path(project: str, dataset: str, annotated_dataset: str) -> str`


Returns a fully-qualified annotated_dataset string.

### batch_migrate_resources

```
batch_migrate_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.migration_service.BatchMigrateResourcesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
migrate_resource_requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.migration_service.MigrateResourceRequest
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


Batch migrates resources from ml.googleapis.com, automl.googleapis.com, and datalabeling.googleapis.com to Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_batch_migrate_resources():
# Create a client
client = aiplatform_v1beta1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
migrate_resource_requests = aiplatform_v1beta1.[MigrateResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MigrateResourceRequest.html)()
migrate_resource_requests.migrate_ml_engine_model_version_config.endpoint = "endpoint_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_version = "model_version_value"
migrate_resource_requests.migrate_ml_engine_model_version_config.model_display_name = "model_display_name_value"
request = aiplatform_v1beta1.[BatchMigrateResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchMigrateResourcesRequest.html)(
parent="parent_value",
migrate_resource_requests=migrate_resource_requests,
)
# Make the request
operation = client.[batch_migrate_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1beta1_services_migration_service_MigrationServiceClient_batch_migrate_resources)(request=request)
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
The request object. Request message for MigrationService.BatchMigrateResources. |
`parent` |
`str`
Required. The location of the migrated resource will live in. Format: |
`migrate_resource_requests` |
`MutableSequence[`
Required. The request messages specifying the resources to migrate. They must be in the same location as the destination. Up to 50 resources can be migrated in one batch. This corresponds to the |
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

### dataset_path

`dataset_path(project: str, location: str, dataset: str) -> str`


Returns a fully-qualified dataset string.

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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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
`MigrationServiceClient` |
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

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

### parse_annotated_dataset_path

`parse_annotated_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a annotated_dataset path into its component segments.

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

### parse_dataset_path

`parse_dataset_path(path: str) -> typing.Dict[str, str]`


Parses a dataset path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_version_path

`parse_version_path(path: str) -> typing.Dict[str, str]`


Parses a version path into its component segments.

### search_migratable_resources

```
search_migratable_resources(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
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
google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager
)
```


Searches all of the resources in automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com that can be migrated to Vertex AI's given location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_search_migratable_resources():
# Create a client
client = aiplatform_v1beta1.
```[MigrationServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchMigratableResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[search_migratable_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient.html#google_cloud_aiplatform_v1beta1_services_migration_service_MigrationServiceClient_search_migratable_resources)(request=request)
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
The request object. Request message for MigrationService.SearchMigratableResources. |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: |
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
Response message for MigrationService.SearchMigratableResources. Iterating over this object will yield results and resolve additional pages automatically. |

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

### version_path

`version_path(project: str, model: str, version: str) -> str`


Returns a fully-qualified version string.

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
