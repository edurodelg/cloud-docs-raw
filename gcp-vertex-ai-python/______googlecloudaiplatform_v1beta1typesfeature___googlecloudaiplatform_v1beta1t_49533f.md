---
merged_at: 2026-01-27T07:03:43.985736
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Feature -->

# Class Feature (1.134.0)

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature Metadata information. For example, color is a feature that describes an apple.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Immutable. Name of the Feature. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}/features/{feature}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}/features/{feature}`
The last part feature is assigned by the client. The feature
can be up to 64 characters long and can consist only of
ASCII Latin letters A-Z and a-z, underscore(\_), and ASCII
digits 0-9 starting with a letter. The value will be unique
given an entity type.
|
`description` |
`str`
Description of the Feature. |
`value_type` |
Immutable. Only applicable for Vertex AI Feature Store (Legacy). Type of Feature value. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Only applicable for Vertex AI Feature Store (Legacy). Timestamp when this EntityType was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Only applicable for Vertex AI Feature Store (Legacy). Timestamp when this EntityType was most recently updated. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your Features. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one Feature (System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`monitoring_config` |
Optional. Only applicable for Vertex AI Feature Store (Legacy). Deprecated: The custom monitoring configuration for this Feature, if not set, use the monitoring_config defined for the EntityType this Feature belongs to. Only Features with type (Feature.ValueType) BOOL, STRING, DOUBLE or INT64 can enable monitoring. If this is populated with [FeaturestoreMonitoringConfig.disabled][] = true, snapshot analysis monitoring is disabled; if [FeaturestoreMonitoringConfig.monitoring_interval][] specified, snapshot analysis monitoring is enabled. Otherwise, snapshot analysis monitoring config is same as the EntityType's this Feature belongs to. |
`disable_monitoring` |
`bool`
Optional. Only applicable for Vertex AI Feature Store (Legacy). If not set, use the monitoring_config defined for the EntityType this Feature belongs to. Only Features with type (Feature.ValueType) BOOL, STRING, DOUBLE or INT64 can enable monitoring. If set to true, all types of data monitoring are disabled despite the config on EntityType. |
`monitoring_stats` |
`MutableSequence[`
Output only. Only applicable for Vertex AI Feature Store (Legacy). A list of historical SnapshotAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending. |
`monitoring_stats_anomalies` |
`MutableSequence[`
Output only. Only applicable for Vertex AI Feature Store (Legacy). The list of historical stats and anomalies with specified objectives. |
`feature_stats_and_anomaly` |
`MutableSequence[`
Output only. Only applicable for Vertex AI Feature Store. The list of historical stats and anomalies. |
`version_column_name` |
`str`
Only applicable for Vertex AI Feature Store. The name of the BigQuery Table/View column hosting data for this version. If no value is provided, will use feature_id. |
`point_of_contact` |
`str`
Entity responsible for maintaining this feature. Can be comma separated list of email addresses or URIs. |

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

### MonitoringStatsAnomaly

`MonitoringStatsAnomaly(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of historical SnapshotAnalysis or ImportFeaturesAnalysis stats requested by user, sorted by FeatureStatsAnomaly.start_time descending.

### ValueType

`ValueType(value)`


Only applicable for Vertex AI Legacy Feature Store. An enum representing the value type of a feature.

## Methods

### Feature

`Feature(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature Metadata information. For example, color is a feature that describes an apple.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchInstance -->

# Class ToolParameterKeyMatchInstance (1.134.0)

```
ToolParameterKeyMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolParameterKeyMatchInstance

```
ToolParameterKeyMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebaseTunedModelRequest -->

# Class RebaseTunedModelRequest (1.134.0)

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: `projects/{project}/locations/{location}`
|
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. |
`tuning_job` |
Optional. The TuningJob to be updated. Users can use this TuningJob field to overwrite tuning configs. |
`artifact_destination` |
Optional. The Google Cloud Storage location to write the artifacts. |
`deploy_to_same_endpoint` |
`bool`
Optional. By default, bison to gemini migration will always create new model/endpoint, but for gemini-1.0 to gemini-1.5 migration, we default deploy to the same endpoint. See details in this Section. |

## Methods

### RebaseTunedModelRequest

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UsageMetadata -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Featurestore.State -->

# Class State (1.134.0)

`State(value)`


Possible states a featurestore can have.

## Enums |
|
|---|---|
Name |
Description |
`STATE_UNSPECIFIED` |
Default value. This value is unused. |
`STABLE` |
State when the featurestore configuration is not being updated and the fields reflect the current configuration of the featurestore. The featurestore is usable in this state. |
`UPDATING` |
The state of the featurestore configuration when it is being updated. During an update, the fields reflect either the original configuration or the updated configuration of the featurestore. For example, `online_serving_config.fixed_node_count` can take minutes to update. While the update is in progress, the featurestore is in the UPDATING state, and the value of `fixed_node_count` can be the original value or the updated value, depending on the progress of the operation. Until the update completes, the actual number of nodes can still be the original value of `fixed_node_count`. The featurestore is still usable in this state. |

## Methods

### State

`State(value)`


Possible states a featurestore can have.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateVideoResponse -->

# Class GenerateVideoResponse (1.134.0)

`GenerateVideoResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Generate video response.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`generated_samples` |
`MutableSequence[str]`
The cloud storage uris of the generated videos. |
`rai_media_filtered_count` |
`int`
Returns if any videos were filtered due to RAI policies. This field is a member of `oneof` _ `_rai_media_filtered_count` .
|
`rai_media_filtered_reasons` |
`MutableSequence[str]`
Returns rai failure reasons if any. |

## Methods

### GenerateVideoResponse

`GenerateVideoResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Generate video response.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchInstance -->

# Class ToolParameterKVMatchInstance (1.134.0)

```
ToolParameterKVMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key value match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolParameterKVMatchInstance

```
ToolParameterKVMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key value match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PSCAutomationState -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorpusStatus -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest -->

# Class ImportIndexRequest (1.134.0)

`ImportIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ImportIndex.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the Index resource to import data to. Format: `projects/{project}/locations/{location}/indexes/{index}`
|
`is_complete_overwrite` |
`bool`
Optional. If true, completely replace existing index data. Must be true for streaming update indexes. |
`config` |
Required. Configuration for importing data from an external source. |

## Classes

### ConnectorConfig

`ConnectorConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for importing data from an external source.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ImportIndexRequest

`ImportIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexService.ImportIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsFilter -->

# Class SearchModelMonitoringStatsFilter (1.134.0)

```
SearchModelMonitoringStatsFilter(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Filter for searching ModelMonitoringStats.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`tabular_stats_filter` |
Tabular statistics filter. This field is a member of `oneof` _ `filter` .
|

## Classes

### TabularStatsFilter

`TabularStatsFilter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tabular statistics filter.

## Methods

### SearchModelMonitoringStatsFilter

```
SearchModelMonitoringStatsFilter(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Filter for searching ModelMonitoringStats.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchReadTensorboardTimeSeriesDataRequest -->

# Class BatchReadTensorboardTimeSeriesDataRequest (1.134.0)

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}` .
The TensorboardTimeSeries referenced by
time_series
must be sub resources of this Tensorboard.
|
`time_series` |
`MutableSequence[str]`
Required. The resource names of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### BatchReadTensorboardTimeSeriesDataRequest

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.VideoActionRecognitionPredictionParams -->

# Class VideoActionRecognitionPredictionParams (1.134.0)

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.

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
The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50. |

## Methods

### VideoActionRecognitionPredictionParams

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.

### VideoActionRecognitionPredictionParams

```
VideoActionRecognitionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Video Action Recognition.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectRawPredictResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetIndexRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentResponse -->

# Class CorroborateContentResponse (1.134.0)

`CorroborateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`corroboration_score` |
`float`
Confidence score of corroborating content. Value is [0,1] with 1 is the most confidence. This field is a member of `oneof` _ `_corroboration_score` .
|
`claims` |
`MutableSequence[`
Claims that are extracted from the input content and facts that support the claims. |

## Methods

### CorroborateContentResponse

`CorroborateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest -->

# Class RebaseTunedModelRequest (1.134.0)

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location into which to rebase the Model. Format: `projects/{project}/locations/{location}`
|
`tuned_model_ref` |
Required. TunedModel reference to retrieve the legacy model information. |
`tuning_job` |
Optional. The TuningJob to be updated. Users can use this TuningJob field to overwrite tuning configs. |
`artifact_destination` |
Optional. The Google Cloud Storage location to write the artifacts. |
`deploy_to_same_endpoint` |
`bool`
Optional. By default, bison to gemini migration will always create new model/endpoint, but for gemini-1.0 to gemini-1.5 migration, we default deploy to the same endpoint. See details in this Section. |

## Methods

### RebaseTunedModelRequest

`RebaseTunedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.RebaseTunedModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchInstance -->

# Class ToolParameterKVMatchInstance (1.134.0)

```
ToolParameterKVMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key value match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the evaluated model. This field is a member of `oneof` _ `_prediction` .
|
`reference` |
`str`
Required. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|

## Methods

### ToolParameterKVMatchInstance

```
ToolParameterKVMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for tool parameter key value match instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StructFieldValue -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorpusStatus.State -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LogprobsResult.TopCandidates -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureValueList -->

# Class FeatureValueList (1.134.0)

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[google.cloud.aiplatform_v1.types.FeatureValue]`
A list of feature values. All of them should be the same data type. |

## Methods

### FeatureValueList

`FeatureValueList(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Container for list of values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig -->

# Class RuntimeConfig (1.134.0)

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime config of a PipelineJob.

## Attributes |
|
|---|---|
Name |
Description |
`parameters` |
`MutableMapping[str, `
Deprecated. Use RuntimeConfig.parameter_values instead. The runtime parameters of the PipelineJob. The parameters will be passed into PipelineJob.pipeline_spec to replace the placeholders at runtime. This field is used by pipelines built using `PipelineJob.pipeline_spec.schema_version` 2.0.0 or lower,
such as pipelines built using Kubeflow Pipelines SDK 1.8 or
lower.
|
`gcs_output_directory` |
`str`
Required. A path in a Cloud Storage bucket, which will be treated as the root output directory of the pipeline. It is used by the system to generate the paths of output artifacts. The artifact paths are generated with a sub-path pattern `{job_id}/{task_id}/{output_key}` under the
specified output directory. The service account specified in
this pipeline must have the `storage.objects.get` and
`storage.objects.create` permissions for this bucket.
|
`parameter_values` |
`MutableMapping[str, google.protobuf.struct_pb2.Value]`
The runtime parameters of the PipelineJob. The parameters will be passed into PipelineJob.pipeline_spec to replace the placeholders at runtime. This field is used by pipelines built using `PipelineJob.pipeline_spec.schema_version` 2.1.0, such as
pipelines built using Kubeflow Pipelines SDK 1.9 or higher
and the v2 DSL.
|
`failure_policy` |
Represents the failure policy of a pipeline. Currently, the default of a pipeline is that the pipeline will continue to run until no more tasks can be executed, also known as PIPELINE_FAILURE_POLICY_FAIL_SLOW. However, if a pipeline is set to PIPELINE_FAILURE_POLICY_FAIL_FAST, it will stop scheduling any new tasks when a task has failed. Any scheduled tasks will continue to completion. |
`input_artifacts` |
`MutableMapping[str, `
The runtime artifacts of the PipelineJob. The key will be the input artifact name and the value would be one of the InputArtifact. |
`default_runtime` |
Optional. The default runtime for the PipelineJob. If not provided, Vertex Custom Job(on demand) is used as the runtime. For Vertex Custom Job, please refer to https://cloud.google.com/vertex-ai/docs/training/overview. |

## Classes

### DefaultRuntime

`DefaultRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The default runtime for the PipelineJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### InputArtifact

`InputArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of an input artifact.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### InputArtifactsEntry

`InputArtifactsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### ParametersEntry

`ParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### PersistentResourceRuntimeDetail

```
PersistentResourceRuntimeDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Persistent resource based runtime detail. For more
information, refer to
[https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview)

## Methods

### RuntimeConfig

`RuntimeConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The runtime config of a PipelineJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob -->

# Class BatchPredictionJob (1.134.0)

```
BatchPredictionJob(
batch_prediction_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves a BatchPredictionJob resource and instantiates its representation.

## Parameter |
|
|---|---|
Name |
Description |
`batch_prediction_job_name` |
`str`
Required. A fully-qualified BatchPredictionJob resource name or ID. Example: "projects/.../locations/.../batchPredictionJobs/456" or "456" when project and location are initialized or passed. |

## Properties

### completion_stats

Statistics on completed and failed prediction instances.

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

### output_info

Information describing the output of this job, including output location into which prediction output is written.

This is only available for batch prediction jobs that have run successfully.

### partial_failures

Partial failures encountered. For example, single files that can't be read. This field never exceeds 20 entries. Status details fields contain standard GCP error details.

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

## Methods

### cancel

`cancel() -> None`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

### create

```
create(
job_display_name: str,
model_name: typing.Union[str, google.cloud.aiplatform.models.Model],
instances_format: str = "jsonl",
predictions_format: str = "jsonl",
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
model_parameters: typing.Optional[typing.Dict] = None,
machine_type: typing.Optional[str] = None,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
starting_replica_count: typing.Optional[int] = None,
max_replica_count: typing.Optional[int] = None,
generate_explanation: typing.Optional[bool] = False,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
model_monitoring_objective_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
] = None,
model_monitoring_alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.AlertConfig
] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Create a batch prediction job.

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Required. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`model_name` |
`Union[str, aiplatform.Model]`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or alias in {model_name}@{version} form. Or an instance of aiplatform.Model. |
`instances_format` |
`str`
Required. The format in which instances are provided. Must be one of the formats listed in |
`predictions_format` |
`str`
Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`gcs_source` |
`Optional[Sequence[str]]`
Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`Optional[str]`
BigQuery URI to a table, up to 2000 characters long. For example: |
`gcs_destination_prefix` |
`Optional[str]`
The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`Optional[str]`
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name |
`model_parameters` |
`Optional[Dict]`
The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`Optional[str]`
The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`Optional[str]`
The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`Optional[int]`
The number of accelerators to attach to the |
`starting_replica_count` |
`Optional[int]`
The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`Optional[int]`
The maximum number of machine replicas the batch operation may be scaled to. Only used if |
`generate_explanation` |
`bool`
Optional. Generate explanation along with the batch prediction results. This will cause the batch prediction output to include explanations based on the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Explanation metadata configuration for this BatchPredictionJob. Can be specified only if |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. Can be specified only if |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`Optional[auth_credentials.Credentials]`
Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`model_monitoring_objective_config` |
`aiplatform.model_monitoring.ObjectiveConfig`
Optional. The objective config for model monitoring. Passing this parameter enables monitoring on the model associated with this batch prediction job. |
`model_monitoring_alert_config` |
`aiplatform.model_monitoring.EmailAlertConfig`
Optional. Configures how model monitoring alerts are sent to the user. Right now only email alert is supported. |
`analysis_instance_schema_uri` |
`str`
Optional. Only applicable if model_monitoring_objective_config is also passed. This parameter specifies the YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`(jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### done

`done() -> bool`


Method indicating whether a job has completed.

### iter_outputs

```
iter_outputs(
bq_max_results: typing.Optional[int] = 100,
) -> typing.Union[
typing.Iterable[storage.Blob], typing.Iterable[bigquery.table.RowIterator]
]
```


Returns an Iterable object to traverse the output files, either a list of GCS Blobs or a BigQuery RowIterator depending on the output config set when the BatchPredictionJob was created.

Parameter |
|
|---|---|
Name |
Description |
`bq_max_results` |
`typing.Optional[int]`
Optional[int] = 100 Limit on rows to retrieve from prediction table in BigQuery dataset. Only used when retrieving predictions from a bigquery_destination_prefix. Default is 100. |

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If BatchPredictionJob is in a JobState other than SUCCEEDED, since outputs cannot be retrieved until the Job has finished. |
`NotImplementedError` |
If BatchPredictionJob succeeded and output_info does not have a GCS or BQ output provided. |

Returns |
|
|---|---|
Type |
Description |
`Union[Iterable[storage.Blob], Iterable[bigquery.table.RowIterator]]` |
Either a list of GCS Blob objects within the prediction output directory or an iterable BigQuery RowIterator with predictions. |

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

### submit

```
submit(
*,
job_display_name: typing.Optional[str] = None,
model_name: typing.Union[str, google.cloud.aiplatform.models.Model],
instances_format: str = "jsonl",
predictions_format: str = "jsonl",
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
model_parameters: typing.Optional[typing.Dict] = None,
machine_type: typing.Optional[str] = None,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
starting_replica_count: typing.Optional[int] = None,
max_replica_count: typing.Optional[int] = None,
generate_explanation: typing.Optional[bool] = False,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
model_monitoring_objective_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
] = None,
model_monitoring_alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.AlertConfig
] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
service_account: typing.Optional[str] = None
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Sumbit a batch prediction job (not waiting for completion).

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Required. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`model_name` |
`Union[str, aiplatform.Model]`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or alias in {model_name}@{version} form. Or an instance of aiplatform.Model. |
`instances_format` |
`str`
Required. The format in which instances are provided. Must be one of the formats listed in |
`predictions_format` |
`str`
Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`gcs_source` |
`Optional[Sequence[str]]`
Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`Optional[str]`
BigQuery URI to a table, up to 2000 characters long. For example: |
`gcs_destination_prefix` |
`Optional[str]`
The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`Optional[str]`
The BigQuery project or dataset location where the output is to be written to. If project is provided, a new dataset is created with name |
`model_parameters` |
`Optional[Dict]`
The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`Optional[str]`
The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`Optional[str]`
The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`Optional[int]`
The number of accelerators to attach to the |
`starting_replica_count` |
`Optional[int]`
The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`Optional[int]`
The maximum number of machine replicas the batch operation may be scaled to. Only used if |
`generate_explanation` |
`bool`
Optional. Generate explanation along with the batch prediction results. This will cause the batch prediction output to include explanations based on the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Explanation metadata configuration for this BatchPredictionJob. Can be specified only if |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. Can be specified only if |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`Optional[auth_credentials.Credentials]`
Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`model_monitoring_objective_config` |
`aiplatform.model_monitoring.ObjectiveConfig`
Optional. The objective config for model monitoring. Passing this parameter enables monitoring on the model associated with this batch prediction job. |
`model_monitoring_alert_config` |
`aiplatform.model_monitoring.EmailAlertConfig`
Optional. Configures how model monitoring alerts are sent to the user. Right now only email alert is supported. |
`analysis_instance_schema_uri` |
`str`
Optional. Only applicable if model_monitoring_objective_config is also passed. This parameter specifies the YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`(jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataRequest -->

# Class BatchReadTensorboardTimeSeriesDataRequest (1.134.0)

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboard` |
`str`
Required. The resource name of the Tensorboard containing TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}` .
The TensorboardTimeSeries referenced by
time_series
must be sub resources of this Tensorboard.
|
`time_series` |
`MutableSequence[str]`
Required. The resource names of the TensorboardTimeSeries to read data from. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### BatchReadTensorboardTimeSeriesDataRequest

```
BatchReadTensorboardTimeSeriesDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchReadTensorboardTimeSeriesData.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateMemoriesRequest.DirectContentsSource.Event -->

# Class Event (1.134.0)

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.

## Attribute |
|
|---|---|
Name |
Description |
`content` |
Required. A single piece of content from which to generate memories. |

## Methods

### Event

`Event(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single piece of conversation from which to generate memories.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CopyModelOperationMetadata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookEucConfig -->

# Class NotebookEucConfig (1.134.0)

`NotebookEucConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The euc configuration of NotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`euc_disabled` |
`bool`
Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate. |
`bypass_actas_check` |
`bool`
Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine Service account. When a Runtime is created, a VM is allocated using Default Compute Engine Service Account. Any user requesting to use this Runtime requires Service Account User (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA. |

## Methods

### NotebookEucConfig

`NotebookEucConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The euc configuration of NotebookRuntimeTemplate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentResponse -->

# Class CorroborateContentResponse (1.134.0)

`CorroborateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`corroboration_score` |
`float`
Confidence score of corroborating content. Value is [0,1] with 1 is the most confidence. This field is a member of `oneof` _ `_corroboration_score` .
|
`claims` |
`MutableSequence[`
Claims that are extracted from the input content and facts that support the claims. |

## Methods

### CorroborateContentResponse

`CorroborateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for CorroborateContent.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PSCAutomationState -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetStudyRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadModelRequest -->

# Class UploadModelRequest (1.134.0)

`UploadModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UploadModel.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location into which to upload the Model. Format: `projects/{project}/locations/{location}`
|
`parent_model` |
`str`
Optional. The resource name of the model into which to upload the version. Only specify this field when uploading a new version. |
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`model` |
Required. The Model to create. |
`service_account` |
`str`
Optional. The user-provided custom service account to use to do the model upload. If empty, `Vertex AI Service Agent |

## Methods

### UploadModelRequest

`UploadModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UploadModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModelRef -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorpusStatus -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexResponse -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetIndexRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportFeatureValuesRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookEucConfig -->

# Class NotebookEucConfig (1.134.0)

`NotebookEucConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The euc configuration of NotebookRuntimeTemplate.

## Attributes |
|
|---|---|
Name |
Description |
`euc_disabled` |
`bool`
Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate. |
`bypass_actas_check` |
`bool`
Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine Service account. When a Runtime is created, a VM is allocated using Default Compute Engine Service Account. Any user requesting to use this Runtime requires Service Account User (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA. |

## Methods

### NotebookEucConfig

`NotebookEucConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The euc configuration of NotebookRuntimeTemplate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Scheduling.Strategy -->

# Class Strategy (1.134.0)

`Strategy(value)`


Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

## Enums |
|
|---|---|
Name |
Description |
`STRATEGY_UNSPECIFIED` |
Strategy will default to STANDARD. |
`ON_DEMAND` |
Deprecated. Regular on-demand provisioning strategy. |
`LOW_COST` |
Deprecated. Low cost by making potential use of spot resources. |
`STANDARD` |
Standard provisioning strategy uses regular on-demand resources. |
`SPOT` |
Spot provisioning strategy uses spot resources. |
`FLEX_START` |
Flex Start strategy uses DWS to queue for resources. |

## Methods

### Strategy

`Strategy(value)`


Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient -->

# Class ModelServiceClient (1.134.0)

```
ModelServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### ModelServiceClient

```
ModelServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the model service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the ModelServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_batch_import_evaluated_annotations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportEvaluatedAnnotationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportEvaluatedAnnotationsRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[batch_import_evaluated_annotations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_batch_import_evaluated_annotations)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.BatchImportEvaluatedAnnotations |
`parent` |
`str`
Required. The name of the parent ModelEvaluationSlice resource. Format: |
`evaluated_annotations` |
`MutableSequence[`
Required. Evaluated annotations resource to be imported. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_batch_import_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[BatchImportModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchImportModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[batch_import_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_batch_import_model_evaluation_slices)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.BatchImportModelEvaluationSlices |
`parent` |
`str`
Required. The name of the parent ModelEvaluation resource. Format: |
`model_evaluation_slices` |
`MutableSequence[`
Required. Model evaluation slice resource to be imported. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_copy_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CopyModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelRequest.html)(
model_id="model_id_value",
parent="parent_value",
source_model="source_model_value",
)
# Make the request
operation = client.[copy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_copy_model)(request=request)
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
The request object. Request message for ModelService.CopyModel. |
`parent` |
`str`
Required. The resource name of the Location into which to copy the Model. Format: |
`source_model` |
`str`
Required. The resource name of the Model to copy. That Model must be in the same Project. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_delete_model)(request=request)
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
The request object. Request message for ModelService.DeleteModel. |
`name` |
`str`
Required. The name of the Model resource to be deleted. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_model_version():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteModelVersionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelVersionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_model_version](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_delete_model_version)(request=request)
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
The request object. Request message for ModelService.DeleteModelVersion. |
`name` |
`str`
Required. The name of the model version to be deleted, with a version ID explicitly included. Example: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_export_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ExportModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest.html)(
name="name_value",
)
# Make the request
operation = client.[export_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_export_model)(request=request)
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
The request object. Request message for ModelService.ExportModel. |
`name` |
`str`
Required. The resource name of the Model to export. The resource name may contain version id or version alias to specify the version, if no version is specified, the default version will be exported. This corresponds to the |
`output_config` |
Required. The desired output location and configuration. This corresponds to the |
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
`ModelServiceClient` |
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
`ModelServiceClient` |
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
`ModelServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModel. |
`name` |
`str`
Required. The name of the Model resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModelEvaluation. |
`name` |
`str`
Required. The name of the ModelEvaluation resource. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_model_evaluation_slice():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetModelEvaluationSliceRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelEvaluationSliceRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_model_evaluation_slice](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_get_model_evaluation_slice)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.GetModelEvaluationSlice. |
`name` |
`str`
Required. The name of the ModelEvaluationSlice resource. Format: |
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
A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations. |

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
google.api_core.retry.retry_unary.Retry,
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
def sample_import_model_evaluation():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ImportModelEvaluationRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[import_model_evaluation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_import_model_evaluation)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.ImportModelEvaluation |
`parent` |
`str`
Required. The name of the parent model resource. Format: |
`model_evaluation` |
Required. Model evaluation resource to be imported. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationSlicesPager
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
def sample_list_model_evaluation_slices():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationSlicesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluation_slices](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_evaluation_slices)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluationSlices. |
`parent` |
`str`
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelEvaluationsPager
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
def sample_list_model_evaluations():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelEvaluationsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_model_evaluations](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_evaluations)(request=request)
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
The request object. Request message for ModelService.ListModelEvaluations. |
`parent` |
`str`
Required. The resource name of the Model to list the ModelEvaluations from. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsPager
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
def sample_list_model_version_checkpoints():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionCheckpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_version_checkpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_version_checkpoints)(request=request)
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
The request object. Request message for ModelService.ListModelVersionCheckpoints. |
`name` |
`str`
Required. The name of the model version to list checkpoints for. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsPager
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
def sample_list_model_versions():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelVersionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsRequest.html)(
name="name_value",
)
# Make the request
page_result = client.[list_model_versions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_model_versions)(request=request)
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
The request object. Request message for ModelService.ListModelVersions. |
`name` |
`str`
Required. The name of the model to list versions for. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelsPager
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
def sample_list_models():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListModelsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_models](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_list_models)(request=request)
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
The request object. Request message for ModelService.ListModels. |
`parent` |
`str`
Required. The resource name of the Location to list the Models from. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_merge_version_aliases():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[MergeVersionAliasesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MergeVersionAliasesRequest.html)(
name="name_value",
version_aliases=['version_aliases_value1', 'version_aliases_value2'],
)
# Make the request
response = client.[merge_version_aliases](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_merge_version_aliases)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.MergeVersionAliases. |
`name` |
`str`
Required. The name of the model version to merge aliases, with a version ID explicitly included. Example: |
`version_aliases` |
`MutableSequence[str]`
Required. The set of version aliases to merge. The alias should be at most 128 characters, and match |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_recommend_spec():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RecommendSpecRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecRequest.html)(
parent="parent_value",
gcs_uri="gcs_uri_value",
)
# Make the request
response = client.[recommend_spec](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_recommend_spec)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.RecommendSpec. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_explanation_dataset():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateExplanationDatasetRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest.html)(
model="model_value",
)
# Make the request
operation = client.[update_explanation_dataset](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_update_explanation_dataset)(request=request)
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
The request object. Request message for ModelService.UpdateExplanationDataset. |
`model` |
`str`
Required. The resource name of the Model to update. Format: |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_update_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UpdateModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelRequest.html)(
model=model,
)
# Make the request
response = client.[update_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_update_model)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for ModelService.UpdateModel. |
`model` |
Required. The Model which replaces the resource on the server. When Model Versioning is enabled, the model.name will be used to determine whether to update the model or model version. 1. model.name with the @ value, e.g. models/123@1, refers to a version specific update. 2. model.name without the @ value, e.g. models/123, refers to a model update. 3. model.name with @-, e.g. models/123@-, refers to a model update. 4. Supported model fields: display_name, description; supported version-specific fields: version_description. Labels are supported in both scenarios. Both the model labels and the version labels are merged when a model is returned. When updating labels, if the request is for model-specific update, model label gets updated. Otherwise, version labels get updated. 5. A model name or model version name fields update mismatch will cause a precondition error. 6. One request cannot update both the model and the version fields. You must update them separately. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_upload_model():
# Create a client
client = aiplatform_v1beta1.
```[ModelServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html)()
# Initialize request argument(s)
model = aiplatform_v1beta1.[Model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.html)()
model.display_name = "display_name_value"
request = aiplatform_v1beta1.[UploadModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest.html)(
parent="parent_value",
model=model,
)
# Make the request
operation = client.[upload_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.ModelServiceClient.html#google_cloud_aiplatform_v1beta1_services_model_service_ModelServiceClient_upload_model)(request=request)
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
The request object. Request message for ModelService.UploadModel. |
`parent` |
`str`
Required. The resource name of the Location into which to upload the Model. Format: |
`model` |
Required. The Model to create. This corresponds to the |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform -->

# Package aiplatform (1.134.0)

API documentation for `aiplatform`

package.

## Classes

[Artifact](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Artifact)

Metadata Artifact resource for Vertex AI

[AutoMLForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLForecastingTrainingJob)

Class to train AutoML forecasting models.

The `AutoMLForecastingTrainingJob`

class uses the AutoML training method
to train and run a forecasting model. The `AutoML`

training method is a good
choice for most forecasting use cases. If your use case doesn't benefit from
the `Seq2seq`

or the `Temporal fusion transformer`

training method offered
by the
[ SequenceToSequencePlusForecastingTrainingJob](https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob)
and
[

`TemporalFusionTransformerForecastingTrainingJob`

][https://cloud.google.com/python/docs/reference/aiplatform/latest/](https://cloud.google.com/python/docs/reference/aiplatform/latest/)

[google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob)) classes respectively, then

`AutoML`

is likely the best training method for
your forecasting predictions.For sample code that shows you how to use `AutoMLForecastingTrainingJob`

see
the [Create a training pipeline forecasting sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_sample.py)
on GitHub.

[AutoMLImageTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLImageTrainingJob)

Creates an AutoML image training job.

Use the `AutoMLImageTrainingJob`

class to create, train, and return an
image model. For more information about working with image data models
in Vertex AI, see [Image data](https://cloud.google.com/vertex-ai/docs/training-overview#image_data).

For an example of how to use the `AutoMLImageTrainingJob`

class, see the
tutorial in the [AutoML image
classification](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/migration/sdk-automl-text-classification-batch-prediction.ipynb)
notebook on GitHub.

[AutoMLTabularTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTabularTrainingJob)

Constructs a AutoML Tabular Training Job.

Example usage:

job = training_jobs.AutoMLTabularTrainingJob( display_name="my_display_name", optimization_prediction_type="classification", optimization_objective="minimize-log-loss", column_specs={"column_1": "auto", "column_2": "numeric"}, labels={'key': 'value'}, )

[AutoMLTextTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLTextTrainingJob)

Constructs a AutoML Text Training Job.

[AutoMLVideoTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.AutoMLVideoTrainingJob)

Constructs a AutoML Video Training Job.

[BatchPredictionJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.BatchPredictionJob)

Retrieves a BatchPredictionJob resource and instantiates its representation.

[CustomContainerTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomContainerTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a Container.

[CustomJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomJob)

Vertex AI Custom Job.

[CustomPythonPackageTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomPythonPackageTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a Python Package.

Use the `CustomPythonPackageTrainingJob`

class to use a Python package to
launch a custom training pipeline in Vertex AI. For an example of how to use
the `CustomPythonPackageTrainingJob`

class, see the tutorial in the [Custom
training using Python package, managed text dataset, and TensorFlow serving
container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/sdk/SDK_Custom_Training_Python_Package_Managed_Text_Dataset_Tensorflow_Serving_Container.ipynb)
notebook.

[CustomTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.CustomTrainingJob)

Class to launch a Custom Training Job in Vertex AI using a script.

Takes a training implementation as a python script and executes that script in Cloud Vertex AI Training.

[DeploymentResourcePool](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.DeploymentResourcePool)

Retrieves a DeploymentResourcePool.

[Endpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint)

Retrieves an endpoint resource.

[EntityType](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.EntityType)

Public managed EntityType resource for Vertex AI.

[Execution](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Execution)

Metadata Execution resource for Vertex AI

[Experiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Experiment)

Represents a Vertex AI Experiment resource.

[ExperimentRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ExperimentRun)

A Vertex AI Experiment run.

[Feature](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Feature)

Managed feature resource for Vertex AI.

[Featurestore](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Featurestore)

Managed featurestore resource for Vertex AI.

[HyperparameterTuningJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.HyperparameterTuningJob)

Vertex AI Hyperparameter Tuning Job.

[ImageDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ImageDataset)

A managed image dataset resource for Vertex AI.

Use this class to work with a managed image dataset. To create a managed image dataset, you need a datasource file in CSV format and a schema file in YAML format. A schema is optional for a custom model. You put the CSV file and the schema into Cloud Storage buckets.

Use image data for the following objectives:

- Single-label classification. For more information, see
[Prepare image training data for single-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#single-label-classification). - Multi-label classification. For more information, see
[Prepare image training data for multi-label classification](https://cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data#multi-label-classification). - Object detection. For more information, see
[Prepare image training data for object detection](https://cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data).

The following code shows you how to create an image dataset by importing data from a CSV datasource file and a YAML schema file. The schema file you use depends on whether your image dataset is used for single-label classification, multi-label classification, or object detection.

```
my_dataset = aiplatform.ImageDataset.create(
display_name="my-image-dataset",
gcs_source=['gs://path/to/my/image-dataset.csv'],
import_schema_uri=['gs://path/to/my/schema.yaml']
)
```


[MatchingEngineIndex](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndex)

Matching Engine index resource for Vertex AI.

[MatchingEngineIndexEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint)

Matching Engine index endpoint resource for Vertex AI.

[Model](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model)

Retrieves the model resource and instantiates its representation.

[ModelDeploymentMonitoringJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob)

Vertex AI Model Deployment Monitoring Job.

This class should be used in conjunction with the Endpoint class in order to configure model monitoring for deployed models.

[ModelEvaluation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelEvaluation)

Retrieves the ModelEvaluation resource and instantiates its representation.

[PipelineJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob)

Retrieves a PipelineJob resource and instantiates its representation.

[PipelineJobSchedule](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJobSchedule)

Retrieves a PipelineJobSchedule resource and instantiates its representation.

[PrivateEndpoint](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint)

Represents a Vertex AI PrivateEndpoint resource.

[SequenceToSequencePlusForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.SequenceToSequencePlusForecastingTrainingJob)

Class to train Sequence to Sequence (Seq2Seq) forecasting models.

The `SequenceToSequencePlusForecastingTrainingJob`

class uses the `Seq2seq+`

training method to train and run a forecasting model. The `Seq2seq+`

training method is a good choice for experimentation. Its algorithm is
simpler and uses a smaller search space than the `AutoML`

option. `Seq2seq+`

is a good option if you want fast results and your datasets are smaller than
1 GB.

For sample code that shows you how to use
`SequenceToSequencePlusForecastingTrainingJob`

, see the [Create a training
pipeline forecasting Seq2seq
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_seq2seq_sample.py)
on GitHub.

[TabularDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TabularDataset)

A managed tabular dataset resource for Vertex AI.

Use this class to work with tabular datasets. You can use a CSV file, BigQuery, or a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html)
to create a tabular dataset. For more information about paging through
BigQuery data, see

[Read data with BigQuery API using pagination](https://cloud.google.com/bigquery/docs/paging-results). For more information about tabular data, see

[Tabular data](https://cloud.google.com/vertex-ai/docs/training-overview#tabular_data).

The following code shows you how to create and import a tabular dataset with a CSV file.

```
my_dataset = aiplatform.TabularDataset.create(
display_name="my-dataset", gcs_source=['gs://path/to/my/dataset.csv'])
```


Contrary to unstructured datasets, creating and importing a tabular dataset can only be done in a single step.

If you create a tabular dataset with a pandas
[ DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html),
you need to use a BigQuery table to stage the data for Vertex AI:

```
my_dataset = aiplatform.TabularDataset.create_from_dataframe(
df_source=my_pandas_dataframe,
staging_path=f"bq://{bq_dataset_id}.table-unique"
)
```


[TemporalFusionTransformerForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TemporalFusionTransformerForecastingTrainingJob)

Class to train Temporal Fusion Transformer (TFT) forecasting models.

The `TemporalFusionTransformerForecastingTrainingJob`

class uses the
Temporal Fusion Transformer (TFT) training method to train and run a
forecasting model. The TFT training method implements an attention-based
deep neural network (DNN) model that uses a multi-horizon forecasting task
to produce predictions.

For sample code that shows you how to use
`TemporalFusionTransformerForecastingTrainingJob, see the
[Create a training pipeline forecasting temporal fusion transformer
sample](https://github.com/googleapis/python-aiplatform/blob/8ddc062669044ac0889d9f27c93a8b36c1140433/samples/model-builder/create_training_pipeline_forecasting_tft_sample.py)
on GitHub.

[Tensorboard](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Tensorboard)

Managed tensorboard resource for Vertex AI.

[TensorboardExperiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardExperiment)

Managed tensorboard resource for Vertex AI.

[TensorboardRun](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardRun)

Managed tensorboard resource for Vertex AI.

[TensorboardTimeSeries](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TensorboardTimeSeries)

Managed tensorboard resource for Vertex AI.

[TextDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TextDataset)

A managed text dataset resource for Vertex AI.

Use this class to work with a managed text dataset. To create a managed text dataset, you need a datasource file in CSV format and a schema file in YAML format. A schema is optional for a custom model. The CSV file and the schema are accessed in Cloud Storage buckets.

Use text data for the following objectives:

- Classification. For more information, see
[Prepare text training data for classification](https://cloud.google.com/vertex-ai/docs/text-data/classification/prepare-data). - Entity extraction. For more information, see
[Prepare text training data for entity extraction](https://cloud.google.com/vertex-ai/docs/text-data/entity-extraction/prepare-data). - Sentiment analysis. For more information, see [Prepare text training data for sentiment analysis](Prepare text training data for sentiment analysis).

The following code shows you how to create and import a text dataset with a CSV datasource file and a YAML schema file. The schema file you use depends on whether your text dataset is used for single-label classification, multi-label classification, or object detection.

```
my_dataset = aiplatform.TextDataset.create(
display_name="my-text-dataset",
gcs_source=['gs://path/to/my/text-dataset.csv'],
import_schema_uri=['gs://path/to/my/schema.yaml'],
)
```


[TimeSeriesDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDataset)

A managed time series dataset resource for Vertex AI.

Use this class to work with time series datasets. A time series is a dataset
that contains data recorded at different time intervals. The dataset
includes time and at least one variable that's dependent on time. You use a
time series dataset for forecasting predictions. For more information, see
[Forecasting overview](https://cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview).

You can create a managed time series dataset from CSV files in a Cloud Storage bucket or from a BigQuery table.

The following code shows you how to create a `TimeSeriesDataset`

with a CSV
file that has the time series dataset:

```
my_dataset = aiplatform.TimeSeriesDataset.create(
display_name="my-dataset",
gcs_source=['gs://path/to/my/dataset.csv'],
)
```


The following code shows you how to create with a `TimeSeriesDataset`

with a
BigQuery table file that has the time series dataset:

```
my_dataset = aiplatform.TimeSeriesDataset.create(
display_name="my-dataset",
bq_source=['bq://path/to/my/bigquerydataset.train'],
)
```


[TimeSeriesDenseEncoderForecastingTrainingJob](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDenseEncoderForecastingTrainingJob)

Class to train Time series Dense Encoder (TiDE) forecasting models.

The `TimeSeriesDenseEncoderForecastingTrainingJob`

class uses the
Time-series Dense Encoder (TiDE) training method to train and run a
forecasting model. TiDE uses a
[multi-layer perceptron](https://arxiv.org/abs/2304.08424) (MLP) to provide
the speed of forecasting linear models with covariates and non-linear
dependencies. For more information about TiDE, see
[Recent advances in deep long-horizon forecasting](https://blog.research.google/2023/04/recent-advances-in-deep-long-horizon.html)
and this
[TiDE blog post](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-forecasting).

[VideoDataset](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.VideoDataset)

A managed video dataset resource for Vertex AI.

Use this class to work with a managed video dataset. To create a video dataset, you need a datasource in CSV format and a schema in YAML format. The CSV file and the schema are accessed in Cloud Storage buckets.

Use video data for the following objectives:

Classification. For more information, see Classification schema files. Action recognition. For more information, see Action recognition schema files. Object tracking. For more information, see Object tracking schema files. The following code shows you how to create and import a dataset to train a video classification model. The schema file you use depends on whether you use your video dataset for action classification, recognition, or object tracking.

```
my_dataset = aiplatform.VideoDataset.create(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=['gs://aip.schema.dataset.ioformat.video.classification.yaml']
)
```


## Packages Functions

### autolog

`autolog(disable=False)`


Enables autologging of parameters and metrics to Vertex Experiments.

After calling `aiplatform.autolog()`

, any metrics and parameters from
model training calls with supported ML frameworks will be automatically
logged to Vertex Experiments.

Using autologging requires setting an experiment and experiment_tensorboard.

Parameter |
|
|---|---|
Name |
Description |
`disable` |
`bool` Optional. Whether to disable autologging. Defaults to False. If set to True, this resets the MLFlow tracking URI to its previous state before autologging was called and remove logging filters. |

### end_run

```
end_run(
state: google.cloud.aiplatform_v1.types.execution.Execution.State = State.COMPLETE,
)
```


Ends the the current experiment run.

```
aiplatform.start_run('my-run')
...
aiplatform.end_run()
```


### end_upload_tb_log

`end_upload_tb_log()`


Ends the current TensorBoard uploader

```
aiplatform.start_upload_tb_log(...)
...
aiplatform.end_upload_tb_log()
```


### get_experiment_df

```
get_experiment_df(
experiment: typing.Optional[str] = None, *, include_time_series: bool = True
) -> pd.DataFrame
```


Returns a Pandas DataFrame of the parameters and metrics associated with one experiment.

Example:

```
aiplatform.init(experiment='exp-1')
aiplatform.start_run(run='run-1')
aiplatform.log_params({'learning_rate': 0.1})
aiplatform.log_metrics({'accuracy': 0.9})
aiplatform.start_run(run='run-2')
aiplatform.log_params({'learning_rate': 0.2})
aiplatform.log_metrics({'accuracy': 0.95})
aiplatform.get_experiment_df()
```


Will result in the following DataFrame:

```
experiment_name | run_name | param.learning_rate | metric.accuracy
exp-1 | run-1 | 0.1 | 0.9
exp-1 | run-2 | 0.2 | 0.95
```


Parameters |
|
|---|---|
Name |
Description |
`experiment` |
`str` Name of the Experiment to filter results. If not set, return results of current active experiment. |
`include_time_series` |
`bool` Optional. Whether or not to include time series metrics in df. Default is True. Setting to False will largely improve execution time and reduce quota contributing calls. Recommended when time series metrics are not needed or number of runs in Experiment is large. For time series metrics consider querying a specific run using get_time_series_data_frame. |

### get_experiment_model

```
get_experiment_model(
artifact_id: str,
*,
metadata_store_id: str = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Retrieves an existing ExperimentModel artifact given an artifact id.

Parameters |
|
|---|---|
Name |
Description |
`artifact_id` |
`str` Required. An artifact id of the ExperimentModel artifact. |
`metadata_store_id` |
`str` Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_id is a fully-qualified resource name, its metadata_store_id overrides this one. |
`project` |
`str` Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

### get_pipeline_df

`get_pipeline_df(pipeline: str) -> pd.DataFrame`


Returns a Pandas DataFrame of the parameters and metrics associated with one pipeline.

### init

```
init(
*,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment: typing.Optional[str] = None,
experiment_description: typing.Optional[str] = None,
experiment_tensorboard: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform.tensorboard.tensorboard_resource.Tensorboard,
bool,
]
] = None,
staging_bucket: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
api_endpoint: typing.Optional[str] = None,
api_key: typing.Optional[str] = None,
api_transport: typing.Optional[str] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = None
)
```


Updates common initialization parameters with provided options.

Parameters |
|
|---|---|
Name |
Description |
`project` |
`str` The default project to use when making API calls. |
`location` |
`str` The default location to use when making API calls. If not set defaults to us-central-1. |
`experiment` |
`str` Optional. The experiment name. |
`experiment_description` |
`str` Optional. The description of the experiment. |
`experiment_tensorboard` |
`Union[str, tensorboard_resource.Tensorboard, bool]` Optional. The Vertex AI TensorBoard instance, Tensorboard resource name, or Tensorboard resource ID to use as a backing Tensorboard for the provided experiment. Example tensorboard resource name format: "projects/123/locations/us-central1/tensorboards/456" If |
`staging_bucket` |
`str` The default staging bucket to use to stage artifacts when making API calls. In the form gs://... |
`credentials` |
`google.auth.credentials.Credentials` The default custom credentials to use when making API calls. If not provided credentials will be ascertained from the environment. |
`encryption_spec_key_name` |
`Optional[str]` Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect a resource. Has the form: |
`network` |
`str` Optional. The full name of the Compute Engine network to which jobs and resources should be peered. E.g. "projects/12345/global/networks/myVPC". Private services access must already be configured for the network. If specified, all eligible jobs and resources created will be peered with this VPC. |
`service_account` |
`str` Optional. The service account used to launch jobs and deploy models. Jobs that use service_account: BatchPredictionJob, CustomJob, PipelineJob, HyperparameterTuningJob, CustomTrainingJob, CustomPythonPackageTrainingJob, CustomContainerTrainingJob, ModelEvaluationJob. |
`api_endpoint` |
`str` Optional. The desired API endpoint, e.g., us-central1-aiplatform.googleapis.com |
`api_key` |
`str` Optional. The API key to use for service calls. NOTE: Not all services support API keys. |
`api_transport` |
`str` Optional. The transport method which is either 'grpc' or 'rest'. NOTE: "rest" transport functionality is currently in a beta state (preview). |

### log

```
log(
*,
pipeline_job: typing.Optional[
google.cloud.aiplatform.pipeline_jobs.PipelineJob
] = None
)
```


Log Vertex AI Resources to the current experiment run.

```
aiplatform.start_run('my-run')
my_job = aiplatform.PipelineJob(...)
my_job.submit()
aiplatform.log(my_job)
```


Parameter |
|
|---|---|
Name |
Description |
`pipeline_job` |
`pipeline_jobs.PipelineJob` Optional. Vertex PipelineJob to associate to this Experiment Run. |

### log_classification_metrics

```
log_classification_metrics(
*,
labels: typing.Optional[typing.List[str]] = None,
matrix: typing.Optional[typing.List[typing.List[int]]] = None,
fpr: typing.Optional[typing.List[float]] = None,
tpr: typing.Optional[typing.List[float]] = None,
threshold: typing.Optional[typing.List[float]] = None,
display_name: typing.Optional[str] = None
) -> (
google.cloud.aiplatform.metadata.schema.google.artifact_schema.ClassificationMetrics
)
```


Create an artifact for classification metrics and log to ExperimentRun. Currently support confusion matrix and ROC curve.

```
my_run = aiplatform.ExperimentRun('my-run', experiment='my-experiment')
classification_metrics = my_run.log_classification_metrics(
display_name='my-classification-metrics',
labels=['cat', 'dog'],
matrix=[[9, 1], [1, 9]],
fpr=[0.1, 0.5, 0.9],
tpr=[0.1, 0.7, 0.9],
threshold=[0.9, 0.5, 0.1],
)
```


Parameters |
|
|---|---|
Name |
Description |
`labels` |
`List[str]` Optional. List of label names for the confusion matrix. Must be set if 'matrix' is set. |
`matrix` |
`List[List[int]` Optional. Values for the confusion matrix. Must be set if 'labels' is set. |
`fpr` |
`List[float]` Optional. List of false positive rates for the ROC curve. Must be set if 'tpr' or 'thresholds' is set. |
`tpr` |
`List[float]` Optional. List of true positive rates for the ROC curve. Must be set if 'fpr' or 'thresholds' is set. |
`threshold` |
`List[float]` Optional. List of thresholds for the ROC curve. Must be set if 'fpr' or 'tpr' is set. |
`display_name` |
`str` Optional. The user-defined name for the classification metric artifact. |

### log_metrics

`log_metrics(metrics: typing.Dict[str, typing.Union[float, int, str]])`


Log single or multiple Metrics with specified key and value pairs.

Metrics with the same key will be overwritten.

```
aiplatform.start_run('my-run', experiment='my-experiment')
aiplatform.log_metrics({'accuracy': 0.9, 'recall': 0.8})
```


Parameter |
|
|---|---|
Name |
Description |
`metrics` |
`Dict[str, Union[float, int, str]]` Required. Metrics key/value pairs. |

### log_model

```
log_model(
model: typing.Union[sklearn.base.BaseEstimator, xgb.Booster, tf.Module],
artifact_id: typing.Optional[str] = None,
*,
uri: typing.Optional[str] = None,
input_example: typing.Union[list, dict, pd.DataFrame, np.ndarray] = None,
display_name: typing.Optional[str] = None,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Saves a ML model into a MLMD artifact and log it to this ExperimentRun.

Supported model frameworks: sklearn, xgboost, tensorflow.

Example usage:

```
model = LinearRegression()
model.fit(X, y)
aiplatform.init(
project="my-project",
location="my-location",
staging_bucket="gs://my-bucket",
experiment="my-exp"
)
with aiplatform.start_run("my-run"):
aiplatform.log_model(model, "my-sklearn-model")
```


Parameters |
|
|---|---|
Name |
Description |
`model` |
`Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"]` Required. A machine learning model. |
`artifact_id` |
`str` Optional. The resource id of the artifact. This id must be globally unique in a metadataStore. It may be up to 63 characters, and valid characters are |
`uri` |
`str` Optional. A gcs directory to save the model file. If not provided, |
`input_example` |
`Union[list, dict, pd.DataFrame, np.ndarray]` Optional. An example of a valid model input. Will be stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. |
`display_name` |
`str` Optional. The display name of the artifact. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |

### log_params

`log_params(params: typing.Dict[str, typing.Union[float, int, str]])`


Log single or multiple parameters with specified key and value pairs.

Parameters with the same key will be overwritten.

```
aiplatform.start_run('my-run')
aiplatform.log_params({'learning_rate': 0.1, 'dropout_rate': 0.2})
```


Parameter |
|
|---|---|
Name |
Description |
`params` |
`Dict[str, Union[float, int, str]]` Required. Parameter key/value pairs. |

### log_time_series_metrics

```
log_time_series_metrics(
metrics: typing.Dict[str, float],
step: typing.Optional[int] = None,
wall_time: typing.Optional[google.protobuf.timestamp_pb2.Timestamp] = None,
)
```


Logs time series metrics to to this Experiment Run.

Requires the experiment or experiment run has a backing Vertex Tensorboard resource.

```
my_tensorboard = aiplatform.Tensorboard(...)
aiplatform.init(experiment='my-experiment', experiment_tensorboard=my_tensorboard)
aiplatform.start_run('my-run')
# increments steps as logged
for i in range(10):
aiplatform.log_time_series_metrics({'loss': loss})
# explicitly log steps
for i in range(10):
aiplatform.log_time_series_metrics({'loss': loss}, step=i)
```


Parameters |
|
|---|---|
Name |
Description |
`metrics` |
`Dict[str, Union[str, float]]` Required. Dictionary of where keys are metric names and values are metric values. |
`step` |
`int` Optional. Step index of this data point within the run. If not provided, the latest step amongst all time series metrics already logged will be used. |
`wall_time` |
`timestamp_pb2.Timestamp` Optional. Wall clock timestamp when this data point is generated by the end user. If not provided, this will be generated based on the value from time.time() |

### save_model

```
save_model(
model: typing.Union[sklearn.base.BaseEstimator, xgb.Booster, tf.Module],
artifact_id: typing.Optional[str] = None,
*,
uri: typing.Optional[str] = None,
input_example: typing.Union[list, dict, pd.DataFrame, np.ndarray] = None,
tf_save_model_kwargs: typing.Optional[typing.Dict[str, typing.Any]] = None,
display_name: typing.Optional[str] = None,
metadata_store_id: typing.Optional[str] = "default",
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
staging_bucket: typing.Optional[str] = None
) -> google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel
```


Saves a ML model into a MLMD artifact.

Supported model frameworks: sklearn, xgboost, tensorflow.

Example usage: aiplatform.init(project="my-project", location="my-location", staging_bucket="gs://my-bucket") model = LinearRegression() model.fit(X, y) aiplatform.save_model(model, "my-sklearn-model")

Parameters |
|
|---|---|
Name |
Description |
`model` |
`Union["sklearn.base.BaseEstimator", "xgb.Booster", "tf.Module"]` Required. A machine learning model. |
`artifact_id` |
`str` Optional. The resource id of the artifact. This id must be globally unique in a metadataStore. It may be up to 63 characters, and valid characters are |
`uri` |
`str` Optional. A gcs directory to save the model file. If not provided, |
`input_example` |
`Union[list, dict, pd.DataFrame, np.ndarray]` Optional. An example of a valid model input. Will be stored as a yaml file in the gcs uri. Accepts list, dict, pd.DataFrame, and np.ndarray The value inside a list must be a scalar or list. The value inside a dict must be a scalar, list, or np.ndarray. |
`tf_save_model_kwargs` |
`Dict[str, Any]` Optional. A dict of kwargs to pass to the model's save method. If saving a tf module, this will pass to "tf.saved_model.save" method. If saving a keras model, this will pass to "tf.keras.Model.save" method. |
`display_name` |
`str` Optional. The display name of the artifact. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Artifact. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Artifact. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Artifact. Overrides credentials set in aiplatform.init. |
`staging_bucket` |
`str` Optional. The staging bucket used to save the model. If not provided, the staging bucket set in aiplatform.init will be used. A staging bucket or uri is required for saving a model. |

### start_execution

```
start_execution(
*,
schema_title: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
resource_id: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict[str, typing.Any]] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
resume: bool = False,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None
) -> google.cloud.aiplatform.metadata.execution.Execution
```


Create and starts a new Metadata Execution or resumes a previously created Execution.

To start a new execution:

```
with aiplatform.start_execution(schema_title='system.ContainerExecution', display_name='trainer) as exc:
exc.assign_input_artifacts([my_artifact])
model = aiplatform.Artifact.create(uri='gs://my-uri', schema_title='system.Model')
exc.assign_output_artifacts([model])
```


To continue a previously created execution:

```
with aiplatform.start_execution(resource_id='my-exc', resume=True) as exc:
...
```


Parameters |
|
|---|---|
Name |
Description |
`schema_title` |
`str` Optional. schema_title identifies the schema title used by the Execution. Required if starting a new Execution. |
`resource_id` |
`str` Optional. The <resource_id> portion of the Execution name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/executions/<resource_id>. |
`display_name` |
`str` Optional. The user-defined name of the Execution. |
`schema_version` |
`str` Optional. schema_version specifies the version used by the Execution. If not set, defaults to use the latest version. |
`metadata` |
`Dict` Optional. Contains the metadata information that will be stored in the Execution. |
`description` |
`str` Optional. Describes the purpose of the Execution to be created. |
`metadata_store_id` |
`str` Optional. The <metadata_store_id> portion of the resource name with the format: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id> If not provided, the MetadataStore's ID will be set to "default". |
`project` |
`str` Optional. Project used to create this Execution. Overrides project set in aiplatform.init. |
`location` |
`str` Optional. Location used to create this Execution. Overrides location set in aiplatform.init. |
`credentials` |
`auth_credentials.Credentials` Optional. Custom credentials used to create this Execution. Overrides credentials set in aiplatform.init. |

### start_run

```
start_run(
run: str,
*,
tensorboard: typing.Optional[
typing.Union[
google.cloud.aiplatform.tensorboard.tensorboard_resource.Tensorboard, str
]
] = None,
resume=False
) -> google.cloud.aiplatform.metadata.experiment_run_resource.ExperimentRun
```


Start a run to current session.

```
aiplatform.init(experiment='my-experiment')
aiplatform.start_run('my-run')
aiplatform.log_params({'learning_rate':0.1})
```


Use as context manager. Run will be ended on context exit:

```
aiplatform.init(experiment='my-experiment')
with aiplatform.start_run('my-run') as my_run:
my_run.log_params({'learning_rate':0.1})
```


Resume a previously started run:

```
aiplatform.init(experiment='my-experiment')
with aiplatform.start_run('my-run', resume=True) as my_run:
my_run.log_params({'learning_rate':0.1})
```


Parameters |
|
|---|---|
Name |
Description |
`run` |
`str` Required. Name of the run to assign current session with. |
`resume` |
`bool` Whether to resume this run. If False a new run will be created. |

### start_upload_tb_log

```
start_upload_tb_log(
tensorboard_experiment_name: str,
logdir: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment_display_name: typing.Optional[str] = None,
run_name_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
allowed_plugins: typing.Optional[typing.FrozenSet[str]] = None,
)
```


Continues to listen for new data in the logdir and uploads when it appears.

Note that after calling `start_upload_tb_log()`

your thread will kept alive even if
an exception is thrown. To ensure the thread gets shut down, put any code after
`start_upload_tb_log()`

and before `end_upload_tb_log()`

in a `try`

statement, and call
`end_upload_tb_log()`

in `finally`

.

```
Sample usage:
aiplatform.init(location='us-central1', project='my-project')
aiplatform.start_upload_tb_log(tensorboard_id='123',tensorboard_experiment_name='my-experiment',logdir='my-logdir')
try:
# your code here
finally:
aiplatform.end_upload_tb_log()
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str` Required. Name of this tensorboard experiment. Unique to the given projects/{project}/locations/{location}/tensorboards/{tensorboard_id}. |
`logdir` |
`str` Required. path of the log directory to upload |
`tensorboard_id` |
`str` Optional. TensorBoard ID. If not set, tensorboard_id in aiplatform.init will be used. |
`project` |
`str` Optional. Project the TensorBoard is in. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location the TensorBoard is in. If not set, location set in aiplatform.init will be used. |
`experiment_display_name` |
`str` Optional. The display name of the experiment. |
`run_name_prefix` |
`str` Optional. If present, all runs created by this invocation will have their name prefixed by this value. |
`description` |
`str` Optional. String description to assign to the experiment. |
`allowed_plugins` |
`FrozenSet[str]` Optional. List of additional allowed plugin names. |

### upload_tb_log

```
upload_tb_log(
tensorboard_experiment_name: str,
logdir: str,
tensorboard_id: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
experiment_display_name: typing.Optional[str] = None,
run_name_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
verbosity: typing.Optional[int] = 1,
allowed_plugins: typing.Optional[typing.FrozenSet[str]] = None,
)
```


upload only the existing data in the logdir and then return immediately

```
Sample usage:
aiplatform.init(location='us-central1', project='my-project')
aiplatform.upload_tb_log(tensorboard_id='123',tensorboard_experiment_name='my-experiment',logdir='my-logdir')
```


Parameters |
|
|---|---|
Name |
Description |
`tensorboard_experiment_name` |
`str` Required. Name of this tensorboard experiment. Unique to the given projects/{project}/locations/{location}/tensorboards/{tensorboard_id} |
`logdir` |
`str` Required. The location of the TensorBoard logs that resides either in the local file system or Cloud Storage |
`tensorboard_id` |
`str` Optional. TensorBoard ID. If not set, tensorboard_id in aiplatform.init will be used. |
`project` |
`str` Optional. Project the TensorBoard is in. If not set, project set in aiplatform.init will be used. |
`location` |
`str` Optional. Location the TensorBoard is in. If not set, location set in aiplatform.init will be used. |
`experiment_display_name` |
`str` Optional. The display name of the experiment. |
`run_name_prefix` |
`str` Optional. If present, all runs created by this invocation will have their name prefixed by this value. |
`description` |
`str` Optional. String description to assign to the experiment. |
`verbosity` |
`str` Optional. Level of verbosity, an integer. Supported value: 0 - No upload statistics is printed. 1 - Print upload statistics while uploading data (default). |
`allowed_plugins` |
`FrozenSet[str]` Optional. List of additional allowed plugin names. |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportFeatureValuesRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeaturestoreRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LogprobsResult.TopCandidates -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AutoscalingMetricSpec -->

# Class AutoscalingMetricSpec (1.134.0)

`AutoscalingMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.

## Attributes |
|
|---|---|
Name |
Description |
`metric_name` |
`str`
Required. The resource metric name. Supported metrics: - For Online Prediction: - `aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle`
- `aiplatform.googleapis.com/prediction/online/cpu/utilization`
|
`target` |
`int`
The target resource utilization in percentage (1% - 100%) for the given metric; once the real usage deviates from the target by a certain percentage, the machine replicas change. The default value is 60 (representing 60%) if not provided. |

## Methods

### AutoscalingMetricSpec

`AutoscalingMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The metric specification that defines the target resource utilization (CPU utilization, accelerator's duty cycle, and so on) for calculating the desired replica count.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StructFieldValue -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorpusStatus.State -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest -->

# Class UploadModelRequest (1.134.0)

`UploadModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UploadModel.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location into which to upload the Model. Format: `projects/{project}/locations/{location}`
|
`parent_model` |
`str`
Optional. The resource name of the model into which to upload the version. Only specify this field when uploading a new version. |
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|
`model` |
Required. The Model to create. |
`service_account` |
`str`
Optional. The user-provided custom service account to use to do the model upload. If empty, `Vertex AI Service Agent |

## Methods

### UploadModelRequest

`UploadModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.UploadModel.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FasterDeploymentConfig -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataStore.MetadataStoreState -->

# Class MetadataStoreState (1.134.0)

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

## Attribute |
|
|---|---|
Name |
Description |
`disk_utilization_bytes` |
`int`
The disk utilization of the MetadataStore in bytes. |

## Methods

### MetadataStoreState

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseMetricInstance -->

# Class PairwiseMetricInstance (1.134.0)

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PairwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|

## Methods

### PairwiseMetricInstance

`PairwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk -->

# Class GroundingChunk (1.134.0)

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

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
`web` |
Grounding chunk from the web. This field is a member of `oneof` _ `chunk_type` .
|
`retrieved_context` |
Grounding chunk from context retrieved by the retrieval tools. This field is a member of `oneof` _ `chunk_type` .
|
`maps` |
Grounding chunk from Google Maps. This field is a member of `oneof` _ `chunk_type` .
|

## Classes

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Web

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### GroundingChunk

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk -->

# Class GroundingChunk (1.134.0)

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

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
`web` |
Grounding chunk from the web. This field is a member of `oneof` _ `chunk_type` .
|
`retrieved_context` |
Grounding chunk from context retrieved by the retrieval tools. This field is a member of `oneof` _ `chunk_type` .
|
`maps` |
Grounding chunk from Google Maps. This field is a member of `oneof` _ `chunk_type` .
|

## Classes

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### RetrievedContext

`RetrievedContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from context retrieved by the retrieval tools.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Web

`Web(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from the web.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### GroundingChunk

`GroundingChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Grounding chunk.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig -->

# Class TrainingPredictionSkewDetectionConfig (1.134.0)

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

## Attributes |
|
|---|---|
Name |
Description |
`skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. If a feature needs to be monitored for skew, a value threshold must be configured for that feature. The threshold here is against feature distribution distance between the training and prediction feature. |
`attribution_score_skew_thresholds` |
`MutableMapping[str, `
Key is the feature name and value is the threshold. The threshold here is against attribution score distance between the training and prediction feature. |
`default_skew_threshold` |
Skew anomaly detection threshold used by all features. When the per-feature thresholds are not set, this field can be used to specify a threshold for all features. |

## Classes

### AttributionScoreSkewThresholdsEntry

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


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

### SkewThresholdsEntry

`SkewThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### TrainingPredictionSkewDetectionConfig

```
TrainingPredictionSkewDetectionConfig(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The config for Training & Prediction data skew detection. It specifies the training dataset sources and the skew detection parameters.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CopyModelOperationMetadata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNasJobRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scheduling.Strategy -->

# Class Strategy (1.134.0)

`Strategy(value)`


Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

## Enums |
|
|---|---|
Name |
Description |
`STRATEGY_UNSPECIFIED` |
Strategy will default to STANDARD. |
`ON_DEMAND` |
Deprecated. Regular on-demand provisioning strategy. |
`LOW_COST` |
Deprecated. Low cost by making potential use of spot resources. |
`STANDARD` |
Standard provisioning strategy uses regular on-demand resources. |
`SPOT` |
Spot provisioning strategy uses spot resources. |
`FLEX_START` |
Flex Start strategy uses DWS to queue for resources. |

## Methods

### Strategy

`Strategy(value)`


Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient -->

# Class FeatureRegistryServiceClient (1.134.0)

```
FeatureRegistryServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
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

### FeatureRegistryServiceClient

```
FeatureRegistryServiceClient(
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
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the feature registry service client.

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
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the FeatureRegistryServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_batch_create_features():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1beta1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_batch_create_features)(request=request)
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature)(request=request)
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[CreateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureGroupRequest.html)(
parent="parent_value",
feature_group=feature_group,
feature_group_id="feature_group_id_value",
)
# Make the request
operation = client.[create_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.CreateFeatureGroup. |
`parent` |
`str`
Required. The resource name of the Location to create FeatureGroups. Format: |
`feature_group` |
Required. The FeatureGroup to create. This corresponds to the |
`feature_group_id` |
`str`
Required. The ID to use for this FeatureGroup, which will become the final component of the FeatureGroup's resource name. This value may be up to 128 characters, and valid characters are |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_create_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorRequest.html)(
parent="parent_value",
feature_monitor_id="feature_monitor_id_value",
)
# Make the request
operation = client.[create_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_monitor)(request=request)
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
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorRequest][]. |
`parent` |
`str`
Required. The resource name of FeatureGroup to create FeatureMonitor. Format: |
`feature_monitor` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_id` |
`str`
Required. The ID to use for this FeatureMonitor, which will become the final component of the FeatureGroup's resource name. This value may be up to 60 characters, and valid characters are |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_create_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[CreateFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureMonitorJobRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [FeatureRegistryService.CreateFeatureMonitorJobRequest][]. |
`parent` |
`str`
Required. The resource name of FeatureMonitor to create FeatureMonitorJob. Format: |
`feature_monitor_job` |
Required. The Monitor to create. This corresponds to the |
`feature_monitor_job_id` |
`int`
Optional. Output only. System-generated ID for feature monitor job. This corresponds to the |
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
from google.cloud import aiplatform_v1beta1
def sample_delete_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature)(request=request)
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureGroup. |
`name` |
`str`
Required. The name of the FeatureGroup to be deleted. Format: |
`force` |
`bool`
If set to true, any Features under this FeatureGroup will also be deleted. (Otherwise, the request will only work if the FeatureGroup has no Features.) This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_delete_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.DeleteFeatureMonitor. |
`name` |
`str`
Required. The name of the FeatureMonitor to be deleted. Format: |
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
`FeatureRegistryServiceClient` |
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
`FeatureRegistryServiceClient` |
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
`FeatureRegistryServiceClient` |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature)(request=request)
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_group)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureGroup. |
`name` |
`str`
Required. The name of the FeatureGroup resource. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_monitor)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitor. |
`name` |
`str`
Required. The name of the FeatureMonitor resource. This corresponds to the |
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
google.api_core.retry.retry_unary.Retry,
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
def sample_get_feature_monitor_job():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetFeatureMonitorJobRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_monitor_job](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_monitor_job)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for FeatureRegistryService.GetFeatureMonitorJob. |
`name` |
`str`
Required. The name of the FeatureMonitorJob resource. Format: |
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
Vertex AI Feature Monitor Job. |

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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager
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
def sample_list_feature_groups():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureGroupsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_groups](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_groups)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureGroups. |
`parent` |
`str`
Required. The resource name of the Location to list FeatureGroups. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager
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
def sample_list_feature_monitor_jobs():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorJobsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitor_jobs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_monitor_jobs)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitorJobs. |
`parent` |
`str`
Required. The resource name of the FeatureMonitor to list FeatureMonitorJobs. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager
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
def sample_list_feature_monitors():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeatureMonitorsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_monitors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_monitors)(request=request)
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
The request object. Request message for FeatureRegistryService.ListFeatureMonitors. |
`parent` |
`str`
Required. The resource name of the FeatureGroup to list FeatureMonitors. Format: |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesPager
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
def sample_list_features():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_list_features)(request=request)
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_feature():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureRequest.html)(
)
# Make the request
operation = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature)(request=request)
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
`google.api_core.operation.Operation` |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_feature_group():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1beta1.[FeatureGroup](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureGroup.html)()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1beta1.[UpdateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureGroupRequest.html)(
feature_group=feature_group,
)
# Make the request
operation = client.[update_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature_group)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureGroup. |
`feature_group` |
Required. The FeatureGroup's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureGroup resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation.Operation
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
def sample_update_feature_monitor():
# Create a client
client = aiplatform_v1beta1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[UpdateFeatureMonitorRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureMonitorRequest.html)(
)
# Make the request
operation = client.[update_feature_monitor](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1beta1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature_monitor)(request=request)
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
The request object. Request message for FeatureRegistryService.UpdateFeatureMonitor. |
`feature_monitor` |
Required. The FeatureMonitor's |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Field mask is used to specify the fields to be overwritten in the FeatureMonitor resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to |
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
