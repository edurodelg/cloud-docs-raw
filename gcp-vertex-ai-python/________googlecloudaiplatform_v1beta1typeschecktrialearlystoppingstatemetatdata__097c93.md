---
merged_at: 2026-01-25T21:47:44.371735
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_g_fe6f92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_go_2ca97d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_goo_5e805c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_goog_b5362a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_googl_39cba4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_google_cc3b12.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata_googlec_5dd083.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeschecktrialearlystoppingstatemetatdata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckTrialEarlyStoppingStateMetatdata -->

# Class CheckTrialEarlyStoppingStateMetatdata (1.134.0)

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for suggesting Trials. |
`study` |
`str`
The name of the Study that the Trial belongs to. |
`trial` |
`str`
The Trial name. |

## Methods

### CheckTrialEarlyStoppingStateMetatdata

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmutatedeployedindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexRequest -->

# Class MutateDeployedIndexRequest (1.134.0)

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoint` |
`str`
Required. The name of the IndexEndpoint resource into which to deploy an Index. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|
`deployed_index` |
Required. The DeployedIndex to be updated within the IndexEndpoint. Currently, the updatable fields are `DeployedIndex][automatic_resources]` and
`DeployedIndex][dedicated_resources]`
|

## Methods

### MutateDeployedIndexRequest

`MutateDeployedIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.MutateDeployedIndex.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescopymodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest -->

# Class CopyModelRequest (1.134.0)

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

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
`model_id` |
`str`
Optional. Copy source_model into a new Model with this ID. The ID will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
This field is a member of `oneof` _ `destination_model` .
|
`parent_model` |
`str`
Optional. Specify this field to copy source_model into this existing Model as a new version. Format: `projects/{project}/locations/{location}/models/{model}`
This field is a member of `oneof` _ `destination_model` .
|
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: `projects/{project}/locations/{location}`
|
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: `projects/{project}/locations/{location}/models/{model}`
|
`encryption_spec` |
Customer-managed encryption key options. If this is set, then the Model copy will be encrypted with the provided encryption key. |

## Methods

### CopyModelRequest

`CopyModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.CopyModel.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeaturenoisesigmanoisesigmaforfeature_google_aa200b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeaturenoisesigmanoisesigmaforfeature_googlec_7be7c6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturenoisesigmanoisesigmaforfeature.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureNoiseSigma.NoiseSigmaForFeature -->

# Class NoiseSigmaForFeature (1.134.0)

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The name of the input feature for which noise sigma is provided. The features are defined in [explanation metadata inputs][google.cloud.aiplatform.v1beta1.ExplanationMetadata.inputs]. |
`sigma` |
`float`
This represents the standard deviation of the Gaussian kernel that will be used to add noise to the feature prior to computing gradients. Similar to noise_sigma but represents the noise added to the current feature. Defaults to 0.1. |

## Methods

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesunmanagedcontainermodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UnmanagedContainerModel -->

# Class UnmanagedContainerModel (1.134.0)

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_uri` |
`str`
The path to the directory containing the Model artifact and any of its supporting files. |
`predict_schemata` |
Contains the schemata used in Model's predictions and explanations |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. |

## Methods

### UnmanagedContainerModel

`UnmanagedContainerModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains model information necessary to perform batch prediction without requiring a full model import.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluatedatasetrun_googlecloudaiplatform_v1be_d9bd6a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluatedatasetrun.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetRun -->

# Class EvaluateDatasetRun (1.134.0)

`EvaluateDatasetRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluate Dataset Run Result for Tuning Job.

## Attributes |
|
|---|---|
Name |
Description |
`operation_name` |
`str`
Output only. The operation ID of the evaluation run. Format: `projects/{project}/locations/{location}/operations/{operation_id}` .
|
`checkpoint_id` |
`str`
Output only. The checkpoint id used in the evaluation run. Only populated when evaluating checkpoints. |
`evaluate_dataset_response` |
Output only. Results for EvaluationService.EvaluateDataset. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error of the evaluation run if any. |

## Methods

### EvaluateDatasetRun

`EvaluateDatasetRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Evaluate Dataset Run Result for Tuning Job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexamplesoverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExamplesOverride -->

# Class ExamplesOverride (1.134.0)

`ExamplesOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Overrides for example-based explanations.

## Attributes |
|
|---|---|
Name |
Description |
`neighbor_count` |
`int`
The number of neighbors to return. |
`crowding_count` |
`int`
The number of neighbors to return that have the same crowding tag. |
`restrictions` |
`MutableSequence[`
Restrict the resulting nearest neighbors to respect these constraints. |
`return_embeddings` |
`bool`
If true, return the embeddings instead of neighbors. |
`data_format` |
The format of the data being provided with each call. |

## Classes

### DataFormat

`DataFormat(value)`


Data format enum.

## Methods

### ExamplesOverride

`ExamplesOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Overrides for example-based explanations.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesresumeschedulerequest_googlecloudaiplatform_5cd9e8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesresumeschedulerequest_googlecloudaiplatform__3cc4cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesresumeschedulerequest_googlecloudaiplatform_v_d126b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesresumeschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResumeScheduleRequest -->

# Class ResumeScheduleRequest (1.134.0)

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: `projects/{project}/locations/{location}/schedules/{schedule}`
|
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. |

## Methods

### ResumeScheduleRequest

`ResumeScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.ResumeSchedule.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslisthyperparametertuningjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse -->

# Class ListHyperparameterTuningJobsResponse (1.134.0)

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`hyperparameter_tuning_jobs` |
`MutableSequence[`
List of HyperparameterTuningJobs in the requested page. HyperparameterTuningJob.trials of the jobs will be not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListHyperparameterTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListHyperparameterTuningJobsResponse

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexportmodeloperationmetadataoutputinfo_google_5df382.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexportmodeloperationmetadataoutputinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelOperationMetadata.OutputInfo -->

# Class OutputInfo (1.134.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_output_uri` |
`str`
Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to. |
`image_output_uri` |
`str`
Output only. If the Model image is being exported to Google Container Registry or Artifact Registry this is the full path of the image created. |

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletecontextrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteContextRequest -->

# Class DeleteContextRequest (1.134.0)

`DeleteContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteContext.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Context to delete. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`force` |
`bool`
The force deletion semantics is still undefined. Users should not use this field. |
`etag` |
`str`
Optional. The etag of the Context to delete. If this is provided, it must match the server's etag. Otherwise, the request will fail with a FAILED_PRECONDITION. |

## Methods

### DeleteContextRequest

`DeleteContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.DeleteContext.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesexportmodeloperationmetadataoutputinfo_googleclou_d94a08.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexportmodeloperationmetadataoutputinfo_googlecloud_4ab665.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportmodeloperationmetadataoutputinfo.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelOperationMetadata.OutputInfo -->

# Class OutputInfo (1.134.0)

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.

## Attributes |
|
|---|---|
Name |
Description |
`artifact_output_uri` |
`str`
Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to. |
`image_output_uri` |
`str`
Output only. If the Model image is being exported to Google Container Registry or Artifact Registry this is the full path of the image created. |

## Methods

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes the output of the ExportModel. Supplements ExportModelRequest.OutputConfig.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typestextsentimentpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextSentimentPredictionInstance -->

# Class TextSentimentPredictionInstance (1.134.0)

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |

## Methods

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdistillationspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationSpec -->

# Class DistillationSpec (1.134.0)

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

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
`base_teacher_model` |
`str`
The base teacher model that is being distilled. See `Supported models |
`tuned_teacher_model_source` |
`str`
The resource name of the Tuned teacher model. Format: `projects/{project}/locations/{location}/models/{model}` .
This field is a member of `oneof` _ `teacher_model` .
|
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. This field is a member of `oneof` _ `_validation_dataset_uri` .
|
`hyper_parameters` |
Optional. Hyperparameters for Distillation. |
`student_model` |
`str`
The student model that is being tuned, e.g., "google/gemma-2b-1.1-it". |
`pipeline_root_directory` |
`str`
Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the distillation pipeline. It is used by the system to generate the paths of output artifacts. |

## Methods

### DistillationSpec

`DistillationSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning Spec for Distillation.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodel____googlecloudaiplatform_v1beta1typesde_c03906.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model -->

# Class Model (1.134.0)

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
The resource name of the Model. |
`version_id` |
`str`
Output only. Immutable. The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation. |
`version_aliases` |
`MutableSequence[str]`
User provided version aliases so that a model version can be referenced via alias (i.e. `projects/{project}/locations/{location}/models/{model_id}@{version_alias}`
instead of auto-generated version id (i.e.
`projects/{project}/locations/{location}/models/{model_id}@{version_id})` .
The format is `a-z][a-zA-Z0-9-]` {0,126}[a-z0-9] to
distinguish from version_id. A default version alias will be
created for the first version of the model, and there must
be exactly one default version alias for a model.
|
`version_create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was created. |
`version_update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this version was most recently updated. |
`display_name` |
`str`
Required. The display name of the Model. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
The description of the Model. |
`version_description` |
`str`
The description of this version. |
`default_checkpoint_id` |
`str`
The default checkpoint id of a model version. |
`predict_schemata` |
The schemata that describe formats of the Model's predictions and explanations as given and returned via PredictionService.Predict and PredictionService.Explain. |
`metadata_schema_uri` |
`str`
Immutable. Points to a YAML file stored on Google Cloud Storage describing additional information about the Model, that is specific to it. Unset if the Model does not have any additional information. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metadata` |
`google.protobuf.struct_pb2.Value`
Immutable. An additional information about the Model; the schema of the metadata can be found in metadata_schema. Unset if the Model does not have any additional information. |
`supported_export_formats` |
`MutableSequence[`
Output only. The formats in which this Model may be exported. If empty, this Model is not available for export. |
`training_pipeline` |
`str`
Output only. The resource name of the TrainingPipeline that uploaded this Model, if any. |
`container_spec` |
Input only. The specification of the container that is to be used when deploying this Model. The specification is ingested upon ModelService.UploadModel, and all binaries it contains are copied and stored internally by Vertex AI. Not required for AutoML Models. |
`artifact_uri` |
`str`
Immutable. The path to the directory containing the Model artifact and any of its supporting files. Not required for AutoML Models. |
`supported_deployment_resources_types` |
`MutableSequence[`
Output only. When this Model is deployed, its prediction resources are described by the `prediction_resources`
field of the
Endpoint.deployed_models
object. Because not all Models support all resource
configuration types, the configuration types this Model
supports are listed here. If no configuration types are
listed, the Model cannot be deployed to an
Endpoint and
does not support online predictions
(PredictionService.Predict
or
PredictionService.Explain).
Such a Model can serve predictions by using a
BatchPredictionJob,
if it has at least one entry each in
supported_input_storage_formats
and
supported_output_storage_formats.
|
`supported_input_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.input_config. If PredictSchemata.instance_schema_uri exists, the instances should be given as per that schema. The possible formats are: - `jsonl` The JSON Lines format, where each instance is a
single line. Uses
GcsSource.
- `csv` The CSV format, where each instance is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsSource.
- `tf-record` The TFRecord format, where each instance is
a single record in tfrecord syntax. Uses
GcsSource.
- `tf-record-gzip` Similar to `tf-record` , but the file
is gzipped. Uses
GcsSource.
- `bigquery` Each instance is a single row in BigQuery.
Uses
BigQuerySource.
- `file-list` Each line of the file is the location of an
instance to process, uses `gcs_source` field of the
InputConfig
object.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`supported_output_storage_formats` |
`MutableSequence[str]`
Output only. The formats this Model supports in BatchPredictionJob.output_config. If both PredictSchemata.instance_schema_uri and PredictSchemata.prediction_schema_uri exist, the predictions are returned together with their instances. In other words, the prediction has the original instance data first, followed by the actual prediction content (as per the schema). The possible formats are: - `jsonl` The JSON Lines format, where each prediction is
a single line. Uses
GcsDestination.
- `csv` The CSV format, where each prediction is a single
comma-separated line. The first line in the file is the
header, containing comma-separated field names. Uses
GcsDestination.
- `bigquery` Each prediction is a single row in a BigQuery
table, uses
BigQueryDestination
.
If this Model doesn't support any of these formats it means
it cannot be used with a
BatchPredictionJob.
However, if it has
supported_deployment_resources_types,
it could serve online predictions by using
PredictionService.Predict
or
PredictionService.Explain.
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was uploaded into Vertex AI. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Model was most recently updated. |
`deployed_models` |
`MutableSequence[`
Output only. The pointers to DeployedModels created from this Model. Note that Model could have been deployed to Endpoints in different Locations. |
`explanation_spec` |
The default explanation specification for this Model. The Model can be used for [requesting explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] after being deployed if it is populated. The Model can be used for [batch explanation][google.cloud.aiplatform.v1beta1.BatchPredictionJob.generate_explanation] if it is populated. All fields of the explanation_spec can be overridden by explanation_spec of DeployModelRequest.deployed_model, or explanation_spec of BatchPredictionJob. If the default explanation specification is not set for this Model, this Model can still be used for [requesting explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] by setting explanation_spec of DeployModelRequest.deployed_model and for [batch explanation][google.cloud.aiplatform.v1beta1.BatchPredictionJob.generate_explanation] by setting explanation_spec of BatchPredictionJob. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key spec for a Model. If set, this Model and all sub-resources of this Model will be secured by this key. |
`model_source_info` |
Output only. Source of a model. It can either be automl training pipeline, custom training pipeline, BigQuery ML, or saved and tuned from Genie or Model Garden. |
`original_model_info` |
Output only. If this Model is a copy of another Model, this contains info about the original. |
`metadata_artifact` |
`str`
Output only. The resource name of the Artifact that was created in MetadataStore when creating the Model. The Artifact resource name pattern is `projects/{project}/locations/{location}/metadataStores/{metadata_store}/artifacts/{artifact}` .
|
`base_model_source` |
Optional. User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`checkpoints` |
`MutableSequence[`
Optional. Output only. The checkpoints of the model. |

## Classes

### BaseModelSource

`BaseModelSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User input field to specify the base model source. Currently it only supports specifing the Model Garden models and Genie models.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeploymentResourcesType

`DeploymentResourcesType(value)`


Identifies a type of Model's prediction resources.

### ExportFormat

`ExportFormat(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents export format supported by the Model. All formats export to Google Cloud Storage.

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

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Methods

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A trained machine learning Model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesdeployresponse_googlecloudaiplatform_v1type_2eafb3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesdeployresponse_googlecloudaiplatform_v1types_90f634.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesdeployresponse_googlecloudaiplatform_v1typesn_96ef37.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeployresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployResponse -->

# Class DeployResponse (1.134.0)

`DeployResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.Deploy.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_model` |
`str`
Output only. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`
|
`endpoint` |
`str`
Output only. The name of the Endpoint created. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Output only. The name of the Model created. Format: `projects/{project}/locations/{location}/models/{model}`
|

## Methods

### DeployResponse

`DeployResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.Deploy.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookidleshutdownconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookIdleShutdownConfig -->

# Class NotebookIdleShutdownConfig (1.134.0)

`NotebookIdleShutdownConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idle_timeout as required field.

## Attributes |
|
|---|---|
Name |
Description |
`idle_timeout` |
`google.protobuf.duration_pb2.Duration`
Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idle_timeout (second) is: 10 \* 60 ` 1440 - 60. |
`idle_shutdown_disabled` |
`bool`
Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate. |

## Methods

### NotebookIdleShutdownConfig

`NotebookIdleShutdownConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idle_timeout as required field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgenerationconfigroutingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.134.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespurgeexecutionsrequest_googlecloudaiplatform_ae100c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespurgeexecutionsrequest_googlecloudaiplatform__b7f0e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespurgeexecutionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeExecutionsRequest -->

# Class PurgeExecutionsRequest (1.134.0)

`PurgeExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Executions from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Executions to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Execution names that would be deleted.
|

## Methods

### PurgeExecutionsRequest

`PurgeExecutionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeExecutions.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateNotebookRuntimeTemplateRequest -->

# Class CreateNotebookRuntimeTemplateRequest (1.134.0)

```
CreateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.CreateNotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. |
`notebook_runtime_template_id` |
`str`
Optional. User specified ID for the notebook runtime template. |

## Methods

### CreateNotebookRuntimeTemplateRequest

```
CreateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.CreateNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessession.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Session -->

# Class Session (1.134.0)

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

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
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp of when this session is considered expired. This is *always* provided on output, regardless of what was sent on input. This field is a member of `oneof` _ `expiration` .
|
`ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. Input only. The TTL for this session. This field is a member of `oneof` _ `expiration` .
|
`name` |
`str`
Identifier. The resource name of the session. Format: 'projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}'. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the session was updated. |
`display_name` |
`str`
Optional. The display name of the session. |
`session_state` |
`google.protobuf.struct_pb2.Struct`
Optional. Session specific memory which stores key conversation points. |
`user_id` |
`str`
Required. Immutable. String id provided by the user |

## Methods

### Session

`Session(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A session contains a set of actions between users and Vertex agents.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagers__32d6b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagers___6a34bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_online_store_admin_service.pagers`

module.

## Classes

[ListFeatureOnlineStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresAsyncPager)

```
ListFeatureOnlineStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureOnlineStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewSyncsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureViewsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsPager)

```
ListFeatureViewsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
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


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesretrievememoriesresponse_googlecloudaiplatf_a63e5b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesretrievememoriesresponse_googlecloudaiplatfo_79044d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesretrievememoriesresponse_googlecloudaiplatfor_8d83dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievememoriesresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesResponse -->

# Class RetrieveMemoriesResponse (1.134.0)

`RetrieveMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.RetrieveMemories.

## Attributes |
|
|---|---|
Name |
Description |
`retrieved_memories` |
`MutableSequence[`
The retrieved memories. |
`next_page_token` |
`str`
A token that can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages. This token is not set if similarity search was used
for retrieval.
|

## Classes

### RetrievedMemory

`RetrievedMemory(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A retrieved memory.

## Methods

### RetrieveMemoriesResponse

`RetrieveMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.RetrieveMemories.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinetaskdetailstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskDetail.State -->

# Class State (1.134.0)

`State(value)`


Specifies state of TaskExecution

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`PENDING` |
Specifies pending state for the task. |
`RUNNING` |
Specifies task is being executed. |
`SUCCEEDED` |
Specifies task completed successfully. |
`CANCEL_PENDING` |
Specifies Task cancel is in pending state. |
`CANCELLING` |
Specifies task is being cancelled. |
`CANCELLED` |
Specifies task was cancelled. |
`FAILED` |
Specifies task failed. |
`SKIPPED` |
Specifies task was skipped due to cache hit. |
`NOT_TRIGGERED` |
Specifies that the task was not triggered because the task's trigger policy is not satisfied. The trigger policy is specified in the `condition` field of PipelineJob.pipeline_spec. |

## Methods

### State

`State(value)`


Specifies state of TaskExecution


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatecontextrequest_googlecloudaiplatform_v1beta1_943afb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatecontextrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateContextRequest -->

# Class UpdateContextRequest (1.134.0)

`UpdateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateContext.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
Required. The Context containing updates. The Context's Context.name field is used to identify the Context to be updated. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. |
`allow_missing` |
`bool`
If set to true, and the Context is not found, a new Context is created. |

## Methods

### UpdateContextRequest

`UpdateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateContext.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrougemetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RougeMetricValue -->

# Class RougeMetricValue (1.134.0)

`RougeMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rouge metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Rouge score. This field is a member of `oneof` _ `_score` .
|

## Methods

### RougeMetricValue

`RougeMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rouge metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeployresponse_googlecloudaiplatform_v1beta1types_20ea14.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeployresponse_googlecloudaiplatform_v1beta1typesl_a6b0e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployResponse -->

# Class DeployResponse (1.134.0)

`DeployResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.Deploy.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_model` |
`str`
Output only. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}` ,
or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`
|
`endpoint` |
`str`
Output only. The name of the Endpoint created. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`model` |
`str`
Output only. The name of the Model created. Format: `projects/{project}/locations/{location}/models/{model}`
|

## Methods

### DeployResponse

`DeployResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.Deploy.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmemoriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesRequest -->

# Class ListMemoriesRequest (1.134.0)

`ListMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.ListMemories.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the ReasoningEngine to list the Memories under. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`filter` |
`str`
Optional. The standard list filter. More detail in `AIP-160 ` __.
Supported fields (equality match only):
- `scope` (as a JSON string)
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. |

## Methods

### ListMemoriesRequest

`ListMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.ListMemories.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesreque_0a4603.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessearchmodeldeploymentmonitoringstatsanomaliesrequeststatsanomaliesobjective.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.134.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescustomoutput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CustomOutput -->

# Class CustomOutput (1.134.0)

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`raw_outputs` |
Output only. List of raw output strings. This field is a member of `oneof` _ `custom_output` .
|

## Methods

### CustomOutput

`CustomOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for custom output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeatureviewsyncconfig_googlecloudaiplatform_v1s_5c5d17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeatureviewsyncconfig_googlecloudaiplatform_v1se_af4cdf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeatureviewsyncconfig_googlecloudaiplatform_v1ser_024229.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeatureviewsyncconfig_googlecloudaiplatform_v1serv_6cd9dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewsyncconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.SyncConfig -->

# Class SyncConfig (1.134.0)

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.

## Attributes |
|
|---|---|
Name |
Description |
`cron` |
`str`
Cron schedule (https://en.wikipedia.org/wiki/Cron) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*". |
`continuous` |
`bool`
Optional. If true, syncs the FeatureView in a continuous manner to Online Store. |

## Methods

### SyncConfig

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service -->

# Package feature_registry_service (1.134.0)

API documentation for `aiplatform_v1.services.feature_registry_service`

package.

## Classes

[FeatureRegistryServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceAsyncClient)

The service that handles CRUD and List for resources for FeatureRegistry.

[FeatureRegistryServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient)

The service that handles CRUD and List for resources for FeatureRegistry.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers)

API documentation for `aiplatform_v1.services.feature_registry_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateschedulerequest_googlecloudaiplatform_v1beta_bcf472.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateschedulerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateScheduleRequest -->

# Class UpdateScheduleRequest (1.134.0)

`UpdateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.UpdateSchedule.

## Attributes |
|
|---|---|
Name |
Description |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### UpdateScheduleRequest

`UpdateScheduleRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ScheduleService.UpdateSchedule.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborsearchoperationmetadatarecorderror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborSearchOperationMetadata.RecordError -->

# Class RecordError (1.134.0)

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`error_type` |
The error type of this record. |
`error_message` |
`str`
A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against error_type as the source of truth. |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`embedding_id` |
`str`
Empty if the embedding id is failed to parse. |
`raw_record` |
`str`
The original content of this record. |

## Classes

### RecordErrorType

`RecordErrorType(value)`


## Methods

### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatarecorderror_ed23a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatarecorderror__8e7ab5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnearestneighborsearchoperationmetadatarecorderror.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighborSearchOperationMetadata.RecordError -->

# Class RecordError (1.134.0)

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`error_type` |
The error type of this record. |
`error_message` |
`str`
A human-readable message that is shown to the user to help them fix the error. Note that this message may change from time to time, your code should check against error_type as the source of truth. |
`source_gcs_uri` |
`str`
Cloud Storage URI pointing to the original file in user's bucket. |
`embedding_id` |
`str`
Empty if the embedding id is failed to parse. |
`raw_record` |
`str`
The original content of this record. |

## Classes

### RecordErrorType

`RecordErrorType(value)`


## Methods

### RecordError

`RecordError(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeschecktrialearlystoppingstatemetatdata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CheckTrialEarlyStoppingStateMetatdata -->

# Class CheckTrialEarlyStoppingStateMetatdata (1.134.0)

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for suggesting Trials. |
`study` |
`str`
The name of the Study that the Trial belongs to. |
`trial` |
`str`
The Trial name. |

## Methods

### CheckTrialEarlyStoppingStateMetatdata

```
CheckTrialEarlyStoppingStateMetatdata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


This message will be placed in the metadata field of a google.longrunning.Operation associated with a CheckTrialEarlyStoppingState request.


---

<!-- DOCUMENTO FUSIONADO: __summary_overview_googlecloudaiplatform_v1typesragvectordbconfigragmanageddbknn_76c97d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _summary_overview_googlecloudaiplatform_v1typesragvectordbconfigragmanageddbknn.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: summary_overview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/summary_overview -->

# AI Platform API

Overview of the APIs available for AI Platform API.

## All entries

Classes, methods and properties & attributes for AI Platform API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragvectordbconfigragmanageddbknn.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb.KNN -->

# Class KNN (1.134.0)

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.

## Methods

### KNN

`KNN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for KNN search.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingchunkweb.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Web -->

# Class Web (1.134.0)

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
URI reference of the chunk. This field is a member of `oneof` _ `_uri` .
|
`title` |
`str`
Title of the chunk. This field is a member of `oneof` _ `_title` .
|

## Methods

### Web

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesragretrievalconfigrankingllmranker_googlecloudai_257c68.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragretrievalconfigrankingllmranker_googlecloudaip_8010d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragretrievalconfigrankingllmranker_googlecloudaipl_30bfe0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragretrievalconfigrankingllmranker.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig.Ranking.LlmRanker -->

# Class LlmRanker (1.134.0)

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Optional. The model name used for ranking. Format: `gemini-1.5-pro`
This field is a member of `oneof` _ `_model_name` .
|

## Methods

### LlmRanker

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescoherenceinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CoherenceInstance -->

# Class CoherenceInstance (1.134.0)

`CoherenceInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|

## Methods

### CoherenceInstance

`CoherenceInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgenerationconfigroutingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.RoutingConfig -->

# Class RoutingConfig (1.134.0)

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

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
`auto_mode` |
Automated routing. This field is a member of `oneof` _ `routing_config` .
|
`manual_mode` |
Manual routing. This field is a member of `oneof` _ `routing_config` .
|

## Classes

### AutoRoutingMode

`AutoRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ManualRoutingMode

`ManualRoutingMode(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


When manual routing is set, the specified model will be used directly.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RoutingConfig

`RoutingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for routing the request to a specific model.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstra_3926a5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformationnumerictransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.134.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforec_eaf64a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomlforecastingmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata -->

# Class AutoMlForecastingMetadata (1.134.0)

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

## Attribute |
|
|---|---|
Name |
Description |
`train_cost_milli_node_hours` |
`int`
Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget. |

## Methods

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.

### AutoMlForecastingMetadata

`AutoMlForecastingMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata specific to AutoML Forecasting.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespoststartupscriptconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig -->

# Class PostStartupScriptConfig (1.134.0)

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.

## Attributes |
|
|---|---|
Name |
Description |
`post_startup_script` |
`str`
Optional. Post startup script to run after runtime is started. |
`post_startup_script_url` |
`str`
Optional. Post startup script url to download. Example: `gs://bucket/script.sh`
|
`post_startup_script_behavior` |
Optional. Post startup script behavior that defines download and execution behavior. |

## Classes

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

## Methods

### PostStartupScriptConfig

`PostStartupScriptConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Post startup script config.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesindex_serviceindexserviceclient_____google_e02505.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesindex_serviceindexserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient -->

# Class IndexServiceClient (1.134.0)

```
IndexServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### IndexServiceClient

```
IndexServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.index_service.transports.base.IndexServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the index service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the IndexServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### create_index

```
create_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.CreateIndexRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
index: typing.Optional[google.cloud.aiplatform_v1beta1.types.index.Index] = None,
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


Creates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_create_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[CreateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateIndexRequest.html)(
parent="parent_value",
index=index,
)
# Make the request
operation = client.[create_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_create_index)(request=request)
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
The request object. Request message for IndexService.CreateIndex. |
`parent` |
`str`
Required. The resource name of the Location to create the Index in. Format: |
`index` |
Required. The Index to create. This corresponds to the |
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

### delete_index

```
delete_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.DeleteIndexRequest, dict
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


Deletes an Index. An Index can only be deleted when all its xref_DeployedIndexes had been undeployed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_delete_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_delete_index)(request=request)
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
The request object. Request message for IndexService.DeleteIndex. |
`name` |
`str`
Required. The name of the Index resource to be deleted. Format: |
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
`IndexServiceClient` |
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
`IndexServiceClient` |
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
`IndexServiceClient` |
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

### get_index

```
get_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.GetIndexRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.types.index.Index
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
from google.cloud import aiplatform_v1beta1
def sample_get_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_get_index)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.GetIndex |
`name` |
`str`
Required. The name of the Index resource. Format: |
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

### import_index

```
import_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.ImportIndexRequest, dict
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


Imports an Index from an external source (e.g., BigQuery).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_import_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
config = aiplatform_v1beta1.[ConnectorConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.html)()
config.big_query_source_config.table_path = "table_path_value"
config.big_query_source_config.datapoint_field_mapping.id_column = "id_column_value"
config.big_query_source_config.datapoint_field_mapping.embedding_column = "embedding_column_value"
request = aiplatform_v1beta1.[ImportIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.html)(
name="name_value",
config=config,
)
# Make the request
operation = client.[import_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_import_index)(request=request)
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
The request object. Request message for IndexService.ImportIndex. |
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
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest, dict
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
) -> google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager
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
from google.cloud import aiplatform_v1beta1
def sample_list_indexes():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListIndexesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_indexes](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_list_indexes)(request=request)
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
The request object. Request message for IndexService.ListIndexes. |
`parent` |
`str`
Required. The resource name of the Location from which to list the Indexes. Format: |
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
google.cloud.aiplatform_v1beta1.types.index_service.RemoveDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_service.RemoveDatapointsResponse
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
from google.cloud import aiplatform_v1beta1
def sample_remove_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RemoveDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[remove_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_remove_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.RemoveDatapoints |
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
Response message for IndexService.RemoveDatapoints |

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

### update_index

```
update_index(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.UpdateIndexRequest, dict
]
] = None,
*,
index: typing.Optional[google.cloud.aiplatform_v1beta1.types.index.Index] = None,
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


Updates an Index.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
def sample_update_index():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
index = aiplatform_v1beta1.[Index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Index.html)()
index.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateIndexRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateIndexRequest.html)(
index=index,
)
# Make the request
operation = client.[update_index](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_update_index)(request=request)
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
The request object. Request message for IndexService.UpdateIndex. |
`index` |
Required. The Index which updates the resource on the server. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
The update mask applies to the resource. For the |
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

### upsert_datapoints

```
upsert_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.index_service.UpsertDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.index_service.UpsertDatapointsResponse
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
from google.cloud import aiplatform_v1beta1
def sample_upsert_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[IndexServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpsertDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertDatapointsRequest.html)(
index="index_value",
)
# Make the request
response = client.[upsert_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.IndexServiceClient.html#google_cloud_aiplatform_v1beta1_services_index_service_IndexServiceClient_upsert_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for IndexService.UpsertDatapoints |
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesruntimeconfig_googlecloudaiplatformv1beta1_f2e2c2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesruntimeconfig_googlecloudaiplatformv1beta1s_98fe85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesruntimeconfig_googlecloudaiplatformv1beta1sc_f13d3a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesruntimeconfig_googlecloudaiplatformv1beta1sch_35459f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesruntimeconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeConfig -->

# Class RuntimeConfig (1.134.0)

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime configuration to run the extension.

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
`code_interpreter_runtime_config` |
Code execution runtime configurations for code interpreter extension. This field is a member of `oneof` _ `GoogleFirstPartyExtensionConfig` .
|
`vertex_ai_search_runtime_config` |
Runtime configuration for Vertex AI Search extension. This field is a member of `oneof` _ `GoogleFirstPartyExtensionConfig` .
|
`default_params` |
`google.protobuf.struct_pb2.Struct`
Optional. Default parameters that will be set for all the execution of this extension. If specified, the parameter values can be overridden by values in [[ExecuteExtensionRequest.operation_params]] at request time. The struct should be in a form of map with param name as the key and actual param value as the value. E.g. If this operation requires a param "name" to be set to "abc". you can set this to something like {"name": "abc"}. |

## Classes

### CodeInterpreterRuntimeConfig

```
CodeInterpreterRuntimeConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### VertexAISearchRuntimeConfig

`VertexAISearchRuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Runtime configuration to run the extension.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types -->

# Package instance_v1beta1.types (1.134.0)

API documentation for `instance_v1beta1.types`

package.

## Classes

[ImageClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance)

Prediction input format for Image Classification.

[ImageObjectDetectionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageObjectDetectionPredictionInstance)

Prediction input format for Image Object Detection.

[ImageSegmentationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageSegmentationPredictionInstance)

Prediction input format for Image Segmentation.

[TextClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextClassificationPredictionInstance)

Prediction input format for Text Classification.

[TextExtractionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextExtractionPredictionInstance)

Prediction input format for Text Extraction.

[TextSentimentPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextSentimentPredictionInstance)

Prediction input format for Text Sentiment.

[VideoActionRecognitionPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoActionRecognitionPredictionInstance)

Prediction input format for Video Action Recognition.

[VideoClassificationPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoClassificationPredictionInstance)

Prediction input format for Video Classification.

[VideoObjectTrackingPredictionInstance](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoObjectTrackingPredictionInstance)

Prediction input format for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessharepointsourcessharepointsource__googlecloudaipl_9087b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessharepointsourcessharepointsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SharePointSources.SharePointSource -->

# Class SharePointSource (1.134.0)

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
`sharepoint_folder_path` |
`str`
The path of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`sharepoint_folder_id` |
`str`
The ID of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`drive_name` |
`str`
The name of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`drive_id` |
`str`
The ID of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`client_id` |
`str`
The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All. |
`client_secret` |
The application secret for the app registered in Azure. |
`tenant_id` |
`str`
Unique identifier of the Azure Active Directory Instance. |
`sharepoint_site_name` |
`str`
The name of the SharePoint site to download from. This can be the site name or the site id. |
`file_id` |
`str`
Output only. The SharePoint file id. Output only. |

## Methods

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadataoverrideinputmetadataoverride_g_3b615f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadataoverrideinputmetadataoverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadataOverride.InputMetadataOverride -->

# Class InputMetadataOverride (1.134.0)

`InputMetadataOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The [input metadata][google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata] entries to be overridden.

## Attribute |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. This overrides the `input_baseline` field of the
ExplanationMetadata.InputMetadata
object of the corresponding feature's input metadata. If
it's not specified, the original baselines are not
overridden.
|

## Methods

### InputMetadataOverride

`InputMetadataOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The [input metadata][google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata] entries to be overridden.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfunctionresponsefiledata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionResponseFileData -->

# Class FunctionResponseFileData (1.134.0)

`FunctionResponseFileData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


URI based data for function response.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Required. The IANA standard MIME type of the source data. |
`file_uri` |
`str`
Required. URI. |
`display_name` |
`str`
Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

## Methods

### FunctionResponseFileData

`FunctionResponseFileData(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


URI based data for function response.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfig__googlecloudaiplat_2cee92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfig__googlecloudaiplatf_d46fc0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodelmonitoringobjectiveconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig -->

# Class ModelMonitoringObjectiveConfig (1.134.0)

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset` |
Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified. |
`training_prediction_skew_detection_config` |
The config for skew between training data and prediction data. |
`prediction_drift_detection_config` |
The config for drift of prediction data. |
`explanation_config` |
The config for integrating with Vertex Explainable AI. |

## Classes

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

### TrainingDataset

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Methods

### ModelMonitoringObjectiveConfig

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessearchmodeldeploymentmonitoringstatsanomalies_708ff9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodeldeploymentmonitoringstatsanomaliesrequeststatsanomaliesobjective.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesRequest.StatsAnomaliesObjective -->

# Class StatsAnomaliesObjective (1.134.0)

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.

## Attribute |
|
|---|---|
Name |
Description |
`top_feature_count` |
`int`
If set, all attribution scores between SearchModelDeploymentMonitoringStatsAnomaliesRequest.start_time and SearchModelDeploymentMonitoringStatsAnomaliesRequest.end_time are fetched, and page token doesn't take effect in this case. Only used to retrieve attribution score for the top Features which has the highest attribution score in the latest monitoring run. |

## Methods

### StatsAnomaliesObjective

`StatsAnomaliesObjective(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Stats requested for specific objective.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslisthyperparametertuningjobsresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse -->

# Class ListHyperparameterTuningJobsResponse (1.134.0)

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs

## Attributes |
|
|---|---|
Name |
Description |
`hyperparameter_tuning_jobs` |
`MutableSequence[`
List of HyperparameterTuningJobs in the requested page. HyperparameterTuningJob.trials of the jobs will be not be returned. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListHyperparameterTuningJobsRequest.page_token to obtain that page. |

## Methods

### ListHyperparameterTuningJobsResponse

```
ListHyperparameterTuningJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for JobService.ListHyperparameterTuningJobs


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesgroundingmetadatasourceflagginguri_googlecloudaip_eb534d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesgroundingmetadatasourceflagginguri_googlecloudaipl_d12227.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesgroundingmetadatasourceflagginguri.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingMetadata.SourceFlaggingUri -->

# Class SourceFlaggingUri (1.134.0)

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.

## Attributes |
|
|---|---|
Name |
Description |
`source_id` |
`str`
Id of the place or review. |
`flag_content_uri` |
`str`
A link where users can flag a problem with the source (place or review). (-- The link is generated by Google and it does not contain information from the user query. It may contain information of the content it is flagging, which can be used to identify places. --) |

## Methods

### SourceFlaggingUri

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelmonitorsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsRequest -->

# Class ListModelMonitorsRequest (1.134.0)

`ListModelMonitorsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.ListModelMonitors.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the ModelMonitors from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. More detail in `AIP-160 ` __.
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListModelMonitorsRequest

`ListModelMonitorsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.ListModelMonitors.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessharepointsourcessharepointsource.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SharePointSources.SharePointSource -->

# Class SharePointSource (1.134.0)

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

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
`sharepoint_folder_path` |
`str`
The path of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`sharepoint_folder_id` |
`str`
The ID of the SharePoint folder to download from. This field is a member of `oneof` _ `folder_source` .
|
`drive_name` |
`str`
The name of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`drive_id` |
`str`
The ID of the drive to download from. This field is a member of `oneof` _ `drive_source` .
|
`client_id` |
`str`
The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All. |
`client_secret` |
The application secret for the app registered in Azure. |
`tenant_id` |
`str`
Unique identifier of the Azure Active Directory Instance. |
`sharepoint_site_name` |
`str`
The name of the SharePoint site to download from. This can be the site name or the site id. |
`file_id` |
`str`
Output only. The SharePoint file id. Output only. |

## Methods

### SharePointSource

`SharePointSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An individual SharePointSource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdatalabelingjob_googlecloudaiplatform_v1beta1type_181b5f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdatalabelingjob_googlecloudaiplatform_v1beta1types_47e75e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdatalabelingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataLabelingJob -->

# Class DataLabelingJob (1.134.0)

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the DataLabelingJob. |
`display_name` |
`str`
Required. The user-defined name of the DataLabelingJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a DataLabelingJob. |
`datasets` |
`MutableSequence[str]`
Required. Dataset resource names. Right now we only support labeling from a single Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`annotation_labels` |
`MutableMapping[str, str]`
Labels to assign to annotations generated by this DataLabelingJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`labeler_count` |
`int`
Required. Number of labelers to work on each DataItem. |
`instruction_uri` |
`str`
Required. The Google Cloud Storage location of the instruction pdf. This pdf is shared with labelers, and provides detailed description on how to label DataItems in Datasets. |
`inputs_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the config for a specific type of DataLabelingJob. The schema files that can be used here are found in the https://storage.googleapis.com/google-cloud-aiplatform bucket in the /schema/datalabelingjob/inputs/ folder. |
`inputs` |
`google.protobuf.struct_pb2.Value`
Required. Input config parameters for the DataLabelingJob. |
`state` |
Output only. The detailed state of the job. |
`labeling_progress` |
`int`
Output only. Current labeling job progress percentage scaled in interval [0, 100], indicating the percentage of DataItems that has been finished. |
`current_spend` |
`google.type.money_pb2.Money`
Output only. Estimated cost(in US dollars) that the DataLabelingJob has incurred to date. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was updated most recently. |
`error` |
`google.rpc.status_pb2.Status`
Output only. DataLabelingJob errors. It is only populated when job's state is `JOB_STATE_FAILED` or
`JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your DataLabelingJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each DataLabelingJob: - "aiplatform.googleapis.com/schema": output only, its value is the inputs_schema's title. |
`specialist_pools` |
`MutableSequence[str]`
The SpecialistPools' resource names associated with this job. |
`encryption_spec` |
Customer-managed encryption key spec for a DataLabelingJob. If set, this DataLabelingJob will be secured by this key. Note: Annotations created in the DataLabelingJob are associated with the EncryptionSpec of the Dataset they are exported to. |
`active_learning_config` |
Parameters that configure the active learning pipeline. Active learning will label the data incrementally via several iterations. For every iteration, it will select a batch of data based on the sampling strategy. |

## Classes

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DataLabelingJob

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdatalabelingjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DataLabelingJob -->

# Class DataLabelingJob (1.134.0)

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the DataLabelingJob. |
`display_name` |
`str`
Required. The user-defined name of the DataLabelingJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a DataLabelingJob. |
`datasets` |
`MutableSequence[str]`
Required. Dataset resource names. Right now we only support labeling from a single Dataset. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`annotation_labels` |
`MutableMapping[str, str]`
Labels to assign to annotations generated by this DataLabelingJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`labeler_count` |
`int`
Required. Number of labelers to work on each DataItem. |
`instruction_uri` |
`str`
Required. The Google Cloud Storage location of the instruction pdf. This pdf is shared with labelers, and provides detailed description on how to label DataItems in Datasets. |
`inputs_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the config for a specific type of DataLabelingJob. The schema files that can be used here are found in the https://storage.googleapis.com/google-cloud-aiplatform bucket in the /schema/datalabelingjob/inputs/ folder. |
`inputs` |
`google.protobuf.struct_pb2.Value`
Required. Input config parameters for the DataLabelingJob. |
`state` |
Output only. The detailed state of the job. |
`labeling_progress` |
`int`
Output only. Current labeling job progress percentage scaled in interval [0, 100], indicating the percentage of DataItems that has been finished. |
`current_spend` |
`google.type.money_pb2.Money`
Output only. Estimated cost(in US dollars) that the DataLabelingJob has incurred to date. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataLabelingJob was updated most recently. |
`error` |
`google.rpc.status_pb2.Status`
Output only. DataLabelingJob errors. It is only populated when job's state is `JOB_STATE_FAILED` or
`JOB_STATE_CANCELLED` .
|
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your DataLabelingJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for each DataLabelingJob: - "aiplatform.googleapis.com/schema": output only, its value is the inputs_schema's title. |
`specialist_pools` |
`MutableSequence[str]`
The SpecialistPools' resource names associated with this job. |
`encryption_spec` |
Customer-managed encryption key spec for a DataLabelingJob. If set, this DataLabelingJob will be secured by this key. Note: Annotations created in the DataLabelingJob are associated with the EncryptionSpec of the Dataset they are exported to. |
`active_learning_config` |
Parameters that configure the active learning pipeline. Active learning will label the data incrementally via several iterations. For every iteration, it will select a batch of data based on the sampling strategy. |

## Classes

### AnnotationLabelsEntry

`AnnotationLabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DataLabelingJob

`DataLabelingJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


DataLabelingJob is used to trigger a human labeling job on unlabeled data from the following Dataset:


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesuploadragfileconfig_googlecloudaiplatform_v_7672ce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesuploadragfileconfig_googlecloudaiplatform_v1_a2923d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesuploadragfileconfig_googlecloudaiplatform_v1t_07a8de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesuploadragfileconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadRagFileConfig -->

# Class UploadRagFileConfig (1.134.0)

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.

## Attributes |
|
|---|---|
Name |
Description |
`rag_file_chunking_config` |
Specifies the size and overlap of chunks after uploading RagFile. |
`rag_file_transformation_config` |
Specifies the transformation config for RagFiles. |
`rag_file_metadata_config` |
Specifies the metadata config for RagFiles. Including paths for metadata schema and metadata. Alteratively, inline metadata schema and metadata can be provided. |
`rag_file_parsing_config` |
Optional. Specifies the parsing config for RagFiles. RAG will use the default parser if this field is not set. |

## Methods

### UploadRagFileConfig

`UploadRagFileConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for uploading RagFile.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritetensorboardexperimentdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteTensorboardExperimentDataRequest -->

# Class WriteTensorboardExperimentDataRequest (1.134.0)

```
WriteTensorboardExperimentDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardExperimentData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard_experiment` |
`str`
Required. The resource name of the TensorboardExperiment to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`write_run_data_requests` |
`MutableSequence[`
Required. Requests containing per-run TensorboardTimeSeries data to write. |

## Methods

### WriteTensorboardExperimentDataRequest

```
WriteTensorboardExperimentDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.WriteTensorboardExperimentData.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturevalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValue -->

# Class FeatureValue (1.134.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

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
`bool_value` |
`bool`
Bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
Double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_value` |
`int`
Int64 feature value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
String feature value. This field is a member of `oneof` _ `value` .
|
`bool_array_value` |
A list of bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_array_value` |
A list of double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_array_value` |
A list of int64 type feature value. This field is a member of `oneof` _ `value` .
|
`string_array_value` |
A list of string type feature value. This field is a member of `oneof` _ `value` .
|
`bytes_value` |
`bytes`
Bytes feature value. This field is a member of `oneof` _ `value` .
|
`struct_value` |
A struct type feature value. This field is a member of `oneof` _ `value` .
|
`metadata` |
Metadata of feature value. |

## Classes

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Methods

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecdatadriftspec_goo_c87235.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecdatadriftspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec.DataDriftSpec -->

# Class DataDriftSpec (1.134.0)

`DataDriftSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data drift monitoring spec. Data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.

## Attributes |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[str]`
Feature names / Prediction output names interested in monitoring. These should be a subset of the input feature names or prediction output names specified in the monitoring schema. If the field is not specified all features / prediction outputs outlied in the monitoring schema will be used. |
`categorical_metric_type` |
`str`
Supported metrics type: - l_infinity - jensen_shannon_divergence |
`numeric_metric_type` |
`str`
Supported metrics type: - jensen_shannon_divergence |
`default_categorical_alert_condition` |
Default alert condition for all the categorical features. |
`default_numeric_alert_condition` |
Default alert condition for all the numeric features. |
`feature_alert_conditions` |
`MutableMapping[str, `
Per feature alert condition will override default alert condition. |

## Classes

### FeatureAlertConditionsEntry

`FeatureAlertConditionsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DataDriftSpec

`DataDriftSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data drift monitoring spec. Data drift measures the distribution distance between the current dataset and a baseline dataset. A typical use case is to detect data drift between the recent production serving dataset and the training dataset, or to compare the recent production dataset with a dataset from a previous period.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturevalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValue -->

# Class FeatureValue (1.134.0)

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

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
`bool_value` |
`bool`
Bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_value` |
`float`
Double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_value` |
`int`
Int64 feature value. This field is a member of `oneof` _ `value` .
|
`string_value` |
`str`
String feature value. This field is a member of `oneof` _ `value` .
|
`bool_array_value` |
A list of bool type feature value. This field is a member of `oneof` _ `value` .
|
`double_array_value` |
A list of double type feature value. This field is a member of `oneof` _ `value` .
|
`int64_array_value` |
A list of int64 type feature value. This field is a member of `oneof` _ `value` .
|
`string_array_value` |
A list of string type feature value. This field is a member of `oneof` _ `value` .
|
`bytes_value` |
`bytes`
Bytes feature value. This field is a member of `oneof` _ `value` .
|
`struct_value` |
A struct type feature value. This field is a member of `oneof` _ `value` .
|
`metadata` |
Metadata of feature value. |

## Classes

### Metadata

`Metadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of feature value.

## Methods

### FeatureValue

`FeatureValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value for a feature.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicefeaturestoreserviceclient___fc2528.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicefeaturestoreserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient -->

# Class FeaturestoreServiceClient (1.134.0)

```
FeaturestoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


The service that handles CRUD and List for resources for Featurestore.

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
`FeaturestoreServiceTransport` |
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

### FeaturestoreServiceClient

```
FeaturestoreServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the featurestore service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,FeaturestoreServiceTransport,Callable[..., FeaturestoreServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeaturestoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### batch_create_features

```
batch_create_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.BatchCreateFeaturesRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
requests: typing.Optional[
typing.MutableSequence[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeatureRequest
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


Creates a batch of Features in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_create_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_batch_create_features)(request=request)
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
The request object. Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures. |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: |
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The |
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

### batch_read_feature_values

```
batch_read_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.BatchReadFeatureValuesRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[str] = None,
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


Batch reads Feature values from a Featurestore.

This API enables batch reading Feature values, where each read instance in the batch may read Feature values of entities from one or more EntityTypes. Point-in-time correctness is guaranteed for Feature values of each read instance as of each instance's read timestamp.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_batch_read_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
csv_read_instances = aiplatform_v1.[CsvSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CsvSource.html)()
csv_read_instances.gcs_source.uris = ['uris_value1', 'uris_value2']
destination = aiplatform_v1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
entity_type_specs = aiplatform_v1.[EntityTypeSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.EntityTypeSpec.html)()
entity_type_specs.entity_type_id = "entity_type_id_value"
entity_type_specs.feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1.[BatchReadFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadFeatureValuesRequest.html)(
csv_read_instances=csv_read_instances,
featurestore="featurestore_value",
destination=destination,
entity_type_specs=entity_type_specs,
)
# Make the request
operation = client.[batch_read_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_batch_read_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.BatchReadFeatureValues. |
`featurestore` |
`str`
Required. The resource name of the Featurestore from which to query Feature values. Format: |
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

### create_entity_type

```
create_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateEntityTypeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
entity_type: typing.Optional[
google.cloud.aiplatform_v1.types.entity_type.EntityType
] = None,
entity_type_id: typing.Optional[str] = None,
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


Creates a new EntityType in a given Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeRequest.html)(
parent="parent_value",
entity_type_id="entity_type_id_value",
)
# Make the request
operation = client.[create_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.CreateEntityType. |
`parent` |
`str`
Required. The resource name of the Featurestore to create EntityTypes. Format: |
`entity_type` |
The EntityType to create. This corresponds to the |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
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

### create_feature

```
create_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeatureRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature: typing.Optional[google.cloud.aiplatform_v1.types.feature.Feature] = None,
feature_id: typing.Optional[str] = None,
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


Creates a new Feature in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_feature)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature. |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: |
`feature` |
Required. The Feature to create. This corresponds to the |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are |
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

### create_featurestore

```
create_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.CreateFeaturestoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
featurestore: typing.Optional[
google.cloud.aiplatform_v1.types.featurestore.Featurestore
] = None,
featurestore_id: typing.Optional[str] = None,
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


Creates a new Featurestore in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeaturestoreRequest.html)(
parent="parent_value",
featurestore_id="featurestore_id_value",
)
# Make the request
operation = client.[create_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_create_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeaturestore. |
`parent` |
`str`
Required. The resource name of the Location to create Featurestores. Format: |
`featurestore` |
Required. The Featurestore to create. This corresponds to the |
`featurestore_id` |
`str`
Required. The ID to use for this Featurestore, which will become the final component of the Featurestore's resource name. This value may be up to 60 characters, and valid characters are |
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

### delete_entity_type

```
delete_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteEntityTypeRequest,
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


Deletes a single EntityType. The EntityType must not have any
Features or `force`

must be set to true for the request to
succeed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEntityTypeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteEntityType. |
`name` |
`str`
Required. The name of the EntityType to be deleted. Format: |
`force` |
`bool`
If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.) This corresponds to the |
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

### delete_feature

```
delete_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeatureRequest,
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


Deletes a single Feature.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_feature)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeature. Request message for FeatureRegistryService.DeleteFeature. |
`name` |
`str`
Required. The name of the Features to be deleted. Format: |
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

### delete_feature_values

```
delete_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Delete Feature values from Featurestore.

The progress of the deletion is tracked by the returned operation. The deleted feature values are guaranteed to be invisible to subsequent read operations after the operation is marked as successfully done.

If a delete feature values operation fails, the feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same delete request again and wait till the new operation returned is marked as successfully done.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
select_entity = aiplatform_v1.SelectEntity()
select_entity.entity_id_selector.csv_source.gcs_source.uris = ['uris_value1', 'uris_value2']
request = aiplatform_v1.[DeleteFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureValuesRequest.html)(
select_entity=select_entity,
entity_type="entity_type_value",
)
# Make the request
operation = client.[delete_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: |
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

### delete_featurestore

```
delete_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.DeleteFeaturestoreRequest,
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


Deletes a single Featurestore. The Featurestore must not contain
any EntityTypes or `force`

must be set to true for the request
to succeed.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_delete_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeaturestore. |
`name` |
`str`
Required. The name of the Featurestore to be deleted. Format: |
`force` |
`bool`
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) This corresponds to the |
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

### entity_type_path

```
entity_type_path(
project: str, location: str, featurestore: str, entity_type: str
) -> str
```


Returns a fully-qualified entity_type string.

### export_feature_values

```
export_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ExportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Exports Feature values from all the entities of a target EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_export_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
feature_selector = aiplatform_v1.[FeatureSelector](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureSelector.html)()
feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1.[ExportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest.html)(
entity_type="entity_type_value",
destination=destination,
feature_selector=feature_selector,
)
# Make the request
operation = client.[export_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_export_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ExportFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType from which to export Feature values. Format: |
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

### feature_path

```
feature_path(
project: str, location: str, featurestore: str, entity_type: str, feature: str
) -> str
```


Returns a fully-qualified feature string.

### featurestore_path

`featurestore_path(project: str, location: str, featurestore: str) -> str`


Returns a fully-qualified featurestore string.

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
`FeaturestoreServiceClient` |
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
`FeaturestoreServiceClient` |
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
`FeaturestoreServiceClient` |
The constructed client. |

### get_entity_type

```
get_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetEntityTypeRequest,
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
) -> google.cloud.aiplatform_v1.types.entity_type.EntityType
```


Gets details of a single EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEntityTypeRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetEntityType. |
`name` |
`str`
Required. The name of the EntityType resource. Format: |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

### get_feature

```
get_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetFeatureRequest,
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
) -> google.cloud.aiplatform_v1.types.feature.Feature
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
from google.cloud import aiplatform_v1
def sample_get_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetFeature. Request message for FeatureRegistryService.GetFeature. |
`name` |
`str`
Required. The name of the Feature resource. Format for entity_type as parent: |
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
Feature Metadata information. For example, color is a feature that describes an apple. |

### get_featurestore

```
get_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.GetFeaturestoreRequest,
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
) -> google.cloud.aiplatform_v1.types.featurestore.Featurestore
```


Gets details of a single Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_get_featurestore)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.GetFeaturestore. |
`name` |
`str`
Required. The name of the Featurestore resource. This corresponds to the |
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
Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values. |

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

### import_feature_values

```
import_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ImportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Imports Feature values into the Featurestore from a source storage. The progress of the import is tracked by the returned operation. The imported features are guaranteed to be visible to subsequent read operations after the operation is marked as successfully done.

If an import operation fails, the Feature values returned from reads and exports may be inconsistent. If consistency is required, the caller must retry the same import request again and wait till the new operation returned is marked as successfully done.

There are also scenarios where the caller can cause inconsistency.

- Source data for import contains multiple distinct Feature values for the same entity ID and timestamp.
- Source is modified during an import. This includes adding, updating, or removing source data and/or metadata. Examples of updating metadata include but are not limited to changing storage location, storage class, or retention policy.
- Online serving cluster is under-provisioned.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_import_feature_values():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
avro_source = aiplatform_v1.[AvroSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AvroSource.html)()
avro_source.gcs_source.uris = ['uris_value1', 'uris_value2']
feature_specs = aiplatform_v1.[FeatureSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest.FeatureSpec.html)()
feature_specs.id = "id_value"
request = aiplatform_v1.[ImportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ImportFeatureValuesRequest.html)(
avro_source=avro_source,
feature_time_field="feature_time_field_value",
entity_type="entity_type_value",
feature_specs=feature_specs,
)
# Make the request
operation = client.[import_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_import_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ImportFeatureValues. |
`entity_type` |
`str`
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: |
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

### list_entity_types

```
list_entity_types(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
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
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesPager
)
```


Lists EntityTypes in a given Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_entity_types():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEntityTypesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_entity_types](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_entity_types)(request=request)
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
The request object. Request message for FeaturestoreService.ListEntityTypes. |
`parent` |
`str`
Required. The resource name of the Featurestore to list EntityTypes. Format: |
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
Response message for FeaturestoreService.ListEntityTypes. Iterating over this object will yield results and resolve additional pages automatically. |

### list_features

```
list_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
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
) -> google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesPager
```


Lists Features in a given EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_features)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures. |
`parent` |
`str`
Required. The resource name of the Location to list Features. Format for entity_type as parent: |
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
Response message for FeaturestoreService.ListFeatures. Response message for FeatureRegistryService.ListFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

### list_featurestores

```
list_featurestores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
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
google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresPager
)
```


Lists Featurestores in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_featurestores():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturestoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_featurestores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_list_featurestores)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeaturestores. |
`parent` |
`str`
Required. The resource name of the Location to list Featurestores. Format: |
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
Response message for FeaturestoreService.ListFeaturestores. Iterating over this object will yield results and resolve additional pages automatically. |

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

### parse_entity_type_path

`parse_entity_type_path(path: str) -> typing.Dict[str, str]`


Parses a entity_type path into its component segments.

### parse_feature_path

`parse_feature_path(path: str) -> typing.Dict[str, str]`


Parses a feature path into its component segments.

### parse_featurestore_path

`parse_featurestore_path(path: str) -> typing.Dict[str, str]`


Parses a featurestore path into its component segments.

### search_features

```
search_features(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
dict,
]
] = None,
*,
location: typing.Optional[str] = None,
query: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesPager
)
```


Searches Features matching a query in a given project.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_search_features():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[SearchFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesRequest.html)(
location="location_value",
)
# Make the request
page_result = client.[search_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_search_features)(request=request)
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
The request object. Request message for FeaturestoreService.SearchFeatures. |
`location` |
`str`
Required. The resource name of the Location to search Features. Format: |
`query` |
`str`
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
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
Response message for FeaturestoreService.SearchFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_entity_type

```
update_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateEntityTypeRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[
google.cloud.aiplatform_v1.types.entity_type.EntityType
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
) -> google.cloud.aiplatform_v1.types.entity_type.EntityType
```


Updates the parameters of a single EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_entity_type():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEntityTypeRequest.html)(
)
# Make the request
response = client.[update_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.UpdateEntityType. |
`entity_type` |
Required. The EntityType's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

### update_feature

```
update_feature(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateFeatureRequest,
dict,
]
] = None,
*,
feature: typing.Optional[google.cloud.aiplatform_v1.types.feature.Feature] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.feature.Feature
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
from google.cloud import aiplatform_v1
def sample_update_feature():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest.html)(
)
# Make the request
response = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_feature)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeaturestoreService.UpdateFeature. Request message for FeatureRegistryService.UpdateFeature. |
`feature` |
Required. The Feature's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Features resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
Feature Metadata information. For example, color is a feature that describes an apple. |

### update_featurestore

```
update_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.featurestore_service.UpdateFeaturestoreRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[
google.cloud.aiplatform_v1.types.featurestore.Featurestore
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


Updates the parameters of a single Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_featurestore():
# Create a client
client = aiplatform_v1.
```[FeaturestoreServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreRequest.html)(
)
# Make the request
operation = client.[update_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.FeaturestoreServiceClient.html#google_cloud_aiplatform_v1_services_featurestore_service_FeaturestoreServiceClient_update_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.UpdateFeaturestore. |
`featurestore` |
Required. The Featurestore's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaipla_cb0c1f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaiplat_25597c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaiplatf_07cc27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaiplatfo_8b273a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaiplatfor_0dc1e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskdetailstate_googlecloudaiplatform_7385d4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskdetailstate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail.State -->

# Class State (1.134.0)

`State(value)`


Specifies state of TaskExecution

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Unspecified. |
`PENDING` |
Specifies pending state for the task. |
`RUNNING` |
Specifies task is being executed. |
`SUCCEEDED` |
Specifies task completed successfully. |
`CANCEL_PENDING` |
Specifies Task cancel is in pending state. |
`CANCELLING` |
Specifies task is being cancelled. |
`CANCELLED` |
Specifies task was cancelled. |
`FAILED` |
Specifies task failed. |
`SKIPPED` |
Specifies task was skipped due to cache hit. |
`NOT_TRIGGERED` |
Specifies that the task was not triggered because the task's trigger policy is not satisfied. The trigger policy is specified in the `condition` field of PipelineJob.pipeline_spec. |

## Methods

### State

`State(value)`


Specifies state of TaskExecution


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsfiltertabularstatsfilter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsFilter.TabularStatsFilter -->

# Class TabularStatsFilter (1.134.0)

`TabularStatsFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular statistics filter.

## Attributes |
|
|---|---|
Name |
Description |
`stats_name` |
`str`
If not specified, will return all the stats_names. |
`objective_type` |
`str`
One of the supported monitoring objectives: `raw-feature-drift` `prediction-output-drift`
`feature-attribution`
|
`model_monitoring_job` |
`str`
From a particular monitoring job. |
`model_monitoring_schedule` |
`str`
From a particular monitoring schedule. |
`algorithm` |
`str`
Specify the algorithm type used for distance calculation, eg: jensen_shannon_divergence, l_infinity. |

## Methods

### TabularStatsFilter

`TabularStatsFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular statistics filter.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig -->

# Class ModelMonitoringObjectiveConfig (1.134.0)

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset` |
Training dataset for models. This field has to be set only if TrainingPredictionSkewDetectionConfig is specified. |
`training_prediction_skew_detection_config` |
The config for skew between training data and prediction data. |
`prediction_drift_detection_config` |
The config for drift of prediction data. |
`explanation_config` |
The config for integrating with Vertex Explainable AI. |

## Classes

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

### PredictionDriftDetectionConfig

```
PredictionDriftDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Prediction data drift detection.

### TrainingDataset

`TrainingDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training Dataset information.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Methods

### ModelMonitoringObjectiveConfig

```
ModelMonitoringObjectiveConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The objective configuration for model monitoring, including the information needed to detect anomalies for one particular model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltable_d5cbd0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1typesautomltablesinputstransformationnumerictransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.NumericTransformation -->

# Class NumericTransformation (1.134.0)

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

## Attribute |
|
|---|---|
Name |
Description |
`invalid_values_allowed` |
`bool`
If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data. |

## Methods

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesruntimeconfigvertexaisearchruntimeconfig_goog_3ad892.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesruntimeconfigvertexaisearchruntimeconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RuntimeConfig.VertexAISearchRuntimeConfig -->

# Class VertexAISearchRuntimeConfig (1.134.0)

`VertexAISearchRuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`serving_config_name` |
`str`
Optional. Vertex AI Search serving config name. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}`
|
`engine_id` |
`str`
Optional. Vertex AI Search engine ID. This is used to construct the search request. By setting this engine_id, API will construct the serving config using the default value to call search API for the user. The engine_id and serving_config_name cannot both be empty at the same time. |

## Methods

### VertexAISearchRuntimeConfig

`VertexAISearchRuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesoutputconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for evaluation output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`gcs_destination` |
Cloud storage destination for evaluation output. This field is a member of `oneof` _ `destination` .
|

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for evaluation output.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchpredictionjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchPredictionJob -->

# Class BatchPredictionJob (1.134.0)

`BatchPredictionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the BatchPredictionJob. |
`display_name` |
`str`
Required. The user-defined name of this BatchPredictionJob. |
`model` |
`str`
The name of the Model resource that produces the predictions via this job, must share the same ancestor Location. Starting this job has no impact on any existing deployments of the Model and their resources. Exactly one of model and unmanaged_container_model must be set. The model resource name may contain version id or version alias to specify the version. Example: `projects/{project}/locations/{location}/models/{model}@2`
or
`projects/{project}/locations/{location}/models/{model}@golden`
if no version is specified, the default version will be
deployed.
The model resource could also be a publisher model. Example:
`publishers/{publisher}/models/{model}` or
`projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`
|
`model_version_id` |
`str`
Output only. The version ID of the Model that produces the predictions via this job. |
`unmanaged_container_model` |
Contains model information necessary to perform batch prediction without requiring uploading to model registry. Exactly one of model and unmanaged_container_model must be set. |
`input_config` |
Required. Input configuration of the instances on which predictions are performed. The schema of any single instance may be specified via the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`instance_config` |
Configuration for how to convert batch prediction input instances to the prediction instances that are sent to the Model. |
`model_parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the predictions. The schema of the parameters may be specified via the [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. |
`output_config` |
Required. The Configuration specifying where output predictions should be written. The schema of any single prediction may be specified as a concatenation of [Model's][google.cloud.aiplatform.v1beta1.BatchPredictionJob.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri and prediction_schema_uri. |
`dedicated_resources` |
The config of resources used by the Model during the batch prediction. If the Model supports DEDICATED_RESOURCES this config may be provided (and the job will use these resources), if the Model doesn't support AUTOMATIC_RESOURCES, this config must be provided. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. If not specified, a system generated one will be used, which has minimal permissions and the custom container, if used, may not have enough permission to access other Google Cloud resources. Users deploying the Model must have the `iam.serviceAccounts.actAs` permission on this service
account.
|
`manual_batch_tuning_parameters` |
Immutable. Parameters configuring the batch behavior. Currently only applicable when dedicated_resources are used (in other cases Vertex AI does the tuning itself). |
`generate_explanation` |
`bool`
Generate explanation with the batch prediction results. When set to `true` , the batch prediction output changes
based on the `predictions_format` field of the
BatchPredictionJob.output_config
object:
- `bigquery` : output includes a column named
`explanation` . The value is a struct that conforms to
the
Explanation
object.
- `jsonl` : The JSON objects on each line include an
additional entry keyed `explanation` . The value of the
entry is a JSON object that conforms to the
Explanation
object.
- `csv` : Generating explanations for CSV format is not
supported.
If this field is set to true, either the
Model.explanation_spec
or
explanation_spec
must be populated.
|
`explanation_spec` |
Explanation configuration for this BatchPredictionJob. Can be specified only if generate_explanation is set to `true` .
This value overrides the value of
Model.explanation_spec.
All fields of
explanation_spec
are optional in the request. If a field of the
explanation_spec
object is not populated, the corresponding field of the
Model.explanation_spec
object is inherited.
|
`output_info` |
Output only. Information further describing the output of this job. |
`state` |
Output only. The detailed state of the job. |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED. |
`partial_failures` |
`MutableSequence[google.rpc.status_pb2.Status]`
Output only. Partial failures encountered. For example, single files that can't be read. This field never exceeds 20 entries. Status details fields contain standard Google Cloud error details. |
`resources_consumed` |
Output only. Information about resources that had been consumed by this job. Provided in real time at best effort basis, as well as a final value once the job completes. Note: This field currently may be not populated for batch predictions that use AutoML Models. |
`completion_stats` |
Output only. Statistics on completed and failed prediction instances. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob was created. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob for the first time entered the `JOB_STATE_RUNNING` state.
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob entered any of the following states: `JOB_STATE_SUCCEEDED` ,
`JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .
|
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the BatchPredictionJob was most recently updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`encryption_spec` |
Customer-managed encryption key options for a BatchPredictionJob. If this is set, then all resources created by the BatchPredictionJob will be encrypted with the provided encryption key. |
`model_monitoring_config` |
Model monitoring config will be used for analysis model behaviors, based on the input and output to the batch prediction job, as well as the provided training dataset. |
`model_monitoring_stats_anomalies` |
`MutableSequence[`
Get batch prediction job monitoring statistics. |
`model_monitoring_status` |
`google.rpc.status_pb2.Status`
Output only. The running status of the model monitoring pipeline. |
`disable_container_logging` |
`bool`
For custom-trained Models and AutoML Tabular Models, the container of the DeployedModel instances will send `stderr` and `stdout` streams to Cloud Logging by
default. Please note that the logs incur cost, which are
subject to `Cloud Logging
pricing |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Classes

### InputConfig

`InputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the input to BatchPredictionJob. See Model.supported_input_storage_formats for Model's supported input formats, and how instances should be expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### InstanceConfig

`InstanceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration defining how to transform batch prediction input instances to the instances that the Model accepts.

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

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configures the output of BatchPredictionJob. See Model.supported_output_storage_formats for supported output formats, and how predictions are expressed via any of them.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OutputInfo

`OutputInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Further describes this job's output. Supplements output_config.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### BatchPredictionJob

`BatchPredictionJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A job that uses a Model to produce predictions on multiple [input instances][google.cloud.aiplatform.v1beta1.BatchPredictionJob.input_config]. If predictions for significant portion of the instances fail, the job may finish without attempting predictions for all remaining instances.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesupdateartifactrequest_googlecloudaiplatform_v1s_2dd861.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesupdateartifactrequest_googlecloudaiplatform_v1se_868121.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdateartifactrequest_googlecloudaiplatform_v1ser_4e5fe8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdateartifactrequest_googlecloudaiplatform_v1serv_dafba3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdateartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateArtifactRequest -->

# Class UpdateArtifactRequest (1.134.0)

`UpdateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
Required. The Artifact containing updates. The Artifact's Artifact.name field is used to identify the Artifact to be updated. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. |
`allow_missing` |
`bool`
If set to true, and the Artifact is not found, a new Artifact is created. |

## Methods

### UpdateArtifactRequest

`UpdateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateArtifact.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service -->

# Package schedule_service (1.134.0)

API documentation for `aiplatform_v1.services.schedule_service`

package.

## Classes

[ScheduleServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient)

A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

[ScheduleServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient)

A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers)

API documentation for `aiplatform_v1.services.schedule_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextsentimentpred_ec5696.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextsentimentpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextSentimentPredictionInstance -->

# Class TextSentimentPredictionInstance (1.134.0)

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The text snippet to make the predictions on. |
`mime_type` |
`str`
The MIME type of the text snippet. The supported MIME types are listed below. - text/plain |

## Methods

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.

### TextSentimentPredictionInstance

```
TextSentimentPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Sentiment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespurgeartifactsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PurgeArtifactsRequest -->

# Class PurgeArtifactsRequest (1.134.0)

`PurgeArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeArtifacts.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The metadata store to purge Artifacts from. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`filter` |
`str`
Required. A required filter matching the Artifacts to be purged. E.g., `update_time <=>` .
|
`force` |
`bool`
Optional. Flag to indicate to actually perform the purge. If `force` is set to false, the method will return a sample
of Artifact names that would be deleted.
|

## Methods

### PurgeArtifactsRequest

`PurgeArtifactsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.PurgeArtifacts.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesbleumetricvalue_googlecloudaiplatform_v1typesmigr_57d4de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesbleumetricvalue_googlecloudaiplatform_v1typesmigra_39b1c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbleumetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BleuMetricValue -->

# Class BleuMetricValue (1.134.0)

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Bleu score. This field is a member of `oneof` _ `_score` .
|

## Methods

### BleuMetricValue

`BleuMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Bleu metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmigrateresourcerequestmigratedatalabelingdatasetconfigmigratedatalabelingannotateddatasetconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MigrateResourceRequest.MigrateDataLabelingDatasetConfig.MigrateDataLabelingAnnotatedDatasetConfig -->

# Class MigrateDataLabelingAnnotatedDatasetConfig (1.134.0)

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.

## Attribute |
|
|---|---|
Name |
Description |
`annotated_dataset` |
`str`
Required. Full resource name of data labeling AnnotatedDataset. Format: `projects/{project}/datasets/{dataset}/annotatedDatasets/{annotated_dataset}` .
|

## Methods

### MigrateDataLabelingAnnotatedDatasetConfig

```
MigrateDataLabelingAnnotatedDatasetConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Config for migrating AnnotatedDataset in datalabeling.googleapis.com to Vertex AI's SavedQuery.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistindexesrequest_googlecloudaiplatform_v1beta1se_586803.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistindexesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexesRequest -->

# Class ListIndexesRequest (1.134.0)

`ListIndexesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ListIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the Indexes. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListIndexesResponse.next_page_token of the previous IndexService.ListIndexes call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListIndexesRequest

`ListIndexesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ListIndexes.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_registry_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service -->

# Package extension_registry_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.extension_registry_service`

package.

## Classes

[ExtensionRegistryServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceAsyncClient)

A service for managing Vertex AI's Extension registry.

[ExtensionRegistryServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.ExtensionRegistryServiceClient)

A service for managing Vertex AI's Extension registry.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers)

API documentation for `aiplatform_v1beta1.services.extension_registry_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schemapredictprediction_v1typesvideoclassificationpredi_064527.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictprediction_v1typesvideoclassificationpredic_c3d862.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typesvideoclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoClassificationPredictionResult -->

# Class VideoClassificationPredictionResult (1.134.0)

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`type_` |
`str`
The type of the prediction. The requested types can be configured via parameters. This will be one of - segment-classification - shot-classification - one-sec-interval-classification |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentStart' from the input instance, for other types it is the start of a shot or a 1 second interval respectively. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentEnd' from the input instance, for other types it is the end of a shot or a 1 second interval respectively. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |

## Methods

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistindexesrequest_googlecloudaiplatform_v1be_37551f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistindexesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesRequest -->

# Class ListIndexesRequest (1.134.0)

`ListIndexesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ListIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the Indexes. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListIndexesResponse.next_page_token of the previous IndexService.ListIndexes call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListIndexesRequest

`ListIndexesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ListIndexes.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdateartifactrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateArtifactRequest -->

# Class UpdateArtifactRequest (1.134.0)

`UpdateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateArtifact.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
Required. The Artifact containing updates. The Artifact's Artifact.name field is used to identify the Artifact to be updated. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. |
`allow_missing` |
`bool`
If set to true, and the Artifact is not found, a new Artifact is created. |

## Methods

### UpdateArtifactRequest

`UpdateArtifactRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.UpdateArtifact.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatedeploymentresourcepoolrequest_googlecloudai_d7f5dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatedeploymentresourcepoolrequest_googlecloudaip_3ae539.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatedeploymentresourcepoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateDeploymentResourcePoolRequest -->

# Class UpdateDeploymentResourcePoolRequest (1.134.0)

```
UpdateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdateDeploymentResourcePool method.

## Attributes |
|
|---|---|
Name |
Description |
`deployment_resource_pool` |
Required. The DeploymentResourcePool to update. The DeploymentResourcePool's `name` field is used to
identify the DeploymentResourcePool to update. Format:
`projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateDeploymentResourcePoolRequest

```
UpdateDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for UpdateDeploymentResourcePool method.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestoreembeddingmanagement.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.EmbeddingManagement -->

# Class EmbeddingManagement (1.134.0)

`EmbeddingManagement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated: This sub message is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. Contains settings for embedding management.

## Attribute |
|
|---|---|
Name |
Description |
`enabled` |
`bool`
Optional. Immutable. Whether to enable embedding management in this FeatureOnlineStore. It's immutable after creation to ensure the FeatureOnlineStore availability. |

## Methods

### EmbeddingManagement

`EmbeddingManagement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated: This sub message is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. Contains settings for embedding management.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdataitem.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DataItem -->

# Class DataItem (1.134.0)

`DataItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A piece of data in a Dataset. Could be an image, a video, a document or plain text.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the DataItem. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataItem was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DataItem was last updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your DataItems. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one DataItem(System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`payload` |
`google.protobuf.struct_pb2.Value`
Required. The data that the DataItem represents (for example, an image or a text snippet). The schema of the payload is stored in the parent Dataset's [metadata schema's][google.cloud.aiplatform.v1.Dataset.metadata_schema_uri] dataItemSchemaUri field. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
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

### DataItem

`DataItem(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A piece of data in a Dataset. Could be an image, a video, a document or plain text.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformcustomjob___googlecloudaiplatform_v1beta1typesfeatureonlin_31b852.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformcustomjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob -->

# Class CustomJob (1.134.0)

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Vertex AI Custom Job.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Time when the Job resource entered the `JOB_STATE_SUCCEEDED`

,
`JOB_STATE_FAILED`

, or `JOB_STATE_CANCELLED`

state.

### error

Detailed error info for this Job resource. Only populated when the
Job's state is `JOB_STATE_FAILED`

or `JOB_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### network

The full name of the Google Compute Engine
[network](https://cloud.google.com/vpc/docs/vpc#networks) to which this
CustomJob should be peered.

Takes the format `projects/{project}/global/networks/{network}`

. Where
{project} is a project number, as in `12345`

, and {network} is a network name.

Private services access must already be configured for the network. If left unspecified, the CustomJob is not peered with any network.

### preview

Exposes features available in preview for this class.

### resource_name

Full qualified resource name.

### start_time

Time when the Job resource entered the `JOB_STATE_RUNNING`

for the
first time.

### state

Fetch Job again and return the current JobState.

Returns |
|
|---|---|
Type |
Description |
`state (job_state.JobState)` |
Enum that describes the state of a Vertex AI job. |

### update_time

Time this resource was last updated.

### web_access_uris

Fetch the runnable job again and return the latest web access uris.

Returns |
|
|---|---|
Type |
Description |
`(Dict[str, Union[str, Dict[str, str]]])` |
Web access uris of the runnable job. |

## Methods

### CustomJob

```
CustomJob(
display_name: str,
worker_pool_specs: typing.Union[
typing.List[typing.Dict],
typing.List[google.cloud.aiplatform_v1.types.custom_job.WorkerPoolSpec],
],
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
)
```


Constructs a Custom Job with Worker Pool Specs.

```
Example usage:
worker_pool_specs = [
{
"machine_spec": {
"machine_type": "n1-standard-4",
"accelerator_type": "NVIDIA_TESLA_K80",
"accelerator_count": 1,
},
"replica_count": 1,
"container_spec": {
"image_uri": container_image_uri,
"command": [],
"args": [],
},
}
]
my_job = aiplatform.CustomJob(
display_name='my_job',
worker_pool_specs=worker_pool_specs,
labels={'my_key': 'my_value'},
)
my_job.run()
```


For more information on configuring worker pool specs please visit:
[https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job](https://cloud.google.com/ai-platform-unified/docs/training/create-custom-job)

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of the HyperparameterTuningJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`worker_pool_specs` |
`Union[List[Dict], List[aiplatform.gapic.WorkerPoolSpec]]`
Required. The spec of the worker pools including machine type and Docker image. Can provided as a list of dictionaries or list of WorkerPoolSpec proto messages. |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional.Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional.Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional.Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional.Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network and CMEK configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

### cancel

`cancel() -> None`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### from_local_script

```
from_local_script(
display_name: str,
script_path: str,
container_uri: str,
enable_autolog: bool = False,
args: typing.Optional[typing.Sequence[str]] = None,
requirements: typing.Optional[typing.Sequence[str]] = None,
environment_variables: typing.Optional[typing.Dict[str, str]] = None,
replica_count: int = 1,
machine_type: str = "n1-standard-4",
accelerator_type: str = "ACCELERATOR_TYPE_UNSPECIFIED",
accelerator_count: int = 0,
boot_disk_type: str = "pd-ssd",
boot_disk_size_gb: int = 100,
reduction_server_replica_count: int = 0,
reduction_server_machine_type: typing.Optional[str] = None,
reduction_server_container_uri: typing.Optional[str] = None,
base_output_dir: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
persistent_resource_id: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.CustomJob
```


Configures a custom job from a local script.

Example usage:

```
job = aiplatform.CustomJob.from_local_script(
display_name="my-custom-job",
script_path="training_script.py",
container_uri="gcr.io/cloud-aiplatform/training/tf-cpu.2-2:latest",
requirements=["gcsfs==0.7.1"],
replica_count=1,
args=['--dataset', 'gs://my-bucket/my-dataset',
'--model_output_uri', 'gs://my-bucket/model']
labels={'my_key': 'my_value'},
)
job.run()
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The user-defined name of this CustomJob. |
`script_path` |
`str`
Required. Local path to training script. |
`container_uri` |
`str`
Required. Uri of the training container image to use for custom job. Support images in Artifact Registry, Container Registry, or Docker Hub. Vertex AI provides a wide range of executor images with pre-installed packages to meet users' various use cases. See the list of |
`enable_autolog` |
`bool`
Optional. If True, the Vertex Experiments autologging feature will be enabled in the CustomJob. Note that this will wrap your training script with some autologging-related code. |
`args` |
`Optional[Sequence[str]]`
Optional. Command line arguments to be passed to the Python task. |
`requirements` |
`Sequence[str]`
Optional. List of python packages dependencies of script. |
`environment_variables` |
`Dict[str, str]`
Optional. Environment variables to be passed to the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. At most 10 environment variables can be specified. The Name of the environment variable must be unique. environment_variables = { 'MY_KEY': 'MY_VALUE' } |
`replica_count` |
`int`
Optional. The number of worker replicas. If replica count = 1 then one chief replica will be provisioned. If replica_count > 1 the remainder will be provisioned as a worker replica pool. |
`machine_type` |
`str`
Optional. The type of machine to use for training. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`boot_disk_type` |
`str`
Optional. Type of the boot disk, default is |
`boot_disk_size_gb` |
`int`
Optional. Size in GB of the boot disk, default is 100GB. boot disk size must be within the range of [100, 64000]. |
`reduction_server_replica_count` |
`int`
The number of reduction server replicas, default is 0. |
`reduction_server_machine_type` |
`str`
Optional. The type of machine to use for reduction server. |
`reduction_server_container_uri` |
`str`
Optional. The Uri of the reduction server container image. See details: |
`base_output_dir` |
`str`
Optional. GCS output directory of job. If not provided a timestamped directory in the staging directory will be used. |
`project` |
`str`
Optional. Project to run the custom job in. Overrides project set in aiplatform.init. |
`location` |
`str`
Optional. Location to run the custom job in. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to run call custom job service. Overrides credentials set in aiplatform.init. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize CustomJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key name for a CustomJob. If this is set, then all resources created by the CustomJob will be encrypted with the provided encryption key. |
`staging_bucket` |
`str`
Optional. Bucket for produced custom job artifacts. Overrides staging_bucket set in aiplatform.init. |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`tpu_topology` |
`str`
Optional. Specifies the tpu topology to be used for TPU training job. This field is required for TPU v5 versions. For details on the TPU topology, refer to |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If staging bucket was not set using aiplatform.init and a staging bucket was not passed in. |

### get

```
get(
resource_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> google.cloud.aiplatform.jobs._RunnableJob
```


Get a Vertex AI Job for the given resource_name.

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
Optional. project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to upload this model. Overrides credentials set in aiplatform.init. |

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


List all instances of this Job Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

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
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None,
) -> None
```


Run this configured CustomJob.

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
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will unblock and it will be executed in a concurrent Future. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

### submit

```
submit(
*,
service_account: typing.Optional[str] = None,
network: typing.Optional[str] = None,
timeout: typing.Optional[int] = None,
restart_job_on_worker_restart: bool = False,
enable_web_access: bool = False,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
experiment_run: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun, str
]
] = None,
tensorboard: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
disable_retries: bool = False,
persistent_resource_id: typing.Optional[str] = None,
scheduling_strategy: typing.Optional[
google.cloud.aiplatform_v1.types.custom_job.Scheduling.Strategy
] = None,
max_wait_duration: typing.Optional[int] = None,
psc_interface_config: typing.Optional[
google.cloud.aiplatform_v1.types.service_networking.PscInterfaceConfig
] = None
) -> None
```


Submit the configured CustomJob.

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
Optional. The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. |
`timeout` |
`int`
The maximum job running time in seconds. The default is 7 days. |
`restart_job_on_worker_restart` |
`bool`
Restarts the entire CustomJob if a worker gets restarted. This feature can be used by distributed training jobs that are not resilient to workers leaving and joining a job. |
`enable_web_access` |
`bool`
Whether you want Vertex AI to enable interactive shell access to training containers. |
`experiment` |
`Union[aiplatform.Experiment, str]`
Optional. The instance or name of an Experiment resource to which this CustomJob will upload training parameters and metrics. |
`experiment_run` |
`Union[aiplatform.ExperimentRun, str]`
Optional. The instance or name of an ExperimentRun resource to which this CustomJob will upload training parameters and metrics. This arg can only be set when |
`tensorboard` |
`str`
Optional. The name of a Vertex AI Tensorboard resource to which this CustomJob will upload Tensorboard logs. Format: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`disable_retries` |
`bool`
Indicates if the job should retry for internal errors after the job starts running. If True, overrides |
`persistent_resource_id` |
`str`
Optional. The ID of the PersistentResource in the same Project and Location. If this is specified, the job will be run on existing machines held by the PersistentResource instead of on-demand short-live machines. The network, CMEK, and node pool configs on the job should be consistent with those on the PersistentResource, otherwise, the job will be rejected. |
`scheduling_strategy` |
`gca_custom_job_compat.Scheduling.Strategy`
Optional. Indicates the job scheduling strategy. |
`max_wait_duration` |
`int`
This is the maximum duration that a job will wait for the requested resources to be provisioned in seconds. If set to 0, the job will wait indefinitely. The default is 1 day. |
`psc_interface_config` |
`gca_service_networking.PscInterfaceConfig`
Optional. Configuration for Private Service Connect interface used for training. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both `experiment` and `tensorboard` are specified or if `enable_autolog` is True in `CustomJob.from_local_script` but `experiment` is not specified or the specified experiment doesn't have a backing tensorboard. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_completion

`wait_for_completion() -> None`


Waits for job to complete.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If job failed or cancelled. |

### wait_for_resource_creation

`wait_for_resource_creation() -> None`


Waits until resource has been created.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeatureonlinestore_googlecloudaiplatform_v1b_6d651b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureonlinestore_googlecloudaiplatform_v1be_14dbce.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestore.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore -->

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
`embedding_management` |
Optional. Deprecated: This field is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. |
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

### EmbeddingManagement

`EmbeddingManagement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Deprecated: This sub message is no longer needed anymore and embedding management is automatically enabled when specifying Optimized storage type. Contains settings for embedding management.

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluationslicesliceslicespecsliceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice.SliceSpec.SliceConfig -->

# Class SliceConfig (1.134.0)

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

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
`value` |
A unique specific value for a given feature. Example: `{ "value": { "string_value": "12345" } }`
This field is a member of `oneof` _ `kind` .
|
`range_` |
A range of values for a numerical feature. Example: `{"range":{"low":10000.0,"high":50000.0}}` will capture
12345 and 23334 in the slice.
This field is a member of `oneof` _ `kind` .
|
`all_values` |
`google.protobuf.wrappers_pb2.BoolValue`
If all_values is set to true, then all possible labels of the keyed feature will have another slice computed. Example: `{"all_values":{"value":true}}`
This field is a member of `oneof` _ `kind` .
|

## Methods

### SliceConfig

`SliceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification message containing the config for this SliceSpec. When
`kind`

is selected as `value`

and/or `range`

, only a single
slice will be computed. When `all_values`

is present, a separate
slice will be computed for each possible label/value for the
corresponding key in `config`

. Examples, with feature zip_code
with values 12345, 23334, 88888 and feature country with values
"US", "Canada", "Mexico" in the dataset:

Example 1:

::

```
{
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


A single slice for any data with zip_code 12345 in the dataset.

Example 2:

::

```
{
"zip_code": { "range": { "low": 12345, "high": 20000 } }
}
```


A single slice containing data where the zip_codes between 12345 and 20000 For this example, data with the zip_code of 12345 will be in this slice.

Example 3:

::

```
{
"zip_code": { "range": { "low": 10000, "high": 20000 } },
"country": { "value": { "string_value": "US" } }
}
```


A single slice containing data where the zip_codes between 10000 and 20000 has the country "US". For this example, data with the zip_code of 12345 and country "US" will be in this slice.

Example 4:

::

```
{ "country": {"all_values": { "value": true } } }
```


Three slices are computed, one for each unique country in the dataset.

Example 5:

::

```
{
"country": { "all_values": { "value": true } },
"zip_code": { "value": { "float_value": 12345.0 } }
}
```


Three slices are computed, one for each unique country in the dataset where the zip_code is also 12345. For this example, data with zip_code 12345 and country "US" will be in one slice, zip_code 12345 and country "Canada" in another slice, and zip_code 12345 and country "Mexico" in another slice, totaling 3 slices.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typescreatenotebookruntimetemplaterequest_google_a9b3f1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreatenotebookruntimetemplaterequest_googlec_75d8cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatenotebookruntimetemplaterequest_googlecl_67654c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateNotebookRuntimeTemplateRequest -->

# Class CreateNotebookRuntimeTemplateRequest (1.134.0)

```
CreateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.CreateNotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: `projects/{project}/locations/{location}`
|
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to create. |
`notebook_runtime_template_id` |
`str`
Optional. User specified ID for the notebook runtime template. |

## Methods

### CreateNotebookRuntimeTemplateRequest

```
CreateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.CreateNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgroundingmetadatasourceflagginguri.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingMetadata.SourceFlaggingUri -->

# Class SourceFlaggingUri (1.134.0)

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.

## Attributes |
|
|---|---|
Name |
Description |
`source_id` |
`str`
Id of the place or review. |
`flag_content_uri` |
`str`
A link where users can flag a problem with the source (place or review). (-- The link is generated by Google and it does not contain information from the user query. It may contain information of the content it is flagging, which can be used to identify places. --) |

## Methods

### SourceFlaggingUri

`SourceFlaggingUri(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Source content flagging uri for a place or review. This is currently populated only for Google Maps grounding.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputmetadataoverr_5eace2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationmetadataoverrideinputmetadataoverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadataOverride.InputMetadataOverride -->

# Class InputMetadataOverride (1.134.0)

`InputMetadataOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The [input metadata][google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata] entries to be overridden.

## Attribute |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. This overrides the `input_baseline` field of the
ExplanationMetadata.InputMetadata
object of the corresponding feature's input metadata. If
it's not specified, the original baselines are not
overridden.
|

## Methods

### InputMetadataOverride

`InputMetadataOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The [input metadata][google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata] entries to be overridden.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescoherenceinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CoherenceInstance -->

# Class CoherenceInstance (1.134.0)

`CoherenceInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|

## Methods

### CoherenceInstance

`CoherenceInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for coherence instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesvideoclassifica_2ebb38.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typesvideoclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoClassificationPredictionResult -->

# Class VideoClassificationPredictionResult (1.134.0)

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
The resource ID of the AnnotationSpec that had been identified. |
`display_name` |
`str`
The display name of the AnnotationSpec that had been identified. |
`type_` |
`str`
The type of the prediction. The requested types can be configured via parameters. This will be one of - segment-classification - shot-classification - one-sec-interval-classification |
`time_segment_start` |
`google.protobuf.duration_pb2.Duration`
The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentStart' from the input instance, for other types it is the start of a shot or a 1 second interval respectively. |
`time_segment_end` |
`google.protobuf.duration_pb2.Duration`
The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentEnd' from the input instance, for other types it is the end of a shot or a 1 second interval respectively. |
`confidence` |
`google.protobuf.wrappers_pb2.FloatValue`
The Model's confidence in correction of this prediction, higher value means higher confidence. |

## Methods

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.

### VideoClassificationPredictionResult

```
VideoClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Video Classification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnotebookidleshutdownconfig_googlecloudaiplatf_1e9dd6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookidleshutdownconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookIdleShutdownConfig -->

# Class NotebookIdleShutdownConfig (1.134.0)

`NotebookIdleShutdownConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idle_timeout as required field.

## Attributes |
|
|---|---|
Name |
Description |
`idle_timeout` |
`google.protobuf.duration_pb2.Duration`
Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idle_timeout (second) is: 10 \* 60 ` 1440 - 60. |
`idle_shutdown_disabled` |
`bool`
Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate. |

## Methods

### NotebookIdleShutdownConfig

`NotebookIdleShutdownConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The idle shutdown configuration of NotebookRuntimeTemplate, which contains the idle_timeout as required field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragretrievalconfigrankingllmranker.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.Ranking.LlmRanker -->

# Class LlmRanker (1.134.0)

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Optional. The model name used for ranking. Format: `gemini-1.5-pro`
This field is a member of `oneof` _ `_model_name` .
|

## Methods

### LlmRanker

`LlmRanker(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for LlmRanker.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
