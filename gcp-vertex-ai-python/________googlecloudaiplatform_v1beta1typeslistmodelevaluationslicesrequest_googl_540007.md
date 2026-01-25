---
merged_at: 2026-01-25T21:47:44.385840
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_google_ec442c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googlec_ab5881.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googlecl_5c14a4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googleclo_c5317f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googleclou_5d9b9b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googlecloud_bb5f38.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest_googleclouda_34b4c5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typeslistmodelevaluationslicesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelEvaluationSlicesRequest -->

# Class ListModelEvaluationSlicesRequest (1.134.0)

```
ListModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelEvaluationSlices.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the ModelEvaluation to list the ModelEvaluationSlices from. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}`
|
`filter` |
`str`
The standard list filter. - `slice.dimension` - for =.
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via ListModelEvaluationSlicesResponse.next_page_token of the previous ModelService.ListModelEvaluationSlices call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListModelEvaluationSlicesRequest

```
ListModelEvaluationSlicesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for ModelService.ListModelEvaluationSlices.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesbatchcreatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCreateTensorboardTimeSeriesRequest -->

# Class BatchCreateTensorboardTimeSeriesRequest (1.134.0)

```
BatchCreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
The TensorboardRuns referenced by the parent fields in the
CreateTensorboardTimeSeriesRequest messages must be sub
resources of this TensorboardExperiment.
|
`requests` |
`MutableSequence[`
Required. The request message specifying the TensorboardTimeSeries to create. A maximum of 1000 TensorboardTimeSeries can be created in a batch. |

## Methods

### BatchCreateTensorboardTimeSeriesRequest

```
BatchCreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerssearchdataitemspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.SearchDataItemsPager -->

# Class SearchDataItemsPager (1.134.0)

```
SearchDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse) object, and
provides an `__iter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchDataItemsPager

```
SearchDataItemsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.SearchDataItemsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelversionspager__1107fd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmodel_servicepagerslistmodelversionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionsPager -->

# Class ListModelVersionsPager (1.134.0)

```
ListModelVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`models`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsPager

```
ListModelVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerssearchfeaturespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.SearchFeaturesPager -->

# Class SearchFeaturesPager (1.134.0)

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesPager

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.SearchFeaturesResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemsasyncpager_g_0239d4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemsasyncpager_go_4a14c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdataitemsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDataItemsAsyncPager -->

# Class ListDataItemsAsyncPager (1.134.0)

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataItemsAsyncPager

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDataItemsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicepagerslisteventsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListEventsAsyncPager -->

# Class ListEventsAsyncPager (1.134.0)

```
ListEventsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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


A pager for iterating through `list_events`

requests.

This class thinly wraps an initial
[ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse) object, and
provides an `__aiter__`

method to iterate through its
`session_events`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEvents`

requests and continue to iterate
through the `session_events`

field on the
corresponding responses.

All the usual [ListEventsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEventsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEventsAsyncPager

```
ListEventsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListEventsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictprediction_v1beta1types__googlecloudai_9be8b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictprediction_v1beta1types.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types -->

# Package prediction_v1beta1.types (1.134.0)

API documentation for `prediction_v1beta1.types`

package.

## Classes

[ClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ClassificationPredictionResult)

Prediction output format for Image and Text Classification.

[ImageObjectDetectionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageObjectDetectionPredictionResult)

Prediction output format for Image Object Detection.

[ImageSegmentationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageSegmentationPredictionResult)

Prediction output format for Image Segmentation.

[TabularClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularClassificationPredictionResult)

Prediction output format for Tabular Classification.

[TabularRegressionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularRegressionPredictionResult)

Prediction output format for Tabular Regression.

[TextExtractionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextExtractionPredictionResult)

Prediction output format for Text Extraction.

[TextSentimentPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult)

Prediction output format for Text Sentiment

[TimeSeriesForecastingPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TimeSeriesForecastingPredictionResult)

Prediction output format for Time Series Forecasting.

[VideoActionRecognitionPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoActionRecognitionPredictionResult)

Prediction output format for Video Action Recognition.

[VideoClassificationPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoClassificationPredictionResult)

Prediction output format for Video Classification.

[VideoObjectTrackingPredictionResult](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult)

Prediction output format for Video Object Tracking.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesimageobjectdetectio_d9e878.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1beta1schemapredictparams_v1beta1typesimageobjectdetectionpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.predict.params_v1beta1.types.ImageObjectDetectionPredictionParams -->

# Class ImageObjectDetectionPredictionParams (1.134.0)

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.

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
The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata's predictionsLimit. Default value is 10. |

## Methods

### ImageObjectDetectionPredictionParams

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.

### ImageObjectDetectionPredictionParams

```
ImageObjectDetectionPredictionParams(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction model parameters for Image Object Detection.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesupdatetensorboardrunrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateTensorboardRunRequest -->

# Class UpdateTensorboardRunRequest (1.134.0)

`UpdateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboardRun.

## Attributes |
|
|---|---|
Name |
Description |
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Required. Field mask is used to specify the fields to be overwritten in the TensorboardRun resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field is overwritten if it's in the mask. If the user does not provide a mask then all fields are overwritten if new values are specified. |
`tensorboard_run` |
Required. The TensorboardRun's `name` field is used to
identify the TensorboardRun to be updated. Format:
`projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### UpdateTensorboardRunRequest

`UpdateTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.UpdateTensorboardRun.


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesimportindexrequest_googlecloudaiplatform_v_1d4187.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesimportindexrequest_googlecloudaiplatform_v1_27fb74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesimportindexrequest_googlecloudaiplatform_v1b_d84c00.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesimportindexrequest_googlecloudaiplatform_v1be_140c53.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesimportindexrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessearchmodelmonitoringstatsfilter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchModelMonitoringStatsFilter -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistartifactsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListArtifactsAsyncPager -->

# Class ListArtifactsAsyncPager (1.134.0)

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

## Methods

### ListArtifactsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestensorboardrun__googlecloudaiplatform_v1beta1_6629b2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestensorboardrun.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TensorboardRun -->

# Class TensorboardRun (1.134.0)

`TensorboardRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Name of the TensorboardRun. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|
`display_name` |
`str`
Required. User provided name of this TensorboardRun. This value must be unique among all TensorboardRuns belonging to the same parent TensorboardExperiment. |
`description` |
`str`
Description of this TensorboardRun. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardRun was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this TensorboardRun was last updated. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your TensorboardRuns. This field will be used to filter and visualize Runs in the Tensorboard UI. For example, a Vertex AI training job can set a label aiplatform.googleapis.com/training_job_id=xxxxx to all the runs created within that job. An end user can set a label experiment_id=xxxxx for all the runs produced in a Jupyter notebook. These runs can be grouped by a label value and visualized together in the Tensorboard UI. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one TensorboardRun (System labels are excluded). See https://goo.gl/xmQnxf for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`etag` |
`str`
Used to perform a consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |

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

### TensorboardRun

`TensorboardRun(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


TensorboardRun maps to a specific execution of a training job with a given set of hyperparameter values, model definition, dataset, etc


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchreadtensorboardtimeseriesdatarequest_goo_1acc4c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchreadtensorboardtimeseriesdatarequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchReadTensorboardTimeSeriesDataRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesnotebookeucconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NotebookEucConfig -->

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

<!-- DOCUMENTO FUSIONADO: instance_v1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/instance_v1 -->

# Types for Google Cloud Aiplatform V1 Schema Predict Instance v1 API

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Classification.

#### content()

The image bytes or Cloud Storage URI to make the prediction on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
- image/gif
- image/png
- image/webp
- image/bmp
- image/tiff
image/vnd.microsoft.icon

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageObjectDetectionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Object Detection.

#### content()

The image bytes or Cloud Storage URI to make the prediction on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
- image/gif
- image/png
- image/webp
- image/bmp
- image/tiff
image/vnd.microsoft.icon

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.ImageSegmentationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Segmentation.

#### content()

The image bytes to make the predictions on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
image/png

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Classification.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextExtractionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Extraction.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### key()

This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Vertex AI will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### key(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.TextSentimentPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Sentiment.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoActionRecognitionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Action Recognition.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Classification.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1.schema.predict.instance_v1.types.VideoObjectTrackingPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Object Tracking.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiesasyncpag_90dedc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiesasyncpage_ac8e94.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiesasyncpager_c08a35.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiesasyncpager__c04343.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvizier_servicepagersliststudiesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vizier_service.pagers.ListStudiesAsyncPager -->

# Class ListStudiesAsyncPager (1.134.0)

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse) object, and
provides an `__aiter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListStudiesAsyncPager

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1beta1.types.vizier_service.ListStudiesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesbatchcreatetensorboardtimeseriesrequest_googl_b9294a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesbatchcreatetensorboardtimeseriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.BatchCreateTensorboardTimeSeriesRequest -->

# Class BatchCreateTensorboardTimeSeriesRequest (1.134.0)

```
BatchCreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardTimeSeries.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
The TensorboardRuns referenced by the parent fields in the
CreateTensorboardTimeSeriesRequest messages must be sub
resources of this TensorboardExperiment.
|
`requests` |
`MutableSequence[`
Required. The request message specifying the TensorboardTimeSeries to create. A maximum of 1000 TensorboardTimeSeries can be created in a batch. |

## Methods

### BatchCreateTensorboardTimeSeriesRequest

```
BatchCreateTensorboardTimeSeriesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for TensorboardService.BatchCreateTensorboardTimeSeries.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkeymatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKeyMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulesasyncpager_g_acd625.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesschedule_servicepagerslistschedulesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.schedule_service.pagers.ListSchedulesAsyncPager -->

# Class ListSchedulesAsyncPager (1.134.0)

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

## Methods

### ListSchedulesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_servicepagerslistendpointsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.pagers.ListEndpointsAsyncPager -->

# Class ListEndpointsAsyncPager (1.134.0)

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

## Methods

### ListEndpointsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesgeneratevideoresponse_googlecloudaiplatform_8e4bea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesgeneratevideoresponse_googlecloudaiplatform__a5c95d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgeneratevideoresponse_googlecloudaiplatform_v_390cb2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgeneratevideoresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateVideoResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolparameterkvmatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolParameterKVMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmeasurement_googlecloudaiplatformv1schematrainingj_b92cf2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmeasurement.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Measurement -->

# Class Measurement (1.134.0)

`Measurement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.

## Attributes |
|
|---|---|
Name |
Description |
`elapsed_duration` |
`google.protobuf.duration_pb2.Duration`
Output only. Time that the Trial has been running at the point of this Measurement. |
`step_count` |
`int`
Output only. The number of steps the machine learning model has been trained for. Must be non-negative. |
`metrics` |
`MutableSequence[`
Output only. A list of metrics got by evaluating the objective functions using suggested Parameter values. |

## Classes

### Metric

`Metric(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a metric in the measurement.

## Methods

### Measurement

`Measurement(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomlvideoclassificationinputsmodeltype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlVideoClassificationInputs.ModelType -->

# Class ModelType (1.134.0)

A model best tailored to be used within Google Cloud, and which cannot be exported. Default.

MOBILE_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) as a TensorFlow or TensorFlow Lite model and used on a mobile or edge device afterwards.

MOBILE_JETSON_VERSATILE_1

A model that, in addition to being available within Google Cloud, can also be exported (see ModelService.ExportModel) to a Jetson device afterwards.

Methods

ModelType

ModelType(value)

ModelType

ModelType(value)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-22 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadatastorespager_g_b4573d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadatastorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataStoresPager -->

# Class ListMetadataStoresPager (1.134.0)

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

## Methods

### ListMetadataStoresPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistsavedqueriespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListSavedQueriesPager -->

# Class ListSavedQueriesPager (1.134.0)

```
ListSavedQueriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
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


A pager for iterating through `list_saved_queries`

requests.

This class thinly wraps an initial
[ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse) object, and
provides an `__iter__`

method to iterate through its
`saved_queries`

field.

If there are more pages, the `__iter__`

method will make additional
`ListSavedQueries`

requests and continue to iterate
through the `saved_queries`

field on the
corresponding responses.

All the usual [ListSavedQueriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSavedQueriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSavedQueriesPager

```
ListSavedQueriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListSavedQueriesResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typesfeaturestorestate_googlecloudaiplatform_v1beta1_d62e23.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesfeaturestorestate_googlecloudaiplatform_v1beta1t_a00e3c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesfeaturestorestate_googlecloudaiplatform_v1beta1ty_c4f640.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesfeaturestorestate_googlecloudaiplatform_v1beta1typ_6b201f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturestorestate.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Featurestore.State -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureviewdirectwriterequestdatakeyandfeaturevalues.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteRequest.DataKeyAndFeatureValues -->

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

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### DataKeyAndFeatureValues

`DataKeyAndFeatureValues(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A data key and associated feature values to write to the feature view.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesgen_ai_tuning_servicepagerslisttuningjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_tuning_service.pagers.ListTuningJobsPager -->

# Class ListTuningJobsPager (1.134.0)

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
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


A pager for iterating through `list_tuning_jobs`

requests.

This class thinly wraps an initial
[ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTuningJobs`

requests and continue to iterate
through the `tuning_jobs`

field on the
corresponding responses.

All the usual [ListTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTuningJobsPager

```
ListTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.genai_tuning_service.ListTuningJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesindexdatapoint_googlecloudaiplatform_v1beta1servic_3788da.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesindexdatapoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.IndexDatapoint -->

# Class IndexDatapoint (1.134.0)

`IndexDatapoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datapoint of Index.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint_id` |
`str`
Required. Unique identifier of the datapoint. |
`feature_vector` |
`MutableSequence[float]`
Required. Feature embedding vector for dense index. An array of numbers with the length of [NearestNeighborSearchConfig.dimensions]. |
`sparse_embedding` |
Optional. Feature embedding vector for sparse index. |
`restricts` |
`MutableSequence[`
Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses categorical tokens. See: https://cloud.google.com/vertex-ai/docs/matching-engine/filtering |
`numeric_restricts` |
`MutableSequence[`
Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses numeric comparisons. |
`crowding_tag` |
Optional. CrowdingTag of the datapoint, the number of neighbors to return in each crowding can be configured during query. |
`embedding_metadata` |
`google.protobuf.struct_pb2.Struct`
Optional. The key-value map of additional metadata for the datapoint. |

## Classes

### CrowdingTag

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

### NumericRestriction

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Restriction

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).

### SparseEmbedding

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.

## Methods

### IndexDatapoint

`IndexDatapoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datapoint of Index.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistcontextsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListContextsAsyncPager -->

# Class ListContextsAsyncPager (1.134.0)

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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
[ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse) object, and
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

All the usual [ListContextsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListContextsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListContextsAsyncPager

```
ListContextsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListContextsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.featurestore_service.pagers`

module.

## Classes

[ListEntityTypesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesAsyncPager)

```
ListEntityTypesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__aiter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListEntityTypesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListEntityTypesPager)

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse) object, and
provides an `__iter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesAsyncPager)

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

[ListFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesPager)

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

[ListFeaturestoresAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresAsyncPager)

```
ListFeaturestoresAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse) object, and
provides an `__aiter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListFeaturestoresPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresPager)

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse) object, and
provides an `__iter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchFeaturesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesAsyncPager)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[SearchFeaturesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesPager)

```
SearchFeaturesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse) object, and
provides an `__iter__`

method to iterate through its
`features`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager__2e209c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager___23d269.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager__g_b10c81.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager__go_e87a11.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager__goo_0c215d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesjob_servicepagerslistdatalabelingjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.job_service.pagers.ListDataLabelingJobsPager -->

# Class ListDataLabelingJobsPager (1.134.0)

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

## Methods

### ListDataLabelingJobsPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigpredictiondrift_63ba43.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectiveconfigpredictiondriftdetectionconfigdriftthresholdsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveConfig.PredictionDriftDetectionConfig.DriftThresholdsEntry -->

# Class DriftThresholdsEntry (1.134.0)

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### DriftThresholdsEntry

`DriftThresholdsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesreasoningenginespecsourcecodespecdeveloperconnectconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ReasoningEngineSpec.SourceCodeSpec.DeveloperConnectConfig -->

# Class DeveloperConnectConfig (1.134.0)

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.

## Attributes |
|
|---|---|
Name |
Description |
`git_repository_link` |
`str`
Required. The Developer Connect Git repository link, formatted as `projects/*/locations/*/connections/*/gitRepositoryLink/*` .
|
`dir_` |
`str`
Required. Directory, relative to the source root, in which to run the build. |
`revision` |
`str`
Required. The revision to fetch from the Git repository such as a branch, a tag, a commit SHA, or any Git ref. |

## Methods

### DeveloperConnectConfig

`DeveloperConnectConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Specifies the configuration for fetching source code from a Git repository that is managed by Developer Connect. This includes the repository, revision, and directory to use.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturesasyncpage_7180fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.134.0)

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

## Methods

### ListFeaturesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerslistfeaturestorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.ListFeaturestoresPager -->

# Class ListFeaturestoresPager (1.134.0)

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse) object, and
provides an `__iter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturestoresPager

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.ListFeaturestoresResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboards_d50b2f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardsp_31d9d5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicestensorboard_servicepagerslisttensorboardspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardsPager -->

# Class ListTensorboardsPager (1.134.0)

```
ListTensorboardsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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


A pager for iterating through `list_tensorboards`

requests.

This class thinly wraps an initial
[ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboards`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboards`

requests and continue to iterate
through the `tensorboards`

field on the
corresponding responses.

All the usual [ListTensorboardsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardsPager

```
ListTensorboardsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesfeaturegroup.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureGroup -->

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

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Group.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typescorroboratecontentresponse_googlecloudaiplat_047fb0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typescorroboratecontentresponse_googlecloudaiplatf_fad69b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescorroboratecontentresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CorroborateContentResponse -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesuploadmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadModelRequest -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesnotebookeucconfig_googlecloudaiplatform_v1typ_c796bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesnotebookeucconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NotebookEucConfig -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesschedulingstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Scheduling.Strategy -->

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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragcorp_c4a270.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragcorpo_03590a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragcorpor_b65aae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesvertex_rag_data_servicepagerslistragcorporapager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.vertex_rag_data_service.pagers.ListRagCorporaPager -->

# Class ListRagCorporaPager (1.134.0)

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

## Methods

### ListRagCorporaPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistmetadataschemaspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListMetadataSchemasPager -->

# Class ListMetadataSchemasPager (1.134.0)

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

## Methods

### ListMetadataSchemasPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvizier_servicepagers.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.vizier_service.pagers`

module.

## Classes

[ListStudiesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager)

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__aiter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListStudiesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesPager)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
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


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__iter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__iter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrialsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__aiter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrialsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
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


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesrebasetunedmodelrequest_googlecloudaiplatfo_73f0a9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesrebasetunedmodelrequest_googlecloudaiplatfor_84a1b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrebasetunedmodelrequest_googlecloudaiplatform_15a1ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrebasetunedmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RebaseTunedModelRequest -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkvmatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKVMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typespipelinejobruntimeconfiginputartifact_googlec_53e83c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typespipelinejobruntimeconfiginputartifact.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineJob.RuntimeConfig.InputArtifact -->

# Class InputArtifact (1.134.0)

`InputArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of an input artifact.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`artifact_id` |
`str`
Artifact resource id from MLMD. Which is the last portion of an artifact resource name: `projects/{project}/locations/{location}/metadataStores/default/artifacts/{artifact_id}` .
The artifact must stay within the same project, location and
default metadatastore as the pipeline.
This field is a member of `oneof` _ `kind` .
|

## Methods

### InputArtifact

`InputArtifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The type of an input artifact.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolparameterkeymatchinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolParameterKeyMatchInstance -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecfeatureattributi_d896f9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecfeatureattributio_e25a34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecfeatureattributionspecfeaturealertconditionsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec.FeatureAttributionSpec.FeatureAlertConditionsEntry -->

# Class FeatureAlertConditionsEntry (1.134.0)

`FeatureAlertConditionsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesdeploymentstage.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeploymentStage -->

# Class DeploymentStage (1.134.0)

`DeploymentStage(value)`


Stage field indicating the current progress of a deployment.

## Enums |
|
|---|---|
Name |
Description |
`DEPLOYMENT_STAGE_UNSPECIFIED` |
Default value. This value is unused. |
`STARTING_DEPLOYMENT` |
The deployment is initializing and setting up the environment. |
`PREPARING_MODEL` |
The deployment is preparing the model assets. |
`CREATING_SERVING_CLUSTER` |
The deployment is creating the underlying serving cluster. |
`ADDING_NODES_TO_CLUSTER` |
The deployment is adding nodes to the serving cluster. |
`GETTING_CONTAINER_IMAGE` |
The deployment is getting the container image for the model server. |
`STARTING_MODEL_SERVER` |
The deployment is starting the model server. |
`FINISHING_UP` |
The deployment is performing finalization steps. |
`DEPLOYMENT_TERMINATED` |
The deployment has terminated. |
`SUCCESSFULLY_DEPLOYED` |
The deployment has succeeded. |
`FAILED_TO_DEPLOY` |
The deployment has failed. |

## Methods

### DeploymentStage

`DeploymentStage(value)`


Stage field indicating the current progress of a deployment.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistdatasetversionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListDatasetVersionsPager -->

# Class ListDatasetVersionsPager (1.134.0)

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetVersionsPager

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListDatasetVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformmetadataschemagoogleartifact_schemaexperimentmodel_instan_46d8b8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformmetadataschemagoogleartifact_schemaexperimentmodel_instanc_3fcb89.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformmetadataschemagoogleartifact_schemaexperimentmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.metadata.schema.google.artifact_schema.ExperimentModel -->

# Class ExperimentModel (1.134.0)

```
ExperimentModel(
*,
framework_name: str,
framework_version: str,
model_file: str,
uri: str,
model_class: typing.Optional[str] = None,
predict_schemata: typing.Optional[
google.cloud.aiplatform.metadata.schema.utils.PredictSchemata
] = None,
artifact_id: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
state: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact.State
] = State.LIVE
)
```


An artifact representing a Vertex Experiment Model.

## Properties

### framework_name

The framework name of the saved ML model.

### framework_version

The framework version of the saved ML model.

### model_class

The class name of the saved ML model.

## Methods

### ExperimentModel

```
ExperimentModel(
*,
framework_name: str,
framework_version: str,
model_file: str,
uri: str,
model_class: typing.Optional[str] = None,
predict_schemata: typing.Optional[
google.cloud.aiplatform.metadata.schema.utils.PredictSchemata
] = None,
artifact_id: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
schema_version: typing.Optional[str] = None,
description: typing.Optional[str] = None,
metadata: typing.Optional[typing.Dict] = None,
state: typing.Optional[
google.cloud.aiplatform_v1.types.artifact.Artifact.State
] = State.LIVE
)
```


Instantiates an ExperimentModel that represents a saved ML model.

Parameters |
|
|---|---|
Name |
Description |
`framework_name` |
`str`
Required. The name of the model's framework. E.g., 'sklearn' |
`framework_version` |
`str`
Required. The version of the model's framework. E.g., '1.1.0' |
`model_file` |
`str`
Required. The file name of the model. E.g., 'model.pkl' |
`uri` |
`str`
Required. The uniform resource identifier of the model artifact directory. |
`model_class` |
`str`
Optional. The class name of the model. E.g., 'sklearn.linear_model._base.LinearRegression' |
`predict_schemata` |
`PredictSchemata`
Optional. An instance of PredictSchemata which holds instance, parameter and prediction schema uris. |
`artifact_id` |
`str`
Optional. The <resource_id> portion of the Artifact name with the format. This is globally unique in a metadataStore: projects/123/locations/us-central1/metadataStores/<metadata_store_id>/artifacts/<resource_id>. |
`display_name` |
`str`
Optional. The user-defined name of the Artifact. |
`schema_version` |
`str`
Optional. schema_version specifies the version used by the Artifact. If not set, defaults to use the latest version. |
`description` |
`str`
Optional. Describes the purpose of the Artifact to be created. |
`metadata` |
`Dict`
Optional. Contains the metadata information that will be stored in the Artifact. |
`state` |
`google.cloud.gapic.types.Artifact.State`
Optional. The state of this Artifact. This is a property of the Artifact, and does not imply or apture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |

### get

```
get(
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
`str`
Required. An artifact id of the ExperimentModel artifact. |
`metadata_store_id` |
`str`
Optional. MetadataStore to retrieve Artifact from. If not set, metadata_store_id is set to "default". If artifact_id is a fully-qualified resource name, its metadata_store_id overrides this one. |
`project` |
`str`
Optional. Project to retrieve the artifact from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve the Artifact from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this Artifact. Overrides credentials set in aiplatform.init. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if artifact's schema title is not 'google.ExperimentModel'. |

### get_model_info

`get_model_info() -> typing.Dict[str, typing.Any]`


Get the model's info from an experiment model artifact.

### load_model

`load_model() -> typing.Union[sklearn.base.BaseEstimator, xgb.Booster, tf.Module]`


Retrieves the original ML model from an ExperimentModel.

Example Usage:

```
experiment_model = aiplatform.get_experiment_model("my-sklearn-model")
sk_model = experiment_model.load_model()
pred_y = model.predict(test_X)
```


Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
if model type is not supported. |

### register_model

```
register_model(
*,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
use_gpu: bool = False,
is_default_version: bool = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
serving_container_image_uri: typing.Optional[str] = None,
serving_container_predict_route: typing.Optional[str] = None,
serving_container_health_route: typing.Optional[str] = None,
serving_container_command: typing.Optional[typing.Sequence[str]] = None,
serving_container_args: typing.Optional[typing.Sequence[str]] = None,
serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync: typing.Optional[bool] = True,
upload_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.models.Model
```


Register an ExperimentModel to Model Registry and returns a Model representing the registered Model resource.

Example Usage:

```
experiment_model = aiplatform.get_experiment_model("my-sklearn-model")
registered_model = experiment_model.register_model()
registered_model.deploy(endpoint=my_endpoint)
```


Parameters |
|
|---|---|
Name |
Description |
`model_id` |
`str`
Optional. The ID to use for the registered Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model that the newly-registered model will be a version of. Only set this field when uploading a new version of an existing model. |
`use_gpu` |
`str`
Optional. Whether or not to use GPUs for the serving container. Only specify this argument when registering a Tensorflow model and 'serving_container_image_uri' is not specified. |
`is_default_version` |
`bool`
Optional. When set to True, the newly registered model version will automatically have alias "default" included. Subsequent uses of this model without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the newly-registered model version will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that a model version can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`version_description` |
`str`
Optional. The description of the model version being uploaded. |
`display_name` |
`str`
Optional. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the model. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`serving_container_image_uri` |
`str`
Optional. The URI of the Model serving container. A pre-built container |
`serving_container_predict_route` |
`str`
Optional. An HTTP path to send prediction requests to the container, and which must be supported by it. If not specified a default HTTP path will be used by Vertex AI. |
`serving_container_health_route` |
`str`
Optional. An HTTP path to send health check requests to the container, and which must be supported by it. If not specified a standard HTTP path will be used by Vertex AI. |
`serving_container_command` |
`Sequence[str]`
Optional. The command with which the container is run. Not executed within a shell. The Docker image's ENTRYPOINT is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`serving_container_args` |
`Sequence[str]`
Optional. The arguments to the command. The Docker image's CMD is used if this is not provided. Variable references $(VAR_NAME) are expanded using the container's environment. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR_NAME) syntax can be escaped with a double $$, ie: $$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |
`serving_container_environment_variables` |
`Dict[str, str]`
Optional. The environment variables that are to be present in the container. Should be a dictionary where keys are environment variable names and values are environment variable values for those names. |
`serving_container_ports` |
`Sequence[int]`
Optional. Declaration of ports that are exposed by the container. This field is primarily informational, it gives Vertex AI information about the network connections the container uses. Listing or not a port here has no impact on whether the port is actually exposed, any port listening on the default "0.0.0.0" address inside a container will be accessible from the network. |
`instance_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in |
`parameters_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via |
`prediction_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form |
`staging_bucket` |
`str`
Optional. Bucket to stage local model artifacts. Overrides staging_bucket set in aiplatform.init. |
`sync` |
`bool`
Optional. Whether to execute this method synchronously. If False, this method will unblock and it will be executed in a concurrent Future. |
`upload_request_timeout` |
`float`
Optional. The timeout for the upload request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If the model doesn't have a pre-built container that is suitable for its framework and 'serving_container_image_uri' is not set. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the registered model resource. |


---

<!-- DOCUMENTO FUSIONADO: instance_v1beta1.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/instance_v1beta1 -->

# Types for Google Cloud Aiplatform V1beta1 Schema Predict Instance v1beta1 API

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Classification.

#### content()

The image bytes or Cloud Storage URI to make the prediction on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
- image/gif
- image/png
- image/webp
- image/bmp
- image/tiff
image/vnd.microsoft.icon

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageObjectDetectionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Object Detection.

#### content()

The image bytes or Cloud Storage URI to make the prediction on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
- image/gif
- image/png
- image/webp
- image/bmp
- image/tiff
image/vnd.microsoft.icon

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.ImageSegmentationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Image Segmentation.

#### content()

The image bytes to make the predictions on.

**Type**

#### mime_type()

The MIME type of the content of the image. Only the images in below listed MIME types are supported.

- image/jpeg
image/png

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Classification.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextExtractionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Extraction.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### key()

This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Vertex AI will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### key(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.TextSentimentPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Text Sentiment.

#### content()

The text snippet to make the predictions on.

**Type**

#### mime_type()

The MIME type of the text snippet. The supported MIME types are listed below.

text/plain

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoActionRecognitionPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Action Recognition.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoClassificationPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Classification.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.instance_v1beta1.types.VideoObjectTrackingPredictionInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction input format for Video Object Tracking.

#### content()

The Google Cloud Storage location of the video on which to perform the prediction.

**Type**

#### mime_type()

The MIME type of the content of the video. Only the following are supported: video/mp4 video/avi video/quicktime

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision.

**Type**

#### time_segment_end()

The end, exclusive, of the video’s time segment on which to perform the prediction. Expressed as a number of seconds as measured from the start of the video, with “s” appended at the end. Fractions are allowed, up to a microsecond precision, and “inf” or “Infinity” is allowed, which means the end of the video.

**Type**

#### content(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### mime_type(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_start(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)


---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typescorroboratecontentresponse__googlecloudaiplatfo_600828.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typescorroboratecontentresponse__googlecloudaiplatfor_1a2369.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typescorroboratecontentresponse__googlecloudaiplatform_858819.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typescorroboratecontentresponse__googlecloudaiplatform__6e53a8.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescorroboratecontentresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CorroborateContentResponse -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typestoolnamematchspec_googlecloudaiplatform_v1bet_7f8d4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolnamematchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolNameMatchSpec -->

# Class ToolNameMatchSpec (1.134.0)

`ToolNameMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match metric.

## Methods

### ToolNameMatchSpec

`ToolNameMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestoolcallvalidspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ToolCallValidSpec -->

# Class ToolCallValidSpec (1.134.0)

`ToolCallValidSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid metric.

## Methods

### ToolCallValidSpec

`ToolCallValidSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesindexdatapoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.IndexDatapoint -->

# Class IndexDatapoint (1.134.0)

`IndexDatapoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datapoint of Index.

## Attributes |
|
|---|---|
Name |
Description |
`datapoint_id` |
`str`
Required. Unique identifier of the datapoint. |
`feature_vector` |
`MutableSequence[float]`
Required. Feature embedding vector for dense index. An array of numbers with the length of [NearestNeighborSearchConfig.dimensions]. |
`sparse_embedding` |
Optional. Feature embedding vector for sparse index. |
`restricts` |
`MutableSequence[`
Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses categorical tokens. See: https://cloud.google.com/vertex-ai/docs/matching-engine/filtering |
`numeric_restricts` |
`MutableSequence[`
Optional. List of Restrict of the datapoint, used to perform "restricted searches" where boolean rule are used to filter the subset of the database eligible for matching. This uses numeric comparisons. |
`crowding_tag` |
Optional. CrowdingTag of the datapoint, the number of neighbors to return in each crowding can be configured during query. |
`embedding_metadata` |
`google.protobuf.struct_pb2.Struct`
Optional. The key-value map of additional metadata for the datapoint. |

## Classes

### CrowdingTag

`CrowdingTag(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Crowding tag is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute.

### NumericRestriction

`NumericRestriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This field allows restricts to be based on numeric comparisons rather than categorical tokens.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### Restriction

`Restriction(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restriction of a datapoint which describe its attributes(tokens) from each of several attribute categories(namespaces).

### SparseEmbedding

`SparseEmbedding(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Feature embedding vector for sparse index. An array of numbers whose values are located in the specified dimensions.

## Methods

### IndexDatapoint

`IndexDatapoint(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A datapoint of Index.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturesasync_91cc95.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.134.0)

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

## Methods

### ListFeaturesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesautoscalingmetricspec_googlecloudaiplatform_v1beta_6958cb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesautoscalingmetricspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AutoscalingMetricSpec -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesuploadmodelrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelRequest -->

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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistentitytypes_029775.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistentitytypesp_ea4f80.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistentitytypespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListEntityTypesPager -->

# Class ListEntityTypesPager (1.134.0)

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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


A pager for iterating through `list_entity_types`

requests.

This class thinly wraps an initial
[ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse) object, and
provides an `__iter__`

method to iterate through its
`entity_types`

field.

If there are more pages, the `__iter__`

method will make additional
`ListEntityTypes`

requests and continue to iterate
through the `entity_types`

field on the
corresponding responses.

All the usual [ListEntityTypesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEntityTypesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEntityTypesPager

```
ListEntityTypesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListEntityTypesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetsAsyncPager -->

# Class ListDatasetsAsyncPager (1.134.0)

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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


A pager for iterating through `list_datasets`

requests.

This class thinly wraps an initial
[ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse) object, and
provides an `__aiter__`

method to iterate through its
`datasets`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDatasets`

requests and continue to iterate
through the `datasets`

field on the
corresponding responses.

All the usual [ListDatasetsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetsAsyncPager

```
ListDatasetsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetsResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typespairwisemetricinstance_googlecloudaiplatform_v1be_0c6846.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typespairwisemetricinstance_googlecloudaiplatform_v1bet_92090d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespairwisemetricinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseMetricInstance -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesschedulingstrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Scheduling.Strategy -->

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmetadata_servicepagerslistexecutionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.metadata_service.pagers.ListExecutionsAsyncPager -->

# Class ListExecutionsAsyncPager (1.134.0)

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

## Methods

### ListExecutionsAsyncPager

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

<!-- DOCUMENTO FUSIONADO: ________googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1t_a3c235.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _______googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1ty_2937bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ______googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1typ_aadb58.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1type_77fbd7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1types_6593fc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1typest_01b1bc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1typesto_20876b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typestoolnamematchspec_googlecloudaiplatform_v1typestoo_7a475c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolnamematchspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolNameMatchSpec -->

# Class ToolNameMatchSpec (1.134.0)

`ToolNameMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match metric.

## Methods

### ToolNameMatchSpec

`ToolNameMatchSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool name match metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typestoolcallvalidspec.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ToolCallValidSpec -->

# Class ToolCallValidSpec (1.134.0)

`ToolCallValidSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid metric.

## Methods

### ToolCallValidSpec

`ToolCallValidSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for tool call valid metric.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictprediction_v1typesclassificationpredictionresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.prediction_v1.types.ClassificationPredictionResult -->

# Class ClassificationPredictionResult (1.134.0)

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.

## Attributes |
|
|---|---|
Name |
Description |
`ids` |
`MutableSequence[int]`
The resource IDs of the AnnotationSpecs that had been identified. |
`display_names` |
`MutableSequence[str]`
The display names of the AnnotationSpecs that had been identified, order matches the IDs. |
`confidences` |
`MutableSequence[float]`
The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids. |

## Methods

### ClassificationPredictionResult

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.

### ClassificationPredictionResult

```
ClassificationPredictionResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Prediction output format for Image and Text Classification.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelevaluationspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationsPager -->

# Class ListModelEvaluationsPager (1.134.0)

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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


A pager for iterating through `list_model_evaluations`

requests.

This class thinly wraps an initial
[ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_evaluations`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelEvaluations`

requests and continue to iterate
through the `model_evaluations`

field on the
corresponding responses.

All the usual [ListModelEvaluationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationsPager

```
ListModelEvaluationsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicessession_servicepagerslistsessionsasyncpage_b4db5d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicessession_servicepagerslistsessionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.session_service.pagers.ListSessionsAsyncPager -->

# Class ListSessionsAsyncPager (1.134.0)

```
ListSessionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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


A pager for iterating through `list_sessions`

requests.

This class thinly wraps an initial
[ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`sessions`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSessions`

requests and continue to iterate
through the `sessions`

field on the
corresponding responses.

All the usual [ListSessionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSessionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSessionsAsyncPager

```
ListSessionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsRequest,
response: google.cloud.aiplatform_v1beta1.types.session_service.ListSessionsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecdatadriftspecfeat_06d7d6.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringobjectivespecdatadriftspecfeaturealertconditionsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringObjectiveSpec.DataDriftSpec.FeatureAlertConditionsEntry -->

# Class FeatureAlertConditionsEntry (1.134.0)

`FeatureAlertConditionsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesautoscalingmetricspecmonitoredresourcelabelsentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.AutoscalingMetricSpec.MonitoredResourceLabelsEntry -->

# Class MonitoredResourceLabelsEntry (1.134.0)

```
MonitoredResourceLabelsEntry(
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

### MonitoredResourceLabelsEntry

```
MonitoredResourceLabelsEntry(
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1typesacceleratortype_googlecloudaiplatform_v1typescre_6d5136.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1typesacceleratortype_googlecloudaiplatform_v1typescrea_ba7c6c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesacceleratortype_googlecloudaiplatform_v1typescreat_8cdea0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesacceleratortype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AcceleratorType -->

# Class AcceleratorType (1.134.0)

`AcceleratorType(value)`


Represents a hardware accelerator type.

## Enums |
|
|---|---|
Name |
Description |
`ACCELERATOR_TYPE_UNSPECIFIED` |
Unspecified accelerator type, which means no accelerator. |
`NVIDIA_TESLA_K80` |
Deprecated: Nvidia Tesla K80 GPU has reached end of support, see https://cloud.google.com/compute/docs/eol/k80-eol. |
`NVIDIA_TESLA_P100` |
Nvidia Tesla P100 GPU. |
`NVIDIA_TESLA_V100` |
Nvidia Tesla V100 GPU. |
`NVIDIA_TESLA_P4` |
Nvidia Tesla P4 GPU. |
`NVIDIA_TESLA_T4` |
Nvidia Tesla T4 GPU. |
`NVIDIA_TESLA_A100` |
Nvidia Tesla A100 GPU. |
`NVIDIA_A100_80GB` |
Nvidia A100 80GB GPU. |
`NVIDIA_L4` |
Nvidia L4 GPU. |
`NVIDIA_H100_80GB` |
Nvidia H100 80Gb GPU. |
`NVIDIA_H100_MEGA_80GB` |
Nvidia H100 Mega 80Gb GPU. |
`NVIDIA_H200_141GB` |
Nvidia H200 141Gb GPU. |
`NVIDIA_B200` |
Nvidia B200 GPU. |
`NVIDIA_GB200` |
Nvidia GB200 GPU. |
`NVIDIA_RTX_PRO_6000` |
Nvidia RTX Pro 6000 GPU. |
`TPU_V2` |
TPU v2. |
`TPU_V3` |
TPU v3. |
`TPU_V4_POD` |
TPU v4. |
`TPU_V5_LITEPOD` |
TPU v5. |

## Methods

### AcceleratorType

`AcceleratorType(value)`


Represents a hardware accelerator type.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typescreatecontextrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateContextRequest -->

# Class CreateContextRequest (1.134.0)

`CreateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateContext.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Context should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`context` |
Required. The Context to create. |
`context_id` |
`str`
The {context} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}` .
If not provided, the Context's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Contexts in the parent MetadataStore. (Otherwise the request
will fail with ALREADY_EXISTS, or PERMISSION_DENIED if the
caller can't view the preexisting Context.)
|

## Methods

### CreateContextRequest

`CreateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateContext.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeaturemonitorjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureMonitorJob -->

# Class FeatureMonitorJob (1.134.0)

`FeatureMonitorJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor Job.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Identifier. Name of the FeatureMonitorJob. Format: `projects/{project}/locations/{location}/featureGroups/{feature_group}/featureMonitors/{feature_monitor}/featureMonitorJobs/{feature_monitor_job}` .
|
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this FeatureMonitorJob was created. Creation of a FeatureMonitorJob means that the job is pending / waiting for sufficient resources but may not have started running yet. |
`final_status` |
`google.rpc.status_pb2.Status`
Output only. Final status of the FeatureMonitorJob. |
`job_summary` |
Output only. Summary from the FeatureMonitorJob. |
`labels` |
`MutableMapping[str, str]`
Optional. The labels with user-defined metadata to organize your FeatureMonitorJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureMonitor(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. |
`description` |
`str`
Optional. Description of the FeatureMonitor. |
`drift_base_feature_monitor_job_id` |
`int`
Output only. FeatureMonitorJob ID comparing to which the drift is calculated. |
`drift_base_snapshot_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Data snapshot time comparing to which the drift is calculated. |
`feature_selection_config` |
Output only. Feature selection config used when creating FeatureMonitorJob. |
`trigger_type` |
Output only. Trigger type of the Feature Monitor Job. |

## Classes

### FeatureMonitorJobTrigger

`FeatureMonitorJobTrigger(value)`


Choices of the trigger type.

### JobSummary

`JobSummary(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Summary from the FeatureMonitorJob.

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

### FeatureMonitorJob

`FeatureMonitorJob(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Vertex AI Feature Monitor Job.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerslistannotationsasyncpager__9eaa4b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerslistannotationsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.ListAnnotationsAsyncPager -->

# Class ListAnnotationsAsyncPager (1.134.0)

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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


A pager for iterating through `list_annotations`

requests.

This class thinly wraps an initial
[ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse) object, and
provides an `__aiter__`

method to iterate through its
`annotations`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListAnnotations`

requests and continue to iterate
through the `annotations`

field on the
corresponding responses.

All the usual [ListAnnotationsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListAnnotationsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListAnnotationsAsyncPager

```
ListAnnotationsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.ListAnnotationsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesgen_ai_cache_servicepagerslistcachedcontentspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.gen_ai_cache_service.pagers.ListCachedContentsPager -->

# Class ListCachedContentsPager (1.134.0)

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
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


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsResponse) object, and
provides an `__iter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__iter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsPager

```
ListCachedContentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
],
request: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1.types.gen_ai_cache_service.ListCachedContentsResponse,
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

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesretrievememoriesrequest_googlecloudaiplatfo_4fa5f3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesretrievememoriesrequest_googlecloudaiplatfor_0e6e4e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesretrievememoriesrequest_googlecloudaiplatform_ce7343.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesretrievememoriesrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RetrieveMemoriesRequest -->

# Class RetrieveMemoriesRequest (1.134.0)

`RetrieveMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.RetrieveMemories.

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
`similarity_search_params` |
Parameters for semantic similarity search based retrieval. This field is a member of `oneof` _ `retrieval_params` .
|
`simple_retrieval_params` |
Parameters for simple (non-similarity search) retrieval. This field is a member of `oneof` _ `retrieval_params` .
|
`parent` |
`str`
Required. The resource name of the ReasoningEngine to retrieve memories from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`scope` |
`MutableMapping[str, str]`
Required. The scope of the memories to retrieve. A memory must have exactly the same scope ( `Memory.scope` ) as the
scope provided here to be retrieved (same keys and values).
Order does not matter, but it is case-sensitive.
|

## Classes

### ScopeEntry

`ScopeEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


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

### SimilaritySearchParams

`SimilaritySearchParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for semantic similarity search based retrieval.

### SimpleRetrievalParams

`SimpleRetrievalParams(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Parameters for simple (non-similarity search) retrieval.

## Methods

### RetrieveMemoriesRequest

`RetrieveMemoriesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MemoryBankService.RetrieveMemories.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicestensorboard_servicepagerslisttensorboardrunspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardRunsPager -->

# Class ListTensorboardRunsPager (1.134.0)

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
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


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardRunsPager

```
ListTensorboardRunsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardRunsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistcustomjobsasyncpager__8225df.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistcustomjobsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListCustomJobsAsyncPager -->

# Class ListCustomJobsAsyncPager (1.134.0)

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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
[ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse) object, and
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

All the usual [ListCustomJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCustomJobsAsyncPager

```
ListCustomJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListCustomJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesvertex_rag_data_servicepagerslistragfilesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vertex_rag_data_service.pagers.ListRagFilesAsyncPager -->

# Class ListRagFilesAsyncPager (1.134.0)

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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
[ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse) object, and
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

All the usual [ListRagFilesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListRagFilesAsyncPager

```
ListRagFilesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse
],
],
request: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesRequest,
response: google.cloud.aiplatform_v1.types.vertex_rag_data_service.ListRagFilesResponse,
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

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnastrialdetailspager_e1bbfa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnastrialdetailspager__5e30b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistnastrialdetailspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListNasTrialDetailsPager -->

# Class ListNasTrialDetailsPager (1.134.0)

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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
[ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse) object, and
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

All the usual [ListNasTrialDetailsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNasTrialDetailsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNasTrialDetailsPager

```
ListNasTrialDetailsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListNasTrialDetailsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typessummarizationqualityresult_googlecloudaiplatform_v_cff21b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typessummarizationqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationQualityResult -->

# Class SummarizationQualityResult (1.134.0)

`SummarizationQualityResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationQualityResult

`SummarizationQualityResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typespointwisemetricinstance.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PointwiseMetricInstance -->

# Class PointwiseMetricInstance (1.134.0)

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attribute |
|
|---|---|
Name |
Description |
`json_instance` |
`str`
Instance specified as a json string. String key-value pairs are expected in the json_instance to render PointwiseMetricSpec.instance_prompt_template. This field is a member of `oneof` _ `instance` .
|

## Methods

### PointwiseMetricInstance

`PointwiseMetricInstance(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdataitemsasyncpag_8b0090.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdataitemsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDataItemsAsyncPager -->

# Class ListDataItemsAsyncPager (1.134.0)

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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


A pager for iterating through `list_data_items`

requests.

This class thinly wraps an initial
[ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_items`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListDataItems`

requests and continue to iterate
through the `data_items`

field on the
corresponding responses.

All the usual [ListDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataItemsAsyncPager

```
ListDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDataItemsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesmodel_servicepagerslistmodelversionsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionsAsyncPager -->

# Class ListModelVersionsAsyncPager (1.134.0)

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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


A pager for iterating through `list_model_versions`

requests.

This class thinly wraps an initial
[ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse) object, and
provides an `__aiter__`

method to iterate through its
`models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersions`

requests and continue to iterate
through the `models`

field on the
corresponding responses.

All the usual [ListModelVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionsAsyncPager

```
ListModelVersionsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegro_918fc9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegrou_00679a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroup_ffe54e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroups_babf20.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeature_registry_servicepagerslistfeaturegroupspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_registry_service.pagers.ListFeatureGroupsPager -->

# Class ListFeatureGroupsPager (1.134.0)

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

## Methods

### ListFeatureGroupsPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesnotebook_servicepagerslistnotebookruntimespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimesPager -->

# Class ListNotebookRuntimesPager (1.134.0)

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesPager

```
ListNotebookRuntimesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemsasyncpager__faca5a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesdataset_servicepagerssearchdataitemsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.dataset_service.pagers.SearchDataItemsAsyncPager -->

# Class SearchDataItemsAsyncPager (1.134.0)

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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


A pager for iterating through `search_data_items`

requests.

This class thinly wraps an initial
[SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse) object, and
provides an `__aiter__`

method to iterate through its
`data_item_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchDataItems`

requests and continue to iterate
through the `data_item_views`

field on the
corresponding responses.

All the usual [SearchDataItemsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchDataItemsAsyncPager

```
SearchDataItemsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse
],
],
request: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsRequest,
response: google.cloud.aiplatform_v1.types.dataset_service.SearchDataItemsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesgenerationconfigthinkingconfig_googlecloudaip_4c196e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesgenerationconfigthinkingconfig.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerationConfig.ThinkingConfig -->

# Class ThinkingConfig (1.134.0)

`ThinkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for thinking features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`include_thoughts` |
`bool`
Indicates whether to include thoughts in the response. If true, thoughts are returned only when available. This field is a member of `oneof` _ `_include_thoughts` .
|
`thinking_budget` |
`int`
Optional. Indicates the thinking budget in tokens. This is only applied when enable_thinking is true. This field is a member of `oneof` _ `_thinking_budget` .
|

## Methods

### ThinkingConfig

`ThinkingConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Config for thinking features.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typestunedmodel.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TunedModel -->

# Class TunedModel (1.134.0)

`TunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Model Registry Model and Online Prediction Endpoint associated with this TuningJob.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
Output only. The resource name of the TunedModel. Format: `projects/{project}/locations/{location}/models/{model}@{version_id}`
When tuning from a base model, the version_id will be 1.
For continuous tuning, the version id will be incremented by
1 from the last version id in the parent model. E.g.,
`projects/{project}/locations/{location}/models/{model}@{last_version_id + 1}`
|
`endpoint` |
`str`
Output only. A resource name of an Endpoint. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .
|
`checkpoints` |
`MutableSequence[`
Output only. The checkpoints associated with this TunedModel. This field is only populated for tuning jobs that enable intermediate checkpoints. |

## Methods

### TunedModel

`TunedModel(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Model Registry Model and Online Prediction Endpoint associated with this TuningJob.


---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatformv1schemapredictparams_v1typesvideoactionrecognitionpredi_fc9b5a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformv1schemapredictparams_v1typesvideoactionrecognitionpredic_636192.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformv1schemapredictparams_v1typesvideoactionrecognitionpredict_147aee.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schemapredictparams_v1typesvideoactionrecognitionpredictionparams.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.predict.params_v1.types.VideoActionRecognitionPredictionParams -->

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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesfeatureonlinestoreoptimized_googlecloudaiplat_529d26.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesfeatureonlinestoreoptimized.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureOnlineStore.Optimized -->

# Class Optimized (1.134.0)

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type

## Methods

### Optimized

`Optimized(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Optimized storage type


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformv1schematrainingjobdefinition_v1typesautomltextextractioninputs.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs -->

# Class AutoMlTextExtractionInputs (1.134.0)

`AutoMlTextExtractionInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


API documentation for `aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTextExtractionInputs`

class.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesextension_registry_servicepagerslistextensionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.extension_registry_service.pagers.ListExtensionsPager -->

# Class ListExtensionsPager (1.134.0)

```
ListExtensionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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


A pager for iterating through `list_extensions`

requests.

This class thinly wraps an initial
[ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse) object, and
provides an `__iter__`

method to iterate through its
`extensions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListExtensions`

requests and continue to iterate
through the `extensions`

field on the
corresponding responses.

All the usual [ListExtensionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExtensionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListExtensionsPager

```
ListExtensionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsRequest,
response: google.cloud.aiplatform_v1beta1.types.extension_registry_service.ListExtensionsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistartifactsasyncpa_92d324.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmetadata_servicepagerslistartifactsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.metadata_service.pagers.ListArtifactsAsyncPager -->

# Class ListArtifactsAsyncPager (1.134.0)

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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
[ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse) object, and
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

All the usual [ListArtifactsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListArtifactsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListArtifactsAsyncPager

```
ListArtifactsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsRequest,
response: google.cloud.aiplatform_v1beta1.types.metadata_service.ListArtifactsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesschedule_servicepagerslistschedulesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.schedule_service.pagers.ListSchedulesAsyncPager -->

# Class ListSchedulesAsyncPager (1.134.0)

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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
[ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse) object, and
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

All the usual [ListSchedulesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSchedulesAsyncPager

```
ListSchedulesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesRequest,
response: google.cloud.aiplatform_v1beta1.types.schedule_service.ListSchedulesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformmatchingengineindexendpoint.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.MatchingEngineIndexEndpoint -->

# Class MatchingEngineIndexEndpoint (1.134.0)

```
MatchingEngineIndexEndpoint(
index_endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Matching Engine index endpoint resource for Vertex AI.

## Properties

### create_time

Time this resource was created.

### deployed_indexes

Returns a list of deployed indexes on this endpoint.

### description

Description of the index endpoint.

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

### name

Name of this resource.

### private_service_access_network

"Private service access network.

### private_service_connect_ip_address

"Private service connect ip address.

### public_endpoint_domain_name

Public endpoint DNS name.

### resource_name

Full qualified resource name.

### update_time

Time this resource was last updated.

## Methods

### MatchingEngineIndexEndpoint

```
MatchingEngineIndexEndpoint(
index_endpoint_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Retrieves an existing index endpoint given a name or ID.

Example Usage:

```
my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
index_endpoint_name='projects/123/locations/us-central1/index_endpoint/my_index_id'
)
or
my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
index_endpoint_name='my_index_endpoint_id'
)
```


Parameters |
|
|---|---|
Name |
Description |
`index_endpoint_name` |
`str`
Required. A fully-qualified index endpoint resource name or a index ID. Example: "projects/123/locations/us-central1/index_endpoints/my_index_id" or "my_index_id" when project and location are initialized or passed. |
`project` |
`str`
Optional. Project to retrieve index endpoint from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve index endpoint from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve this IndexEndpoint. Overrides credentials set in aiplatform.init. |

### create

```
create(
display_name: str,
network: typing.Optional[str] = None,
public_endpoint_enabled: bool = False,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
enable_private_service_connect: bool = False,
project_allowlist: typing.Optional[typing.Sequence[str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
create_request_timeout: typing.Optional[float] = None,
) -> (
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchingEngineIndexEndpoint
)
```


Creates a MatchingEngineIndexEndpoint resource.

Example Usage:

```
my_index_endpoint = aiplatform.IndexEndpoint.create(
display_name='my_endpoint',
)
```


Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The display name of the IndexEndpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`network` |
`str`
Optional. The full name of the Google Compute Engine |
`public_endpoint_enabled` |
`bool`
Optional. If true, the deployed index will be accessible through public endpoint. |
`description` |
`str`
Optional. The description of the IndexEndpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your IndexEndpoint. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`project` |
`str`
Optional. Project to create IndexEndpoint in. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to create IndexEndpoint in. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to create IndexEndpoints. Overrides credentials set in aiplatform.init. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`sync` |
`bool`
Optional. Whether to execute this creation synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_private_service_connect` |
`bool`
If true, expose the index endpoint via private service connect. |
`project_allowlist` |
`Sequence[str]`
Optional. List of projects from which the forwarding rule will target the service attachment. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the index endpoint. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
A network must be instantiated when creating a IndexEndpoint. |

### delete

`delete(force: bool = False, sync: bool = True) -> None`


Deletes this MatchingEngineIndexEndpoint resource. If force is set to True, all indexes on this endpoint will be undeployed prior to deletion.

Parameters |
|
|---|---|
Name |
Description |
`force` |
`bool`
Required. If force is set to True, all deployed indexes on this endpoint will be undeployed first. Default is False. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`FailedPrecondition` |
If indexes are deployed on this MatchingEngineIndexEndpoint and force = False. |

### deploy_index

```
deploy_index(
index: google.cloud.aiplatform.matching_engine.matching_engine_index.MatchingEngineIndex,
deployed_index_id: str,
display_name: typing.Optional[str] = None,
machine_type: typing.Optional[str] = None,
min_replica_count: typing.Optional[int] = None,
max_replica_count: typing.Optional[int] = None,
enable_access_logging: typing.Optional[bool] = None,
reserved_ip_ranges: typing.Optional[typing.Sequence[str]] = None,
deployment_group: typing.Optional[str] = None,
auth_config_audiences: typing.Optional[typing.Sequence[str]] = None,
auth_config_allowed_issuers: typing.Optional[typing.Sequence[str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
sync: bool = True,
deploy_request_timeout: typing.Optional[float] = None,
psc_automation_configs: typing.Optional[
typing.Sequence[typing.Tuple[str, str]]
] = None,
deployment_tier: typing.Optional[str] = None,
) -> (
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchingEngineIndexEndpoint
)
```


Deploys an existing index resource to this endpoint resource.

Parameters |
|
|---|---|
Name |
Description |
`index` |
`MatchingEngineIndex`
Required. The Index this is the deployment of. We may refer to this Index as the DeployedIndex's "original" Index. |
`deployed_index_id` |
`str`
Required. The user specified ID of the DeployedIndex. The ID can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The ID must be unique within the project it is created in. |
`display_name` |
`str`
The display name of the DeployedIndex. If not provided upon creation, the Index's display_name is used. |
`machine_type` |
`str`
Optional. The type of machine. Not specifying machine type will result in model to be deployed with automatic resources. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. If this value is not provided, the value of 2 will be used. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the larger value of min_replica_count or 2 will be used. If value provided is smaller than min_replica_count, it will automatically be increased to be min_replica_count. |
`enable_access_logging` |
`bool`
Optional. If true, private endpoint's access logs are sent to StackDriver Logging. These logs are like standard server access logs, containing information like timestamp and latency for each MatchRequest. Note that Stackdriver logs may incur a cost, especially if the deployed index receives a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`reserved_ip_ranges` |
`Sequence[str]`
Optional. A list of reserved ip ranges under the VPC network that can be used for this DeployedIndex. If set, we will deploy the index within the provided ip ranges. Otherwise, the index might be deployed to any ip ranges under the provided VPC network. The value sohuld be the name of the address ( |
`deployment_group` |
`str`
Optional. The deployment group can be no longer than 64 characters (eg: 'test', 'prod'). If not set, we will use the 'default' deployment group. Creating |
`auth_config_audiences` |
`Sequence[str]`
The list of JWT |
`auth_config_allowed_issuers` |
`Sequence[str]`
A list of allowed JWT issuers. Each entry must be a valid Google service account, in the following format: |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in a concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`deploy_request_timeout` |
`float`
Optional. The timeout for the request in seconds. |
`psc_automation_configs` |
`Sequence[Tuple[str, str]]`
Optional. A list of (project_id, network) pairs for Private Service Connection endpoints to be setup for the deployed index. The project_id is the project number of the project that the network is in, and network is the name of the network. Network is the full name of the Google Compute Engine |
`deployment_tier` |
`str`
Optional. The deployment tier that the index is deployed to. |

### find_neighbors

```
find_neighbors(
*,
deployed_index_id: str,
queries: typing.Optional[
typing.Union[
typing.List[typing.List[float]],
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.HybridQuery
],
]
] = None,
num_neighbors: int = 10,
filter: typing.Optional[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.Namespace
]
] = None,
per_crowding_attribute_neighbor_count: typing.Optional[int] = None,
approx_num_neighbors: typing.Optional[int] = None,
fraction_leaf_nodes_to_search_override: typing.Optional[float] = None,
return_full_datapoint: bool = False,
numeric_filter: typing.Optional[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.NumericNamespace
]
] = None,
embedding_ids: typing.Optional[typing.List[str]] = None,
signed_jwt: typing.Optional[str] = None,
psc_network: typing.Optional[str] = None
) -> typing.List[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchNeighbor
]
]
```


Retrieves nearest neighbors for the given embedding queries on the specified deployed index which is deployed to either public or private endpoint.

```
Example usage:
my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
index_endpoint_name='projects/123/locations/us-central1/index_endpoint/my_index_endpoint_id'
)
my_index_endpoint.find_neighbors(deployed_index_id="deployed_index_id", queries= [[1, 1]],)
```


Parameters |
|
|---|---|
Name |
Description |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to match the queries against. |
`queries` |
`Union[List[List[float]], List[HybridQuery]]`
Optional. A list of queries. For regular dense-only queries, each query is a list of floats, representing a single embedding. For hybrid queries, each query is a hybrid query of type aiplatform.matching_engine.matching_engine_index_endpoint.HybridQuery. |
`num_neighbors` |
`int`
Required. The number of nearest neighbors to be retrieved from database for each query. |
`filter` |
`List[Namespace]`
Optional. A list of Namespaces for filtering the matching results. For example, [Namespace("color", ["red"], []), Namespace("shape", [], ["squared"])] will match datapoints that satisfy "red color" but not include datapoints with "squared shape". Please refer to |
`per_crowding_attribute_neighbor_count` |
`int`
Optional. Crowding is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute. It's used for improving result diversity. This field is the maximum number of matches with the same crowding tag. |
`approx_num_neighbors` |
`int`
Optional. The number of neighbors to find via approximate search before exact reordering is performed. If not set, the default value from scam config is used; if set, this value must be > 0. |
`fraction_leaf_nodes_to_search_override` |
`float`
Optional. The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. |
`return_full_datapoint` |
`bool`
Optional. If set to true, the full datapoints (including all vector values and of the nearest neighbors are returned. Note that returning full datapoint will significantly increase the latency and cost of the query. |
`numeric_filter` |
`List[NumericNamespace]`
Optional. A list of NumericNamespaces for filtering the matching results. For example: [NumericNamespace(name="cost", value_int=5, op="GREATER")] will match datapoints that its cost is greater than 5. |
`embedding_ids` |
`str`
Optional. If |
`signed_jwt` |
`str`
Optional. A signed JWT for accessing the private endpoint. |
`psc_network` |
`Optional[str]`
Optional. Required for private service automation enabled deployed index. This network is the PSC network the match query is executed in. This (project, network) pair must already be specified for psc automation when the index is deployed. The format is |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
parent: typing.Optional[str] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Vertex AI Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

aiplatform.Model.list(order_by="create_time desc, display_name")

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
`parent` |
`str`
Optional. The parent resource name if any to retrieve list from. |

### match

```
match(
deployed_index_id: str,
queries: typing.Optional[
typing.Union[
typing.List[typing.List[float]],
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.HybridQuery
],
]
] = None,
num_neighbors: int = 1,
filter: typing.Optional[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.Namespace
]
] = None,
per_crowding_attribute_num_neighbors: typing.Optional[int] = None,
approx_num_neighbors: typing.Optional[int] = None,
fraction_leaf_nodes_to_search_override: typing.Optional[float] = None,
low_level_batch_size: int = 0,
numeric_filter: typing.Optional[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.NumericNamespace
]
] = None,
signed_jwt: typing.Optional[str] = None,
psc_network: typing.Optional[str] = None,
) -> typing.List[
typing.List[
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchNeighbor
]
]
```


Retrieves nearest neighbors for the given embedding queries on the specified deployed index for private endpoint only.

Parameters |
|
|---|---|
Name |
Description |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to match the queries against. |
`queries` |
`Union[List[List[float]], List[HybridQuery]]`
Optional. A list of queries. For regular dense-only queries, each query is a list of floats, representing a single embedding. For hybrid queries, each query is a hybrid query of type aiplatform.matching_engine.matching_engine_index_endpoint.HybridQuery. |
`num_neighbors` |
`int`
Required. The number of nearest neighbors to be retrieved from database for each query. |
`filter` |
`List[Namespace]`
Optional. A list of Namespaces for filtering the matching results. For example, [Namespace("color", ["red"], []), Namespace("shape", [], ["squared"])] will match datapoints that satisfy "red color" but not include datapoints with "squared shape". Please refer to |
`per_crowding_attribute_num_neighbors` |
`int`
Optional. Crowding is a constraint on a neighbor list produced by nearest neighbor search requiring that no more than some value k' of the k neighbors returned have the same value of crowding_attribute. It's used for improving result diversity. This field is the maximum number of matches with the same crowding tag. |
`approx_num_neighbors` |
`int`
The number of neighbors to find via approximate search before exact reordering is performed. If not set, the default value from scam config is used; if set, this value must be > 0. |
`fraction_leaf_nodes_to_search_override` |
`float`
Optional. The fraction of the number of leaves to search, set at query time allows user to tune search performance. This value increase result in both search accuracy and latency increase. The value should be between 0.0 and 1.0. |
`low_level_batch_size` |
`int`
Optional. Selects the optimal batch size to use for low-level batching. Queries within each low level batch are executed sequentially while low level batches are executed in parallel. This field is optional, defaults to 0 if not set. A non-positive number disables low level batching, i.e. all queries are executed sequentially. |
`numeric_filter` |
`Optional[list[NumericNamespace]]`
Optional. A list of NumericNamespaces for filtering the matching results. For example: [NumericNamespace(name="cost", value_int=5, op="GREATER")] will match datapoints that its cost is greater than 5. |
`signed_jwt` |
`str`
Optional. A signed JWT for accessing the private endpoint. |
`psc_network` |
`Optional[str]`
Optional. Required for private service automation enabled deployed index. This network is the PSC network the match query is executed in. This (project, network) pair must already be specified for psc automation when the index is deployed. The format is |

### mutate_deployed_index

```
mutate_deployed_index(
deployed_index_id: str,
min_replica_count: int = 1,
max_replica_count: int = 1,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
mutate_request_timeout: typing.Optional[float] = None,
)
```


Updates an existing deployed index under this endpoint resource.

Parameters |
|
|---|---|
Name |
Description |
`index_id` |
`str`
Required. The ID of the MatchingEnginIndex associated with the DeployedIndex. |
`deployed_index_id` |
`str`
Required. The user specified ID of the DeployedIndex. The ID can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The ID must be unique within the project it is created in. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the larger value of min_replica_count or 1 will be used. If value provided is smaller than min_replica_count, it will automatically be increased to be min_replica_count. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`timeout` |
`float`
Optional. The timeout for the request in seconds. |

### read_index_datapoints

```
read_index_datapoints(
*,
deployed_index_id: str,
ids: typing.List[str] = [],
signed_jwt: typing.Optional[str] = None,
psc_network: typing.Optional[str] = None
) -> typing.List[google.cloud.aiplatform_v1beta1.types.index.IndexDatapoint]
```


Reads the datapoints/vectors of the given IDs on the specified deployed index which is deployed to public or private endpoint.

```
Example Usage:
my_index_endpoint = aiplatform.MatchingEngineIndexEndpoint(
index_endpoint_name='projects/123/locations/us-central1/index_endpoint/my_index_id'
)
my_index_endpoint.read_index_datapoints(deployed_index_id="public_test1", ids= ["606431", "896688"],)
```


Parameters |
|
|---|---|
Name |
Description |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to match the queries against. |
`ids` |
`List[str]`
Required. IDs of the datapoints to be searched for. |
`signed_jwt` |
`str`
Optional. A signed JWT for accessing the private endpoint. |
`psc_network` |
`Optional[str]`
Optional. Required for private service automation enabled deployed index. This network is the PSC network the match query is executed in. This (project, network) pair must already be specified for psc automation when the index is deployed. The format is |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### undeploy_all

```
undeploy_all(
sync: bool = True,
) -> (
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchingEngineIndexEndpoint
)
```


Undeploys every index deployed to this MatchingEngineIndexEndpoint.

Parameter |
|
|---|---|
Name |
Description |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

### undeploy_index

```
undeploy_index(
deployed_index_id: str,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
undeploy_request_timeout: typing.Optional[float] = None,
) -> (
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchingEngineIndexEndpoint
)
```


Undeploy a deployed index endpoint resource.

Parameters |
|
|---|---|
Name |
Description |
`deployed_index_id` |
`str`
Required. The ID of the DeployedIndex to be undeployed from the IndexEndpoint. |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`undeploy_request_timeout` |
`float`
Optional. The timeout for the request in seconds. |

### update

```
update(
display_name: str,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
request_metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
update_request_timeout: typing.Optional[float] = None,
) -> (
google.cloud.aiplatform.matching_engine.matching_engine_index_endpoint.MatchingEngineIndexEndpoint
)
```


Updates an existing index endpoint resource.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Required. The display name of the IndexEndpoint. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
Optional. The description of the IndexEndpoint. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Indexs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`request_metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`update_request_timeout` |
`float`
Optional. The timeout for the request in seconds. |

### wait

`wait()`


Helper method that blocks until all futures are complete.


---

<!-- DOCUMENTO FUSIONADO: _____googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasy_5f433c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasyn_f317e4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasync_33935b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasyncp_22928d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasyncpa_b88878.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesendpoint_servicepagerslistendpointsasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.endpoint_service.pagers.ListEndpointsAsyncPager -->

# Class ListEndpointsAsyncPager (1.134.0)

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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
[ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse) object, and
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

All the usual [ListEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListEndpointsAsyncPager

```
ListEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.endpoint_service.ListEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesindex_endpoint_servicepagerslistindexendpointspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.index_endpoint_service.pagers.ListIndexEndpointsPager -->

# Class ListIndexEndpointsPager (1.134.0)

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsPager

```
ListIndexEndpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
],
request: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1.types.index_endpoint_service.ListIndexEndpointsResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1servicesfeaturestore_servicepagerssearchfeaturesasyncpa_dac4ff.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesfeaturestore_servicepagerssearchfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.featurestore_service.pagers.SearchFeaturesAsyncPager -->

# Class SearchFeaturesAsyncPager (1.134.0)

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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


A pager for iterating through `search_features`

requests.

This class thinly wraps an initial
[SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse) object, and
provides an `__aiter__`

method to iterate through its
`features`

field.

If there are more pages, the `__aiter__`

method will make additional
`SearchFeatures`

requests and continue to iterate
through the `features`

field on the
corresponding responses.

All the usual [SearchFeaturesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchFeaturesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchFeaturesAsyncPager

```
SearchFeaturesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse
],
],
request: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesRequest,
response: google.cloud.aiplatform_v1.types.featurestore_service.SearchFeaturesResponse,
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

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesragchunk_googlecloudaiplatform_v1beta1typescreatec_1d7fe9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesragchunk.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RagChunk -->

# Class RagChunk (1.134.0)

`RagChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`text` |
`str`
The content of the chunk. |
`page_span` |
If populated, represents where the chunk starts and ends in the document. This field is a member of `oneof` _ `_page_span` .
|

## Classes

### PageSpan

`PageSpan(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents where the chunk starts and ends in the document.

## Methods

### RagChunk

`RagChunk(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typescreatecontextrequest.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateContextRequest -->

# Class CreateContextRequest (1.134.0)

`CreateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateContext.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the MetadataStore where the Context should be created. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`
|
`context` |
Required. The Context to create. |
`context_id` |
`str`
The {context} portion of the resource name with the format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/contexts/{context}` .
If not provided, the Context's ID will be a UUID generated
by the service. Must be 4-128 characters in length. Valid
characters are `/` a-z][0-9]`-/` . Must be unique across all
Contexts in the parent MetadataStore. (Otherwise the request
will fail with ALREADY_EXISTS, or PERMISSION_DENIED if the
caller can't view the preexisting Context.)
|

## Methods

### CreateContextRequest

`CreateContextRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.CreateContext.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1typesmodeldeploymentmonitoringjob__googlecloudaiplatfor_de383b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesmodeldeploymentmonitoringjob.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ModelDeploymentMonitoringJob -->

# Class ModelDeploymentMonitoringJob (1.134.0)

```
ModelDeploymentMonitoringJob(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Resource name of a ModelDeploymentMonitoringJob. |
`display_name` |
`str`
Required. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`endpoint` |
`str`
Required. Endpoint resource name. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`state` |
Output only. The detailed state of the monitoring job. When the job is still creating, the state will be 'PENDING'. Once the job is successfully created, the state will be 'RUNNING'. Pause the job, the state will be 'PAUSED'. Resume the job, the state will return to 'RUNNING'. |
`schedule_state` |
Output only. Schedule state when the monitoring job is in Running state. |
`latest_monitoring_pipeline_metadata` |
Output only. Latest triggered monitoring pipeline metadata. |
`model_deployment_monitoring_objective_configs` |
`MutableSequence[`
Required. The config for monitoring objectives. This is a per DeployedModel config. Each DeployedModel needs to be configured separately. |
`model_deployment_monitoring_schedule_config` |
Required. Schedule config for running the monitoring job. |
`logging_sampling_strategy` |
Required. Sample Strategy for logging. |
`model_monitoring_alert_config` |
Alert config for model monitoring. |
`predict_instance_schema_uri` |
`str`
YAML schema file uri describing the format of a single instance, which are given to format this Endpoint's prediction (and explanation). If not set, we will generate predict schema from collected predict requests. |
`sample_predict_instance` |
`google.protobuf.struct_pb2.Value`
Sample Predict instance, same format as PredictRequest.instances, this can be set as a replacement of ModelDeploymentMonitoringJob.predict_instance_schema_uri. If not set, we will generate predict schema from collected predict requests. |
`analysis_instance_schema_uri` |
`str`
YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format(data type) as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`bigquery_tables` |
`MutableSequence[`
Output only. The created bigquery tables for the job under customer project. Customer could do their own query & analysis. There could be 4 log tables in maximum: 1. Training data logging predict request/response 2. Serving data logging predict request/response |
`log_ttl` |
`google.protobuf.duration_pb2.Duration`
The TTL of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See https://goo.gl/xmQnxf for more information and examples of labels. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelDeploymentMonitoringJob was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this ModelDeploymentMonitoringJob was updated most recently. |
`next_schedule_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this monitoring pipeline will be scheduled to run for the next round. |
`stats_anomalies_base_directory` |
Stats anomalies base folder path. |
`encryption_spec` |
Customer-managed encryption key spec for a ModelDeploymentMonitoringJob. If set, this ModelDeploymentMonitoringJob and all sub-resources of this ModelDeploymentMonitoringJob will be secured by this key. |
`enable_monitoring_pipeline_logs` |
`bool`
If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to `Cloud Logging pricing |
`error` |
`google.rpc.status_pb2.Status`
Output only. Only populated when the job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .
|
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

### LatestMonitoringPipelineMetadata

```
LatestMonitoringPipelineMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


All metadata of most recent monitoring pipelines.

### MonitoringScheduleState

`MonitoringScheduleState(value)`


The state to Specify the monitoring pipeline.

## Methods

### ModelDeploymentMonitoringJob

```
ModelDeploymentMonitoringJob(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Represents a job that runs periodically to monitor the deployed models in an endpoint. It will analyze the logged training & prediction data to detect any abnormal behaviors.


---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesjob_servicepagerslistdatalabelingjobspager_484391.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesjob_servicepagerslistdatalabelingjobspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListDataLabelingJobsPager -->

# Class ListDataLabelingJobsPager (1.134.0)

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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
[ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse) object, and
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

All the usual [ListDataLabelingJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDataLabelingJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDataLabelingJobsPager

```
ListDataLabelingJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListDataLabelingJobsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturestorespager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturestoresPager -->

# Class ListFeaturestoresPager (1.134.0)

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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


A pager for iterating through `list_featurestores`

requests.

This class thinly wraps an initial
[ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse) object, and
provides an `__iter__`

method to iterate through its
`featurestores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeaturestores`

requests and continue to iterate
through the `featurestores`

field on the
corresponding responses.

All the usual [ListFeaturestoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeaturestoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeaturestoresPager

```
ListFeaturestoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
],
request: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresRequest,
response: google.cloud.aiplatform_v1beta1.types.featurestore_service.ListFeaturestoresResponse,
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

<!-- DOCUMENTO FUSIONADO: ____googlecloudaiplatform_v1beta1typesrecommendspecresponse_googlecloudaiplatfor_b75d7b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudaiplatform_v1beta1typesrecommendspecresponse_googlecloudaiplatform_9c5190.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1typesrecommendspecresponse_googlecloudaiplatform__7484b4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1typesrecommendspecresponse_googlecloudaiplatform_v_a4d81a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrecommendspecresponse.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RecommendSpecResponse -->

# Class RecommendSpecResponse (1.134.0)

`RecommendSpecResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.RecommendSpec.

## Attributes |
|
|---|---|
Name |
Description |
`base_model` |
`str`
Output only. The base model used to finetune the custom model. |
`recommendations` |
`MutableSequence[`
Output only. Recommendations of deployment options for the given custom weights model. |
`specs` |
`MutableSequence[`
Output only. The machine and model container specs. |

## Classes

### MachineAndModelContainerSpec

```
MachineAndModelContainerSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


A machine and model container spec.

### Recommendation

`Recommendation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Recommendation of one deployment option for the given custom weights model in one region. Contains the machine and container spec, and user accelerator quota state.

## Methods

### RecommendSpecResponse

`RecommendSpecResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ModelService.RecommendSpec.


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesrubricbasedinstructionfollowingresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RubricBasedInstructionFollowingResult -->

# Class RubricBasedInstructionFollowingResult (1.134.0)

```
RubricBasedInstructionFollowingResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Result for RubricBasedInstructionFollowing metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Overall score for the instruction following. This field is a member of `oneof` _ `_score` .
|
`rubric_critique_results` |
`MutableSequence[`
Output only. List of per rubric critique results. |

## Methods

### RubricBasedInstructionFollowingResult

```
RubricBasedInstructionFollowingResult(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Result for RubricBasedInstructionFollowing metric.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesfeaturestore_servicepagerslistfeaturesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.featurestore_service.pagers.ListFeaturesAsyncPager -->

# Class ListFeaturesAsyncPager (1.134.0)

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

## Methods

### ListFeaturesAsyncPager

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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1typesdeployedindex.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployedIndex -->

# Class DeployedIndex (1.134.0)

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.

## Attributes |
|
|---|---|
Name |
Description |
`id` |
`str`
Required. The user specified ID of the DeployedIndex. The ID can be up to 128 characters long and must start with a letter and only contain letters, numbers, and underscores. The ID must be unique within the project it is created in. |
`index` |
`str`
Required. The name of the Index this is the deployment of. We may refer to this Index as the DeployedIndex's "original" Index. |
`display_name` |
`str`
The display name of the DeployedIndex. If not provided upon creation, the Index's display_name is used. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the DeployedIndex was created. |
`private_endpoints` |
Output only. Provides paths for users to send requests directly to the deployed index services running on Cloud via private services access. This field is populated if network is configured. |
`index_sync_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. The DeployedIndex may depend on various data on its original Index. Additionally when certain changes to the original Index are being done (e.g. when what the Index contains is being changed) the DeployedIndex may be asynchronously updated in the background to reflect these changes. If this timestamp's value is at least the Index.update_time of the original Index, it means that this DeployedIndex and the original Index are in sync. If this timestamp is older, then to see which updates this DeployedIndex already contains (and which it does not), one must `list][google.longrunning.Operations.ListOperations]` the
operations that are running on the original Index. Only the
successfully completed Operations with
update_time
equal or before this sync time are contained in this
DeployedIndex.
|
`automatic_resources` |
Optional. A description of resources that the DeployedIndex uses, which to large degree are decided by Vertex AI, and optionally allows only a modest additional configuration. If min_replica_count is not set, the default value is 2 (we don't provide SLA when min_replica_count=1). If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. |
`dedicated_resources` |
Optional. A description of resources that are dedicated to the DeployedIndex, and that need a higher degree of manual configuration. The field min_replica_count must be set to a value strictly greater than 0, or else validation will fail. We don't provide SLA when min_replica_count=1. If max_replica_count is not set, the default value is min_replica_count. The max allowed replica count is 1000. Available machine types for SMALL shard: e2-standard-2 and all machine types available for MEDIUM and LARGE shard. Available machine types for MEDIUM shard: e2-standard-16 and all machine types available for LARGE shard. Available machine types for LARGE shard: e2-highmem-16, n2d-standard-32. n1-standard-16 and n1-standard-32 are still available, but we recommend e2-standard-16 and e2-highmem-16 for cost efficiency. |
`enable_access_logging` |
`bool`
Optional. If true, private endpoint's access logs are sent to Cloud Logging. These logs are like standard server access logs, containing information like timestamp and latency for each MatchRequest. Note that logs may incur a cost, especially if the deployed index receives a high queries per second rate (QPS). Estimate your costs before enabling this option. |
`enable_datapoint_upsert_logging` |
`bool`
Optional. If true, logs to Cloud Logging errors relating to datapoint upserts. Under normal operation conditions, these log entries should be very rare. However, if incompatible datapoint updates are being uploaded to an index, a high volume of log entries may be generated in a short period of time. Note that logs may incur a cost, especially if the deployed index receives a high volume of datapoint upserts. Estimate your costs before enabling this option. |
`deployed_index_auth_config` |
Optional. If set, the authentication is enabled for the private endpoint. |
`reserved_ip_ranges` |
`MutableSequence[str]`
Optional. A list of reserved ip ranges under the VPC network that can be used for this DeployedIndex. If set, we will deploy the index within the provided ip ranges. Otherwise, the index might be deployed to any ip ranges under the provided VPC network. The value should be the name of the address (https://cloud.google.com/compute/docs/reference/rest/v1/addresses) Example: ['vertex-ai-ip-range']. For more information about subnets and network IP ranges, please see https://cloud.google.com/vpc/docs/subnets#manually_created_subnet_ip_ranges. |
`deployment_group` |
`str`
Optional. The deployment group can be no longer than 64 characters (eg: 'test', 'prod'). If not set, we will use the 'default' deployment group. Creating `deployment_groups` with `reserved_ip_ranges`
is a recommended practice when the peered network has
multiple peering ranges. This creates your deployments from
predictable IP spaces for easier traffic administration.
Also, one deployment_group (except 'default') can only be
used with the same reserved_ip_ranges which means if the
deployment_group has been used with reserved_ip_ranges: [a,
b, c], using it with [a, b] or [d, e] is disallowed.
Note: we only support up to 5 deployment groups(not
including 'default').
|
`deployment_tier` |
Optional. The deployment tier that the index is deployed to. DEPLOYMENT_TIER_UNSPECIFIED will use a system-chosen default tier. |
`psc_automation_configs` |
`MutableSequence[`
Optional. If set for PSC deployed index, PSC connection will be automatically created after deployment is done and the endpoint information is populated in private_endpoints.psc_automated_endpoints. |

## Classes

### DeploymentTier

`DeploymentTier(value)`


Tiers encapsulate serving time attributes like latency and throughput.

## Methods

### DeployedIndex

`DeployedIndex(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A deployment of an Index. IndexEndpoints contain one or more DeployedIndexes.


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetversionsp_f5758d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetversionspa_ff109b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesdataset_servicepagerslistdatasetversionspager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.dataset_service.pagers.ListDatasetVersionsPager -->

# Class ListDatasetVersionsPager (1.134.0)

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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


A pager for iterating through `list_dataset_versions`

requests.

This class thinly wraps an initial
[ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse) object, and
provides an `__iter__`

method to iterate through its
`dataset_versions`

field.

If there are more pages, the `__iter__`

method will make additional
`ListDatasetVersions`

requests and continue to iterate
through the `dataset_versions`

field on the
corresponding responses.

All the usual [ListDatasetVersionsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetVersionsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListDatasetVersionsPager

```
ListDatasetVersionsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsRequest,
response: google.cloud.aiplatform_v1beta1.types.dataset_service.ListDatasetVersionsResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typesmodelmonitoringinput.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ModelMonitoringInput -->

# Class ModelMonitoringInput (1.134.0)

`ModelMonitoringInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model monitoring data input spec.

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
`columnized_dataset` |
Columnized dataset. This field is a member of `oneof` _ `dataset` .
|
`batch_prediction_output` |
Vertex AI Batch prediction Job. This field is a member of `oneof` _ `dataset` .
|
`vertex_endpoint_logs` |
Vertex AI Endpoint request & response logging. This field is a member of `oneof` _ `dataset` .
|
`time_interval` |
`google.type.interval_pb2.Interval`
The time interval (pair of start_time and end_time) for which results should be returned. This field is a member of `oneof` _ `time_spec` .
|
`time_offset` |
The time offset setting for which results should be returned. This field is a member of `oneof` _ `time_spec` .
|

## Classes

### BatchPredictionOutput

`BatchPredictionOutput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Batch prediction job output.

### ModelMonitoringDataset

`ModelMonitoringDataset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Input dataset spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### TimeOffset

`TimeOffset(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Time offset setting.

### VertexEndpointLogs

`VertexEndpointLogs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Data from Vertex AI Endpoint request response logging.

## Methods

### ModelMonitoringInput

`ModelMonitoringInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Model monitoring data input spec.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: __googlecloudaiplatformpredictiondefaultserializer_googlecloudaiplatform_v1beta1_9b4bfe.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudaiplatformpredictiondefaultserializer_googlecloudaiplatform_v1beta1t_768a31.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatformpredictiondefaultserializer.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.DefaultSerializer -->

# Class DefaultSerializer (1.134.0)

`DefaultSerializer()`


Default serializer for serialization and deserialization for prediction.

## Methods

### deserialize

`deserialize(data: typing.Any, content_type: typing.Optional[str]) -> typing.Any`


Deserializes the request data. Invoked before predict.

Parameters |
|
|---|---|
Name |
Description |
`data` |
`Any`
Required. The request data sent to the application. |
`content_type` |
`str`
Optional. The specified content type of the request. |

Exceptions |
|
|---|---|
Type |
Description |
`HTTPException` |
If Json deserialization failed or the specified content type is not supported. |

### serialize

`serialize(prediction: typing.Any, accept: typing.Optional[str]) -> typing.Any`


Serializes the prediction results. Invoked after predict.

Parameters |
|
|---|---|
Name |
Description |
`prediction` |
`Any`
Required. The generated prediction to be sent back to clients. |
`accept` |
`str`
Optional. The specified content type of the response. |

Exceptions |
|
|---|---|
Type |
Description |
`HTTPException` |
If Json serialization failed or the specified accept is not supported. |


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1typessummarizationqualityresult.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SummarizationQualityResult -->

# Class SummarizationQualityResult (1.134.0)

`SummarizationQualityResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`score` |
`float`
Output only. Summarization Quality score. This field is a member of `oneof` _ `_score` .
|
`explanation` |
`str`
Output only. Explanation for summarization quality score. |
`confidence` |
`float`
Output only. Confidence for summarization quality score. This field is a member of `oneof` _ `_confidence` .
|

## Methods

### SummarizationQualityResult

`SummarizationQualityResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Spec for summarization quality result.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)


---

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1beta1servicesmemory_bank_servicepagerslistmemoriesasyncpager.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.memory_bank_service.pagers.ListMemoriesAsyncPager -->

# Class ListMemoriesAsyncPager (1.134.0)

```
ListMemoriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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


A pager for iterating through `list_memories`

requests.

This class thinly wraps an initial
[ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse) object, and
provides an `__aiter__`

method to iterate through its
`memories`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListMemories`

requests and continue to iterate
through the `memories`

field on the
corresponding responses.

All the usual [ListMemoriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListMemoriesAsyncPager

```
ListMemoriesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesRequest,
response: google.cloud.aiplatform_v1beta1.types.memory_bank_service.ListMemoriesResponse,
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

<!-- DOCUMENTO FUSIONADO: googlecloudaiplatform_v1servicesendpoint_serviceendpointserviceasyncclient.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.endpoint_service.EndpointServiceAsyncClient -->

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
