---
merged_at: 2026-01-25T21:47:44.364582
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesfeatureonlinestore_googlecloudaiplatform_v1typ_94c9ab.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeatureonlinestore_googlecloudaiplatform_v1type_7cdb57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeatureonlinestore_googlecloudaiplatform_v1types_b283d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeatureonlinestore_googlecloudaiplatform_v1typese_86e61d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureonlinestore_googlecloudaiplatform_v1typesev_7364c8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureonlinestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore -->

# Class FeatureOnlineStore (1.134.0)

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

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
`bigtable` |
Contains settings for the Cloud Bigtable instance that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. This field is a member of `oneof` _ `storage_type` .
|
`optimized` |
Contains settings for the Optimized store that will be created to serve featureValues for all FeatureViews under this FeatureOnlineStore. When choose Optimized storage type, need to set PrivateServiceConnectConfig.enable_private_service_connect to use private endpoint. Otherwise will use public endpoint by default. This field is a member of `oneof` _ `storage_type` .
|
`name` |
`str`
Identifier. Name of the FeatureOnlineStore. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureOnlineStore was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureOnlineStore. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`state` |
Output only. State of the featureOnlineStore. |
`dedicated_serving_endpoint` |
Optional. The dedicated serving endpoint for this FeatureOnlineStore, which is different from common Vertex service endpoint. |
`encryption_spec` |
Optional. Customer-managed encryption key spec for data storage. If set, online store will be secured by this key. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### Bigtable

`Bigtable(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### DedicatedServingEndpoint

`DedicatedServingEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The dedicated serving endpoint for this FeatureOnlineStore. Only need to set when you choose Optimized storage type. Public endpoint is provisioned by default.

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

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

### State

`State(value)`


Possible states a featureOnlineStore can have.

## Methods

### FeatureOnlineStore

`FeatureOnlineStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevaluateinstancesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluateInstancesResponse -->

# Class EvaluateInstancesResponse (1.134.0)

`EvaluateInstancesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EvaluationService.EvaluateInstances.

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
`exact_match_results` |
Auto metric evaluation results. Results for exact match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`bleu_results` |
Results for bleu metric. This field is a member of `oneof` _ `evaluation_results` .
|
`rouge_results` |
Results for rouge metric. This field is a member of `oneof` _ `evaluation_results` .
|
`fluency_result` |
LLM-based metric evaluation result. General text generation metrics, applicable to other categories. Result for fluency metric. This field is a member of `oneof` _ `evaluation_results` .
|
`coherence_result` |
Result for coherence metric. This field is a member of `oneof` _ `evaluation_results` .
|
`safety_result` |
Result for safety metric. This field is a member of `oneof` _ `evaluation_results` .
|
`groundedness_result` |
Result for groundedness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`fulfillment_result` |
Result for fulfillment metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_quality_result` |
Summarization only metrics. Result for summarization quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_summarization_quality_result` |
Result for pairwise summarization quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_helpfulness_result` |
Result for summarization helpfulness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`summarization_verbosity_result` |
Result for summarization verbosity metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_quality_result` |
Question answering only metrics. Result for question answering quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_question_answering_quality_result` |
Result for pairwise question answering quality metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_relevance_result` |
Result for question answering relevance metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_helpfulness_result` |
Result for question answering helpfulness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`question_answering_correctness_result` |
Result for question answering correctness metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pointwise_metric_result` |
Generic metrics. Result for pointwise metric. This field is a member of `oneof` _ `evaluation_results` .
|
`pairwise_metric_result` |
Result for pairwise metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_call_valid_results` |
Tool call metrics. Results for tool call valid metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_name_match_results` |
Results for tool name match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_parameter_key_match_results` |
Results for tool parameter key match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`tool_parameter_kv_match_results` |
Results for tool parameter key value match metric. This field is a member of `oneof` _ `evaluation_results` .
|
`comet_result` |
Translation metrics. Result for Comet metric. This field is a member of `oneof` _ `evaluation_results` .
|
`metricx_result` |
Result for Metricx metric. This field is a member of `oneof` _ `evaluation_results` .
|

## Methods

### EvaluateInstancesResponse

`EvaluateInstancesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EvaluationService.EvaluateInstances.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesvertexragstore__googlecloudaiplatformv1schem_a1f2a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesvertexragstore__googlecloudaiplatformv1schema_5da6a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesvertexragstore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.VertexRagStore -->

# Class VertexRagStore (1.134.0)

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex RAG Store for grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpora` |
`MutableSequence[str]`
Optional. Deprecated. Please use rag_resources instead. |
`rag_resources` |
`MutableSequence[`
Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support. |
`similarity_top_k` |
`int`
Optional. Number of top k results to return from the selected corpora. This field is a member of `oneof` _ `_similarity_top_k` .
|
`vector_distance_threshold` |
`float`
Optional. Only return results with vector distance smaller than the threshold. This field is a member of `oneof` _ `_vector_distance_threshold` .
|
`rag_retrieval_config` |
Optional. The retrieval config for the Rag query. |
`store_context` |
`bool`
Optional. Currently only supported for Gemini Multimodal Live API. In Gemini Multimodal Live API, if `store_context` bool is
true, Gemini will leverage it to automatically memorize the
interactions between the client and Gemini, and retrieve
context when needed to augment the response generation for
users' ongoing and future interactions.
|

## Classes

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Methods

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Retrieve from Vertex RAG Store for grounding.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoclassifica_87f61d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoclassification.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassification -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardblobsequence.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlobSequence -->

# Class TensorboardBlobSequence (1.134.0)

`TensorboardBlobSequence(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a blob metric plot, but mostly just a wrapper
message to work around repeated fields can't be used directly within
`oneof`

fields.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.TensorboardBlob]`
List of blobs contained within the sequence. |

## Methods

### TensorboardBlobSequence

`TensorboardBlobSequence(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One point viewable on a blob metric plot, but mostly just a wrapper
message to work around repeated fields can't be used directly within
`oneof`

fields.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmetadata_service_googlecloudaiplatform_v1_c18db3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmetadata_service_googlecloudaiplatform_v1b_0ea451.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service -->

# Package metadata_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.metadata_service`

package.

## Classes

[MetadataServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.MetadataServiceAsyncClient)

Service for reading and writing metadata entries.

[MetadataServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.MetadataServiceClient)

Service for reading and writing metadata entries.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers)

API documentation for `aiplatform_v1beta1.services.metadata_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadindexdatapointsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest -->

# Class ReadIndexDatapointsRequest (1.134.0)

`ReadIndexDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.ReadIndexDatapoints.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the index endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index_id` |
`str`
The ID of the DeployedIndex that will serve the request. |
`ids` |
`MutableSequence[str]`
IDs of the datapoints to be searched for. |

## Methods

### ReadIndexDatapointsRequest

`ReadIndexDatapointsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The request message for MatchService.ReadIndexDatapoints.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesscheduleconfig_googlecloudaiplatform_v1typesi_9d3c03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesscheduleconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ScheduleConfig -->

# Class ScheduleConfig (1.134.0)

`ScheduleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schedule configuration for the FeatureMonitor.

## Attribute |
|
|---|---|
Name |
Description |
`cron` |
`str`
Cron schedule (https://en.wikipedia.org/wiki/Cron) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*". |

## Methods

### ScheduleConfig

`ScheduleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schedule configuration for the FeatureMonitor.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexdatapointrestriction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint.Restriction -->

# Class Restriction (1.134.0)

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).

## Attributes |
|
|---|---|
Name |
Description |
`namespace` |
`str`
The namespace of this restriction. e.g.: color. |
`allow_list` |
`MutableSequence[str]`
The attributes to allow in this namespace. e.g.: 'red' |
`deny_list` |
`MutableSequence[str]`
The attributes to deny in this namespace. e.g.: 'blue' |

## Methods

### Restriction

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesencryptionspec_googlecloudaiplatform_v1typ_b6d250.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesencryptionspec_googlecloudaiplatform_v1type_0d97a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesencryptionspec_googlecloudaiplatform_v1types_8a8530.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesencryptionspec_googlecloudaiplatform_v1typesc_c59103.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesencryptionspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EncryptionSpec -->

# Class EncryptionSpec (1.134.0)

`EncryptionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a customer-managed encryption key spec that can be applied to a top-level resource.

## Attribute |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
Required. The Cloud KMS resource identifier of the customer managed encryption key used to protect a resource. Has the form: `projects/my-project/locations/my-region/keyRings/my-kr/cryptoKeys/my-key` .
The key needs to be in the same region as where the compute
resource is created.
|

## Methods

### EncryptionSpec

`EncryptionSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a customer-managed encryption key spec that can be applied to a top-level resource.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescodeexecutionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CodeExecutionResult -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesresumemodeldeploymentmonitoringjobrequest_goo_8c742b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesresumemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeModelDeploymentMonitoringJobRequest -->

# Class ResumeModelDeploymentMonitoringJobRequest (1.134.0)

```
ResumeModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ResumeModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to resume. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### ResumeModelDeploymentMonitoringJobRequest

```
ResumeModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ResumeModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessegment.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Segment -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesembedcontentresponse_googlecloudaiplatform_v_c88e9c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesembedcontentresponse_googlecloudaiplatform_v1_d0dfe0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesembedcontentresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EmbedContentResponse -->

# Class EmbedContentResponse (1.134.0)

`EmbedContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.EmbedContent.

## Attributes |
|
|---|---|
Name |
Description |
`embedding` |
The embedding generated from the input content. |
`usage_metadata` |
Metadata about the response(s). |
`truncated` |
`bool`
Whether the input content was truncated before generating the embedding. |

## Classes

### Embedding

`Embedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of floats representing an embedding.

## Methods

### EmbedContentResponse

`EmbedContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.EmbedContent.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteArtifactRequest -->

# Class DeleteArtifactRequest (1.134.0)

`DeleteArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Artifact to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`etag` |
`str`
Optional. The etag of the Artifact to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteArtifactRequest

`DeleteArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteArtifact.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragvectordbconfigragmanagedvertexvectorsearch_a862ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragvectordbconfigragmanagedvertexvectorsearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.RagManagedVertexVectorSearch -->

# Class RagManagedVertexVectorSearch (1.134.0)

```
RagManagedVertexVectorSearch(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for the RAG-managed Vertex Vector Search 2.0.

## Attribute |
|
|---|---|
Name |
Description |
`collection_name` |
`str`
Output only. The resource name of the Vector Search 2.0 Collection that RAG Created for the corpus. Only populated after the corpus is successfully created. Format: `projects/{project}/locations/{location}/collections/{collection_id}`
|

## Methods

### RagManagedVertexVectorSearch

```
RagManagedVertexVectorSearch(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for the RAG-managed Vertex Vector Search 2.0.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesendpoint_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service -->

# Package endpoint_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.endpoint_service`

package.

## Classes

[EndpointServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceAsyncClient)

A service for managing Vertex AI's Endpoints.

[EndpointServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.EndpointServiceClient)

A service for managing Vertex AI's Endpoints.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers)

API documentation for `aiplatform_v1beta1.services.endpoint_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesdeleteentitytyperequest_googlecloudaiplatform_v1_16ee68.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeleteentitytyperequest_googlecloudaiplatform_v1b_3062eb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeleteentitytyperequest_googlecloudaiplatform_v1be_0fb14b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeleteentitytyperequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEntityTypeRequest -->

# Class DeleteEntityTypeRequest (1.134.0)

`DeleteEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.DeleteEntityType.

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


Request message for FeaturestoreService.DeleteEntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service -->

# Package session_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.session_service`

package.

## Classes

[SessionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceAsyncClient)

The service that manages Vertex Session related resources.

[SessionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.SessionServiceClient)

The service that manages Vertex Session related resources.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers)

API documentation for `aiplatform_v1beta1.services.session_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatavisualization_54792c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadatainputmetadatavisualizationcolormap.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata.Visualization.ColorMap -->

# Class ColorMap (1.134.0)

`ColorMap(value)`


The color scheme used for highlighting areas.

## Enums |
|
|---|---|
Name |
Description |
`COLOR_MAP_UNSPECIFIED` |
Should not be used. |
`PINK_GREEN` |
Positive: green. Negative: pink. |
`VIRIDIS` |
Viridis color map: A perceptually uniform color mapping which is easier to see by those with colorblindness and progresses from yellow to green to blue. Positive: yellow. Negative: blue. |
`RED` |
Positive: red. Negative: red. |
`GREEN` |
Positive: green. Negative: green. |
`RED_GREEN` |
Positive: green. Negative: red. |
`PINK_WHITE_GREEN` |
PiYG palette. |

## Methods

### ColorMap

`ColorMap(value)`


The color scheme used for highlighting areas.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatedatasetrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDatasetRequest -->

# Class UpdateDatasetRequest (1.134.0)

`UpdateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`dataset` |
Required. The Dataset which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
Updatable fields:
- `display_name`
- `description`
- `labels`
|

## Methods

### UpdateDatasetRequest

`UpdateDatasetRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.UpdateDataset.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgroundingmetadata__googlecloudaiplatform_v1beta1ty_dfb13c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingMetadata -->

# Class GroundingMetadata (1.134.0)

`GroundingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata returned to client when grounding is enabled.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`web_search_queries` |
`MutableSequence[str]`
Optional. Web search queries for the following-up web search. |
`search_entry_point` |
Optional. Google search entry for the following-up web searches. This field is a member of `oneof` _ `_search_entry_point` .
|
`grounding_chunks` |
`MutableSequence[`
List of supporting references retrieved from specified grounding source. |
`grounding_supports` |
`MutableSequence[`
Optional. List of grounding support. |
`retrieval_metadata` |
Optional. Output only. Retrieval metadata. This field is a member of `oneof` _ `_retrieval_metadata` .
|
`google_maps_widget_context_token` |
`str`
Optional. Output only. Resource name of the Google Maps widget context token to be used with the PlacesContextElement widget to render contextual data. This is populated only for Google Maps grounding. This field is a member of `oneof` _ `_google_maps_widget_context_token` .
|
`source_flagging_uris` |
`MutableSequence[`
List of source flagging uris. This is currently populated only for Google Maps grounding. |

## Classes

### SourceFlaggingUri

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.

## Methods

### GroundingMetadata

`GroundingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata returned to client when grounding is enabled.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureonlinestorestate_googlecloudaiplatform_02b021.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestorestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.State -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespscinterfaceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PscInterfaceConfig -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescustomjobspec___googlecloudaiplatform_v1beta1typ_6596f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescustomjobspec___googlecloudaiplatform_v1beta1type_a21ff9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescustomjobspec___googlecloudaiplatform_v1beta1types_03d529.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescustomjobspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CustomJobSpec -->

# Class CustomJobSpec (1.134.0)

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location which to run If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`worker_pool_specs` |
`MutableSequence[`
Required. The spec of the worker pools including machine type and Docker image. All worker pools except the first one are optional and can be skipped by providing an empty value. |
`scheduling` |
Scheduling options for a CustomJob. |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If unspecified, the `Vertex AI Custom Code Service Agent |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to which the Job should be peered. For example,
`projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved ip ranges under the VPC network that can be used for this job. If set, we will deploy the job within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for CustomJob. |
`base_output_directory` |
The Cloud Storage location to store the output of this CustomJob or HyperparameterTuningJob. For HyperparameterTuningJob, the baseOutputDirectory of each child CustomJob backing a Trial is set to a subdirectory of name id under its parent HyperparameterTuningJob's baseOutputDirectory. The following Vertex AI environment variables will be passed to containers or python modules when this field is set: For CustomJob: - AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
For CustomJob backing a Trial of HyperparameterTuningJob:
- AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
|
`protected_artifact_location_id` |
`str`
The ID of the location to store protected artifacts. e.g. us-central1. Populate only when the location is different than CustomJob location. List of supported locations: https://cloud.google.com/vertex-ai/docs/general/locations |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`enable_web_access` |
`bool`
Optional. Whether you want Vertex AI to enable `interactive shell access |
`enable_dashboard_access` |
`bool`
Optional. Whether you want Vertex AI to enable access to the customized dashboard in training chief container. If set to `true` , you can access the dashboard at the URIs
given by
CustomJob.web_access_uris
or
Trial.web_access_uris
(within
HyperparameterTuningJob.trials).
|
`experiment` |
`str`
Optional. The Experiment associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}`
|
`experiment_run` |
`str`
Optional. The Experiment Run associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}-{experiment-run-name}`
|
`models` |
`MutableSequence[str]`
Optional. The name of the Model resources for which to generate a mapping to artifact URIs. Applicable only to some of the Google-provided custom jobs. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### CustomJobSpec

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesindexdatapointrestriction_googlecloudaiplatf_69ae2e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesindexdatapointrestriction_googlecloudaiplatfo_9d17dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapointrestriction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint.Restriction -->

# Class Restriction (1.134.0)

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).

## Attributes |
|
|---|---|
Name |
Description |
`namespace` |
`str`
The namespace of this restriction. e.g.: color. |
`allow_list` |
`MutableSequence[str]`
The attributes to allow in this namespace. e.g.: 'red' |
`deny_list` |
`MutableSequence[str]`
The attributes to deny in this namespace. e.g.: 'blue' |

## Methods

### Restriction

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service -->

# Package notebook_service (1.134.0)

API documentation for `aiplatform_v1.services.notebook_service`

package.

## Classes

[NotebookServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceAsyncClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

[NotebookServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.NotebookServiceClient)

The interface for Vertex Notebook service (a.k.a. Colab on Workbench).

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers)

API documentation for `aiplatform_v1.services.notebook_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfindneighborsresponse_googlecloudaiplatform_v_10a8ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsResponse -->

# Class FindNeighborsResponse (1.134.0)

`FindNeighborsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.FindNeighbors.

## Attribute |
|
|---|---|
Name |
Description |
`nearest_neighbors` |
`MutableSequence[`
The nearest neighbors of the query datapoints. |

## Classes

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Methods

### FindNeighborsResponse

`FindNeighborsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The response message for MatchService.FindNeighbors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistmodeldeploymentmonitoringjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesresponse_googleclo_16932f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesresponse_googleclou_c6cf93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesresponse_googlecloud_594d49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesResponse -->

# Class ListModelEvaluationSlicesResponse (1.134.0)

```
ListModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluationSlices.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluation_slices` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationSlicesRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationSlicesResponse

```
ListModelEvaluationSlicesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluationSlices.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextclassification.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassification -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeletefeaturegrouprequest_googlecloudaiplatform_v1_12f52e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeaturegrouprequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureGroupRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprobeexecaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.ExecAction -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturevaluedestination_googlecloudaiplatform_v1be_484960.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturevaluedestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueDestination -->

# Class FeatureValueDestination (1.134.0)

`FeatureValueDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A destination location for Feature values and format.

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
`bigquery_destination` |
Output in BigQuery format. BigQueryDestination.output_uri in FeatureValueDestination.bigquery_destination must refer to a table. This field is a member of `oneof` _ `destination` .
|
`tfrecord_destination` |
Output in TFRecord format. Below are the mapping from Feature value type in Featurestore to Feature value type in TFRecord: :: Value type in Featurestore | Value type in TFRecord DOUBLE, DOUBLE_ARRAY | FLOAT_LIST INT64, INT64_ARRAY | INT64_LIST STRING, STRING_ARRAY, BYTES | BYTES_LIST true -> byte_string("true"), false -> byte_string("false") BOOL, BOOL_ARRAY (true, false) | BYTES_LIST This field is a member of `oneof` _ `destination` .
|
`csv_destination` |
Output in CSV format. Array Feature value types are not allowed in CSV format. This field is a member of `oneof` _ `destination` .
|

## Methods

### FeatureValueDestination

`FeatureValueDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A destination location for Feature values and format.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigsnapshotanalysis.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.SnapshotAnalysis -->

# Class SnapshotAnalysis (1.134.0)

`SnapshotAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's Snapshot Analysis Based Monitoring. This type of analysis generates statistics for each Feature based on a snapshot of the latest feature value of each entities every monitoring_interval.

## Attributes |
|
|---|---|
Name |
Description |
`disabled` |
`bool`
The monitoring schedule for snapshot analysis. For EntityType-level config: unset / disabled = true indicates disabled by default for Features under it; otherwise by default enable snapshot analysis monitoring with monitoring_interval for Features under it. Feature-level config: disabled = true indicates disabled regardless of the EntityType-level config; unset monitoring_interval indicates going with EntityType-level config; otherwise run snapshot analysis monitoring with monitoring_interval regardless of the EntityType-level config. Explicitly Disable the snapshot analysis based monitoring. |
`monitoring_interval` |
`google.protobuf.duration_pb2.Duration`
Configuration of the snapshot analysis based monitoring pipeline running interval. The value is rolled up to full day. If both monitoring_interval_days and the deprecated `monitoring_interval` field are set
when creating/updating EntityTypes/Features,
monitoring_interval_days
will be used.
|
`monitoring_interval_days` |
`int`
Configuration of the snapshot analysis based monitoring pipeline running interval. The value indicates number of days. |
`staleness_days` |
`int`
Customized export features time window for snapshot analysis. Unit is one day. Default value is 3 weeks. Minimum value is 1 day. Maximum value is 4000 days. |

## Methods

### SnapshotAnalysis

`SnapshotAnalysis(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration of the Featurestore's Snapshot Analysis Based Monitoring. This type of analysis generates statistics for each Feature based on a snapshot of the latest feature value of each entities every monitoring_interval.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpipelinejob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob -->

# Class PipelineJob (1.134.0)

```
PipelineJob(
display_name: str,
template_path: str,
job_id: typing.Optional[str] = None,
pipeline_root: typing.Optional[str] = None,
parameter_values: typing.Optional[typing.Dict[str, typing.Any]] = None,
input_artifacts: typing.Optional[typing.Dict[str, str]] = None,
enable_caching: typing.Optional[bool] = None,
encryption_spec_key_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
failure_policy: typing.Optional[str] = None,
)
```


Retrieves a PipelineJob resource and instantiates its representation.

## Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this Pipeline. |
`template_path` |
`str`
Required. The path of PipelineJob or PipelineSpec JSON or YAML file. It can be a local path, a Google Cloud Storage URI (e.g. "gs://project.name"), an Artifact Registry URI (e.g. " |
`job_id` |
`str`
Optional. The unique ID of the job run. If not specified, pipeline name + timestamp will be used. |
`pipeline_root` |
`str`
Optional. The root of the pipeline outputs. If not set, the staging bucket set in aiplatform.init will be used. If that's not set a pipeline-specific artifacts bucket will be used. |
`parameter_values` |
`Dict[str, Any]`
Optional. The mapping from runtime parameter names to its values that control the pipeline run. |
`input_artifacts` |
`Dict[str, str]`
Optional. The mapping from the runtime parameter name for this artifact to its resource id. For example: "vertex_model":"456". Note: full resource name ("projects/123/locations/us-central1/metadataStores/default/artifacts/456") cannot be used. |
`enable_caching` |
`bool`
Optional. Whether to turn on caching for the run. If this is not set, defaults to the compile time settings, which are True for all tasks by default, while users may specify different caching options for individual tasks. If this is set, the setting applies to all tasks in the pipeline. Overrides the compile time settings. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`labels` |
`Dict[str, str]`
Optional. The user defined metadata to organize PipelineJob. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to create this PipelineJob. Overrides credentials set in aiplatform.init. |
`project` |
`str`
Optional. The project that you want to run this PipelineJob in. If not set, the project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to create PipelineJob. If not set, location set in aiplatform.init will be used. |
`failure_policy` |
`str`
Optional. The failure policy - "slow" or "fast". Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW (corresponds to "slow"). However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST (corresponds to "fast"), it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion. |

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### has_failed

Returns True if pipeline has failed.

False otherwise.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### state

Current pipeline state.

### update_time

Time this resource was last updated.

## Methods

### __init_subclass__

```
__init_subclass__(
*,
experiment_loggable_schemas: typing.Tuple[
google.cloud.aiplatform.metadata.experiment_resources._ExperimentLoggableSchema
],
**kwargs
)
```


Register the metadata_schema for the subclass so Experiment can use it to retrieve the associated types.

usage:

class PipelineJob(..., experiment_loggable_schemas= (_ExperimentLoggableSchema(title='system.PipelineRun'), )

### batch_cancel

```
batch_cancel(
project: str, location: str, names: typing.List[str]
) -> google.api_core.operation.Operation
```


Example Usage: pipeline_job = aiplatform.PipelineJob( display_name='job_display_name', template_path='your_pipeline.yaml', ) pipeline_job.batch_cancel( project='your_project_id', location='your_location', names=['pipeline_job_name', 'pipeline_job_name2'] )

Returns |
|
|---|---|
Type |
Description |
`operation (Operation)` |
An object representing a long-running operation. |

### batch_delete

```
batch_delete(
project: str, location: str, names: typing.List[str]
) -> google.cloud.aiplatform_v1.types.pipeline_service.BatchDeletePipelineJobsResponse
```


Example Usage: pipeline_job = aiplatform.PipelineJob( display_name='job_display_name', template_path='your_pipeline.yaml', ) pipeline_job.batch_delete( project='your_project_id', location='your_location', names=['pipeline_job_name', 'pipeline_job_name2'] )

### cancel

`cancel() -> None`


Starts asynchronous cancellation on the PipelineJob. The server
makes a best effort to cancel the job, but success is not guaranteed.
On successful cancellation, the PipelineJob is not deleted; instead it
becomes a job with state set to `CANCELLED`

.

### clone

```
clone(
display_name: typing.Optional[str] = None,
job_id: typing.Optional[str] = None,
pipeline_root: typing.Optional[str] = None,
parameter_values: typing.Optional[typing.Dict[str, typing.Any]] = None,
input_artifacts: typing.Optional[typing.Dict[str, str]] = None,
enable_caching: typing.Optional[bool] = None,
encryption_spec_key_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
) -> google.cloud.aiplatform.pipeline_jobs.PipelineJob
```


Returns a new PipelineJob object with the same settings as the original one.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of this cloned Pipeline. If not specified, original pipeline display name will be used. |
`job_id` |
`str`
Optional. The unique ID of the job run. If not specified, "cloned" + pipeline name + timestamp will be used. |
`pipeline_root` |
`str`
Optional. The root of the pipeline outputs. Default to be the same staging bucket as original pipeline. |
`parameter_values` |
`Dict[str, Any]`
Optional. The mapping from runtime parameter names to its values that control the pipeline run. Defaults to be the same values as original PipelineJob. |
`input_artifacts` |
`Dict[str, str]`
Optional. The mapping from the runtime parameter name for this artifact to its resource id. Defaults to be the same values as original PipelineJob. For example: "vertex_model":"456". Note: full resource name ("projects/123/locations/us-central1/metadataStores/default/artifacts/456") cannot be used. |
`enable_caching` |
`bool`
Optional. Whether to turn on caching for the run. If this is not set, defaults to be the same as original pipeline. If this is set, the setting applies to all tasks in the pipeline. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`labels` |
`Dict[str, str]`
Optional. The user defined metadata to organize PipelineJob. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to create this PipelineJob. Overrides credentials set in aiplatform.init. |
`project` |
`str`
Optional. The project that you want to run this PipelineJob in. If not set, the project set in original PipelineJob will be used. |
`location` |
`str`
Optional. Location to create PipelineJob. If not set, location set in original PipelineJob will be used. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If job_id or labels have incorrect format. |

### create_schedule

```
create_schedule(
cron: str,
display_name: str,
start_time: typing.Optional[str] = None,
end_time: typing.Optional[str] = None,
allow_queueing: bool = False,
max_run_count: typing.Optional[int] = None,
max_concurrent_run_count: int = 1,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.pipeline_job_schedules.PipelineJobSchedule
```


Creates a PipelineJobSchedule directly from a PipelineJob.

Example Usage:

pipeline_job = aiplatform.PipelineJob( display_name='job_display_name', template_path='your_pipeline.yaml', ) pipeline_job.run() pipeline_job_schedule = pipeline_job.create_schedule( cron='* * * * *', display_name='schedule_display_name', )

Parameters |
|
|---|---|
Name |
Description |
`cron` |
`str`
Required. Time specification (cron schedule expression) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 * * * *", or "TZ=America/New_York 1 * * * *". |
`display_name` |
`str`
Required. The user-defined name of this PipelineJobSchedule. |
`start_time` |
`str`
Optional. Timestamp after which the first run can be scheduled. If unspecified, it defaults to the schedule creation timestamp. |
`end_time` |
`str`
Optional. Timestamp after which no more runs will be scheduled. If unspecified, then runs will be scheduled indefinitely. |
`allow_queueing` |
`bool`
Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. |
`max_run_count` |
`int`
Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count >= max_run_count or when end_time is reached. Must be positive and <= 2^63-1. |
`max_concurrent_run_count` |
`int`
Optional. Maximum number of runs that can be started concurrently for this PipelineJobSchedule. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Helper method that return True is PipelineJob is done. False otherwise.

### from_pipeline_func

```
from_pipeline_func(
pipeline_func: typing.Callable,
parameter_values: typing.Optional[typing.Dict[str, typing.Any]] = None,
input_artifacts: typing.Optional[typing.Dict[str, str]] = None,
output_artifacts_gcs_dir: typing.Optional[str] = None,
enable_caching: typing.Optional[bool] = None,
context_name: typing.Optional[str] = "pipeline",
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
job_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
) -> google.cloud.aiplatform.pipeline_jobs.PipelineJob
```


Creates PipelineJob by compiling a pipeline function.

Parameters |
|
|---|---|
Name |
Description |
`pipeline_func` |
`Callable`
Required. A pipeline function to compile. A pipeline function creates instances of components and connects component inputs to outputs. |
`parameter_values` |
`Dict[str, Any]`
Optional. The mapping from runtime parameter names to its values that control the pipeline run. |
`input_artifacts` |
`Dict[str, str]`
Optional. The mapping from the runtime parameter name for this artifact to its resource id. For example: "vertex_model":"456". Note: full resource name ("projects/123/locations/us-central1/metadataStores/default/artifacts/456") cannot be used. |
`output_artifacts_gcs_dir` |
`str`
Optional. The GCS location of the pipeline outputs. A GCS bucket for artifacts will be created if not specified. |
`enable_caching` |
`bool`
Optional. Whether to turn on caching for the run. If this is not set, defaults to the compile time settings, which are True for all tasks by default, while users may specify different caching options for individual tasks. If this is set, the setting applies to all tasks in the pipeline. Overrides the compile time settings. |
`context_name` |
`str`
Optional. The name of metadata context. Used for cached execution reuse. |
`display_name` |
`str`
Optional. The user-defined name of this Pipeline. |
`labels` |
`Dict[str, str]`
Optional. The user defined metadata to organize PipelineJob. |
`job_id` |
`str`
Optional. The unique ID of the job run. If not specified, pipeline name + timestamp will be used. |
`project` |
`str`
Optional. The project that you want to run this PipelineJob in. If not set, the project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to create PipelineJob. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to create this PipelineJob. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If job_id or labels have incorrect format. |

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.pipeline_jobs.PipelineJob
```


Get a Vertex AI Pipeline Job for the given resource_name.

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
Optional. Project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

### get_associated_experiment

```
get_associated_experiment() -> (
typing.Optional[google.cloud.aiplatform.metadata.experiment_resources.Experiment]
)
```


Gets the aiplatform.Experiment associated with this PipelineJob, or None if this PipelineJob is not associated with an experiment.

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
enable_simple_view: bool = False,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.pipeline_jobs.PipelineJob]
```


List all instances of this PipelineJob resource.

Example Usage:

aiplatform.PipelineJob.list( filter='display_name="experiment_a27"', order_by='create_time desc' )

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`enable_simple_view` |
`bool`
Optional. Whether to pass the |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### run

```
run(
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
reserved_ip_ranges: typing.Optional[typing.List[str]] = None,
sync: typing.Optional[bool] = True,
create_request_timeout: typing.Optional[float] = None,
enable_preflight_validations: typing.Optional[bool] = False,
) -> None
```


Run this configured PipelineJob and monitor the job until completion.

Parameters |
|
|---|---|
Name |
Description |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`reserved_ip_ranges` |
`List[str]`
Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this PipelineJob's workload. For example: ['vertex-ai-ip-range']. |
`sync` |
`bool`
Optional. Whether to execute this method synchronously. If False, this method will unblock and it will be executed in a concurrent Future. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`enable_preflight_validations` |
`bool`
Optional. Whether to enable preflight validations for the PipelineJob. |

### submit

```
submit(
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
reserved_ip_ranges: typing.Optional[typing.List[str]] = None,
create_request_timeout: typing.Optional[float] = None,
*,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
enable_preflight_validations: typing.Optional[bool] = False
) -> None
```


Run this configured PipelineJob.

Parameters |
|
|---|---|
Name |
Description |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the network set in aiplatform.init will be used. Otherwise, the job is not peered with any network. |
`reserved_ip_ranges` |
`List[str]`
Optional. A list of names for the reserved IP ranges under the VPC network that can be used for this PipelineJob's workload. For example: ['vertex-ai-ip-range']. If left unspecified, the job will be deployed to any IP ranges under the provided VPC network. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`experiment` |
`Union[str, experiments_resource.Experiment]`
Optional. The Vertex AI experiment name or instance to associate to this PipelineJob. Metrics produced by the PipelineJob as system.Metric Artifacts will be associated as metrics to the current Experiment Run. Pipeline parameters will be associated as parameters to the current Experiment Run. |
`enable_preflight_validations` |
`bool`
Optional. Whether to enable preflight validations for the PipelineJob. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Wait for this PipelineJob to complete.

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until resource has been created.


---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapoi_f3e777.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapoin_7db60a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapoint_19ca57.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointf_ace3cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfi_0b7963.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfie_28f668.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfieldmappingnumericrestrict.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping.NumericRestrict -->

# Class NumericRestrict (1.134.0)

`NumericRestrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on numeric values.

## Attributes |
|
|---|---|
Name |
Description |
`namespace` |
`str`
Required. The namespace of the restrict. |
`value_column` |
`str`
Optional. The column containing the numeric value. |
`value_type` |
Required. Numeric type of the restrict. Must be consistent for all datapoints within the namespace. |

## Classes

### ValueType

`ValueType(value)`


The type of numeric value for the restrict.

## Methods

### NumericRestrict

`NumericRestrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on numeric values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestimeseriesdata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TimeSeriesData -->

# Class TimeSeriesData (1.134.0)

`TimeSeriesData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All the data stored in a TensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_time_series_id` |
`str`
Required. The ID of the TensorboardTimeSeries, which will become the final component of the TensorboardTimeSeries' resource name |
`value_type` |
Required. Immutable. The value type of this time series. All the values in this time series data must match this value type. |
`values` |
`MutableSequence[`
Required. Data points in this time series. |

## Methods

### TimeSeriesData

`TimeSeriesData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


All the data stored in a TensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewsyncconfig_googlecloudaiplatform_v_314c89.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewsyncconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.SyncConfig -->

# Class SyncConfig (1.134.0)

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.

## Attribute |
|
|---|---|
Name |
Description |
`cron` |
`str`
Cron schedule (https://en.wikipedia.org/wiki/Cron) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*". |

## Methods

### SyncConfig

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnotebookexecutionjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse -->

# Class ListNotebookExecutionJobsResponse (1.134.0)

```
ListNotebookExecutionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [NotebookService.CreateNotebookExecutionJob]

## Attributes |
|
|---|---|
Name |
Description |
`notebook_execution_jobs` |
`MutableSequence[`
List of NotebookExecutionJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookExecutionJobsRequest.page_token to obtain that page. |

## Methods

### ListNotebookExecutionJobsResponse

```
ListNotebookExecutionJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [NotebookService.CreateNotebookExecutionJob]


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesuploadragfilerequest_googlecloudaiplatform_v_41744b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesuploadragfilerequest_googlecloudaiplatform_v1_905a7b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesuploadragfilerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileRequest -->

# Class UploadRagFileRequest (1.134.0)

`UploadRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UploadRagFile.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the RagCorpus resource into which to upload the file. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`rag_file` |
Required. The RagFile to upload. |
`upload_rag_file_config` |
Required. The config for the RagFiles to be uploaded into the RagCorpus. VertexRagDataService.UploadRagFile. |

## Methods

### UploadRagFileRequest

`UploadRagFileRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.UploadRagFile.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessuggesttrialsmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SuggestTrialsMetadata -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesresumemodeldeploymentmonitoringjobrequest_googlecl_b6b5af.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesresumemodeldeploymentmonitoringjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeModelDeploymentMonitoringJobRequest -->

# Class ResumeModelDeploymentMonitoringJobRequest (1.134.0)

```
ResumeModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ResumeModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelDeploymentMonitoringJob to resume. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{model_deployment_monitoring_job}`
|

## Methods

### ResumeModelDeploymentMonitoringJobRequest

```
ResumeModelDeploymentMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ResumeModelDeploymentMonitoringJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragmanageddbconfigbasic.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig.Basic -->

# Class Basic (1.134.0)

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

## Methods

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeleteexecutionrequest_googlecloudaiplatfor_2c730c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeleteexecutionrequest_googlecloudaiplatform_022f2c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeleteexecutionrequest_googlecloudaiplatform__f118dc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeleteexecutionrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExecutionRequest -->

# Class DeleteExecutionRequest (1.134.0)

`DeleteExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteExecution.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Execution to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/executions/{execution}`
|
`etag` |
`str`
Optional. The etag of the Execution to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteExecutionRequest

`DeleteExecutionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteExecution.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeatureviewsyncsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse -->

# Class ListFeatureViewSyncsResponse (1.134.0)

```
ListFeatureViewSyncsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view_syncs` |
`MutableSequence[`
The FeatureViewSyncs matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeatureViewSyncsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeatureViewSyncsResponse

```
ListFeatureViewSyncsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturevaluedestination.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination -->

# Class FeatureValueDestination (1.134.0)

`FeatureValueDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A destination location for Feature values and format.

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
`bigquery_destination` |
Output in BigQuery format. BigQueryDestination.output_uri in FeatureValueDestination.bigquery_destination must refer to a table. This field is a member of `oneof` _ `destination` .
|
`tfrecord_destination` |
Output in TFRecord format. Below are the mapping from Feature value type in Featurestore to Feature value type in TFRecord: :: Value type in Featurestore | Value type in TFRecord DOUBLE, DOUBLE_ARRAY | FLOAT_LIST INT64, INT64_ARRAY | INT64_LIST STRING, STRING_ARRAY, BYTES | BYTES_LIST true -> byte_string("true"), false -> byte_string("false") BOOL, BOOL_ARRAY (true, false) | BYTES_LIST This field is a member of `oneof` _ `destination` .
|
`csv_destination` |
Output in CSV format. Array Feature value types are not allowed in CSV format. This field is a member of `oneof` _ `destination` .
|

## Methods

### FeatureValueDestination

`FeatureValueDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A destination location for Feature values and format.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescustomjobspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomJobSpec -->

# Class CustomJobSpec (1.134.0)

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location which to run If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`worker_pool_specs` |
`MutableSequence[`
Required. The spec of the worker pools including machine type and Docker image. All worker pools except the first one are optional and can be skipped by providing an empty value. |
`scheduling` |
Scheduling options for a CustomJob. |
`service_account` |
`str`
Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. If unspecified, the `Vertex AI Custom Code Service Agent |
`network` |
`str`
Optional. The full name of the Compute Engine `network ` __
to which the Job should be peered. For example,
`projects/12345/global/networks/myVPC` .
`Format ` __
is of the form
`projects/{project}/global/networks/{network}` . Where
{project} is a project number, as in `12345` , and
{network} is a network name.
To specify this field, you must have already `configured VPC
Network Peering for Vertex
AI |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of names for the reserved ip ranges under the VPC network that can be used for this job. If set, we will deploy the job within the provided ip ranges. Otherwise, the job will be deployed to any ip ranges under the provided VPC network. Example: ['vertex-ai-ip-range']. |
`psc_interface_config` |
Optional. Configuration for PSC-I for CustomJob. |
`base_output_directory` |
The Cloud Storage location to store the output of this CustomJob or HyperparameterTuningJob. For HyperparameterTuningJob, the baseOutputDirectory of each child CustomJob backing a Trial is set to a subdirectory of name id under its parent HyperparameterTuningJob's baseOutputDirectory. The following Vertex AI environment variables will be passed to containers or python modules when this field is set: For CustomJob: - AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
For CustomJob backing a Trial of HyperparameterTuningJob:
- AIP_MODEL_DIR =
- AIP_CHECKPOINT_DIR =
- AIP_TENSORBOARD_LOG_DIR =
|
`protected_artifact_location_id` |
`str`
The ID of the location to store protected artifacts. e.g. us-central1. Populate only when the location is different than CustomJob location. List of supported locations: https://cloud.google.com/vertex-ai/docs/general/locations |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`enable_web_access` |
`bool`
Optional. Whether you want Vertex AI to enable `interactive shell access |
`enable_dashboard_access` |
`bool`
Optional. Whether you want Vertex AI to enable access to the customized dashboard in training chief container. If set to `true` , you can access the dashboard at the URIs
given by
CustomJob.web_access_uris
or
Trial.web_access_uris
(within
HyperparameterTuningJob.trials).
|
`experiment` |
`str`
Optional. The Experiment associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}`
|
`experiment_run` |
`str`
Optional. The Experiment Run associated with this job. Format: `projects/{project}/locations/{location}/metadataStores/{metadataStores}/contexts/{experiment-name}-{experiment-run-name}`
|
`models` |
`MutableSequence[str]`
Optional. The name of the Model resources for which to generate a mapping to artifact URIs. Applicable only to some of the Google-provided custom jobs. Format: `projects/{project}/locations/{location}/models/{model}`
In order to retrieve a specific version of the model, also
provide the version ID or version alias. Example:
`projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
If no version ID or alias is specified, the "default"
version will be returned. The "default" version alias is
created for the first version of the model, and can be moved
to other versions later on. There will be exactly one
default version.
|

## Methods

### CustomJobSpec

`CustomJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a CustomJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformautomltabulartrainingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob -->

# Class AutoMLTabularTrainingJob (1.134.0)

```
AutoMLTabularTrainingJob(
display_name: str,
optimization_prediction_type: str,
optimization_objective: typing.Optional[str] = None,
column_specs: typing.Optional[typing.Dict[str, str]] = None,
column_transformations: typing.Optional[
typing.List[typing.Dict[str, typing.Dict[str, str]]]
] = None,
optimization_objective_recall_value: typing.Optional[float] = None,
optimization_objective_precision_value: typing.Optional[float] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
training_encryption_spec_key_name: typing.Optional[str] = None,
model_encryption_spec_key_name: typing.Optional[str] = None,
)
```


Constructs a AutoML Tabular Training Job.

Example usage:

job = training_jobs.AutoMLTabularTrainingJob( display_name="my_display_name", optimization_prediction_type="classification", optimization_objective="minimize-log-loss", column_specs={"column_1": "auto", "column_2": "numeric"}, labels={'key': 'value'}, )

## Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this TrainingPipeline. |
`optimization_prediction_type` |
`str`
The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings. |
`optimization_objective` |
`str`
Optional. Objective function the Model is to be optimized towards. The training task creates a Model that maximizes/minimizes the value of the objective function over the validation set. The supported optimization objectives depend on the prediction type, and in the case of classification also the number of distinct values in the target column (two distint values -> binary, 3 or more distinct values -> multi class). If the field is not set, the default objective function is used. Classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value. Classification (multi class): "minimize-log-loss" (default) - Minimize log loss. Regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). |
`column_specs` |
`Dict[str, str]`
Optional. Alternative to column_transformations where the keys of the dict are column names and their respective values are one of AutoMLTabularTrainingJob.column_data_types. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. If none of column_transformations or column_specs is passed, the local credentials being used will try setting column_specs to "auto". To do this, the local credentials require read access to the GCS or BigQuery training data source. |
`column_transformations` |
`List[Dict[str, Dict[str, str]]]`
Optional. Transformations to apply to the input columns (i.e. columns other than the targetColumn). Each transformation may produce multiple result values from the column's value, and all are used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. Only columns with no child should have a transformation. If an input column has no transformations on it, such a column is ignored by the training, except for the targetColumn, which should have no transformations defined on. Only one of column_transformations or column_specs should be passed. Consider using column_specs as column_transformations will be deprecated eventually. If none of column_transformations or column_specs is passed, the local credentials being used will try setting column_transformations to "auto". To do this, the local credentials require read access to the GCS or BigQuery training data source. |
`optimization_objective_recall_value` |
`float`
Optional. Required when maximize-precision-at-recall optimizationObjective was picked, represents the recall value at which the optimization is done. The minimum value is 0 and the maximum is 1.0. |
`optimization_objective_precision_value` |
`float`
Optional. Required when maximize-recall-at-precision optimizationObjective was picked, represents the precision value at which the optimization is done. The minimum value is 0 and the maximum is 1.0. |
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

### get_auto_column_specs

```
get_auto_column_specs(
dataset: google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset,
target_column: str,
) -> typing.Dict[str, str]
```


Returns a dict with all non-target columns as keys and 'auto' as values.

Example usage:

column_specs = training_jobs.AutoMLTabularTrainingJob.get_auto_column_specs( dataset=my_dataset, target_column="my_target_column", )

Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TabularDataset`
Required. Intended dataset. |
`target_column` |
`str`
Required. Intended target column. |

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
dataset: google.cloud.aiplatform.datasets.tabular_dataset.TabularDataset,
target_column: str,
training_fraction_split: typing.Optional[float] = None,
validation_fraction_split: typing.Optional[float] = None,
test_fraction_split: typing.Optional[float] = None,
predefined_split_column_name: typing.Optional[str] = None,
timestamp_split_column_name: typing.Optional[str] = None,
weight_column: typing.Optional[str] = None,
budget_milli_node_hours: int = 1000,
model_display_name: typing.Optional[str] = None,
model_labels: typing.Optional[typing.Dict[str, str]] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
model_version_aliases: typing.Optional[typing.Sequence[str]] = None,
model_version_description: typing.Optional[str] = None,
disable_early_stopping: bool = False,
export_evaluated_data_items: bool = False,
export_evaluated_data_items_bigquery_destination_uri: typing.Optional[str] = None,
export_evaluated_data_items_override_destination: bool = False,
additional_experiments: typing.Optional[typing.List[str]] = None,
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
Predefined splits:
Assigns input data to training, validation, and test sets based on the value of a provided key.
If using predefined splits, `predefined_split_column_name` must be provided.
Supported only for tabular Datasets.
Timestamp splits:
Assigns input data to training, validation, and test sets
based on a provided timestamps. The youngest data pieces are
assigned to training set, next to validation set, and the oldest
to the test set.
Supported only for tabular Datasets.
```


Parameters |
|
|---|---|
Name |
Description |
`dataset` |
`datasets.TabularDataset`
Required. The dataset within the same Project from which data will be used to train the Model. The Dataset must use schema compatible with Model being trained, and what is compatible should be described in the used TrainingPipeline's [training_task_definition] [google.cloud.aiplatform.v1beta1.TrainingPipeline.training_task_definition]. For tabular Datasets, all their data is exported to training, to pick and choose from. |
`target_column` |
`str`
Required. The name of the column values of which the Model is to predict. |
`training_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to train the Model. This is ignored if Dataset is not provided. |
`validation_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to validate the Model. This is ignored if Dataset is not provided. |
`test_fraction_split` |
`float`
Optional. The fraction of the input data that is to be used to evaluate the Model. This is ignored if Dataset is not provided. |
`predefined_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { |
`timestamp_split_column_name` |
`str`
Optional. The key is a name of one of the Dataset's data columns. The value of the key values of the key (the values in the column) must be in RFC 3339 |
`weight_column` |
`str`
Optional. Name of the column that should be used as the weight column. Higher values in this column give more importance to the row during Model training. The column must have numeric values between 0 and 10000 inclusively, and 0 value means that the row is ignored. If the weight column field is not set, then all rows are assumed to have equal weight of 1. |
`budget_milli_node_hours` |
`int`
Optional. The train budget of creating this Model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a Model for the given training set, the training won't be attempted and will error. The minimum value is 1000 and the maximum is 72000. |
`model_display_name` |
`str`
Optional. If the script produces a managed Vertex AI Model. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. If not provided upon creation, the job's display_name is used. |
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
`disable_early_stopping` |
`bool`
Required. If true, the entire budget is used. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that training might stop before the entire training budget has been used, if further training does no longer brings significant improvement to the model. |
`export_evaluated_data_items` |
`bool`
Whether to export the test set predictions to a BigQuery table. If False, then the export is not performed. |
`export_evaluated_data_items_bigquery_destination_uri` |
`string`
Optional. URI of desired destination BigQuery table for exported test set predictions. Expected format: `<project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd'T'HH_mm_ss_SSS'Z'>.evaluated_examples` Applies only if [export_evaluated_data_items] is True.
|
`export_evaluated_data_items_override_destination` |
`bool`
Whether to override the contents of [export_evaluated_data_items_bigquery_destination_uri], if the table exists, for exported test set predictions. If False, and the table exists, then the training job will fail. Applies only if [export_evaluated_data_items] is True and [export_evaluated_data_items_bigquery_destination_uri] is specified. |
`additional_experiments` |
`List[str]`
Optional. Additional experiment flags for the automl tables training. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |

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
The trained Vertex AI Model resource or None if training did not produce a Vertex AI Model. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicespersistent_resource_servicepersistentresourceserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient -->

# Class PersistentResourceServiceClient (1.134.0)

```
PersistentResourceServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
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
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.persistent_resource_service.transports.base.PersistentResourceServiceTransport,
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
google.cloud.aiplatform_v1.types.persistent_resource_service.CreatePersistentResourceRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1
def sample_create_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreatePersistentResourceRequest.html)(
parent="parent_value",
persistent_resource_id="persistent_resource_id_value",
)
# Make the request
operation = client.[create_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_create_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1.types.persistent_resource_service.DeletePersistentResourceRequest,
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
from google.cloud import aiplatform_v1
def sample_delete_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeletePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_delete_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1.types.persistent_resource_service.GetPersistentResourceRequest,
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
) -> google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1
def sample_get_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_get_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
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
google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesPager
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
from google.cloud import aiplatform_v1
def sample_list_persistent_resources():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListPersistentResourcesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_persistent_resources](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_list_persistent_resources)(request=request)
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
The request object. Request message for PersistentResourceService.ListPersistentResources. |
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
google.cloud.aiplatform_v1.types.persistent_resource_service.RebootPersistentResourceRequest,
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
from google.cloud import aiplatform_v1
def sample_reboot_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RebootPersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest.html)(
name="name_value",
)
# Make the request
operation = client.[reboot_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_reboot_persistent_resource)(request=request)
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
google.cloud.aiplatform_v1.types.persistent_resource_service.UpdatePersistentResourceRequest,
dict,
]
] = None,
*,
persistent_resource: typing.Optional[
google.cloud.aiplatform_v1.types.persistent_resource.PersistentResource
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
from google.cloud import aiplatform_v1
def sample_update_persistent_resource():
# Create a client
client = aiplatform_v1.
```[PersistentResourceServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdatePersistentResourceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdatePersistentResourceRequest.html)(
)
# Make the request
operation = client.[update_persistent_resource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.PersistentResourceServiceClient.html#google_cloud_aiplatform_v1_services_persistent_resource_service_PersistentResourceServiceClient_update_persistent_resource)(request=request)
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicemodelserviceasyncclient_googl_a6604f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicemodelserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient -->

# Class ModelServiceAsyncClient (1.134.0)

```
ModelServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing Vertex AI's machine learning Models.

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
`ModelServiceTransport` |
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

### ModelServiceAsyncClient

```
ModelServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ModelServiceTransport,Callable[..., ModelServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_import_evaluated_annotations

```
batch_import_evaluated_annotations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportEvaluatedAnnotationsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
evaluated_annotations: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.evaluated_annotation.EvaluatedAnnotation
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportEvaluatedAnnotationsResponse
)
```


Imports a list of externally generated EvaluatedAnnotations.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_import_evaluated_annotations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportEvaluatedAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[batch_import_evaluated_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_batch_import_evaluated_annotations)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.BatchImportEvaluatedAnnotations |
`parent` |
Required. The name of the parent ModelEvaluationSlice resource. Format: |
`evaluated_annotations` |
`:class:`
Required. Evaluated annotations resource to be imported. This corresponds to the |
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
Response message for ModelService.BatchImportEvaluatedAnnotations |

### batch_import_model_evaluation_slices

```
batch_import_model_evaluation_slices(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportModelEvaluationSlicesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation_slices: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.model_evaluation_slice.ModelEvaluationSlice
]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.types.model_service.BatchImportModelEvaluationSlicesResponse
)
```


Imports a list of externally generated ModelEvaluationSlice.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_import_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[batch_import_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_batch_import_model_evaluation_slices)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.BatchImportModelEvaluationSlices |
`parent` |
Required. The name of the parent ModelEvaluation resource. Format: |
`model_evaluation_slices` |
`:class:`
Required. Model evaluation slice resource to be imported. This corresponds to the |
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
Response message for ModelService.BatchImportModelEvaluationSlices |

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

### copy_model

```
copy_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.CopyModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
source_model: typing.Optional[str] = None,
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


Copies an already existing Vertex AI Model into the specified Location. The source Model must exist in the same Project. When copying custom Models, the users themselves are responsible for xref_Model.metadata content to be region-agnostic, as well as making sure that any resources (e.g. files) it depends on remain accessible.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_copy_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CopyModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest.html)(
model_id="model_id_value",
parent="parent_value",
source_model="source_model_value",
)
# Make the request
operation = client.[copy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_copy_model)(request=request)
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
The request object. Request message for ModelService.CopyModel. |
`parent` |
Required. The resource name of the Location into which to copy the Model. Format: |
`source_model` |
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: |
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

### delete_model

```
delete_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.DeleteModelRequest, dict
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


Deletes a Model.

A model cannot be deleted if any xref_Endpoint resource has a xref_DeployedModel based on the model in its xref_deployed_models field.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_delete_model)(request=request)
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
The request object. Request message for ModelService.DeleteModel. |
`name` |
Required. The name of the Model resource to be deleted. Format: |
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

### delete_model_version

```
delete_model_version(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.DeleteModelVersionRequest,
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


Deletes a Model version.

Model version can only be deleted if there are no xref_DeployedModels created from it. Deleting the only version in the Model is not allowed. Use xref_DeleteModel for deleting the Model instead.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_model_version():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_delete_model_version)(request=request)
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
The request object. Request message for ModelService.DeleteModelVersion. |
`name` |
Required. The name of the model version to be deleted, with a version ID explicitly included. Example: |
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

### endpoint_path

`endpoint_path(project: str, location: str, endpoint: str) -> str`


Returns a fully-qualified endpoint string.

### export_model

```
export_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ExportModelRequest, dict
]
] = None,
*,
name: typing.Optional[str] = None,
output_config: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_service.ExportModelRequest.OutputConfig
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


Exports a trained, exportable Model to a location specified by the user. A Model is considered to be exportable if it has at least one [supported export format][google.cloud.aiplatform.v1beta1.Model.supported_export_formats].

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_export_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ExportModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[export_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_export_model)(request=request)
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
The request object. Request message for ModelService.ExportModel. |
`name` |
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. This corresponds to the |
`output_config` |
Required. The desired output location and configuration. This corresponds to the |
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
`ModelServiceAsyncClient` |
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
`ModelServiceAsyncClient` |
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
`ModelServiceAsyncClient` |
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

### get_model

```
get_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.GetModelRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.model.Model
```


Gets a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_get_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModel. |
`name` |
Required. The name of the Model resource. Format: |
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
A trained machine learning Model. |

### get_model_evaluation

```
get_model_evaluation(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.GetModelEvaluationRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
```


Gets a ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_get_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModelEvaluation. |
`name` |
Required. The name of the ModelEvaluation resource. Format: |
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
A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data. |

### get_model_evaluation_slice

```
get_model_evaluation_slice(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.GetModelEvaluationSliceRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation_slice.ModelEvaluationSlice
```


Gets a ModelEvaluationSlice.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_model_evaluation_slice():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationSliceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationSliceRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_model_evaluation_slice](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_get_model_evaluation_slice)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.GetModelEvaluationSlice. |
`name` |
Required. The name of the ModelEvaluationSlice resource. Format: |
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
A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations. |

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
google.cloud.aiplatform_v1beta1.services.model_service.transports.base.ModelServiceTransport
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

### import_model_evaluation

```
import_model_evaluation(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ImportModelEvaluationRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model_evaluation: typing.Optional[
google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model_evaluation.ModelEvaluation
```


Imports an externally generated ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_import_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ImportModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[import_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_import_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.ImportModelEvaluation |
`parent` |
Required. The name of the parent model resource. Format: |
`model_evaluation` |
Required. Model evaluation resource to be imported. This corresponds to the |
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
A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data. |

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

### list_model_evaluation_slices

```
list_model_evaluation_slices(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationSlicesRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationSlicesAsyncPager
)
```


Lists ModelEvaluationSlices in a ModelEvaluation.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_list_model_evaluation_slices)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluationSlices. |
`parent` |
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: |
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
Response message for ModelService.ListModelEvaluationSlices. Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_evaluations

```
list_model_evaluations(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelEvaluationsRequest,
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
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsAsyncPager
)
```


Lists ModelEvaluations in a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_model_evaluations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_list_model_evaluations)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluations. |
`parent` |
Required. The resource name of the Model to list the ModelEvaluations from. Format: |
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
Response message for ModelService.ListModelEvaluations. Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_version_checkpoints

```
list_model_version_checkpoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsAsyncPager
)
```


Lists checkpoints of the specified model version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_model_version_checkpoints():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionCheckpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_version_checkpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_list_model_version_checkpoints)(request=request)
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
The request object. Request message for ModelService.ListModelVersionCheckpoints. |
`name` |
Required. The name of the model version to list checkpoints for. |
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
Response message for ModelService.ListModelVersionCheckpoints Iterating over this object will yield results and resolve additional pages automatically. |

### list_model_versions

```
list_model_versions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
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
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsAsyncPager
)
```


Lists versions of the specified model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_model_versions():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_list_model_versions)(request=request)
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
The request object. Request message for ModelService.ListModelVersions. |
`name` |
Required. The name of the model to list versions for. This corresponds to the |
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
Response message for ModelService.ListModelVersions Iterating over this object will yield results and resolve additional pages automatically. |

### list_models

```
list_models(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.ListModelsRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsAsyncPager
```


Lists Models in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_list_models)(request=request)
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
The request object. Request message for ModelService.ListModels. |
`parent` |
Required. The resource name of the Location to list the Models from. Format: |
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
Response message for ModelService.ListModels Iterating over this object will yield results and resolve additional pages automatically. |

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

### merge_version_aliases

```
merge_version_aliases(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.MergeVersionAliasesRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
version_aliases: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model.Model
```


Merges a set of aliases for a Model version.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_merge_version_aliases():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[MergeVersionAliasesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MergeVersionAliasesRequest.html)(
name="name_value",
version_aliases=['version_aliases_value1', 'version_aliases_value2'],
)
# Make the request
response = await client.[merge_version_aliases](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_merge_version_aliases)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.MergeVersionAliases. |
`name` |
Required. The name of the model version to merge aliases, with a version ID explicitly included. Example: |
`version_aliases` |
`:class:`
Required. The set of version aliases to merge. The alias should be at most 128 characters, and match |
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
A trained machine learning Model. |

### model_evaluation_path

```
model_evaluation_path(
project: str, location: str, model: str, evaluation: str
) -> str
```


Returns a fully-qualified model_evaluation string.

### model_evaluation_slice_path

```
model_evaluation_slice_path(
project: str, location: str, model: str, evaluation: str, slice: str
) -> str
```


Returns a fully-qualified model_evaluation_slice string.

### model_path

`model_path(project: str, location: str, model: str) -> str`


Returns a fully-qualified model string.

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

### parse_endpoint_path

`parse_endpoint_path(path: str) -> typing.Dict[str, str]`


Parses a endpoint path into its component segments.

### parse_model_evaluation_path

`parse_model_evaluation_path(path: str) -> typing.Dict[str, str]`


Parses a model_evaluation path into its component segments.

### parse_model_evaluation_slice_path

`parse_model_evaluation_slice_path(path: str) -> typing.Dict[str, str]`


Parses a model_evaluation_slice path into its component segments.

### parse_model_path

`parse_model_path(path: str) -> typing.Dict[str, str]`


Parses a model path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_training_pipeline_path

`parse_training_pipeline_path(path: str) -> typing.Dict[str, str]`


Parses a training_pipeline path into its component segments.

### recommend_spec

```
recommend_spec(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.RecommendSpecRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.model_service.RecommendSpecResponse
```


Gets a Model's spec recommendations.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_recommend_spec():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RecommendSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest.html)(
parent="parent_value",
gcs_uri="gcs_uri_value",
)
# Make the request
response = await client.[recommend_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_recommend_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.RecommendSpec. |
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
Response message for ModelService.RecommendSpec. |

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

### training_pipeline_path

`training_pipeline_path(project: str, location: str, training_pipeline: str) -> str`


Returns a fully-qualified training_pipeline string.

### update_explanation_dataset

```
update_explanation_dataset(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.UpdateExplanationDatasetRequest,
dict,
]
] = None,
*,
model: typing.Optional[str] = None,
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


Incrementally update the dataset used for an examples model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_explanation_dataset():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateExplanationDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest.html)(
model="model_value",
)
# Make the request
operation = client.[update_explanation_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_update_explanation_dataset)(request=request)
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
The request object. Request message for ModelService.UpdateExplanationDataset. |
`model` |
Required. The resource name of the Model to update. Format: |
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

### update_model

```
update_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.UpdateModelRequest, dict
]
] = None,
*,
model: typing.Optional[google.cloud.aiplatform_v1beta1.types.model.Model] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.model.Model
```


Updates a Model.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelRequest.html)(
model=model,
)
# Make the request
response = await client.[update_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_update_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ModelService.UpdateModel. |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. This corresponds to the |
`update_mask` |
Required. The update mask applies to the resource. For the |
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
A trained machine learning Model. |

### upload_model

```
upload_model(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.model_service.UploadModelRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[google.cloud.aiplatform_v1beta1.types.model.Model] = None,
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


Uploads a Model artifact into Vertex AI.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upload_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest.html)(
parent="parent_value",
model=model,
)
# Make the request
operation = client.[upload_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceAsyncClient_upload_model)(request=request)
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
The request object. Request message for ModelService.UploadModel. |
`parent` |
Required. The resource name of the Location into which to upload the Model. Format: |
`model` |
Required. The Model to create. This corresponds to the |
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicefeatureregistryserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient -->

# Class FeatureRegistryServiceAsyncClient (1.134.0)

```
FeatureRegistryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for FeatureRegistry.

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
`FeatureRegistryServiceTransport` |
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

### FeatureRegistryServiceAsyncClient

```
FeatureRegistryServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature registry service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeatureRegistryServiceTransport,Callable[..., FeatureRegistryServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureRegistryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_create_features

```
batch_create_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.BatchCreateFeaturesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeatureRequest
]
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


Creates a batch of Features in a given FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_batch_create_features():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1beta1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_batch_create_features)(request=request)
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
The request object. Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures. |
`parent` |
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: |
`requests` |
`:class:`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The |
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

### create_feature

```
create_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeatureRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature.Feature
] = None,
feature_id: typing.Optional[str] = None,
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


Creates a new Feature in a given FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_create_feature)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature. |
`parent` |
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: |
`feature` |
Required. The Feature to create. This corresponds to the |
`feature_id` |
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are |
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

### create_feature_group

```
create_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureGroupRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_group: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
] = None,
feature_group_id: typing.Optional[str] = None,
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


Creates a new FeatureGroup in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[CreateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureGroupRequest.html)(
parent="parent_value",
feature_group=feature_group,
feature_group_id="feature_group_id_value",
)
# Make the request
operation = client.[create_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_create_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.CreateFeatureGroup. |
`parent` |
Required. The resource name of the Location to create FeatureGroups. Format: |
`feature_group` |
Required. The FeatureGroup to create. This corresponds to the |
`feature_group_id` |
Required. The ID to use for this FeatureGroup, which will become the final component of the FeatureGroup's resource name. This value may be up to 128 characters, and valid characters are |
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

### create_feature_monitor

```
create_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureMonitorRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
] = None,
feature_monitor_id: typing.Optional[str] = None,
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


Creates a new FeatureMonitor in a given project, location and FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest.html)(
parent="parent_value",
feature_monitor_id="feature_monitor_id_value",
)
# Make the request
operation = client.[create_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_create_feature_monitor)(request=request)
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
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][]. |
`parent` |
Required. The resource name of FeatureGroup to create FeatureMonitor. Format: |
`feature_monitor` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_id` |
Required. The ID to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name. This value may be up to 60 characters, and valid characters are |
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

### create_feature_monitor_job

```
create_feature_monitor_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.CreateFeatureMonitorJobRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_monitor_job: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
] = None,
feature_monitor_job_id: typing.Optional[int] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
```


Creates a new feature monitor job.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorJobRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[create_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_create_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][]. |
`parent` |
Required. The resource name of FeatureMonitor to create FeatureMonitorJob. Format: |
`feature_monitor_job` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_job_id` |
Optional. Output only. System-generated ID for feature monitor job. This corresponds to the |
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
Vertex AI Feature Monitor Job. |

### delete_feature

```
delete_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeatureRequest,
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


Deletes a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_delete_feature)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature. |
`name` |
Required. The name of the Features to be deleted. Format: |
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

### delete_feature_group

```
delete_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.DeleteFeatureGroupRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
force: typing.Optional[bool] = None,
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


Deletes a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_delete_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureGroup. |
`name` |
Required. The name of the FeatureGroup to be deleted. Format: |
`force` |
If set to true, any Features under this FeatureGroup will also be deleted. (Otherwise, the request will only work if the FeatureGroup has no Features.) This corresponds to the |
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

### delete_feature_monitor

```
delete_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.DeleteFeatureMonitorRequest,
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


Deletes a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_delete_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureMonitor. |
`name` |
Required. The name of the FeatureMonitor to be deleted. Format: |
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

### feature_group_path

`feature_group_path(project: str, location: str, feature_group: str) -> str`


Returns a fully-qualified feature_group string.

### feature_monitor_job_path

```
feature_monitor_job_path(
project: str,
location: str,
feature_group: str,
feature_monitor: str,
feature_monitor_job: str,
) -> str
```


Returns a fully-qualified feature_monitor_job string.

### feature_monitor_path

```
feature_monitor_path(
project: str, location: str, feature_group: str, feature_monitor: str
) -> str
```


Returns a fully-qualified feature_monitor string.

### feature_path

```
feature_path(
project: str, location: str, featurestore: str, entity_type: str, feature: str
) -> str
```


Returns a fully-qualified feature string.

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
`FeatureRegistryServiceAsyncClient` |
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
`FeatureRegistryServiceAsyncClient` |
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
`FeatureRegistryServiceAsyncClient` |
The constructed client. |

### get_feature

```
get_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetFeatureRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature.Feature
```


Gets details of a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_get_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature. |
`name` |
Required. The name of the Feature resource. Format for entity_type as parent: |
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
Feature Metadata information. For example, color is a feature that describes an apple. |

### get_feature_group

```
get_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureGroupRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
```


Gets details of a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_get_feature_group)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureRegistryService.GetFeatureGroup. |
`name` |
Required. The name of the FeatureGroup resource. This corresponds to the |
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
Vertex AI Feature Group. |

### get_feature_monitor

```
get_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureMonitorRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
```


Gets details of a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_get_feature_monitor)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitor. |
`name` |
Required. The name of the FeatureMonitor resource. This corresponds to the |
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
Vertex AI Feature Monitor. |

### get_feature_monitor_job

```
get_feature_monitor_job(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.GetFeatureMonitorJobRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.feature_monitor_job.FeatureMonitorJob
```


Get a feature monitor job.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_get_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitorJob. |
`name` |
Required. The name of the FeatureMonitorJob resource. Format: |
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
Vertex AI Feature Monitor Job. |

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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport
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

### list_feature_groups

```
list_feature_groups(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager
)
```


Lists FeatureGroups in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_feature_groups():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureGroupsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_groups](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_list_feature_groups)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureGroups. |
`parent` |
Required. The resource name of the Location to list FeatureGroups. Format: |
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
Response message for FeatureRegistryService.ListFeatureGroups. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_monitor_jobs

```
list_feature_monitor_jobs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsAsyncPager
)
```


List feature monitor jobs.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_feature_monitor_jobs():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitor_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_list_feature_monitor_jobs)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitorJobs. |
`parent` |
Required. The resource name of the FeatureMonitor to list FeatureMonitorJobs. Format: |
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
Response message for FeatureRegistryService.ListFeatureMonitorJobs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_monitors

```
list_feature_monitors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsAsyncPager
)
```


Lists FeatureGroups in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_feature_monitors():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_list_feature_monitors)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitors. |
`parent` |
Required. The resource name of the FeatureGroup to list FeatureMonitors. Format: |
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
Response message for FeatureRegistryService.ListFeatureMonitors. Iterating over this object will yield results and resolve additional pages automatically. |

### list_features

```
list_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
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
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesAsyncPager
)
```


Lists Features in a given FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_features():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_list_features)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures. |
`parent` |
Required. The resource name of the Location to list Features. Format for entity_type as parent: |
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
Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_feature_group_path

`parse_feature_group_path(path: str) -> typing.Dict[str, str]`


Parses a feature_group path into its component segments.

### parse_feature_monitor_job_path

`parse_feature_monitor_job_path(path: str) -> typing.Dict[str, str]`


Parses a feature_monitor_job path into its component segments.

### parse_feature_monitor_path

`parse_feature_monitor_path(path: str) -> typing.Dict[str, str]`


Parses a feature_monitor path into its component segments.

### parse_feature_path

`parse_feature_path(path: str) -> typing.Dict[str, str]`


Parses a feature path into its component segments.

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

### update_feature

```
update_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateFeatureRequest,
dict,
]
] = None,
*,
feature: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature.Feature
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


Updates the parameters of a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest.html)(
)
# Make the request
operation = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_update_feature)(request=request)
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
The request object. Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature. |
`feature` |
Required. The Feature's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

### update_feature_group

```
update_feature_group(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.UpdateFeatureGroupRequest,
dict,
]
] = None,
*,
feature_group: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_group.FeatureGroup
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


Updates the parameters of a single FeatureGroup.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[UpdateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest.html)(
feature_group=feature_group,
)
# Make the request
operation = client.[update_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_update_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureGroup. |
`feature_group` |
Required. The FeatureGroup's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

### update_feature_monitor

```
update_feature_monitor(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.UpdateFeatureMonitorRequest,
dict,
]
] = None,
*,
feature_monitor: typing.Optional[
google.cloud.aiplatform_v1beta1.types.feature_monitor.FeatureMonitor
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


Updates the parameters of a single FeatureMonitor.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest.html)(
)
# Make the request
operation = client.[update_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceAsyncClient_update_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureMonitor. |
`feature_monitor` |
Required. The FeatureMonitor's |
`update_mask` |
Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
