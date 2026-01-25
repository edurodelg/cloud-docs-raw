---
merged_at: 2026-01-25T21:47:44.337626
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatfo_cd009c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatfor_2830c1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatform_212fb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatform__e8f580.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatform_v_8457b6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatform_v1_a72ab5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdirectrawpredictresponse_googlecloudaiplatform_v1b_8a0df6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdirectrawpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectRawPredictResponse -->

# Class DirectRawPredictResponse (1.134.0)

`DirectRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### DirectRawPredictResponse

`DirectRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectRawPredict.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploymodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelResponse -->

# Class DeployModelResponse (1.134.0)

`DeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.DeployModel.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_model` |
The DeployedModel that had been deployed in the Endpoint. |

## Methods

### DeployModelResponse

`DeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.DeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringjobexecutiondetail.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringJobExecutionDetail -->

# Class ModelMonitoringJobExecutionDetail (1.134.0)

```
ModelMonitoringJobExecutionDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represent the execution details of the job.

## Attributes |
|
|---|---|
Name |
Description |
`baseline_datasets` |
`MutableSequence[`
Processed baseline datasets. |
`target_datasets` |
`MutableSequence[`
Processed target datasets. |
`objective_status` |
`MutableMapping[str, google.rpc.status_pb2.Status]`
Status of data processing for each monitoring objective. Key is the objective. |
`error` |
`google.rpc.status_pb2.Status`
Additional job error status. |

## Classes

### ObjectiveStatusEntry

`ObjectiveStatusEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ProcessedDataset

`ProcessedDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Processed dataset information.

## Methods

### ModelMonitoringJobExecutionDetail

```
ModelMonitoringJobExecutionDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represent the execution details of the job.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolphishblockthreshold_googlecloudaiplatform_v1be_3af77b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolphishblockthreshold.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.PhishBlockThreshold -->

# Class PhishBlockThreshold (1.134.0)

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Enums |
|
|---|---|
Name |
Description |
`PHISH_BLOCK_THRESHOLD_UNSPECIFIED` |
Defaults to unspecified. |
`BLOCK_LOW_AND_ABOVE` |
Blocks Low and above confidence URL that is risky. |
`BLOCK_MEDIUM_AND_ABOVE` |
Blocks Medium and above confidence URL that is risky. |
`BLOCK_HIGH_AND_ABOVE` |
Blocks High and above confidence URL that is risky. |
`BLOCK_HIGHER_AND_ABOVE` |
Blocks Higher and above confidence URL that is risky. |
`BLOCK_VERY_HIGH_AND_ABOVE` |
Blocks Very high and above confidence URL that is risky. |
`BLOCK_ONLY_EXTREMELY_HIGH` |
Blocks Extremely high confidence URL that is risky. |

## Methods

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeseventmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EventMetadata -->

# Class EventMetadata (1.134.0)

`EventMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata relating to a LLM response event.

## Attributes |
|
|---|---|
Name |
Description |
`grounding_metadata` |
Optional. Metadata returned to client when grounding is enabled. |
`partial` |
`bool`
Optional. Indicates whether the text content is part of a unfinished text stream. Only used for streaming mode and when the content is plain text. |
`turn_complete` |
`bool`
Optional. Indicates whether the response from the model is complete. Only used for streaming mode. |
`interrupted` |
`bool`
Optional. Flag indicating that LLM was interrupted when generating the content. Usually it's due to user interruption during a bidi streaming. |
`long_running_tool_ids` |
`MutableSequence[str]`
Optional. Set of ids of the long running function calls. Agent client will know from this field about which function call is long running. Only valid for function call event. |
`branch` |
`str`
Optional. The branch of the event. The format is like agent_1.agent_2.agent_3, where agent_1 is the parent of agent_2, and agent_2 is the parent of agent_3. Branch is used when multiple child agents shouldn't see their siblings' conversation history. |
`custom_metadata` |
`google.protobuf.struct_pb2.Struct`
The custom metadata of the LlmResponse. |

## Methods

### EventMetadata

`EventMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata relating to a LLM response event.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchfeaturesrequest___googlecloudaiplatform_396b05.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchfeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesRequest -->

# Class SearchFeaturesRequest (1.134.0)

`SearchFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.SearchFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`location` |
`str`
Required. The resource name of the Location to search Features. Format: `projects/{project}/locations/{location}`
|
`query` |
`str`
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using `AND` to form a
conjunction.
A field query is in the form FIELD:QUERY. This implicitly
checks if QUERY exists as a substring within Feature's
FIELD. The QUERY and the FIELD are converted to a sequence
of words (i.e. tokens) for comparison. This is done by:
- Removing leading/trailing whitespace and tokenizing the
search value. Characters that are not one of alphanumeric
`[a-zA-Z0-9]` , underscore `_` , or asterisk `*` are
treated as delimiters for tokens. `*` is treated as a
wildcard that matches characters within a token.
- Ignoring case.
- Prepending an asterisk to the first and appending an
asterisk to the last token in QUERY.
A QUERY must be either a singular token or a phrase. A
phrase is one or multiple words enclosed in double quotation
marks ("). With phrases, the order of the words is
important. Words in the phrase must be matching in order and
consecutively.
Supported FIELDs for field-restricted queries:
- `feature_id`
- `description`
- `entity_type_id`
Examples:
- `feature_id: foo` --> Matches a Feature with ID
containing the substring `foo` (eg. `foo` ,
`foofeature` , `barfoo` ).
- `feature_id: foo*feature` --> Matches a Feature with ID
containing the substring `foo*feature` (eg.
`foobarfeature` ).
- `feature_id: foo AND description: bar` --> Matches a
Feature with ID containing the substring `foo` and
description containing the substring `bar` .
Besides field queries, the following exact-match filters are
supported. The exact-match filters do not support wildcards.
Unlike field-restricted queries, exact-match filters are
case-sensitive.
- `feature_id` : Supports = comparisons.
- `description` : Supports = comparisons. Multi-token
filters should be enclosed in quotes.
- `entity_type_id` : Supports = comparisons.
- `value_type` : Supports = and != comparisons.
- `labels` : Supports key-value equality as well as key
presence.
- `featurestore_id` : Supports = comparisons.
Examples:
- `description = "foo bar"` --> Any Feature with
description exactly equal to `foo bar`
- `value_type = DOUBLE` --> Features whose type is DOUBLE.
- `labels.active = yes AND labels.env = prod` --> Features
having both (active: yes) and (env: prod) labels.
- `labels.env: *` --> Any Feature which has a label with
`env` as the key.
|
`page_size` |
`int`
The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 100 Features will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.SearchFeatures call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.SearchFeatures, except `page_size` , must match the call that provided the
page token.
|

## Methods

### SearchFeaturesRequest

`SearchFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.SearchFeatures.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetstudyrequest_googlecloudaiplatform_v1typesdepl_088d3d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetstudyrequest_googlecloudaiplatform_v1typesdeplo_d5bec1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetstudyrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest -->

# Class GetStudyRequest (1.134.0)

`GetStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetStudy.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Study resource. Format: `projects/{project}/locations/{location}/studies/{study}`
|

## Methods

### GetStudyRequest

`GetStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetStudy.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedmodelref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModelRef -->

# Class DeployedModelRef (1.134.0)

`DeployedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Immutable. A resource name of an Endpoint. |
`deployed_model_id` |
`str`
Immutable. An ID of a DeployedModel in the above Endpoint. |

## Methods

### DeployedModelRef

`DeployedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedModel.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescorpusstatus_googlecloudaiplatform_v1beta1typesdir_fdead5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescorpusstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorpusStatus -->

# Class CorpusStatus (1.134.0)

`CorpusStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RagCorpus status.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Output only. RagCorpus life state. |
`error_status` |
`str`
Output only. Only when the `state` field is ERROR.
|

## Classes

### State

`State(value)`


RagCorpus life state.

## Methods

### CorpusStatus

`CorpusStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RagCorpus status.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdirectrawpredictresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictResponse -->

# Class DirectRawPredictResponse (1.134.0)

`DirectRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectRawPredict.

## Attribute |
|
|---|---|
Name |
Description |
`output` |
`bytes`
The prediction output. |

## Methods

### DirectRawPredictResponse

`DirectRawPredictResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for PredictionService.DirectRawPredict.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexplanationmetadata__googlecloudaiplatform_v1type_bf5644.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadata__googlecloudaiplatform_v1types_fcabd4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata -->

# Class ExplanationMetadata (1.134.0)

`ExplanationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describing the Model's input and output for explanation.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
`MutableMapping[str, `
Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature. An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in ExplanationMetadata.inputs. The baseline of the empty feature is chosen by Vertex AI. For Vertex AI-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, featureAttributions are keyed by this key (if not grouped with another feature). For custom images, the key must match with the key in instance. |
`outputs` |
`MutableMapping[str, `
Required. Map from output names to output metadata. For Vertex AI-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters. For custom images, keys are the name of the output field in the prediction to be explained. Currently only one key is allowed. |
`feature_attributions_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing the format of the [feature attributions][google.cloud.aiplatform.v1.Attribution.feature_attributions]. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`latent_space_source` |
`str`
Name of the source to generate embeddings for example based explanations. |

## Classes

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

### InputsEntry

`InputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### OutputMetadata

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OutputsEntry

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ExplanationMetadata

`ExplanationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describing the Model's input and output for explanation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistnasjobsrequest__googlecloudaiplatform_v1typess_6f7f78.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistnasjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsRequest -->

# Class ListNasJobsRequest (1.134.0)

`ListNasJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the NasJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListNasJobsResponse.next_page_token of the previous JobService.ListNasJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListNasJobsRequest

`ListNasJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasJobs.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessyntheticfield_googlecloudaiplatform_v1beta1typesg_502a0a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessyntheticfield.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyntheticField -->

# Class SyntheticField (1.134.0)

`SyntheticField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single named field within a SyntheticExample.

## Attributes |
|
|---|---|
Name |
Description |
`field_name` |
`str`
Optional. The name of the field. |
`content` |
Required. The content of the field. |

## Methods

### SyntheticField

`SyntheticField(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a single named field within a SyntheticExample.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetfeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeaturestoreRequest -->

# Class GetFeaturestoreRequest (1.134.0)

`GetFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeaturestore.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Featurestore resource. |

## Methods

### GetFeaturestoreRequest

`GetFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputs__googlecloudai_be2c85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputs__googlecloudaip_7539f5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskrerunconfiginputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskRerunConfig.Inputs -->

# Class Inputs (1.134.0)

`Inputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime inputs data of the task.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableMapping[str, `
Optional. Input artifacts. |
`parameter_values` |
`MutableMapping[str, google.protobuf.struct_pb2.Value]`
Optional. Input parameters. |

## Classes

### ArtifactsEntry

`ArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParameterValuesEntry

`ParameterValuesEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### Inputs

`Inputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime inputs data of the task.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescorpusstatus_googlecloudaiplatform_v1typesdep_4caa8e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescorpusstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorpusStatus -->

# Class CorpusStatus (1.134.0)

`CorpusStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RagCorpus status.

## Attributes |
|
|---|---|
Name |
Description |
`state` |
Output only. RagCorpus life state. |
`error_status` |
`str`
Output only. Only when the `state` field is ERROR.
|

## Classes

### State

`State(value)`


RagCorpus life state.

## Methods

### CorpusStatus

`CorpusStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


RagCorpus status.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployindexresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexResponse -->

# Class DeployIndexResponse (1.134.0)

`DeployIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.DeployIndex.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_index` |
The DeployedIndex that had been deployed in the IndexEndpoint. |

## Methods

### DeployIndexResponse

`DeployIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.DeployIndex.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetindexrequest_googlecloudaiplatform_v1typesstru_f008f8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetindexrequest_googlecloudaiplatform_v1typesstruc_2787a1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexRequest -->

# Class GetIndexRequest (1.134.0)

`GetIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.GetIndex

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Index resource. Format: `projects/{project}/locations/{location}/indexes/{index}`
|

## Methods

### GetIndexRequest

`GetIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.GetIndex


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstructfieldvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StructFieldValue -->

# Class StructFieldValue (1.134.0)

`StructFieldValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One field of a Struct (or object) type feature value.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Name of the field in the struct feature. |
`value` |
The value for this field. |

## Methods

### StructFieldValue

`StructFieldValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One field of a Struct (or object) type feature value.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeploymodelresponse_googlecloudaiplatform_v1beta1t_765a2b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeploymodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelResponse -->

# Class DeployModelResponse (1.134.0)

`DeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.DeployModel.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_model` |
The DeployedModel that had been deployed in the Endpoint. |

## Methods

### DeployModelResponse

`DeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.DeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesurlmetadataurlretrievalstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlMetadata.UrlRetrievalStatus -->

# Class UrlRetrievalStatus (1.134.0)

`UrlRetrievalStatus(value)`


Status of the url retrieval.

## Enums |
|
|---|---|
Name |
Description |
`URL_RETRIEVAL_STATUS_UNSPECIFIED` |
Default value. This value is unused. |
`URL_RETRIEVAL_STATUS_SUCCESS` |
Url retrieval is successful. |
`URL_RETRIEVAL_STATUS_ERROR` |
Url retrieval is failed due to error. |

## Methods

### UrlRetrievalStatus

`UrlRetrievalStatus(value)`


Status of the url retrieval.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesexplanationmetadata___googlecloudaiplatform_7a8e9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexplanationmetadata___googlecloudaiplatform__8bc0e9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplanationmetadata___googlecloudaiplatform_v_c83434.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata -->

# Class ExplanationMetadata (1.134.0)

`ExplanationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describing the Model's input and output for explanation.

## Attributes |
|
|---|---|
Name |
Description |
`inputs` |
`MutableMapping[str, `
Required. Map from feature names to feature input metadata. Keys are the name of the features. Values are the specification of the feature. An empty InputMetadata is valid. It describes a text feature which has the name specified as the key in ExplanationMetadata.inputs. The baseline of the empty feature is chosen by Vertex AI. For Vertex AI-provided Tensorflow images, the key can be any friendly name of the feature. Once specified, featureAttributions are keyed by this key (if not grouped with another feature). For custom images, the key must match with the key in instance. |
`outputs` |
`MutableMapping[str, `
Required. Map from output names to output metadata. For Vertex AI-provided Tensorflow images, keys can be any user defined string that consists of any UTF-8 characters. For custom images, keys are the name of the output field in the prediction to be explained. Currently only one key is allowed. |
`feature_attributions_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing the format of the [feature attributions][google.cloud.aiplatform.v1beta1.Attribution.feature_attributions]. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`latent_space_source` |
`str`
Name of the source to generate embeddings for example based explanations. |

## Classes

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

### InputsEntry

`InputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### OutputMetadata

`OutputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the prediction output to be explained.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OutputsEntry

`OutputsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ExplanationMetadata

`ExplanationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata describing the Model's input and output for explanation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespublishermodelversionstate_googlecloudaiplatform__d5de71.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespublishermodelversionstate_googlecloudaiplatform_v_35c077.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespublishermodelversionstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PublisherModel.VersionState -->

# Class VersionState (1.134.0)

`VersionState(value)`


An enum representing the state of the PublicModelVersion.

## Enums |
|
|---|---|
Name |
Description |
`VERSION_STATE_UNSPECIFIED` |
The version state is unspecified. |
`VERSION_STATE_STABLE` |
Used to indicate the version is stable. |
`VERSION_STATE_UNSTABLE` |
Used to indicate the version is unstable. |

## Methods

### VersionState

`VersionState(value)`


An enum representing the state of the PublicModelVersion.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetstudyrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetStudyRequest -->

# Class GetStudyRequest (1.134.0)

`GetStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetStudy.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Study resource. Format: `projects/{project}/locations/{location}/studies/{study}`
|

## Methods

### GetStudyRequest

`GetStudyRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.GetStudy.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types -->

# Package params_v1.types (1.134.0)

API documentation for `params_v1.types`

package.

## Classes

[ImageClassificationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageClassificationPredictionParams)

Prediction model parameters for Image Classification.

[ImageObjectDetectionPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageObjectDetectionPredictionParams)

Prediction model parameters for Image Object Detection.

[ImageSegmentationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.ImageSegmentationPredictionParams)

Prediction model parameters for Image Segmentation.

[VideoActionRecognitionPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoActionRecognitionPredictionParams)

Prediction model parameters for Video Action Recognition.

[VideoClassificationPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoClassificationPredictionParams)

Prediction model parameters for Video Classification.

[VideoObjectTrackingPredictionParams](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoObjectTrackingPredictionParams)

Prediction model parameters for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistnasjobsrequest__googlecloudaiplatform_v1_fc6a5e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistnasjobsrequest__googlecloudaiplatform_v1b_8c1453.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnasjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasJobsRequest -->

# Class ListNasJobsRequest (1.134.0)

`ListNasJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the NasJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. Supported fields: - `display_name` supports `=` , `!=` comparisons, and
`:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `create_time` supports `=` , `!=` ,\ ,
`<>` ,\ `>` , `>=` comparisons. `create_time` must
be in RFC 3339 format.
- `labels` supports general map functions that is:
`labels.key=value` - key:value equality \`labels.key:\*
- key existence
Some examples of using the filter are:
- `state="JOB_STATE_SUCCEEDED" AND display_name:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR display_name="my_job"`
- `NOT display_name="my_job"`
- `create_time>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListNasJobsResponse.next_page_token of the previous JobService.ListNasJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListNasJobsRequest

`ListNasJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListNasJobs.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesretrievecontextsresponse_googlecloudaiplatfor_ad6d7f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievecontextsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsResponse -->

# Class RetrieveContextsResponse (1.134.0)

`RetrieveContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagService.RetrieveContexts.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
The contexts of the query. |

## Methods

### RetrieveContextsResponse

`RetrieveContextsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagService.RetrieveContexts.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreadtensorboardusageresponseperuserusagedata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadTensorboardUsageResponse.PerUserUsageData -->

# Class PerUserUsageData (1.134.0)

`PerUserUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per user usage data.

## Attributes |
|
|---|---|
Name |
Description |
`username` |
`str`
User's username |
`view_count` |
`int`
Number of times the user has read data within the Tensorboard. |

## Methods

### PerUserUsageData

`PerUserUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per user usage data.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Featurestore -->

# Class Featurestore (1.134.0)

`Featurestore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Featurestore. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Featurestore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Featurestore was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Featurestore. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one Featurestore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`online_serving_config` |
Optional. Config for online storage resources. The field should not co-exist with the field of `OnlineStoreReplicationConfig` . If both of it and
OnlineStoreReplicationConfig are unset, the feature store
will not have an online store and cannot be used for online
serving.
|
`state` |
Output only. State of the featurestore. |
`online_storage_ttl_days` |
`int`
Optional. TTL in days for feature values that will be stored in online serving storage. The Feature Store online storage periodically removes obsolete feature values older than `online_storage_ttl_days` since the feature generation
time. Note that `online_storage_ttl_days` should be less
than or equal to `offline_storage_ttl_days` for each
EntityType under a featurestore. If not set, default to 4000
days
|
`encryption_spec` |
Optional. Customer-managed encryption key spec for data storage. If set, both of the online and offline data storage will be secured by this key. |
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

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

### State

`State(value)`


Possible states a featurestore can have.

## Methods

### Featurestore

`Featurestore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesmetadatastoredataplexconfig_googlecloudaiplatfo_d0e1bd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmetadatastoredataplexconfig_googlecloudaiplatfor_cc8adb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmetadatastoredataplexconfig_googlecloudaiplatform_81b5a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetadatastoredataplexconfig_googlecloudaiplatform__e1e439.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetadatastoredataplexconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataStore.DataplexConfig -->

# Class DataplexConfig (1.134.0)

`DataplexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents Dataplex integration settings.

## Attribute |
|
|---|---|
Name |
Description |
`enabled_pipelines_lineage` |
`bool`
Optional. Whether or not Data Lineage synchronization is enabled for Vertex Pipelines. |

## Methods

### DataplexConfig

`DataplexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents Dataplex integration settings.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployindexresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexResponse -->

# Class DeployIndexResponse (1.134.0)

`DeployIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.DeployIndex.

## Attribute |
|
|---|---|
Name |
Description |
`deployed_index` |
The DeployedIndex that had been deployed in the IndexEndpoint. |

## Methods

### DeployIndexResponse

`DeployIndexResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.DeployIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesuploadragfileresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadRagFileResponse -->

# Class UploadRagFileResponse (1.134.0)

`UploadRagFileResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.UploadRagFile.

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
`rag_file` |
The RagFile that had been uploaded into the RagCorpus. This field is a member of `oneof` _ `result` .
|
`error` |
`google.rpc.status_pb2.Status`
The error that occurred while processing the RagFile. This field is a member of `oneof` _ `result` .
|

## Methods

### UploadRagFileResponse

`UploadRagFileResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.UploadRagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore -->

# Class Featurestore (1.134.0)

`Featurestore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Featurestore. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Featurestore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Featurestore was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Featurestore. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one Featurestore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`online_serving_config` |
Optional. Config for online storage resources. The field should not co-exist with the field of `OnlineStoreReplicationConfig` . If both of it and
OnlineStoreReplicationConfig are unset, the feature store
will not have an online store and cannot be used for online
serving.
|
`state` |
Output only. State of the featurestore. |
`online_storage_ttl_days` |
`int`
Optional. TTL in days for feature values that will be stored in online serving storage. The Feature Store online storage periodically removes obsolete feature values older than `online_storage_ttl_days` since the feature generation
time. Note that `online_storage_ttl_days` should be less
than or equal to `offline_storage_ttl_days` for each
EntityType under a featurestore. If not set, default to 4000
days
|
`encryption_spec` |
Optional. Customer-managed encryption key spec for data storage. If set, both of the online and offline data storage will be secured by this key. |
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

### OnlineServingConfig

`OnlineServingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


OnlineServingConfig specifies the details for provisioning online serving resources.

### State

`State(value)`


Possible states a featurestore can have.

## Methods

### Featurestore

`Featurestore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeaturerequest__googlecloudaiplatform__ebf019.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeaturerequest__googlecloudaiplatform_v_4564cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest -->

# Class UpdateFeatureRequest (1.134.0)

`UpdateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`feature` |
Required. The Feature's `name` field is used to identify
the Feature to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all fields.
Updatable fields:
- `description`
- `labels`
- `disable_monitoring` (Not supported for
FeatureRegistryService Feature)
- `point_of_contact` (Not supported for
FeaturestoreService FeatureStore)
|

## Methods

### UpdateFeatureRequest

`UpdateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratememoriesrequestdirectmemoriessourcedi_e5aa64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratememoriesrequestdirectmemoriessourcedirectmemory.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.DirectMemoriesSource.DirectMemory -->

# Class DirectMemory (1.134.0)

`DirectMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A direct memory to upload to Memory Bank.

## Attribute |
|
|---|---|
Name |
Description |
`fact` |
`str`
Required. The fact to consolidate with existing memories. |

## Methods

### DirectMemory

`DirectMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A direct memory to upload to Memory Bank.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontentsexampleexpectedcontent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentsExample.ExpectedContent -->

# Class ExpectedContent (1.134.0)

`ExpectedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single step of the expected output.

## Attribute |
|
|---|---|
Name |
Description |
`content` |
`google.cloud.aiplatform_v1beta1.types.Content`
Required. A single step's content. |

## Methods

### ExpectedContent

`ExpectedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single step of the expected output.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesspecialist_pool_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.specialist_pool_service.pagers`

module.

## Classes

[ListSpecialistPoolsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager)

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSpecialistPoolsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsPager)

```
ListSpecialistPoolsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
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


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse) object, and
provides an `__iter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicefeatureonlinestoreadminserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient -->

# Class FeatureOnlineStoreAdminServiceClient (1.134.0)

```
FeatureOnlineStoreAdminServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for FeatureOnlineStore.

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
`FeatureOnlineStoreAdminServiceTransport` |
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

### FeatureOnlineStoreAdminServiceClient

```
FeatureOnlineStoreAdminServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.transports.base.FeatureOnlineStoreAdminServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature online store admin service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeatureOnlineStoreAdminServiceTransport,Callable[..., FeatureOnlineStoreAdminServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureOnlineStoreAdminServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_feature_online_store

```
create_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.CreateFeatureOnlineStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_online_store: typing.Optional[
google.cloud.aiplatform_v1.types.feature_online_store.FeatureOnlineStore
] = None,
feature_online_store_id: typing.Optional[str] = None,
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


Creates a new FeatureOnlineStore in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_feature_online_store():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_online_store = aiplatform_v1.[FeatureOnlineStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.html)()
feature_online_store.bigtable.auto_scaling.min_node_count = 1489
feature_online_store.bigtable.auto_scaling.max_node_count = 1491
request = aiplatform_v1.[CreateFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureOnlineStoreRequest.html)(
parent="parent_value",
feature_online_store=feature_online_store,
feature_online_store_id="feature_online_store_id_value",
)
# Make the request
operation = client.[create_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_create_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.CreateFeatureOnlineStore. |
`parent` |
`str`
Required. The resource name of the Location to create FeatureOnlineStores. Format: |
`feature_online_store` |
Required. The FeatureOnlineStore to create. This corresponds to the |
`feature_online_store_id` |
`str`
Required. The ID to use for this FeatureOnlineStore, which will become the final component of the FeatureOnlineStore's resource name. This value may be up to 60 characters, and valid characters are |
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

### create_feature_view

```
create_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.CreateFeatureViewRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_view: typing.Optional[
google.cloud.aiplatform_v1.types.feature_view.FeatureView
] = None,
feature_view_id: typing.Optional[str] = None,
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


Creates a new FeatureView in a given FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_feature_view():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_view = aiplatform_v1.[FeatureView](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.html)()
feature_view.big_query_source.uri = "uri_value"
feature_view.big_query_source.entity_id_columns = ['entity_id_columns_value1', 'entity_id_columns_value2']
request = aiplatform_v1.[CreateFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureViewRequest.html)(
parent="parent_value",
feature_view=feature_view,
feature_view_id="feature_view_id_value",
)
# Make the request
operation = client.[create_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_create_feature_view)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.CreateFeatureView. |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to create FeatureViews. Format: |
`feature_view` |
Required. The FeatureView to create. This corresponds to the |
`feature_view_id` |
`str`
Required. The ID to use for the FeatureView, which will become the final component of the FeatureView's resource name. This value may be up to 60 characters, and valid characters are |
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

### delete_feature_online_store

```
delete_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.DeleteFeatureOnlineStoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
force: typing.Optional[bool] = None,
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


Deletes a single FeatureOnlineStore. The FeatureOnlineStore must not contain any FeatureViews.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature_online_store():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureOnlineStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_delete_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore. |
`name` |
`str`
Required. The name of the FeatureOnlineStore to be deleted. Format: |
`force` |
`bool`
If set to true, any FeatureViews and Features for this FeatureOnlineStore will also be deleted. (Otherwise, the request will only work if the FeatureOnlineStore has no FeatureViews.) This corresponds to the |
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

### delete_feature_view

```
delete_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.DeleteFeatureViewRequest,
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


Deletes a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature_view():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureViewRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_delete_feature_view)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.DeleteFeatureView. |
`name` |
`str`
Required. The name of the FeatureView to be deleted. Format: |
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

### feature_online_store_path

```
feature_online_store_path(
project: str, location: str, feature_online_store: str
) -> str
```


Returns a fully-qualified feature_online_store string.

### feature_view_path

```
feature_view_path(
project: str, location: str, feature_online_store: str, feature_view: str
) -> str
```


Returns a fully-qualified feature_view string.

### feature_view_sync_path

```
feature_view_sync_path(
project: str, location: str, feature_online_store: str, feature_view: str
) -> str
```


Returns a fully-qualified feature_view_sync string.

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
`FeatureOnlineStoreAdminServiceClient` |
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
`FeatureOnlineStoreAdminServiceClient` |
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
`FeatureOnlineStoreAdminServiceClient` |
The constructed client. |

### get_feature_online_store

```
get_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.GetFeatureOnlineStoreRequest,
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
) -> google.cloud.aiplatform_v1.types.feature_online_store.FeatureOnlineStore
```


Gets details of a single FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_feature_online_store():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureOnlineStoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_online_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureOnlineStore. |
`name` |
`str`
Required. The name of the FeatureOnlineStore resource. This corresponds to the |
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
Vertex AI Feature Online Store provides a centralized repository for serving ML features and embedding indexes at low latency. The Feature Online Store is a top-level container. |

### get_feature_view

```
get_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.GetFeatureViewRequest,
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
) -> google.cloud.aiplatform_v1.types.feature_view.FeatureView
```


Gets details of a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_feature_view():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_view)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureView. |
`name` |
`str`
Required. The name of the FeatureView resource. Format: |
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
FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig. |

### get_feature_view_sync

```
get_feature_view_sync(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.GetFeatureViewSyncRequest,
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
) -> google.cloud.aiplatform_v1.types.feature_view_sync.FeatureViewSync
```


Gets details of a single FeatureViewSync.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_feature_view_sync():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureViewSyncRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewSyncRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_view_sync](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_get_feature_view_sync)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync. |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: |
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
FeatureViewSync is a representation of sync operation which copies data from data source to Feature View in Online Store. |

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

### list_feature_online_stores

```
list_feature_online_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
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
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager
)
```


Lists FeatureOnlineStores in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_feature_online_stores():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeatureOnlineStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_online_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_online_stores)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores. |
`parent` |
`str`
Required. The resource name of the Location to list FeatureOnlineStores. Format: |
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
Response message for FeatureOnlineStoreAdminService.ListFeatureOnlineStores. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_view_syncs

```
list_feature_view_syncs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
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
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager
)
```


Lists FeatureViewSyncs in a given FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_feature_view_syncs():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeatureViewSyncsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_view_syncs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_view_syncs)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs. |
`parent` |
`str`
Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: |
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
Response message for FeatureOnlineStoreAdminService.ListFeatureViewSyncs. Iterating over this object will yield results and resolve additional pages automatically. |

### list_feature_views

```
list_feature_views(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
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
google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager
)
```


Lists FeatureViews in a given FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_feature_views():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeatureViewsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_views](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_list_feature_views)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.ListFeatureViews. |
`parent` |
`str`
Required. The resource name of the FeatureOnlineStore to list FeatureViews. Format: |
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
Response message for FeatureOnlineStoreAdminService.ListFeatureViews. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_feature_online_store_path

`parse_feature_online_store_path(path: str) -> typing.Dict[str, str]`


Parses a feature_online_store path into its component segments.

### parse_feature_view_path

`parse_feature_view_path(path: str) -> typing.Dict[str, str]`


Parses a feature_view path into its component segments.

### parse_feature_view_sync_path

`parse_feature_view_sync_path(path: str) -> typing.Dict[str, str]`


Parses a feature_view_sync path into its component segments.

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

### sync_feature_view

```
sync_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.SyncFeatureViewRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.SyncFeatureViewResponse
)
```


Triggers on-demand sync for the FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_sync_feature_view():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SyncFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SyncFeatureViewRequest.html)(
feature_view="feature_view_value",
)
# Make the request
response = client.[sync_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_sync_feature_view)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureOnlineStoreAdminService.SyncFeatureView. |
`feature_view` |
`str`
Required. Format: |
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
Response message for FeatureOnlineStoreAdminService.SyncFeatureView. |

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

### update_feature_online_store

```
update_feature_online_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.UpdateFeatureOnlineStoreRequest,
dict,
]
] = None,
*,
feature_online_store: typing.Optional[
google.cloud.aiplatform_v1.types.feature_online_store.FeatureOnlineStore
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


Updates the parameters of a single FeatureOnlineStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_feature_online_store():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_online_store = aiplatform_v1.[FeatureOnlineStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.html)()
feature_online_store.bigtable.auto_scaling.min_node_count = 1489
feature_online_store.bigtable.auto_scaling.max_node_count = 1491
request = aiplatform_v1.[UpdateFeatureOnlineStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureOnlineStoreRequest.html)(
feature_online_store=feature_online_store,
)
# Make the request
operation = client.[update_feature_online_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_update_feature_online_store)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.UpdateFeatureOnlineStore. |
`feature_online_store` |
Required. The FeatureOnlineStore's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureOnlineStore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

### update_feature_view

```
update_feature_view(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.UpdateFeatureViewRequest,
dict,
]
] = None,
*,
feature_view: typing.Optional[
google.cloud.aiplatform_v1.types.feature_view.FeatureView
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


Updates the parameters of a single FeatureView.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_feature_view():
# Create a client
client = aiplatform_v1.
```[FeatureOnlineStoreAdminServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html)()
# Initialize request argument(s)
feature_view = aiplatform_v1.[FeatureView](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.html)()
feature_view.big_query_source.uri = "uri_value"
feature_view.big_query_source.entity_id_columns = ['entity_id_columns_value1', 'entity_id_columns_value2']
request = aiplatform_v1.[UpdateFeatureViewRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureViewRequest.html)(
feature_view=feature_view,
)
# Make the request
operation = client.[update_feature_view](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.FeatureOnlineStoreAdminServiceClient.html#google_cloud_aiplatform_v1_services_feature_online_store_admin_service_FeatureOnlineStoreAdminServiceClient_update_feature_view)(request=request)
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
The request object. Request message for FeatureOnlineStoreAdminService.UpdateFeatureView. |
`feature_view` |
Required. The FeatureView's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureView resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googleclouda_a2a3bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googlecloudai_269c62.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googlecloudaip_3f24c7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googlecloudaipl_e2c108.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googlecloudaipla_76fa85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest_googlecloudaiplat_bb33e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisttensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesRequest -->

# Class ListTensorboardTimeSeriesRequest (1.134.0)

```
ListTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardRun to list TensorboardTimeSeries. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`filter` |
`str`
Lists the TensorboardTimeSeries that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardTimeSeries to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardTimeSeries are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardTimeSeries call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardTimeSeries must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardTimeSeriesRequest

```
ListTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.ListTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest -->

# Class ListModelsRequest (1.134.0)

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the Models from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `model` supports = and !=. `model` represents the
Model ID, i.e. the last segment of the Model's [resource
name][google.cloud.aiplatform.v1beta1.Model.name].
- `display_name` supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `base_model_name` only supports =
Some examples:
- `model=1234`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `baseModelName="text-bison"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelsResponse.next_page_token of the previous ModelService.ListModels call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListModelsRequest

`ListModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModels.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolphishblockthreshold_googlecloudaiplatform_c425db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolphishblockthreshold.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tool.PhishBlockThreshold -->

# Class PhishBlockThreshold (1.134.0)

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)

## Enums |
|
|---|---|
Name |
Description |
`PHISH_BLOCK_THRESHOLD_UNSPECIFIED` |
Defaults to unspecified. |
`BLOCK_LOW_AND_ABOVE` |
Blocks Low and above confidence URL that is risky. |
`BLOCK_MEDIUM_AND_ABOVE` |
Blocks Medium and above confidence URL that is risky. |
`BLOCK_HIGH_AND_ABOVE` |
Blocks High and above confidence URL that is risky. |
`BLOCK_HIGHER_AND_ABOVE` |
Blocks Higher and above confidence URL that is risky. |
`BLOCK_VERY_HIGH_AND_ABOVE` |
Blocks Very high and above confidence URL that is risky. |
`BLOCK_ONLY_EXTREMELY_HIGH` |
Blocks Extremely high confidence URL that is risky. |

## Methods

### PhishBlockThreshold

`PhishBlockThreshold(value)`


These are available confidence level user can set to block
malicious urls with chosen confidence and above. For
understanding different confidence of webrisk, please refer to
[https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel](https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfileparsingconfiglayoutparser.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileParsingConfig.LayoutParser -->

# Class LayoutParser (1.134.0)

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.

## Attributes |
|
|---|---|
Name |
Description |
`processor_name` |
`str`
The full resource name of a Document AI processor or processor version. The processor must have type `LAYOUT_PARSER_PROCESSOR` . If specified, the
`additional_config.parse_as_scanned_pdf` field must be
false. Format:
- `projects/{project_id}/locations/{location}/processors/{processor_id}`
- `projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}`
|
`max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult https://cloud.google.com/document-ai/quotas and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM would be used. |
`global_max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the Document AI processor per minute in this project. Consult https://cloud.google.com/document-ai/quotas and the Quota page for your project to set an appropriate value here. If this value is not specified, max_parsing_requests_per_min will be used by indexing pipeline as the global limit. |

## Methods

### LayoutParser

`LayoutParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Document AI Layout Parser config.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesexactmatchinput_googlecloudaiplatform_v1typ_1b1246.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesexactmatchinput_googlecloudaiplatform_v1type_995bc5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexactmatchinput_googlecloudaiplatform_v1types_bc9265.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexactmatchinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchInput -->

# Class ExactMatchInput (1.134.0)

`ExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for exact match metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for exact match metric. |
`instances` |
`MutableSequence[`
Required. Repeated exact match instances. |

## Methods

### ExactMatchInput

`ExactMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input for exact match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreadtensorboardusageresponseperuserusagedata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadTensorboardUsageResponse.PerUserUsageData -->

# Class PerUserUsageData (1.134.0)

`PerUserUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per user usage data.

## Attributes |
|
|---|---|
Name |
Description |
`username` |
`str`
User's username |
`view_count` |
`int`
Number of times the user has read data within the Tensorboard. |

## Methods

### PerUserUsageData

`PerUserUsageData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Per user usage data.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfindneighborsresponsenearestneighbors_googlec_15c786.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfindneighborsresponsenearestneighbors.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsResponse.NearestNeighbors -->

# Class NearestNeighbors (1.134.0)

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The ID of the query datapoint. |
`neighbors` |
`MutableSequence[`
All its neighbors. |

## Methods

### NearestNeighbors

`NearestNeighbors(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Nearest neighbors for one query.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesapiauthapikeyconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ApiAuth.ApiKeyConfig -->

# Class ApiKeyConfig (1.134.0)

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.

## Attribute |
|
|---|---|
Name |
Description |
`api_key_secret_version` |
`str`
Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version} |

## Methods

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgetnasjobrequest_googlecloudaiplatform_v1beta1typ_677f53.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgetnasjobrequest_googlecloudaiplatform_v1beta1type_c79076.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetnasjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNasJobRequest -->

# Class GetNasJobRequest (1.134.0)

`GetNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### GetNasJobRequest

`GetNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployedmodelref.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployedModelRef -->

# Class DeployedModelRef (1.134.0)

`DeployedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Immutable. A resource name of an Endpoint. |
`deployed_model_id` |
`str`
Immutable. An ID of a DeployedModel in the above Endpoint. |

## Methods

### DeployedModelRef

`DeployedModelRef(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Points to a DeployedModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievecontextsrequestvertexragstore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.VertexRagStore -->

# Class VertexRagStore (1.134.0)

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpora` |
`MutableSequence[str]`
Optional. Deprecated. Please use rag_resources to specify the data source. |
`rag_resources` |
`MutableSequence[`
Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support. |
`vector_distance_threshold` |
`float`
Optional. Only return contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `_vector_distance_threshold` .
|

## Classes

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Methods

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.metadata_service.pagers`

module.

## Classes

[ListArtifactsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsAsyncPager)

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
provides an `__aiter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListArtifactsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsPager)

```
ListArtifactsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsResponse,
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


A pager for iterating through `list_artifacts`

requests.

This class thinly wraps an initial
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse) object, and
provides an `__iter__`

method to iterate through its
`artifacts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListArtifacts`

requests and continue to iterate
through the `artifacts`

field on the
corresponding responses.

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListContextsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsAsyncPager)

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__aiter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListContextsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsPager)

```
ListContextsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListContextsResponse,
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


A pager for iterating through `list_contexts`

requests.

This class thinly wraps an initial
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse) object, and
provides an `__iter__`

method to iterate through its
`contexts`

field.

If there are more pages, the `__iter__`

method will make additional
`ListContexts`

requests and continue to iterate
through the `contexts`

field on the
corresponding responses.

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExecutionsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsAsyncPager)

```
ListExecutionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExecutionsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsPager)

```
ListExecutionsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsResponse,
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


A pager for iterating through `list_executions`

requests.

This class thinly wraps an initial
[ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse) object, and
provides an `__iter__`

method to iterate through its
`executions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExecutions`

requests and continue to iterate
through the `executions`

field on the
corresponding responses.

All the usual [ListExecutionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataSchemasAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasAsyncPager)

```
ListMetadataSchemasAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataSchemasPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasPager)

```
ListMetadataSchemasPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasResponse,
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


A pager for iterating through `list_metadata_schemas`

requests.

This class thinly wraps an initial
[ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_schemas`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataSchemas`

requests and continue to iterate
through the `metadata_schemas`

field on the
corresponding responses.

All the usual [ListMetadataSchemasResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresAsyncPager)

```
ListMetadataStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse
],
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListMetadataStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresPager)

```
ListMetadataStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
],
request: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
response: google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresResponse,
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


A pager for iterating through `list_metadata_stores`

requests.

This class thinly wraps an initial
[ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`metadata_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListMetadataStores`

requests and continue to iterate
through the `metadata_stores`

field on the
corresponding responses.

All the usual [ListMetadataStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_servicevertexragserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient -->

# Class VertexRagServiceAsyncClient (1.134.0)

```
VertexRagServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

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
`VertexRagServiceTransport` |
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

### VertexRagServiceAsyncClient

```
VertexRagServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_augment_prompt():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceAsyncClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
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
Response message for AugmentPrompt. |

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

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[google.cloud.aiplatform_v1.types.content.Content] = None,
facts: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.vertex_rag_service.Fact]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.CorroborateContentResponse
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_corroborate_content():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceAsyncClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for CorroborateContent. |
`parent` |
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`:class:`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
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
Response message for CorroborateContent. |

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
`VertexRagServiceAsyncClient` |
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
`VertexRagServiceAsyncClient` |
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
`VertexRagServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.vertex_rag_service.transports.base.VertexRagServiceTransport
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

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
query = aiplatform_v1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = await client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1_services_vertex_rag_service_VertexRagServiceAsyncClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
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
Response message for VertexRagService.RetrieveContexts. |

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesmigration_servicepagers_googlecloudaiplatfor_68344a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesmigration_servicepagers_googlecloudaiplatform_5515b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmigration_servicepagers_googlecloudaiplatform__61590d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmigration_servicepagers_googlecloudaiplatform_v_8f675f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmigration_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.migration_service.pagers`

module.

## Classes

[SearchMigratableResourcesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager)

```
SearchMigratableResourcesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse
],
],
request: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse) object, and
provides an `__aiter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchMigratableResourcesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesPager)

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1.types.migration_service.SearchMigratableResourcesResponse,
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


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeshyperparametertuningjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HyperparameterTuningJob -->

# Class HyperparameterTuningJob (1.134.0)

`HyperparameterTuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the HyperparameterTuningJob. |
`display_name` |
`str`
Required. The display name of the HyperparameterTuningJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`study_spec` |
Required. Study configuration of the HyperparameterTuningJob. |
`max_trial_count` |
`int`
Required. The desired total number of Trials. |
`parallel_trial_count` |
`int`
Required. The desired number of Trials to run in parallel. |
`max_failed_trial_count` |
`int`
The number of failed Trials that need to be seen before failing the HyperparameterTuningJob. If set to 0, Vertex AI decides how many Trials must fail before the whole job fails. |
`trial_job_spec` |
Required. The spec of a trial job. The same spec applies to the CustomJobs created in all the trials. |
`trials` |
`MutableSequence[`
Output only. Trials of the HyperparameterTuningJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize HyperparameterTuningJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a HyperparameterTuningJob. If this is set, then all resources created by the HyperparameterTuningJob will be encrypted with the provided encryption key. |
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

## Methods

### HyperparameterTuningJob

`HyperparameterTuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeshyperparametertuningjob__googlecloudaiplatform_v1b_6482ce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeshyperparametertuningjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.HyperparameterTuningJob -->

# Class HyperparameterTuningJob (1.134.0)

`HyperparameterTuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the HyperparameterTuningJob. |
`display_name` |
`str`
Required. The display name of the HyperparameterTuningJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`study_spec` |
Required. Study configuration of the HyperparameterTuningJob. |
`max_trial_count` |
`int`
Required. The desired total number of Trials. |
`parallel_trial_count` |
`int`
Required. The desired number of Trials to run in parallel. |
`max_failed_trial_count` |
`int`
The number of failed Trials that need to be seen before failing the HyperparameterTuningJob. If set to 0, Vertex AI decides how many Trials must fail before the whole job fails. |
`trial_job_spec` |
Required. The spec of a trial job. The same spec applies to the CustomJobs created in all the trials. |
`trials` |
`MutableSequence[`
Output only. Trials of the HyperparameterTuningJob. |
`state` |
Output only. The detailed state of the job. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the HyperparameterTuningJob was most recently updated. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize HyperparameterTuningJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a HyperparameterTuningJob. If this is set, then all resources created by the HyperparameterTuningJob will be encrypted with the provided encryption key. |
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

## Methods

### HyperparameterTuningJob

`HyperparameterTuningJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a HyperparameterTuningJob. A HyperparameterTuningJob has a Study specification and multiple CustomJobs with identical CustomJob specification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespredictschemata_googlecloudaiplatform_v1beta1_cf1888.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredictschemata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictSchemata -->

# Class PredictSchemata (1.134.0)

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.

## Attributes |
|
|---|---|
Name |
Description |
`instance_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in PredictRequest.instances, ExplainRequest.instances and BatchPredictionJob.input_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`parameters_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via PredictRequest.parameters, ExplainRequest.parameters and BatchPredictionJob.model_parameters. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`prediction_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via PredictResponse.predictions, ExplainResponse.explanations, and BatchPredictionJob.output_config. The schema is defined as an OpenAPI 3.0.2 `Schema Object |

## Methods

### PredictSchemata

`PredictSchemata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains the schemata used in Model's predictions and explanations via PredictionService.Predict, PredictionService.Explain and BatchPredictionJob.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescorroboratecontentrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest -->

# Class CorroborateContentRequest (1.134.0)

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`content` |
Optional. Input content to corroborate, only text format is supported for now. This field is a member of `oneof` _ `_content` .
|
`facts` |
`MutableSequence[`
Optional. Facts used to generate the text can also be used to corroborate the text. |
`parameters` |
Optional. Parameters that can be set to override default settings per request. |

## Classes

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.

## Methods

### CorroborateContentRequest

`CorroborateContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typescorroboratecontentrequestparameters_google_527ef4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescorroboratecontentrequestparameters_googlec_4e6600.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescorroboratecontentrequestparameters_googlecl_571516.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescorroboratecontentrequestparameters_googleclo_9ba47a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescorroboratecontentrequestparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest.Parameters -->

# Class Parameters (1.134.0)

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.

## Attribute |
|
|---|---|
Name |
Description |
`citation_threshold` |
`float`
Optional. Only return claims with citation score larger than the threshold. |

## Methods

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided per request.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespscautomationstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PSCAutomationState -->

# Class PSCAutomationState (1.134.0)

`PSCAutomationState(value)`


The state of the PSC service automation.

## Enums |
|
|---|---|
Name |
Description |
`PSC_AUTOMATION_STATE_UNSPECIFIED` |
Should not be used. |
`PSC_AUTOMATION_STATE_SUCCESSFUL` |
The PSC service automation is successful. |
`PSC_AUTOMATION_STATE_FAILED` |
The PSC service automation has failed. |

## Methods

### PSCAutomationState

`PSCAutomationState(value)`


The state of the PSC service automation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescopymodeloperationmetadata_googlecloudaiplatform_v_dde487.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescopymodeloperationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelOperationMetadata -->

# Class CopyModelOperationMetadata (1.134.0)

`CopyModelOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of ModelService.CopyModel operation.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### CopyModelOperationMetadata

`CopyModelOperationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details of ModelService.CopyModel operation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespscautomationstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationState -->

# Class PSCAutomationState (1.134.0)

`PSCAutomationState(value)`


The state of the PSC service automation.

## Enums |
|
|---|---|
Name |
Description |
`PSC_AUTOMATION_STATE_UNSPECIFIED` |
Should not be used. |
`PSC_AUTOMATION_STATE_SUCCESSFUL` |
The PSC service automation is successful. |
`PSC_AUTOMATION_STATE_FAILED` |
The PSC service automation has failed. |

## Methods

### PSCAutomationState

`PSCAutomationState(value)`


The state of the PSC service automation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescorpusstatusstate_googlecloudaiplatform_v1ty_48216d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescorpusstatusstate_googlecloudaiplatform_v1typ_c25c1c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescorpusstatusstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorpusStatus.State -->

# Class State (1.134.0)

`State(value)`


RagCorpus life state.

## Enums |
|
|---|---|
Name |
Description |
`UNKNOWN` |
This state is not supposed to happen. |
`INITIALIZED` |
RagCorpus resource entry is initialized, but hasn't done validation. |
`ACTIVE` |
RagCorpus is provisioned successfully and is ready to serve. |
`ERROR` |
RagCorpus is in a problematic situation. See `error_message` field for details. |

## Methods

### State

`State(value)`


RagCorpus life state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgetfeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeaturestoreRequest -->

# Class GetFeaturestoreRequest (1.134.0)

`GetFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeaturestore.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Featurestore resource. |

## Methods

### GetFeaturestoreRequest

`GetFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.GetFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgeniesource_googlecloudaiplatform_v1beta1typesgetn_b14e51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgeniesource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenieSource -->

# Class GenieSource (1.134.0)

`GenieSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Generative AI Studio.

## Attribute |
|
|---|---|
Name |
Description |
`base_model_uri` |
`str`
Required. The public base model URI. |

## Methods

### GenieSource

`GenieSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Generative AI Studio.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgetnasjobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNasJobRequest -->

# Class GetNasJobRequest (1.134.0)

`GetNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nas_job}`
|

## Methods

### GetNasJobRequest

`GetNasJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.GetNasJob.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslogprobsresulttopcandidates_googlecloudaipl_b7b5a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslogprobsresulttopcandidates_googlecloudaipla_a543e1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslogprobsresulttopcandidates_googlecloudaiplat_49014c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslogprobsresulttopcandidates.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult.TopCandidates -->

# Class TopCandidates (1.134.0)

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.

## Attribute |
|
|---|---|
Name |
Description |
`candidates` |
`MutableSequence[`
Sorted by log probability in descending order. |

## Methods

### TopCandidates

`TopCandidates(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Candidates with top log probabilities at each decoding step.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfasterdeploymentconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FasterDeploymentConfig -->

# Class FasterDeploymentConfig (1.134.0)

`FasterDeploymentConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for faster model deployment.

## Attribute |
|
|---|---|
Name |
Description |
`fast_tryout_enabled` |
`bool`
If true, enable fast tryout feature for this deployed model. |

## Methods

### FasterDeploymentConfig

`FasterDeploymentConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for faster model deployment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfasterdeploymentconfig_googlecloudaiplatform__0d62bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfasterdeploymentconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FasterDeploymentConfig -->

# Class FasterDeploymentConfig (1.134.0)

`FasterDeploymentConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for faster model deployment.

## Attribute |
|
|---|---|
Name |
Description |
`fast_tryout_enabled` |
`bool`
If true, enable fast tryout feature for this deployed model. |

## Methods

### FasterDeploymentConfig

`FasterDeploymentConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for faster model deployment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstoptrialrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopTrialRequest -->

# Class StopTrialRequest (1.134.0)

`StopTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.StopTrial.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The Trial's name. Format: `projects/{project}/locations/{location}/studies/{study}/trials/{trial}`
|

## Methods

### StopTrialRequest

`StopTrialRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VizierService.StopTrial.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturegroup.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup -->

# Class FeatureGroup (1.134.0)

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Group.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`big_query` |
Indicates that features for this group come from BigQuery Table/View. By default treats the source as a sparse time series source. The BigQuery source table or view must have at least one entity ID column and a column named `feature_timestamp` .
This field is a member of `oneof` _ `source` .
|
`name` |
`str`
Identifier. Name of the FeatureGroup. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureGroup was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureGroup was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureGroup. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureGroup(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`description` |
`str`
Optional. Description of the FeatureGroup. |
`service_agent_type` |
Optional. Service agent type used during jobs under a FeatureGroup. By default, the Vertex AI Service Agent is used. When using an IAM Policy to isolate this FeatureGroup within a project, a separate service account should be provisioned by setting this field to `SERVICE_AGENT_TYPE_FEATURE_GROUP` . This will generate a
separate service account to access the BigQuery source
table.
|
`service_account_email` |
`str`
Output only. A Service Account unique to this FeatureGroup. The role bigquery.dataViewer should be granted to this service account to allow Vertex AI Feature Store to access source data while running jobs under this FeatureGroup. |

## Classes

### BigQuery

`BigQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input source type for BigQuery Tables and Views.

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

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during jobs under a FeatureGroup.

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Group.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_servicevertexragserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient -->

# Class VertexRagServiceAsyncClient (1.134.0)

```
VertexRagServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for retrieving relevant contexts.

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
`VertexRagServiceTransport` |
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

### VertexRagServiceAsyncClient

```
VertexRagServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the vertex rag service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,VertexRagServiceTransport,Callable[..., VertexRagServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the VertexRagServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### augment_prompt

```
augment_prompt(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
model: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptRequest.Model
] = None,
vertex_rag_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.tool.VertexRagStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.AugmentPromptResponse
```


Given an input prompt, it returns augmented prompt from vertex rag store to guide LLM towards generating grounded responses.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_augment_prompt():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[AugmentPromptRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AugmentPromptRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[augment_prompt](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceAsyncClient_augment_prompt)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for AugmentPrompt. |
`parent` |
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: |
`model` |
Optional. Metadata of the backend deployed model. This corresponds to the |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This corresponds to the |
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
Response message for AugmentPrompt. |

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

### corroborate_content

```
corroborate_content(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
content: typing.Optional[
google.cloud.aiplatform_v1beta1.types.content.Content
] = None,
facts: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.Fact
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
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.CorroborateContentResponse
)
```


Given an input text, it returns a score that evaluates the factuality of the text. It also extracts and returns claims from the text and provides supporting facts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_corroborate_content():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CorroborateContentRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest.html)(
parent="parent_value",
)
# Make the request
response = await client.[corroborate_content](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceAsyncClient_corroborate_content)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for CorroborateContent. |
`parent` |
Required. The resource name of the Location from which to corroborate text. The users must have permission to make a call in the project. Format: |
`content` |
Optional. Input content to corroborate, only text format is supported for now. This corresponds to the |
`facts` |
`:class:`
Optional. Facts used to generate the text can also be used to corroborate the text. This corresponds to the |
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
Response message for CorroborateContent. |

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
`VertexRagServiceAsyncClient` |
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
`VertexRagServiceAsyncClient` |
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
`VertexRagServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.vertex_rag_service.transports.base.VertexRagServiceTransport
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

### parse_rag_corpus_path

`parse_rag_corpus_path(path: str) -> typing.Dict[str, str]`


Parses a rag_corpus path into its component segments.

### rag_corpus_path

`rag_corpus_path(project: str, location: str, rag_corpus: str) -> str`


Returns a fully-qualified rag_corpus string.

### retrieve_contexts

```
retrieve_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
query: typing.Optional[
google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RagQuery
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.vertex_rag_service.RetrieveContextsResponse
```


Retrieves relevant contexts for a query.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_retrieve_contexts():
# Create a client
client = aiplatform_v1beta1.
```[VertexRagServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html)()
# Initialize request argument(s)
query = aiplatform_v1beta1.[RagQuery](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagQuery.html)()
query.text = "text_value"
request = aiplatform_v1beta1.[RetrieveContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest.html)(
parent="parent_value",
query=query,
)
# Make the request
response = await client.[retrieve_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_service.VertexRagServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_vertex_rag_service_VertexRagServiceAsyncClient_retrieve_contexts)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for VertexRagService.RetrieveContexts. |
`parent` |
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: |
`query` |
Required. Single RAG retrieve query. This corresponds to the |
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
Response message for VertexRagService.RetrieveContexts. |

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
