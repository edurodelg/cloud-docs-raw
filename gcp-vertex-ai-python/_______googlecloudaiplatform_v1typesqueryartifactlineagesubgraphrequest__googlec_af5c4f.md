---
merged_at: 2026-01-25T21:47:44.374442
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googlecl_8c95f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googleclo_c13f74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googleclou_b41ad2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googlecloud_83c4ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googleclouda_99390b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest__googlecloudai_6eeb30.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesqueryartifactlineagesubgraphrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryArtifactLineageSubgraphRequest -->

# Class QueryArtifactLineageSubgraphRequest (1.134.0)

```
QueryArtifactLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryArtifactLineageSubgraph.

## Attributes |
|
|---|---|
Name |
Description |
`artifact` |
`str`
Required. The resource name of the Artifact whose Lineage needs to be retrieved as a LineageSubgraph. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/artifacts/{artifact}`
The request may error with FAILED_PRECONDITION if the number
of Artifacts, the number of Executions, or the number of
Events that would be returned for the Context exceeds 1000.
|
`max_hops` |
`int`
Specifies the size of the lineage graph in terms of number of hops from the specified artifact. Negative Value: INVALID_ARGUMENT error is returned 0: Only input artifact is returned. No value: Transitive closure is performed to return the complete graph. |
`filter` |
`str`
Filter specifying the boolean condition for the Artifacts to satisfy in order to be part of the Lineage Subgraph. The syntax to define filter query is based on https://google.aip.dev/160. The supported set of filters include the following: - **Attribute filtering**: For example: `display_name = "test"` Supported fields include:
`name` , `display_name` , `uri` , `state` ,
`schema_title` , `create_time` , and `update_time` .
Time fields, such as `create_time` and `update_time` ,
require values specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"`
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` In case the field
name contains special characters (such as colon), one can
embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
Each of the above supported filter types can be combined
together using logical operators (`AND` & `OR` ). Maximum
nested expression depth allowed is 5.
For example:
`display_name = "test" AND metadata.field1.bool_value = true` .
|

## Methods

### QueryArtifactLineageSubgraphRequest

```
QueryArtifactLineageSubgraphRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MetadataService.QueryArtifactLineageSubgraph.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesauthconfiggoogleserviceaccountconfig_googlecl_7eb29b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesauthconfiggoogleserviceaccountconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig.GoogleServiceAccountConfig -->

# Class GoogleServiceAccountConfig (1.134.0)

`GoogleServiceAccountConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Google Service Account Authentication.

## Attribute |
|
|---|---|
Name |
Description |
`service_account` |
`str`
Optional. The service account that the extension execution service runs as. - If the service account is specified, the `iam.serviceAccounts.getAccessToken` permission should
be granted to Vertex AI Extension Service Agent
(https://cloud.google.com/vertex-ai/docs/general/access-control#service-agents)
on the specified service account.
- If not specified, the Vertex AI Extension Service Agent
will be used to execute the Extension.
|

## Methods

### GoogleServiceAccountConfig

`GoogleServiceAccountConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Google Service Account Authentication.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexactmatchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExactMatchMetricValue -->

# Class ExactMatchMetricValue (1.134.0)

`ExactMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Exact match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Exact match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ExactMatchMetricValue

`ExactMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Exact match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schemapredictprediction_v1typestabularregressionpredict_af8cad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictprediction_v1typestabularregressionpredicti_14a549.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typestabularregressionpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularRegressionPredictionResult -->

# Class TabularRegressionPredictionResult (1.134.0)

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.

## Attributes |
|
|---|---|
Name |
Description |
`value` |
`float`
The regression value. |
`lower_bound` |
`float`
The lower bound of the prediction interval. |
`upper_bound` |
`float`
The upper bound of the prediction interval. |

## Methods

### TabularRegressionPredictionResult

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.

### TabularRegressionPredictionResult

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescheckpublishermodeleulaacceptancerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CheckPublisherModelEulaAcceptanceRequest -->

# Class CheckPublisherModelEulaAcceptanceRequest (1.134.0)

```
CheckPublisherModelEulaAcceptanceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ModelGardenService.CheckPublisherModelEula][].

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The project requesting access for named model. The format is `projects/{project}` .
|
`publisher_model` |
`str`
Required. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}` , or
`publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}`
|

## Methods

### CheckPublisherModelEulaAcceptanceRequest

```
CheckPublisherModelEulaAcceptanceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [ModelGardenService.CheckPublisherModelEula][].


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnearestneighborqueryparameters_googlecloudaip_151fc9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnearestneighborqueryparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighborQuery.Parameters -->

# Class Parameters (1.134.0)

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided in each query to tune query latency and recall.

## Attributes |
|
|---|---|
Name |
Description |
`approximate_neighbor_candidates` |
`int`
Optional. The number of neighbors to find via approximate search before exact reordering is performed; if set, this value must be > neighbor_count. |
`leaf_nodes_search_fraction` |
`float`
Optional. The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. |

## Methods

### Parameters

`Parameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters that can be overrided in each query to tune query latency and recall.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluationsliceslice.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluationSlice.Slice -->

# Class Slice (1.134.0)

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.

## Attributes |
|
|---|---|
Name |
Description |
`dimension` |
`str`
Output only. The dimension of the slice. Well-known dimensions are: - `annotationSpec` : This slice is on the test data that
has either ground truth or prediction with
AnnotationSpec.display_name
equals to
value.
- `slice` : This slice is a user customized slice defined
by its SliceSpec.
|
`value` |
`str`
Output only. The value of the dimension in this slice. |
`slice_spec` |
Output only. Specification for how the data was sliced. |

## Classes

### SliceSpec

`SliceSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for how the data should be sliced.

## Methods

### Slice

`Slice(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Definition of a slice.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesdeployrequestendpointconfig__googlecloudaiplatfor_265242.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesdeployrequestendpointconfig__googlecloudaiplatform_9b82be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployrequestendpointconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.EndpointConfig -->

# Class EndpointConfig (1.134.0)

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint_display_name` |
`str`
Optional. The user-specified display name of the endpoint. If not set, a default name will be used. |
`dedicated_endpoint_enabled` |
`bool`
Optional. Deprecated. Use dedicated_endpoint_disabled instead. If true, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. |
`dedicated_endpoint_disabled` |
`bool`
Optional. By default, if dedicated endpoint is enabled, the endpoint will be exposed through a dedicated DNS [Endpoint.dedicated_endpoint_dns]. Your request to the dedicated DNS will be isolated from other users' traffic and will have better performance and reliability. Note: Once you enabled dedicated endpoint, you won't be able to send request to the shared DNS {region}-aiplatform.googleapis.com. The limitations will be removed soon. If this field is set to true, the dedicated endpoint will be disabled and the deployed model will be exposed through the shared DNS {region}-aiplatform.googleapis.com. |
`endpoint_user_id` |
`str`
Optional. Immutable. The ID to use for endpoint, which will become the final component of the endpoint resource name. If not provided, Vertex AI will generate a value for this ID. If the first character is a letter, this value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The
last character must be a letter or number.
If the first character is a number, this value may be up to
9 characters, and valid characters are `[0-9]` with no
leading zeros.
When using HTTP/JSON, this field is populated based on a
query string argument, such as `?endpoint_id=12345` . This
is the fallback for fields that are not included in either
the URI or the body.
|

## Methods

### EndpointConfig

`EndpointConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The endpoint config to use for the deployment.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesoutputfieldspec_googlecloudaiplatform_v1typesfeatu_96d478.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesoutputfieldspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.OutputFieldSpec -->

# Class OutputFieldSpec (1.134.0)

`OutputFieldSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a specification for a single output field.

## Attributes |
|
|---|---|
Name |
Description |
`field_name` |
`str`
Required. The name of the output field. |
`guidance` |
`str`
Optional. Optional, but recommended. Additional guidance specific to this field to provide targeted instructions for the LLM to generate the content of a single output field. While the LLM can sometimes infer content from the field name, providing explicit guidance is preferred. |
`field_type` |
Optional. The data type of the field. Defaults to CONTENT if not set. |

## Classes

### FieldType

`FieldType(value)`


The data type of the field.

## Methods

### OutputFieldSpec

`OutputFieldSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Defines a specification for a single output field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestoremonitoringconfigimportfeaturesanalysisbaseline.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.Baseline -->

# Class Baseline (1.134.0)

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

## Enums |
|
|---|---|
Name |
Description |
`BASELINE_UNSPECIFIED` |
Should not be used. |
`LATEST_STATS` |
Choose the later one statistics generated by either most recent snapshot analysis or previous import features analysis. If non of them exists, skip anomaly detection and only generate a statistics. |
`MOST_RECENT_SNAPSHOT_STATS` |
Use the statistics generated by the most recent snapshot analysis if exists. |
`PREVIOUS_IMPORT_FEATURES_STATS` |
Use the statistics generated by the previous import features analysis if exists. |

## Methods

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesnasjobspecmultitrialalgorithmspecsearchtrialspec__a67bb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnasjobspecmultitrialalgorithmspecsearchtrialspec_g_618d06.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnasjobspecmultitrialalgorithmspecsearchtrialspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec.MultiTrialAlgorithmSpec.SearchTrialSpec -->

# Class SearchTrialSpec (1.134.0)

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.

## Attributes |
|
|---|---|
Name |
Description |
`search_trial_job_spec` |
Required. The spec of a search trial job. The same spec applies to all search trials. |
`max_trial_count` |
`int`
Required. The maximum number of Neural Architecture Search (NAS) trials to run. |
`max_parallel_trial_count` |
`int`
Required. The maximum number of trials to run in parallel. |
`max_failed_trial_count` |
`int`
The number of failed trials that need to be seen before failing the NasJob. If set to 0, Vertex AI decides how many trials must fail before the whole job fails. |

## Methods

### SearchTrialSpec

`SearchTrialSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represent spec for search trials.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespipelinetaskdetailpipelinetaskstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskDetail.PipelineTaskStatus -->

# Class PipelineTaskStatus (1.134.0)

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.

## Attributes |
|
|---|---|
Name |
Description |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Update time of this status. |
`state` |
Output only. The state of the task. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during the state. May be set when the state is any of the non-final state (PENDING/RUNNING/CANCELLING) or FAILED state. If the state is FAILED, the error here is final and not going to be retried. If the state is a non-final state, the error indicates a system-error being retried. |

## Methods

### PipelineTaskStatus

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureviewsyncsyncsummary_googlecloudaiplatf_811694.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewsyncsyncsummary.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewSync.SyncSummary -->

# Class SyncSummary (1.134.0)

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.

## Attributes |
|
|---|---|
Name |
Description |
`row_synced` |
`int`
Output only. Total number of rows synced. |
`total_slot` |
`int`
Output only. BigQuery slot milliseconds consumed for the sync job. |
`system_watermark_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Lower bound of the system time watermark for the sync job. This is only set for continuously syncing feature views. |

## Methods

### SyncSummary

`SyncSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the Sync job. For continuous syncs, the summary is updated periodically. For batch syncs, it gets updated on completion of the sync.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturenoisesigma.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureNoiseSigma -->

# Class FeatureNoiseSigma (1.134.0)

`FeatureNoiseSigma(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.

## Attribute |
|
|---|---|
Name |
Description |
`noise_sigma` |
`MutableSequence[`
Noise sigma per feature. No noise is added to features that are not set. |

## Classes

### NoiseSigmaForFeature

`NoiseSigmaForFeature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma for a single feature.

## Methods

### FeatureNoiseSigma

`FeatureNoiseSigma(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Noise sigma by features. Noise sigma represents the standard deviation of the gaussian kernel that will be used to add noise to interpolated inputs prior to computing gradients.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesvideoclassificati_08715b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesvideoclassificatio_9b9765.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesvideoclassification_3c9012.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesvideoclassificationpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoClassificationPredictionParams -->

# Class VideoClassificationPredictionParams (1.134.0)

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.

## Attributes |
|
|---|---|
Name |
Description |
`confidence_threshold` |
`float`
The Model only returns predictions with at least this confidence score. Default value is 0.0 |
`max_predictions` |
`int`
The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10,000. |
`segment_classification` |
`bool`
Set to true to request segment-level classification. Vertex AI returns labels and their confidence scores for the entire time segment of the video that user specified in the input instance. Default value is true |
`shot_classification` |
`bool`
Set to true to request shot-level classification. Vertex AI determines the boundaries for each camera shot in the entire time segment of the video that user specified in the input instance. Vertex AI then returns labels and their confidence scores for each detected shot, along with the start and end time of the shot. WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false |
`one_sec_interval_classification` |
`bool`
Set to true to request classification for a video at one-second intervals. Vertex AI returns labels and their confidence scores for each second of the entire time segment of the video that user specified in the input WARNING: Model evaluation is not done for this classification type, the quality of it depends on the training data, but there are no metrics provided to describe that quality. Default value is false |

## Methods

### VideoClassificationPredictionParams

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.

### VideoClassificationPredictionParams

```
VideoClassificationPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Classification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinetaskdetailpipelinetaskstatus_googlecl_6665e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinetaskdetailpipelinetaskstatus.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskDetail.PipelineTaskStatus -->

# Class PipelineTaskStatus (1.134.0)

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.

## Attributes |
|
|---|---|
Name |
Description |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Update time of this status. |
`state` |
Output only. The state of the task. |
`error` |
`google.rpc.status_pb2.Status`
Output only. The error that occurred during the state. May be set when the state is any of the non-final state (PENDING/RUNNING/CANCELLING) or FAILED state. If the state is FAILED, the error here is final and not going to be retried. If the state is a non-final state, the error indicates a system-error being retried. |

## Methods

### PipelineTaskStatus

`PipelineTaskStatus(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single record of the task status.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeletefeatureonlinestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureOnlineStoreRequest -->

# Class DeleteFeatureOnlineStoreRequest (1.134.0)

```
DeleteFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureOnlineStore to be deleted. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}`
|
`force` |
`bool`
If set to true, any FeatureViews and Features for this FeatureOnlineStore will also be deleted. (Otherwise, the request will only work if the FeatureOnlineStore has no FeatureViews.) |

## Methods

### DeleteFeatureOnlineStoreRequest

```
DeleteFeatureOnlineStoreRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeatureOnlineStoreAdminService.DeleteFeatureOnlineStore.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmigration_service_googlecloudaiplatformv1schem_a65fbf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmigration_service_googlecloudaiplatformv1schema_2a938a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmigration_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service -->

# Package migration_service (1.134.0)

API documentation for `aiplatform_v1.services.migration_service`

package.

## Classes

[MigrationServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceAsyncClient)

A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

[MigrationServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.MigrationServiceClient)

A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers)

API documentation for `aiplatform_v1.services.migration_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typestextclassificationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextClassificationPredictionInstance -->

# Class TextClassificationPredictionInstance (1.134.0)

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.

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

### TextClassificationPredictionInstance

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.

### TextClassificationPredictionInstance

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesretrievememoriesrequestsimilaritysearchparams_635185.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievememoriesrequestsimilaritysearchparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest.SimilaritySearchParams -->

# Class SimilaritySearchParams (1.134.0)

`SimilaritySearchParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for semantic similarity search based retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`search_query` |
`str`
Required. Query to use for similarity search retrieval. If provided, then the parent ReasoningEngine must have ReasoningEngineContextSpec.MemoryBankConfig.SimilaritySearchConfig set. |
`top_k` |
`int`
Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100. |

## Methods

### SimilaritySearchParams

`SimilaritySearchParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for semantic similarity search based retrieval.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesresourceruntimespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntimeSpec -->

# Class ResourceRuntimeSpec (1.134.0)

`ResourceRuntimeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the runtime on a PersistentResource instance, including but not limited to:

- Service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.

## Attributes |
|
|---|---|
Name |
Description |
`service_account_spec` |
Optional. Configure the use of workload identity on the PersistentResource |
`ray_spec` |
Optional. Ray cluster configuration. Required when creating a dedicated RayCluster on the PersistentResource. |

## Methods

### ResourceRuntimeSpec

`ResourceRuntimeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for the runtime on a PersistentResource instance, including but not limited to:

- Service accounts used to run the workloads.
- Whether to make it a dedicated Ray Cluster.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typespretunedmodel_googlecloudaiplatform_v1typesapiau_8b832c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespretunedmodel_googlecloudaiplatform_v1typesapiaut_c0f063.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespretunedmodel_googlecloudaiplatform_v1typesapiauth.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespretunedmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PreTunedModel -->

# Class PreTunedModel (1.134.0)

`PreTunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A pre-tuned model for continuous tuning.

## Attributes |
|
|---|---|
Name |
Description |
`tuned_model_name` |
`str`
The resource name of the Model. E.g., a model resource name with a specified version id or alias: `projects/{project}/locations/{location}/models/{model}@{version_id}`
`projects/{project}/locations/{location}/models/{model}@{alias}`
Or, omit the version id to use the default version:
`projects/{project}/locations/{location}/models/{model}`
|
`checkpoint_id` |
`str`
Optional. The source checkpoint id. If not specified, the default checkpoint will be used. |
`base_model` |
`str`
Output only. The name of the base model this PreTunedModel was tuned from. |

## Methods

### PreTunedModel

`PreTunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A pre-tuned model for continuous tuning.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesapiauth.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ApiAuth -->

# Class ApiAuth (1.134.0)

`ApiAuth(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The generic reusable api auth config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`api_key_config` |
The API secret. This field is a member of `oneof` _ `auth_config` .
|

## Classes

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.

## Methods

### ApiAuth

`ApiAuth(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The generic reusable api auth config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragretrievalconfigrankingrankservice_googlecl_b4e548.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragretrievalconfigrankingrankservice.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.Ranking.RankService -->

# Class RankService (1.134.0)

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`
This field is a member of `oneof` _ `_model_name` .
|

## Methods

### RankService

`RankService(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Rank Service.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatepipelinejobrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreatePipelineJobRequest -->

# Class CreatePipelineJobRequest (1.134.0)

`CreatePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CreatePipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`
|
`pipeline_job` |
Required. The PipelineJob to create. |
`pipeline_job_id` |
`str`
The ID to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an ID will be automatically generated. This value should be less than 128 characters, and valid characters are `/` a-z][0-9]`-/` .
|

## Methods

### CreatePipelineJobRequest

`CreatePipelineJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.CreatePipelineJob.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistnotebookruntimetemplatesrequest__googlecl_cc832a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnotebookruntimetemplatesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesRequest -->

# Class ListNotebookRuntimeTemplatesRequest (1.134.0)

```
ListNotebookRuntimeTemplatesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.ListNotebookRuntimeTemplates.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1beta1.NotebookRuntimeTemplate.name].
- `display_name` supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
- `notebookRuntimeType` supports = and !=.
notebookRuntimeType enum: [USER_DEFINED, ONE_CLICK].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.
Some examples:
- `notebookRuntimeTemplate=notebookRuntimeTemplate123`
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookRuntimeTemplatesResponse.next_page_token of the previous NotebookService.ListNotebookRuntimeTemplates call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListNotebookRuntimeTemplatesRequest

```
ListNotebookRuntimeTemplatesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.ListNotebookRuntimeTemplates.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextclassificatio_8e1957.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextclassificationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextClassificationPredictionInstance -->

# Class TextClassificationPredictionInstance (1.134.0)

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.

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

### TextClassificationPredictionInstance

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.

### TextClassificationPredictionInstance

```
TextClassificationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcall.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCall -->

# Class ToolCall (1.134.0)

`ToolCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`tool_name` |
`str`
Required. Spec for tool name This field is a member of `oneof` _ `_tool_name` .
|
`tool_input` |
`str`
Optional. Spec for tool input This field is a member of `oneof` _ `_tool_input` .
|

## Methods

### ToolCall

`ToolCall(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_servicescheduleserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient -->

# Class ScheduleServiceClient (1.134.0)

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

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
`ScheduleServiceTransport` |
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

### ScheduleServiceClient

```
ScheduleServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the schedule service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ScheduleServiceTransport,Callable[..., ScheduleServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ScheduleServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_schedule

```
create_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.CreateScheduleRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Creates a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[CreateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateScheduleRequest.html)(
parent="parent_value",
schedule=schedule,
)
# Make the request
response = client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_create_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.CreateSchedule. |
`parent` |
`str`
Required. The resource name of the Location to create the Schedule in. Format: |
`schedule` |
Required. The Schedule to create. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

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

### delete_schedule

```
delete_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.DeleteScheduleRequest,
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


Deletes a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_delete_schedule)(request=request)
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
The request object. Request message for ScheduleService.DeleteSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be deleted. Format: |
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

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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
`ScheduleServiceClient` |
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

### get_schedule

```
get_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.GetScheduleRequest, dict
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Gets a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_get_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.GetSchedule. |
`name` |
`str`
Required. The name of the Schedule resource. Format: |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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

### list_schedules

```
list_schedules(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest, dict
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
) -> google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesPager
```


Lists Schedules in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_schedules():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_list_schedules)(request=request)
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
The request object. Request message for ScheduleService.ListSchedules. |
`parent` |
`str`
Required. The resource name of the Location to list the Schedules from. Format: |
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
Response message for ScheduleService.ListSchedules Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### pause_schedule

```
pause_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.PauseScheduleRequest, dict
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
) -> None
```


Pauses a Schedule. Will mark xref_Schedule.state to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_pause_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_pause_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.PauseSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be paused. Format: |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_schedule

```
resume_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ResumeScheduleRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
catch_up: typing.Optional[bool] = None,
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


Resumes a paused Schedule to start scheduling new runs. Will mark xref_Schedule.state to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time_specification in the Schedule. If xref_Schedule.catch_up is set up true, all missed runs will be scheduled for backfill first.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_resume_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_resume_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.ResumeSchedule. |
`name` |
`str`
Required. The name of the Schedule resource to be resumed. Format: |
`catch_up` |
`bool`
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. This corresponds to the |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_schedule

```
update_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.UpdateScheduleRequest,
dict,
]
] = None,
*,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[UpdateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateScheduleRequest.html)(
schedule=schedule,
)
# Make the request
response = client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceClient_update_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ScheduleService.UpdateSchedule. |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. This corresponds to the |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicefeaturestoreserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient -->

# Class FeaturestoreServiceAsyncClient (1.134.0)

```
FeaturestoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### FeaturestoreServiceAsyncClient

```
FeaturestoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the featurestore service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeaturestoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
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


Creates a batch of Features in a given EntityType.

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
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1beta1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_batch_create_features)(request=request)
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

### batch_read_feature_values

```
batch_read_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.BatchReadFeatureValuesRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[str] = None,
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
from google.cloud import aiplatform_v1beta1
async def sample_batch_read_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
csv_read_instances = aiplatform_v1beta1.[CsvSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CsvSource.html)()
csv_read_instances.gcs_source.uris = ['uris_value1', 'uris_value2']
destination = aiplatform_v1beta1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
entity_type_specs = aiplatform_v1beta1.[EntityTypeSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.EntityTypeSpec.html)()
entity_type_specs.entity_type_id = "entity_type_id_value"
entity_type_specs.feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1beta1.[BatchReadFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadFeatureValuesRequest.html)(
csv_read_instances=csv_read_instances,
featurestore="featurestore_value",
destination=destination,
entity_type_specs=entity_type_specs,
)
# Make the request
operation = client.[batch_read_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_batch_read_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.BatchReadFeatureValues. |
`featurestore` |
Required. The resource name of the Featurestore from which to query Feature values. Format: |
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

### create_entity_type

```
create_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateEntityTypeRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
entity_type: typing.Optional[
google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
] = None,
entity_type_id: typing.Optional[str] = None,
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


Creates a new EntityType in a given Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateEntityTypeRequest.html)(
parent="parent_value",
entity_type_id="entity_type_id_value",
)
# Make the request
operation = client.[create_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_entity_type)(request=request)
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
The request object. Request message for FeaturestoreService.CreateEntityType. |
`parent` |
Required. The resource name of the Featurestore to create EntityTypes. Format: |
`entity_type` |
The EntityType to create. This corresponds to the |
`entity_type_id` |
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are |
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


Creates a new Feature in a given EntityType.

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
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_feature)(request=request)
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

### create_featurestore

```
create_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.CreateFeaturestoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
featurestore: typing.Optional[
google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
] = None,
featurestore_id: typing.Optional[str] = None,
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


Creates a new Featurestore in a given project and location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeaturestoreRequest.html)(
parent="parent_value",
featurestore_id="featurestore_id_value",
)
# Make the request
operation = client.[create_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_create_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.CreateFeaturestore. |
`parent` |
Required. The resource name of the Location to create Featurestores. Format: |
`featurestore` |
Required. The Featurestore to create. This corresponds to the |
`featurestore_id` |
Required. The ID to use for this Featurestore, which will become the final component of the Featurestore's resource name. This value may be up to 60 characters, and valid characters are |
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

### delete_entity_type

```
delete_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteEntityTypeRequest,
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
from google.cloud import aiplatform_v1beta1
async def sample_delete_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteEntityTypeRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_entity_type)(request=request)
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
The request object. Request message for [FeaturestoreService.DeleteEntityTypes][]. |
`name` |
Required. The name of the EntityType to be deleted. Format: |
`force` |
If set to true, any Features for this EntityType will also be deleted. (Otherwise, the request will only work if the EntityType has no Features.) This corresponds to the |
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
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_feature)(request=request)
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

### delete_feature_values

```
delete_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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
from google.cloud import aiplatform_v1beta1
async def sample_delete_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
select_entity = aiplatform_v1beta1.SelectEntity()
select_entity.entity_id_selector.csv_source.gcs_source.uris = ['uris_value1', 'uris_value2']
request = aiplatform_v1beta1.[DeleteFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureValuesRequest.html)(
select_entity=select_entity,
entity_type="entity_type_value",
)
# Make the request
operation = client.[delete_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType grouping the Features for which values are being deleted from. Format: |
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

### delete_featurestore

```
delete_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.DeleteFeaturestoreRequest,
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
from google.cloud import aiplatform_v1beta1
async def sample_delete_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_delete_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.DeleteFeaturestore. |
`name` |
Required. The name of the Featurestore to be deleted. Format: |
`force` |
If set to true, any EntityTypes and Features for this Featurestore will also be deleted. (Otherwise, the request will only work if the Featurestore has no EntityTypes.) This corresponds to the |
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.ExportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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


Exports Feature values from all the entities of a target EntityType.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_export_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
destination = aiplatform_v1beta1.[FeatureValueDestination](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureValueDestination.html)()
destination.bigquery_destination.output_uri = "output_uri_value"
feature_selector = aiplatform_v1beta1.[FeatureSelector](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureSelector.html)()
feature_selector.id_matcher.ids = ['ids_value1', 'ids_value2']
request = aiplatform_v1beta1.[ExportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest.html)(
entity_type="entity_type_value",
destination=destination,
feature_selector=feature_selector,
)
# Make the request
operation = client.[export_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_export_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ExportFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType from which to export Feature values. Format: |
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
`FeaturestoreServiceAsyncClient` |
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
`FeaturestoreServiceAsyncClient` |
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
`FeaturestoreServiceAsyncClient` |
The constructed client. |

### get_entity_type

```
get_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetEntityTypeRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
from google.cloud import aiplatform_v1beta1
async def sample_get_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetEntityTypeRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetEntityType. |
`name` |
Required. The name of the EntityType resource. Format: |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

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
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_feature)(request=request)
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

### get_featurestore

```
get_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.GetFeaturestoreRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
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
from google.cloud import aiplatform_v1beta1
async def sample_get_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeaturestoreRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_get_featurestore)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.GetFeaturestore. |
`name` |
Required. The name of the Featurestore resource. This corresponds to the |
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
Vertex AI Feature Store provides a centralized repository for organizing, storing, and serving ML features. The Featurestore is a top-level container for your features and their values. |

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
google.cloud.aiplatform_v1beta1.services.featurestore_service.transports.base.FeaturestoreServiceTransport
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

### import_feature_values

```
import_feature_values(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ImportFeatureValuesRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[str] = None,
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
from google.cloud import aiplatform_v1beta1
async def sample_import_feature_values():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
avro_source = aiplatform_v1beta1.[AvroSource](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AvroSource.html)()
avro_source.gcs_source.uris = ['uris_value1', 'uris_value2']
feature_specs = aiplatform_v1beta1.[FeatureSpec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest.FeatureSpec.html)()
feature_specs.id = "id_value"
request = aiplatform_v1beta1.[ImportFeatureValuesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportFeatureValuesRequest.html)(
avro_source=avro_source,
feature_time_field="feature_time_field_value",
entity_type="entity_type_value",
feature_specs=feature_specs,
)
# Make the request
operation = client.[import_feature_values](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_import_feature_values)(request=request)
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
The request object. Request message for FeaturestoreService.ImportFeatureValues. |
`entity_type` |
Required. The resource name of the EntityType grouping the Features for which values are being imported. Format: |
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

### list_entity_types

```
list_entity_types(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_entity_types():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListEntityTypesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_entity_types](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_entity_types)(request=request)
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
The request object. Request message for FeaturestoreService.ListEntityTypes. |
`parent` |
Required. The resource name of the Featurestore to list EntityTypes. Format: |
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
Response message for FeaturestoreService.ListEntityTypes. Iterating over this object will yield results and resolve additional pages automatically. |

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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesAsyncPager
)
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
from google.cloud import aiplatform_v1beta1
async def sample_list_features():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_features)(request=request)
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

### list_featurestores

```
list_featurestores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
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
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_list_featurestores():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturestoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_featurestores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_list_featurestores)(request=request)
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
The request object. Request message for FeaturestoreService.ListFeaturestores. |
`parent` |
Required. The resource name of the Location to list Featurestores. Format: |
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
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
dict,
]
] = None,
*,
location: typing.Optional[str] = None,
query: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesAsyncPager
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
from google.cloud import aiplatform_v1beta1
async def sample_search_features():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[SearchFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesRequest.html)(
location="location_value",
)
# Make the request
page_result = client.[search_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_search_features)(request=request)
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
The request object. Request message for FeaturestoreService.SearchFeatures. |
`location` |
Required. The resource name of the Location to search Features. Format: |
`query` |
Query string that is a conjunction of field-restricted queries and/or field-restricted filters. Field-restricted queries and filters can be combined using |
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
Response message for FeaturestoreService.SearchFeatures. Iterating over this object will yield results and resolve additional pages automatically. |

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

### update_entity_type

```
update_entity_type(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateEntityTypeRequest,
dict,
]
] = None,
*,
entity_type: typing.Optional[
google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
) -> google.cloud.aiplatform_v1beta1.types.entity_type.EntityType
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
from google.cloud import aiplatform_v1beta1
async def sample_update_entity_type():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateEntityTypeRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateEntityTypeRequest.html)(
)
# Make the request
response = await client.[update_entity_type](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_entity_type)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for FeaturestoreService.UpdateEntityType. |
`entity_type` |
Required. The EntityType's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the EntityType resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
An entity type is a type of object in a system that needs to be modeled and have stored information about. For example, driver is an entity type, and driver0 is an instance of an entity type driver. |

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
) -> google.cloud.aiplatform_v1beta1.types.feature.Feature
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
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest.html)(
)
# Make the request
response = await client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_feature)(request=request)
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
|
Feature Metadata information. For example, color is a feature that describes an apple. |

### update_featurestore

```
update_featurestore(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.featurestore_service.UpdateFeaturestoreRequest,
dict,
]
] = None,
*,
featurestore: typing.Optional[
google.cloud.aiplatform_v1beta1.types.featurestore.Featurestore
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


Updates the parameters of a single Featurestore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_featurestore():
# Create a client
client = aiplatform_v1beta1.
```[FeaturestoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeaturestoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreRequest.html)(
)
# Make the request
operation = client.[update_featurestore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.FeaturestoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_featurestore_service_FeaturestoreServiceAsyncClient_update_featurestore)(request=request)
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
The request object. Request message for FeaturestoreService.UpdateFeaturestore. |
`featurestore` |
Required. The Featurestore's |
`update_mask` |
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatf_a29d20.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatfo_176e51.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatfor_a17dc4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatform_4a134f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatform__514f35.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatform_v_cf6592.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmigration_service_googlecloudaiplatform_v1_f4042a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmigration_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service -->

# Package migration_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.migration_service`

package.

## Classes

[MigrationServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceAsyncClient)

A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

[MigrationServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.MigrationServiceClient)

A service that migrates resources from automl.googleapis.com, datalabeling.googleapis.com and ml.googleapis.com to Vertex AI.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers)

API documentation for `aiplatform_v1beta1.services.migration_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprebuiltvoiceconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PrebuiltVoiceConfig -->

# Class PrebuiltVoiceConfig (1.134.0)

`PrebuiltVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the prebuilt speaker to use.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`voice_name` |
`str`
The name of the preset voice to use. This field is a member of `oneof` _ `_voice_name` .
|

## Methods

### PrebuiltVoiceConfig

`PrebuiltVoiceConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration for the prebuilt speaker to use.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringschema.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringSchema -->

# Class ModelMonitoringSchema (1.134.0)

`ModelMonitoringSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Model Monitoring Schema definition.

## Attributes |
|
|---|---|
Name |
Description |
`feature_fields` |
`MutableSequence[`
Feature names of the model. Vertex AI will try to match the features from your dataset as follows: - For 'csv' files, the header names are required, and we will extract the corresponding feature values when the header names align with the feature names. - For 'jsonl' files, we will extract the corresponding feature values if the key names match the feature names. Note: Nested features are not supported, so please ensure your features are flattened. Ensure the feature values are scalar or an array of scalars. - For 'bigquery' dataset, we will extract the corresponding feature values if the column names match the feature names. Note: The column type can be a scalar or an array of scalars. STRUCT or JSON types are not supported. You may use SQL queries to select or aggregate the relevant features from your original table. However, ensure that the 'schema' of the query results meets our requirements. - For the Vertex AI Endpoint Request Response Logging table or Vertex AI Batch Prediction Job results. If the instance_type is an array, ensure that the sequence in feature_fields matches the order of features in the prediction instance. We will match the feature with the array in the order specified in [feature_fields]. |
`prediction_fields` |
`MutableSequence[`
Prediction output names of the model. The requirements are the same as the feature_fields. For AutoML Tables, the prediction output name presented in schema will be: `predicted_{target_column}` , the
`target_column` is the one you specified when you train
the model. For Prediction output drift analysis:
- AutoML Classification, the distribution of the argmax
label will be analyzed.
- AutoML Regression, the distribution of the value will be
analyzed.
|
`ground_truth_fields` |
`MutableSequence[`
Target /ground truth names of the model. |

## Classes

### FieldSchema

`FieldSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Schema field definition.

## Methods

### ModelMonitoringSchema

`ModelMonitoringSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Model Monitoring Schema definition.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformpredictionhandler_googlecloudaiplatform_v1typestoolcallva_a733c7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformpredictionhandler_googlecloudaiplatform_v1typestoolcallval_2ae47c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpredictionhandler.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.Handler -->

# Class Handler (1.134.0)

```
Handler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Interface for Handler class to handle prediction requests.

## Methods

### Handler

```
Handler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Initializes a Handler instance.

Parameters |
|
|---|---|
Name |
Description |
`artifacts_uri` |
`str`
Required. The value of the environment variable AIP_STORAGE_URI. |
`predictor` |
`Type[Predictor]`
Optional. The Predictor class this handler uses to initiate predictor instance if given. |

### handle

`handle(request: starlette.requests.Request) -> starlette.responses.Response`


Handles a prediction request.

Parameter |
|
|---|---|
Name |
Description |
`request` |
`Request`
The request sent to the application. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolcallvalidmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidMetricValue -->

# Class ToolCallValidMetricValue (1.134.0)

`ToolCallValidMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool call valid metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool call valid score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolCallValidMetricValue

`ToolCallValidMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool call valid metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespersistentresourcestate_googlecloudaiplatform_849092.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespersistentresourcestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PersistentResource.State -->

# Class State (1.134.0)

`State(value)`


Describes the PersistentResource state.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Not set. |
`PROVISIONING` |
The PROVISIONING state indicates the persistent resources is being created. |
`RUNNING` |
The RUNNING state indicates the persistent resource is healthy and fully usable. |
`STOPPING` |
The STOPPING state indicates the persistent resource is being deleted. |
`ERROR` |
The ERROR state indicates the persistent resource may be unusable. Details can be found in the `error` field. |
`REBOOTING` |
The REBOOTING state indicates the persistent resource is being rebooted (PR is not available right now but is expected to be ready again later). |
`UPDATING` |
The UPDATING state indicates the persistent resource is being updated. |

## Methods

### State

`State(value)`


Describes the PersistentResource state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureviewdirectwriterequestdatakeyandfeaturevalues.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues -->

# Class DataKeyAndFeatureValues (1.134.0)

`DataKeyAndFeatureValues(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A data key and associated feature values to write to the feature view.

## Attributes |
|
|---|---|
Name |
Description |
`data_key` |
The data key. |
`features` |
`MutableSequence[`
List of features to write. |

## Classes

### Feature

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### DataKeyAndFeatureValues

`DataKeyAndFeatureValues(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A data key and associated feature values to write to the feature view.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesusagemetadata_googlecloudaiplatform_v1beta1typesr_d458be.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesusagemetadata_googlecloudaiplatform_v1beta1typesra_1c0fe3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesusagemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UsageMetadata -->

# Class UsageMetadata (1.134.0)

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.

## Attributes |
|
|---|---|
Name |
Description |
`prompt_token_count` |
`int`
The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of
tokens in the cached content.
|
`candidates_token_count` |
`int`
The total number of tokens in the generated candidates. |
`total_token_count` |
`int`
The total number of tokens for the entire request. This is the sum of `prompt_token_count` ,
`candidates_token_count` , `tool_use_prompt_token_count` ,
and `thoughts_token_count` .
|
`tool_use_prompt_token_count` |
`int`
Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable. |
`thoughts_token_count` |
`int`
Output only. The number of tokens that were part of the model's generated "thoughts" output, if applicable. |
`cached_content_token_count` |
`int`
Output only. The number of tokens in the cached content that was used for this request. |
`prompt_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the prompt. |
`cache_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the cached content. |
`candidates_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the generated candidates. |
`tool_use_prompt_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input. |
`traffic_type` |
Output only. The traffic type for this request. |

## Classes

### TrafficType

`TrafficType(value)`


The type of traffic that this request was processed with, indicating which quota gets consumed.

## Methods

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragembeddingmodelconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagEmbeddingModelConfig -->

# Class RagEmbeddingModelConfig (1.134.0)

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

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
`vertex_prediction_endpoint` |
The Vertex AI Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. Endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search. This field is a member of `oneof` _ `model_config` .
|
`hybrid_search_config` |
Configuration for hybrid search. This field is a member of `oneof` _ `model_config` .
|

## Classes

### HybridSearchConfig

`HybridSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for hybrid search.

### SparseEmbeddingConfig

`SparseEmbeddingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for sparse emebdding generation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### VertexPredictionEndpoint

`VertexPredictionEndpoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config representing a model hosted on Vertex Prediction Endpoint.

## Methods

### RagEmbeddingModelConfig

`RagEmbeddingModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the embedding model to use for RAG.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesrecommendspecresponserecommendation_googlecl_e84c9c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrecommendspecresponserecommendation_googleclo_936000.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrecommendspecresponserecommendation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse.Recommendation -->

# Class Recommendation (1.134.0)

`Recommendation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Recommendation of one deployment option for the given custom weights model in one region. Contains the machine and container spec, and user accelerator quota state.

## Attributes |
|
|---|---|
Name |
Description |
`region` |
`str`
The region for the deployment spec (machine). |
`spec` |
Output only. The machine and model container specs. |
`user_quota_state` |
Output only. The user accelerator quota state. |

## Classes

### QuotaState

`QuotaState(value)`


The user accelerator quota state.

## Methods

### Recommendation

`Recommendation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Recommendation of one deployment option for the given custom weights model in one region. Contains the machine and container spec, and user accelerator quota state.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatemodelmonitorrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateModelMonitorRequest -->

# Class CreateModelMonitorRequest (1.134.0)

`CreateModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.CreateModelMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ModelMonitor in. Format: `projects/{project}/locations/{location}`
|
`model_monitor` |
Required. The ModelMonitor to create. |
`model_monitor_id` |
`str`
Optional. The ID to use for the Model Monitor, which will become the final component of the model monitor resource name. The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .
|

## Methods

### CreateModelMonitorRequest

`CreateModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.CreateModelMonitor.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatedeploymentresourcepoolrequest_googleclo_22fcec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatedeploymentresourcepoolrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateDeploymentResourcePoolRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1typestabularregressionpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularRegressionPredictionResult -->

# Class TabularRegressionPredictionResult (1.134.0)

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.

## Attributes |
|
|---|---|
Name |
Description |
`value` |
`float`
The regression value. |
`lower_bound` |
`float`
The lower bound of the prediction interval. |
`upper_bound` |
`float`
The upper bound of the prediction interval. |

## Methods

### TabularRegressionPredictionResult

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.

### TabularRegressionPredictionResult

```
TabularRegressionPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Tabular Regression.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesreasoningenginespecsourcecodespec_googlecloudaip_731109.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesreasoningenginespecsourcecodespec_googlecloudaipl_7cafdc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesreasoningenginespecsourcecodespec_googlecloudaipla_a20123.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecsourcecodespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.SourceCodeSpec -->

# Class SourceCodeSpec (1.134.0)

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

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
`inline_source` |
Source code is provided directly in the request. This field is a member of `oneof` _ `source` .
|
`developer_connect_source` |
Source code is in a Git repository managed by Developer Connect. This field is a member of `oneof` _ `source` .
|
`python_spec` |
Configuration for a Python application. This field is a member of `oneof` _ `language_spec` .
|

## Classes

### DeveloperConnectConfig

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

### InlineSource

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Methods

### SourceCodeSpec

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecsourcecodespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec -->

# Class SourceCodeSpec (1.134.0)

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

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
`inline_source` |
Source code is provided directly in the request. This field is a member of `oneof` _ `source` .
|
`developer_connect_source` |
Source code is in a Git repository managed by Developer Connect. This field is a member of `oneof` _ `source` .
|
`python_spec` |
Configuration for a Python application. This field is a member of `oneof` _ `language_spec` .
|

## Classes

### DeveloperConnectConfig

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.

### DeveloperConnectSource

`DeveloperConnectSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code to be fetched from a Git repository managed through the Developer Connect service.

### InlineSource

`InlineSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies source code provided as a byte stream.

### PythonSpec

`PythonSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for running a Python application from source.

## Methods

### SourceCodeSpec

`SourceCodeSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specification for deploying from source code.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestoolnamematchmetricvalue_googlecloudaiplatform_v1_4817ba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolnamematchmetricvalue_googlecloudaiplatform_v1b_c7db0d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolnamematchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchMetricValue -->

# Class ToolNameMatchMetricValue (1.134.0)

`ToolNameMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool name match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool name match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolNameMatchMetricValue

`ToolNameMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool name match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinputtimeoffset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.TimeOffset -->

# Class TimeOffset (1.134.0)

`TimeOffset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time offset setting.

## Attributes |
|
|---|---|
Name |
Description |
`offset` |
`str`
[offset] is the time difference from the cut-off time. For scheduled jobs, the cut-off time is the scheduled time. For non-scheduled jobs, it's the time when the job was created. Currently we support the following format: 'w|W': Week, 'd|D': Day, 'h|H': Hour E.g. '1h' stands for 1 hour, '2d' stands for 2 days. |
`window` |
`str`
[window] refers to the scope of data selected for analysis. It allows you to specify the quantity of data you wish to examine. Currently we support the following format: 'w|W': Week, 'd|D': Day, 'h|H': Hour E.g. '1h' stands for 1 hour, '2d' stands for 2 days. |

## Methods

### TimeOffset

`TimeOffset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time offset setting.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelevaluation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelEvaluation -->

# Class ModelEvaluation (1.134.0)

`ModelEvaluation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the ModelEvaluation. |
`display_name` |
`str`
The display name of the ModelEvaluation. |
`metrics_schema_uri` |
`str`
Points to a YAML file stored on Google Cloud Storage describing the metrics of this ModelEvaluation. The schema is defined as an OpenAPI 3.0.2 `Schema Object |
`metrics` |
`google.protobuf.struct_pb2.Value`
Evaluation metrics of the Model. The schema of the metrics is stored in metrics_schema_uri |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelEvaluation was created. |
`slice_dimensions` |
`MutableSequence[str]`
All possible dimensions of ModelEvaluationSlices. The dimensions can be used as the filter of the ModelService.ListModelEvaluationSlices request, in the form of `slice.dimension = ` .
|
`model_explanation` |
Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for AutoML tabular Models. |
`explanation_specs` |
`MutableSequence[`
Describes the values of ExplanationSpec that are used for explaining the predicted values on the evaluated data. |
`metadata` |
`google.protobuf.struct_pb2.Value`
The metadata of the ModelEvaluation. For the ModelEvaluation uploaded from Managed Pipeline, metadata contains a structured value with keys of "pipeline_job_id", "evaluation_dataset_type", "evaluation_dataset_path", "row_based_metrics_path". |
`bias_configs` |
Specify the configuration for bias detection. |

## Classes

### BiasConfig

`BiasConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for bias detection.

### ModelEvaluationExplanationSpec

```
ModelEvaluationExplanationSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Methods

### ModelEvaluation

`ModelEvaluation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typessampledshapleyattribution_googlecloudaiplat_6b5abe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessampledshapleyattribution_googlecloudaiplatf_f99805.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessampledshapleyattribution_googlecloudaiplatfo_f30920.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessampledshapleyattribution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SampledShapleyAttribution -->

# Class SampledShapleyAttribution (1.134.0)

`SampledShapleyAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.

## Attribute |
|
|---|---|
Name |
Description |
`path_count` |
`int`
Required. The number of feature permutations to consider when approximating the Shapley values. Valid range of its value is [1, 50], inclusively. |

## Methods

### SampledShapleyAttribution

`SampledShapleyAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespredefinedsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredefinedSplit -->

# Class PredefinedSplit (1.134.0)

`PredefinedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.

## Attribute |
|
|---|---|
Name |
Description |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { `training` ,
`validation` , `test` }, and it defines to which set the
given piece of data is assigned. If for a piece of data the
key is not present or has an invalid value, that piece is
ignored by the pipeline.
|

## Methods

### PredefinedSplit

`PredefinedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodelcalltoaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel.CallToAction -->

# Class CallToAction (1.134.0)

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### Deploy

`Deploy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model metadata that is needed for UploadModel or DeployModel/CreateEndpoint requests.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### DeployGke

`DeployGke(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configurations for PublisherModel GKE deployment

### DeployVertex

`DeployVertex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Multiple setups to deploy the PublisherModel.

### OpenFineTuningPipelines

`OpenFineTuningPipelines(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open fine tuning pipelines.

### OpenNotebooks

`OpenNotebooks(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Open notebooks.

### RegionalResourceReferences

`RegionalResourceReferences(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The regional resource name or the URI. Key is region, e.g., us-central1, europe-west2, global, etc..

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ViewRestApi

`ViewRestApi(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Rest API docs.

## Methods

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesupdatenotebookruntimetemplaterequest_googleclouda_95b90a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatenotebookruntimetemplaterequest_googlecloudai_9e7374.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateNotebookRuntimeTemplateRequest -->

# Class UpdateNotebookRuntimeTemplateRequest (1.134.0)

```
UpdateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpdateNotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
Input format: `{paths: "${updated_filed}"}` Updatable
fields:
- `encryption_spec.kms_key_name`
|

## Methods

### UpdateNotebookRuntimeTemplateRequest

```
UpdateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpdateNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecpackagespec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.PackageSpec -->

# Class PackageSpec (1.134.0)

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.

## Attributes |
|
|---|---|
Name |
Description |
`pickle_object_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the pickled python object. |
`dependency_files_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the dependency files in tar.gz format. |
`requirements_gcs_uri` |
`str`
Optional. The Cloud Storage URI of the `requirements.txt`
file
|
`python_version` |
`str`
Optional. The Python version. Supported values are 3.9, 3.10, 3.11, 3.12, 3.13. If not specified, the default value is 3.10. |

## Methods

### PackageSpec

`PackageSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


User-provided package specification, containing pickled object and package requirements.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessampledshapleyattribution_googlecloudaiplatform_v1_f4bdaa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessampledshapleyattribution.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SampledShapleyAttribution -->

# Class SampledShapleyAttribution (1.134.0)

`SampledShapleyAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.

## Attribute |
|
|---|---|
Name |
Description |
`path_count` |
`int`
Required. The number of feature permutations to consider when approximating the Shapley values. Valid range of its value is [1, 50], inclusively. |

## Methods

### SampledShapleyAttribution

`SampledShapleyAttribution(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An attribution method that approximates Shapley values for features that contribute to the label being predicted. A sampling strategy is used to approximate the value rather than considering all subsets of features.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesprobehttpgetaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Probe.HttpGetAction -->

# Class HttpGetAction (1.134.0)

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Path to access on the HTTP server. |
`port` |
`int`
Number of the port to access on the container. Number must be in the range 1 to 65535. |
`host` |
`str`
Host name to connect to, defaults to the model serving container's IP. You probably want to set "Host" in httpHeaders instead. |
`scheme` |
`str`
Scheme to use for connecting to the host. Defaults to HTTP. Acceptable values are "HTTP" or "HTTPS". |
`http_headers` |
`MutableSequence[`
Custom headers to set in the request. HTTP allows repeated headers. |

## Methods

### HttpGetAction

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicespersistent_resource_service_googleclou_80e909.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicespersistent_resource_service_googlecloud_edb171.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicespersistent_resource_service_googleclouda_dfa8a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicespersistent_resource_service_googlecloudai_40f7f4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicespersistent_resource_service_googlecloudaip_1d2427.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespersistent_resource_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service -->

# Package persistent_resource_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.persistent_resource_service`

package.

## Classes

[PersistentResourceServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceAsyncClient)

A service for managing Vertex AI's machine learning PersistentResource.

[PersistentResourceServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.PersistentResourceServiceClient)

A service for managing Vertex AI's machine learning PersistentResource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers)

API documentation for `aiplatform_v1beta1.services.persistent_resource_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespredefinedsplit.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredefinedSplit -->

# Class PredefinedSplit (1.134.0)

`PredefinedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.

## Attribute |
|
|---|---|
Name |
Description |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The value of the key (either the label's value or value in the column) must be one of { `training` ,
`validation` , `test` }, and it defines to which set the
given piece of data is assigned. If for a piece of data the
key is not present or has an invalid value, that piece is
ignored by the pipeline.
|

## Methods

### PredefinedSplit

`PredefinedSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on the value of a provided key.

Supported only for tabular Datasets.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstoredcontentsexamplefilter_googlecloudaiplat_083ac0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstoredcontentsexamplefilter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleFilter -->

# Class StoredContentsExampleFilter (1.134.0)

`StoredContentsExampleFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metadata filters that will be used to remove or fetch StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied.

## Attributes |
|
|---|---|
Name |
Description |
`search_keys` |
`MutableSequence[str]`
Optional. The search keys for filtering. Only examples with one of the specified search keys (StoredContentsExample.search_key) are eligible to be returned. |
`function_names` |
Optional. The function names for filtering. |

## Methods

### StoredContentsExampleFilter

`StoredContentsExampleFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metadata filters that will be used to remove or fetch StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringstats.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStats -->

# Class ModelMonitoringStats (1.134.0)

`ModelMonitoringStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the collection of statistics for a metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`tabular_stats` |
Generated tabular statistics. This field is a member of `oneof` _ `stats` .
|

## Methods

### ModelMonitoringStats

`ModelMonitoringStats(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the collection of statistics for a metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesevaluatedannotationevaluatedannotationtype_g_642214.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesevaluatedannotationevaluatedannotationtype_go_e01d0f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesevaluatedannotationevaluatedannotationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotation.EvaluatedAnnotationType -->

# Class EvaluatedAnnotationType (1.134.0)

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Enums |
|
|---|---|
Name |
Description |
`EVALUATED_ANNOTATION_TYPE_UNSPECIFIED` |
Invalid value. |
`TRUE_POSITIVE` |
The EvaluatedAnnotation is a true positive. It has a prediction created by the Model and a ground truth Annotation which the prediction matches. |
`FALSE_POSITIVE` |
The EvaluatedAnnotation is false positive. It has a prediction created by the Model which does not match any ground truth annotation. |
`FALSE_NEGATIVE` |
The EvaluatedAnnotation is false negative. It has a ground truth annotation which is not matched by any of the model created predictions. |

## Methods

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesexplanationspecoverride.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationSpecOverride -->

# Class ExplanationSpecOverride (1.134.0)

`ExplanationSpecOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The ExplanationSpec entries that can be overridden at [online explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] time.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
The parameters to be overridden. Note that the attribution method cannot be changed. If not specified, no parameter is overridden. |
`metadata` |
The metadata to be overridden. If not specified, no metadata is overridden. |
`examples_override` |
The example-based explanations parameter overrides. |

## Methods

### ExplanationSpecOverride

`ExplanationSpecOverride(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The ExplanationSpec entries that can be overridden at [online explanation][google.cloud.aiplatform.v1beta1.PredictionService.Explain] time.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringobjectivetype_google_e65238.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodeldeploymentmonitoringobjectivetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelDeploymentMonitoringObjectiveType -->

# Class ModelDeploymentMonitoringObjectiveType (1.134.0)

`ModelDeploymentMonitoringObjectiveType(value)`


The Model Monitoring Objective types.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_DEPLOYMENT_MONITORING_OBJECTIVE_TYPE_UNSPECIFIED` |
Default value, should not be set. |
`RAW_FEATURE_SKEW` |
Raw feature values' stats to detect skew between Training-Prediction datasets. |
`RAW_FEATURE_DRIFT` |
Raw feature values' stats to detect drift between Serving-Prediction datasets. |
`FEATURE_ATTRIBUTION_SKEW` |
Feature attribution scores to detect skew between Training-Prediction datasets. |
`FEATURE_ATTRIBUTION_DRIFT` |
Feature attribution scores to detect skew between Prediction datasets collected within different time windows. |

## Methods

### ModelDeploymentMonitoringObjectiveType

`ModelDeploymentMonitoringObjectiveType(value)`


The Model Monitoring Objective types.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescontentsexample.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ContentsExample -->

# Class ContentsExample (1.134.0)

`ContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single example of a conversation with the model.

## Attributes |
|
|---|---|
Name |
Description |
`contents` |
`MutableSequence[google.cloud.aiplatform_v1beta1.types.Content]`
Required. The content of the conversation with the model that resulted in the expected output. |
`expected_contents` |
`MutableSequence[`
Required. The expected output for the given `contents` . To
represent multi-step reasoning, this is a repeated field
that contains the iterative steps of the expected output.
|

## Classes

### ExpectedContent

`ExpectedContent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single step of the expected output.

## Methods

### ContentsExample

`ContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single example of a conversation with the model.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesmodeldeploymentmonitoringobjectivetype_googleclo_3f71c3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesmodeldeploymentmonitoringobjectivetype_googleclou_f476b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringobjectivetype_googlecloud_587c93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringobjectivetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringObjectiveType -->

# Class ModelDeploymentMonitoringObjectiveType (1.134.0)

`ModelDeploymentMonitoringObjectiveType(value)`


The Model Monitoring Objective types.

## Enums |
|
|---|---|
Name |
Description |
`MODEL_DEPLOYMENT_MONITORING_OBJECTIVE_TYPE_UNSPECIFIED` |
Default value, should not be set. |
`RAW_FEATURE_SKEW` |
Raw feature values' stats to detect skew between Training-Prediction datasets. |
`RAW_FEATURE_DRIFT` |
Raw feature values' stats to detect drift between Serving-Prediction datasets. |
`FEATURE_ATTRIBUTION_SKEW` |
Feature attribution scores to detect skew between Training-Prediction datasets. |
`FEATURE_ATTRIBUTION_DRIFT` |
Feature attribution scores to detect skew between Prediction datasets collected within different time windows. |

## Methods

### ModelDeploymentMonitoringObjectiveType

`ModelDeploymentMonitoringObjectiveType(value)`


The Model Monitoring Objective types.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatenotebookruntimetemplaterequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateNotebookRuntimeTemplateRequest -->

# Class UpdateNotebookRuntimeTemplateRequest (1.134.0)

```
UpdateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpdateNotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtime_template` |
Required. The NotebookRuntimeTemplate to update. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. For the `FieldMask` definition, see
`google.protobuf.FieldMask][google.protobuf.FieldMask]` .
Input format: `{paths: "${updated_filed}"}` Updatable
fields:
- `encryption_spec.kms_key_name`
|

## Methods

### UpdateNotebookRuntimeTemplateRequest

```
UpdateNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.UpdateNotebookRuntimeTemplate.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinputmodelmonitoringdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput.ModelMonitoringDataset -->

# Class ModelMonitoringDataset (1.134.0)

`ModelMonitoringDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input dataset spec.

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
`vertex_dataset` |
`str`
Resource name of the Vertex AI managed dataset. This field is a member of `oneof` _ `data_location` .
|
`gcs_source` |
Google Cloud Storage data source. This field is a member of `oneof` _ `data_location` .
|
`bigquery_source` |
BigQuery data source. This field is a member of `oneof` _ `data_location` .
|
`timestamp_field` |
`str`
The timestamp field. Usually for serving data. |

## Classes

### ModelMonitoringBigQuerySource

```
ModelMonitoringBigQuerySource(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Dataset spec for data sotred in BigQuery.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### ModelMonitoringGcsSource

`ModelMonitoringGcsSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset spec for data stored in Google Cloud Storage.

## Methods

### ModelMonitoringDataset

`ModelMonitoringDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input dataset spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesusagemetadata_googlecloudaiplatformv1schematr_d4c634.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesusagemetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UsageMetadata -->

# Class UsageMetadata (1.134.0)

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.

## Attributes |
|
|---|---|
Name |
Description |
`prompt_token_count` |
`int`
The total number of tokens in the prompt. This includes any text, images, or other media provided in the request. When `cached_content` is set, this also includes the number of
tokens in the cached content.
|
`candidates_token_count` |
`int`
The total number of tokens in the generated candidates. |
`total_token_count` |
`int`
The total number of tokens for the entire request. This is the sum of `prompt_token_count` ,
`candidates_token_count` , `tool_use_prompt_token_count` ,
and `thoughts_token_count` .
|
`tool_use_prompt_token_count` |
`int`
Output only. The number of tokens in the results from tool executions, which are provided back to the model as input, if applicable. |
`thoughts_token_count` |
`int`
Output only. The number of tokens that were part of the model's generated "thoughts" output, if applicable. |
`cached_content_token_count` |
`int`
Output only. The number of tokens in the cached content that was used for this request. |
`prompt_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the prompt. |
`cache_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the cached content. |
`candidates_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown of the token count for each modality in the generated candidates. |
`tool_use_prompt_tokens_details` |
`MutableSequence[`
Output only. A detailed breakdown by modality of the token counts from the results of tool executions, which are provided back to the model as input. |
`traffic_type` |
Output only. The traffic type for this request. |

## Classes

### TrafficType

`TrafficType(value)`


The type of traffic that this request was processed with, indicating which quota gets consumed.

## Methods

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about the content generation request and response. This message provides a detailed breakdown of token usage and other relevant metrics.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimageclassificationinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs -->

# Class AutoMlImageClassificationInputs (1.134.0)

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`base_model_id` |
`str`
The ID of the `base` model. If it is specified, the new
model will be trained based on the `base` model.
Otherwise, the new model will be trained from scratch. The
`base` model must be in the same Project and Location as
the new Model to train, and have the same modelType.
|
`budget_milli_node_hours` |
`int`
The training budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The actual metadata.costMilliNodeHours will be equal or less than this value. If further model training ceases to provide any improvements, it will stop without using the full budget and the metadata.successfulStopReason will be `model-converged` . Note, node_hour = actual_hour \*
number_of_nodes_involved. For modelType
`cloud` \ (default), the budget must be between 8,000 and
800,000 milli node hours, inclusive. The default value is
192,000 which represents one day in wall time, considering 8
nodes are used. For model types `mobile-tf-low-latency-1` ,
`mobile-tf-versatile-1` , `mobile-tf-high-accuracy-1` ,
the training budget must be between 1,000 and 100,000 milli
node hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.
|
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used. |
`multi_label` |
`bool`
If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable). |

## Classes

### ModelType

`ModelType(value)`


## Methods

### AutoMlImageClassificationInputs

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageClassificationInputs

```
AutoMlImageClassificationInputs(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesfeaturevaluetype_googlecloudaiplatform_v1b_e04573.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesfeaturevaluetype_googlecloudaiplatform_v1be_fdf623.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfeaturevaluetype_googlecloudaiplatform_v1bet_553902.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeaturevaluetype_googlecloudaiplatform_v1beta_ef7cd0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturevaluetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature.ValueType -->

# Class ValueType (1.134.0)

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.

## Enums |
|
|---|---|
Name |
Description |
`VALUE_TYPE_UNSPECIFIED` |
The value type is unspecified. |
`BOOL` |
Used for Feature that is a boolean. |
`BOOL_ARRAY` |
Used for Feature that is a list of boolean. |
`DOUBLE` |
Used for Feature that is double. |
`DOUBLE_ARRAY` |
Used for Feature that is a list of double. |
`INT64` |
Used for Feature that is INT64. |
`INT64_ARRAY` |
Used for Feature that is a list of INT64. |
`STRING` |
Used for Feature that is string. |
`STRING_ARRAY` |
Used for Feature that is a list of String. |
`BYTES` |
Used for Feature that is bytes. |
`STRUCT` |
Used for Feature that is struct. |

## Methods

### ValueType

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespretunedmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PreTunedModel -->

# Class PreTunedModel (1.134.0)

`PreTunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A pre-tuned model for continuous tuning.

## Attributes |
|
|---|---|
Name |
Description |
`tuned_model_name` |
`str`
The resource name of the Model. E.g., a model resource name with a specified version id or alias: `projects/{project}/locations/{location}/models/{model}@{version_id}`
`projects/{project}/locations/{location}/models/{model}@{alias}`
Or, omit the version id to use the default version:
`projects/{project}/locations/{location}/models/{model}`
|
`checkpoint_id` |
`str`
Optional. The source checkpoint id. If not specified, the default checkpoint will be used. |
`base_model` |
`str`
Output only. The name of the base model this PreTunedModel was tuned from. |

## Methods

### PreTunedModel

`PreTunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A pre-tuned model for continuous tuning.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesprobehttpgetaction_googlecloudaiplatformv1schematr_a93420.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesprobehttpgetaction.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Probe.HttpGetAction -->

# Class HttpGetAction (1.134.0)

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.

## Attributes |
|
|---|---|
Name |
Description |
`path` |
`str`
Path to access on the HTTP server. |
`port` |
`int`
Number of the port to access on the container. Number must be in the range 1 to 65535. |
`host` |
`str`
Host name to connect to, defaults to the model serving container's IP. You probably want to set "Host" in httpHeaders instead. |
`scheme` |
`str`
Scheme to use for connecting to the host. Defaults to HTTP. Acceptable values are "HTTP" or "HTTPS". |
`http_headers` |
`MutableSequence[`
Custom headers to set in the request. HTTP allows repeated headers. |

## Methods

### HttpGetAction

`HttpGetAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


HttpGetAction describes an action based on HTTP Get requests.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextsentimentinputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs -->

# Class AutoMlTextSentimentInputs (1.134.0)

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attribute |
|
|---|---|
Name |
Description |
`sentiment_max` |
`int`
A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive). |

## Methods

### AutoMlTextSentimentInputs

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### AutoMlTextSentimentInputs

`AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesqueryreasoningenginerequest_googlecloudaiplatform_7214ac.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesqueryreasoningenginerequest_googlecloudaiplatform__8b0931.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesqueryreasoningenginerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryReasoningEngineRequest -->

# Class QueryReasoningEngineRequest (1.134.0)

`QueryReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [ReasoningEngineExecutionService.Query][].

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`input` |
`google.protobuf.struct_pb2.Struct`
Optional. Input content provided by users in JSON object format. Examples include text query, function calling parameters, media bytes, etc. |
`class_method` |
`str`
Optional. Class method to be used for the query. It is optional and defaults to "query" if unspecified. |

## Methods

### QueryReasoningEngineRequest

`QueryReasoningEngineRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for [ReasoningEngineExecutionService.Query][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragfileparsingconfigllmparser.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagFileParsingConfig.LlmParser -->

# Class LlmParser (1.134.0)

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`model_name` |
`str`
The name of a LLM model used for parsing. Format: - `projects/{project_id}/locations/{location}/publishers/{publisher}/models/{model}`
|
`max_parsing_requests_per_min` |
`int`
The maximum number of requests the job is allowed to make to the LLM model per minute. Consult https://cloud.google.com/vertex-ai/generative-ai/docs/quotas and your document size to set an appropriate value here. If unspecified, a default value of 5000 QPM would be used. |
`custom_parsing_prompt` |
`str`
The prompt to use for parsing. If not specified, a default prompt will be used. |

## Methods

### LlmParser

`LlmParser(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the advanced parsing for RagFiles.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types -->

# Package prediction_v1.types (1.134.0)

API documentation for `prediction_v1.types`

package.

## Classes

[ClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ClassificationPredictionResult)

Prediction output format for Image and Text Classification.

[ImageObjectDetectionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageObjectDetectionPredictionResult)

Prediction output format for Image Object Detection.

[ImageSegmentationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ImageSegmentationPredictionResult)

Prediction output format for Image Segmentation.

[TabularClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularClassificationPredictionResult)

Prediction output format for Tabular Classification.

[TabularRegressionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TabularRegressionPredictionResult)

Prediction output format for Tabular Regression.

[TextExtractionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextExtractionPredictionResult)

Prediction output format for Text Extraction.

[TextSentimentPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.TextSentimentPredictionResult)

Prediction output format for Text Sentiment

[VideoActionRecognitionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoActionRecognitionPredictionResult)

Prediction output format for Video Action Recognition.

[VideoClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoClassificationPredictionResult)

Prediction output format for Video Classification.

[VideoObjectTrackingPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.VideoObjectTrackingPredictionResult)

Prediction output format for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typeslistpersistentresourcesrequest_googlecloudaiplat_268a5f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typeslistpersistentresourcesrequest_googlecloudaiplatf_ac32d9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeslistpersistentresourcesrequest_googlecloudaiplatfo_f9f6a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistpersistentresourcesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesRequest -->

# Class ListPersistentResourcesRequest (1.134.0)

```
ListPersistentResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.ListPersistentResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PersistentResources from. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListPersistentResourcesResponse.next_page_token of the previous [PersistentResourceService.ListPersistentResource][] call. |

## Methods

### ListPersistentResourcesRequest

```
ListPersistentResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.ListPersistentResources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelmonitoringjobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsRequest -->

# Class ListModelMonitoringJobsRequest (1.134.0)

```
ListModelMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.ListModelMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}`
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
Mask specifying which fields to read |

## Methods

### ListModelMonitoringJobsRequest

```
ListModelMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.ListModelMonitoringJobs.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolnamematchmetricvalue_googlecloudaiplatfor_4bd6de.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolnamematchmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchMetricValue -->

# Class ToolNameMatchMetricValue (1.134.0)

`ToolNameMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool name match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool name match score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolNameMatchMetricValue

`ToolNameMatchMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool name match metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcallvalidmetricvalue.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidMetricValue -->

# Class ToolCallValidMetricValue (1.134.0)

`ToolCallValidMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool call valid metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Tool call valid score. This field is a member of `oneof` _ `_score` .
|

## Methods

### ToolCallValidMetricValue

`ToolCallValidMetricValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool call valid metric value for an instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesevaluatedannotationevaluatedannotationtype_google_0a526d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesevaluatedannotationevaluatedannotationtype_googlec_5cb19e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesevaluatedannotationevaluatedannotationtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotation.EvaluatedAnnotationType -->

# Class EvaluatedAnnotationType (1.134.0)

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Enums |
|
|---|---|
Name |
Description |
`EVALUATED_ANNOTATION_TYPE_UNSPECIFIED` |
Invalid value. |
`TRUE_POSITIVE` |
The EvaluatedAnnotation is a true positive. It has a prediction created by the Model and a ground truth Annotation which the prediction matches. |
`FALSE_POSITIVE` |
The EvaluatedAnnotation is false positive. It has a prediction created by the Model which does not match any ground truth annotation. |
`FALSE_NEGATIVE` |
The EvaluatedAnnotation is false negative. It has a ground truth annotation which is not matched by any of the model created predictions. |

## Methods

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturestoremonitoringconfigimportfeaturesanalysisbaseline.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeaturestoreMonitoringConfig.ImportFeaturesAnalysis.Baseline -->

# Class Baseline (1.134.0)

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.

## Enums |
|
|---|---|
Name |
Description |
`BASELINE_UNSPECIFIED` |
Should not be used. |
`LATEST_STATS` |
Choose the later one statistics generated by either most recent snapshot analysis or previous import features analysis. If non of them exists, skip anomaly detection and only generate a statistics. |
`MOST_RECENT_SNAPSHOT_STATS` |
Use the statistics generated by the most recent snapshot analysis if exists. |
`PREVIOUS_IMPORT_FEATURES_STATS` |
Use the statistics generated by the previous import features analysis if exists. |

## Methods

### Baseline

`Baseline(value)`


Defines the baseline to do anomaly detection for feature values imported by each ImportFeatureValues operation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typeswritefeaturevaluesrequest_googlecloudaiplatform_v1_b3b7bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeswritefeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.WriteFeatureValuesRequest -->

# Class WriteFeatureValuesRequest (1.134.0)

`WriteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.WriteFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the EntityType for the entities being written. Value format: `projects/{project}/locations/{location}/featurestores/ {featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`payloads` |
`MutableSequence[`
Required. The entities to be written. Up to 100,000 feature values can be written across all `payloads` .
|

## Methods

### WriteFeatureValuesRequest

`WriteFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreOnlineServingService.WriteFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistdataitemsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsRequest -->

# Class ListDataItemsRequest (1.134.0)

`ListDataItemsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDataItems.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DataItems from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDataItemsRequest

`ListDataItemsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDataItems.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesschedule___googlecloudaiplatform_v1beta1typessa_8d0806.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesschedule___googlecloudaiplatform_v1beta1typessaf_823dfd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesschedule___googlecloudaiplatform_v1beta1typessafe_9de6ad.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesschedule___googlecloudaiplatform_v1beta1typessafet_38a684.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesschedule.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule -->

# Class Schedule (1.134.0)

`Schedule(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

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
`cron` |
`str`
Cron schedule (https://en.wikipedia.org/wiki/Cron) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=${IANA_TIME_ZONE}" or "TZ=${IANA_TIME_ZONE}". The ${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*". This field is a member of `oneof` _ `time_specification` .
|
`create_pipeline_job_request` |
Request for PipelineService.CreatePipelineJob. CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}). This field is a member of `oneof` _ `request` .
|
`create_notebook_execution_job_request` |
Request for NotebookService.CreateNotebookExecutionJob. This field is a member of `oneof` _ `request` .
|
`name` |
`str`
Immutable. The resource name of the Schedule. |
`display_name` |
`str`
Required. User provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp after which the first run can be scheduled. Default to Schedule create time if not specified. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Optional. Timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either end_time is reached or when scheduled_run_count >= max_run_count. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. |
`max_run_count` |
`int`
Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either started_run_count >= max_run_count or when end_time is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified. |
`started_run_count` |
`int`
Output only. The number of runs started by this schedule. |
`state` |
Output only. The state of this Schedule. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was updated. |
`next_run_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule should schedule the next run. Having a next_run_time in the past means the runs are being started behind schedule. |
`last_pause_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was last paused. Unset if never paused. |
`last_resume_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Schedule was last resumed. Unset if never resumed from pause. |
`max_concurrent_run_count` |
`int`
Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). |
`allow_queueing` |
`bool`
Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false. |
`catch_up` |
`bool`
Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false. |
`last_scheduled_run_response` |
Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet. |

## Classes

### RunResponse

`RunResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Status of a scheduled run.

### State

`State(value)`


Possible state of the schedule.

## Methods

### Schedule

`Schedule(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typessafetyrating_googlecloudaiplatform_v1beta1ty_d90ce6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessafetyrating_googlecloudaiplatform_v1beta1typ_dc3cb7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessafetyrating.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SafetyRating -->

# Class SafetyRating (1.134.0)

`SafetyRating(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety rating corresponding to the generated content.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
Output only. Harm category. |
`probability` |
Output only. Harm probability levels in the content. |
`probability_score` |
`float`
Output only. Harm probability score. |
`severity` |
Output only. Harm severity levels in the content. |
`severity_score` |
`float`
Output only. Harm severity score. |
`blocked` |
`bool`
Output only. Indicates whether the content was filtered out because of this rating. |

## Classes

### HarmProbability

`HarmProbability(value)`


Harm probability levels in the content.

### HarmSeverity

`HarmSeverity(value)`


Harm severity levels.

## Methods

### SafetyRating

`SafetyRating(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety rating corresponding to the generated content.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesslacksourceslackchannels.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SlackSource.SlackChannels -->

# Class SlackChannels (1.134.0)

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.

## Attributes |
|
|---|---|
Name |
Description |
`channels` |
`MutableSequence[`
Required. The Slack channel IDs. |
`api_key_config` |
Required. The SecretManager secret version resource name (e.g. projects/{project}/secrets/{secret}/versions/{version}) storing the Slack channel access token that has access to the slack channel IDs. See: https://api.slack.com/tutorials/tracks/getting-a-token. |

## Classes

### SlackChannel

`SlackChannel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannel contains the Slack channel ID and the time range to import.

## Methods

### SlackChannels

`SlackChannels(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


SlackChannels contains the Slack channels and corresponding access token.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest -->

# Class ExportFeatureValuesRequest (1.134.0)

`ExportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ExportFeatureValues.

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
`snapshot_export` |
Exports the latest Feature values of all entities of the EntityType within a time range. This field is a member of `oneof` _ `mode` .
|
`full_export` |
Exports all historical values of all entities of the EntityType within a time range This field is a member of `oneof` _ `mode` .
|
`entity_type` |
`str`
Required. The resource name of the EntityType from which to export Feature values. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
|
`destination` |
Required. Specifies destination location and format. |
`feature_selector` |
Required. Selects Features to export values of. |
`settings` |
`MutableSequence[`
Per-Feature export settings. |

## Classes

### FullExport

`FullExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting all historical Feature values of all entities of the EntityType between [start_time, end_time].

### SnapshotExport

`SnapshotExport(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes exporting the latest Feature values of all entities of the EntityType between [start_time, snapshot_time].

## Methods

### ExportFeatureValuesRequest

`ExportFeatureValuesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ExportFeatureValues.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistdataitemsrequest_googlecloudaiplatform__89b3f5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistdataitemsrequest_googlecloudaiplatform_v_95f543.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistdataitemsrequest_googlecloudaiplatform_v1_81228d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistdataitemsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsRequest -->

# Class ListDataItemsRequest (1.134.0)

`ListDataItemsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDataItems.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Dataset to list DataItems from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`
|
`filter` |
`str`
The standard list filter. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |

## Methods

### ListDataItemsRequest

`ListDataItemsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDataItems.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamingpredictrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingPredictRequest -->

# Class StreamingPredictRequest (1.134.0)

`StreamingPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`inputs` |
`MutableSequence[`
The prediction input. |
`parameters` |
The parameters that govern the prediction. |

## Methods

### StreamingPredictRequest

`StreamingPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.StreamingPredict.

The first message must contain endpoint field and optionally [input][]. The subsequent messages must contain [input][].


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistcontextsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsRequest -->

# Class ListContextsRequest (1.134.0)

`ListContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListContexts

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Contexts should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Contexts to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListContexts call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Contexts to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. Following are the supported set of filters: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `schema_title` ,
`create_time` , and `update_time` . Time fields, such as
`create_time` and `update_time` , require values
specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"` .
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` . In case the
field name contains special characters (such as colon),
one can embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Parent Child filtering**: To filter Contexts based on
parent-child relationship use the HAS operator as follows:
::
parent_contexts:
"projects/ |
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListContextsRequest

`ListContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListContexts


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesnastrialdetail_googlecloudaiplatform_v1types_251846.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnastrialdetail_googlecloudaiplatform_v1typess_862dbf.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnastrialdetail.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasTrialDetail -->

# Class NasTrialDetail (1.134.0)

`NasTrialDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the NasTrialDetail. |
`parameters` |
`str`
The parameters for the NasJob NasTrial. |
`search_trial` |
`google.cloud.aiplatform_v1beta1.types.NasTrial`
The requested search NasTrial. |
`train_trial` |
`google.cloud.aiplatform_v1beta1.types.NasTrial`
The train NasTrial corresponding to search_trial. Only populated if search_trial is used for training. |

## Methods

### NasTrialDetail

`NasTrialDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetyrating.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetyRating -->

# Class SafetyRating (1.134.0)

`SafetyRating(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety rating corresponding to the generated content.

## Attributes |
|
|---|---|
Name |
Description |
`category` |
Output only. Harm category. |
`probability` |
Output only. Harm probability levels in the content. |
`probability_score` |
`float`
Output only. Harm probability score. |
`severity` |
Output only. Harm severity levels in the content. |
`severity_score` |
`float`
Output only. Harm severity score. |
`blocked` |
`bool`
Output only. Indicates whether the content was filtered out because of this rating. |

## Classes

### HarmProbability

`HarmProbability(value)`


Harm probability levels in the content.

### HarmSeverity

`HarmSeverity(value)`


Harm severity levels.

## Methods

### SafetyRating

`SafetyRating(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Safety rating corresponding to the generated content.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesapiauth_googlecloudaiplatform_v1beta1typesfea_8cb35b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesapiauth.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ApiAuth -->

# Class ApiAuth (1.134.0)

`ApiAuth(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The generic reusable api auth config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`api_key_config` |
The API secret. This field is a member of `oneof` _ `auth_config` .
|

## Classes

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API secret.

## Methods

### ApiAuth

`ApiAuth(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The generic reusable api auth config.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestorebigtableautoscaling.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Bigtable.AutoScaling -->

# Class AutoScaling (1.134.0)

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Attributes |
|
|---|---|
Name |
Description |
`min_node_count` |
`int`
Required. The minimum number of nodes to scale down to. Must be greater than or equal to 1. |
`max_node_count` |
`int`
Required. The maximum number of nodes to scale up to. Must be greater than or equal to min_node_count, and less than or equal to 10 times of 'min_node_count'. |
`cpu_utilization_target` |
`int`
Optional. A percentage of the cluster's CPU capacity. Can be from 10% to 80%. When a cluster's CPU utilization exceeds the target that you have set, Bigtable immediately adds nodes to the cluster. When CPU utilization is substantially lower than the target, Bigtable removes nodes. If not set will default to 50%. |

## Methods

### AutoScaling

`AutoScaling(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatformv1schemapredictinstance_v1typesimagesegmentationpredict_532423.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1schemapredictinstance_v1typesimagesegmentationpredicti_65a71f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schemapredictinstance_v1typesimagesegmentationpredictio_756bb6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictinstance_v1typesimagesegmentationprediction_e1a8da.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictinstance_v1typesimagesegmentationpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageSegmentationPredictionInstance -->

# Class ImageSegmentationPredictionInstance (1.134.0)

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.

## Attributes |
|
|---|---|
Name |
Description |
`content` |
`str`
The image bytes to make the predictions on. |
`mime_type` |
`str`
The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/png |

## Methods

### ImageSegmentationPredictionInstance

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.

### ImageSegmentationPredictionInstance

```
ImageSegmentationPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Image Segmentation.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_service.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service -->

# Package deployment_resource_pool_service (1.134.0)

API documentation for `aiplatform_v1.services.deployment_resource_pool_service`

package.

## Classes

[DeploymentResourcePoolServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceAsyncClient)

A service that manages the DeploymentResourcePool resource.

[DeploymentResourcePoolServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.DeploymentResourcePoolServiceClient)

A service that manages the DeploymentResourcePool resource.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers)

API documentation for `aiplatform_v1.services.deployment_resource_pool_service.pagers`

module.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragquery_googlecloudaiplatform_v1typesfetchfeature_0045ec.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragquery.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagQuery -->

# Class RagQuery (1.134.0)

`RagQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to retrieve relevant contexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`text` |
`str`
Optional. The query in text format to get relevant contexts. This field is a member of `oneof` _ `query` .
|
`rag_retrieval_config` |
Optional. The retrieval config for the query. |

## Methods

### RagQuery

`RagQuery(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A query to retrieve relevant contexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfetchfeaturevaluesresponsefeaturenamevaluepairlistfeaturenamevaluepair.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FetchFeatureValuesResponse.FeatureNameValuePairList.FeatureNameValuePair -->

# Class FeatureNameValuePair (1.134.0)

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`value` |
Feature value. This field is a member of `oneof` _ `data` .
|
`name` |
`str`
Feature short name. |

## Methods

### FeatureNameValuePair

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescreateentitytyperequest_googlecloudaiplatform_v1t_ba9dc1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescreateentitytyperequest_googlecloudaiplatform_v1ty_112021.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreateentitytyperequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEntityTypeRequest -->

# Class CreateEntityTypeRequest (1.134.0)

`CreateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateEntityType.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Featurestore to create EntityTypes. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`entity_type` |
The EntityType to create. |
`entity_type_id` |
`str`
Required. The ID to use for the EntityType, which will become the final component of the EntityType's resource name. This value may be up to 60 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within a featurestore.
|

## Methods

### CreateEntityTypeRequest

`CreateEntityTypeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateEntityType.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfunctionresponseblob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionResponseBlob -->

# Class FunctionResponseBlob (1.134.0)

`FunctionResponseBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw media bytes for function response.

Text should not be sent as raw bytes, use the 'text' field.

## Attributes |
|
|---|---|
Name |
Description |
`mime_type` |
`str`
Required. The IANA standard MIME type of the source data. |
`data` |
`bytes`
Required. Raw bytes. |
`display_name` |
`str`
Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

## Methods

### FunctionResponseBlob

`FunctionResponseBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw media bytes for function response.

Text should not be sent as raw bytes, use the 'text' field.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistcontextsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsRequest -->

# Class ListContextsRequest (1.134.0)

`ListContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListContexts

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The MetadataStore whose Contexts should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`page_size` |
`int`
The maximum number of Contexts to return. The service may return fewer. Must be in range 1-1000, inclusive. Defaults to 100. |
`page_token` |
`str`
A page token, received from a previous MetadataService.ListContexts call. Provide this to retrieve the subsequent page. When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID_ARGUMENT error.) |
`filter` |
`str`
Filter specifying the boolean condition for the Contexts to satisfy in order to be part of the result set. The syntax to define filter query is based on https://google.aip.dev/160. Following are the supported set of filters: - **Attribute filtering**: For example: `display_name = "test"` . Supported fields include:
`name` , `display_name` , `schema_title` ,
`create_time` , and `update_time` . Time fields, such as
`create_time` and `update_time` , require values
specified in RFC-3339 format. For example:
`create_time = "2020-11-19T11:30:00-04:00"` .
- **Metadata field**: To filter on metadata fields use
traversal operation as follows:
`metadata.` . For example:
`metadata.field_1.number_value = 10.0` . In case the
field name contains special characters (such as colon),
one can embed it inside double quote. For example:
`metadata."field:1".number_value = 10.0`
- **Parent Child filtering**: To filter Contexts based on
parent-child relationship use the HAS operator as follows:
::
parent_contexts:
"projects/ |
`order_by` |
`str`
How the list of messages is ordered. Specify the values to order by and an ordering operation. The default sorting order is ascending. To specify descending order for a field, users append a " desc" suffix; for example: "foo desc, bar". Subfields are specified with a `.` character, such as
foo.bar. see https://google.aip.dev/132#ordering for more
details.
|

## Methods

### ListContextsRequest

`ListContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.ListContexts


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstra_61e28b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltablesinputstransformation.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation -->

# Class Transformation (1.134.0)

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Classes

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalTransformation

`CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The categorical string as is--no change to case, punctuation, spelling, tense, and so on.
- Convert the category name to a dictionary lookup index and generate an embedding for each index.
- Categories that appear less than 5 times in the training dataset are treated as the "unknown" category. The "unknown" category gets its own special lookup index and resulting embedding.

### NumericArrayTransformation

`NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as numerical array and performs following transformation functions.

- All transformations for Numerical types applied to the average of the all elements.
- The average of empty arrays is treated as zero.

### NumericTransformation

`NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The value converted to float32.
- The z_score of the value.
- log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.
- z_score of log(value+1) when the value is greater than or equal to
- Otherwise, this transformation is not applied and the value is considered a missing value.

- A boolean value that indicates whether the value is valid.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextTransformation

`TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- The text as is--no change to case, punctuation, spelling, tense, and so on.
- Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Tokenization is based on unicode script boundaries.
- Missing values get their own lookup index and resulting embedding.
- Stop-words receive no special treatment and are not removed.

### TimestampTransformation

`TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will perform following transformation functions.

- Apply the transformation functions for Numerical columns.
- Determine the year, month, day,and weekday. Treat each value from the
- timestamp as a Categorical column.
- Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.

## Methods

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesfetchfeaturevaluesresponsefeaturenamevaluepa_064a18.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfetchfeaturevaluesresponsefeaturenamevaluepai_134e41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfetchfeaturevaluesresponsefeaturenamevaluepairlist.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchFeatureValuesResponse.FeatureNameValuePairList -->

# Class FeatureNameValuePairList (1.134.0)

`FeatureNameValuePairList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response structure in the format of key (feature name) and (feature) value pair.

## Attribute |
|
|---|---|
Name |
Description |
`features` |
`MutableSequence[`
List of feature names and values. |

## Classes

### FeatureNameValuePair

`FeatureNameValuePair(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature name & value pair.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### FeatureNameValuePairList

`FeatureNameValuePairList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response structure in the format of key (feature name) and (feature) value pair.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnastrialdetail.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasTrialDetail -->

# Class NasTrialDetail (1.134.0)

`NasTrialDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the NasTrialDetail. |
`parameters` |
`str`
The parameters for the NasJob NasTrial. |
`search_trial` |
`google.cloud.aiplatform_v1.types.NasTrial`
The requested search NasTrial. |
`train_trial` |
`google.cloud.aiplatform_v1.types.NasTrial`
The train NasTrial corresponding to search_trial. Only populated if search_trial is used for training. |

## Methods

### NasTrialDetail

`NasTrialDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents a NasTrial details along with its parameters. If there is a corresponding train NasTrial, the train NasTrial is also returned.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentati_ff5e25.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentationmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata -->

# Class AutoMlImageSegmentationMetadata (1.134.0)

```
AutoMlImageSegmentationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


## Attributes |
|
|---|---|
Name |
Description |
`cost_milli_node_hours` |
`int`
The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours. |
`successful_stop_reason` |
For successful job completions, this is the reason why the job has finished. |

## Classes

### SuccessfulStopReason

`SuccessfulStopReason(value)`


## Methods

### AutoMlImageSegmentationMetadata

```
AutoMlImageSegmentationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


### AutoMlImageSegmentationMetadata

```
AutoMlImageSegmentationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturevaluetype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Feature.ValueType -->

# Class ValueType (1.134.0)

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.

## Enums |
|
|---|---|
Name |
Description |
`VALUE_TYPE_UNSPECIFIED` |
The value type is unspecified. |
`BOOL` |
Used for Feature that is a boolean. |
`BOOL_ARRAY` |
Used for Feature that is a list of boolean. |
`DOUBLE` |
Used for Feature that is double. |
`DOUBLE_ARRAY` |
Used for Feature that is a list of double. |
`INT64` |
Used for Feature that is INT64. |
`INT64_ARRAY` |
Used for Feature that is a list of INT64. |
`STRING` |
Used for Feature that is string. |
`STRING_ARRAY` |
Used for Feature that is a list of String. |
`BYTES` |
Used for Feature that is bytes. |
`STRUCT` |
Used for Feature that is struct. |

## Methods

### ValueType

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_servicescheduleserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient -->

# Class ScheduleServiceAsyncClient (1.134.0)

```
ScheduleServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for creating and managing Vertex AI's Schedule resources to periodically launch shceudled runs to make API calls.

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
`ScheduleServiceTransport` |
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

### ScheduleServiceAsyncClient

```
ScheduleServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the schedule service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ScheduleServiceTransport,Callable[..., ScheduleServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ScheduleServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### artifact_path

```
artifact_path(
project: str, location: str, metadata_store: str, artifact: str
) -> str
```


Returns a fully-qualified artifact string.

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

### context_path

`context_path(project: str, location: str, metadata_store: str, context: str) -> str`


Returns a fully-qualified context string.

### create_schedule

```
create_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.CreateScheduleRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Creates a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_create_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[CreateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateScheduleRequest.html)(
parent="parent_value",
schedule=schedule,
)
# Make the request
response = await client.[create_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_create_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.CreateSchedule. |
`parent` |
Required. The resource name of the Location to create the Schedule in. Format: |
`schedule` |
Required. The Schedule to create. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### custom_job_path

`custom_job_path(project: str, location: str, custom_job: str) -> str`


Returns a fully-qualified custom_job string.

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

### delete_schedule

```
delete_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.DeleteScheduleRequest,
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


Deletes a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_delete_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteScheduleRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_delete_schedule)(request=request)
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
The request object. Request message for ScheduleService.DeleteSchedule. |
`name` |
Required. The name of the Schedule resource to be deleted. Format: |
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

### execution_path

```
execution_path(
project: str, location: str, metadata_store: str, execution: str
) -> str
```


Returns a fully-qualified execution string.

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
`ScheduleServiceAsyncClient` |
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
`ScheduleServiceAsyncClient` |
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
`ScheduleServiceAsyncClient` |
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

### get_schedule

```
get_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.GetScheduleRequest, dict
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Gets a Schedule.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_get_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetScheduleRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_get_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.GetSchedule. |
`name` |
Required. The name of the Schedule resource. Format: |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1.services.schedule_service.transports.base.ScheduleServiceTransport
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

### list_schedules

```
list_schedules(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest, dict
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
google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesAsyncPager
)
```


Lists Schedules in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_list_schedules():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListSchedulesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_schedules](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_list_schedules)(request=request)
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
The request object. Request message for ScheduleService.ListSchedules. |
`parent` |
Required. The resource name of the Location to list the Schedules from. Format: |
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
Response message for ScheduleService.ListSchedules Iterating over this object will yield results and resolve additional pages automatically. |

### network_attachment_path

`network_attachment_path(project: str, region: str, networkattachment: str) -> str`


Returns a fully-qualified network_attachment string.

### network_path

`network_path(project: str, network: str) -> str`


Returns a fully-qualified network string.

### notebook_execution_job_path

```
notebook_execution_job_path(
project: str, location: str, notebook_execution_job: str
) -> str
```


Returns a fully-qualified notebook_execution_job string.

### notebook_runtime_template_path

```
notebook_runtime_template_path(
project: str, location: str, notebook_runtime_template: str
) -> str
```


Returns a fully-qualified notebook_runtime_template string.

### parse_artifact_path

`parse_artifact_path(path: str) -> typing.Dict[str, str]`


Parses a artifact path into its component segments.

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

### parse_context_path

`parse_context_path(path: str) -> typing.Dict[str, str]`


Parses a context path into its component segments.

### parse_custom_job_path

`parse_custom_job_path(path: str) -> typing.Dict[str, str]`


Parses a custom_job path into its component segments.

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_network_attachment_path

`parse_network_attachment_path(path: str) -> typing.Dict[str, str]`


Parses a network_attachment path into its component segments.

### parse_network_path

`parse_network_path(path: str) -> typing.Dict[str, str]`


Parses a network path into its component segments.

### parse_notebook_execution_job_path

`parse_notebook_execution_job_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_execution_job path into its component segments.

### parse_notebook_runtime_template_path

`parse_notebook_runtime_template_path(path: str) -> typing.Dict[str, str]`


Parses a notebook_runtime_template path into its component segments.

### parse_pipeline_job_path

`parse_pipeline_job_path(path: str) -> typing.Dict[str, str]`


Parses a pipeline_job path into its component segments.

### parse_reservation_path

`parse_reservation_path(path: str) -> typing.Dict[str, str]`


Parses a reservation path into its component segments.

### parse_schedule_path

`parse_schedule_path(path: str) -> typing.Dict[str, str]`


Parses a schedule path into its component segments.

### parse_subnetwork_path

`parse_subnetwork_path(path: str) -> typing.Dict[str, str]`


Parses a subnetwork path into its component segments.

### pause_schedule

```
pause_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.PauseScheduleRequest, dict
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
) -> None
```


Pauses a Schedule. Will mark xref_Schedule.state to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_pause_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PauseScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PauseScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[pause_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_pause_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.PauseSchedule. |
`name` |
Required. The name of the Schedule resource to be paused. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### pipeline_job_path

`pipeline_job_path(project: str, location: str, pipeline_job: str) -> str`


Returns a fully-qualified pipeline_job string.

### reservation_path

```
reservation_path(
project_id_or_number: str, zone: str, reservation_name: str
) -> str
```


Returns a fully-qualified reservation string.

### resume_schedule

```
resume_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.ResumeScheduleRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
catch_up: typing.Optional[bool] = None,
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


Resumes a paused Schedule to start scheduling new runs. Will mark xref_Schedule.state to 'ACTIVE'. Only paused Schedule can be resumed.

When the Schedule is resumed, new runs will be scheduled starting from the next execution time after the current time based on the time_specification in the Schedule. If xref_Schedule.catch_up is set up true, all missed runs will be scheduled for backfill first.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_resume_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ResumeScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResumeScheduleRequest.html)(
name="name_value",
)
# Make the request
await client.[resume_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_resume_schedule)(request=request)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.ResumeSchedule. |
`name` |
Required. The name of the Schedule resource to be resumed. Format: |
`catch_up` |
Optional. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. This will also update Schedule.catch_up field. Default to false. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### schedule_path

`schedule_path(project: str, location: str, schedule: str) -> str`


Returns a fully-qualified schedule string.

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

### subnetwork_path

`subnetwork_path(project: str, region: str, subnetwork: str) -> str`


Returns a fully-qualified subnetwork string.

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

### update_schedule

```
update_schedule(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.schedule_service.UpdateScheduleRequest,
dict,
]
] = None,
*,
schedule: typing.Optional[
google.cloud.aiplatform_v1.types.schedule.Schedule
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
) -> google.cloud.aiplatform_v1.types.schedule.Schedule
```


Updates an active or paused Schedule.

When the Schedule is updated, new runs will be scheduled starting from the updated next execution time after the update time based on the time_specification in the updated Schedule. All unstarted runs before the update time will be skipped while already created runs will NOT be paused or canceled.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
async def sample_update_schedule():
# Create a client
client = aiplatform_v1.
```[ScheduleServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html)()
# Initialize request argument(s)
schedule = aiplatform_v1.[Schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Schedule.html)()
schedule.cron = "cron_value"
schedule.create_pipeline_job_request.parent = "parent_value"
schedule.display_name = "display_name_value"
schedule.max_concurrent_run_count = 2596
request = aiplatform_v1.[UpdateScheduleRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateScheduleRequest.html)(
schedule=schedule,
)
# Make the request
response = await client.[update_schedule](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.ScheduleServiceAsyncClient.html#google_cloud_aiplatform_v1_services_schedule_service_ScheduleServiceAsyncClient_update_schedule)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ScheduleService.UpdateSchedule. |
`schedule` |
Required. The Schedule which replaces the resource on the server. The following restrictions will be applied: - The scheduled request type cannot be changed. - The non-empty fields cannot be unset. - The output_only fields will be ignored if specified. This corresponds to the |
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
An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type. |

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
