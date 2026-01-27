---
merged_at: 2026-01-27T07:03:44.008379
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedIndexOperationMetadata -->

# Class MutateDeployedIndexOperationMetadata (1.134.0)

```
MutateDeployedIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.MutateDeployedIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployed_index_id` |
`str`
The unique index id specified by user |

## Methods

### MutateDeployedIndexOperationMetadata

```
MutateDeployedIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.MutateDeployedIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportModelEvaluationRequest -->

# Class ImportModelEvaluationRequest (1.134.0)

```
ImportModelEvaluationRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ImportModelEvaluation

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the parent model resource. Format: `projects/{project}/locations/{location}/models/{model}`
|
`model_evaluation` |
Required. Model evaluation resource to be imported. |

## Methods

### ImportModelEvaluationRequest

```
ImportModelEvaluationRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ImportModelEvaluation

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityInstance -->

# Class PairwiseSummarizationQualityInstance (1.134.0)

```
PairwiseSummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the candidate model. This field is a member of `oneof` _ `_prediction` .
|
`baseline_prediction` |
`str`
Required. Output of the baseline model. This field is a member of `oneof` _ `_baseline_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to be summarized. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Summarization prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### PairwiseSummarizationQualityInstance

```
PairwiseSummarizationQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise summarization quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageSegmentationPredictionResult -->

# Class ImageSegmentationPredictionResult (1.134.0)

```
ImageSegmentationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Segmentation.

## Attributes |
|
|---|---|
Name |
Description |
`category_mask` |
`str`
A PNG image where each pixel in the mask represents the category in which the pixel in the original image was predicted to belong to. The size of this image will be the same as the original image. The mapping between the AnntoationSpec and the color can be found in model's metadata. The model will choose the most likely category and if none of the categories reach the confidence threshold, the pixel will be marked as background. |
`confidence_mask` |
`str`
A one channel image which is encoded as an 8bit lossless PNG. The size of the image will be the same as the original image. For a specific pixel, darker color means less confidence in correctness of the cateogry in the categoryMask for the corresponding pixel. Black means no confidence and white means complete confidence. |

## Methods

### ImageSegmentationPredictionResult

```
ImageSegmentationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Segmentation.

### ImageSegmentationPredictionResult

```
ImageSegmentationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image Segmentation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateSyntheticDataRequest -->

# Class GenerateSyntheticDataRequest (1.134.0)

```
GenerateSyntheticDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DataFoundryService.GenerateSyntheticData.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`task_description` |
Generate data from a high-level task description. This field is a member of `oneof` _ `strategy` .
|
`location` |
`str`
Required. The resource name of the Location to run the job. Format: `projects/{project}/locations/{location}`
|
`count` |
`int`
Required. The number of synthetic examples to generate. For this stateless API, the count is limited to a small number. |
`output_field_specs` |
`MutableSequence[`
Required. The schema of the desired output, defined by a list of fields. |
`examples` |
`MutableSequence[`
Optional. A list of few-shot examples to guide the model's output style and format. |

## Methods

### GenerateSyntheticDataRequest

```
GenerateSyntheticDataRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DataFoundryService.GenerateSyntheticData.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.feature_registry_service.pagers`

module.

## Classes

[ListFeatureGroupsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager)

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureGroupsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsPager)

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesAsyncPager)

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesPager)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types -->

# Package definition_v1beta1.types (1.134.0)

API documentation for `definition_v1beta1.types`

package.

## Classes

[AutoMlForecasting](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecasting)

A TrainingJob that trains and uploads an AutoML Forecasting Model.

[AutoMlForecastingInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs)

[AutoMlForecastingMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingMetadata)

Model metadata specific to AutoML Forecasting.

[AutoMlImageClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassification)

A TrainingJob that trains and uploads an AutoML Image Classification Model.

[AutoMlImageClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationInputs)

[AutoMlImageClassificationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageClassificationMetadata)

[AutoMlImageObjectDetection](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetection)

A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

[AutoMlImageObjectDetectionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionInputs)

[AutoMlImageObjectDetectionMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageObjectDetectionMetadata)

[AutoMlImageSegmentation](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentation)

A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

[AutoMlImageSegmentationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationInputs)

[AutoMlImageSegmentationMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlImageSegmentationMetadata)

[AutoMlTables](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTables)

A TrainingJob that trains and uploads an AutoML Tables Model.

[AutoMlTablesInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs)

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

[AutoMlTablesMetadata](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesMetadata)

Model metadata specific to AutoML Tables.

[AutoMlTextClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassification)

A TrainingJob that trains and uploads an AutoML Text Classification Model.

[AutoMlTextClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextClassificationInputs)

[AutoMlTextExtraction](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtraction)

A TrainingJob that trains and uploads an AutoML Text Extraction Model.

[AutoMlTextExtractionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs)

API documentation for `aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextExtractionInputs`

class.

[AutoMlTextSentiment](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentiment)

A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

[AutoMlTextSentimentInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTextSentimentInputs)

[AutoMlVideoActionRecognition](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognition)

A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

[AutoMlVideoActionRecognitionInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoActionRecognitionInputs)

[AutoMlVideoClassification](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassification)

A TrainingJob that trains and uploads an AutoML Video Classification Model.

[AutoMlVideoClassificationInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoClassificationInputs)

[AutoMlVideoObjectTracking](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTracking)

A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

[AutoMlVideoObjectTrackingInputs](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs)

[ExportEvaluatedDataItemsConfig](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.ExportEvaluatedDataItemsConfig)

Configuration for exporting test set predictions to a BigQuery table.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagEngineConfigRequest -->

# Class UpdateRagEngineConfigRequest (1.134.0)

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

## Attribute |
|
|---|---|
Name |
Description |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. |

## Methods

### UpdateRagEngineConfigRequest

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexRequest -->

# Class DeployIndexRequest (1.134.0)

`DeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeployIndex.

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
Required. The DeployedIndex to be created within the IndexEndpoint. |

## Methods

### DeployIndexRequest

`DeployIndexRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeployIndex.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SamplingStrategy -->

# Class SamplingStrategy (1.134.0)

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

## Attribute |
|
|---|---|
Name |
Description |
`random_sample_config` |
Random sample config. Will support more sampling strategies later. |

## Classes

### RandomSampleConfig

`RandomSampleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Requests are randomly selected.

## Methods

### SamplingStrategy

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_online_serving_service -->

# Package featurestore_online_serving_service (1.134.0)

API documentation for `aiplatform_v1.services.featurestore_online_serving_service`

package.

## Classes

[FeaturestoreOnlineServingServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceAsyncClient)

A service for serving online feature values.

[FeaturestoreOnlineServingServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceClient)

A service for serving online feature values.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetPersistentResourceRequest -->

# Class GetPersistentResourceRequest (1.134.0)

```
GetPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.GetPersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: `projects/{project_id_or_number}/locations/{location_id}/persistentResources/{persistent_resource_id}`
|

## Methods

### GetPersistentResourceRequest

```
GetPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.GetPersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringStatsDataPoint -->

# Class ModelMonitoringStatsDataPoint (1.134.0)

```
ModelMonitoringStatsDataPoint(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a single statistics data point.

## Attributes |
|
|---|---|
Name |
Description |
`current_stats` |
Statistics from current dataset. |
`baseline_stats` |
Statistics from baseline dataset. |
`threshold_value` |
`float`
Threshold value. |
`has_anomaly` |
`bool`
Indicate if the statistics has anomaly. |
`model_monitoring_job` |
`str`
Model monitoring job resource name. |
`schedule` |
`str`
Schedule resource name. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Statistics create time. |
`algorithm` |
`str`
Algorithm used to calculated the metrics, eg: jensen_shannon_divergence, l_infinity. |

## Classes

### TypedValue

`TypedValue(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Typed value of the statistics.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ModelMonitoringStatsDataPoint

```
ModelMonitoringStatsDataPoint(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a single statistics data point.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDeploymentResourcePoolRequest -->

# Class DeleteDeploymentResourcePoolRequest (1.134.0)

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DeploymentResourcePool to delete. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|

## Methods

### DeleteDeploymentResourcePoolRequest

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureOnlineStore.Optimized -->

# Class Optimized (1.134.0)

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

## Methods

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UrlContext -->

# Class UrlContext (1.134.0)

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

## Methods

### UrlContext

`UrlContext(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tool to support URL context.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (1.134.0)

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`executions` |
`MutableSequence[`
The Executions retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListExecutionsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListExecutionsResponse

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.CustomEnvironmentSpec -->

# Class CustomEnvironmentSpec (1.134.0)

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

## Attributes |
|
|---|---|
Name |
Description |
`machine_spec` |
The specification of a single machine for the execution job. |
`persistent_disk_spec` |
The specification of a persistent disk to attach for the execution job. |
`network_spec` |
The network configuration to use for the execution job. |

## Methods

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.ListDeploymentResourcePoolsAsyncPager -->

# Class ListDeploymentResourcePoolsAsyncPager (1.134.0)

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


A pager for iterating through `list_deployment_resource_pools`

requests.

This class thinly wraps an initial
[ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployment_resource_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDeploymentResourcePools`

requests and continue to iterate
through the `deployment_resource_pools`

field on the
corresponding responses.

All the usual [ListDeploymentResourcePoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDeploymentResourcePoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDeploymentResourcePoolsAsyncPager

```
ListDeploymentResourcePoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.ListDeploymentResourcePoolsResponse,
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


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.DistanceMeasureType -->

# Class DistanceMeasureType (1.134.0)

We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.

Enums

Name

Description

DISTANCE_MEASURE_TYPE_UNSPECIFIED

Should not be set.

SQUARED_L2_DISTANCE

Euclidean (L_2) Distance.

COSINE_DISTANCE

Cosine Distance. Defined as 1 - cosine similarity.

Methods

DistanceMeasureType

DistanceMeasureType(value)

We strongly suggest using DOT_PRODUCT_DISTANCE +
UNIT_L2_NORM instead of COSINE distance. Our algorithms have
been more optimized for DOT_PRODUCT distance which, when
combined with UNIT_L2_NORM, is mathematically equivalent to
COSINE distance and results in the same ranking.
DOT_PRODUCT_DISTANCE (3):
Dot Product Distance. Defined as a negative
of the dot product.

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DirectPredictRequest -->

# Class DirectPredictRequest (1.134.0)

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

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

### DirectPredictRequest

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DatasetDistribution.DistributionBucket -->

# Class DistributionBucket (1.134.0)

`DistributionBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

## Attributes |
|
|---|---|
Name |
Description |
`count` |
`int`
Output only. Number of values in the bucket. |
`left` |
`float`
Output only. Left bound of the bucket. |
`right` |
`float`
Output only. Right bound of the bucket. |

## Methods

### DistributionBucket

`DistributionBucket(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Dataset bucket used to create a histogram for the distribution given a population of values.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardExperimentRequest -->

# Class GetTensorboardExperimentRequest (1.134.0)

```
GetTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardExperiment.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardExperiment resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### GetTensorboardExperimentRequest

```
GetTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.GetTensorboardExperiment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse -->

# Class ListIndexEndpointsResponse (1.134.0)

`ListIndexEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.ListIndexEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`index_endpoints` |
`MutableSequence[`
List of IndexEndpoints in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListIndexEndpointsRequest.page_token to obtain that page. |

## Methods

### ListIndexEndpointsResponse

`ListIndexEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for IndexEndpointService.ListIndexEndpoints.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CachedContent.UsageMetadata -->

# Class UsageMetadata (1.134.0)

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

## Attributes |
|
|---|---|
Name |
Description |
`total_token_count` |
`int`
Total number of tokens that the cached content consumes. |
`text_count` |
`int`
Number of text characters. |
`image_count` |
`int`
Number of images. |
`video_duration_seconds` |
`int`
Duration of video in seconds. |
`audio_duration_seconds` |
`int`
Duration of audio in seconds. |

## Methods

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata on the usage of the cached content.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetHyperparameterTuningJobRequest -->

# Class GetHyperparameterTuningJobRequest (1.134.0)

```
GetHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob resource. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### GetHyperparameterTuningJobRequest

```
GetHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetHyperparameterTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.VideoDataset -->

# Class VideoDataset (1.134.0)

```
VideoDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


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

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### metadata_schema_uri

The metadata schema uri of this dataset resource.

### name

Name of this resource.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### VideoDataset

```
VideoDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing managed dataset given a dataset name or ID.

Parameters |
|
|---|---|
Name |
Description |
`dataset_name` |
`str`
Required. A fully-qualified dataset resource name or dataset ID. Example: "projects/123/locations/us-central1/datasets/456" or "456" when project and location are initialized or passed. |
`project` |
`str`
Optional project to retrieve dataset from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve dataset from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Custom credentials to use to retrieve this Dataset. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
import_schema_uri: typing.Optional[str] = None,
data_item_labels: typing.Optional[typing.Dict] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.video_dataset.VideoDataset
```


Creates a new video dataset.

Optionally imports data into the dataset when a source and
`import_schema_uri`

are passed in. The following is an example of how
this method is used:

```
my_dataset = aiplatform.VideoDataset.create(
gcs_source=['gs://path/to/my/dataset.csv'],
import_schema_uri=['gs://aip.schema.dataset.ioformat.video.classification.yaml']
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the dataset. The name must contain 128 or fewer UTF-8 characters. |
`gcs_source` |
`Union[str, Sequence[str]]`
The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each item in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Dataset items are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
`project` |
`str`
The name of the Google Cloud project to which this |
`location` |
`str`
The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Strings that contain metadata that's sent with the request. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Vertex AI Tensorboards. The maximum length of a key and of a value is 64 unicode characters. Labels and keys can contain only lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (system labels are excluded). For more information and examples of using labels, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key that's used to protect the dataset. The format of the key is |
`sync` |
`bool`
If |
`create_request_timeout` |
`float`
Optional. The number of seconds for the timeout of the create request. |

Returns |
|
|---|---|
Type |
Description |
`video_dataset (VideoDataset)` |
An instantiated representation of the managed `VideoDataset` resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### export_data

`export_data(output_dir: str) -> typing.Sequence[str]`


Exports data to output dir to GCS.

Parameter |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |

Returns |
|
|---|---|
Type |
Description |
`exported_files (Sequence[str])` |
All of the files that are exported in this export operation. |

### export_data_for_custom_training

```
export_data_for_custom_training(
output_dir: str,
annotation_filter: typing.Optional[str] = None,
saved_query_id: typing.Optional[str] = None,
annotation_schema_uri: typing.Optional[str] = None,
split: typing.Optional[
typing.Union[typing.Dict[str, str], typing.Dict[str, float]]
] = None,
) -> typing.Dict[str, typing.Any]
```


Exports data to output dir to GCS for custom training use case.

Example annotation_schema_uri (image classification): gs://google-cloud-aiplatform/schema/dataset/annotation/image_classification_1.0.0.yaml

Example split (filter split): { "training_filter": "labels.aiplatform.googleapis.com/ml_use=training", "validation_filter": "labels.aiplatform.googleapis.com/ml_use=validation", "test_filter": "labels.aiplatform.googleapis.com/ml_use=test", } Example split (fraction split): { "training_fraction": 0.7, "validation_fraction": 0.2, "test_fraction": 0.1, }

Parameters |
|
|---|---|
Name |
Description |
`output_dir` |
`str`
Required. The Google Cloud Storage location where the output is to be written to. In the given directory a new directory will be created with name: |
`annotation_filter` |
`str`
Optional. An expression for filtering what part of the Dataset is to be exported. Only Annotations that match this filter will be exported. The filter syntax is the same as in |
`saved_query_id` |
`str`
Optional. The ID of a SavedQuery (annotation set) under this Dataset used for filtering Annotations for training. Only used for custom training data export use cases. Only applicable to Datasets that have SavedQueries. Only Annotations that are associated with this SavedQuery are used in respectively training. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both saved_query_id and annotations_filter. Only one of saved_query_id and annotation_schema_uri should be specified as both of them represent the same thing: problem type. |
`annotation_schema_uri` |
`str`
Optional. The Cloud Storage URI that points to a YAML file describing the annotation schema. The schema is defined as an OpenAPI 3.0.2 Schema Object. The schema files that can be used here are found in gs://google-cloud-aiplatform/schema/dataset/annotation/, note that the chosen schema must be consistent with metadata_schema_uri of this Dataset. Only used for custom training data export use cases. Only applicable if this Dataset that have DataItems and Annotations. Only Annotations that both match this schema and belong to DataItems not ignored by the split method are used in respectively training, validation or test role, depending on the role of the DataItem they are on. When used in conjunction with annotations_filter, the Annotations used for training are filtered by both annotations_filter and annotation_schema_uri. |
`split` |
`Union[Dict[str, str], Dict[str, float]]`
The instructions how the export data should be split between the training, validation and test sets. |

Returns |
|
|---|---|
Type |
Description |
`export_data_response (Dict)` |
Response message for DatasetService.ExportData in Dictionary format. |

### import_data

```
import_data(
gcs_source: typing.Union[str, typing.Sequence[str]],
import_schema_uri: str,
data_item_labels: typing.Optional[typing.Dict] = None,
sync: bool = True,
import_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Upload data to existing managed dataset.

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Instantiated representation of the managed dataset resource. |

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


List all instances of this Dataset resource.

Example Usage:

aiplatform.TabularDataset.list( filter='labels.my_key="my_value"', order_by='display_name' )

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

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
description: typing.Optional[str] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.datasets.dataset._Dataset
```


Update the dataset. Updatable fields:

`display_name`

`description`

`labels`


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the Dataset. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`labels` |
`Dict[str, str]`
Optional. Labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See |
`description` |
`str`
Optional. The description of the Dataset. |
`update_request_timeout` |
`float`
Optional. The timeout for the update request in seconds. |

Returns |
|
|---|---|
Type |
Description |
`dataset (Dataset)` |
Updated dataset. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient -->

# Class EndpointServiceAsyncClient (1.134.0)

```
EndpointServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
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
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport,
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
google.cloud.aiplatform_v1.types.endpoint_service.CreateEndpointRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_create_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[CreateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateEndpointRequest.html)(
parent="parent_value",
endpoint=endpoint,
)
# Make the request
operation = client.[create_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_create_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.DeleteEndpointRequest,
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
from google.cloud import aiplatform_v1
async def sample_delete_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteEndpointRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_delete_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.DeployModelRequest, dict
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
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
from google.cloud import aiplatform_v1
async def sample_deploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[DeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[deploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_deploy_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.GetEndpointRequest, dict
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_get_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetEndpointRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_get_endpoint)(request=request)
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
google.cloud.aiplatform_v1.services.endpoint_service.transports.base.EndpointServiceTransport
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
google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest, dict
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
google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsAsyncPager
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
from google.cloud import aiplatform_v1
async def sample_list_endpoints():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListEndpointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_endpoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_list_endpoints)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.MutateDeployedModelRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[str] = None,
deployed_model: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.DeployedModel
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
from google.cloud import aiplatform_v1
async def sample_mutate_deployed_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
deployed_model = aiplatform_v1.[DeployedModel](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedModel.html)()
deployed_model.dedicated_resources.min_replica_count = 1803
request = aiplatform_v1.[MutateDeployedModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MutateDeployedModelRequest.html)(
endpoint="endpoint_value",
deployed_model=deployed_model,
)
# Make the request
operation = client.[mutate_deployed_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_mutate_deployed_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UndeployModelRequest, dict
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
from google.cloud import aiplatform_v1
async def sample_undeploy_model():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UndeployModelRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelRequest.html)(
endpoint="endpoint_value",
deployed_model_id="deployed_model_id_value",
)
# Make the request
operation = client.[undeploy_model](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_undeploy_model)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
) -> google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_update_endpoint():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointRequest.html)(
endpoint=endpoint,
)
# Make the request
response = await client.[update_endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint)(request=request)
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
google.cloud.aiplatform_v1.types.endpoint_service.UpdateEndpointLongRunningRequest,
dict,
]
] = None,
*,
endpoint: typing.Optional[
google.cloud.aiplatform_v1.types.endpoint.Endpoint
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
from google.cloud import aiplatform_v1
async def sample_update_endpoint_long_running():
# Create a client
client = aiplatform_v1.
```[EndpointServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html)()
# Initialize request argument(s)
endpoint = aiplatform_v1.[Endpoint](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Endpoint.html)()
endpoint.display_name = "display_name_value"
request = aiplatform_v1.[UpdateEndpointLongRunningRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest.html)(
endpoint=endpoint,
)
# Make the request
operation = client.[update_endpoint_long_running](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient.html#google_cloud_aiplatform_v1_services_endpoint_service_EndpointServiceAsyncClient_update_endpoint_long_running)(request=request)
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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesPager

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse -->

# Class ListEntityTypesResponse (1.134.0)

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`entity_types` |
`MutableSequence[`
The EntityTypes matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListEntityTypesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListEntityTypesResponse

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeletePersistentResourceRequest -->

# Class DeletePersistentResourceRequest (1.134.0)

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|

## Methods

### DeletePersistentResourceRequest

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PredictSchemata -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentRequest -->

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryExtensionResponse -->

# Class QueryExtensionResponse (1.134.0)

`QueryExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.QueryExtension.

## Attributes |
|
|---|---|
Name |
Description |
`steps` |
`MutableSequence[`
Steps of extension or LLM interaction, can contain function call, function response, or text response. The last step contains the final response to the query. |
`failure_message` |
`str`
Failure message if any. |

## Methods

### QueryExtensionResponse

`QueryExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.QueryExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse -->

# Class ListPublisherModelsResponse (1.134.0)

`ListPublisherModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.ListPublisherModels.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_models` |
`MutableSequence[`
List of PublisherModels in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to [ListPublisherModels.page_token][] to obtain that page. |

## Methods

### ListPublisherModelsResponse

`ListPublisherModelsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelGardenService.ListPublisherModels.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsRequest -->

# Class ListCustomJobsRequest (1.134.0)

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: `projects/{project}/locations/{location}`
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
The standard list page token. Typically obtained via ListCustomJobsResponse.next_page_token of the previous JobService.ListCustomJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListCustomJobsRequest

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.PersistentResourceRuntimeDetail -->

# Class PersistentResourceRuntimeDetail (1.134.0)

```
PersistentResourceRuntimeDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Persistent resource based runtime detail. For more
information, refer to
[https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview)

## Attributes |
|
|---|---|
Name |
Description |
`persistent_resource_name` |
`str`
Persistent resource name. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|
`task_resource_unavailable_wait_time_ms` |
`int`
The max time a pipeline task waits for the required CPU, memory, or accelerator resource to become available from the specified persistent resource. Default wait time is 0. |
`task_resource_unavailable_timeout_behavior` |
Specifies the behavior to take if the timeout is reached. |

## Classes

### TaskResourceUnavailableTimeoutBehavior

`TaskResourceUnavailableTimeoutBehavior(value)`


An enum that specifies the behavior to take if the timeout is reached.

## Methods

### PersistentResourceRuntimeDetail

```
PersistentResourceRuntimeDetail(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Persistent resource based runtime detail. For more
information, refer to
[https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview](https://cloud.google.com/vertex-ai/docs/training/persistent-resource-overview)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigRequest -->

# Class UpdateRagEngineConfigRequest (1.134.0)

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

## Attribute |
|
|---|---|
Name |
Description |
`rag_engine_config` |
Required. The updated RagEngineConfig. NOTE: Downgrading your RagManagedDb's ComputeTier could temporarily increase request latencies until the operation is fully complete. |

## Methods

### UpdateRagEngineConfigRequest

```
UpdateRagEngineConfigRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for VertexRagDataService.UpdateRagEngineConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service -->

# Package job_service (1.134.0)

API documentation for `aiplatform_v1.services.job_service`

package.

## Classes

[JobServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceAsyncClient)

A service for creating and managing Vertex AI's jobs.

[JobServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.JobServiceClient)

A service for creating and managing Vertex AI's jobs.

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers)

API documentation for `aiplatform_v1.services.job_service.pagers`

module.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetNotebookRuntimeTemplateRequest -->

# Class GetNotebookRuntimeTemplateRequest (1.134.0)

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### GetNotebookRuntimeTemplateRequest

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues.Feature.FeatureValueAndTimestamp -->

# Class FeatureValueAndTimestamp (1.134.0)

`FeatureValueAndTimestamp(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature value and timestamp.

## Attributes |
|
|---|---|
Name |
Description |
`value` |
The feature value. |
`timestamp` |
`google.protobuf.timestamp_pb2.Timestamp`
The feature timestamp to store with this value. If not set, then the Feature Store server will generate a timestamp when it receives the write request. |

## Methods

### FeatureValueAndTimestamp

`FeatureValueAndTimestamp(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature value and timestamp.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Part -->

# Class Part (1.134.0)

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

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
`text` |
`str`
Optional. Text part (can be code). This field is a member of `oneof` _ `data` .
|
`inline_data` |
Optional. Inlined bytes data. This field is a member of `oneof` _ `data` .
|
`file_data` |
Optional. URI based data. This field is a member of `oneof` _ `data` .
|
`function_call` |
Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values. This field is a member of `oneof` _ `data` .
|
`function_response` |
Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model. This field is a member of `oneof` _ `data` .
|
`executable_code` |
Optional. Code generated by the model that is meant to be executed. This field is a member of `oneof` _ `data` .
|
`code_execution_result` |
Optional. Result of executing the [ExecutableCode]. This field is a member of `oneof` _ `data` .
|
`thought` |
`bool`
Indicates if the part is thought from the model. |
`thought_signature` |
`bytes`
An opaque signature for the thought so it can be reused in subsequent requests. |
`video_metadata` |
Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data. This field is a member of `oneof` _ `metadata` .
|

## Methods

### Part

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListOptimalTrialsResponse -->

# Class ListOptimalTrialsResponse (1.134.0)

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`optimal_trials` |
`MutableSequence[`
The pareto-optimal Trials for multiple objective Study or the optimal trial for single objective Study. The definition of pareto-optimal can be checked in wiki page. https://en.wikipedia.org/wiki/Pareto_efficiency |

## Methods

### ListOptimalTrialsResponse

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SamplingStrategy -->

# Class SamplingStrategy (1.134.0)

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

## Attribute |
|
|---|---|
Name |
Description |
`random_sample_config` |
Random sample config. Will support more sampling strategies later. |

## Classes

### RandomSampleConfig

`RandomSampleConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Requests are randomly selected.

## Methods

### SamplingStrategy

`SamplingStrategy(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Sampling Strategy for logging, can be for both training and prediction dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PredictSchemata -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.index_service.pagers`

module.

## Classes

[ListIndexesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesAsyncPager)

```
ListIndexesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__aiter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListIndexesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_service.pagers.ListIndexesPager)

```
ListIndexesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse
],
request: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesRequest,
response: google.cloud.aiplatform_v1beta1.types.index_service.ListIndexesResponse,
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


A pager for iterating through `list_indexes`

requests.

This class thinly wraps an initial
[ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse) object, and
provides an `__iter__`

method to iterate through its
`indexes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexes`

requests and continue to iterate
through the `indexes`

field on the
corresponding responses.

All the usual [ListIndexesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentRequest -->

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsRequest -->

# Class ListCustomJobsRequest (1.134.0)

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the CustomJobs from. Format: `projects/{project}/locations/{location}`
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
The standard list page token. Typically obtained via ListCustomJobsResponse.next_page_token of the previous JobService.ListCustomJobs call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListCustomJobsRequest

`ListCustomJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for JobService.ListCustomJobs.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDeploymentResourcePoolRequest -->

# Class DeleteDeploymentResourcePoolRequest (1.134.0)

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DeploymentResourcePool to delete. Format: `projects/{project}/locations/{location}/deploymentResourcePools/{deployment_resource_pool}`
|

## Methods

### DeleteDeploymentResourcePoolRequest

```
DeleteDeploymentResourcePoolRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for DeleteDeploymentResourcePool method.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExecutionsResponse -->

# Class ListExecutionsResponse (1.134.0)

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

## Attributes |
|
|---|---|
Name |
Description |
`executions` |
`MutableSequence[`
The Executions retrieved from the MetadataStore. |
`next_page_token` |
`str`
A token, which can be sent as ListExecutionsRequest.page_token to retrieve the next page. If this field is not populated, there are no subsequent pages. |

## Methods

### ListExecutionsResponse

`ListExecutionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MetadataService.ListExecutions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetModelMonitoringJobRequest -->

# Class GetModelMonitoringJobRequest (1.134.0)

```
GetModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.GetModelMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMonitors/{model_monitor}/modelMonitoringJobs/{model_monitoring_job}`
|

## Methods

### GetModelMonitoringJobRequest

```
GetModelMonitoringJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelMonitoringService.GetModelMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookExecutionJob.CustomEnvironmentSpec -->

# Class CustomEnvironmentSpec (1.134.0)

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

## Attributes |
|
|---|---|
Name |
Description |
`machine_spec` |
The specification of a single machine for the execution job. |
`persistent_disk_spec` |
The specification of a persistent disk to attach for the execution job. |
`network_spec` |
The network configuration to use for the execution job. |

## Methods

### CustomEnvironmentSpec

`CustomEnvironmentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Compute configuration to use for an execution job.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Part -->

# Class Part (1.134.0)

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

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
`text` |
`str`
Optional. Text part (can be code). This field is a member of `oneof` _ `data` .
|
`inline_data` |
Optional. Inlined bytes data. This field is a member of `oneof` _ `data` .
|
`file_data` |
Optional. URI based data. This field is a member of `oneof` _ `data` .
|
`function_call` |
Optional. A predicted [FunctionCall] returned from the model that contains a string representing the [FunctionDeclaration.name] with the parameters and their values. This field is a member of `oneof` _ `data` .
|
`function_response` |
Optional. The result output of a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function call. It is used as context to the model. This field is a member of `oneof` _ `data` .
|
`executable_code` |
Optional. Code generated by the model that is meant to be executed. This field is a member of `oneof` _ `data` .
|
`code_execution_result` |
Optional. Result of executing the [ExecutableCode]. This field is a member of `oneof` _ `data` .
|
`video_metadata` |
Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data. This field is a member of `oneof` _ `metadata` .
|
`thought` |
`bool`
Indicates if the part is thought from the model. |
`thought_signature` |
`bytes`
An opaque signature for the thought so it can be reused in subsequent requests. |

## Methods

### Part

`Part(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datatype containing media that is part of a multi-part `Content`

message.

A `Part`

consists of data which has an associated datatype. A
`Part`

can only contain one of the accepted types in
`Part.data`

.

A `Part`

must have a fixed IANA MIME type identifying the type and
subtype of the media if `inline_data`

or `file_data`

field is
filled with raw bytes.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployRequest.ModelConfig -->

# Class ModelConfig (1.134.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`accept_eula` |
`bool`
Optional. Whether the user accepts the End User License Agreement (EULA) for the model. |
`hugging_face_access_token` |
`str`
Optional. The Hugging Face read access token used to access the model artifacts of gated models. |
`hugging_face_cache_enabled` |
`bool`
Optional. If true, the model will deploy with a cached version instead of directly downloading the model artifacts from Hugging Face. This is suitable for VPC-SC users with limited internet access. |
`model_display_name` |
`str`
Optional. The user-specified display name of the uploaded model. If not set, a default name will be used. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying. If not set, the default container spec will be used. |
`model_user_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. When not provided, Vertex AI will generate a value for this ID. When Model Registry model is provided, this field will be ignored. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DirectPredictRequest -->

# Class DirectPredictRequest (1.134.0)

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

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

### DirectPredictRequest

`DirectPredictRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.DirectPredict.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TensorboardBlob -->

# Class TensorboardBlob (1.134.0)

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project. |
`data` |
`bytes`
Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint. |

## Methods

### TensorboardBlob

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.vertex_rag_data_service.pagers`

module.

## Classes

[ListRagCorporaAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaAsyncPager)

```
ListRagCorporaAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagCorporaPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaPager)

```
ListRagCorporaPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagCorporaResponse,
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


A pager for iterating through `list_rag_corpora`

requests.

This class thinly wraps an initial
[ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_corpora`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagCorpora`

requests and continue to iterate
through the `rag_corpora`

field on the
corresponding responses.

All the usual [ListRagCorporaResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagCorporaResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagFilesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager)

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse) object, and
provides an `__aiter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListRagFilesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagFilesPager)

```
ListRagFilesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1beta1.types.vertex_rag_data_service.ListRagFilesResponse,
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


A pager for iterating through `list_rag_files`

requests.

This class thinly wraps an initial
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse) object, and
provides an `__iter__`

method to iterate through its
`rag_files`

field.

If there are more pages, the `__iter__`

method will make additional
`ListRagFiles`

requests and continue to iterate
through the `rag_files`

field on the
corresponding responses.

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse -->

# Class ListEventsResponse (1.134.0)

`ListEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListEvents.

## Attributes |
|
|---|---|
Name |
Description |
`session_events` |
`MutableSequence[`
A list of events matching the request. Ordered by timestamp in ascending order. |
`next_page_token` |
`str`
A token, which can be sent as ListEventsRequest.page_token to retrieve the next page. Absence of this field indicates there are no subsequent pages. |

## Methods

### ListEventsResponse

`ListEventsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for SessionService.ListEvents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse -->

# Class ListEntityTypesResponse (1.134.0)

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

## Attributes |
|
|---|---|
Name |
Description |
`entity_types` |
`MutableSequence[`
The EntityTypes matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListEntityTypesRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListEntityTypesResponse

`ListEntityTypesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListEntityTypes.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service -->

# Package reasoning_engine_execution_service (1.134.0)

API documentation for `aiplatform_v1.services.reasoning_engine_execution_service`

package.

## Classes

[ReasoningEngineExecutionServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceAsyncClient)

A service for executing queries on Reasoning Engine.

[ReasoningEngineExecutionServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_execution_service.ReasoningEngineExecutionServiceClient)

A service for executing queries on Reasoning Engine.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeletePersistentResourceRequest -->

# Class DeletePersistentResourceRequest (1.134.0)

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource to be deleted. Format: `projects/{project}/locations/{location}/persistentResources/{persistent_resource}`
|

## Methods

### DeletePersistentResourceRequest

```
DeletePersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.DeletePersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.DiscreteValueSpec -->

# Class DiscreteValueSpec (1.134.0)

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. A list of possible values. The list should be in increasing order and at least 1e-10 apart. For instance, this parameter might have possible settings of 1.5, 2.5, and 4.0. This list should not contain more than 1,000 values. |
`default_value` |
`float`
A default value for a `DISCRETE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point. It automatically
rounds to the nearest feasible discrete point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DiscreteValueSpec

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudyTimeConstraint -->

# Class StudyTimeConstraint (1.134.0)

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

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
`max_duration` |
`google.protobuf.duration_pb2.Duration`
Counts the wallclock time passed since the creation of this Study. This field is a member of `oneof` _ `constraint` .
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Compares the wallclock time to this time. Must use UTC timezone. This field is a member of `oneof` _ `constraint` .
|

## Methods

### StudyTimeConstraint

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/definition_v1 -->

# Types for Google Cloud Aiplatform V1 Schema Trainingjob Definition v1 API

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs)

#### metadata()

The metadata information.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_classification.AutoMlImageClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_classification.AutoMlImageClassificationMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 8,000 and
800,000 milli node hours, inclusive. The default value is
192,000 which represents one day in wall time, considering 8
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

,
the training budget must be between 1,000 and 100,000 milli
node hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Classification might stop training before the entire training budget has been used.

**Type**

#### multi_label()

If false, a single-label (multi-class) Model will be trained (i.e. assuming that for each image just up to one annotation may be applicable). If true, a multi-label Model will be trained (i.e. assuming that for each image multiple annotations may be applicable).

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A Model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_TF_LOW_LATENCY_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have low latency, but
may have lower prediction quality than other
mobile models.
MOBILE_TF_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
with afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow or Core
ML model and used on a mobile or edge device
afterwards. Expected to have a higher latency,
but should also have a higher prediction quality
than other mobile models.
```


#### CLOUD(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationInputs.ModelType_ )

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageClassificationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetection(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Object Detection Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs)

#### metadata()

The metadata information

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_object_detection.AutoMlImageObjectDetectionInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_object_detection.AutoMlImageObjectDetectionMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. For modelType
`cloud`

(default), the budget must be between 20,000 and
900,000 milli node hours, inclusive. The default value is
216,000 which represents one day in wall time, considering 9
nodes are used. For model types `mobile-tf-low-latency-1`

,
`mobile-tf-versatile-1`

, `mobile-tf-high-accuracy-1`

the
training budget must be between 1,000 and 100,000 milli node
hours, inclusive. The default value is 24,000 which
represents one day in wall time on a single node that is
used.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. When false the early stopping feature is enabled, which means that AutoML Image Object Detection might stop training before the entire training budget has been used.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a higher latency, but should
also have a higher prediction quality than other
cloud models.
CLOUD_LOW_LATENCY_1 (2):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Expected to have a low latency, but may have
lower prediction quality than other cloud
models.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
MOBILE_TF_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
MOBILE_TF_HIGH_ACCURACY_1 (5):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) and used on a mobile
or edge device with TensorFlow afterwards.
Expected to have a higher latency, but should
also have a higher prediction quality than other
mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_LATENCY_1(* = * )

#### MOBILE_TF_HIGH_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MOBILE_TF_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageObjectDetectionMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Image Segmentation Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs)

#### metadata()

The metadata information.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_segmentation.AutoMlImageSegmentationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_image_segmentation.AutoMlImageSegmentationMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

#### budget_milli_node_hours()

The training budget of creating this model, expressed in
milli node hours i.e. 1,000 value in this field means 1 node
hour. The actual metadata.costMilliNodeHours will be equal
or less than this value. If further model training ceases to
provide any improvements, it will stop without using the
full budget and the metadata.successfulStopReason will be
`model-converged`

. Note, node_hour = actual_hour *
number_of_nodes_involved. Or actaul_wall_clock_hours =
train_budget_milli_node_hours / (number_of_nodes_involved *
1000) For modelType `cloud-high-accuracy-1`

(default),
the budget must be between 20,000 and 2,000,000 milli node
hours, inclusive. The default value is 192,000 which
represents one day in wall time (1000 milli * 24 hours * 8
nodes).

**Type**

#### base_model_id()

The ID of the `base`

model. If it is specified, the new
model will be trained based on the `base`

model.
Otherwise, the new model will be trained from scratch. The
`base`

model must be in the same Project and Location as
the new Model to train, and have the same modelType.

**Type**

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD_HIGH_ACCURACY_1 (1):
A model to be used via prediction calls to
uCAIP API. Expected to have a higher latency,
but should also have a higher prediction quality
than other models.
CLOUD_LOW_ACCURACY_1 (2):
A model to be used via prediction calls to
uCAIP API. Expected to have a lower latency but
relatively lower prediction quality.
MOBILE_TF_LOW_LATENCY_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as TensorFlow model
and used on a mobile or edge device afterwards.
Expected to have low latency, but may have lower
prediction quality than other mobile models.
```


#### CLOUD_HIGH_ACCURACY_1(* = * )

#### CLOUD_LOW_ACCURACY_1(* = * )

#### MOBILE_TF_LOW_LATENCY_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### base_model_id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### cost_milli_node_hours()

The actual training cost of creating this model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed inputs.budgetMilliNodeHours.

**Type**

#### successful_stop_reason()

For successful job completions, this is the reason why the job has finished.

*class* SuccessfulStopReason(value)

Bases: `proto.enums.Enum`


Values:

```
SUCCESSFUL_STOP_REASON_UNSPECIFIED (0):
Should not be set.
BUDGET_REACHED (1):
The inputs.budgetMilliNodeHours had been
reached.
MODEL_CONVERGED (2):
Further training of the Model ceased to
increase its quality, since it already has
converged.
```


#### BUDGET_REACHED(* = * )

#### MODEL_CONVERGED(* = * )

#### SUCCESSFUL_STOP_REASON_UNSPECIFIED(* = * )

#### cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### successful_stop_reason(*: [SuccessfulStopReason](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationMetadata.SuccessfulStopReason_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTables(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Tables Model.

#### inputs()

The input parameters of this TrainingJob.

#### metadata()

The metadata information.

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs_ )

#### metadata(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesMetadata](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### optimization_objective_recall_value()

Required when optimization_objective is “maximize-precision-at-recall”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### optimization_objective_precision_value()

Required when optimization_objective is “maximize-recall-at-precision”. Must be between 0 and 1, inclusive.

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `additional_optimization_objective_config`

.

**Type**

#### prediction_type()

The type of prediction the Model is to produce. “classification” - Predict one out of multiple target values is picked for each row.

“regression” - Predict a value based on its


relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings.

**Type**

#### target_column()

The column name of the target column that the model is to predict.

**Type**

#### transformations()

Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using “.” as the delimiter.

**Type**MutableSequence[

[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation)]

#### optimization_objective()

Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set.

The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used.

classification (binary):

“maximize-au-roc” (default) - Maximize the


area under the receiver operating characteristic (ROC) curve. “minimize-log-loss” - Minimize log loss.

“maximize-au-prc” - Maximize the area under


the precision-recall curve. “maximize-precision-at-recall” - Maximize precision for a specified recall value. “maximize-recall-at-precision” - Maximize recall for a specified precision value.

classification (multi-class):

“minimize-log-loss” (default) - Minimize log


loss.

regression:

“minimize-rmse” (default) - Minimize


root-mean-squared error (RMSE). “minimize-mae”

Minimize mean-absolute error (MAE). “minimize-rmsle” - Minimize root-mean-squared log error (RMSLE).

**Type**

#### train_budget_milli_node_hours()

Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour.

The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend’s discretion. This especially may happen when further model training ceases to provide any improvements.

If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won’t be attempted and will error.

The train budget must be between 1,000 and 72,000 milli node hours, inclusive.

**Type**

#### disable_early_stopping()

Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used.

**Type**

#### weight_column_name()

Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1.

**Type**

#### export_evaluated_data_items_config()

Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig)

#### additional_experiments()

Additional experiment flags for the Tables training pipeline.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

*class* Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


This message has [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

#### auto()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### timestamp()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_numeric()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_categorical()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

#### repeated_text()

This field is a member of [oneof](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields) `transformation_detail`

.

*class* AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will infer the proper transformation based on the statistic of dataset.

#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as categorical array and performs following transformation functions.

For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Empty arrays treated as an embedding of zeroes.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* CategoricalTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The categorical string as is–no change to case, punctuation, spelling, tense, and so on.

Convert the category name to a dictionary lookup index and generate an embedding for each index.

Categories that appear less than 5 times in the training dataset are treated as the “unknown” category. The “unknown” category gets its own special lookup index and resulting embedding.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* NumericArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as numerical array and performs following transformation functions.

All transformations for Numerical types applied to the average of the all elements.

The average of empty arrays is treated as zero.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* NumericTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The value converted to float32.

The z_score of the value.

log(value+1) when the value is greater than or equal to 0. Otherwise, this transformation is not applied and the value is considered a missing value.

z_score of log(value+1) when the value is greater than or equal to

Otherwise, this transformation is not applied and the value is considered a missing value.

A boolean value that indicates whether the value is valid.


#### column_name()

**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Treats the column as text array and performs following transformation functions.

Concatenate all text values in the array into a single text value using a space (” “) as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.

Empty arrays treated as an empty text.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TextTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

The text as is–no change to case, punctuation, spelling, tense, and so on.

Tokenize text to words. Convert each words to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.

Tokenization is based on unicode script boundaries.

Missing values get their own lookup index and resulting embedding.

Stop-words receive no special treatment and are not removed.


#### column_name()

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* TimestampTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Training pipeline will perform following transformation functions.

Apply the transformation functions for Numerical columns.

Determine the year, month, day,and weekday. Treat each value from the

timestamp as a Categorical column.

Invalid numerical values (for example, values that fall outside of a typical timestamp range, or are extreme values) receive no special treatment and are not removed.


#### column_name()

**Type**

#### time_format()

The format in which that time field is expressed. The time_format must either be one of:

`unix-seconds`

`unix-milliseconds`

`unix-microseconds`

`unix-nanoseconds`

(for respectively number of seconds, milliseconds, microseconds and nanoseconds since start of the Unix epoch); or be written in`strftime`

syntax. If time_format is not set, then the default format is RFC 3339`date-time`

format, where`time-offset`

=`"Z"`

(e.g. 1985-04-12T23:20:50.52Z)**Type**

#### invalid_values_allowed()

If invalid values is allowed, the training pipeline will create a boolean feature that indicated whether the value is valid. Otherwise, the training pipeline will discard the input row from trainining data.

**Type**

#### column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### invalid_values_allowed(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### time_format(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### auto(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.AutoTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.AutoTransformation_ )

#### categorical(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalTransformation_ )

#### numeric(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericTransformation_ )

#### repeated_categorical(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation_ )

#### repeated_numeric(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.NumericArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.NumericArrayTransformation_ )

#### repeated_text(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TextArrayTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation_ )

#### text(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TextTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextTransformation_ )

#### timestamp(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_tables.AutoMlTablesInputs.Transformation.TimestampTransformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TimestampTransformation_ )

#### additional_experiments(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### disable_early_stopping(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

#### export_evaluated_data_items_config(*: gcastd_export_evaluated_data_items_config.ExportEvaluatedDataItemsConfi* )

#### optimization_objective(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### optimization_objective_precision_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### optimization_objective_recall_value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### prediction_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### target_column(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### train_budget_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

#### transformations(*: MutableSequence[[Transformation](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation)_ )

#### weight_column_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Model metadata specific to AutoML Tables.

#### train_cost_milli_node_hours()

Output only. The actual training cost of the model, expressed in milli node hours, i.e. 1,000 value in this field means 1 node hour. Guaranteed to not exceed the train budget.

**Type**

#### train_cost_milli_node_hours(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_classification.AutoMlTextClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### multi_label()

**Type**

#### multi_label(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtraction(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Extraction Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs


#### inputs(*: google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_extraction.AutoMlTextExtractionInput* )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

#### inputs()

The input parameters of this TrainingJob.

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_text_sentiment.AutoMlTextSentimentInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentimentInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### sentiment_max()

A sentiment is expressed as an integer ordinal, where higher value means a more positive sentiment. The range of sentiments that will be used is between 0 and sentimentMax (inclusive on both ends), and all the values in the range must be represented in the dataset before a model can be created. Only the Annotations with this sentimentMax will be used for training. sentimentMax value must be between 1 and 10 (inclusive).

**Type**

#### sentiment_max(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognition(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Action Recognition Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_action_recognition.AutoMlVideoActionRecognitionInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
MOBILE_CORAL_VERSATILE_1 (4):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a Coral device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoActionRecognitionInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassification(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video Classification Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_classification.AutoMlVideoClassificationInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which cannot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_JETSON_VERSATILE_1 (3):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) to a Jetson device
afterwards.
```


#### CLOUD(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTracking(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


A TrainingJob that trains and uploads an AutoML Video ObjectTracking Model.

#### inputs()

The input parameters of this TrainingJob.

**Type**[google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/definition_v1/types_.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs)

#### inputs(*: [google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.automl_video_object_tracking.AutoMlVideoObjectTrackingInputs](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


#### model_type()

*class* ModelType(value)

Bases: `proto.enums.Enum`


Values:

```
MODEL_TYPE_UNSPECIFIED (0):
Should not be set.
CLOUD (1):
A model best tailored to be used within
Google Cloud, and which c annot be exported.
Default.
MOBILE_VERSATILE_1 (2):
A model that, in addition to being available
within Google Cloud, can also be exported (see
ModelService.ExportModel) as a TensorFlow or
TensorFlow Lite model and used on a mobile or
edge device afterwards.
MOBILE_CORAL_VERSATILE_1 (3):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on a Google Coral device.
MOBILE_CORAL_LOW_LATENCY_1 (4):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on a Google
Coral device.
MOBILE_JETSON_VERSATILE_1 (5):
A versatile model that is meant to be
exported (see ModelService.ExportModel) and used
on an NVIDIA Jetson device.
MOBILE_JETSON_LOW_LATENCY_1 (6):
A model that trades off quality for low
latency, to be exported (see
ModelService.ExportModel) and used on an NVIDIA
Jetson device.
```


#### CLOUD(* = * )

#### MOBILE_CORAL_LOW_LATENCY_1(* = * )

#### MOBILE_CORAL_VERSATILE_1(* = * )

#### MOBILE_JETSON_LOW_LATENCY_1(* = * )

#### MOBILE_JETSON_VERSATILE_1(* = * )

#### MOBILE_VERSATILE_1(* = * )

#### MODEL_TYPE_UNSPECIFIED(* = * )

#### model_type(*: [ModelType](../definition_v1/types*.md#google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs.ModelType_ )

*class* google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.ExportEvaluatedDataItemsConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Configuration for exporting test set predictions to a BigQuery table.

#### destination_bigquery_uri()

URI of desired destination BigQuery table. Expected format: bq://<project_id>:<dataset_id>:

If not specified, then results are exported to the following auto-created BigQuery table: <project_id>:export_evaluated_examples_<model_name>_<yyyy_MM_dd’T’HH_mm_ss_SSS’Z’>.evaluated_examples

**Type**

#### override_existing_table()

If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails.

**Type**

#### destination_bigquery_uri(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### override_existing_table(*: [bool](*[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool) )

[https://docs.python.org/3/library/functions.html#bool](https://docs.python.org/3/library/functions.html#bool)

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
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoObjectTrackingInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_CORAL_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_CORAL_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_JETSON_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

MOBILE_JETSON_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateCachedContentRequest -->

# Class UpdateCachedContentRequest (1.134.0)

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

## Attributes |
|
|---|---|
Name |
Description |
`cached_content` |
Required. The cached content to update |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateCachedContentRequest

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse.PromptFeedback -->

# Class PromptFeedback (1.134.0)

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

## Attributes |
|
|---|---|
Name |
Description |
`block_reason` |
Output only. Blocked reason. |
`safety_ratings` |
`MutableSequence[`
Output only. Safety ratings. |
`block_reason_message` |
`str`
Output only. A readable block reason message. |

## Classes

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

## Methods

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployRequest.ModelConfig -->

# Class ModelConfig (1.134.0)

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

## Attributes |
|
|---|---|
Name |
Description |
`accept_eula` |
`bool`
Optional. Whether the user accepts the End User License Agreement (EULA) for the model. |
`hugging_face_access_token` |
`str`
Optional. The Hugging Face read access token used to access the model artifacts of gated models. |
`hugging_face_cache_enabled` |
`bool`
Optional. If true, the model will deploy with a cached version instead of directly downloading the model artifacts from Hugging Face. This is suitable for VPC-SC users with limited internet access. |
`model_display_name` |
`str`
Optional. The user-specified display name of the uploaded model. If not set, a default name will be used. |
`container_spec` |
Optional. The specification of the container that is to be used when deploying. If not set, the default container spec will be used. |
`model_user_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. When not provided, Vertex AI will generate a value for this ID. When Model Registry model is provided, this field will be ignored. This value may be up to 63 characters, and valid characters are `[a-z0-9_-]` . The first character cannot be a number
or hyphen.
|

## Methods

### ModelConfig

`ModelConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model config to use for the deployment.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenRequest -->

# Class GenerateFetchAccessTokenRequest (1.134.0)

```
GenerateFetchAccessTokenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

## Attribute |
|
|---|---|
Name |
Description |
`feature_view` |
`str`
FeatureView resource format `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`
|

## Methods

### GenerateFetchAccessTokenRequest

```
GenerateFetchAccessTokenRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateFetchAccessTokenResponse -->

# Class GenerateFetchAccessTokenResponse (1.134.0)

```
GenerateFetchAccessTokenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

## Attributes |
|
|---|---|
Name |
Description |
`access_token` |
`str`
The OAuth 2.0 access token. |
`expire_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Token expiration time. This is always set |

## Methods

### GenerateFetchAccessTokenResponse

```
GenerateFetchAccessTokenResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for [FeatureOnlineStoreService.GenerateFetchAccessToken][].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView -->

# Class FeatureView (1.134.0)

`FeatureView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

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
`big_query_source` |
Optional. Configures how data is supposed to be extracted from a BigQuery source to be loaded onto the FeatureOnlineStore. This field is a member of `oneof` _ `source` .
|
`feature_registry_source` |
Optional. Configures the features from a Feature Registry source that need to be loaded onto the FeatureOnlineStore. This field is a member of `oneof` _ `source` .
|
`vertex_rag_source` |
Optional. The Vertex RAG Source that the FeatureView is linked to. This field is a member of `oneof` _ `source` .
|
`name` |
`str`
Identifier. Name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureView was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureView was last updated. |
`etag` |
`str`
Optional. Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureViews. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureOnlineStore(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`sync_config` |
Configures when data is to be synced/updated for this FeatureView. At the end of the sync the latest featureValues for each entityId of this FeatureView are made ready for online serving. |
`index_config` |
Optional. Configuration for index preparation for vector search. It contains the required configurations to create an index from source data, so that approximate nearest neighbor (a.k.a ANN) algorithms search can be performed during online serving. |
`optimized_config` |
Optional. Configuration for FeatureView created under Optimized FeatureOnlineStore. |
`service_agent_type` |
Optional. Service agent type used during data sync. By default, the Vertex AI Service Agent is used. When using an IAM Policy to isolate this FeatureView within a project, a separate service account should be provisioned by setting this field to `SERVICE_AGENT_TYPE_FEATURE_VIEW` . This will
generate a separate service account to access the BigQuery
source table.
|
`service_account_email` |
`str`
Output only. A Service Account unique to this FeatureView. The role bigquery.dataViewer should be granted to this service account to allow Vertex AI Feature Store to sync data to the online store. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |
`bigtable_metadata` |
Metadata containing information about the Cloud Bigtable. |

## Classes

### BigQuerySource

`BigQuerySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


### BigtableMetadata

`BigtableMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata for the Cloud Bigtable that supports directly interacting Bigtable instances.

### FeatureRegistrySource

`FeatureRegistrySource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Feature Registry source for features that need to be synced to Online Store.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### IndexConfig

`IndexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for vector indexing.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

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

### OptimizedConfig

`OptimizedConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for FeatureViews created in Optimized FeatureOnlineStore.

### ServiceAgentType

`ServiceAgentType(value)`


Service agent type used during data sync.

### SyncConfig

`SyncConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for Sync. Only one option is set.

### VertexRagSource

`VertexRagSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Vertex Rag source for features that need to be synced to Online Store.

## Methods

### FeatureView

`FeatureView(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


FeatureView is representation of values that the FeatureOnlineStore will serve based on its syncConfig.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata -->

# Class InputMetadata (1.134.0)

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

## Attributes |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. If no baseline is specified, Vertex AI chooses the baseline for this feature. If multiple baselines are specified, Vertex AI returns the average attributions across them in Attribution.feature_attributions. For Vertex AI-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the instance[]. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1.Model.predict_schemata] instance_schema_uri. |
`input_tensor_name` |
`str`
Name of the input tensor for this feature. Required and is only applicable to Vertex AI-provided images for Tensorflow. |
`encoding` |
Defines how the feature is encoded into the input tensor. Defaults to IDENTITY. |
`modality` |
`str`
Modality of the feature. Valid values are: numeric, image. Defaults to numeric. |
`feature_value_domain` |
The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized. |
`indices_tensor_name` |
`str`
Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`dense_shape_tensor_name` |
`str`
Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`index_feature_mapping` |
`MutableSequence[str]`
A list of feature names for each index in the input tensor. Required when the input InputMetadata.encoding is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR. |
`encoded_tensor_name` |
`str`
Encoded tensor is a transformation of the input tensor. Must be provided if choosing [Integrated Gradients attribution][google.cloud.aiplatform.v1.ExplanationParameters.integrated_gradients_attribution] or [XRAI attribution][google.cloud.aiplatform.v1.ExplanationParameters.xrai_attribution] and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table. |
`encoded_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Vertex AI broadcasts to the same shape as the encoded tensor. |
`visualization` |
Visualization configurations for image explanation. |
`group_name` |
`str`
Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in Attribution.feature_attributions, keyed by the group name. |

## Classes

### Encoding

`Encoding(value)`


Defines how a feature is encoded. Defaults to IDENTITY.

```
::
input = [27, 6.0, 150]
index_feature_mapping = ["age", "height", "weight"]
BAG_OF_FEATURES_SPARSE (3):
The tensor represents a bag of features where each index
maps to a feature. Zero values in the tensor indicates
feature being non-existent.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [2, 0, 5, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
INDICATOR (4):
The tensor is a list of binaries representing whether a
feature exists or not (1 indicates existence).
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [1, 0, 1, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
COMBINED_EMBEDDING (5):
The tensor is encoded into a 1-dimensional array represented
by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]
CONCAT_EMBEDDING (6):
Select this encoding when the input tensor is encoded into a
2-dimensional array represented by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. The first dimension of
the encoded tensor's shape is the same as the input tensor's
shape. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
[0.2, 0.1, 0.4, 0.3, 0.5],
[0.5, 0.1, 0.3, 0.5, 0.4],
[0.5, 0.3, 0.1, 0.2, 0.4],
[0.4, 0.3, 0.2, 0.5, 0.1]]
```


### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Methods

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.endpoint_service.pagers`

module.

## Classes

[ListEndpointsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsAsyncPager)

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEndpointsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsPager)

```
ListEndpointsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse
],
request: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1.types.endpoint_service.ListEndpointsResponse,
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


A pager for iterating through `list_endpoints`

requests.

This class thinly wraps an initial
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEndpoints`

requests and continue to iterate
through the `endpoints`

field on the
corresponding responses.

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.134.0)

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateModelDeploymentMonitoringJobOperationMetadata

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.134.0)

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### PairwiseQuestionAnsweringQualitySpec

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetNotebookRuntimeTemplateRequest -->

# Class GetNotebookRuntimeTemplateRequest (1.134.0)

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntimeTemplate resource. Format: `projects/{project}/locations/{location}/notebookRuntimeTemplates/{notebook_runtime_template}`
|

## Methods

### GetNotebookRuntimeTemplateRequest

```
GetNotebookRuntimeTemplateRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for NotebookService.GetNotebookRuntimeTemplate

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListOptimalTrialsResponse -->

# Class ListOptimalTrialsResponse (1.134.0)

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

## Attribute |
|
|---|---|
Name |
Description |
`optimal_trials` |
`MutableSequence[`
The pareto-optimal Trials for multiple objective Study or the optimal trial for single objective Study. The definition of pareto-optimal can be checked in wiki page. https://en.wikipedia.org/wiki/Pareto_efficiency |

## Methods

### ListOptimalTrialsResponse

`ListOptimalTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListOptimalTrials.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.schedule_service.pagers`

module.

## Classes

[ListSchedulesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesAsyncPager)

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse) object, and
provides an `__aiter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListSchedulesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesPager)

```
ListSchedulesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse
],
request: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1.types.schedule_service.ListSchedulesResponse,
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


A pager for iterating through `list_schedules`

requests.

This class thinly wraps an initial
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse) object, and
provides an `__iter__`

method to iterate through its
`schedules`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSchedules`

requests and continue to iterate
through the `schedules`

field on the
corresponding responses.

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AuthConfig -->

# Class AuthConfig (1.134.0)

`AuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Auth configuration to run the extension.

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
`api_key_config` |
Config for API key auth. This field is a member of `oneof` _ `auth_config` .
|
`http_basic_auth_config` |
Config for HTTP Basic auth. This field is a member of `oneof` _ `auth_config` .
|
`google_service_account_config` |
Config for Google Service Account auth. This field is a member of `oneof` _ `auth_config` .
|
`oauth_config` |
Config for user oauth. This field is a member of `oneof` _ `auth_config` .
|
`oidc_config` |
Config for user OIDC auth. This field is a member of `oneof` _ `auth_config` .
|
`auth_type` |
Type of auth scheme. |

## Classes

### ApiKeyConfig

`ApiKeyConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for authentication with API key.

### GoogleServiceAccountConfig

`GoogleServiceAccountConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for Google Service Account Authentication.

### HttpBasicAuthConfig

`HttpBasicAuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for HTTP Basic Authentication.

### OauthConfig

`OauthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user oauth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### OidcConfig

`OidcConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for user OIDC auth.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AuthConfig

`AuthConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Auth configuration to run the extension.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudyTimeConstraint -->

# Class StudyTimeConstraint (1.134.0)

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

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
`max_duration` |
`google.protobuf.duration_pb2.Duration`
Counts the wallclock time passed since the creation of this Study. This field is a member of `oneof` _ `constraint` .
|
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Compares the wallclock time to this time. Must use UTC timezone. This field is a member of `oneof` _ `constraint` .
|

## Methods

### StudyTimeConstraint

`StudyTimeConstraint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time-based Constraint for Study

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.DiscreteValueSpec -->

# Class DiscreteValueSpec (1.134.0)

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[float]`
Required. A list of possible values. The list should be in increasing order and at least 1e-10 apart. For instance, this parameter might have possible settings of 1.5, 2.5, and 4.0. This list should not contain more than 1,000 values. |
`default_value` |
`float`
A default value for a `DISCRETE` parameter that is assumed
to be a relatively good starting point. Unset value signals
that there is no offered starting point. It automatically
rounds to the nearest feasible discrete point.
Currently only supported by the Vertex AI Vizier service.
Not supported by HyperparameterTuningJob or
TrainingPipeline.
This field is a member of `oneof` _ `_default_value` .
|

## Methods

### DiscreteValueSpec

`DiscreteValueSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Value specification for a parameter in `DISCRETE`

type.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.134.0)

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboards` |
`MutableSequence[`
The Tensorboards mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardsResponse

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureView.VectorSearchConfig.TreeAHConfig -->

# Class TreeAHConfig (1.134.0)

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`leaf_node_embedding_count` |
`int`
Optional. Number of embeddings on each leaf node. The default value is 1000 if not set. This field is a member of `oneof` _ `_leaf_node_embedding_count` .
|

## Methods

### TreeAHConfig

`TreeAHConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelMonitorRequest -->

# Class DeleteModelMonitorRequest (1.134.0)

`DeleteModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.DeleteModelMonitor.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the ModelMonitor resource to be deleted. Format: `projects/{project}/locations/{location}/modelMonitords/{model_monitor}`
|
`force` |
`bool`
Optional. Force delete the model monitor with schedules. |

## Methods

### DeleteModelMonitorRequest

`DeleteModelMonitorRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelMonitoringService.DeleteModelMonitor.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardBlob -->

# Class TensorboardBlob (1.134.0)

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project. |
`data` |
`bytes`
Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint. |

## Methods

### TensorboardBlob

`TensorboardBlob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


One blob (e.g, image, graph) viewable on a blob metric plot.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewSyncRequest -->

# Class GetFeatureViewSyncRequest (1.134.0)

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### GetFeatureViewSyncRequest

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExample -->

# Class StoredContentsExample (1.134.0)

`StoredContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

## Attributes |
|
|---|---|
Name |
Description |
`search_key` |
`str`
Optional. (Optional) the search key used for retrieval. If not provided at upload-time, the search key will be generated from `contents_example.contents` using the
method provided by `search_key_generation_method` . The
generated search key will be included in retrieved examples.
|
`contents_example` |
Required. The example to be used with GenerateContent. |
`search_key_generation_method` |
Optional. The method used to generate the search key from `contents_example.contents` . This is ignored when
uploading an example if `search_key` is provided.
|

## Classes

### SearchKeyGenerationMethod

`SearchKeyGenerationMethod(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Options for generating the search key from the conversation history.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### StoredContentsExample

`StoredContentsExample(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A ContentsExample to be used with GenerateContent alongside information required for storage and retrieval with Example Store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager -->

# Class SearchModelDeploymentMonitoringStatsAnomaliesPager (1.134.0)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelDeploymentMonitoringStatsAnomaliesPager

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlVideoObjectTrackingInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which c annot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_CORAL_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_CORAL_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on a Google Coral device.

MOBILE_JETSON_VERSATILE_1

A versatile model that is meant to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

MOBILE_JETSON_LOW_LATENCY_1

A model that trades off quality for low latency, to be exported (see ModelService.ExportModel) and used on an NVIDIA Jetson device.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextChildrenRequest -->

# Class AddContextChildrenRequest (1.134.0)

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### AddContextChildrenRequest

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.134.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingInput -->

# Class RubricBasedInstructionFollowingInput (1.134.0)

```
RubricBasedInstructionFollowingInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instance and metric spec for RubricBasedInstructionFollowing metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for RubricBasedInstructionFollowing metric. |
`instance` |
Required. Instance for RubricBasedInstructionFollowing metric. |

## Methods

### RubricBasedInstructionFollowingInput

```
RubricBasedInstructionFollowingInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Instance and metric spec for RubricBasedInstructionFollowing metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentResponse.PromptFeedback -->

# Class PromptFeedback (1.134.0)

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

## Attributes |
|
|---|---|
Name |
Description |
`block_reason` |
Output only. Blocked reason. |
`safety_ratings` |
`MutableSequence[`
Output only. Safety ratings. |
`block_reason_message` |
`str`
Output only. A readable block reason message. |

## Classes

### BlockedReason

`BlockedReason(value)`


Blocked reason enumeration.

## Methods

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateCachedContentRequest -->

# Class UpdateCachedContentRequest (1.134.0)

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

## Attributes |
|
|---|---|
Name |
Description |
`cached_content` |
Required. The cached content to update |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The list of fields to update. |

## Methods

### UpdateCachedContentRequest

`UpdateCachedContentRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiCacheService.UpdateCachedContent. Only expire_time or ttl can be updated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DiskSpec -->

# Class DiskSpec (1.134.0)

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.

## Attributes |
|
|---|---|
Name |
Description |
`boot_disk_type` |
`str`
Type of the boot disk. For non-A3U machines, the default value is "pd-ssd", for A3U machines, the default value is "hyperdisk-balanced". Valid values: "pd-ssd" (Persistent Disk Solid State Drive), "pd-standard" (Persistent Disk Hard Disk Drive) or "hyperdisk-balanced". |
`boot_disk_size_gb` |
`int`
Size in GB of the boot disk (default is 100GB). |

## Methods

### DiskSpec

`DiskSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of disk options.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.job_service.pagers`

module.

## Classes

[ListBatchPredictionJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListBatchPredictionJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListBatchPredictionJobsPager)

```
ListBatchPredictionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListBatchPredictionJobsResponse,
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


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListCustomJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsAsyncPager)

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListCustomJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListCustomJobsPager)

```
ListCustomJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListCustomJobsResponse,
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


A pager for iterating through `list_custom_jobs`

requests.

This class thinly wraps an initial
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`custom_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCustomJobs`

requests and continue to iterate
through the `custom_jobs`

field on the
corresponding responses.

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsAsyncPager)

```
ListDataLabelingJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse,
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


A pager for iterating through `list_data_labeling_jobs`

requests.

This class thinly wraps an initial
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_labeling_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataLabelingJobs`

requests and continue to iterate
through the `data_labeling_jobs`

field on the
corresponding responses.

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListDataLabelingJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsPager)

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListDataLabelingJobsResponse,
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


A pager for iterating through `list_data_labeling_jobs`

requests.

This class thinly wraps an initial
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_labeling_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDataLabelingJobs`

requests and continue to iterate
through the `data_labeling_jobs`

field on the
corresponding responses.

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager)

```
ListHyperparameterTuningJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListHyperparameterTuningJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsPager)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListHyperparameterTuningJobsResponse,
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


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsAsyncPager)

```
ListModelDeploymentMonitoringJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListModelDeploymentMonitoringJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListModelDeploymentMonitoringJobsPager)

```
ListModelDeploymentMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListModelDeploymentMonitoringJobsResponse,
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


A pager for iterating through `list_model_deployment_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_deployment_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelDeploymentMonitoringJobs`

requests and continue to iterate
through the `model_deployment_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelDeploymentMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsAsyncPager)

```
ListNasJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasJobsPager)

```
ListNasJobsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasJobsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasJobsResponse,
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


A pager for iterating through `list_nas_jobs`

requests.

This class thinly wraps an initial
[ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasJobs`

requests and continue to iterate
through the `nas_jobs`

field on the
corresponding responses.

All the usual [ListNasJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsAsyncPager)

```
ListNasTrialDetailsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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


A pager for iterating through `list_nas_trial_details`

requests.

This class thinly wraps an initial
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse) object, and
provides an `__aiter__`

method to iterate through its
`nas_trial_details`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNasTrialDetails`

requests and continue to iterate
through the `nas_trial_details`

field on the
corresponding responses.

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListNasTrialDetailsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListNasTrialDetailsPager)

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse
],
request: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1.types.job_service.ListNasTrialDetailsResponse,
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


A pager for iterating through `list_nas_trial_details`

requests.

This class thinly wraps an initial
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse) object, and
provides an `__iter__`

method to iterate through its
`nas_trial_details`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNasTrialDetails`

requests and continue to iterate
through the `nas_trial_details`

field on the
corresponding responses.

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse
],
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__aiter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchModelDeploymentMonitoringStatsAnomaliesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.SearchModelDeploymentMonitoringStatsAnomaliesPager)

```
SearchModelDeploymentMonitoringStatsAnomaliesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
],
request: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesRequest,
response: google.cloud.aiplatform_v1.types.job_service.SearchModelDeploymentMonitoringStatsAnomaliesResponse,
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


A pager for iterating through `search_model_deployment_monitoring_stats_anomalies`

requests.

This class thinly wraps an initial
[SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelDeploymentMonitoringStatsAnomalies`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelDeploymentMonitoringStatsAnomaliesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchModelDeploymentMonitoringStatsAnomaliesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.pipeline_service.pagers`

module.

## Classes

[ListPipelineJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsAsyncPager)

```
ListPipelineJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListPipelineJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListPipelineJobsPager)

```
ListPipelineJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListPipelineJobsResponse,
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


A pager for iterating through `list_pipeline_jobs`

requests.

This class thinly wraps an initial
[ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`pipeline_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPipelineJobs`

requests and continue to iterate
through the `pipeline_jobs`

field on the
corresponding responses.

All the usual [ListPipelineJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse) object, and
provides an `__aiter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrainingPipelinesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.pipeline_service.pagers.ListTrainingPipelinesPager)

```
ListTrainingPipelinesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
],
request: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1.types.pipeline_service.ListTrainingPipelinesResponse,
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


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse) object, and
provides an `__iter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureMonitorJobRequest -->

# Class GetFeatureMonitorJobRequest (1.134.0)

`GetFeatureMonitorJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitorJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureMonitorJob resource. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}/featureMonitorJobs/{feature_monitor_job}`
|

## Methods

### GetFeatureMonitorJobRequest

`GetFeatureMonitorJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureRegistryService.GetFeatureMonitorJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateModelDeploymentMonitoringJobOperationMetadata -->

# Class UpdateModelDeploymentMonitoringJobOperationMetadata (1.134.0)

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateModelDeploymentMonitoringJobOperationMetadata

```
UpdateModelDeploymentMonitoringJobOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for JobService.UpdateModelDeploymentMonitoringJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.134.0)

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

## Attribute |
|
|---|---|
Name |
Description |
`enable_secure_boot` |
`bool`
Defines whether the instance has `Secure Boot |

## Methods

### ShieldedVmConfig

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StopNotebookRuntimeRequest -->

# Class StopNotebookRuntimeRequest (1.134.0)

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StopNotebookRuntimeRequest

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelMonitoringObjectiveConfig.ExplanationConfig -->

# Class ExplanationConfig (1.134.0)

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

## Attributes |
|
|---|---|
Name |
Description |
`enable_feature_attributes` |
`bool`
If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Vertex AI will log the feature attributions from explain response and do the skew/drift detection for them. |
`explanation_baseline` |
Predictions generated by the BatchPredictionJob using baseline dataset. |

## Classes

### ExplanationBaseline

`ExplanationBaseline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output from BatchPredictionJob for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateTrainingPipelineRequest -->

# Class CreateTrainingPipelineRequest (1.134.0)

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: `projects/{project}/locations/{location}`
|
`training_pipeline` |
Required. The TrainingPipeline to create. |

## Methods

### CreateTrainingPipelineRequest

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PostStartupScriptConfig.PostStartupScriptBehavior -->

# Class PostStartupScriptBehavior (1.134.0)

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

## Enums |
|
|---|---|
Name |
Description |
`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` |
Unspecified post startup script behavior. |
`RUN_ONCE` |
Run post startup script after runtime is started. |
`RUN_EVERY_START` |
Run post startup script after runtime is stopped. |
`DOWNLOAD_AND_RUN_EVERY_START` |
Download and run post startup script every time runtime is started. |

## Methods

### PostStartupScriptBehavior

`PostStartupScriptBehavior(value)`


Represents a notebook runtime post startup script behavior.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportPublisherModelResponse -->

# Class ExportPublisherModelResponse (1.134.0)

```
ExportPublisherModelResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelGardenService.ExportPublisherModel.

## Attributes |
|
|---|---|
Name |
Description |
`publisher_model` |
`str`
The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisher_model}@{version_id}`
|
`destination_uri` |
`str`
The destination uri of the model weights. |

## Methods

### ExportPublisherModelResponse

```
ExportPublisherModelResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelGardenService.ExportPublisherModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateReasoningEngineRequest -->

# Class UpdateReasoningEngineRequest (1.134.0)

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. |

## Methods

### UpdateReasoningEngineRequest

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagRetrievalConfig.Filter -->

# Class Filter (1.134.0)

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
`vector_distance_threshold` |
`float`
Optional. Only returns contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`vector_similarity_threshold` |
`float`
Optional. Only returns contexts with vector similarity larger than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`metadata_filter` |
`str`
Optional. String for metadata filtering. |

## Methods

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelDeploymentMonitoringJobsRequest -->

# Class ListModelDeploymentMonitoringJobsRequest (1.134.0)

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
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
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read |

## Methods

### ListModelDeploymentMonitoringJobsRequest

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualitySpec -->

# Class PairwiseQuestionAnsweringQualitySpec (1.134.0)

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute question answering quality. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### PairwiseQuestionAnsweringQualitySpec

```
PairwiseQuestionAnsweringQualitySpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse -->

# Class ListTensorboardsResponse (1.134.0)

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

## Attributes |
|
|---|---|
Name |
Description |
`tensorboards` |
`MutableSequence[`
The Tensorboards mathching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListTensorboardsRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListTensorboardsResponse

`ListTensorboardsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for TensorboardService.ListTensorboards.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.example_store_service.pagers`

module.

## Classes

[FetchExamplesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager)

```
FetchExamplesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


A pager for iterating through `fetch_examples`

requests.

This class thinly wraps an initial
[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse) object, and
provides an `__aiter__`

method to iterate through its
`examples`

field.

If there are more pages, the `__aiter__`

method will make additional
`FetchExamples`

requests and continue to iterate
through the `examples`

field on the
corresponding responses.

All the usual [FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[FetchExamplesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesPager)

```
FetchExamplesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesResponse,
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


A pager for iterating through `fetch_examples`

requests.

This class thinly wraps an initial
[FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse) object, and
provides an `__iter__`

method to iterate through its
`examples`

field.

If there are more pages, the `__iter__`

method will make additional
`FetchExamples`

requests and continue to iterate
through the `examples`

field on the
corresponding responses.

All the usual [FetchExamplesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExampleStoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresAsyncPager)

```
ListExampleStoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
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


A pager for iterating through `list_example_stores`

requests.

This class thinly wraps an initial
[ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`example_stores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListExampleStores`

requests and continue to iterate
through the `example_stores`

field on the
corresponding responses.

All the usual [ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListExampleStoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresPager)

```
ListExampleStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
response: google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresResponse,
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


A pager for iterating through `list_example_stores`

requests.

This class thinly wraps an initial
[ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`example_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExampleStores`

requests and continue to iterate
through the `example_stores`

field on the
corresponding responses.

All the usual [ListExampleStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplanationMetadata.InputMetadata -->

# Class InputMetadata (1.134.0)

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

## Attributes |
|
|---|---|
Name |
Description |
`input_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Baseline inputs for this feature. If no baseline is specified, Vertex AI chooses the baseline for this feature. If multiple baselines are specified, Vertex AI returns the average attributions across them in Attribution.feature_attributions. For Vertex AI-provided Tensorflow images (both 1.x and 2.x), the shape of each baseline must match the shape of the input tensor. If a scalar is provided, we broadcast to the same shape as the input tensor. For custom images, the element of the baselines must be in the same format as the feature's input in the instance[]. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`input_tensor_name` |
`str`
Name of the input tensor for this feature. Required and is only applicable to Vertex AI-provided images for Tensorflow. |
`encoding` |
Defines how the feature is encoded into the input tensor. Defaults to IDENTITY. |
`modality` |
`str`
Modality of the feature. Valid values are: numeric, image. Defaults to numeric. |
`feature_value_domain` |
The domain details of the input feature value. Like min/max, original mean or standard deviation if normalized. |
`indices_tensor_name` |
`str`
Specifies the index of the values of the input tensor. Required when the input tensor is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`dense_shape_tensor_name` |
`str`
Specifies the shape of the values of the input if the input is a sparse representation. Refer to Tensorflow documentation for more details: https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor. |
`index_feature_mapping` |
`MutableSequence[str]`
A list of feature names for each index in the input tensor. Required when the input InputMetadata.encoding is BAG_OF_FEATURES, BAG_OF_FEATURES_SPARSE, INDICATOR. |
`encoded_tensor_name` |
`str`
Encoded tensor is a transformation of the input tensor. Must be provided if choosing [Integrated Gradients attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.integrated_gradients_attribution] or [XRAI attribution][google.cloud.aiplatform.v1beta1.ExplanationParameters.xrai_attribution] and the input tensor is not differentiable. An encoded tensor is generated if the input tensor is encoded by a lookup table. |
`encoded_baselines` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
A list of baselines for the encoded tensor. The shape of each baseline should match the shape of the encoded tensor. If a scalar is provided, Vertex AI broadcasts to the same shape as the encoded tensor. |
`visualization` |
Visualization configurations for image explanation. |
`group_name` |
`str`
Name of the group that the input belongs to. Features with the same group name will be treated as one feature when computing attributions. Features grouped together can have different shapes in value. If provided, there will be one single attribution generated in Attribution.feature_attributions, keyed by the group name. |

## Classes

### Encoding

`Encoding(value)`


Defines how a feature is encoded. Defaults to IDENTITY.

```
::
input = [27, 6.0, 150]
index_feature_mapping = ["age", "height", "weight"]
BAG_OF_FEATURES_SPARSE (3):
The tensor represents a bag of features where each index
maps to a feature. Zero values in the tensor indicates
feature being non-existent.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [2, 0, 5, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
INDICATOR (4):
The tensor is a list of binaries representing whether a
feature exists or not (1 indicates existence).
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.index_feature_mapping">InputMetadata.index_feature_mapping</xref>
must be provided for this encoding. For example:
::
input = [1, 0, 1, 0, 1]
index_feature_mapping = ["a", "b", "c", "d", "e"]
COMBINED_EMBEDDING (5):
The tensor is encoded into a 1-dimensional array represented
by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [0.1, 0.2, 0.3, 0.4, 0.5]
CONCAT_EMBEDDING (6):
Select this encoding when the input tensor is encoded into a
2-dimensional array represented by an encoded tensor.
<xref uid="google.cloud.aiplatform.v1beta1.ExplanationMetadata.InputMetadata.encoded_tensor_name">InputMetadata.encoded_tensor_name</xref>
must be provided for this encoding. The first dimension of
the encoded tensor's shape is the same as the input tensor's
shape. For example:
::
input = ["This", "is", "a", "test", "."]
encoded = [[0.1, 0.2, 0.3, 0.4, 0.5],
[0.2, 0.1, 0.4, 0.3, 0.5],
[0.5, 0.1, 0.3, 0.5, 0.4],
[0.5, 0.3, 0.1, 0.2, 0.4],
[0.4, 0.3, 0.2, 0.5, 0.1]]
```


### FeatureValueDomain

`FeatureValueDomain(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Domain details of the input feature value. Provides numeric information about the feature, such as its range (min, max). If the feature has been pre-processed, for example with z-scoring, then it provides information about how to recover the original feature. For example, if the input feature is an image and it has been pre-processed to obtain 0-mean and stddev = 1 values, then original_mean, and original_stddev refer to the mean and stddev of the original feature (e.g. image tensor) from which input feature (with mean = 0 and stddev = 1) was obtained.

### Visualization

`Visualization(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Visualization configurations for image explanation.

## Methods

### InputMetadata

`InputMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the input of a feature.

Fields other than InputMetadata.input_baselines are applicable only for Models that are using Vertex AI-provided images for Tensorflow.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlForecastingInputs.Transformation.AutoTransformation -->

# Class AutoTransformation (1.134.0)

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

## Methods

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

### AutoTransformation

`AutoTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Training pipeline will infer the proper transformation based on the statistic of dataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetAnnotationSpecRequest -->

# Class GetAnnotationSpecRequest (1.134.0)

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/annotationSpecs/{annotation_spec}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetAnnotationSpecRequest

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.MetricSpec.SafetyMetricConfig -->

# Class SafetyMetricConfig (1.134.0)

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`safety_threshold` |
`float`
Safety threshold (boundary value between safe and unsafe). NOTE that if you leave SafetyMetricConfig unset, a default value of 0 will be used. |
`desired_min_safe_trials_fraction` |
`float`
Desired minimum fraction of safe trials (over total number of trials) that should be targeted by the algorithm at any time during the study (best effort). This should be between 0.0 and 1.0 and a value of 0.0 means that there is no minimum and an algorithm proceeds without targeting any specific fraction. A value of 1.0 means that the algorithm attempts to only Suggest safe Trials. This field is a member of `oneof` _ `_desired_min_safe_trials_fraction` .
|

## Methods

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
The id of the similar entity. |
`distance` |
`float`
The distance between the neighbor and the query vector. |
`entity_key_values` |
The attributes of the neighbor, e.g. filters, crowding and metadata Note that full entities are returned only when "return_full_entity" is set to true. Otherwise, only the "entity_id" and "distance" fields are populated. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RebootPersistentResourceRequest -->

# Class RebootPersistentResourceRequest (1.134.0)

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: `projects/{project_id_or_number}/locations/{location_id}/persistentResources/{persistent_resource_id}`
|

## Methods

### RebootPersistentResourceRequest

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse -->

# Class ListModelEvaluationsResponse (1.134.0)

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluations` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationsRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationsResponse

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagContexts -->

# Class RagContexts (1.134.0)

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
All its contexts. |

## Classes

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagContexts

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.ExplanationConfig -->

# Class ExplanationConfig (1.134.0)

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

## Attributes |
|
|---|---|
Name |
Description |
`enable_feature_attributes` |
`bool`
If want to analyze the Vertex Explainable AI feature attribute scores or not. If set to true, Vertex AI will log the feature attributions from explain response and do the skew/drift detection for them. |
`explanation_baseline` |
Predictions generated by the BatchPredictionJob using baseline dataset. |

## Classes

### ExplanationBaseline

`ExplanationBaseline(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output from BatchPredictionJob for Model Monitoring baseline dataset, which can be used to generate baseline attribution scores.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### ExplanationConfig

`ExplanationConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for integrating with Vertex Explainable AI. Only applicable if the Model has explanation_spec populated.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualityInstance -->

# Class PairwiseQuestionAnsweringQualityInstance (1.134.0)

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the candidate model. This field is a member of `oneof` _ `_prediction` .
|
`baseline_prediction` |
`str`
Required. Output of the baseline model. This field is a member of `oneof` _ `_baseline_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### PairwiseQuestionAnsweringQualityInstance

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewSyncRequest -->

# Class GetFeatureViewSyncRequest (1.134.0)

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureViewSync resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}/featureViewSyncs/{feature_view_sync}`
|

## Methods

### GetFeatureViewSyncRequest

`GetFeatureViewSyncRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureViewSync.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextSentiment -->

# Class AutoMlTextSentiment (1.134.0)

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

## Attribute |
|
|---|---|
Name |
Description |
`inputs` |
The input parameters of this TrainingJob. |

## Methods

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

### AutoMlTextSentiment

`AutoMlTextSentiment(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A TrainingJob that trains and uploads an AutoML Text Sentiment Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagRetrievalConfig.Filter -->

# Class Filter (1.134.0)

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
`vector_distance_threshold` |
`float`
Optional. Only returns contexts with vector distance smaller than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`vector_similarity_threshold` |
`float`
Optional. Only returns contexts with vector similarity larger than the threshold. This field is a member of `oneof` _ `vector_db_threshold` .
|
`metadata_filter` |
`str`
Optional. String for metadata filtering. |

## Methods

### Filter

`Filter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for filters.

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
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelDeploymentMonitoringJobsRequest -->

# Class ListModelDeploymentMonitoringJobsRequest (1.134.0)

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`
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
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read |

## Methods

### ListModelDeploymentMonitoringJobsRequest

```
ListModelDeploymentMonitoringJobsRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.ListModelDeploymentMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.134.0)

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The resource name of the Model to update. Format: `projects/{project}/locations/{location}/models/{model}`
|
`examples` |
The example config containing the location of the dataset. |

## Methods

### UpdateExplanationDatasetRequest

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AddContextChildrenRequest -->

# Class AddContextChildrenRequest (1.134.0)

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

## Attributes |
|
|---|---|
Name |
Description |
`context` |
`str`
Required. The resource name of the parent Context. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}`
|
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. |

## Methods

### AddContextChildrenRequest

`AddContextChildrenRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.AddContextChildren.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tensorboard -->

# Class Tensorboard (1.134.0)

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Tensorboard. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`display_name` |
`str`
Required. User provided name of this Tensorboard. |
`description` |
`str`
Description of this Tensorboard. |
`encryption_spec` |
Customer-managed encryption key spec for a Tensorboard. If set, this Tensorboard and all sub-resources of this Tensorboard will be secured by this key. |
`blob_storage_path_prefix` |
`str`
Output only. Consumer project Cloud Storage path prefix used to store blob data, which can either be a bucket or directory. Does not end with a '/'. |
`run_count` |
`int`
Output only. The number of Runs stored in this Tensorboard. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`is_default` |
`bool`
Used to indicate if the TensorBoard instance is the default one. Each project & region can have at most one default TensorBoard instance. Creation of a default TensorBoard instance and updating an existing TensorBoard instance to be default will mark all other TensorBoard instances (if any) as non default. |
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

### Tensorboard

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.MetricSpec.SafetyMetricConfig -->

# Class SafetyMetricConfig (1.134.0)

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`safety_threshold` |
`float`
Safety threshold (boundary value between safe and unsafe). NOTE that if you leave SafetyMetricConfig unset, a default value of 0 will be used. |
`desired_min_safe_trials_fraction` |
`float`
Desired minimum fraction of safe trials (over total number of trials) that should be targeted by the algorithm at any time during the study (best effort). This should be between 0.0 and 1.0 and a value of 0.0 means that there is no minimum and an algorithm proceeds without targeting any specific fraction. A value of 1.0 means that the algorithm attempts to only Suggest safe Trials. This field is a member of `oneof` _ `_desired_min_safe_trials_fraction` .
|

## Methods

### SafetyMetricConfig

`SafetyMetricConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Used in safe optimization to specify threshold levels and risk tolerance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.ParameterSpec.ConditionalParameterSpec.CategoricalValueCondition -->

# Class CategoricalValueCondition (1.134.0)

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
Required. Matches values of the parent parameter of 'CATEGORICAL' type. All values must exist in `categorical_value_spec` of parent parameter.
|

## Methods

### CategoricalValueCondition

`CategoricalValueCondition(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec to match categorical values from parent parameter.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.134.0)

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ReasoningEngine in. Format: `projects/{project}/locations/{location}`
|
`reasoning_engine` |
Required. The ReasoningEngine to create. |

## Methods

### CreateReasoningEngineRequest

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.LineageSubgraph -->

# Class LineageSubgraph (1.134.0)

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifact nodes in the subgraph. |
`executions` |
`MutableSequence[`
The Execution nodes in the subgraph. |
`events` |
`MutableSequence[`
The Event edges between Artifacts and Executions in the subgraph. |

## Methods

### LineageSubgraph

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateReasoningEngineRequest -->

# Class UpdateReasoningEngineRequest (1.134.0)

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`reasoning_engine` |
Required. The ReasoningEngine which replaces the resource on the server. |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to update. |

## Methods

### UpdateReasoningEngineRequest

```
UpdateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.UpdateReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.134.0)

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

## Attributes |
|
|---|---|
Name |
Description |
`explanation_type` |
`str`
Explanation type. For AutoML Image Classification models, possible values are: - `image-integrated-gradients`
- `image-xrai`
|
`explanation` |
Explanation attribution response details. |

## Methods

### EvaluatedAnnotationExplanation

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTrainingPipelineRequest -->

# Class CreateTrainingPipelineRequest (1.134.0)

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the TrainingPipeline in. Format: `projects/{project}/locations/{location}`
|
`training_pipeline` |
Required. The TrainingPipeline to create. |

## Methods

### CreateTrainingPipelineRequest

```
CreateTrainingPipelineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PipelineService.CreateTrainingPipeline.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Tensorboard -->

# Class Tensorboard (1.134.0)

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the Tensorboard. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`
|
`display_name` |
`str`
Required. User provided name of this Tensorboard. |
`description` |
`str`
Description of this Tensorboard. |
`encryption_spec` |
Customer-managed encryption key spec for a Tensorboard. If set, this Tensorboard and all sub-resources of this Tensorboard will be secured by this key. |
`blob_storage_path_prefix` |
`str`
Output only. Consumer project Cloud Storage path prefix used to store blob data, which can either be a bucket or directory. Does not end with a '/'. |
`run_count` |
`int`
Output only. The number of Runs stored in this Tensorboard. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Tensorboard was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Tensorboards. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Tensorboard (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`is_default` |
`bool`
Used to indicate if the TensorBoard instance is the default one. Each project & region can have at most one default TensorBoard instance. Creation of a default TensorBoard instance and updating an existing TensorBoard instance to be default will mark all other TensorBoard instances (if any) as non default. |
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

### Tensorboard

`Tensorboard(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tensorboard is a physical database that stores users' training metrics. A default Tensorboard is provided in each region of a Google Cloud project. If needed users can also create extra Tensorboards in their projects.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.134.0)

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### CancelHyperparameterTuningJobRequest

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ShieldedVmConfig -->

# Class ShieldedVmConfig (1.134.0)

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

## Attribute |
|
|---|---|
Name |
Description |
`enable_secure_boot` |
`bool`
Defines whether the instance has `Secure Boot |

## Methods

### ShieldedVmConfig

`ShieldedVmConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A set of Shielded Instance options. See ```
Images using supported
Shielded VM
features <https://cloud.google.com/compute/docs/instances/modifying-shielded-vm>
```

__.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.CategoricalArrayTransformation -->

# Class CategoricalArrayTransformation (1.134.0)

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

## Methods

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

### CategoricalArrayTransformation

```
CategoricalArrayTransformation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Treats the column as categorical array and performs following transformation functions.

- For each element in the array, convert the category name to a dictionary lookup index and generate an embedding for each index. Combine the embedding of all elements into a single embedding using the mean.
- Empty arrays treated as an embedding of zeroes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1beta1.services.feature_registry_service.pagers`

module.

## Classes

[ListFeatureGroupsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager)

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureGroupsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsPager)

```
ListFeatureGroupsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
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


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorJobsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsAsyncPager)

```
ListFeatureMonitorJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorJobsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager)

```
ListFeatureMonitorJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
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


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsAsyncPager)

```
ListFeatureMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
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


A pager for iterating through `list_feature_monitors`

requests.

This class thinly wraps an initial
[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitors`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitors`

requests and continue to iterate
through the `feature_monitors`

field on the
corresponding responses.

All the usual [ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeatureMonitorsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsPager)

```
ListFeatureMonitorsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
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


A pager for iterating through `list_feature_monitors`

requests.

This class thinly wraps an initial
[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_monitors`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureMonitors`

requests and continue to iterate
through the `feature_monitors`

field on the
corresponding responses.

All the usual [ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesAsyncPager)

```
ListFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeaturesPager)

```
ListFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturesResponse,
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


A pager for iterating through `list_features`

requests.

This class thinly wraps an initial
[ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [ListFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient -->

# Class MatchServiceClient (1.134.0)

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


MatchService is a Google managed service for efficient vector similarity search at scale.

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
`MatchServiceTransport` |
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

### MatchServiceClient

```
MatchServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MatchServiceTransport,Callable[..., MatchServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.FindNeighborsRequest, dict
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
) -> google.cloud.aiplatform_v1.types.match_service.FindNeighborsResponse
```


Finds the nearest neighbors of each vector within the request.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_find_neighbors():
# Create a client
client = aiplatform_v1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
The response message for MatchService.FindNeighbors. |

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
`MatchServiceClient` |
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
`MatchServiceClient` |
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
`MatchServiceClient` |
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

### index_endpoint_path

`index_endpoint_path(project: str, location: str, index_endpoint: str) -> str`


Returns a fully-qualified index_endpoint string.

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

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1.types.match_service.ReadIndexDatapointsResponse
```


Reads the datapoints/vectors of the given IDs. A maximum of 1000 datapoints can be retrieved in a batch.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1.
```[MatchServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseQuestionAnsweringQualityInstance -->

# Class PairwiseQuestionAnsweringQualityInstance (1.134.0)

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`prediction` |
`str`
Required. Output of the candidate model. This field is a member of `oneof` _ `_prediction` .
|
`baseline_prediction` |
`str`
Required. Output of the baseline model. This field is a member of `oneof` _ `_baseline_prediction` .
|
`reference` |
`str`
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`context` |
`str`
Required. Text to answer the question. This field is a member of `oneof` _ `_context` .
|
`instruction` |
`str`
Required. Question Answering prompt for LLM. This field is a member of `oneof` _ `_instruction` .
|

## Methods

### PairwiseQuestionAnsweringQualityInstance

```
PairwiseQuestionAnsweringQualityInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StopNotebookRuntimeRequest -->

# Class StopNotebookRuntimeRequest (1.134.0)

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be stopped. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StopNotebookRuntimeRequest

`StopNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StopNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookExecutionJob.GcsNotebookSource -->

# Class GcsNotebookSource (1.134.0)

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`
|
`generation` |
`str`
The version of the Cloud Storage object to read. If unset, the current version of the object is read. See https://cloud.google.com/storage/docs/metadata#generation-number. |

## Methods

### GcsNotebookSource

`GcsNotebookSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Cloud Storage uri for the input notebook.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseMetricSpec -->

# Class PairwiseMetricSpec (1.134.0)

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`metric_prompt_template` |
`str`
Required. Metric prompt template for pairwise metric. This field is a member of `oneof` _ `_metric_prompt_template` .
|
`candidate_response_field_name` |
`str`
Optional. The field name of the candidate response. |
`baseline_response_field_name` |
`str`
Optional. The field name of the baseline response. |
`system_instruction` |
`str`
Optional. System instructions for pairwise metric. This field is a member of `oneof` _ `_system_instruction` .
|
`custom_output_format_config` |
Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwise_choice` and `explanation`
fields in the corresponding metric result will be empty.
|

## Methods

### PairwiseMetricSpec

`PairwiseMetricSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for pairwise metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service -->

# Package featurestore_online_serving_service (1.134.0)

API documentation for `aiplatform_v1beta1.services.featurestore_online_serving_service`

package.

## Classes

[FeaturestoreOnlineServingServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceAsyncClient)

A service for serving online feature values.

[FeaturestoreOnlineServingServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_online_serving_service.FeaturestoreOnlineServingServiceClient)

A service for serving online feature values.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateEndpointLongRunningRequest -->

# Class UpdateEndpointLongRunningRequest (1.134.0)

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

## Attribute |
|
|---|---|
Name |
Description |
`endpoint` |
Required. The Endpoint which replaces the resource on the server. Currently we only support updating the `client_connection_config` field, all the other fields'
update will be blocked.
|

## Methods

### UpdateEndpointLongRunningRequest

```
UpdateEndpointLongRunningRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for EndpointService.UpdateEndpointLongRunning.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.VertexAiSearchConfig -->

# Class VertexAiSearchConfig (1.134.0)

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

## Attribute |
|
|---|---|
Name |
Description |
`serving_config` |
`str`
Vertex AI Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}`
or
`projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` .
|

## Methods

### VertexAiSearchConfig

`VertexAiSearchConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for the Vertex AI Search.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetAnnotationSpecRequest -->

# Class GetAnnotationSpecRequest (1.134.0)

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the AnnotationSpec resource. Format: `projects/{project}/locations/{location}/datasets/{dataset}/annotationSpecs/{annotation_spec}`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### GetAnnotationSpecRequest

`GetAnnotationSpecRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.GetAnnotationSpec.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NearestNeighbors.Neighbor -->

# Class Neighbor (1.134.0)

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

## Attributes |
|
|---|---|
Name |
Description |
`entity_id` |
`str`
The id of the similar entity. |
`distance` |
`float`
The distance between the neighbor and the query vector. |
`entity_key_values` |
The attributes of the neighbor, e.g. filters, crowding and metadata Note that full entities are returned only when "return_full_entity" is set to true. Otherwise, only the "entity_id" and "distance" fields are populated. |

## Methods

### Neighbor

`Neighbor(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A neighbor of the query vector.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeRequest -->

# Class StartNotebookRuntimeRequest (1.134.0)

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the NotebookRuntime resource to be started. Instead of checking whether the name is in valid NotebookRuntime resource name format, directly throw NotFound exception if there is no such NotebookRuntime in spanner. |

## Methods

### StartNotebookRuntimeRequest

`StartNotebookRuntimeRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.StartNotebookRuntime.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationsResponse -->

# Class ListModelEvaluationsResponse (1.134.0)

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

## Attributes |
|
|---|---|
Name |
Description |
`model_evaluations` |
`MutableSequence[`
List of ModelEvaluations in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListModelEvaluationsRequest.page_token to obtain that page. |

## Methods

### ListModelEvaluationsResponse

```
ListModelEvaluationsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelService.ListModelEvaluations.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse -->

# Class ListFeaturestoresResponse (1.134.0)

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

## Attributes |
|
|---|---|
Name |
Description |
`featurestores` |
`MutableSequence[`
The Featurestores matching the request. |
`next_page_token` |
`str`
A token, which can be sent as ListFeaturestoresRequest.page_token to retrieve the next page. If this field is omitted, there are no subsequent pages. |

## Methods

### ListFeaturestoresResponse

`ListFeaturestoresResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for FeaturestoreService.ListFeaturestores.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebootPersistentResourceRequest -->

# Class RebootPersistentResourceRequest (1.134.0)

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the PersistentResource resource. Format: `projects/{project_id_or_number}/locations/{location_id}/persistentResources/{persistent_resource_id}`
|

## Methods

### RebootPersistentResourceRequest

```
RebootPersistentResourceRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for PersistentResourceService.RebootPersistentResource.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagContexts -->

# Class RagContexts (1.134.0)

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

## Attribute |
|
|---|---|
Name |
Description |
`contexts` |
`MutableSequence[`
All its contexts. |

## Classes

### Context

`Context(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A context of the query.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RagContexts

`RagContexts(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Relevant contexts for one query.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest -->

# Class RetrieveContextsRequest (1.134.0)

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
The data source for Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`query` |
Required. Single RAG retrieve query. |

## Classes

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RetrieveContextsRequest

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteTensorboardExperimentRequest -->

# Class DeleteTensorboardExperimentRequest (1.134.0)

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardExperiment to be deleted. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|

## Methods

### DeleteTensorboardExperimentRequest

```
DeleteTensorboardExperimentRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.DeleteTensorboardExperiment.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExplanationDatasetRequest -->

# Class UpdateExplanationDatasetRequest (1.134.0)

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Required. The resource name of the Model to update. Format: `projects/{project}/locations/{location}/models/{model}`
|
`examples` |
The example config containing the location of the dataset. |

## Methods

### UpdateExplanationDatasetRequest

```
UpdateExplanationDatasetRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.UpdateExplanationDataset.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse -->

# Class ListNotebookRuntimesResponse (1.134.0)

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`notebook_runtimes` |
`MutableSequence[`
List of NotebookRuntimes in the requested page. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to ListNotebookRuntimesRequest.page_token to obtain that page. |

## Methods

### ListNotebookRuntimesResponse

```
ListNotebookRuntimesResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for NotebookService.ListNotebookRuntimes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse -->

# Class ListModelMonitoringJobsResponse (1.134.0)

```
ListModelMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.ListModelMonitoringJobs.

## Attributes |
|
|---|---|
Name |
Description |
`model_monitoring_jobs` |
`MutableSequence[`
A list of ModelMonitoringJobs that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListModelMonitoringJobsResponse

```
ListModelMonitoringJobsResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for ModelMonitoringService.ListModelMonitoringJobs.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.LineageSubgraph -->

# Class LineageSubgraph (1.134.0)

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

## Attributes |
|
|---|---|
Name |
Description |
`artifacts` |
`MutableSequence[`
The Artifact nodes in the subgraph. |
`executions` |
`MutableSequence[`
The Execution nodes in the subgraph. |
`events` |
`MutableSequence[`
The Event edges between Artifacts and Executions in the subgraph. |

## Methods

### LineageSubgraph

`LineageSubgraph(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateReasoningEngineRequest -->

# Class CreateReasoningEngineRequest (1.134.0)

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the ReasoningEngine in. Format: `projects/{project}/locations/{location}`
|
`reasoning_engine` |
Required. The ReasoningEngine to create. |

## Methods

### CreateReasoningEngineRequest

```
CreateReasoningEngineRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ReasoningEngineService.CreateReasoningEngine.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StartNotebookRuntimeOperationMetadata -->

# Class StartNotebookRuntimeOperationMetadata (1.134.0)

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`progress_message` |
`str`
A human-readable message that shows the intermediate progress details of NotebookRuntime. |

## Methods

### StartNotebookRuntimeOperationMetadata

```
StartNotebookRuntimeOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Metadata information for NotebookService.StartNotebookRuntime.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelGardenSource -->

# Class ModelGardenSource (1.134.0)

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

## Attributes |
|
|---|---|
Name |
Description |
`public_model_name` |
`str`
Required. The model garden source model resource name. |
`version_id` |
`str`
Optional. The model garden source model version ID. |
`skip_hf_model_cache` |
`bool`
Optional. Whether to avoid pulling the model from the HF cache. |

## Methods

### ModelGardenSource

`ModelGardenSource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the source of the models generated from Model Garden.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service -->

# Package tensorboard_service (1.134.0)

API documentation for `aiplatform_v1.services.tensorboard_service`

package.

## Classes

[TensorboardServiceAsyncClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceAsyncClient)

TensorboardService

[TensorboardServiceClient](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.TensorboardServiceClient)

TensorboardService

## Modules

[pagers](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers)

API documentation for `aiplatform_v1.services.tensorboard_service.pagers`

module.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CancelHyperparameterTuningJobRequest -->

# Class CancelHyperparameterTuningJobRequest (1.134.0)

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameter_tuning_job}`
|

## Methods

### CancelHyperparameterTuningJobRequest

```
CancelHyperparameterTuningJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.CancelHyperparameterTuningJob.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata.Visualization.OverlayType -->

# Class OverlayType (1.134.0)

`OverlayType(value)`


How the original image is displayed in the visualization.

## Enums |
|
|---|---|
Name |
Description |
`OVERLAY_TYPE_UNSPECIFIED` |
Default value. This is the same as NONE. |
`NONE` |
No overlay. |
`ORIGINAL` |
The attributions are shown on top of the original image. |
`GRAYSCALE` |
The attributions are shown on top of grayscaled version of the original image. |
`MASK_BLACK` |
The attributions are used as a mask to reveal predictive parts of the image and hide the un-predictive parts. |

## Methods

### OverlayType

`OverlayType(value)`


How the original image is displayed in the visualization.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluatedAnnotationExplanation -->

# Class EvaluatedAnnotationExplanation (1.134.0)

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

## Attributes |
|
|---|---|
Name |
Description |
`explanation_type` |
`str`
Explanation type. For AutoML Image Classification models, possible values are: - `image-integrated-gradients`
- `image-xrai`
|
`explanation` |
Explanation attribution response details. |

## Methods

### EvaluatedAnnotationExplanation

```
EvaluatedAnnotationExplanation(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Explanation result of the prediction produced by the Model.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveContextsRequest -->

# Class RetrieveContextsRequest (1.134.0)

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
The data source for Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`query` |
Required. Single RAG retrieve query. |

## Classes

### VertexRagStore

`VertexRagStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The data source for Vertex RagStore.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### RetrieveContextsRequest

`RetrieveContextsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagService.RetrieveContexts.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)
