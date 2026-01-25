---
merged_at: 2026-01-25T21:47:44.392607
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__goog_9fd00f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__googl_9ba1e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__google_ab2955.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__googlec_cfc1cc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__googlecl_94d694.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__googleclo_74b3bb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest__googleclou_d2928c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstreamingreadfeaturevaluesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StreamingReadFeatureValuesRequest -->

# Class StreamingReadFeatureValuesRequest (1.134.0)

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.

## Attributes |
|
|---|---|
Name |
Description |
`entity_type` |
`str`
Required. The resource name of the entities' type. Value format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entityType}` .
For example, for a machine learning model predicting user
clicks on a website, an EntityType ID could be `user` .
|
`entity_ids` |
`MutableSequence[str]`
Required. IDs of entities to read Feature values of. The maximum number of IDs is 100. For example, for a machine learning model predicting user clicks on a website, an entity ID could be `user_123` .
|
`feature_selector` |
Required. Selector choosing Features of the target EntityType. Feature IDs will be deduplicated. |

## Methods

### StreamingReadFeatureValuesRequest

```
StreamingReadFeatureValuesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for FeaturestoreOnlineServingService.StreamingReadFeatureValues.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesboolarray_googlecloudaiplatform_v1typesexportmodel_e90963.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesboolarray.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BoolArray -->

# Class BoolArray (1.134.0)

`BoolArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of boolean values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[bool]`
A list of bool values. |

## Methods

### BoolArray

`BoolArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of boolean values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexportmodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelResponse -->

# Class ExportModelResponse (1.134.0)

`ExportModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.ExportModel operation.

## Methods

### ExportModelResponse

`ExportModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.ExportModel operation.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmetricxinstance_googlecloudaiplatform_v1beta1types_58c49f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmetricxinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetricxInstance -->

# Class MetricxInstance (1.134.0)

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

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
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### MetricxInstance

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesclaim.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Claim -->

# Class Claim (1.134.0)

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Index in the input text where the claim starts (inclusive). This field is a member of `oneof` _ `_start_index` .
|
`end_index` |
`int`
Index in the input text where the claim ends (exclusive). This field is a member of `oneof` _ `_end_index` .
|
`fact_indexes` |
`MutableSequence[int]`
Indexes of the facts supporting this claim. |
`score` |
`float`
Confidence score of this corroboration. This field is a member of `oneof` _ `_score` .
|

## Methods

### Claim

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schematrainingjobdefinition_v1beta1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmo_2de1d5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmon_e0a7c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerslistmodelmonitoringjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitoringJobsPager -->

# Class ListModelMonitoringJobsPager (1.134.0)

```
ListModelMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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


A pager for iterating through `list_model_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelMonitoringJobs`

requests and continue to iterate
through the `model_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitoringJobsPager

```
ListModelMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesnotebooksoftwareconfig_googlecloudaiplatform_v1typ_3dcd3f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebooksoftwareconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookSoftwareConfig -->

# Class NotebookSoftwareConfig (1.134.0)

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`colab_image` |
Optional. Google-managed NotebookRuntime colab image. This field is a member of `oneof` _ `runtime_image` .
|
`env` |
`MutableSequence[`
Optional. Environment variables to be passed to the container. Maximum limit is 100. |
`post_startup_script_config` |
Optional. Post startup script config. |

## Methods

### NotebookSoftwareConfig

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesclaim.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Claim -->

# Class Claim (1.134.0)

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`start_index` |
`int`
Index in the input text where the claim starts (inclusive). This field is a member of `oneof` _ `_start_index` .
|
`end_index` |
`int`
Index in the input text where the claim ends (exclusive). This field is a member of `oneof` _ `_end_index` .
|
`fact_indexes` |
`MutableSequence[int]`
Indexes of the facts supporting this claim. |
`score` |
`float`
Confidence score of this corroboration. This field is a member of `oneof` _ `_score` .
|

## Methods

### Claim

`Claim(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Claim that is extracted from the input text and facts that support it.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescreatefeaturerequest_googlecloudaiplatform_v_c6b2fb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescreatefeaturerequest_googlecloudaiplatform_v1_b7ca36.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatefeaturerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateFeatureRequest -->

# Class CreateFeatureRequest (1.134.0)

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType or FeatureGroup to create a Feature. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`feature` |
Required. The Feature to create. |
`feature_id` |
`str`
Required. The ID to use for the Feature, which will become the final component of the Feature's resource name. This value may be up to 128 characters, and valid characters are `[a-z0-9_]` . The first character cannot be a number.
The value must be unique within an EntityType/FeatureGroup.
|

## Methods

### CreateFeatureRequest

`CreateFeatureRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.CreateFeature. Request message for FeatureRegistryService.CreateFeature.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesquestionansweringrelevanceresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringRelevanceResult -->

# Class QuestionAnsweringRelevanceResult (1.134.0)

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Relevance score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering relevance score. |
`confidence` |
`float`
Output only. Confidence for question answering relevance score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringRelevanceResult

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistnotebookruntimesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest -->

# Class ListNotebookRuntimesRequest (1.134.0)

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookRuntime` supports = and !=. `notebookRuntime`
represents the NotebookRuntime ID, i.e. the last segment
of the NotebookRuntime's [resource name]
[google.cloud.aiplatform.v1beta1.NotebookRuntime.name].
- `displayName` supports = and != and regex.
- `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1beta1.NotebookRuntimeTemplate.name].
- `healthState` supports = and !=. healthState enum:
[HEALTHY, UNHEALTHY, HEALTH_STATE_UNSPECIFIED].
- `runtimeState` supports = and !=. runtimeState enum:
[RUNTIME_STATE_UNSPECIFIED, RUNNING, BEING_STARTED,
BEING_STOPPED, STOPPED, BEING_UPGRADED, ERROR, INVALID].
- `runtimeUser` supports = and !=.
- API version is UI only: `uiState` supports = and !=.
uiState enum: [UI_RESOURCE_STATE_UNSPECIFIED,
UI_RESOURCE_STATE_BEING_CREATED, UI_RESOURCE_STATE_ACTIVE,
UI_RESOURCE_STATE_BEING_DELETED,
UI_RESOURCE_STATE_CREATION_FAILED].
- `notebookRuntimeType` supports = and !=.
notebookRuntimeType enum: [USER_DEFINED, ONE_CLICK].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.
Some examples:
- `notebookRuntime="notebookRuntime123"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
- `notebookRuntimeTemplate="notebookRuntimeTemplate321"`
- `healthState=HEALTHY`
- `runtimeState=RUNNING`
- `runtimeUser="test@google.com"`
- `uiState=UI_RESOURCE_STATE_BEING_DELETED`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookRuntimesResponse.next_page_token of the previous NotebookService.ListNotebookRuntimes call. |
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

### ListNotebookRuntimesRequest

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationslicesa_47572d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationslicesas_aba7e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationslicesasy_53367f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationslicesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationSlicesAsyncPager -->

# Class ListModelEvaluationSlicesAsyncPager (1.134.0)

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesAsyncPager

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesquestionansweringrelevanceresult_googlecloudaiplat_3d3d93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesquestionansweringrelevanceresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringRelevanceResult -->

# Class QuestionAnsweringRelevanceResult (1.134.0)

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Question Answering Relevance score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for question answering relevance score. |
`confidence` |
`float`
Output only. Confidence for question answering relevance score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### QuestionAnsweringRelevanceResult

```
QuestionAnsweringRelevanceResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for question answering relevance result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdistillationhyperparameters.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DistillationHyperParameters -->

# Class DistillationHyperParameters (1.134.0)

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`epoch_count` |
`int`
Optional. Number of complete passes the model makes over the entire training dataset during training. This field is a member of `oneof` _ `_epoch_count` .
|
`learning_rate_multiplier` |
`float`
Optional. Multiplier for adjusting the default learning rate. This field is a member of `oneof` _ `_learning_rate_multiplier` .
|
`adapter_size` |
Optional. Adapter size for distillation. |

## Methods

### DistillationHyperParameters

`DistillationHyperParameters(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Hyperparameters for Distillation.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesboolarray_googlecloudaiplatform_v1beta1type_e1eec9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesboolarray_googlecloudaiplatform_v1beta1types_e45b45.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesboolarray_googlecloudaiplatform_v1beta1typesi_58ff79.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesboolarray.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BoolArray -->

# Class BoolArray (1.134.0)

`BoolArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of boolean values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[bool]`
A list of bool values. |

## Methods

### BoolArray

`BoolArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of boolean values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesint64array.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Int64Array -->

# Class Int64Array (1.134.0)

`Int64Array(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of int64 values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[int]`
A list of int64 values. |

## Methods

### Int64Array

`Int64Array(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of int64 values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpredictionpredictionhandler.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.PredictionHandler -->

# Class PredictionHandler (1.134.0)

```
PredictionHandler(
artifacts_uri: str,
predictor: typing.Optional[
typing.Type[google.cloud.aiplatform.prediction.predictor.Predictor]
] = None,
)
```


Default prediction handler for the prediction requests sent to the application.

## Methods

### PredictionHandler

```
PredictionHandler(
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

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If predictor is None. |

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
Required. The prediction request sent to the application. |

Exceptions |
|
|---|---|
Type |
Description |
`HTTPException` |
If any exception is thrown from predictor object. |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmutatedeployedmodelrequest_googlecloudaiplatf_191cbc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmutatedeployedmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MutateDeployedModelRequest -->

# Class MutateDeployedModelRequest (1.134.0)

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint resource into which to mutate a DeployedModel. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`deployed_model` |
Required. The DeployedModel to be mutated within the Endpoint. Only the following fields can be mutated: - `min_replica_count` in either
DedicatedResources
or
AutomaticResources
- `max_replica_count` in either
DedicatedResources
or
AutomaticResources
- `required_replica_count` in
DedicatedResources
- autoscaling_metric_specs
- `disable_container_logging` (v1 only)
- `enable_container_logging` (v1beta1 only)
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. The update mask applies to the resource. See `google.protobuf.FieldMask][google.protobuf.FieldMask]` .
|

## Methods

### MutateDeployedModelRequest

`MutateDeployedModelRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for EndpointService.MutateDeployedModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchcreatefeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateFeaturesRequest -->

# Class BatchCreateFeaturesRequest (1.134.0)

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the EntityType/FeatureGroup to create the batch of Features under. Format: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`requests` |
`MutableSequence[`
Required. The request message specifying the Features to create. All Features must be created under the same parent EntityType / FeatureGroup. The `parent` field in each
child request message can be omitted. If `parent` is set
in a child request, then the value must match the `parent`
value in this request message.
|

## Methods

### BatchCreateFeaturesRequest

`BatchCreateFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.BatchCreateFeatures. Request message for FeatureRegistryService.BatchCreateFeatures.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtimeseriesdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TimeSeriesDataset -->

# Class TimeSeriesDataset (1.134.0)

```
TimeSeriesDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


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


## Properties

### column_names

Retrieve the columns for the dataset by extracting it from the Google Cloud Storage or Google BigQuery source.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
When no valid source is found. |

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

### TimeSeriesDataset

```
TimeSeriesDataset(
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
bq_source: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.datasets.time_series_dataset.TimeSeriesDataset
```


Creates a new time series dataset.

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
`bq_source` |
`str`
A BigQuery URI for the input table. For example, |
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
`time_series_dataset (TimeSeriesDataset)` |
An instantiated representation of the managed `TimeSeriesDataset` resource. |

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

`import_data()`


Upload data to existing managed dataset.

Parameters |
|
|---|---|
Name |
Description |
`gcs_source` |
`Union[str, Sequence[str]]`
Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see |
`import_schema_uri` |
`str`
Required. Points to a YAML file stored on Google Cloud Storage describing the import format. Validation will be done against the schema. The schema is defined as an |
`data_item_labels` |
`Dict`
Labels that will be applied to newly imported DataItems. If an identical DataItem as one being imported already exists in the Dataset, then these labels will be appended to these of the already existing one, and if labels with identical key is imported before, the old label value will be overwritten. If two DataItems are identical in the same import data operation, the labels will be combined and if key collision happens in this case, one of the values will be picked randomly. Two DataItems are considered identical if their content bytes are identical (e.g. image bytes or pdf bytes). These labels will be overridden by Annotation labels specified inside index file referenced by |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`import_request_timeout` |
`float`
Optional. The timeout for the import request in seconds. |

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmatch_servicematchserviceasyncclient_____google_f7eec2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmatch_servicematchserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient -->

# Class MatchServiceAsyncClient (1.134.0)

```
MatchServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### MatchServiceAsyncClient

```
MatchServiceAsyncClient(
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
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_find_neighbors():
# Create a client
client = aiplatform_v1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceAsyncClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
google.cloud.aiplatform_v1.services.match_service.transports.base.MatchServiceTransport
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
google.api_core.retry.retry_unary_async.AsyncRetry,
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
async def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1_services_match_service_MatchServiceAsyncClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpred_699ce0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredi_5f2edc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredic_2488ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredict_176d93.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigtrainingpredictionskewdetectionconfigattributionscoreskewthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.TrainingPredictionSkewDetectionConfig.AttributionScoreSkewThresholdsEntry -->

# Class AttributionScoreSkewThresholdsEntry (1.134.0)

```
AttributionScoreSkewThresholdsEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The abstract base class for a message.

## Parameters |
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


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrawoutput_googlecloudaiplatform_v1typesmodali_b0ac7d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrawoutput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RawOutput -->

# Class RawOutput (1.134.0)

`RawOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw output.

## Attribute |
|
|---|---|
Name |
Description |
`raw_output` |
`MutableSequence[str]`
Output only. Raw output string. |

## Methods

### RawOutput

`RawOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Raw output.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodality.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Modality -->

# Class Modality (1.134.0)

`Modality(value)`


Content Part modality

## Enums |
|
|---|---|
Name |
Description |
`MODALITY_UNSPECIFIED` |
Unspecified modality. |
`TEXT` |
Plain text. |
`IMAGE` |
Image. |
`VIDEO` |
Video. |
`AUDIO` |
Audio. |
`DOCUMENT` |
Document, e.g. PDF. |

## Methods

### Modality

`Modality(value)`


Content Part modality


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversioncheckpointsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionCheckpointsAsyncPager -->

# Class ListModelVersionCheckpointsAsyncPager (1.134.0)

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
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


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsAsyncPager

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookruntimet_40ee2d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesnotebook_servicepagerslistnotebookruntimetemplatespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager -->

# Class ListNotebookRuntimeTemplatesPager (1.134.0)

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesPager

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistpipelinejobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPipelineJobsRequest -->

# Class ListPipelineJobsRequest (1.134.0)

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the PipelineJobs that match the filter expression. The following fields are supported: - `pipeline_name` : Supports `=` and `!=` comparisons.
- `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `pipeline_job_user_id` : Supports `=` , `!=`
comparisons, and `:` wildcard. for example, can check if
pipeline's display_name contains *step* by doing
display_name:"*step*"
- `state` : Supports `=` and `!=` comparisons.
- `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `end_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
- `template_uri` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `template_metadata.version` : Supports `=` , `!=`
comparisons, and `:` wildcard.
Filter expressions can be combined together using logical
operators (`AND` & `OR` ). For example:
`pipeline_name="test" AND create_time>"2020-05-18T13:30:00Z"` .
The syntax to define filter expression is based on
https://google.aip.dev/160.
Examples:
- `create_time>"2021-05-18T00:00:00Z" OR update_time>"2020-05-18T00:00:00Z"`
PipelineJobs created or updated after 2020-05-18 00:00:00
UTC.
- `labels.env = "prod"` PipelineJobs with label "env" set
to "prod".
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListPipelineJobsResponse.next_page_token of the previous PipelineService.ListPipelineJobs call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided e.g. "create_time desc, end_time", "end_time, start_time, update_time" For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple jobs having the same create time, order them by the end time in ascending order. if order_by is not specified, it will order by default order is create time in descending order. Supported fields: - `create_time`
- `update_time`
- `end_time`
- `start_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListPipelineJobsRequest

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformtextdataset.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.TextDataset -->

# Class TextDataset (1.134.0)

```
TextDataset(
dataset_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


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

### TextDataset

```
TextDataset(
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
) -> google.cloud.aiplatform.datasets.text_dataset.TextDataset
```


Creates a new text dataset.

Optionally imports data into this dataset when a source and
`import_schema_uri`

are passed in. The following is an example of how
this method is used:

```
ds = aiplatform.TextDataset.create(
display_name='my-dataset',
gcs_source='gs://my-bucket/dataset.csv',
import_schema_uri=aiplatform.schema.dataset.ioformat.text.multi_label_classification
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
Optional. The URI to one or more Google Cloud Storage buckets that contain your datasets. For example, |
`import_schema_uri` |
`str`
Optional. A URI for a YAML file stored in Cloud Storage that describes the import schema used to validate the dataset. The schema is an |
`data_item_labels` |
`Dict`
Optional. A dictionary of label information. Each dictionary item contains a label and a label key. Each item in the dataset includes one dictionary of label information. If a data item is added or merged into a dataset, and that data item contains an image that's identical to an image that’s already in the dataset, then the data items are merged. If two identical labels are detected during the merge, each with a different label key, then one of the label and label key dictionary items is randomly chosen to be into the merged data item. Data items are compared using their binary data (bytes), not on their content. If annotation labels are referenced in a schema specified by the |
`project` |
`str`
Optional. The name of the Google Cloud project to which this |
`location` |
`str`
Optional. The Google Cloud region where this dataset is uploaded. This region overrides the region that was set by |
`credentials` |
`auth_credentials.Credentials`
Optional. The credentials that are used to upload the |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings that contain metadata that's sent with the request. |
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
`text_dataset (TextDataset)` |
An instantiated representation of the managed `TextDataset` resource. |

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicemetadataserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient -->

# Class MetadataServiceClient (1.134.0)

```
MetadataServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Service for reading and writing metadata entries.

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
`MetadataServiceTransport` |
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

### MetadataServiceClient

```
MetadataServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.metadata_service.transports.base.MetadataServiceTransport,
],
]
] = None,
client_options: typing.Optional[
typing.Union[google.api_core.client_options.ClientOptions, dict]
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the metadata service client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,MetadataServiceTransport,Callable[..., MetadataServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport. If a Callable is given, it will be called with the same set of initialization arguments as used in the MetadataServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### add_context_artifacts_and_executions

```
add_context_artifacts_and_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddContextArtifactsAndExecutionsRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
artifacts: typing.Optional[typing.MutableSequence[str]] = None,
executions: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1.types.metadata_service.AddContextArtifactsAndExecutionsResponse
)
```


Adds a set of Artifacts and Executions to a Context. If any of the Artifacts or Executions have already been added to a Context, they are simply skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_add_context_artifacts_and_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddContextArtifactsAndExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextArtifactsAndExecutionsRequest.html)(
context="context_value",
)
# Make the request
response = client.[add_context_artifacts_and_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_add_context_artifacts_and_executions)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.AddContextArtifactsAndExecutions. |
`context` |
`str`
Required. The resource name of the Context that the Artifacts and Executions belong to. Format: |
`artifacts` |
`MutableSequence[str]`
The resource names of the Artifacts to attribute to the Context. Format: |
`executions` |
`MutableSequence[str]`
The resource names of the Executions to associate with the Context. Format: |
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
Response message for MetadataService.AddContextArtifactsAndExecutions. |

### add_context_children

```
add_context_children(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddContextChildrenRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
child_contexts: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.AddContextChildrenResponse
```


Adds a set of Contexts as children to a parent Context. If any of the child Contexts have already been added to the parent Context, they are simply skipped. If this call would create a cycle or cause any Context to have more than 10 parents, the request will fail with an INVALID_ARGUMENT error.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_add_context_children():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddContextChildrenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddContextChildrenRequest.html)(
context="context_value",
)
# Make the request
response = client.[add_context_children](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_add_context_children)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.AddContextChildren. |
`context` |
`str`
Required. The resource name of the parent Context. Format: |
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. This corresponds to the |
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
Response message for MetadataService.AddContextChildren. |

### add_execution_events

```
add_execution_events(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.AddExecutionEventsRequest,
dict,
]
] = None,
*,
execution: typing.Optional[str] = None,
events: typing.Optional[
typing.MutableSequence[google.cloud.aiplatform_v1.types.event.Event]
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.AddExecutionEventsResponse
```


Adds Events to the specified Execution. An Event indicates whether an Artifact was used as an input or output for an Execution. If an Event already exists between the Execution and the Artifact, the Event is skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_add_execution_events():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[AddExecutionEventsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AddExecutionEventsRequest.html)(
execution="execution_value",
)
# Make the request
response = client.[add_execution_events](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_add_execution_events)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.AddExecutionEvents. |
`execution` |
`str`
Required. The resource name of the Execution that the Events connect Artifacts with. Format: |
`events` |
`MutableSequence[`
The Events to create and add. This corresponds to the |
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
Response message for MetadataService.AddExecutionEvents. |

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

### create_artifact

```
create_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateArtifactRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
artifact: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact
] = None,
artifact_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Creates an Artifact associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateArtifactRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_create_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.CreateArtifact. |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Artifact should be created. Format: |
`artifact` |
Required. The Artifact to create. This corresponds to the |
`artifact_id` |
`str`
The {artifact} portion of the resource name with the format: |
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
Instance of a general artifact. |

### create_context

```
create_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateContextRequest, dict
]
] = None,
*,
parent: typing.Optional[str] = None,
context: typing.Optional[google.cloud.aiplatform_v1.types.context.Context] = None,
context_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.context.Context
```


Creates a Context associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateContextRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_create_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.CreateContext. |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Context should be created. Format: |
`context` |
Required. The Context to create. This corresponds to the |
`context_id` |
`str`
The {context} portion of the resource name with the format: |
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
Instance of a general context. |

### create_execution

```
create_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateExecutionRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
execution: typing.Optional[
google.cloud.aiplatform_v1.types.execution.Execution
] = None,
execution_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Creates an Execution associated with a MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateExecutionRequest.html)(
parent="parent_value",
)
# Make the request
response = client.[create_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_create_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.CreateExecution. |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Execution should be created. Format: |
`execution` |
Required. The Execution to create. This corresponds to the |
`execution_id` |
`str`
The {execution} portion of the resource name with the format: |
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
Instance of a general execution. |

### create_metadata_schema

```
create_metadata_schema(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateMetadataSchemaRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
metadata_schema: typing.Optional[
google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
] = None,
metadata_schema_id: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
```


Creates a MetadataSchema.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_metadata_schema():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
metadata_schema = aiplatform_v1.[MetadataSchema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataSchema.html)()
metadata_schema.schema = "schema_value"
request = aiplatform_v1.[CreateMetadataSchemaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataSchemaRequest.html)(
parent="parent_value",
metadata_schema=metadata_schema,
)
# Make the request
response = client.[create_metadata_schema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_create_metadata_schema)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.CreateMetadataSchema. |
`parent` |
`str`
Required. The resource name of the MetadataStore where the MetadataSchema should be created. Format: |
`metadata_schema` |
Required. The MetadataSchema to create. This corresponds to the |
`metadata_schema_id` |
`str`
The {metadata_schema} portion of the resource name with the format: |
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
Instance of a general MetadataSchema. |

### create_metadata_store

```
create_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.CreateMetadataStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
metadata_store: typing.Optional[
google.cloud.aiplatform_v1.types.metadata_store.MetadataStore
] = None,
metadata_store_id: typing.Optional[str] = None,
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


Initializes a MetadataStore, including allocation of resources.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_create_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateMetadataStoreRequest.html)(
parent="parent_value",
)
# Make the request
operation = client.[create_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_create_metadata_store)(request=request)
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
The request object. Request message for MetadataService.CreateMetadataStore. |
`parent` |
`str`
Required. The resource name of the Location where the MetadataStore should be created. Format: |
`metadata_store` |
Required. The MetadataStore to create. This corresponds to the |
`metadata_store_id` |
`str`
The {metadatastore} portion of the resource name with the format: |
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

### delete_artifact

```
delete_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteArtifactRequest,
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


Deletes an Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteArtifactRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_delete_artifact)(request=request)
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
The request object. Request message for MetadataService.DeleteArtifact. |
`name` |
`str`
Required. The resource name of the Artifact to delete. Format: |
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

### delete_context

```
delete_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteContextRequest, dict
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


Deletes a stored Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteContextRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_delete_context)(request=request)
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
The request object. Request message for MetadataService.DeleteContext. |
`name` |
`str`
Required. The resource name of the Context to delete. Format: |
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

### delete_execution

```
delete_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteExecutionRequest,
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


Deletes an Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteExecutionRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_delete_execution)(request=request)
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
The request object. Request message for MetadataService.DeleteExecution. |
`name` |
`str`
Required. The resource name of the Execution to delete. Format: |
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

### delete_metadata_store

```
delete_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.DeleteMetadataStoreRequest,
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


Deletes a single MetadataStore and all its child resources (Artifacts, Executions, and Contexts).

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_delete_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteMetadataStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_delete_metadata_store)(request=request)
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
The request object. Request message for MetadataService.DeleteMetadataStore. |
`name` |
`str`
Required. The resource name of the MetadataStore to delete. Format: |
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
`MetadataServiceClient` |
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
`MetadataServiceClient` |
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
`MetadataServiceClient` |
The constructed client. |

### get_artifact

```
get_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetArtifactRequest, dict
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
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Retrieves a specific Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetArtifactRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_get_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.GetArtifact. |
`name` |
`str`
Required. The resource name of the Artifact to retrieve. Format: |
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
Instance of a general artifact. |

### get_context

```
get_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetContextRequest, dict
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
) -> google.cloud.aiplatform_v1.types.context.Context
```


Retrieves a specific Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetContextRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_get_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.GetContext. |
`name` |
`str`
Required. The resource name of the Context to retrieve. Format: |
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
Instance of a general context. |

### get_execution

```
get_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetExecutionRequest, dict
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
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Retrieves a specific Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetExecutionRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_get_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.GetExecution. |
`name` |
`str`
Required. The resource name of the Execution to retrieve. Format: |
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
Instance of a general execution. |

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

### get_metadata_schema

```
get_metadata_schema(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetMetadataSchemaRequest,
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
) -> google.cloud.aiplatform_v1.types.metadata_schema.MetadataSchema
```


Retrieves a specific MetadataSchema.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_metadata_schema():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetMetadataSchemaRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetMetadataSchemaRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_metadata_schema](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_get_metadata_schema)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.GetMetadataSchema. |
`name` |
`str`
Required. The resource name of the MetadataSchema to retrieve. Format: |
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
Instance of a general MetadataSchema. |

### get_metadata_store

```
get_metadata_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.GetMetadataStoreRequest,
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
) -> google.cloud.aiplatform_v1.types.metadata_store.MetadataStore
```


Retrieves a specific MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_get_metadata_store():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetMetadataStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetMetadataStoreRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_metadata_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_get_metadata_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.GetMetadataStore. |
`name` |
`str`
Required. The resource name of the MetadataStore to retrieve. Format: |
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
Instance of a metadata store. Contains a set of metadata that can be queried. |

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

### list_artifacts

```
list_artifacts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListArtifactsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsPager
```


Lists Artifacts in the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_artifacts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListArtifactsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListArtifactsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_artifacts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_list_artifacts)(request=request)
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
The request object. Request message for MetadataService.ListArtifacts. |
`parent` |
`str`
Required. The MetadataStore whose Artifacts should be listed. Format: |
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
Response message for MetadataService.ListArtifacts. Iterating over this object will yield results and resolve additional pages automatically. |

### list_contexts

```
list_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListContextsRequest, dict
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
) -> google.cloud.aiplatform_v1.services.metadata_service.pagers.ListContextsPager
```


Lists Contexts on the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_contexts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListContextsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_list_contexts)(request=request)
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
The request object. Request message for MetadataService.ListContexts |
`parent` |
`str`
Required. The MetadataStore whose Contexts should be listed. Format: |
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
Response message for MetadataService.ListContexts. Iterating over this object will yield results and resolve additional pages automatically. |

### list_executions

```
list_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListExecutionsRequest,
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
) -> google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsPager
```


Lists Executions in the MetadataStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListExecutionsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_list_executions)(request=request)
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
The request object. Request message for MetadataService.ListExecutions. |
`parent` |
`str`
Required. The MetadataStore whose Executions should be listed. Format: |
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
Response message for MetadataService.ListExecutions. Iterating over this object will yield results and resolve additional pages automatically. |

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

### list_metadata_schemas

```
list_metadata_schemas(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataSchemasRequest,
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
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasPager
)
```


Lists MetadataSchemas.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_metadata_schemas():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListMetadataSchemasRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataSchemasRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_metadata_schemas](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_list_metadata_schemas)(request=request)
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
The request object. Request message for MetadataService.ListMetadataSchemas. |
`parent` |
`str`
Required. The MetadataStore whose MetadataSchemas should be listed. Format: |
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
Response message for MetadataService.ListMetadataSchemas. Iterating over this object will yield results and resolve additional pages automatically. |

### list_metadata_stores

```
list_metadata_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.ListMetadataStoresRequest,
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
google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresPager
)
```


Lists MetadataStores for a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_list_metadata_stores():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListMetadataStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListMetadataStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_metadata_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_list_metadata_stores)(request=request)
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
The request object. Request message for MetadataService.ListMetadataStores. |
`parent` |
`str`
Required. The Location whose MetadataStores should be listed. Format: |
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
Response message for MetadataService.ListMetadataStores. Iterating over this object will yield results and resolve additional pages automatically. |

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

### metadata_schema_path

```
metadata_schema_path(
project: str, location: str, metadata_store: str, metadata_schema: str
) -> str
```


Returns a fully-qualified metadata_schema string.

### metadata_store_path

`metadata_store_path(project: str, location: str, metadata_store: str) -> str`


Returns a fully-qualified metadata_store string.

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

### parse_execution_path

`parse_execution_path(path: str) -> typing.Dict[str, str]`


Parses a execution path into its component segments.

### parse_metadata_schema_path

`parse_metadata_schema_path(path: str) -> typing.Dict[str, str]`


Parses a metadata_schema path into its component segments.

### parse_metadata_store_path

`parse_metadata_store_path(path: str) -> typing.Dict[str, str]`


Parses a metadata_store path into its component segments.

### purge_artifacts

```
purge_artifacts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeArtifactsRequest,
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
) -> google.api_core.operation.Operation
```


Purges Artifacts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_purge_artifacts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeArtifactsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeArtifactsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_artifacts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_purge_artifacts)(request=request)
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
The request object. Request message for MetadataService.PurgeArtifacts. |
`parent` |
`str`
Required. The metadata store to purge Artifacts from. Format: |
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

### purge_contexts

```
purge_contexts(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeContextsRequest, dict
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
) -> google.api_core.operation.Operation
```


Purges Contexts.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_purge_contexts():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeContextsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeContextsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_contexts](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_purge_contexts)(request=request)
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
The request object. Request message for MetadataService.PurgeContexts. |
`parent` |
`str`
Required. The metadata store to purge Contexts from. Format: |
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

### purge_executions

```
purge_executions(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.PurgeExecutionsRequest,
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
) -> google.api_core.operation.Operation
```


Purges Executions.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_purge_executions():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[PurgeExecutionsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PurgeExecutionsRequest.html)(
parent="parent_value",
filter="filter_value",
)
# Make the request
operation = client.[purge_executions](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_purge_executions)(request=request)
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
The request object. Request message for MetadataService.PurgeExecutions. |
`parent` |
`str`
Required. The metadata store to purge Executions from. Format: |
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

### query_artifact_lineage_subgraph

```
query_artifact_lineage_subgraph(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryArtifactLineageSubgraphRequest,
dict,
]
] = None,
*,
artifact: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_query_artifact_lineage_subgraph():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryArtifactLineageSubgraphRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryArtifactLineageSubgraphRequest.html)(
artifact="artifact_value",
)
# Make the request
response = client.[query_artifact_lineage_subgraph](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_query_artifact_lineage_subgraph)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.QueryArtifactLineageSubgraph. |
`artifact` |
`str`
Required. The resource name of the Artifact whose Lineage needs to be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### query_context_lineage_subgraph

```
query_context_lineage_subgraph(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryContextLineageSubgraphRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_query_context_lineage_subgraph():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryContextLineageSubgraphRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryContextLineageSubgraphRequest.html)(
context="context_value",
)
# Make the request
response = client.[query_context_lineage_subgraph](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_query_context_lineage_subgraph)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.QueryContextLineageSubgraph. |
`context` |
`str`
Required. The resource name of the Context whose Artifacts and Executions should be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### query_execution_inputs_and_outputs

```
query_execution_inputs_and_outputs(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.QueryExecutionInputsAndOutputsRequest,
dict,
]
] = None,
*,
execution: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.lineage_subgraph.LineageSubgraph
```


Obtains the set of input and output Artifacts for this Execution, in the form of LineageSubgraph that also contains the Execution and connecting Events.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_query_execution_inputs_and_outputs():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[QueryExecutionInputsAndOutputsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryExecutionInputsAndOutputsRequest.html)(
execution="execution_value",
)
# Make the request
response = client.[query_execution_inputs_and_outputs](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_query_execution_inputs_and_outputs)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.QueryExecutionInputsAndOutputs. |
`execution` |
`str`
Required. The resource name of the Execution whose input and output Artifacts should be retrieved as a LineageSubgraph. Format: |
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
A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes. |

### remove_context_children

```
remove_context_children(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.RemoveContextChildrenRequest,
dict,
]
] = None,
*,
context: typing.Optional[str] = None,
child_contexts: typing.Optional[typing.MutableSequence[str]] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.metadata_service.RemoveContextChildrenResponse
```


Remove a set of children contexts from a parent Context. If any of the child Contexts were NOT added to the parent Context, they are simply skipped.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_remove_context_children():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[RemoveContextChildrenRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RemoveContextChildrenRequest.html)(
context="context_value",
)
# Make the request
response = client.[remove_context_children](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_remove_context_children)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for [MetadataService.DeleteContextChildrenRequest][]. |
`context` |
`str`
Required. The resource name of the parent Context. Format: |
`child_contexts` |
`MutableSequence[str]`
The resource names of the child Contexts. This corresponds to the |
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
Response message for MetadataService.RemoveContextChildren. |

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

### update_artifact

```
update_artifact(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateArtifactRequest,
dict,
]
] = None,
*,
artifact: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact
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
) -> google.cloud.aiplatform_v1.types.artifact.Artifact
```


Updates a stored Artifact.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_artifact():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateArtifactRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateArtifactRequest.html)(
)
# Make the request
response = client.[update_artifact](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_update_artifact)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.UpdateArtifact. |
`artifact` |
Required. The Artifact containing updates. The Artifact's Artifact.name field is used to identify the Artifact to be updated. Format: |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general artifact. |

### update_context

```
update_context(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateContextRequest, dict
]
] = None,
*,
context: typing.Optional[google.cloud.aiplatform_v1.types.context.Context] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1.types.context.Context
```


Updates a stored Context.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_context():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateContextRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateContextRequest.html)(
)
# Make the request
response = client.[update_context](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_update_context)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.UpdateContext. |
`context` |
Required. The Context containing updates. The Context's Context.name field is used to identify the Context to be updated. Format: |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general context. |

### update_execution

```
update_execution(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1.types.metadata_service.UpdateExecutionRequest,
dict,
]
] = None,
*,
execution: typing.Optional[
google.cloud.aiplatform_v1.types.execution.Execution
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
) -> google.cloud.aiplatform_v1.types.execution.Execution
```


Updates a stored Execution.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1
def sample_update_execution():
# Create a client
client = aiplatform_v1.
```[MetadataServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateExecutionRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExecutionRequest.html)(
)
# Make the request
response = client.[update_execution](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.MetadataServiceClient.html#google_cloud_aiplatform_v1_services_metadata_service_MetadataServiceClient_update_execution)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Union[`
The request object. Request message for MetadataService.UpdateExecution. |
`execution` |
Required. The Execution containing updates. The Execution's Execution.name field is used to identify the Execution to be updated. Format: |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. A FieldMask indicating which fields should be updated. This corresponds to the |
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
Instance of a general execution. |

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

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatf_92c32c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatfo_b64878.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatfor_5607e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatform_c9b49f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatform__bec7f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfilemetadataconfig_googlecloudaiplatform_v_45fdbd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfilemetadataconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFileMetadataConfig -->

# Class RagFileMetadataConfig (1.134.0)

`RagFileMetadataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata config for RagFile.

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
`gcs_metadata_schema_source` |
Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucket_name/my_directory/object_name/metadata_schema.json`
- `gs://bucket_name/my_directory` If the user provides a
directory, the metadata schema will be read from the files
that ends with "metadata_schema.json" in the directory.
This field is a member of `oneof` _ `metadata_schema_source` .
|
`google_drive_metadata_schema_source` |
Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a folder, the metadata schema will be read from the files that ends with "metadata_schema.json" in the directory. This field is a member of `oneof` _ `metadata_schema_source` .
|
`inline_metadata_schema_source` |
`str`
Inline metadata schema source. Must be a JSON string. This field is a member of `oneof` _ `metadata_schema_source` .
|
`gcs_metadata_source` |
Google Cloud Storage location. Supports importing individual files as well as entire Google Cloud Storage directories. Sample formats: - `gs://bucket_name/my_directory/object_name/metadata.json`
- `gs://bucket_name/my_directory` If the user provides a
directory, the metadata will be read from the files that
ends with "metadata.json" in the directory.
This field is a member of `oneof` _ `metadata_source` .
|
`google_drive_metadata_source` |
Google Drive location. Supports importing individual files as well as Google Drive folders. If the user provides a directory, the metadata will be read from the files that ends with "metadata.json" in the directory. This field is a member of `oneof` _ `metadata_source` .
|
`inline_metadata_source` |
`str`
Inline metadata source. Must be a JSON string. This field is a member of `oneof` _ `metadata_source` .
|

## Methods

### RagFileMetadataConfig

`RagFileMetadataConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata config for RagFile.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestrial.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Trial -->

# Class Trial (1.134.0)

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Trial assigned by the service. |
`id` |
`str`
Output only. The identifier of the Trial assigned by the service. |
`state` |
Output only. The detailed state of the Trial. |
`parameters` |
`MutableSequence[`
Output only. The parameters of the Trial. |
`final_measurement` |
Output only. The final measurement containing the objective value. |
`measurements` |
`MutableSequence[`
Output only. A list of measurements that are strictly lexicographically ordered by their induced tuples (steps, elapsed_duration). These are used for early stopping computations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial's status changed to `SUCCEEDED` or `INFEASIBLE` .
|
`client_id` |
`str`
Output only. The identifier of the client that originally requested this Trial. Each client is identified by a unique client_id. When a client asks for a suggestion, Vertex AI Vizier will assign it a Trial. The client should evaluate the Trial, complete it, and report back to Vertex AI Vizier. If suggestion is asked again by same client_id before the Trial is completed, the same Trial will be returned. Multiple clients with different client_ids can ask for suggestions simultaneously, each of them will get their own Trial. |
`infeasible_reason` |
`str`
Output only. A human readable string describing why the Trial is infeasible. This is set only if Trial state is `INFEASIBLE` .
|
`custom_job` |
`str`
Output only. The CustomJob name linked to the Trial. It's set for a HyperparameterTuningJob's Trial. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |

## Classes

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

### State

`State(value)`


Describes a Trial state.

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

### Trial

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescometinstance__googlecloudaiplatform_v1beta1_c005b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescometinstance__googlecloudaiplatform_v1beta1t_f8c296.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescometinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CometInstance -->

# Class CometInstance (1.134.0)

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

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
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### CometInstance

`CometInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesundeploymodelresponse_googlecloudaiplatform_v_70542a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesundeploymodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UndeployModelResponse -->

# Class UndeployModelResponse (1.134.0)

`UndeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.UndeployModel.

## Methods

### UndeployModelResponse

`UndeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.UndeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessafetyspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SafetySpec -->

# Class SafetySpec (1.134.0)

`SafetySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety metric.

## Attribute |
|
|---|---|
Name |
Description |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SafetySpec

`SafetySpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for safety metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typeslistpipelinejobsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPipelineJobsRequest -->

# Class ListPipelineJobsRequest (1.134.0)

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list the PipelineJobs from. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Lists the PipelineJobs that match the filter expression. The following fields are supported: - `pipeline_name` : Supports `=` and `!=` comparisons.
- `display_name` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `pipeline_job_user_id` : Supports `=` , `!=`
comparisons, and `:` wildcard. for example, can check if
pipeline's display_name contains *step* by doing
display_name:"*step*"
- `state` : Supports `=` and `!=` comparisons.
- `create_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `update_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `end_time` : Supports `=` , `!=` , , `>` ,
`<>` , and `>=` comparisons. Values must be in RFC 3339
format.
- `labels` : Supports key-value equality and key presence.
- `template_uri` : Supports `=` , `!=` comparisons, and
`:` wildcard.
- `template_metadata.version` : Supports `=` , `!=`
comparisons, and `:` wildcard.
Filter expressions can be combined together using logical
operators (`AND` & `OR` ). For example:
`pipeline_name="test" AND create_time>"2020-05-18T13:30:00Z"` .
The syntax to define filter expression is based on
https://google.aip.dev/160.
Examples:
- `create_time>"2021-05-18T00:00:00Z" OR update_time>"2020-05-18T00:00:00Z"`
PipelineJobs created or updated after 2020-05-18 00:00:00
UTC.
- `labels.env = "prod"` PipelineJobs with label "env" set
to "prod".
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListPipelineJobsResponse.next_page_token of the previous PipelineService.ListPipelineJobs call. |
`order_by` |
`str`
A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple order_by fields provided e.g. "create_time desc, end_time", "end_time, start_time, update_time" For example, using "create_time desc, end_time" will order results by create time in descending order, and if there are multiple jobs having the same create time, order them by the end time in ascending order. if order_by is not specified, it will order by default order is create time in descending order. Supported fields: - `create_time`
- `update_time`
- `end_time`
- `start_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListPipelineJobsRequest

`ListPipelineJobsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PipelineService.ListPipelineJobs.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesragfile_googlecloudaiplatform_v1beta1service_2e0c12.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesragfile_googlecloudaiplatform_v1beta1services_400b62.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesragfile.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagFile -->

# Class RagFile (1.134.0)

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

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
Output only. Google Cloud Storage location of the RagFile. It does not support wildcards in the Cloud Storage uri for now. This field is a member of `oneof` _ `rag_file_source` .
|
`google_drive_source` |
Output only. Google Drive location. Supports importing individual files as well as Google Drive folders. This field is a member of `oneof` _ `rag_file_source` .
|
`direct_upload_source` |
Output only. The RagFile is encapsulated and uploaded in the UploadRagFile request. This field is a member of `oneof` _ `rag_file_source` .
|
`slack_source` |
The RagFile is imported from a Slack channel. This field is a member of `oneof` _ `rag_file_source` .
|
`jira_source` |
The RagFile is imported from a Jira query. This field is a member of `oneof` _ `rag_file_source` .
|
`share_point_sources` |
The RagFile is imported from a SharePoint source. This field is a member of `oneof` _ `rag_file_source` .
|
`name` |
`str`
Output only. The resource name of the RagFile. |
`display_name` |
`str`
Required. The display name of the RagFile. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the RagFile. |
`size_bytes` |
`int`
Output only. The size of the RagFile in bytes. |
`rag_file_type` |
Output only. The type of the RagFile. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this RagFile was last updated. |
`file_status` |
Output only. State of the RagFile. |
`user_metadata` |
`str`
Output only. The metadata for metadata search. The user_metadata Needs to be in JSON format. |

## Classes

### RagFileType

`RagFileType(value)`


The type of the RagFile.

## Methods

### RagFile

`RagFile(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagFile contains user data for chunking, embedding and indexing.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesreasoning_engine_servicepagerslistreasoningenginesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager -->

# Class ListReasoningEnginesAsyncPager (1.134.0)

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse) object, and
provides an `__aiter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListReasoningEnginesAsyncPager

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1beta1.types.reasoning_engine_service.ListReasoningEnginesResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfi_1eeda2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfie_55dfb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequestconnectorconfigdatapointfieldmapping.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping -->

# Class DatapointFieldMapping (1.134.0)

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.

## Attributes |
|
|---|---|
Name |
Description |
`id_column` |
`str`
Required. The column with unique identifiers for each data point. |
`embedding_column` |
`str`
Required. The column with the vector embeddings for each data point. |
`restricts` |
`MutableSequence[`
Optional. List of restricts for string values. |
`numeric_restricts` |
`MutableSequence[`
Optional. List of restricts for numeric values. |
`metadata_columns` |
`MutableSequence[str]`
Optional. List of columns containing metadata to be included in the index. |

## Classes

### NumericRestrict

`NumericRestrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on numeric values.

### Restrict

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

## Methods

### DatapointFieldMapping

`DatapointFieldMapping(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Mapping of datapoint fields to column names for columnar data sources.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolgooglesearch.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Tool.GoogleSearch -->

# Class GoogleSearch (1.134.0)

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`exclude_domains` |
`MutableSequence[str]`
Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: ["amazon.com", "facebook.com"]. |
`blocking_confidence` |
Optional. Sites with confidence level chosen & above this value will be blocked from the search results. This field is a member of `oneof` _ `_blocking_confidence` .
|

## Methods

### GoogleSearch

`GoogleSearch(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_registry_servicepagerslistfeaturemonitorsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsAsyncPager -->

# Class ListFeatureMonitorsAsyncPager (1.134.0)

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

## Methods

### ListFeatureMonitorsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicespersistent_resource_servicepagerslistper_df7cd4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicespersistent_resource_servicepagerslistpers_774769.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicespersistent_resource_servicepagerslistpersi_ef6f74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicespersistent_resource_servicepagerslistpersistentresourcespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesPager -->

# Class ListPersistentResourcesPager (1.134.0)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse) object, and
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

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPersistentResourcesPager

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardexperimentspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager -->

# Class ListTensorboardExperimentsPager (1.134.0)

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsPager

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistfeaturesrequest_googlecloudaiplatform_v1b_4a5bf1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistfeaturesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturesRequest -->

# Class ListFeaturesRequest (1.134.0)

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to list Features. Format for entity_type as parent: `projects/{project}/locations/{location}/featurestores/{featurestore}/entityTypes/{entity_type}`
Format for feature_group as parent:
`projects/{project}/locations/{location}/featureGroups/{feature_group}`
|
`filter` |
`str`
Lists the Features that match the filter expression. The following filters are supported: - `value_type` : Supports = and != comparisons.
- `create_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`update_time` : Supports =, !=, <,>, >=, and <= comparisons.="" values="" must="" be="" in="" rfc="" 3339="" format.="" -="">`labels` : Supports key-value equality as well as key
presence.
Examples:
- `value_type = DOUBLE` --> Features whose type is DOUBLE.
- `create_time > \"2020-01-31T15:30:00.000000Z\" OR update_time > \"2020-01-31T15:30:00.000000Z\"`
--> EntityTypes created or updated after
2020-01-31T15:30:00.000000Z.
- `labels.active = yes AND labels.env = prod` --> Features
having both (active: yes) and (env: prod) labels.
- `labels.env: *` --> Any Feature which has a label with
'env' as the key.
|
`page_size` |
`int`
The maximum number of Features to return. The service may return fewer than this value. If unspecified, at most 1000 Features will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous FeaturestoreService.ListFeatures call or FeatureRegistryService.ListFeatures call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to FeaturestoreService.ListFeatures or FeatureRegistryService.ListFeatures must match the call that provided the page token. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `feature_id`
- `value_type` (Not supported for FeatureRegistry Feature)
- `create_time`
- `update_time`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`latest_stats_count` |
`int`
Only applicable for Vertex AI Feature Store (Legacy). If set, return the most recent ListFeaturesRequest.latest_stats_count of stats for each Feature in response. Valid value is [0, 10]. If number of stats exists <>ListFeaturesRequest.latest_stats_count, return all existing stats. |

## Methods

### ListFeaturesRequest

`ListFeaturesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.ListFeatures. Request message for FeatureRegistryService.ListFeatures.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_monitoring_servicepagerssearchmodelmonitoringstatspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.SearchModelMonitoringStatsPager -->

# Class SearchModelMonitoringStatsPager (1.134.0)

```
SearchModelMonitoringStatsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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


A pager for iterating through `search_model_monitoring_stats`

requests.

This class thinly wraps an initial
[SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse) object, and
provides an `__iter__`

method to iterate through its
`monitoring_stats`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchModelMonitoringStats`

requests and continue to iterate
through the `monitoring_stats`

field on the
corresponding responses.

All the usual [SearchModelMonitoringStatsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchModelMonitoringStatsPager

```
SearchModelMonitoringStatsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.SearchModelMonitoringStatsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagers___googleclou_858fb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatefeaturestorerequest_googlecloudaiplatf_465be7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatefeaturestorerequest_googlecloudaiplatfo_19dc32.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatefeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeaturestoreRequest -->

# Class UpdateFeaturestoreRequest (1.134.0)

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`featurestore` |
Required. The Featurestore's `name` field is used to
identify the Featurestore to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `online_serving_config.fixed_node_count`
- `online_serving_config.scaling`
- `online_storage_ttl_days`
|

## Methods

### UpdateFeaturestoreRequest

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebooksoftwareconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookSoftwareConfig -->

# Class NotebookSoftwareConfig (1.134.0)

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`colab_image` |
Optional. Google-managed NotebookRuntime colab image. This field is a member of `oneof` _ `runtime_image` .
|
`env` |
`MutableSequence[`
Optional. Environment variables to be passed to the container. Maximum limit is 100. |
`post_startup_script_config` |
Optional. Post-startup script config. |

## Methods

### NotebookSoftwareConfig

`NotebookSoftwareConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Notebook Software Config. This is passed to the backend when user makes software configurations in UI.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmetricxinstance_googlecloudaiplatform_v1beta1_f32b91.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmetricxinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetricxInstance -->

# Class MetricxInstance (1.134.0)

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

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
Optional. Ground truth used to compare against the prediction. This field is a member of `oneof` _ `_reference` .
|
`source` |
`str`
Optional. Source text in original language. This field is a member of `oneof` _ `_source` .
|

## Methods

### MetricxInstance

`MetricxInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistsessionsrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsRequest -->

# Class ListSessionsRequest (1.134.0)

`ListSessionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListSessions.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the location to list sessions from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`page_size` |
`int`
Optional. The maximum number of sessions to return. The service may return fewer than this value. If unspecified, at most 100 sessions will be returned. |
`page_token` |
`str`
Optional. The next_page_token value returned from a previous list SessionService.ListSessions call. |
`filter` |
`str`
Optional. The standard list filter. Supported fields: \* `display_name` \* `user_id`
Example: `display_name="abc"` , `user_id="123"` .
|
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
- `update_time`
Example: `create_time desc` .
|

## Methods

### ListSessionsRequest

`ListSessionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.ListSessions.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmatch_servicematchserviceasyncclient_____g_a5fe4d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmatch_servicematchserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient -->

# Class MatchServiceAsyncClient (1.134.0)

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
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

### MatchServiceAsyncClient

```
MatchServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the match service async client.

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
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the MatchServiceTransport constructor. If set to None, a transport is chosen automatically. |
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

### find_neighbors

```
find_neighbors(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.FindNeighborsResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_find_neighbors():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FindNeighborsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FindNeighborsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[find_neighbors](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceAsyncClient_find_neighbors)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.FindNeighbors. |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
`MatchServiceAsyncClient` |
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
google.cloud.aiplatform_v1beta1.services.match_service.transports.base.MatchServiceTransport
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

### read_index_datapoints

```
read_index_datapoints(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsRequest,
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
) -> google.cloud.aiplatform_v1beta1.types.match_service.ReadIndexDatapointsResponse
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
from google.cloud import aiplatform_v1beta1
async def sample_read_index_datapoints():
# Create a client
client = aiplatform_v1beta1.
```[MatchServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ReadIndexDatapointsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReadIndexDatapointsRequest.html)(
index_endpoint="index_endpoint_value",
)
# Make the request
response = await client.[read_index_datapoints](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.match_service.MatchServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_match_service_MatchServiceAsyncClient_read_index_datapoints)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. The request message for MatchService.ReadIndexDatapoints. |
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
The response message for MatchService.ReadIndexDatapoints. |

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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesmodelmonitoringconfig_googlecloudaiplatfor_7ccf85.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesmodelmonitoringconfig_googlecloudaiplatform_40b662.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringconfig_googlecloudaiplatform__56b035.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringconfig_googlecloudaiplatform_v_0a94e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringConfig -->

# Class ModelMonitoringConfig (1.134.0)

`ModelMonitoringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model monitoring configuration used for Batch Prediction Job.

## Attributes |
|
|---|---|
Name |
Description |
`objective_configs` |
`MutableSequence[`
Model monitoring objective config. |
`alert_config` |
Model monitoring alert config. |
`analysis_instance_schema_uri` |
`str`
YAML schema file uri in Cloud Storage describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`stats_anomalies_base_directory` |
A Google Cloud Storage location for batch prediction model monitoring to dump statistics and anomalies. If not provided, a folder will be created in customer project to hold statistics and anomalies. |

## Methods

### ModelMonitoringConfig

`ModelMonitoringConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The model monitoring configuration used for Batch Prediction Job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryexactmatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryExactMatchInstance -->

# Class TrajectoryExactMatchInstance (1.134.0)

```
TrajectoryExactMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryExactMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryExactMatchInstance

```
TrajectoryExactMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryExactMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfeatureonlinestorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager -->

# Class ListFeatureOnlineStoresPager (1.134.0)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse) object, and
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

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureOnlineStoresPager

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmigration_servicepagerssearchmigratableresource_20da41.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmigration_servicepagerssearchmigratableresourcesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.migration_service.pagers.SearchMigratableResourcesAsyncPager -->

# Class SearchMigratableResourcesAsyncPager (1.134.0)

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

## Methods

### SearchMigratableResourcesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookexecutionjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookExecutionJobsAsyncPager -->

# Class ListNotebookExecutionJobsAsyncPager (1.134.0)

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsAsyncPager

```
ListNotebookExecutionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse
],
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookExecutionJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesupdatetensorboardtimeseriesrequest_googlecl_d99bbd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesupdatetensorboardtimeseriesrequest_googleclo_640207.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesupdatetensorboardtimeseriesrequest_googleclou_59882c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardTimeSeriesRequest -->

# Class UpdateTensorboardTimeSeriesRequest (1.134.0)

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardTimeSeries resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_time_series` |
Required. The TensorboardTimeSeries' `name` field is used
to identify the TensorboardTimeSeries to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}/timeSeries/{time_series}`
|

## Methods

### UpdateTensorboardTimeSeriesRequest

```
UpdateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.UpdateTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlimagesegmentationinputsmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlImageSegmentationInputs.ModelType -->

# Class ModelType (1.134.0)

A model to be used via prediction calls to uCAIP API. Expected to have a higher latency, but should also have a higher prediction quality than other models.

CLOUD_LOW_ACCURACY_1

A model to be used via prediction calls to uCAIP API. Expected to have a lower latency but relatively lower prediction quality.

MOBILE_TF_LOW_LATENCY_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as TensorFlow model and used on a mobile or edge device afterwards. Expected to have low latency, but may have lower prediction quality than other mobile models.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typessessionevent_googlecloudaiplatform_v1beta1typ_3b1b64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessessionevent.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SessionEvent -->

# Class SessionEvent (1.134.0)

`SessionEvent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An event represents a message from either the user or agent.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. The resource name of the event. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}/sessions/{session}/events/{event}` .
|
`author` |
`str`
Required. The name of the agent that sent the event, or user. |
`content` |
Optional. Content of the event provided by the author. |
`invocation_id` |
`str`
Required. The invocation id of the event, multiple events can have the same invocation id. |
`actions` |
Optional. Actions executed by the agent. |
`timestamp` |
`google.protobuf.timestamp_pb2.Timestamp`
Required. Timestamp when the event was created on client side. |
`error_code` |
`str`
Optional. Error code if the response is an error. Code varies by model. |
`error_message` |
`str`
Optional. Error message if the response is an error. |
`event_metadata` |
Optional. Metadata relating to this event. |

## Methods

### SessionEvent

`SessionEvent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


An event represents a message from either the user or agent.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrajectoryinordermatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchInstance -->

# Class TrajectoryInOrderMatchInstance (1.134.0)

```
TrajectoryInOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryInOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`predicted_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for predicted tool call trajectory. This field is a member of `oneof` _ `_predicted_trajectory` .
|
`reference_trajectory` |
`google.cloud.aiplatform_v1beta1.types.Trajectory`
Required. Spec for reference tool call trajectory. This field is a member of `oneof` _ `_reference_trajectory` .
|

## Methods

### TrajectoryInOrderMatchInstance

```
TrajectoryInOrderMatchInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for TrajectoryInOrderMatch instance.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeatureview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_registry_servicefeatureregistryservicec_7a89dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicefeatureregistryserviceclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient -->

# Class FeatureRegistryServiceClient (1.134.0)

```
FeatureRegistryServiceClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
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
google.cloud.aiplatform_v1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1.services.feature_registry_service.transports.base.FeatureRegistryServiceTransport,
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


Creates a batch of Features in a given FeatureGroup.

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
requests = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)()
requests.parent = "parent_value"
requests.feature_id = "feature_id_value"
request = aiplatform_v1.[BatchCreateFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateFeaturesRequest.html)(
parent="parent_value",
requests=requests,
)
# Make the request
operation = client.[batch_create_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_batch_create_features)(request=request)
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


Creates a new Feature in a given FeatureGroup.

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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[CreateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureRequest.html)(
parent="parent_value",
feature_id="feature_id_value",
)
# Make the request
operation = client.[create_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature)(request=request)
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
google.cloud.aiplatform_v1.types.feature_registry_service.CreateFeatureGroupRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
feature_group: typing.Optional[
google.cloud.aiplatform_v1.types.feature_group.FeatureGroup
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
from google.cloud import aiplatform_v1
def sample_create_feature_group():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1.FeatureGroup()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1.[CreateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateFeatureGroupRequest.html)(
parent="parent_value",
feature_group=feature_group,
feature_group_id="feature_group_id_value",
)
# Make the request
operation = client.[create_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_create_feature_group)(request=request)
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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature)(request=request)
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
google.cloud.aiplatform_v1.types.feature_registry_service.DeleteFeatureGroupRequest,
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
from google.cloud import aiplatform_v1
def sample_delete_feature_group():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[DeleteFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_delete_feature_group)(request=request)
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
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature)(request=request)
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
google.cloud.aiplatform_v1.types.feature_registry_service.GetFeatureGroupRequest,
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
) -> google.cloud.aiplatform_v1.types.feature_group.FeatureGroup
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
from google.cloud import aiplatform_v1
def sample_get_feature_group():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[GetFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureGroupRequest.html)(
name="name_value",
)
# Make the request
response = client.[get_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_get_feature_group)(request=request)
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
google.cloud.aiplatform_v1.types.feature_registry_service.ListFeatureGroupsRequest,
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
google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsPager
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
from google.cloud import aiplatform_v1
def sample_list_feature_groups():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeatureGroupsRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureGroupsRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_feature_groups](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_list_feature_groups)(request=request)
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
) -> (
google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesPager
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
from google.cloud import aiplatform_v1
def sample_list_features():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[ListFeaturesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturesRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_features](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_list_features)(request=request)
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
from google.cloud import aiplatform_v1
def sample_update_feature():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
request = aiplatform_v1.[UpdateFeatureRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureRequest.html)(
)
# Make the request
operation = client.[update_feature](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature)(request=request)
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
google.cloud.aiplatform_v1.types.feature_registry_service.UpdateFeatureGroupRequest,
dict,
]
] = None,
*,
feature_group: typing.Optional[
google.cloud.aiplatform_v1.types.feature_group.FeatureGroup
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
from google.cloud import aiplatform_v1
def sample_update_feature_group():
# Create a client
client = aiplatform_v1.
```[FeatureRegistryServiceClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html)()
# Initialize request argument(s)
feature_group = aiplatform_v1.FeatureGroup()
feature_group.big_query.big_query_source.input_uri = "input_uri_value"
request = aiplatform_v1.[UpdateFeatureGroupRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeatureGroupRequest.html)(
feature_group=feature_group,
)
# Make the request
operation = client.[update_feature_group](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.FeatureRegistryServiceClient.html#google_cloud_aiplatform_v1_services_feature_registry_service_FeatureRegistryServiceClient_update_feature_group)(request=request)
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersqueryd_7e21e3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersqueryde_a7043e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersquerydep_054f13.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersquerydepl_6b1999.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdeployment_resource_pool_servicepagersquerydeployedmodelsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager -->

# Class QueryDeployedModelsAsyncPager (1.134.0)

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsAsyncPager

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeature_online_store_admin_servicepagerslistfeatureviewsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager -->

# Class ListFeatureViewsAsyncPager (1.134.0)

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

## Methods

### ListFeatureViewsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespairwisequestionansweringqualityresult__googleclo_a18f24.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisequestionansweringqualityresult__googleclou_9ac68f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisequestionansweringqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseQuestionAnsweringQualityResult -->

# Class PairwiseQuestionAnsweringQualityResult (1.134.0)

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`pairwise_choice` |
Output only. Pairwise question answering prediction choice. |
`explanation` |
`str`
Output only. Explanation for question answering quality score. |
`confidence` |
`float`
Output only. Confidence for question answering quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### PairwiseQuestionAnsweringQualityResult

```
PairwiseQuestionAnsweringQualityResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for pairwise question answering quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesundeploymodelresponse_googlecloudaiplatform_v1type_a6959c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesundeploymodelresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UndeployModelResponse -->

# Class UndeployModelResponse (1.134.0)

`UndeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.UndeployModel.

## Methods

### UndeployModelResponse

`UndeployModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.UndeployModel.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkeymatchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKeyMatchSpec -->

# Class ToolParameterKeyMatchSpec (1.134.0)

`ToolParameterKeyMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key match metric.

## Methods

### ToolParameterKeyMatchSpec

`ToolParameterKeyMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesreasoningenginespecdeploymentspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ReasoningEngineSpec.DeploymentSpec -->

# Class DeploymentSpec (1.134.0)

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`env` |
`MutableSequence[`
Optional. Environment variables to be set with the Reasoning Engine deployment. The environment variables can be updated through the UpdateReasoningEngine API. |
`secret_env` |
`MutableSequence[`
Optional. Environment variables where the value is a secret in Cloud Secret Manager. To use this feature, add 'Secret Manager Secret Accessor' role (roles/secretmanager.secretAccessor) to AI Platform Reasoning Engine Service Agent. |
`psc_interface_config` |
Optional. Configuration for PSC-I. |
`min_instances` |
`int`
Optional. The minimum number of application instances that will be kept running at all times. Defaults to 1. Range: [0, 10]. This field is a member of `oneof` _ `_min_instances` .
|
`max_instances` |
`int`
Optional. The maximum number of application instances that can be launched to handle increased traffic. Defaults to 100. Range: [1, 1000]. If VPC-SC or PSC-I is enabled, the acceptable range is [1, 100]. This field is a member of `oneof` _ `_max_instances` .
|
`resource_limits` |
`MutableMapping[str, str]`
Optional. Resource limits for each container. Only 'cpu' and 'memory' keys are supported. Defaults to {"cpu": "4", "memory": "4Gi"}. - The only supported values for CPU are '1', '2', '4', '6' and '8'. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. - The only supported values for memory are '1Gi', '2Gi', ... '32 Gi'. - For required cpu on different memory values, go to https://cloud.google.com/run/docs/configuring/memory-limits |
`container_concurrency` |
`int`
Optional. Concurrency for each container and agent server. Recommended value: 2 \* cpu + 1. Defaults to 9. This field is a member of `oneof` _ `_container_concurrency` .
|

## Classes

### ResourceLimitsEntry

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesexplanationmetadatainputmetadata___googlecloudaipl_99bbfb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesexplanationmetadatainputmetadata.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExplanationMetadata.InputMetadata -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesragvectordbconfigragmanageddbann_googlecloudaipla_20d765.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragvectordbconfigragmanageddbann_googlecloudaiplat_614ad8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragvectordbconfigragmanageddbann.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagVectorDbConfig.RagManagedDb.ANN -->

# Class ANN (1.134.0)

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.

## Attributes |
|
|---|---|
Name |
Description |
`tree_depth` |
`int`
The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2. |
`leaf_count` |
`int`
Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

## Methods

### ANN

`ANN(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and UpdateRagCorpus API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstudyspecdecaycurveautomatedstoppingspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StudySpec.DecayCurveAutomatedStoppingSpec -->

# Class DecayCurveAutomatedStoppingSpec (1.134.0)

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.

## Attribute |
|
|---|---|
Name |
Description |
`use_elapsed_duration` |
`bool`
True if Measurement.elapsed_duration is used as the x-axis of each Trials Decay Curve. Otherwise, Measurement.step_count will be used as the x-axis. |

## Methods

### DecayCurveAutomatedStoppingSpec

```
DecayCurveAutomatedStoppingSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The decay curve automated stopping rule builds a Gaussian Process Regressor to predict the final objective value of a Trial based on the already completed Trials and the intermediate measurements of the current Trial. Early stopping is requested for the current Trial if there is very low probability to exceed the optimal value found so far.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecdeploymentspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.DeploymentSpec -->

# Class DeploymentSpec (1.134.0)

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`env` |
`MutableSequence[`
Optional. Environment variables to be set with the Reasoning Engine deployment. The environment variables can be updated through the UpdateReasoningEngine API. |
`secret_env` |
`MutableSequence[`
Optional. Environment variables where the value is a secret in Cloud Secret Manager. To use this feature, add 'Secret Manager Secret Accessor' role (roles/secretmanager.secretAccessor) to AI Platform Reasoning Engine Service Agent. |
`psc_interface_config` |
Optional. Configuration for PSC-I. |
`min_instances` |
`int`
Optional. The minimum number of application instances that will be kept running at all times. Defaults to 1. Range: [0, 10]. This field is a member of `oneof` _ `_min_instances` .
|
`max_instances` |
`int`
Optional. The maximum number of application instances that can be launched to handle increased traffic. Defaults to 100. Range: [1, 1000]. If VPC-SC or PSC-I is enabled, the acceptable range is [1, 100]. This field is a member of `oneof` _ `_max_instances` .
|
`resource_limits` |
`MutableMapping[str, str]`
Optional. Resource limits for each container. Only 'cpu' and 'memory' keys are supported. Defaults to {"cpu": "4", "memory": "4Gi"}. - The only supported values for CPU are '1', '2', '4', '6' and '8'. For more information, go to https://cloud.google.com/run/docs/configuring/cpu. - The only supported values for memory are '1Gi', '2Gi', ... '32 Gi'. - For required cpu on different memory values, go to https://cloud.google.com/run/docs/configuring/memory-limits |
`container_concurrency` |
`int`
Optional. Concurrency for each container and agent server. Recommended value: 2 \* cpu + 1. Defaults to 9. This field is a member of `oneof` _ `_container_concurrency` .
|

## Classes

### ResourceLimitsEntry

`ResourceLimitsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DeploymentSpec

`DeploymentSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The specification of a Reasoning Engine deployment.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesstudyspecstudystoppingconfig_googlecloudaip_3e9a7e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesstudyspecstudystoppingconfig_googlecloudaipl_21a085.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesstudyspecstudystoppingconfig_googlecloudaipla_e2f3e6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesstudyspecstudystoppingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StudySpec.StudyStoppingConfig -->

# Class StudyStoppingConfig (1.134.0)

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.

## Attributes |
|
|---|---|
Name |
Description |
`should_stop_asap` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, a Study enters STOPPING_ASAP whenever it would normally enters STOPPING state. The bottom line is: set to true if you want to interrupt on-going evaluations of Trials as soon as the study stopping condition is met. (Please see Study.State documentation for the source of truth). |
`minimum_runtime_constraint` |
Each "stopping rule" in this proto specifies an "if" condition. Before Vizier would generate a new suggestion, it first checks each specified stopping rule, from top to bottom in this list. Note that the first few rules (e.g. minimum_runtime_constraint, min_num_trials) will prevent other stopping rules from being evaluated until they are met. For example, setting `min_num_trials=5` and
`always_stop_after= 1 hour` means that the Study will ONLY
stop after it has 5 COMPLETED trials, even if more than an
hour has passed since its creation. It follows the first
applicable rule (whose "if" condition is satisfied) to make
a stopping decision. If none of the specified rules are
applicable, then Vizier decides that the study should not
stop. If Vizier decides that the study should stop, the
study enters STOPPING state (or STOPPING_ASAP if
should_stop_asap = true). IMPORTANT: The automatic study
state transition happens precisely as described above; that
is, deleting trials or updating StudyConfig NEVER
automatically moves the study state back to ACTIVE. If you
want to *resume* a Study that was stopped, 1) change the
stopping conditions if necessary, 2) activate the study, and
then 3) ask for suggestions. If the specified time or
duration has not passed, do not stop the study.
|
`maximum_runtime_constraint` |
If the specified time or duration has passed, stop the study. |
`min_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are fewer than this many COMPLETED trials, do not stop the study. |
`max_num_trials` |
`google.protobuf.wrappers_pb2.Int32Value`
If there are more than this many trials, stop the study. |
`max_num_trials_no_progress` |
`google.protobuf.wrappers_pb2.Int32Value`
If the objective value has not improved for this many consecutive trials, stop the study. WARNING: Effective only for single-objective studies. |
`max_duration_no_progress` |
`google.protobuf.duration_pb2.Duration`
If the objective value has not improved for this much time, stop the study. WARNING: Effective only for single-objective studies. |

## Methods

### StudyStoppingConfig

`StudyStoppingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The configuration (stopping conditions) for automated stopping of a Study. Conditions include trial budgets, time budgets, and convergence detection.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespublishermodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PublisherModel -->

# Class PublisherModel (1.134.0)

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the PublisherModel. |
`version_id` |
`str`
Output only. Immutable. The version ID of the PublisherModel. A new version is committed when a new model version is uploaded under an existing model id. It is an auto-incrementing decimal number in string representation. |
`open_source_category` |
Required. Indicates the open source category of the publisher model. |
`parent` |
Optional. The parent that this model was customized from. E.g., Vision API, Natural Language API, LaMDA, T5, etc. Foundation models don't have parents. |
`supported_actions` |
Optional. Supported call-to-action options. |
`frameworks` |
`MutableSequence[str]`
Optional. Additional information about the model's Frameworks. |
`launch_stage` |
Optional. Indicates the launch stage of the model. |
`version_state` |
Optional. Indicates the state of the model version. |
`publisher_model_template` |
`str`
Optional. Output only. Immutable. Used to indicate this model has a publisher model and provide the template of the publisher model resource name. |
`predict_schemata` |
Optional. The schemata that describes formats of the PublisherModel's predictions and explanations as given and returned via PredictionService.Predict. |

## Classes

### CallToAction

`CallToAction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Actions could take on this Publisher Model.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Documentation

`Documentation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A named piece of documentation.

### LaunchStage

`LaunchStage(value)`


An enum representing the launch stage of a PublisherModel.

### OpenSourceCategory

`OpenSourceCategory(value)`


An enum representing the open source category of a PublisherModel.

### Parent

`Parent(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The information about the parent of a model.

### ResourceReference

`ResourceReference(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Reference to a resource.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### VersionState

`VersionState(value)`


An enum representing the state of the PublicModelVersion.

## Methods

### PublisherModel

`PublisherModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A Model Garden Publisher Model.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfea_0b983f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_online_store_admin_servicepagerslistfeatureviewsyncsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsAsyncPager -->

# Class ListFeatureViewSyncsAsyncPager (1.134.0)

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
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

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsAsyncPager

```
ListFeatureViewSyncsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestrial.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Trial -->

# Class Trial (1.134.0)

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of the Trial assigned by the service. |
`id` |
`str`
Output only. The identifier of the Trial assigned by the service. |
`state` |
Output only. The detailed state of the Trial. |
`parameters` |
`MutableSequence[`
Output only. The parameters of the Trial. |
`final_measurement` |
Output only. The final measurement containing the objective value. |
`measurements` |
`MutableSequence[`
Output only. A list of measurements that are strictly lexicographically ordered by their induced tuples (steps, elapsed_duration). These are used for early stopping computations. |
`start_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial was started. |
`end_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Time when the Trial's status changed to `SUCCEEDED` or `INFEASIBLE` .
|
`client_id` |
`str`
Output only. The identifier of the client that originally requested this Trial. Each client is identified by a unique client_id. When a client asks for a suggestion, Vertex AI Vizier will assign it a Trial. The client should evaluate the Trial, complete it, and report back to Vertex AI Vizier. If suggestion is asked again by same client_id before the Trial is completed, the same Trial will be returned. Multiple clients with different client_ids can ask for suggestions simultaneously, each of them will get their own Trial. |
`infeasible_reason` |
`str`
Output only. A human readable string describing why the Trial is infeasible. This is set only if Trial state is `INFEASIBLE` .
|
`custom_job` |
`str`
Output only. The CustomJob name linked to the Trial. It's set for a HyperparameterTuningJob's Trial. |
`web_access_uris` |
`MutableMapping[str, str]`
Output only. URIs for accessing `interactive shells |

## Classes

### Parameter

`Parameter(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a parameter to be tuned.

### State

`State(value)`


Describes a Trial state.

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

### Trial

`Trial(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextextractionp_d432a0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextextractionpr_bcff03.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextextractionpre_90f4b1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictinstance_v1beta1typestextextractionpredictioninstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextExtractionPredictionInstance -->

# Class TextExtractionPredictionInstance (1.134.0)

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

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
`key` |
`str`
This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Vertex AI will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique. |

## Methods

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.

### TextExtractionPredictionInstance

```
TextExtractionPredictionInstance(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction input format for Text Extraction.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginecontextspecmemorybankconfigttlconfiggranularttlconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineContextSpec.MemoryBankConfig.TtlConfig.GranularTtlConfig -->

# Class GranularTtlConfig (1.134.0)

`GranularTtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.

## Attributes |
|
|---|---|
Name |
Description |
`create_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories uploaded via CreateMemory. |
`generate_created_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories newly generated via GenerateMemories (GenerateMemoriesResponse.GeneratedMemory.Action.CREATED). |
`generate_updated_ttl` |
`google.protobuf.duration_pb2.Duration`
Optional. The TTL duration for memories updated via GenerateMemories (GenerateMemoriesResponse.GeneratedMemory.Action.CREATED). In the case of an UPDATE action, the `expire_time` of the
existing memory will be updated to the new value (now +
TTL).
|

## Methods

### GranularTtlConfig

`GranularTtlConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration for TTL of the memories in the Memory Bank based on the action that created or updated the memory.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesupdatefeaturestorerequest__googlecloudaiplatform_v_03796a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesupdatefeaturestorerequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateFeaturestoreRequest -->

# Class UpdateFeaturestoreRequest (1.134.0)

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.

## Attributes |
|
|---|---|
Name |
Description |
`featurestore` |
Required. The Featurestore's `name` field is used to
identify the Featurestore to be updated. Format:
`projects/{project}/locations/{location}/featurestores/{featurestore}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the Featurestore resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `online_serving_config.fixed_node_count`
- `online_serving_config.scaling`
- `online_storage_ttl_days`
|

## Methods

### UpdateFeaturestoreRequest

`UpdateFeaturestoreRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeaturestoreService.UpdateFeaturestore.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolparameterkeymatchspec_googlecloudaiplatfo_3bf4dd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkeymatchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchSpec -->

# Class ToolParameterKeyMatchSpec (1.134.0)

`ToolParameterKeyMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key match metric.

## Methods

### ToolParameterKeyMatchSpec

`ToolParameterKeyMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool parameter key match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesstringarray.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.StringArray -->

# Class StringArray (1.134.0)

`StringArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of string values.

## Attribute |
|
|---|---|
Name |
Description |
`values` |
`MutableSequence[str]`
A list of string values. |

## Methods

### StringArray

`StringArray(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A list of string values.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardtimeser_ad29a6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardtimeseriesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesAsyncPager -->

# Class ListTensorboardTimeSeriesAsyncPager (1.134.0)

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesAsyncPager

```
ListTensorboardTimeSeriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse
],
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslisthyperparametertuningjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListHyperparameterTuningJobsAsyncPager -->

# Class ListHyperparameterTuningJobsAsyncPager (1.134.0)

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

## Methods

### ListHyperparameterTuningJobsAsyncPager

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
